---
title: AD FS 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더 배포 - 3단계, 클라우드 폴더 설치
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: 5a43b104-4d02-4d73-a385-da1cfb67e341
ms.openlocfilehash: d6b21579fb1dedc777733317e7222debd8d944a1
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812670"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-3-set-up-work-folders"></a>AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 3, 작업 폴더 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 AD FS(Active Directory Federation Services) 및 웹 응용 프로그램 프록시를 사용하여 클라우드 폴더를 배포하는 세 번째 단계를 설명합니다. 이 과정의 다른 단계는 다음 항목에서 찾을 수 있습니다.  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 개요](deploy-work-folders-adfs-overview.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 1 단계, AD FS 설정](deploy-work-folders-adfs-step1.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 단계 2에서 AD FS 구성 후 작업](deploy-work-folders-adfs-step2.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 4 단계, 웹 응용 프로그램 프록시 설정](deploy-work-folders-adfs-step4.md)  
  
-   [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 5 단계 클라이언트 설정](deploy-work-folders-adfs-step5.md)  
  
> [!NOTE]
>   Windows Server 2019 또는 Windows Server 2016 환경에 대 한 지침은이 섹션에서 설명 합니다. Windows Server 2012 R2를 사용하는 경우 [Windows Server 2012 R2 instructions(Windows Server 2012 R2 지침)](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx)을 따르세요.

클라우드 폴더를 설정하려면 다음 절차를 수행합니다.  
  
## <a name="pre-installment-work"></a>사전 설치 작업  
클라우드 폴더를 설치하려면 해당 도메인에 가입되어 있고 Windows Server 2016을 실행하는 서버가 필요합니다. 서버에 유효한 네트워크 구성이 있어야 합니다.  
  
테스트 예제의 경우 클라우드 폴더를 실행할 컴퓨터를 Contoso 도메인에 가입하고 다음 섹션에 설명된 대로 네트워크 인터페이스를 설정하면 됩니다. 

### <a name="set-the-server-ip-address"></a>서버 IP 주소 설정  
서버 IP 주소를 고정 IP 주소로 변경합니다. 테스트 예를 들어 192.168.0.170 인 IP 클래스 A를 사용 하 여 / 서브넷 마스크: 255.255.0.0/기본 게이트웨이: 192.168.0.1/DNS를 기본 설정: 192.168.0.150 (도메인 컨트롤러의 IP 주소). 
  
### <a name="create-the-cname-record-for-work-folders"></a>클라우드 폴더의 CNAME 레코드 만들기  
클라우드 폴더의 CNAME 레코드를 만들려면 다음 단계를 따릅니다.  
  
1.  도메인 컨트롤러에서 **DNS 관리자**를 엽니다.  
  
2.  정방향 조회 영역 폴더를 확장하고 도메인을 마우스 오른쪽 단추로 클릭한 다음 **새 별칭(CNAME)** 을 클릭합니다.  
  
3.  **새 리소스 레코드** 창의 **별칭 이름** 필드에 클라우드 폴더의 별칭을 입력합니다. 테스트 예제에서는 **workfolders**입니다.  
  
4.  **정규화된 도메인 이름** 필드의 값은 **workfolders.contoso.com**이어야 합니다.  
  
5.  **대상 호스트의 정규화된 도메인 이름** 필드에 클라우드 폴더 서버의 FQDN을 입력합니다. 이 예제에서는 **2016-WF.contoso.com**입니다.  
  
6.  **확인**을 클릭합니다.  
  
Windows PowerShell을 사용하여 해당 단계를 수행하려면 다음 명령을 사용합니다. 이 명령은 도메인 컨트롤러에서 실행해야 합니다.  
  
```powershell  
Add-DnsServerResourceRecord  -ZoneName "contoso.com" -Name workfolders -CName  -HostNameAlias 2016-wf.contoso.com   
```  
  
### <a name="install-the-ad-fs-certificate"></a>AD FS 인증서 설치  
AD FS를 설치하는 동안 만든 AD FS 인증서를 다음 단계에 따라 로컬 컴퓨터 인증서 저장소에 설치합니다.  
  
1.  **시작**을 클릭한 다음 **실행**을 클릭합니다.  
  
2.  **MMC**를 입력합니다.  
  
3.  **파일** 메뉴에서 **스냅인 추가/제거**를 클릭합니다.  
  
4.  **사용 가능한 스냅인** 목록에서 **인증서**를 선택한 다음 **추가**를 클릭합니다. 인증서 스냅인 마법사가 시작됩니다.  
  
