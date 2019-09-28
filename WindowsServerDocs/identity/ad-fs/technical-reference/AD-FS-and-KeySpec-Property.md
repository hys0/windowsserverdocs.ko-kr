---
title: Active Directory Federation Services 및 인증서 키 사양 속성 정보
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: a5307da5-02ff-4c31-80f0-47cb17a87272
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 51c9828cfe494c68422f4985e5b17113020c8414
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407422"
---
# <a name="ad-fs-and-certificate-keyspec-property-information"></a>AD FS 및 certificate KeySpec 속성 정보
키 사양 ("KeySpec")은 인증서 및 키와 연결 된 속성입니다. 인증서와 연결 된 개인 키를 서명, 암호화 또는 둘 다에 사용할 수 있는지 여부를 지정 합니다.   

KeySpec 값이 잘못 되 면 다음과 같은 AD FS 및 웹 응용 프로그램 프록시 오류가 발생할 수 있습니다.


- AD FS 이벤트가 기록 되지 않고 AD FS 또는 웹 응용 프로그램 프록시에 대 한 SSL/TLS 연결을 설정 하지 못했습니다 (SChannel 36888 및 36874 이벤트가 기록 될 수 있음).
- AD FS 또는 WAP 폼 기반 인증 페이지에서 로그인 하지 못했습니다. 페이지에 오류 메시지가 표시 되지 않습니다.

이벤트 로그에 다음이 표시 될 수 있습니다.

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

## <a name="what-causes-the-problem"></a>문제의 원인
KeySpec 속성은 microsoft 레거시 CSP (암호화 저장소 공급자)에서 Microsoft CryptoAPI (CAPI)에 의해 생성 되거나 검색 된 키를 사용할 수 있는 방법을 식별 합니다.

KeySpec 값 **1**또는 **AT_KEYEXCHANGE**는 서명 및 암호화에 사용할 수 있습니다.  값 **2**또는 **AT_SIGNATURE**는 서명에만 사용 됩니다.

가장 일반적으로 사용 되는 KeySpec는 토큰 서명 인증서 이외의 인증서에 값 2를 사용 하는 것입니다.  

CNG (Cryptography Next Generation) 공급자를 사용 하 여 키가 생성 된 인증서의 경우 키 사양의 개념이 없고 KeySpec 값은 항상 0이 됩니다.

아래에서 유효한 KeySpec 값을 확인 하는 방법을 참조 하세요. 

### <a name="example"></a>예제
레거시 CSP의 예로는 Microsoft 고급 암호화 공급자가 있습니다. 

Microsoft RSA CSP key blob 형식에는 각 <strong>AT_KEYEXCHANGE * * 또는 * * AT_SIGNATURE</strong> 키에 대 한 요청을 처리 하기 위한 알고리즘 식별자 ( **CALG_RSA_KEYX** 또는 **CALG_RSA_SIGN**)가 포함 되어 있습니다.

RSA 키 알고리즘 식별자는 다음과 같이 KeySpec 값에 매핑됩니다.

| 공급자 지원 알고리즘| CAPI 호출에 대 한 키 사양 값 |
| --- | --- |
|CALG_RSA_KEYX : 서명 및 암호 해독에 사용할 수 있는 RSA 키입니다.| AT_KEYEXCHANGE (또는 KeySpec = 1)|
CALG_RSA_SIGN : RSA 서명만 키 |AT_SIGNATURE (또는 KeySpec = 2)|

## <a name="keyspec-values-and-associated-meanings"></a>KeySpec 값 및 관련 된 의미
다음은 다양 한 KeySpec 값의 의미입니다.

|Keyspec 값|그러므로|권장 AD FS 사용|
| --- | --- | --- |
|0|인증서가 CNG 인증서 인 경우|SSL 인증서만|
|1|레거시 CAPI (비 CNG) 인증서의 경우 서명 및 암호 해독에 키를 사용할 수 있습니다.|    SSL, 토큰 서명, 토큰 암호 해독, 서비스 통신 인증서|
|2|레거시 CAPI (비 CNG) 인증서의 경우 서명에만 키를 사용할 수 있습니다.|권장 하지 않음|

## <a name="how-to-check-the-keyspec-value-for-your-certificates--keys"></a>인증서/키에 대 한 KeySpec 값을 확인 하는 방법
인증서 값을 보려면 **certutil** 명령줄 도구를 사용할 수 있습니다.  

다음은 **certutil – v – store my**입니다.  그러면 인증서 정보가 화면에 덤프 됩니다.

![Keyspec cert](media/AD-FS-and-KeySpec-Property/keyspec1.png)

CERT_KEY_PROV_INFO_PROP_ID 아래에서 두 가지를 찾습니다.


1. **Providertype:** 인증서가 기존 CSP (암호화 저장소 공급자)를 사용 하는지 아니면 최신 CNG (Certificate next Generation) api를 기반으로 하는 키 저장소 공급자를 사용 하는지 여부를 나타냅니다.  0이 아닌 값은 레거시 공급자를 나타냅니다.
2. **KeySpec** AD FS 인증서의 유효한 KeySpec 값은 다음과 같습니다.

   레거시 CSP 공급자 (ProviderType은 0과 같지 않음):

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

## <a name="how-to-change-the-keyspec-for-your-certificate-to-a-supported-value"></a>인증서에 대 한 keyspec를 지원 되는 값으로 변경 하는 방법
KeySpec 값을 변경 하는 경우 인증서를 다시 생성 하거나 인증 기관에서 다시 발급 하지 않아도 됩니다.  다음 단계를 사용 하 여 PFX 파일에서 전체 인증서 및 개인 키를 인증서 저장소로 다시 가져와서 KeySpec를 변경할 수 있습니다.


1. 먼저, 다시 가져온 후 필요한 경우 다시 구성할 수 있도록 기존 인증서에 대 한 개인 키 권한을 확인 하 고 기록 합니다.
2. 개인 키를 포함 하는 인증서를 PFX 파일로 내보냅니다.
3. 각 AD FS 및 WAP 서버에 대해 다음 단계를 수행 합니다.
    1. AD FS/WAP 서버에서 인증서를 삭제 합니다.
    2. 관리자 권한 PowerShell 명령 프롬프트를 열고 아래 cmdlet 구문을 사용 하 여 각 AD FS 및 WAP 서버에서 PFX 파일을 가져오고, AT_KEYEXCHANGE 값 (모든 AD FS 인증 목적으로 작동)을 지정 합니다.
        1. C: \>certutil – importpfx certfile .pfx .pfx AT_KEYEXCHANGE
        2. PFX 암호 입력
    3. 위의 작업이 완료 되 면 다음을 수행 합니다.
        1. 개인 키 사용 권한 확인
        2. adfs 또는 wap 서비스를 다시 시작 합니다.





