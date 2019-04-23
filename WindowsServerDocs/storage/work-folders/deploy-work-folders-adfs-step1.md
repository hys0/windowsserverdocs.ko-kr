---
title: AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포 - 1단계, AD FS 설치
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 10/18/2018
ms.assetid: 938cdda2-f17e-4964-9218-f5868fd96735
ms.openlocfilehash: a26b784c18049ee473a191abc7bfa0a5d253d15e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883034"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-1-set-up-ad-fs"></a>AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. AD FS 설치 1 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 AD FS(Active Directory Federation Services) 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더를 배포하는 첫 번째 단계를 설명합니다. 이 과정의 다른 단계는 다음 항목에서 찾을 수 있습니다.  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 개요](deploy-work-folders-adfs-overview.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 2에서 AD FS 구성 후 작업](deploy-work-folders-adfs-step2.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 3, 작업 폴더 설정](deploy-work-folders-adfs-step3.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 4 단계, 웹 응용 프로그램 프록시 설정](deploy-work-folders-adfs-step4.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 5 단계 클라이언트 설정](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
>   이 섹션에서는 Windows Server 2016 환경에 대한 지침을 다룹니다. Windows Server 2012 R2를 사용하는 경우 [Windows Server 2012 R2 instructions(Windows Server 2012 R2 지침)](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx)을 따르세요.

클라우드 폴더에 사용할 AD FS를 설치하려면 다음 절차를 수행하세요.  
  
## <a name="pre-installment-work"></a>사전 설치 작업  
다음 지침에 따라 설치하는 테스트 환경을 프로덕션 환경으로 전환하려면 시작하기 전에 다음과 같은 두 가지 작업을 수행해야 합니다.  
  
-   AD FS 서비스를 실행하는 데 사용할 Active Directory 도메인 관리자 계정을 설정합니다.
  
-   서버 인증에 사용할 SSL(Secure Sockets Layer) SAN(주체 대체 이름) 인증서를 얻습니다. 테스트 예제에서는 자체 서명된 인증서를 사용하지만 프로덕션 환경에서는 공개적으로 신뢰할 수 있는 인증서를 사용해야 합니다.  
  
회사 정책에 따라 이러한 항목을 모두 준비하는 데 다소 시간이 걸릴 수 있으므로 테스트 환경 만들기를 시작하기 전에 항목 요청 프로세스를 미리 시작하는 것이 좋습니다.  
  
인증서를 구입할 수 있는 여러 상용 CA(인증 기관)가 있습니다. Microsoft에서 신뢰할 수 있는 CA 목록은 [KB 문서 931125](https://support.microsoft.com/kb/931125)에서 찾을 수 있습니다. 또 다른 방법은 회사의 엔터프라이즈 CA에서 인증서를 얻는 것입니다.  
  
테스트 환경에서는 제공된 스크립트 중 하나를 통해 생성되는 자체 서명된 인증서를 사용합니다.  
  
> [!NOTE]  
> AD FS는 CNG(Cryptography Next Generation) 인증서를 지원하지 않습니다. Windows PowerShell cmdlet New-SelfSignedCertificate를 사용하여 자체 서명된 인증서를 만들 수 없다는 뜻입니다. 하지만 [Deploying Work Folders with AD FS and Web Application Proxy(AD FS 및 WAP(웹 응용 프로그램 프록시)를 사용하여 클라우드 폴더 배포)](https://blogs.technet.microsoft.com/filecab/2014/03/03/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap) 블로그 게시물에 포함된 makecert.ps1 스크립트를 사용할 수 있습니다. 이 스크립트는 AD FS와 호환되고 인증서를 만드는 데 필요한 SAN 이름을 요청하는 자체 서명된 인증서를 만듭니다.  
  
그리고 다음 섹션에 설명된 추가적인 사전 설치 작업을 수행합니다.  
  
### <a name="create-an-ad-fs-self-signed-certificate"></a>AD FS 자체 서명된 인증서  
AD FS 자체 서명된 인증서를 만들려면 다음 단계를 따릅니다.  
  
1.  [AD FS 및 WAP(웹 응용 프로그램 프록시)를 사용하여 클라우드 폴더 배포](https://blogs.technet.microsoft.com/filecab/2014/03/03/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap) 블로그 게시물에 제공된 스크립트를 다운로드한 다음 makecert.ps1 파일을 AD FS 컴퓨터로 복사합니다.  
  
2.  관리자 권한으로 Windows PowerShell 창을 엽니다.  
  
3.  실행 정책을 제한 없음으로 설정합니다.  
  
    ```powershell  
    Set-ExecutionPolicy –ExecutionPolicy Unrestricted   
    ```  
  
4.  스크립트를 복사한 디렉터리로 변경합니다.  
  
5.  makecert 스크립트를 실행합니다.  
  
    ```powershell  
    .\makecert.ps1  
    ```  
  
6.  주체 인증서를 변경하라는 메시지가 나타나면 새로운 주체 값을 입력합니다. 이 예의 값은 **blueadfs.contoso.com**입니다.  
  
7.  SAN 이름을 입력하라는 메시지가 나타나면 Y를 누른 다음 SAN 이름을 한 번에 하나씩 입력합니다.  
  
    이 예에서는 **blueadfs.contoso.com**을 입력하고 Enter 키를 누른 다음, **2016-adfs.contoso.com**을 입력하고 Enter 키를 누른 다음, **enterpriseregistration.contoso.com**을 입력하고 Enter 키를 누릅니다.  
  
    모든 SAN 이름을 입력한 후 빈 줄에서 Enter 키를 누릅니다.  
  
8.  신뢰할 수 있는 루트 인증 기관 저장소에 인증서를 설치하라는 메시지가 나타나면 Y를 누릅니다.  
  
AD FS 인증서는 다음 값을 가진 SAN 인증서여야 합니다.  

-   AD FS service name.domain

-   enterpriseregistration.domain

-   AD FS server name.domain

테스트 예제의 값은 다음과 같습니다.  
  
-   **blueadfs.contoso.com**
  
-   **enterpriseregistration.contoso.com**
  
-   **2016-adfs.contoso.com**
  
enterpriseregistration SAN은 Workplace Join에 필요합니다.  
  
### <a name="set-the-server-ip-address"></a>서버 IP 주소 설정  
서버 IP 주소를 고정 IP 주소로 변경합니다. 테스트 예를 들어 192.168.0.160 인 IP 클래스 A를 사용 하 여 / 서브넷 마스크: 255.255.0.0/기본 게이트웨이: 192.168.0.1/DNS를 기본 설정: 192.168.0.150 (도메인 컨트롤러의 IP 주소\)합니다.  
  
## <a name="install-the-ad-fs-role-service"></a>AD FS 역할 서비스 설치  
AD DS를 설치하려면 다음 단계를 따릅니다.  
  
1.  AD FS를 설치할 실제 컴퓨터 또는 가상 컴퓨터에 로그인하고, **서버 관리자**를 열고, 역할 및 기능 추가 마법사를 시작합니다.  
  
2.  **서버 역할** 페이지에서 **Active Directory Federation Services** 역할을 선택한 후 **다음**을 클릭합니다.  
  
3.  **AD FS(Active Directory Federation Services)** 페이지에 AD FS와 동일한 컴퓨터에는 웹 응용 프로그램 프록시 역할을 설치할 수 없다는 메시지가 표시될 것입니다. **다음**을 클릭합니다.  
  
4.  확인 페이지에서 **설치**를 클릭합니다.  
  
Windows PowerShell을 통해 해당 AD FS 설치를 수행하려면 다음 명령을 사용합니다.  
  
```powershell  
Add-WindowsFeature RSAT-AD-Tools  
Add-WindowsFeature ADFS-Federation –IncludeManagementTools  
```  
  
## <a name="configure-ad-fs"></a>AD FS 구성  
다음으로 서버 관리자 또는 Windows PowerShell을 사용하여 AD FS를 구성합니다.  
  
### <a name="configure-ad-fs-by-using-server-manager"></a>서버 관리자를 사용하여 AD FS 구성  
서버 관리자를 사용하여 AD FS를 구성하려면 다음 단계를 따릅니다.  
  
1.  서버 관리자를 엽니다.  
  
2.  서버 관리자 창의 맨 위에서 **알림** 플래그를 클릭한 다음 **이 서버에 페더레이션 서비스를 구성하십시오.** 를 클릭합니다.  
  
3.  Active Directory Federation Services 구성 마법사가 실행됩니다. **AD DS에 연결** 페이지에서 AD FS 계정으로 사용할 도메인 관리자 계정을 입력하고 **다음**을 클릭합니다.  
  
4.  **서비스 속성 지정** 페이지에서 AD FS 통신에 사용할 SSL 인증서의 주체 이름을 입력합니다. 테스트 예제에서는 **blueadfs.contoso.com**입니다.  
  
5.  페더레이션 서비스 이름을 입력합니다. 테스트 예제에서는 **blueadfs.contoso.com**입니다. **다음**을 클릭합니다.  
  
    > [!NOTE]  
    > 페더레이션 서비스 이름에 환경의 기존 서버 이름을 사용하면 안 됩니다. 기존 서버 이름을 사용하면 AD FS 설치가 실패하며 설치 작업을 다시 시작해야 합니다.  
  
6.  **서비스 계정 지정** 페이지에서 관리 서비스 계정에 사용할 이름을 입력합니다. 테스트 예제의 경우 **그룹 관리 서비스 계정 만들기**를 선택하고 **계정 이름**에 **ADFSService**를 입력합니다. **다음**을 클릭합니다.  
  
7.  **구성 데이터베이스 지정** 페이지에서 **Windows 내부 데이터베이스를 사용하여 이 서버에 데이터베이스를 만듭니다.** 를 선택하고 **다음**을 클릭합니다.  
  
8.  **검토 옵션** 페이지에 사용자가 선택한 옵션의 개요가 표시됩니다. **다음**을 클릭합니다.  
  
9. **필수 조건 확인** 페이지에 모든 필수 조건 검사가 성공했는지 여부가 표시됩니다. 문제가 없으면 **구성**을 클릭합니다.  
  
    > [!NOTE]  
    > AD FS 서버 또는 다른 기존 컴퓨터의 이름을 페더레이션 서비스 이름에 사용한 경우에는 오류 메시지가 표시됩니다. 이 경우 설치 작업을 다시 시작하고 기존 컴퓨터의 이름이 아닌 다른 이름을 선택해야 합니다.  
  
10. 구성이 완료되면 **결과** 페이지에 AD FS가 구성되었다는 확인 메시지가 표시됩니다.  
  
### <a name="configure-ad-fs-by-using-powershell"></a>PowerShell을 사용하여 AD FS 구성  
Windows PowerShell을 통해 해당 AD FS 구성을 수행하려면 다음 명령을 사용합니다.  
  
AD FS를 설치하려면:  
  
```powershell  
Add-WindowsFeature RSAT-AD-Tools  
Add-WindowsFeature ADFS-Federation -IncludeManagementTools   
```  
  
관리 서비스 계정을 만들려면:  
  
```powershell  
New-ADServiceAccount "ADFSService"-Server 2016-DC.contoso.com -Path "CN=Managed Service Accounts,DC=Contoso,DC=COM" -DNSHostName 2016-ADFS.contoso.com -ServicePrincipalNames HTTP/2016-ADFS,HTTP/2016-ADFS.contoso.com  
```  
  
AD FS를 구성한 후에는 이전 단계에서 만든 관리 서비스 계정과 사전 구성 단계에서 만든 인증서를 사용하여 AD FS 팜을 설치해야 합니다.  
  
AD FS 팜을 설치하려면:  
  
```powershell  
$cert = Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match blueadfs.contoso.com} | sort $_.NotAfter -Descending | select -first 1    
$thumbprint = $cert.Thumbprint  
Install-ADFSFarm -CertificateThumbprint $thumbprint -FederationServiceDisplayName "Contoso Corporation" –FederationServiceName blueadfs.contoso.com -GroupServiceAccountIdentifier contoso\ADFSService$ -OverwriteConfiguration -ErrorAction Stop  
```  
  
다음 단계: [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 2에서 AD FS 구성 후 작업](deploy-work-folders-adfs-step2.md)  
  
## <a name="see-also"></a>관련 항목  
[클라우드 폴더 개요](Work-Folders-Overview.md)  
  