5.  **컴퓨터 계정**을 선택한 다음 **다음**을 클릭합니다.  
  
6.  **로컬 컴퓨터: (이 콘솔이 실행되고 있는 컴퓨터)** 를 선택하고 **마침**을 클릭합니다.  
  
7.  **확인**을 클릭합니다.  
  
8.  **Console Root\Certificates\(Local Computer)\Personal\Certificates** 폴더를 확장합니다.  
  
9. **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **가져오기**를 클릭합니다.  
  
10. AD FS 인증서가 들어 있는 폴더를 찾은 후 마법사의 지침에 따라 파일을 가져와서 인증서 저장소에 배치합니다.

11. **Console Root\Certificates\(Local Computer)\Trusted Root Certification Authorities\Certificates** 폴더를 확장합니다.  
  
12. **인증서**를 마우스 오른쪽 단추로 클릭하고 **모든 작업**을 클릭한 다음 **가져오기**를 클릭합니다.  
  
13. AD FS 인증서가 들어 있는 폴더를 찾은 후 마법사의 지침에 따라 파일을 가져와서 신뢰할 수 있는 루트 인증 기관 저장소에 배치합니다.  
  
### <a name="create-the-work-folders-self-signed-certificate"></a>클라우드 폴더 자체 서명된 인증서 만들기  
클라우드 폴더 자체 서명된 인증서를 만들려면 다음 단계를 따릅니다.  
  
