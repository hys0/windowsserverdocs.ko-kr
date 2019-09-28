---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Windows Server 2012 R2 AD FS 배포 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c549b52f697db889bf638470aca03f02e1323ed5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359731"
---
# <a name="configure-a-federation-server"></a>페더레이션 서버 구성

컴퓨터에 Active Directory Federation Services \(AD FS\) 역할 서비스를 설치한 후이 컴퓨터가 페더레이션 서버가 되도록 구성할 준비가 되었습니다. 다음 방법 중 하나를 수행할 수 있습니다.  
  
-   [새 페더레이션 서버 팜에서 첫 번째 페더레이션 서버 구성](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [기존 페더레이션 서버 팜에 페더레이션 서버 추가](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>새 페더레이션 서버 팜에서 첫 번째 페더레이션 서버 구성  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>Active Directory 페더레이션 서비스 구성 마법사를 사용 하 여 새 페더레이션 서버 팜에서 첫 번째 페더레이션 서버를 구성 하려면  
  
> [!NOTE]  
> 이 절차를 수행 하기 전에 도메인 관리자 권한 또는 도메인 관리자 자격 증명을 사용할 수 있는지 확인 하십시오.  
  
1.  서버 관리자 **대시보드** 페이지에서 **알림** 플래그를 클릭한 다음 **이 서버에 페더레이션 서비스를 구성하십시오.** 을 클릭합니다.  
  
    **Active Directory Federation Service 구성 마법사** 가 열립니다.  
  
2.  **시작** 페이지에서 **페더레이션 서버 팜에 첫 번째 페더레이션 서버를 만듭니다.** 를 선택하고 **다음**을 클릭합니다.  
  
3.  **AD DS에 연결** 페이지에서이 컴퓨터가 가입 된 Active Directory \(AD\) 도메인에 대 한 도메인 관리자 권한을 사용 하 여 계정을 지정 하 고 **다음**을 클릭 합니다.  
  
4.  **서비스 속성 지정** 페이지에서 다음을 수행한 후 **다음**을 클릭합니다.  
  
    -   이전에 얻은 보안 소켓 계층 \(SSL\) 인증서 및 키가 포함 된 .pfx 파일을 가져옵니다. 2 [단계: AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)에 대 한 SSL 인증서를 등록 하 고,이 인증서를 가져와 페더레이션 서버로 구성 하려는 컴퓨터에 복사 했습니다. 마법사를 통해 .pfx 파일을 가져오려면 **가져오기**를 클릭 한 다음 파일 위치를 찾습니다. 메시지가 표시 되 면 .pfx 파일의 암호를 입력 합니다.  
  
    -   페더레이션 서비스의 이름을 제공 합니다. 예를 들면 **fs.contoso.com**입니다. 이 이름은 인증서의 주체 또는 주체 대체 이름 중 하 나와 일치 해야 합니다.  
  
    -   페더레이션 서비스의 표시 이름을 제공 합니다. 예: **Contoso Corporation**. 사용자는 Active Directory Federation Services \(AD FS\) 로그인\-페이지에서이 이름을 볼 수 있습니다.  
  
5.  **서비스 계정 지정** 페이지에서 서비스 계정을 지정 합니다. 기존 그룹 관리 서비스 계정 \(gMSA\) 을 만들거나 사용 하거나 기존 도메인 사용자 계정을 사용할 수 있습니다. 새 gMSA 계정을 만드는 옵션을 선택 하는 경우 새 계정의 이름을 지정 합니다. 기존 gMSA 또는 도메인 계정을 사용 하는 옵션을 선택 하는 경우 **선택** 을 클릭 하 여 계정을 선택 합니다.  
  
    > [!NOTE]  
    > GMSA 계정을 사용 하는 경우의 혜택은 자동\-으로 협상 된 암호 업데이트 기능입니다.  
  
    > [!WARNING]  
    > GMSA 계정을 사용 하려면 환경에 Windows Server 2012 운영 체제를 실행 하는 도메인 컨트롤러가 하나 이상 있어야 합니다.  
    >   
    > GMSA 옵션을 사용 하지 않도록 설정 하 고 **KDS 루트 키가 설정 되지 않았기 때문에 그룹 관리 서비스 계정을 사용할 수 없다는**오류 메시지가 표시 되는 경우 도메인에서 다음 Windows PowerShell 명령을 실행 하 여 도메인에서 gMSA를 사용 하도록 설정할 수 있습니다. Active Directory 도메인 `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`에서 Windows Server 2012 이상을 실행 하는 컨트롤러입니다. 그런 다음 마법사로 돌아가 **이전**을 클릭 한 후 **다음** 을 클릭 하 여\- **서비스 계정 지정** 페이지를 다시 입력 합니다. 이제 gMSA 옵션을 사용 하도록 설정 해야 합니다. 이를 선택 하 고 사용 하려는 gMSA 계정 이름을 입력할 수 있습니다.  
  
6.  **구성 데이터베이스 지정** 페이지에서 AD FS 구성 데이터베이스를 지정 하 고 **다음**을 클릭 합니다. Windows 내부 데이터베이스 \(WID\)를 사용 하 여이 컴퓨터에 데이터베이스를 만들거나 Microsoft SQL Server의 위치 및 인스턴스 이름을 지정할 수 있습니다.  
  
    자세한 내용은 [AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우 SQL Server 2012 및 SQL Server 2014를 비롯 한 SQL Server 2008 이상 버전을 사용할 수 있습니다.  
  
7.  **검토 옵션** 페이지에서 구성 선택 사항을 확인하고 **다음**을 클릭합니다.  
  
8.  필수 구성 요소 확인 페이지에서 모든 필수 구성 요소 검사가 성공적으로 완료 되었는지 확인 하 고 **구성**을 클릭 합니다. **\-**  
  
9. **결과** 페이지에서 결과를 검토 하 고 구성이 성공적으로 완료 되었는지 확인 한 다음 **페더레이션 서비스 배포를 완료 하는 데 필요한 다음 단계**를 클릭 합니다. 자세한 내용은 [AD FS 설치를 완료 하기 위한 다음 단계](https://go.microsoft.com/fwlink/p/?LinkId=286704)를 참조 하세요. **닫기**를 클릭하여 마법사를 종료합니다.  
  
### <a name="BKMK_3"></a>Windows PowerShell을 통해 새 페더레이션 서버 팜에서 첫 번째 페더레이션 서버를 구성 하려면  
새 gMSA 계정이 나 기존 도메인 사용자 계정을 사용 하 여 새 페더레이션 서버 팜을 만들 수 있습니다.  
  
-   **새 gMSA 계정을 사용 하 여 새 페더레이션 서버를 만들려면 다음을 수행 합니다.**  
  
    > [!IMPORTANT]  
    > 새 페더레이션 서버 팜에서 첫 번째 페더레이션 서버를 만들려면 도메인 관리자 권한이 있어야 합니다.  
  
    1.  페더레이션 서버로 구성 하려는 컴퓨터에서 필요한 SSL 인증서를 **로컬 컴퓨터\\내 저장소** 디렉터리로 가져왔는지 확인 합니다. Windows PowerShell 명령 창 `dir Cert:\LocalMachine\My`에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 여부를 확인할 수 있습니다. 인증서는 **로컬 컴퓨터\\내 저장소** 디렉터리에 해당 지 문으로 나열 됩니다.  
  
    2.  도메인 컨트롤러에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 하 여 도메인 `Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`에 KDS 루트 키가 만들어졌는지 여부를 확인 합니다. 출력에 정보가 표시 되지 않도록 해당 파일을 만들지 않은 경우 다음 명령을 실행 하 여 키 `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`를 만듭니다.  
  
    3.  페더레이션 서버로 구성 하려는 컴퓨터에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > 이전 명령이 끝날 때 기호가필요합니다.`$`  
  
        에 대 한 `<certificate_thumbprint>`값을 가져오려면를 `dir Cert:\LocalMachine\My`실행 하 고 SSL 인증서의 지문을 선택 합니다. 값 `<federation_service_name>` 은 페더레이션 서비스의 이름 (예: **fs.contoso.com**)입니다.  
  
        > [!NOTE]  
        > 이 명령을 처음 실행 하는 경우 `OverwriteConfiguration` 매개 변수를 추가 합니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 팜을 만듭니다. SQL Server 서버 팜을 만들려면 이미 설치 되어 작동 중인 SQL Server 인스턴스가 있어야 합니다.  
        >   
        > 다음 명령을 사용 하 여 SQL Server 인스턴스를 사용 하는 새 팜에 첫 번째 페더레이션 서버를 만들 수 있습니다. 여기서 `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"` **< SQL\_\_호스트 이름 >** 은 SQL Server를 실행 하는 서버의 이름입니다. **SQL\_인스턴스\_이름 > <** SQL Server 인스턴스의 이름입니다. SQL Server의 기본 인스턴스를 사용 하는 경우 "**데이터\=원본 < SQL\_\_호스트 이름 >; 통합\=보안 True**"의 **SQLConnectionString** 값을 사용 합니다.  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용하여 구성 데이터를 저장하려면 SQL Server 2008 이상(SQL Server 2012 포함)을 사용하면 됩니다.  
  
-   **기존 도메인 사용자 계정을 사용 하 여 새 페더레이션 서버를 만들려는 경우 다음을 수행 합니다.**  
  
    1.  페더레이션 서버로 구성 하려는 컴퓨터에서 필요한 SSL 인증서를 **로컬 컴퓨터\\내 저장소** 디렉터리로 가져왔는지 확인 합니다. Windows PowerShell 명령 창 `dir Cert:\LocalMachine\My`에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 여부를 확인할 수 있습니다. 인증서는 **로컬 컴퓨터\\내 저장소** 디렉터리에 해당 지 문으로 나열 됩니다.  
  
    2.  페더레이션 서버로 구성 하려는 컴퓨터에서 Windows PowerShell 명령 창을 열고 다음 명령을 `$fscred = Get-Credential`실행 합니다. 도메인\\사용자 이름 형식으로 페더레이션 서비스 계정에 사용할 도메인 사용자 계정 자격 증명을 입력 합니다.  
  
    3.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행합니다.  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        **인증서\_지문 > <** 값을 얻으려면를 실행 `dir Cert:\LocalMachine\My`하 고 SSL 인증서의 지문을 선택 합니다. **< 페더레이션\_서비스\_이름 >** 의 값은 페더레이션 서비스의 이름 (예: fs.contoso.com)입니다.  
  
        > [!NOTE]  
        > 이 명령을 처음 실행 하는 경우 `OverwriteConfiguration` 매개 변수를 추가 합니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 팜을 만듭니다. SQL Server 팜을 만들려면 SQL Server 인스턴스를 이미 설치 하 고 작동 해야 합니다.  
        >   
        > 다음 명령을 사용 하 여 SQL Server 인스턴스를 사용 하는 새 팜에 첫 번째 페더레이션 서버를 만들 수 있습니다. 여기서 `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` **sql\_호스트\_Name** 은 SQL Server를 실행 하는 서버의 이름 및 sql입니다.  **인스턴스\_이름SQL Server 인스턴스의 이름입니다. \_** SQL Server의 기본 인스턴스를 사용 하는 경우 "**데이터\=원본 < SQL\_\_호스트 이름 >; 통합\=보안 True**"의 **SQLConnectionString** 값을 사용 합니다.  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우 SQL Server 2012 및 SQL Server 2014를 비롯 한 SQL Server 2008 이상 버전을 사용할 수 있습니다.  
  
## <a name="BKMK_2"></a>기존 페더레이션 서버 팜에 페더레이션 서버 추가  
  
> [!IMPORTANT]  
> 3 단계를 완료 [했는지 확인 합니다. 이 섹션의 절차를](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)시작 하기 전에 AD FS 역할 서비스를 설치 합니다.  
  
> [!IMPORTANT]  
> 이 절차를 완료 하기 전에 유효한 SSL 서버 인증 인증서를 가져왔는지 확인 합니다.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Active Directory 페더레이션 서비스 구성 마법사를 통해 기존 페더레이션 서버 팜에 페더레이션 서버를 추가 하려면  
  
1.  서버 관리자 **대시보드** 페이지에서 **알림** 플래그를 클릭한 다음 **이 서버에 페더레이션 서비스를 구성하십시오.** 을 클릭합니다.  
  
    **Active Directory Federation Service 구성 마법사** 가 열립니다.  
  
2.  **시작** 페이지에서 페더레이션 서버 **팜에 페더레이션 서버 추가**를 선택 하 고 **다음**을 클릭 합니다.  
  
3.  **AD DS에 연결** 페이지에서이 컴퓨터가 가입 된 AD 도메인에 대 한 도메인 관리자 권한을 사용 하 여 계정을 지정 하 고 **다음**을 클릭 합니다.  
  
4.  **팜 지정** 페이지에서 WID를 사용 하는 팜의 기본 페더레이션 서버 이름을 제공 하거나 데이터베이스 호스트 이름과 SQL Server를 사용 하는 기존 페더레이션 서버 팜의 데이터베이스 인스턴스 이름을 지정 합니다.  
  
    > [!WARNING]  
    > Windows Server® 2012 r 2에서는 SQL Server의 기본 인스턴스를 지정 하는 해결 방법이 있습니다. 해결 방법은 사용자 인터페이스를 사용 하지 않는 것입니다. 대신의 단계를 사용 [하 여 Windows PowerShell을 통해 새 페더레이션 서버 팜에서 첫 번째 페더레이션 서버를 구성](Configure-a-Federation-Server.md#BKMK_3)합니다.  
  
    > [!IMPORTANT]  
    > AD FS 팜을 만들고 SQL Server를 사용하여 구성 데이터를 저장하려면 SQL Server 2008 이상(SQL Server 2012 포함)을 사용하면 됩니다.  
  
5.  **Ssl 인증서 지정** 페이지에서 이전에 얻은 ssl 인증서 및 키가 포함 된 .pfx 파일을 가져옵니다. 이 인증서는 필수 서비스 인증 인증서입니다. 2 [단계: AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)에 대 한 SSL 인증서를 등록 하 고,이 인증서를 가져와 페더레이션 서버로 구성 하려는 컴퓨터에 복사 했습니다. 마법사를 통해 .pfx 파일을 가져오려면 **가져오기** 를 클릭 하 고 파일의 위치를 찾습니다. 메시지가 표시 되 면 .pfx 파일의 암호를 입력 합니다.  
  
6.  **서비스 계정 지정** 페이지에서 팜의 첫 번째 페더레이션 서버를 만들 때 구성한 것과 같은 서비스 계정을 지정 합니다. 기존 그룹 관리 서비스 계정 또는 기존 도메인 사용자 계정을 사용할 수 있습니다.  
  
    > [!IMPORTANT]  
    > 지정 하는 계정은이 팜의 기본 페더레이션 서버에서 사용 되는 계정과 동일한 계정 이어야 합니다.  
  
7.  **검토 옵션** 페이지에서 구성 선택 사항을 확인하고 **다음**을 클릭합니다.  
  
8.  필수 구성 요소 확인 페이지에서 모든 필수 구성 요소 검사가 성공적으로 완료 되었는지 확인 하 고 **구성**을 클릭 합니다. **\-**  
  
9. **결과** 페이지에서 결과를 검토 하 고 구성이 성공적으로 완료 되었는지 확인 한 다음 **페더레이션 서비스 배포를 완료 하는 데 필요한 다음 단계**를 클릭 합니다. 자세한 내용은 [AD FS 설치를 완료 하기 위한 다음 단계](https://go.microsoft.com/fwlink/p/?LinkId=286704)를 참조 하세요. **닫기**를 클릭하여 마법사를 종료합니다.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Windows PowerShell을 통해 기존 페더레이션 서버 팜에 페더레이션 서버를 추가 하려면  
기존 gMSA 계정이 나 기존 도메인 사용자 계정을 사용 하 여 기존 팜에 페더레이션 서버를 추가할 수 있습니다.  
  
-   기존 gMSA 계정을 사용 하 여 페더레이션 서버를 팜에 연결 하려면 다음을 수행 합니다.  
  
    1.  페더레이션 서버로 구성 하려는 컴퓨터에서 필요한 SSL 인증서를 **로컬 컴퓨터\\내 저장소** 디렉터리로 가져왔는지 확인 합니다. Windows PowerShell 명령 창 `dir Cert:\LocalMachine\My`에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 여부를 확인할 수 있습니다. 인증서는 **로컬 컴퓨터\\내 저장소** 디렉터리에 해당 지 문으로 나열 됩니다.  
  
    2.  페더레이션 서버로 구성 하려는 컴퓨터에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>`는 AD 도메인 및 해당 도메인에 있는 gMSA 계정의 이름입니다. `<first_federation_server_hostname>`이 기존 팜에 있는 기본 페더레이션 서버의 호스트 이름입니다.  
  
        이전 단계에서를 실행 `<certificate_thumbprint>` `dir Cert:\LocalMachine\My` 하 여에 대 한 값을 가져올 수 있습니다.  
  
        > [!NOTE]  
        > 이 명령을 처음 실행 하는 경우 `OverwriteConfiguration` 매개 변수를 추가 합니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 팜 노드를 만듭니다. SQL Server를 실행 하는 컴퓨터의 서버 팜 노드를 만들려는 경우 SQL Server 인스턴스가 이미 설치 되어 있고 작동 해야 합니다.  
        >   
        > 다음 명령을 사용 하 여 SQL Server 인스턴스를 사용 하는 기존 팜에 페더레이션 서버를 추가할 수 있습니다. 여기서 `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` **sql\_호스트\_Name** 은 SQL Server를 실행 하는 서버의 이름 및 sql입니다.  **인스턴스\_이름SQL Server 인스턴스의 이름입니다. \_** SQL Server의 기본 인스턴스를 사용 하는 경우 "**데이터\=원본 < SQL\_\_호스트 이름 >; 통합\=보안 True**"의 **SQLConnectionString** 값을 사용 합니다.  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우 SQL Server 2012 및 SQL Server 2014를 비롯 한 SQL Server 2008 이상 버전을 사용할 수 있습니다.  
  
-   기존 도메인 사용자 계정을 사용 하 여 페더레이션 서버를 팜에 연결 하려면 다음을 수행 합니다.  
  
    1.  페더레이션 서버로 구성할 컴퓨터에서 Windows PowerShellcommand 창을 열고 다음 명령을 `$fscred = get-credential`실행 합니다. 합니다. 도메인\\사용자 이름 형식으로 페더레이션 서비스 계정에 사용할 도메인 사용자 계정 자격 증명을 입력 합니다.  
  
    2.  페더레이션 서버로 구성 하려는 컴퓨터에서 필요한 SSL 인증서를 **로컬 컴퓨터\\내 저장소** 디렉터리로 가져왔는지 확인 합니다. Windows PowerShellcommand 창 `dir Cert:\LocalMachine\My`에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 여부를 확인할 수 있습니다. 인증서는 **로컬 컴퓨터\\내 저장소** 디렉터리에 해당 지 문으로 나열 됩니다.  
  
    3.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > 이 명령을 처음 실행 하는 경우 `OverwriteConfiguration` 매개 변수를 추가 합니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 팜 노드를 만듭니다. SQL Server를 실행 하는 컴퓨터의 서버 팜 노드를 만들려는 경우 SQL Server 인스턴스가 이미 설치 되어 있고 작동 해야 합니다. SQL Server 인스턴스를 사용 하 여 기존 팜에 페더레이션 서버를 추가 하려면 다음 명령을 사용할 수 있습니다. 여기서 `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` **\_SQL 호스트\_Name** 은 SQL Server의 인스턴스가 실행 되 고 있는 서버의 이름입니다. **SQL\_인스턴스\_이름** SQL Server 인스턴스의 이름입니다. SQL Server의 기본 인스턴스를 사용 하는 경우 "**데이터\=원본 < SQL\_\_호스트 이름 >; 통합\=보안 True**"의 **SQLConnectionString** 값을 사용 합니다.  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우 SQL Server 2012 및 SQL Server 2014를 비롯 한 SQL Server 2008 이상 버전을 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

