---
title: Active Directory Federation Services 및 인증서 키 사양 속성 정보
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32b0d08f678e9e612bb0ce9cc38d254564bd9b2f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444094"
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>AD FS 및 인증서 KeySpec 속성 정보
키 사양 ("KeySpec")에 인증서 및 키와 연결 된 속성입니다. 서명, 암호화 또는 둘 다에 대 한 인증서와 연결 된 개인 키를 사용할 수 있는지 여부를 지정 합니다.   

잘못 된 KeySpec 값에는 같은 AD FS 및 웹 응용 프로그램 프록시 오류가 발생할 수 있습니다.


- (하지만 36888 및 36874 SChannel 이벤트를 기록 될 수 있습니다)를 기록 된 이벤트는 AD FS 사용 하 여 AD FS 또는 웹 응용 프로그램 프록시에 SSL/TLS 연결을 설정 하지 못함
- WAP를 AD FS에 로그인 하지 못했습니다 페이지에 표시 된 오류 메시지 없이 기반된 인증 페이지를 형성 합니다.

다음 이벤트 로그에 나타날 수 있습니다.

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

## <a name="what-causes-the-problem"></a>문제 원인
KeySpec 속성 키를 생성 하거나 검색 하 여 Microsoft CryptoAPI (CAPI)에서 Microsoft 레거시 저장소 공급자 (CSP 암호화)를 사용할 수 있는 방법을 식별 합니다.

KeySpec 값 **1**, 또는 **AT_KEYEXCHANGE**, 서명 및 암호화에 사용할 수 있습니다.  값이 **2**, 또는 **AT_SIGNATURE**, 로그인에 사용 됩니다.

가장 일반적인 KeySpec 잘못 된 구성 값이 2 사용 하 여 토큰 서명 인증서 이외의 인증서 됩니다.  

키 생성 CNG (Cryptography Next) 공급자를 사용 하 여 생성 된 인증서에 대 한 키 사양에 대 한 개념이 없습니다 되며 KeySpec 값은 항상 0이 됩니다.

아래 유효한 KeySpec 값을 확인 하는 방법을 참조 하세요. 

### <a name="example"></a>예제
기존 CSP의 예로 Microsoft Enhanced Cryptographic Provider입니다. 

Microsoft RSA CSP 키 blob 형식을 하거나 알고리즘 식별자를 포함 **CALG_RSA_KEYX** 하거나 **CALG_RSA_SIGN**각각에 대 한 서비스 요청에 <strong>AT_KEYEXCHANGE * * 또는 * * AT_ 서명</strong> 키입니다.

다음과 같이 KeySpec 값에 매핑되는 RSA 키 알고리즘 식별자

| 알고리즘 공급자 지원| CAPI 호출에 대 한 키 지정 값 |
| --- | --- |
|CALG_RSA_KEYX : 서명 및 암호 해독에 사용할 수 있는 RSA 키| AT_KEYEXCHANGE (또는 KeySpec = 1)|
CALG_RSA_SIGN : RSA 서명 전용 키 |AT_SIGNATURE (또는 KeySpec = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec 값과 연결 된 의미
다음은 다양 한 KeySpec 값의 의미입니다.

|Keyspec 값|의미|권장 되는 AD FS 사용|
| --- | --- | --- |
|0|인증서에 CNG 인증서가|SSL 인증서만|
|1|레거시 CAPI (비 CNG) 인증서, 키 서명 및 암호 해독에 사용할 수 있습니다.|    SSL, 토큰 서명, 토큰 암호 해독, 서비스 통신 인증서|
|2|레거시 CAPI (비 CNG) 인증서를 키 서명에 사용할 수 있습니다.|권장 되지 않음|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>인증서에 KeySpec 값을 확인 하는 방법 / 키
사용할 수는 인증서 값을 확인 합니다 **certutil** 명령줄 도구입니다.  

다음은 예: **certutil – v – 저장 내**합니다.  이 화면으로 인증서 정보를 덤프 합니다.

![Keyspec 인증서](media/AD-FS-and-KeySpec-Property/keyspec1.png)

아래의 두 가지 CERT_KEY_PROV_INFO_PROP_ID 찾습니다.


1. **ProviderType:** 이 레거시 저장소 공급자 (CSP (암호화)를 사용 하는 인증서 또는 키 저장소 공급자를 기반으로 새 인증서 CNG (Next Generation) Api 여부를 나타냅니다.  0이 아닌 모든 값에는 레거시 공급자를 나타냅니다.
2. **KeySpec:** 다음은 AD FS 인증서의 유효한 KeySpec 값입니다.

   기존 CSP 공급자 (0과 같지 않은 ProviderType):

   |AD FS 인증서 용도|유효한 KeySpec 값|
   | --- | --- |
   |서비스 통신|1|
   |토큰 암호 해독|1|
   |토큰 서명|1과 2|
   |SSL|1|

   CNG 공급자 (ProviderType = 0):

   |AD FS 인증서 용도|유효한 KeySpec 값|
   | --- | --- |   
   |SSL|0|

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>지원 되는 값에는 인증서에 keyspec 변경 하는 방법
KeySpec 값을 변경 하는 경우에 다시 생성 하거나 다시 인증 기관에서 발급 한 인증서가 필요 하지 않습니다.  아래 단계를 사용 하 여 인증서 저장소에 완전 한 인증서 및 PFX 파일에서 개인 키를 가져와 다시 KeySpec는 변경할 수 있습니다.


1. 먼저 확인 하 고 해당 될 수 있도록 다시 구성할 필요에 따라 다시 가져오기 후 기존 인증서의 개인 키 사용 권한을 기록 합니다.
2. PFX 파일로 개인 키를 포함 하 여 인증서를 내보냅니다.
3. 각 AD FS 및 WAP 서버에 대해 다음 단계를 수행 합니다.
    1. 인증서를 삭제 (에서 AD FS / WAP 서버)
    2. 관리자 권한 PowerShell 명령 프롬프트를 열고 AT_KEYEXCHANGE 값 (모든 AD FS 인증서 용도 적합)를 지정 하 여 아래 cmdlet 구문을 사용 하 여 각 AD FS 및 WAP 서버에 PFX 파일을 가져옵니다.
        1. C:\>certutil –importpfx certfile.pfx AT_KEYEXCHANGE
        2. PFX 암호를 입력 합니다.
    3. 위의 완료 되 면 다음을 수행합니다
        1. 개인 키 사용 권한 확인
        2. adfs 또는 wap 서비스를 다시 시작





