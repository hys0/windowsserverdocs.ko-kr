---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: "지침에 따라 Windows Server 2012 r 2 광고 FS 배포"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13ce514dc5f3f70217a26c898cde6fe24d4967c6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-a-federation-server"></a>Federation 서버 구성

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

컴퓨터에 Active Directory Federation Services \(AD FS\) 역할 서비스를 설치한 후이 컴퓨터 federation 서버를 구성 준비가 됩니다. 다음 중 하나를 수행할 수 있습니다.  
  
-   [새 federation 서버 농장의 첫 번째 federation 서버 구성](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [기존 federation 서버 팜 federation 서버를 추가](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>새 federation 서버 농장의 첫 번째 federation 서버 구성  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>Active Directory Federation 서비스 구성 마법사를 사용 하 여 새 federation 서버 농장의 첫 번째 federation 서버 구성 하려면  
  
> [!NOTE]  
> 관리자 권한이 도메인 없거나이 절차를 수행 하기 전에 도메인 관리자 자격 증명 사용할 수 있는 있는지 확인 합니다.  
  
1.  서버 관리자에서 **대시보드** 페이지, 클릭는 **알림**, 플래그 지정 및 클릭 한 다음 **서버의 federation 서비스 구성**합니다.  
  
    **Active Directory Federation 서비스 구성 마법사** 열립니다.  
  
2.  에 **시작** 페이지를 선택 하 고 **federation 서버 농장의 첫 번째 federation 서버를 만들**을 차례로 클릭 하 고 **다음**합니다.  
  
3.  에 **AD DS에 연결** 페이지, 클릭 하 고이 컴퓨터에 가입 된, Active Directory \(AD\) 도메인에 대 한 관리자 권한이 도메인을 사용 하 여 계정을 지정 **다음**합니다.  
  
4.  에 **서비스 속성 지정** 페이지에서 다음을 수행 하 고 클릭 한 다음 **다음 **:  
  
    -   이전 받은 키와 Secure Socket 계층 \(SSL\) 인증서 포함 된.pfx 파일을 가져옵니다. [2 단계: adfs SSL 인증서 등록](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md),이 인증서을 federation 서버 구성 하려면 컴퓨터에 복사 합니다. 마법사를 통해.pfx 파일을 가져오려면 클릭 **가져오기**, 다음 해당 파일의 위치를 찾습니다. 메시지가 표시 되 면.pfx 파일의 암호를 입력 합니다.  
  
    -   이름을 federation 서비스를 제공 합니다. 예를 들어, **fs.contoso.com**합니다. 이 이름은 제목이 나 인증서에 대체 이름 주제 중 하나 일치 해야 합니다.  
  
    -   표시 이름을 federation 서비스를 제공 합니다. 예를 들어, **Contoso Corporation**합니다. 사용자가 Active Directory Federation Services \(AD FS\) sign\에이 이름이 표시-페이지에 있습니다.  
  
5.  에 **서비스 계정 지정** 페이지에서 서비스 계정을 지정 합니다. 만들기 하거나 기존 그룹 관리 서비스 계정 \(gMSA\) 사용 하거나 기존 도메인 사용자 계정을 사용 합니다. 새 gMSA 계정을 생성 하는 옵션을 선택 하면 새 계정의 이름을 지정 합니다. 기존 gMSA 또는 도메인 계정을 사용 하는 옵션을 선택 하면 클릭 **선택** 계정을 선택 합니다.  
  
    > [!NOTE]  
    > GMSA 계정을 사용 하 여의 혜택은 해당 암호 auto\ 협상 업데이트 기능입니다.  
  
    > [!WARNING]  
    > GMSA 계정을 사용 하려는 경우 Windows Server 2012 운영 체제를 실행 하는 환경에서 하나 이상의 도메인 컨트롤러가 있어야 합니다.  
    >   
    > GMSA 옵션을 해제 하 고과 같은 오류 메시지가 표시 되는 경우 **그룹 관리 서비스 계정 사용할 수 없는 KDS 루트 키 설정 되지 않았으므로**, Windows Server 2012를 실행 하는 도메인 컨트롤러에서 이상, Active Directory 도메인에 다음과 같은 Windows PowerShell 명령을 실행 하 여 gMSA 도메인에 사용할 수 있습니다: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`합니다. 다음 돌아가기 마법사를 클릭 **이전**을 차례로 클릭 하 고 **다음** re\를-입력는 **지정 서비스 계정** 페이지 합니다. GMSA 옵션이 이제 활성화 됩니다. 선택 하 고 사용 하 여 원하는 gMSA 계정 이름을 입력 합니다.  
  
6.  에 **구성 데이터베이스 지정** 페이지를 지정 ADFS 구성 데이터베이스를 클릭 한 다음 **다음**합니다. 하면 데이터베이스가이 컴퓨터에서 Windows 내부 데이터베이스 \(WID\)를 사용 하 여 만들거나 위치와 Microsoft SQL Server 인스턴스 이름을 지정할 수 있습니다.  
  
    자세한 내용은 참조 [AD FS 구성 데이터베이스의 The 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)합니다.  
  
    > [!IMPORTANT]  
    > ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 2014 SQL Server, SQL Server 2012 등 최신 버전을 사용할 수 있습니다.  
  
7.  에 **리뷰 옵션** 페이지 구성 선택을 확인 하 고 클릭 한 다음 **다음**합니다.  
  
8.  에 **Pre\ 필수 조건 검사** 페이지에서 확인 모든 필수 검사를 성공적으로 완료 한 다음 클릭 **구성**합니다.  
  
9. 에 **결과** 페이지 결과 검토 하 고 구성 성공적으로 완료 있는지 여부를 확인 하 고 클릭 한 다음 **다음 단계를 완료 federation 서비스 배포 하는 데 필요한**합니다. 자세한 내용은 참조 [ADFS 설치를 완료 하기 위해 다음 단계](https://go.microsoft.com/fwlink/p/?LinkId=286704)합니다. 클릭 **닫기** 마법사를 종료 합니다.  
  
### <a name="BKMK_3"></a>Windows PowerShell를 통해 새로운 federation 서버 그룹에서 첫 번째 federation 서버 구성 하려면  
새 federation 서버 팜 새로운 기능이 나 기존 gMSA 계정이 나 기존 도메인 사용자 계정을 사용 하 여 만들 수 있습니다.  
  
-   **새 gMSA 계정을 사용 하 여 새 federation 서버 만들려는 경우 다음을 수행 합니다.**  
  
    > [!IMPORTANT]  
    > 도메인에 새 federation 서버 발전소의 첫 번째 federation 서버를 만들 관리자 권한이 있어야 합니다.  
  
    1.  Federation 서버로 구성 컴퓨터에 필요한 SSL 인증서를 가져온 후에 있는지 확인는 **로컬 Computer\\My 스토어** 디렉터리 합니다. Windows PowerShell 명령 창에서 다음 명령을 실행 하 여 ssl 가져온 후에 있는지 여부를 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서에는 지문 표시 되는 **로컬 Computer\\My 스토어** 디렉터리 합니다.  
  
    2.  도메인 컨트롤러에서 Windows PowerShell 명령 창 열고 KDS 루트 키 도메인에서 생성 된 있는지 여부를 확인 하려면 다음 명령을 실행: `Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`합니다. 키를 만드는 다음 명령을 실행 되지 만든 출력 정보는 없음 표시 되도록를: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`합니다.  
  
    3.  Federation 서버 구성 하려면 컴퓨터에서 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > `$`기호 이전 명령 끝날 때가 필요 합니다.  
  
        에 대 한 값을 얻기 위해 `<certificate_thumbprint>`, 실행 `dir Cert:\LocalMachine\My`를 선택한 다음 SSL 인증서의 지문 합니다. 값 `<federation_service_name>`이름인 federation 서비스의 예를 들어, **fs.contoso.com**합니다.  
  
        > [!NOTE]  
        > 이 명령을 실행 하는 처음으로 없는 경우 추가 `OverwriteConfiguration`매개 합니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 농장 합니다. 서버 SQL Server 팜 만들기 하려는 경우 이미 설치 되 고 작동 SQL Server 인스턴스가 있어야 합니다.  
        >   
        > 다음 명령을 사용 하 여 서버를 만드는 첫 번째 federation SQL Server 인스턴스를 사용 하는 새 그룹에: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"`어디 **< SQL\_Host\_Name >** SQL Server을 실행 하는 서버 이름 및 **< SQL\_instance\_name >** SQL Server 인스턴스의 이름입니다. 기본 SQL Server 인스턴스를 사용 하는 경우는 **포트가** 값 "**데이터 Source\ < SQL\_Host\_Name > =; 통합 Security\ 않게**" 합니다.  
  
        > [!IMPORTANT]  
        > ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 SQL Server 2012를 포함 하 여 최신 버전을 사용할 수 있습니다.  
  
-   **기존 도메인 사용자 계정을 사용 하 여 새 federation 서버 만들려는 경우 다음을 수행 합니다.**  
  
    1.  Federation 서버로 구성 컴퓨터에 필요한 SSL 인증서를 가져온 후에 있는지 확인는 **로컬 Computer\\My 스토어** 디렉터리 합니다. Windows PowerShell 명령 창에서 다음 명령을 실행 하 여 ssl 가져온 후에 있는지 여부를 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서에는 지문 표시 되는 **로컬 Computer\\My 스토어** 디렉터리 합니다.  
  
    2.  Federation 서버 구성 하려면 컴퓨터에서 Windows PowerShell 명령 창을 연 다음 명령을 실행: `$fscred = Get-Credential`합니다. 형식 domain\\user 이름에 해당 federation 서비스 계정 하려는 도메인 사용자 계정 자격 증명을 입력 합니다.  
  
    3.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        에 대 한 값을 얻기 위해 **< certificate\_thumbprint >**, 실행 `dir Cert:\LocalMachine\My`를 선택한 다음 SSL 인증서의 지문 합니다. 값 **< federation\_service\_name >** federation 서비스를 fs.contoso.com 등의 이름입니다.  
  
        > [!NOTE]  
        > 이 명령을 실행 하는 처음으로 없는 경우 추가 `OverwriteConfiguration`매개 합니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 농장 합니다. SQL Server 팜 만들기 하려는 경우 이미 설치 되 고 작동 SQL Server 인스턴스가 있어야 합니다.  
        >   
        > 다음 명령을 사용 하 여 서버를 만드는 첫 번째 federation SQL Server 인스턴스를 사용 하는 새 그룹에: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`어디 **SQL\_Host\_Name** SQL Server을 실행 하는 서버 이름 및 **SQL\_instance\_name** SQL Server 인스턴스의 이름입니다. 기본 SQL Server 인스턴스를 사용 하는 경우는 **포트가** 값 "**데이터 Source\ < SQL\_Host\_Name > =; 통합 Security\ 않게**" 합니다.  
  
        > [!IMPORTANT]  
        > ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 2014 SQL Server, SQL Server 2012 등 최신 버전을 사용할 수 있습니다.  
  
## <a name="BKMK_2"></a>기존 federation 서버 팜 federation 서버를 추가  
  
> [!IMPORTANT]  
> 완료 한 [3 단계: ADFS 역할 서비스 설치](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md),이 섹션의이 절차를 시작 하기 전에 합니다.  
  
> [!IMPORTANT]  
> 갖고 유효한 SSL 서버 인증 인증서가이 절차를 수행 하기 전에 있는지 확인 합니다.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Federation 서버 Active Directory Federation 서비스 구성 마법사를 통해는 기존 federation 서버 그룹에 추가 하려면  
  
1.  서버 관리자에서 **대시보드** 페이지, 클릭는 **알림**, 플래그 지정 및 클릭 한 다음 **서버의 federation 서비스 구성**합니다.  
  
    **Active Directory Federation 서비스 구성 마법사** 열립니다.  
  
2.  에 **시작** 페이지를 선택 하 고 **federation 서버 federation 서버 팜을 추가**을 차례로 클릭 하 고 **다음**합니다.  
  
3.  에 **AD DS에 연결** 페이지에서 계정을 도메인 관리자 권한이 및을 사용 하는 광고는이 컴퓨터 가입 된 도메인을를 클릭 하 여 지정 **다음**합니다.  
  
4.  에 **지정 농장** 페이지 기본 federation 서버 WID 사용 하는 그룹에 이름을 입력 하거나 데이터베이스 호스트 이름과 SQL Server를 사용 하는 기존 federation 서버 팜 데이터베이스 인스턴스 이름을 지정 합니다.  
  
    > [!WARNING]  
    > ® Windows Server 2012 r 2는 기본 SQL Server 인스턴스를 지정 하려면 해결 합니다. 해결 방법은 사용자 인터페이스를 사용 하지 않도록 합니다. 단계를 사용 하는 대신 [Windows PowerShell를 통해 새로운 federation 서버 그룹에서 첫 번째 federation 서버 구성 하려면](Configure-a-Federation-Server.md#BKMK_3)합니다.  
  
    > [!IMPORTANT]  
    > ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 SQL Server 2012를 포함 하 여 최신 버전을 사용할 수 있습니다.  
  
5.  에 **SSL 인증서를 지정** 페이지에서 가져올 SSL 인증서 하 고 이전에 받은 키를 포함 하는.pfx 파일. 이 인증서가 필요한 서비스 인증 인증서 합니다. [2 단계: adfs SSL 인증서 등록](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md),이 인증서을 federation 서버 구성 하려면 컴퓨터에 복사 합니다. 마법사를 통해.pfx 파일을 가져오려면 클릭 **가져오기** 파일의 위치를 찾습니다. 메시지가 표시 되 면.pfx 파일의 암호를 입력 합니다.  
  
6.  에 **서비스 계정 지정** 페이지를 구성 해 농장의 첫 번째 federation 서버를 만들 때 동일한 서비스 계정을 지정 합니다. 기존 그룹 관리 서비스 계정 또는 기존 도메인 사용자 계정에 사용할 수 있습니다.  
  
    > [!IMPORTANT]  
    > 사용자가 지정 된 계정에서이 농장 기본 federation 서버에 사용 된 계정으로 동일한 계정 있어야 합니다.  
  
7.  에 **리뷰 옵션** 페이지 구성 선택을 확인 하 고 클릭 한 다음 **다음**합니다.  
  
8.  에 **Pre\ 필수 조건 검사** 페이지에서 확인 모든 필수 검사를 성공적으로 완료 한 다음 클릭 **구성**합니다.  
  
9. 에 **결과** 페이지 결과 검토 하 고 구성 성공적으로 완료 있는지 여부를 확인 하 고 클릭 한 다음 **다음 단계를 완료 federation 서비스 배포 하는 데 필요한**합니다. 자세한 내용은 참조 [ADFS 설치를 완료 하기 위해 다음 단계](https://go.microsoft.com/fwlink/p/?LinkId=286704)합니다. 클릭 **닫기** 마법사를 종료 합니다.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Federation 서버를 Windows PowerShell 통해는 기존 federation 서버 그룹에 추가 하려면  
기존 gMSA 계정이 나 기존 도메인 사용자 계정을 사용 하 여 federation 서버 기존 그룹에 추가할 수 있습니다.  
  
-   기존 gMSA 계정을 사용 하 여 농장 federation 서버 연결 하려는 경우 다음을 수행 합니다.  
  
    1.  Federation 서버로 구성 컴퓨터에 필요한 SSL 인증서를 가져온 후에 있는지 확인는 **로컬 Computer\\My 스토어** 디렉터리 합니다. Windows PowerShell 명령 창에서 다음 명령을 실행 하 여 ssl 가져온 후에 있는지 여부를 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서에는 지문 표시 되는 **로컬 Computer\\My 스토어** 디렉터리 합니다.  
  
    2.  Federation 서버 구성 하려면 컴퓨터에서 Windows PowerShell 명령 창 열고 다음 명령을 실행 합니다.  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>` 광고 도메인 및 해당 도메인 gMSA 계정 이름입니다. `<first_federation_server_hostname>` 이 기존 농장의 기본 federation 서버 호스트 이름이입니다.  
  
        값을 받을 수 있는 `<certificate_thumbprint>`실행 하 여 `dir Cert:\LocalMachine\My`이전 단계에서 합니다.  
  
        > [!NOTE]  
        > 이 명령을 실행 하는 처음으로 없는 경우 추가 `OverwriteConfiguration`매개 합니다.  
  
        > [!NOTE]  
        > 이전 명령을 WID 농장 노드를 만듭니다. 서버 농장 노드 SQL Server 실행 하는 컴퓨터의 만들 하려는 경우 이미 설치 되 고 작동 SQL Server 인스턴스가 있어야 합니다.  
        >   
        > 다음 명령을 사용 하 여 federation 서버 SQL Server 인스턴스를 사용 하는 기존 농장을 추가 하려면: `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`어디 **SQL\_Host\_Name** SQL Server을 실행 하는 서버 이름 및 **SQL\_instance\_name** SQL Server 인스턴스의 이름입니다. 기본 SQL Server 인스턴스를 사용 하는 경우는 **포트가** 값 "**데이터 Source\ < SQL\_Host\_Name > =; 통합 Security\ 않게**" 합니다.  
  
        > [!IMPORTANT]  
        > ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 2014 SQL Server, SQL Server 2012 등 최신 버전을 사용할 수 있습니다.  
  
-   기존 도메인 사용자 계정을 사용 하 여 농장 federation 서버 연결 하려는 경우 다음을 수행 합니다.  
  
    1.  Federation 서버 구성 하려면 컴퓨터에서 Windows PowerShellcommand 창을 연 다음 명령을 실행: `$fscred = get-credential`합니다. 형식 domain\\user 이름에 해당 federation 서비스 계정 하려는 도메인 사용자 계정 자격 증명을 입력 합니다.  
  
    2.  Federation 서버로 구성 컴퓨터에 필요한 SSL 인증서를 가져온 후에 있는지 확인는 **로컬 Computer\\My 스토어** 디렉터리 합니다. Windows PowerShellcommand 창에서 다음 명령을 실행 하 여 ssl 가져온 후에 있는지 여부를 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서에는 지문 표시 되는 **로컬 Computer\\My 스토어** 디렉터리 합니다.  
  
    3.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > 이 명령을 실행 하는 처음으로 없는 경우 추가 `OverwriteConfiguration`매개 합니다.  
  
        > [!NOTE]  
        > 이전 명령을 WID 농장 노드를 만듭니다. 서버 농장 노드 SQL Server 실행 하는 컴퓨터의 만들 하려는 경우 이미 설치 되 고 작동 SQL Server 인스턴스가 있어야 합니다. 다음 명령을 사용 하 여 SQL Server 인스턴스를 사용 하 여 federation 서버 기존 농장을 추가 하려면: `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`어디 **SQL\_Host\_Name** SQL Server 인스턴스를 실행 하는 서버 이름 및 **SQL\_instance\_name** SQL Server 인스턴스의 이름입니다. 기본 SQL Server 인스턴스를 사용 하는 경우는 **포트가** 값 "**데이터 Source\ < SQL\_Host\_Name > =; 통합 Security\ 않게**" 합니다.  
  
        > [!IMPORTANT]  
        > ADFS 농장을 만들고 사용 SQL Server 구성 데이터를 저장 하려는 경우 SQL Server 2008 및 2014 SQL Server, SQL Server 2012 등 최신 버전을 사용할 수 있습니다.  
  
## <a name="see-also"></a>참조 하십시오 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[지침에 따라 Windows Server 2012 r 2 광고 FS 배포](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Federation 서버 농장 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