1.  [AD FS 및 WAP(웹 응용 프로그램 프록시)를 사용하여 클라우드 폴더 배포](https://blogs.technet.microsoft.com/filecab/2014/03/03/deploying-work-folders-with-ad-fs-and-web-application-proxy-wap) 블로그 게시물에 제공된 스크립트를 다운로드한 다음 makecert.ps1 파일을 클라우드 폴더 컴퓨터로 복사합니다.  
  
2.  관리자 권한으로 Windows PowerShell 창을 엽니다.  
  
3.  실행 정책을 제한 없음으로 설정합니다.  
  
    ```powershell  
    PS C:\temp\scripts> Set-ExecutionPolicy -ExecutionPolicy Unrestricted   
    ```  
  
4.  스크립트를 복사한 디렉터리로 변경합니다.  
  
5.  makeCert 스크립트를 실행합니다.  
  
    ```powershell  
    PS C:\temp\scripts> .\makecert.ps1  
    ```  
  
6.  주체 인증서를 변경하라는 메시지가 나타나면 새로운 주체 값을 입력합니다. 이 예의 값은 **workfolders.contoso.com**입니다.  
  
7.  SAN(주체 대체 이름) 이름을 입력하라는 메시지가 나타나면 Y를 누른 다음 SAN 이름을 한 번에 하나씩 입력합니다.  
  
    이 예에서는 **workfolders.contoso.com**을 입력하고 Enter 키를 누릅니다. 그런 다음 **2016-WF.contoso.com**을 입력하고 Enter 키를 누릅니다.  
  
    모든 SAN 이름을 입력한 후 빈 줄에서 Enter 키를 누릅니다.  
  
8.  신뢰할 수 있는 루트 인증 기관 저장소에 인증서를 설치하라는 메시지가 나타나면 Y를 누릅니다.  
  
클라우드 폴더 인증서는 다음 값을 가진 SAN 인증서여야 합니다.  
  
-   **workfolders**.**domain**  
  
-   **machine name**.**domain**  
  
테스트 예제의 값은 다음과 같습니다.  
  
-   **workfolders.contoso.com**  
  
-   **2016-WF.contoso.com**  
  
## <a name="install-work-folders"></a>클라우드 폴더 설치  
클라우드 폴더 역할을 설치하려면 다음 단계를 따릅니다.  
  
1.  **서버 관리자**를 열고 **역할 및 기능 추가**를 클릭한 후 **다음**을 클릭합니다.  
  
2.  **설치 유형** 페이지에서 **역할 기반 또는 기능 기반 설치**를 선택하고 **다음**을 클릭합니다.  
  
3.  **서버 선택** 페이지에서 현재 서버를 선택하고 **다음**을 클릭합니다.  
  
4.  **서버 역할** 페이지에서 **파일 및 저장소 서비스**를 확장하고 **파일 및 iSCSI 서비스**를 확장한 다음 **클라우드 폴더**를 선택합니다.  
  
5.  **역할 및 기능 추가 마법사** 페이지에서 **기능 추가**, **다음**을 차례로 클릭합니다.  
  
6.  **기능** 페이지에서 **다음**을 클릭합니다.  
  
7.  **확인** 페이지에서 **설치**를 클릭합니다.  
  
## <a name="configure-work-folders"></a>클라우드 폴더 구성  
클라우드 폴더를 구성하려면 다음 단계를 따릅니다.  
  
1.  **서버 관리자**를 엽니다.  
  
2.  **파일 및 저장소 서비스**를 선택한 다음 **클라우드 폴더**를 선택합니다.  
  
3.  **클라우드 폴더** 페이지에서 **새 동기화 공유 마법사**를 시작하고 **다음**을 클릭합니다.  
  
4.  **서버 및 경로** 페이지에서 동기화 공유를 만들 서버를 선택하고, 클라우드 폴더 데이터를 저장할 로컬 경로를 입력하고, **다음**을 클릭합니다.  
  
    해당 경로가 없는 경우 만들라는 메시지가 표시됩니다. **확인**을 클릭합니다.  
  
5.  **사용자 폴더 구조** 페이지에서 **사용자 별칭**을 선택하고 **다음**을 클릭합니다.  
  
6.  **동기화 공유 이름** 페이지에서 동기화 공유의 이름을 입력합니다. 테스트 예제에서는 **WorkFolders**입니다. **다음**을 클릭합니다.  
  
7.  **동기화 액세스** 페이지에서 새 동기화 공유에 액세스할 사용자 또는 그룹을 추가합니다. 테스트 예제에서는 모든 도메인 사용자에게 권한을 부여하겠습니다. **다음**을 클릭합니다.  
  
8.  **PC 보안 정책** 페이지에서 **클라우드 폴더 암호화**, **자동으로 화면 잠금 및 암호 설정**을 차례로 선택합니다. **다음**을 클릭합니다.  
  
9. **확인** 페이지에서 **만들기**를 클릭하여 구성 절차를 마칩니다.  
  
## <a name="work-folders-post-configuration-work"></a>클라우드 폴더 구성 후 작업  
클라우드 폴더 설치를 완료하려면 다음과 같은 추가 단계를 완료해야 합니다.  
  
-   클라우드 폴더 인증서를 SSL 포트에 연결  
  
-   AD FS 인증을 사용하도록 클라우드 폴더 구성  
  
-   클라우드 폴더 인증서 내보내기(자체 서명된 인증서를 사용하는 경우)  
  
### <a name="bind-the-certificate"></a>인증서 연결  
클라우드 폴더는 SSL을 통해서만 통신하며 사용자가 이전에 만든(또는 인증서 기관에서 발급한) 자체 서명된 인증서가 포트에 연결되어야 합니다.  
  
사용 하 여 Windows PowerShell을 통해 포트에 인증서를 바인딩할 수 있는 방법은 두 가지가 있습니다. IIS cmdlet 및 netsh 합니다.  
  
#### <a name="bind-the-certificate-by-using-netsh"></a>netsh를 사용하여 인증서 연결  
Windows PowerShell에서 netsh 명령줄 스크립팅 유틸리티를 사용하려면 명령을 netsh에 파이프해야 합니다. 다음은 netsh를 사용하여 주체가 **workfolders.contoso.com**인 인증서를 찾아서 443 포트에 연결하는 예제 스크립트입니다.  
  
```powershell  
$subject = "workfolders.contoso.com"   
Try  
{  
#In case there are multiple certificates with the same subject, get the latest version   
$cert = Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match $subject} | sort $_.NotAfter -Descending | select -first 1    
$thumbprint = $cert.Thumbprint  
$Command = "http add sslcert ipport=0.0.0.0:443 certhash=$thumbprint appid={CE66697B-3AA0-49D1-BDBD-A25C8359FD5D} certstorename=MY"  
$Command | netsh  
}  
Catch  
{  
"     Error: unable to locate certificate for $($subject)"  
Exit  
}   
```  
  
#### <a name="bind-the-certificate-by-using-iis-cmdlets"></a>IIS cmdlet을 사용하여 인증서 연결  
IIS 관리 도구 및 스크립트를 설치한 경우에 제공되는 IIS 관리 cmdlet을 사용하여 인증서를 포트에 연결할 수도 있습니다.  
  
> [!NOTE]  
> IIS 관리 도구를 설치해도 클라우드 폴더 컴퓨터에서 IIS(인터넷 정보 서비스) 전체 버전을 사용할 수 있는 것은 아니며 관리 cmdlet만 사용할 수 있습니다. 이 도구를 설치하면 몇 가지 이점이 있습니다. 예를 들어 netsh에서 얻은 기능을 제공하기 위해 cmdlet을 검색할 수 있습니다. New-WebBinding cmdlet을 통해 인증서가 포트에 연결되면 해당 연결은 어떤 식으로든 IIS에 따라 좌우되지 않습니다. 인증서를 연결한 후에는 Web-Mgmt-Console 기능을 제거해도 인증서가 계속 포트에 연결되어 있습니다. netsh를 통해 **netsh http show sslcert**를 입력하여 연결을 검사할 수 있습니다.  
  
다음은 New-WebBinding cmdlet을 사용하여 주체가 **workfolders.contoso.com**인 인증서를 찾아서 443 포트에 연결하는 예제입니다.  
  
```powershell  
$subject = "workfolders.contoso.com"  
Try  
{  
#In case there are multiple certificates with the same subject, get the latest version   
$cert =Get-ChildItem CERT:\LocalMachine\My |where {$_.Subject -match $subject } | sort $_.NotAfter -Descending | select -first 1   
$thumbprint = $cert.Thumbprint  
New-WebBinding -Name "Default Web Site" -IP * -Port 443 -Protocol https  
#The default IIS website name must be used for the binding. Because Work Folders uses Hostable Web Core and its own configuration file, its website name, 'ECSsite', will not work with the cmdlet. The workaround is to use the default IIS website name, even though IIS is not enabled, because the NewWebBinding cmdlet looks for a site in the default IIS configuration file.   
Push-Location IIS:\SslBindings  
Get-Item cert:\LocalMachine\MY\$thumbprint | new-item *!443  
Pop-Location  
}  
Catch  
{  
"     Error: unable to locate certificate for $($subject)"  
Exit  
}   
```  
  
### <a name="set-up-ad-fs-authentication"></a>AD FS 인증 설정  
AD FS 인증을 사용하도록 클라우드 폴더를 구성하려면 다음 단계를 따릅니다.  
  
1.  **서버 관리자**를 엽니다.  
  
2.  **서버**를 클릭한 다음 목록에서 클라우드 폴더 서버를 선택합니다.  
  
3.  서버 이름을 마우스 오른쪽 단추로 클릭하고 **클라우드 폴더 설정**을 클릭합니다.  
  
4.  **클라우드 폴더 설정** 창에서 **Active Directory Federation Services**를 선택하고 페더레이션 서비스 URL을 입력합니다. **적용**을 클릭합니다.  
  
    URL은 테스트 예에서 **https://blueadfs.contoso.com** 합니다.  
  
Windows PowerShell을 통해 같은 작업을 수행하는 cmdlet은 다음과 같습니다.  
  
```powershell  
Set-SyncServerSetting -ADFSUrl "https://blueadfs.contoso.com"   
```  
  
자체 서명된 인증서를 사용하여 AD FS를 설정하는 경우 페더레이션 서비스 URL이 잘못되어 연결할 수 없다거나 신뢰 당사자 트러스트가 설치되지 않았다는 오류 메시지가 나타날 수 있습니다.  
  
클라우드 폴더 서버에 AD FS 인증서가 설치되지 않았거나 AD FS의 CNAME이 올바르게 설정되지 않은 경우에도 이 오류가 발생할 수 있습니다. 계속 진행하기 전에 이러한 문제를 수정해야 합니다.  
  
### <a name="export-the-work-folders-certificate"></a>클라우드 폴더 인증서 내보내기  
나중에 테스트 환경에서 다음 컴퓨터에 설치할 수 있도록 자체 서명된 클라우드 폴더 인증서를 내보내야 합니다.  
  
-   웹 응용 프로그램 프록시에 사용되는 서버  
  
-   도메인에 가입된 Windows 클라이언트  
  
-   도메인에 가입되지 않은 Windows 클라이언트  
  
인증서를 내보내려면에 설명 된 대로 이전에 AD FS 인증서 내보내기에 사용 되는 동일한 단계를 수행 [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포: 단계 2에서 AD FS 구성 후 작업](deploy-work-folders-adfs-step2.md), AD FS 인증서를 내보냅니다.  
  
다음 단계: [AD FS 및 웹 응용 프로그램 프록시를 사용 하 여 클라우드 폴더 배포 합니다. 4 단계, 웹 응용 프로그램 프록시 설정](deploy-work-folders-adfs-step4.md)  
  
## <a name="see-also"></a>관련 항목  
[클라우드 폴더 개요](Work-Folders-Overview.md)  
  

