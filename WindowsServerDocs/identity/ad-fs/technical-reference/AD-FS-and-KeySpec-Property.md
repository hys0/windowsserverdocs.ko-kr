---
title: "Active Directory Federation Services 및 인증서 키 사양 속성 정보"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: db58fcce054f34c4b0a3f6725456badae9fd0468
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>ADFS 및 인증서 KeySpec 속성 정보
키 사양 ("KeySpec") 인증서 및 키와 관련 된 재산입니다. 로그인, 암호화 또는 둘 다에 대 한 인증서를와 관련 된 개인 키를 사용할 수 있는지 여부를 지정 합니다.   

잘못 된 KeySpec 값 ADFS 및 웹 응용 프로그램 프록시 오류와 같은 발생할 수 있습니다.


- 연결할 SSL/TLS ADFS 또는 웹 응용 프로그램 프록시 (하지만 SChannel 36888 및 36874 이벤트를 기록) 기록 없이 ADFS 이벤트와 함께 실패
- ADFS 또는 WAP 로그인 하지 않으면 페이지에 표시 된 오류 메시지 없이 기반된 인증 페이지를 구성 합니다.

이벤트 로그에서 다음을 볼 수 있습니다.

    Log Name:      AD FS Tracing/Debug
    Source:        AD FS Tracing
    Date:          2/12/2015 9:03:08 AM
    Event ID:      67
    Task Category: None
    Level:         Error
    Keywords:      ADFSProtocol
    User:          S-1-5-21-3723329422-3858836549-556620232-1580884
    Computer:      ADFS1.contoso.com
    Description:
    Ignore corrupted SSO cookie.

## <a name="what-causes-the-problem"></a>문제를 일으키는 항목
KeySpec 속성 키를 생성 하거나 검색 하 여 Microsoft CryptoAPI (CAPI)에서 Microsoft 레거시 저장소 공급자 CSP (암호화)를 사용할 수 있는 방법을 확인 합니다.

KeySpec 값 **1**, 또는 **AT_KEYEXCHANGE**, 서명 및 암호화를 사용할 수 있습니다.  값 **2**, 또는 **AT_SIGNATURE**에 로그인 하는 데만 사용 됩니다.

가장 일반적인 KeySpec 잘못 구성 2를 사용 하 여 토큰 서명 인증서 이외의 인증서에 대 한입니다.  

공급자 Cryptography Next Generation (CNG)를 사용 하 여 키를 생성 된 인증서를에 대 한 주요 사양의 개념이 이며 KeySpec 값 항상 0 됩니다.

아래의 유효한 KeySpec 값을 확인 하는 방법을 확인 합니다. 

### <a name="example"></a>예제
레거시 CSP의 예로 Microsoft 향상 암호화 공급자 있습니다. 

Microsoft RSA CSP 주요 물방울 형식 하거나 알고리즘 식별자를 포함 **CALG_RSA_KEYX** 또는 **CALG_RSA_SIGN**각각 서비스 요청 중 하나에 * * AT_KEYEXCHANGE * * 또는 **AT_SIGNATURE** 키.
  
다음과 같이 RSA 키 알고리즘 식별자 KeySpec 값으로 지도

| 지원 되는 공급자 알고리즘| 키의 사양이 값 CAPI 통화 |
| --- | --- |
|로그인 및 암호를 해독 사용할 수 있는 CALG_RSA_KEYX: RSA 키| AT_KEYEXCHANGE (또는 KeySpec 1 대당)|
중요: CALG_RSA_SIGN RSA 서명 |AT_SIGNATURE (또는 KeySpec 2 =)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec 값과 관련 된 의미
다음은 다양 한 KeySpec 값 의미입니다.

|Keyspec 값|의미|권장 되는 ADFS 사용|
| --- | --- | --- |
|0|인증서가 CNG 인증서|SSL 인증서만|
|1|레거시 CAPI (비 CNG) 인증서를에 대 한 키 서명 및 암호를 해독에 사용할 수 있는|    토큰 서명 토큰 암호를 해독 서비스 통신 인증서 SSL|
|2|레거시 CAPI (비 CNG) 인증서를에 대 한 키에 사용할 수만 로그인|권장 하지 않음|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>인증서에 대 한 KeySpec 값을 확인 하는 방법을 / 키
사용할 수 있는 인증서 값을 확인 하 고 **certutil** 명령줄 도구입니다.  

다음은 예: **certutil – v-저장 내**합니다.  이 화면에 인증서 정보를 덤프 합니다.

![Keyspec 인증서](media/AD-FS-and-KeySpec-Property/keyspec1.png)

CERT_KEY_PROV_INFO_PROP_ID 찾고 두 가지 아래에서


1. **ProviderType:** 인증서를 레거시 저장소 공급자 CSP (암호화)를 사용 하 여 속하는지 키 저장소 공급자의 최신 인증서 CNG (차세대) Api를 기반으로이 있습니다.  모든 0이 아닌 값 레거시 공급자를 나타냅니다.
2.  **KeySpec:** 다음 ADFS 인증서에 대 한 올바른 KeySpec 값은 다음과 같습니다.

    레거시 CSP 공급자 (ProviderType 0 일치 하지 않는 경우).
    
    |광고 FS 인증서 목적|유효한 KeySpec 값|
    | --- | --- |
    |서비스 통신|1|
    |토큰 암호를 해독|1|
    |토큰 서명|1과 2|
    |SSL|1|

    CNG 공급자 (ProviderType 0):
    |광고 FS 인증서 목적|유효한 KeySpec 값|
    | --- | --- |   
    |SSL|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>인증서에 대 한 keyspec 지원 되는 값을 변경 하는 방법
KeySpec 값 변경 다시 생성 하거나 다시 인증 기관에서 발급 된 인증서가 필요 하지 않습니다.  전체 인증서 및 PFX 파일에서 개인 키 다음 단계에 따라 인증서 스토어에 다시 가져올는 KeySpec 변경할 수 있습니다.


1. 먼저 확인 하 고 자녀가 될 수 있도록 다시 구성 필요 하면 다시 가져올 후에 기존 인증서 개인 주요 사용 권한 녹화 합니다.
2. 개인 키 PFX 파일을 포함 하 여 인증서를 내보냅니다.
3. 각 ADFS 및 WAP 서버에 대 한 다음 단계를 수행 합니다.
    1. 인증서 삭제 (의 Adfs의 / WAP 서버)
    2. 관리자 PowerShell 명령 프롬프트를 열고 각 ADFS 및 WAP 서버 cmdlet 구문을 아래 사용 하 여 지정 하 고 AT_KEYEXCHANGE 값 (모든 ADFS 인증서 목적을 위해 작동), PFX 파일.
        1. C:\ > certutil – importpfx certfile.pfx AT_KEYEXCHANGE
        2. PFX 암호를 입력 합니다.
    3. 위의 완료 되 면 다음을 수행합니다
        1. 개인 주요 사용 권한을 확인합니다
        2. adfs 또는 wap 서비스를 다시 시작





