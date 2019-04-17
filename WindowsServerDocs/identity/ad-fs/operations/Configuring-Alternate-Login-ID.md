---
ms.assetid: f0cbdd78-f5ae-47ff-b5d3-96faf4940f4a
title: "암호 확인용 로그인 ID 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 12/04/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb4c98ff1090a9d3c35654614a43e12db99d691d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-alternate-login-id"></a>암호 확인용 로그인 ID 구성

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

사용자가 어떤 형태의 Active Directory Domain Services (AD DS)에서 허용 되는 사용자 id 사용 하 여 사용 하는 AD FS(Active Directory Federation Services) 응용 프로그램에 로그인 할 수 있습니다. 여기에 (Upn) 사용자 이름 (johndoe@contoso.com) 또는 도메인 한정 (contoso\johndoe 또는 contoso.com\johndoe) 삼로 계정 이름입니다.

기업 정책이 나 방침 온-프레미스 온라인 비즈니스 응용 프로그램 종속성 인해 일부 환경에서 최종 사용자에 게 메일 주소 하지 사항과 UPN 또는 삼로 계정 이름을 알고 수만 있습니다. 경우에 따라 UPN 이기도 불가능 (jdoe@contoso.local)를 인증 회사 네트워크에서 응용 프로그램에만 사용 됩니다.

이후 불가능 하는 도메인의 (여러분입니다. Contoso.local) 확인할 수 없는, Office 365 모든 사용자 Id를 완전히 경로 조정 가능 인터넷 수 로그인 필요 합니다. 온-프레미스 UPN (전직 불가능 도메인을 사용 하는 경우. Contoso.local) 또는 기존 UPN 로컬 응용 프로그램 종속성 인해 변경할 수 없는, 좋습니다 대체 로그인 id입니다. 암호 확인용 로그인 ID 사용자가 메일 등 자녀가 UPN 이외의 특성 수 로그인 로그 환경을 구성할 수 있습니다.

이 기능은 혜택 중 하나는 온-프레미스 Upn 수정 하지 않고 Office 365 같은 SaaS 공급자 채택 수 있습니다. 또한 소비자 프로 비전 id와의 업무 서비스 응용 프로그램을 지원할 수 있습니다.

