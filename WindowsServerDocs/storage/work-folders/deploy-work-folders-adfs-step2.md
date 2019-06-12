---
title: AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포 - 2단계, AD FS 구성 후 작업
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 06/06/2019
ms.assetid: 0a48852e-48cc-4047-ae58-99f11c273942
ms.openlocfilehash: 5497651f57a0276daced614687e89f8047af9116
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812679"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-2-ad-fs-post-configuration-work"></a>AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 2에서 AD FS 구성 후 작업

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 AD FS(Active Directory Federation Services) 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더를 배포하는 두 번째 단계를 설명합니다. 이 과정의 다른 단계는 다음 항목에서 찾을 수 있습니다.  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 개요](deploy-work-folders-adfs-overview.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 1 단계, AD FS 설정](deploy-work-folders-adfs-step1.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 3, 작업 폴더 설정](deploy-work-folders-adfs-step3.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 4 단계, 웹 응용 프로그램 프록시 설정](deploy-work-folders-adfs-step4.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 5 단계 클라이언트 설정](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
> Windows Server 2019 또는 Windows Server 2016 환경에 대 한 지침은이 섹션에서 설명 합니다. Windows Server 2012 R2를 사용하는 경우 [Windows Server 2012 R2 instructions(Windows Server 2012 R2 지침)](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx)을 따르세요.

1단계에서 AD FS를 설치하고 구성했습니다. 이제 다음과 같은 AD FS 구성 후 단계를 수행해야 합니다.  
  
## <a name="configure-dns-entries"></a>DNS 항목 구성

AD FS에 대한 DNS 항목 두 개를 만들어야 합니다. SAN(주체 대체 이름) 인증서를 만들 때 사전 설치 단계에서 사용한 것과 똑같은 두 개 항목입니다.  
  
DNS 항목은 다음과 같은 형식입니다.  
  
-   AD FS service name.domain  
  
-   enterpriseregistration.domain  
  
-   AD FS server name.domain(DNS 항목이 있어야 합니다. 예: 2016-ADFS.contoso.com)
  
테스트 예제의 값은 다음과 같습니다.  
  
-   **blueadfs.contoso.com**  
  
-   **enterpriseregistration.contoso.com**  
  
## <a name="create-the-a-and-cname-records-for-ad-fs"></a>AD FS에 대한 A 및 CNAME 레코드 만들기

AD FS에 대한 A 및 CNAME 레코드를 만들려면 다음 단계를 따릅니다.  
  
1.  도메인 컨트롤러에서 DNS 관리자를 엽니다.  
  
2.  정방향 조회 영역 폴더를 확장하고 도메인을 마우스 오른쪽 단추로 클릭한 다음 **새로운 호스트(A)** 를 선택합니다.  
  
3.  **새 호스트** 창이 열립니다. **이름** 필드에 AD FS 서비스 이름의 별칭을 입력합니다. 테스트 예제에서는 **blueadfs**입니다.  
  
    별칭은 AD FS에 사용된 인증서의 주체와 동일해야 합니다. 예를 들어 주체가 adfs.contoso.com이면 여기에 입력할 별칭은 **adfs**입니다.  
  
    > [!IMPORTANT]  
    > Windows PowerShell 대신 Windows Server UI(사용자 인터페이스)를 사용하여 AD FS를 설정하는 경우 AD FS에 대한 CNAME 레코드 대신 A 레코드를 만들어야 합니다. UI를 통해 생성되는 SPN(서비스 사용자 이름)에는 호스트로 AD FS 서비스를 설치하는 데 사용되는 별칭만 포함되기 때문입니다.  

4.  **IP 주소**에 AD FS 서버의 IP 주소를 입력합니다. 테스트 예제에서는 **192.168.0.160**입니다. **호스트 추가**를 클릭합니다.  
  
5.  정방향 조회 영역 폴더에서 다시 한 번 도메인을 마우스 오른쪽 단추로 클릭하고 **새 별칭(CNAME)** 을 선택합니다.  
  
6.  **새 리소스 레코드** 창에서 별칭 이름 **enterpriseregistration**을 추가하고 AD FS 서버의 FQDN을 입력합니다. 이 별칭은 디바이스 연결에 사용되며 **enterpriseregistration**으로 불러야 합니다.
  
7.  **확인**을 클릭합니다.  
  
Windows PowerShell을 사용하여 해당 단계를 수행하려면 다음 명령을 사용합니다. 이 명령은 도메인 컨트롤러에서 실행해야 합니다.  
  
```Powershell  
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name blueadfs -A -IPv4Address 192.168.0.160   
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name enterpriseregistration -CName  -HostNameAlias 2016-ADFS.contoso.com
```  
  
## <a name="set-up-the-ad-fs-relying-party-trust-for-work-folders"></a>클라우드 폴더의 신뢰 당사자 트러스트 설치

아직 클라우드 폴더가 설치되지 않았더라도 클라우드 폴더의 신뢰 당사자 트러스트를 설치하고 구성할 수 있습니다. 클라우드 폴더가 AD FS를 사용할 수 있게 하려면 신뢰 당사자 트러스트를 설치해야 합니다. 현재 AD FS를 설치 중이므로 이 단계를 수행하기에 적절한 시기입니다.  
  
신뢰 당사자 트러스트를 설치하려면:  
  
1.  **서버 관리자**를 열고 **도구** 메뉴에서 **AD FS 관리**를 선택합니다.  
  
2.  오른쪽 창의 **작업**에서 **신뢰 당사자 트러스트 추가**를 클릭합니다.  
  
3.  **시작** 페이지에서 **클레임 인식**을 선택하고 **시작**을 클릭합니다.  
  
4.  **데이터 원본 선택** 페이지에서 **수동으로 신뢰 당사자 트러스트 데이터 입력**을 선택한 후 **다음**을 클릭합니다.  
  
5.  **표시 이름** 필드에 **WorkFolders**를 입력하고 **다음**을 클릭합니다.  
  
6.  **인증서 구성** 페이지에서 **다음**을 클릭합니다. 토큰 암호화 인증서는 선택 사항이며 테스트 구성에는 필요하지 않습니다.  
  
7.  **URL 구성** 페이지에서 **다음**을 클릭합니다.  
  
8. 에 **식별자 구성** 페이지에서 다음 식별자 추가: `https://windows-server-work-folders/V1`합니다. 이 식별자는 클라우드 폴더에서 사용하는 하드 코드 값이며, 클라우드 폴더가 AD FS와 통신할 때 이 식별자를 전송합니다. **다음**을 클릭합니다.  
  
9. 액세스 제어 정책 선택 페이지에서 **모든 사용자 허용**을 선택하고 **다음**을 클릭합니다.  
  
10. **트러스트 추가 준비** 페이지에서 **다음**을 클릭합니다.  
  
11. 구성이 완료되면 마법사의 마지막 페이지에 구성이 완료되었다고 표시됩니다. 클레임 규칙을 편집하는 확인란을 선택하고 **닫기**를 클릭합니다.  
  
12. AD FS 스냅인에서 **WorkFolders** 신뢰 당사자 트러스트를 선택하고 작업 아래에서 **클레임 발급 정책 편집**을 클릭합니다.

13. **클라우드 폴더에 대한 클레임 발급 정책 편집** 창이 열립니다. **규칙 추가**를 클릭합니다.  
  
14. **클레임 규칙 템플릿** 드롭다운 목록에서 **LDAP 특성을 클레임으로 보내기**를 선택하고 **다음**을 클릭합니다.  
  
15. **클레임 규칙 구성** 페이지의 **클레임 규칙 이름** 필드에 **WorkFolders**를 입력합니다.  
  
16. **특성 저장소** 드롭다운 목록에서 **Active Directory**를 선택합니다.  
  
17. 매핑 테이블에서 다음 값을 입력합니다.  
  
    -   사용자-사용자 이름: UPN  
  
    -   표시 이름: 이름  
  
    -   성: 성  
  
    -   지정 된 이름: 지정된 이름  
  
18. **마침**을 클릭합니다. 발급 변환 규칙 탭에 WorkFolders 규칙이 보이면 **확인**을 클릭합니다.  
  
### <a name="set-relying-part-trust-options"></a>신뢰 당사자 트러스트 설정 옵션

AD FS의 신뢰 당사자 트러스트를 설치한 후에는 5개의 Windows PowerShell 명령을 실행하여 구성을 완료해야 합니다. 이러한 명령은 클라우드 폴더가 AD FS와 통신하는 데 필요한 옵션을 설정하며, UI를 통해 설정할 수 없습니다. 이러한 옵션은 다음과 같습니다.  
  
-   JWT(JSON 웹 토큰) 사용  
  
-   암호화된 클레임 사용 안 함  
  
-   자동 업데이트 사용  
  
-   모든 디바이스에 Oauth 새로 고침 토큰 발급을 설정합니다.  

-   신뢰 당사자 트러스트에 대한 클라이언트 액세스 권한 부여

이러한 옵션을 설정하려면 다음 명령을 사용합니다.  
  
```powershell  
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -EnableJWT $true   
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -Encryptclaims $false   
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -AutoupdateEnabled $true   
Set-ADFSRelyingPartyTrust -TargetIdentifier "https://windows-server-work-folders/V1" -IssueOAuthRefreshTokensTo AllDevices
Grant-AdfsApplicationPermission -ServerRoleIdentifier "https://windows-server-work-folders/V1" -AllowAllRegisteredClients -ScopeNames openid,profile  
```  
  
## <a name="enable-workplace-join"></a>Workplace Join을 사용하도록 설정

Workplace Join을 사용하도록 설정하는 것은 선택 사항이지만 사용자가 본인의 개인 디바이스를 사용하여 회사 리소스에 액세스할 수 있도록 하고자 할 때에는 유용할 수 있습니다.  
  
Workplace Join에 디바이스를 등록할 수 있게 하려면 디바이스 등록을 구성하고 전역 인증 정책을 설정하는 다음 Windows PowerShell 명령을 실행해야 합니다.  
  
```powershell  
Initialize-ADDeviceRegistration -ServiceAccountName <your AD FS service account>
    Example: Initialize-ADDeviceRegistration -ServiceAccountName contoso\adfsservice$
Set-ADFSGlobalAuthenticationPolicy -DeviceAuthenticationEnabled $true   
```  
  
## <a name="export-the-ad-fs-certificate"></a>AD FS 인증서 내보내기

다음으로 테스트 환경의 다음 컴퓨터에 설치할 수 있도록 자체 서명된 AD FS 인증서를 내보내야 합니다.  
  
-   클라우드 폴더에 사용되는 서버  
  
-   웹 응용 프로그램 프록시에 사용되는 서버  
  
-   도메인에 가입된 Windows 클라이언트  
  
-   도메인에 가입되지 않은 Windows 클라이언트  
  
인증서를 내보내려면 다음 단계를 따릅니다.  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  **MMC**를 입력합니다.  
  
3.  **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
4.  **사용 가능한 스냅인** 목록에서 **인증서**를 선택한 다음 **추가**를 클릭합니다. 인증서 스냅인 마법사가 시작됩니다.  
  
5.  **컴퓨터 계정**을 선택한 다음 **다음**을 클릭합니다.  
  
6.  **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 를 선택하고 **마침**을 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **Console Root\Certificates\(Local Computer)\Personal\Certificates** 폴더를 확장합니다.  
  
9.  **AD FS 인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **내보내기...** 를 클릭합니다.  
  
10. 인증서 내보내기 마법사가 열립니다. **예, 개인 키를 내보냅니다.** 를 선택합니다.  
  
11. **파일 내보내기 형식** 페이지에서 기본 옵션을 선택한 상태로 두고 **다음**을 클릭합니다.  
  
12. 인증서 암호를 만듭니다. 나중에 다른 디바이스로 인증서를 가져올 때 이 암호가 사용됩니다. **다음**을 클릭합니다.  
  
13. 인증서의 위치와 이름을 입력한 다음 **마침**을 클릭합니다.  
  
인증서 설치는 배포 절차의 후반부에서 다루겠습니다.  
  
## <a name="manage-the-private-key-setting"></a>키 개인 설정 관리

새 인증서의 개인 키에 액세스할 수 있도록 AD FS 서비스 계정을 권한을 부여해야 합니다. 통신 인증서가 만료되어 새 인증서로 대체할 때 이 권한을 다시 부여해야 합니다. 권한을 부여하려면 다음 단계를 따릅니다.  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  **MMC**를 입력합니다.  
  
3.  **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
4.  **사용 가능한 스냅인** 목록에서 **인증서**를 선택한 다음 **추가**를 클릭합니다. 인증서 스냅인 마법사가 시작됩니다.  
  
5.  **컴퓨터 계정**을 선택한 다음 **다음**을 클릭합니다.  
  
6.  **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 를 선택하고 **마침**을 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **Console Root\Certificates\(Local Computer)\Personal\Certificates** 폴더를 확장합니다.  
  
9.  **AD FS 인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **개인 키 관리**를 클릭합니다.  
  
10. **권한** 창에서 **추가**를 클릭합니다.  
  
11. **개체 유형** 창에서 **서비스 계정**을 선택한 다음 **확인**을 클릭합니다.  
  
12. AD FS를 실행하는 계정 이름을 입력합니다. 테스트 예제에서는 ADFSService입니다. **확인**을 클릭합니다.  
  
13. **권한** 창에서 계정에 적어도 읽기 권한 이상을 부여하고 **확인**을 클릭합니다.  
  
개인 키를 관리 하는 옵션 목록에 없으면 다음 명령을 실행 해야 합니다. `certutil -repairstore my *`  
  
## <a name="verify-that-ad-fs-is-operational"></a>AD FS가 작동하는지 확인

AD FS 작동 중인지를 확인 하려면 브라우저 창을 열고 이동할 `https://blueadfs.contoso.com/federationmetadata/2007-06/federationmetadata.xml`, 환경에 맞게 URL을 변경 합니다.
  
브라우저 창에 아무 서식 없는 페더레이션 서버 메타데이터가 표시됩니다. SSL 오류나 경고 없이 데이터가 표시되면 페더레이션 서버가 정상적으로 작동하는 것입니다.  
  
다음 단계: [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 3, 작업 폴더 설정](deploy-work-folders-adfs-step3.md)  
  
## <a name="see-also"></a>관련 항목  
[클라우드 폴더 개요](Work-Folders-Overview.md)