> [!IMPORTANT]
> Exchange 및/또는 비즈니스용 Skype와 하이브리드 환경에서 암호 확인용 ID를 사용 하 여 지원 있지만 권장 되지 않습니다. 온-프레미스 및 온라인 동일한 집합이 자격 증명 (예: UPN)를 사용 하 여 사용자 환경을 최적화 하이브리드 환경에서 제공 합니다.  고객 대체 id 하지 않으려면 해당 Upn 가능한 경우 변경 하는 것이 좋습니다. 암호 확인용 ID를 사용 하 여 비즈니스용 Lync 또는 Skype와 Lync Server 2013 이상이 필요 합니다. 암호 확인용 ID를 사용 하는 고객 사용 고려해 야 [최신 인증](https://support.office.com/article/using-office-365-modern-authentication-with-office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) Office 365에 대 한 향상 된 사용자 환경에서 거래소에 대 한 합니다. 또한 모바일 고객과 비즈니스용 Skype를 사용 하는 고객 SIP 주소는 사용자의 메일 주소 (와 대체 ID)를 동일 해야 합니다. 

다양 한 Office 365 클라이언트를 사용 하 여 일반 인증과 최신 인증 인증서 기반 인증 (최신 인증 설정 해야 함)으로 대체 ID를 가진 사용자 환경에 대 한 아래 표를 참조 하세요.

|**클라이언트 유형**|**자세한 내용**|**지원 정책-일반 및 최신 인증**|**설명**|
|--------------------|------------------------------|------------------------------|------------------------------|
|Outlook|일반 인증: 사용자 도메인 연결 된 컴퓨터에 있어야 하며 회사 네트워크에 연결<br /><br />최신 인증: 지원|만 사서함 사용자 외부 액세스 허용 하지 않는 환경에서 암호 확인용 ID를 사용할 수 있습니다. 이 사용자가 수만 인증 사서함 그 자리에 지원 되는 방법에 연결 하 고, vpn 회사 네트워크에 가입 하거나 직접 액세스를 통해 연결 된 때를 의미 합니다. 최신 인증 (ADAL 라고) 구성 하기로 선택한 경우 비 도메인 가입 연결 된 컴퓨터에서 Outlook을 사용할 수 있지만 Outlook 프로필 구성 하는 경우 몇 가지 추가 메시지를 받습니다.<br /><br />첫 번째 이미지 사용자 환경 데모 표 아래를 참조 하십시오.|[Office 2013에서 최신 인증](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|하이브리드 공용 폴더|지원 되지 일반 인증:<br /><br />최신 인증: 지원|하이브리드 공용 폴더를 사용 하 고 따라서 하지 사용 해야 오늘 일반 인증 방법으로 대체 ID 확장 수 없습니다. 공용 폴더 하이브리드에 사용 하려는 경우 최신 인증 (이 ADAL 라고 함)를 구성 해야 합니다.<br /><br />첫 번째 이미지 사용자 환경 데모 표 아래를 참조 하십시오.|[Office 2013에서 최신 인증](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|프레미스 위임 간|지원 되지 않음|현재 사용 권한을 하이브리드 구성에서 지원 되지 않는 프레미스 크로스 하지만 작동 하지 않습니다 AltID 사용 하는 경우 합니다.||
|보관 사서함 액세스 (사서함 온-프레미스-클라우드에서 보관)|지원|보관 파일에 액세스할 때 사용자가 자격에 대 한 추가 메시지를 얻을 제공 하는 메시지가 표시 되 면 ID 있는 대체 합니다.<br /><br />첫 번째 이미지 사용자 환경 데모 표 아래를 참조 하십시오.||
|Office 365 Pro 이용 정품 인증 페이지|지원 되는-권장 되는 클라이언트 쪽 레지스트리 키|구성 대체 id 검증 필드에 온-프레미스 UPN 미리 입력이 표시 됩니다. 이 사용 하는 암호 확인용 Id를 변경 해야 합니다. 링크 열의 했음을 알아차렸을 클라이언트 측 레지스트리 키를 사용 하는 것이 좋습니다.<br /><br />두 번째 이미지 사용자 환경 데모 표 아래를 참조 하십시오.|[Office 2013 및 Lync 2013 주기적으로 자격 증명 하 고 온라인 Lync, OneDrive, SharePoint Online](https://support.microsoft.com/en-us/kb/2913639)|
|Microsoft Teams|지원|Microsoft Teams supports AD FS (SAML-P, WS-Fed, WS-Trust, and OAuth) and Modern Authentication.<br/><br/> Core Microsoft Teams such as Channels, chats and files functionalities does work with Altnernate Login ID. </br></br>1st and 3rd party apps have to be separately investigated  by the customer. This is because each application has their own supportability authentication protocols.| 
|비즈니스용 Skype / Lync|지원 되는 (언급 했 듯이 제외) 가능성 사용자 인 한 혼동을 하지만 합니다.  모바일 클라이언트에서 암호 확인용 Id는 경우에 지원 SIP 주소 메일 주소를 = = 대체 id.|사용자가 로그인 비즈니스용 Skype 데스크톱 클라이언트 먼저 온-프레미스 UPN 사용 하 고 사용 하 여 대체 id.을 두 번 해야 할 수 있습니다. ("로그인 주소"은 수 없음 "사용자 이름을" 동일 하지만 자주 SIP 주소 실제로).  먼저 사용자 이름에 대 한 메시지가 표시 되 면 사용자 올바르게 사전 채웁니다 하지 대체 ID 또는 SIP 주소를 사용 하는 경우에 UPN를 입력 해야 합니다. 사용자가 로그인 UPN, 사용자 이름이 프롬프트 나타나므로, UPN 채워집니다이 이번 합니다. 로그인 프로세스를 완료 하려면 사용자 해야 대체 ID로 대체 놓은이 지금 로그인 합니다. 모바일 클라이언트에서 사용자가 입력 해야 온-프레미스 사용자 ID 고급 페이지에서 UPN 포맷 하지 삼로 스타일 형식을 (도메인 \)를 사용 하 여 합니다.<br /><br />성공적으로 로그인 한 후 비즈니스용 Skype 또는 Lync "Exchange 필요한 자격 증명" 표시 되 면 해야 사서함이 있는에 사용할 수 있는 자격 증명을 제공 합니다. 암호 확인용 id. 제공 하기 위해 필요한 사서함 클라우드 중인 경우 사서함은 온-프레미스 온-프레미스 UPN 제공 해야 합니다.|[Office 2013에서 최신 인증](https://blogs.office.com/2015/03/23/office-2013-modern-authentication-public-preview-announced/)|
|Outlook 웹 액세스|지원|||
|Android, IOS, 및 Windows Phone에 outlook 모바일 앱|지원|||
|OneDrive for Business|지원 되는-권장 되는 클라이언트 쪽 레지스트리 키|구성 대체 id 검증 필드에 온-프레미스 UPN 미리 입력이 표시 됩니다. 이 사용 하는 암호 확인용 Id를 변경 해야 합니다. 링크 열의 했음을 알아차렸을 클라이언트 측 레지스트리 키를 사용 하는 것이 좋습니다.<br /><br />두 번째 이미지 사용자 환경 데모 표 아래를 참조 하십시오.|[Office 2013 및 Lync 2013 주기적으로 자격 증명 하 고 온라인 Lync, OneDrive, SharePoint Online](https://support.microsoft.com/en-us/kb/2913639)|
|OneDrive for Business 모바일 클라이언트|지원|||

![암호 확인용 로그인](media/Configure-Alternate-Login-ID/ADFS_Alt_ID1.png)

![암호 확인용 로그인](media/Configure-Alternate-Login-ID/ADFS_Alt_ID2.png)

![암호 확인용 로그인](media/Configure-Alternate-Login-ID/ADFS_Alt_ID3.png)

다음, 다음과 같은 스크린샷은 비즈니스용 Skype를 사용 하 여 추가 예입니다.  예는 다음과 같은 정보를 사용


- SIP:userA@contoso.com 
- UPN:userA@contoso.local
- 메일 주소:userA@contoso.com
- AltId:userA@contoso.com 

로그인 필드에 SIP 주소를 입력 합니다.

![Skype](media/Configure-Alternate-Login-ID/SkypeA.png)

![Skype](media/Configure-Alternate-Login-ID/SkypeB.png)

![Skype](media/Configure-Alternate-Login-ID/SkypeC.png)

## <a name="to-configure-alternate-login-id"></a>암호 확인용 로그인 ID 구성 하려면
암호 확인용 로그인 ID를 구성 하기 위해 다음과 같은 작업을 수행 해야 합니다.

대체 로그인 ID를 사용 하 여 ADFS 청구 제공자 신뢰를 구성 합니다.

1.  Install [KB2919355](https://go.microsoft.com/fwlink/?LinkID=396590).  Windows 업데이트 서비스를 통해 다운로드 하거나 직접 다운로드할 수 있습니다.

2.  다음 PowerShell cmdlet에 농장의 federation 서버에서 실행 하 여 ADFS 구성을 업데이트 (WID 농장을 사용 하는 경우이 명령을 실행 해야이 하면 농장 주 ADFS 서버의):

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID <attribute> -LookupForests <forest domain>

    ```

    **AlternateLoginID** 로그인에 사용 하려는 특성 LDAP 이름입니다.

    **LookupForests** DNS 사용자에 속하는 숲 속의 목록입니다.

    암호 확인용 로그인 ID 기능을 사용 하려면-AlternateLoginID 및-LookupForests 매개 null, 올바르지 값으로 구성 해야 합니다.

    다음 예제에서 사용 하는 암호 확인용 로그인 ID 기능 계정 contoso.com 및 fabrikam.com 숲에 사용자가 자신의 "메일" 특성으로 FS 사용 응용 AD에 로그인 할 수 있도록 합니다.

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID mail -LookupForests contoso.com,fabrikam.com
    ```

3.  이 기능을 해제 하려면 null 두 매개에 대 한 값을 설정 합니다.

    ```
    Set-AdfsClaimsProviderTrust -TargetIdentifier "AD AUTHORITY" -AlternateLoginID $NULL -LookupForests $NULL
    ```

4.  Azure AD로 대체 로그인 ID를 사용 하려면 추가 구성 단계가 없는 Azure AD 연결을 사용 하는 경우 필요 합니다.   암호 확인용 ID 마법사에서 직접 구성할 수 있습니다.  섹션 아래에서 사용자를 식별 고유 하 게 표시 [Azure AD에 연결](https://azure.microsoft.com/en-us/documentation/articles/active-directory-aadconnect-get-started-custom/#connect-to-azure-ad)합니다.

## <a name="additional-details--considerations"></a>추가 세부 정보 및 고려

-   암호 확인용 로그인 ID 기능을 배포 Adfs와 연결 된 환경에 대 한 사용할 수만 합니다.  다음과 같은 경우에는 지원 되지 않습니다.
    -   비 경로 조정 가능 (예: Contoso.local) 하는 도메인 Azure AD 하 여 확인할 수 없습니다.
    -   ADFS 배포 하지 않은 환경을 관리 합니다.


-   활성화 되 면, 암호 확인용 로그인 ID 기능은 사용자 이름/암호 인증 사용할 수 있는 Adfs에서 지 원하는 하는 모든 사용자 이름/암호 인증 프로토콜 (SAML P, WS 급지됨 Ws-trust, 및 OAuth).


-   Windows 통합 인증 (WIA) 때 수행 됩니다 (예를 들어, 사용자가 도메인에 가입 컴퓨터에서 기업 응용 프로그램은 인트라넷에서 액세스 하려는 및 ADFS 관리자가 WIA 인트라넷 사용할 인증 정책을 구성), UPN 인증을 위해 사용 됩니다. 암호 확인용 로그인 ID 기능에 대 한 신뢰 당사자에 대 한 모든 클레임 규칙 구성한 경우 해당 규칙 WIA 경우에도 유효한 지 확인 해야 합니다.

-   활성화 되 면, 암호 확인용 로그인 ID 기능을 지 원하는 ADFS 각 사용자 계정 숲 ADFS 서버에서 액세스할 수 있는 하나 이상의 드 서버가 필요 합니다. 사용자 계정 숲 속의 드 서버에 도달 하는 오류 UPN를 사용 하 여 대체 ADFS 발생 합니다. 기본적으로 모든 도메인 컨트롤러 서버 드 됩니다.

-   ADFS 서버 구성 된 사용자 계정 숲에서 지정 된 대체 로그인 ID 값 개 이상의 사용자 개체 발견 되 면 사용을 하는 경우 로그인을 실패 합니다.

-   암호 확인용 로그인 ID 기능이 활성화 된 경우 Adfs는 하려고 먼저 최종 사용자 대체 로그인 ID 인증 고 대체 로그인 id 식별할 수 있는 계정 찾을 수 없는 경우 UPN를 사용 하 여 다시 전환 여전히 지원 UPN 로그인 하려는 경우 대체 로그인 ID와 UPN 간의 충돌 하지는 있는지 확인 해야 합니다. 예를 들어, 다른 사람의 UPN 사용 하 여 메일 특성 설정의 다른 사용자가 자신의 UPN 로그인 차단 됩니다.

-   관리자가 구성 되어 숲 중 하나를 경우 사용자 계정에 대체 로그인 ID 구성 되어 있는 다른 숲에서 조회 ADFS 계속 됩니다. ADFS 서버 찾습니다 고유한 사용자가 검색 숲에서 사용자 성공적으로 로그인 합니다.

-   일부 ID 대체 로그인에 대 한 힌트 최종 사용자에 게 ADFS 로그인 페이지를 사용자 지정 또한. 사용자 지정 된 로그인 페이지 설명 추가 하거나 로그인 할 수도 있습니다 (자세한 내용은 참조 [AD FS 로그인 페이지 사용자 지정](https://technet.microsoft.com/library/dn280950.aspx) 또는 사용자 이름 들판 위 문자열 "조직 계정으로 로그인" 사용자 지정 (자세한 내용은 참조 [광고 FS 로그인 페이지 고급 사용자 지정](https://technet.microsoft.com/library/dn636121.aspx)합니다.

-   암호 확인용 로그인 ID 값을 포함 하는 새로운 클레임 형식이 **http:schemas.microsoft.com/ws/2013/11/alternateloginid**

## <a name="events-and-performance-counters"></a>이벤트 및 성능 카운터
다음과 같은 성능 카운터 대체 로그인 ID가 활성화 되어 ADFS 서버의 성능을 측정 추가 되었습니다.

-   암호 확인용 로그인 ID를 사용 하 여 수행 인증 수 대체 로그인 Id 인증이:

-   초당 대체 로그인 ID를 사용 하 여 수행 인증 수 로그인 Id 인증/초 대체:

-   암호 확인용 로그인 id 평균 검색 대기 시간: 관리자가 암호 확인용 로그인 id 구성 숲에서 평균 검색 대기 시간

다음은 다양 한 경우 오류 및 기록 ADFS 하 여 이벤트와 함께 사용자의 로그인 경험에 영향을 해당입니다.



**오류의 경우**|**로그인 경험에 영향**|**이벤트**|
---------|---------|---------
사용자 개체 SAMAccountName에 대 한 값을 받을 수 없습니다.|로그인에 실패|이벤트 ID 364 MSIS8012 예외 메시지로: samAccountName 사용자를 찾을 수 없습니다.: ' {0} ' 합니다.|
CanonicalName 특성 액세스할 수 없는 경우|로그인에 실패|이벤트 ID 364 예외 MSIS8013 메시지와 함께: CanonicalName: 사용자의 ' {0} ':' {1} '는 잘못 형식에서 있습니다.|
여러 사용자 개체 한 숲에 있습니다.|로그인에 실패|된 예외 메시지 MSIS8015 364 이벤트 ID: ' {1} ' id와 숲 속의 id ' {0} ' (를) 사용 하 여 여러 사용자 계정 발견: {2}|
여러 사용자 개체 여러 숲에서 발견 된|로그인에 실패|된 예외 메시지 MSIS8014 364 이벤트 ID: ' {0} ' id 가진 사용자 계정이 여러 개 숲에서 찾을 수: {1}|

## <a name="see-also"></a>참조 하십시오
[AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)


