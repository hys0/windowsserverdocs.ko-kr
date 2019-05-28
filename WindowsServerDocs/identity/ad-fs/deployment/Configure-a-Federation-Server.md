---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Windows Server 2012 R2 AD FS 배포 가이드
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d2f597994aa74f453903e09f7d3eefd83f26faba
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192275"
---
# <a name="configure-a-federation-server"></a>페더레이션 서버 구성

Active Directory Federation Services를 설치한 후 \(AD FS\) 역할 서비스 컴퓨터에서이 컴퓨터를 페더레이션 서버로 구성할 수 있습니다. 다음 중 하나를 수행하십시오.  
  
-   [새 페더레이션 서버 팜의 첫 번째 페더레이션 서버 구성](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [기존 페더레이션 서버 팜에 페더레이션 서버 추가](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>새 페더레이션 서버 팜의 첫 번째 페더레이션 서버 구성  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>Active Directory Federation Service 구성 마법사를 사용 하 여 새 페더레이션 서버 팜의 첫 번째 페더레이션 서버를 구성 하려면  
  
> [!NOTE]  
> 도메인 관리자 권한이 없거나이 절차를 수행 하기 전에 도메인 관리자 자격 증명 사용할 수 있는 확인 합니다.  
  
1.  서버 관리자 **대시보드** 페이지에서 **알림** 플래그를 클릭한 다음 **이 서버에 페더레이션 서비스를 구성하십시오.** 을 클릭합니다.  
  
    **Active Directory Federation Service 구성 마법사** 가 열립니다.  
  
2.  **시작** 페이지에서 **페더레이션 서버 팜에 첫 번째 페더레이션 서버를 만듭니다.** 를 선택하고 **다음**을 클릭합니다.  
  
3.  에 **AD DS에 연결** 페이지에서 Active Directory에 대 한 도메인 관리자 권한을 사용 하 여 계정을 지정 \(AD\) 는이 컴퓨터가 가입 된, 도메인 및 클릭 **다음**.  
  
4.  **서비스 속성 지정** 페이지에서 다음을 수행한 후 **다음**을 클릭합니다.  
  
    -   Secure Socket Layer를 포함 하는.pfx 파일을 가져옵니다 \(SSL\) 인증서와 이전에 얻은 키입니다. [2 단계: AD FS에 대 한 SSL 인증서를 등록](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md),이 인증서를 받을 있고 페더레이션 서버로 구성할 컴퓨터에 복사 합니다. 마법사를 통해.pfx 파일을 가져오려면 클릭 **가져올**, 한 다음 파일의 위치를 찾습니다. 메시지가 표시 되 면.pfx 파일에 대 한 암호를 입력 합니다.  
  
    -   페더레이션 서비스에 대 한 이름을 제공 합니다. 예를 들어 **fs.contoso.com**합니다. 이 이름은 주체 또는 인증서의 주체 대체 이름 중 하나가 일치 해야 합니다.  
  
    -   페더레이션 서비스의 표시 이름을 제공 합니다. 예를 들어 **Contoso Corporation**합니다. 사용자 Active Directory Federation Services에서이 이름을 보게 \(AD FS\) 로그인\-페이지에서입니다.  
  
5.  에 **서비스 계정 지정** 페이지, 서비스 계정을 지정 합니다. 만들기 또는 기존 그룹 관리 서비스 계정 사용 수 있습니다 \(gMSA\) 하거나 기존 도메인 사용자 계정을 사용 합니다. 새 gMSA 계정을 작성 하는 옵션을 선택 하면 새 계정의 이름을 지정 합니다. 기존 gMSA 또는 도메인 계정을 사용 하는 옵션을 선택 하면 클릭 **선택** 계정을 선택 합니다.  
  
    > [!NOTE]  
    > GMSA 계정을 사용 하 여의 장점은 해당 자동\-암호 업데이트 기능을 협상 합니다.  
  
    > [!WARNING]  
    > GMSA 계정을 사용 하려는 경우 Windows Server 2012 운영 체제에서 실행 되는 환경의 도메인 컨트롤러가 하나 이상 있어야 합니다.  
    >   
    > GMSA 옵션을 사용할 경우와 같은 오류 메시지가 표시 **KDS 루트 키를 설정 하지 않았기 때문에 그룹 관리 서비스 계정을 사용할 수 없는**, 다음 Windows를 실행 하 여 도메인에서 gMSA를 설정할 수 있습니다. Windows Server 2012를 실행 하는 도메인 컨트롤러 이상에서 Active Directory 도메인에서 PowerShell 명령: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`합니다. 반환 마법사를 클릭 **이전**를 클릭 하 고 **다음** 를 다시\-입력 합니다 **서비스 계정 지정** 페이지입니다. GMSA 옵션을 이제 활성화 되어야 합니다. 선택 하 고 사용 하려는 gMSA 계정 이름을 입력 합니다.  
  
6.  에 **구성 데이터베이스 지정** 페이지에서 AD FS 구성 데이터베이스를 지정 하 고 클릭 **다음**합니다. Windows 내부 데이터베이스를 사용 하 여이 컴퓨터에는 데이터베이스를 하거나 만들 수 있습니다 \(WID\), 또는 Microsoft SQL server 인스턴스 이름과 위치를 지정할 수 있습니다.  
  
    자세한 내용은 [AD FS 구성 데이터베이스의 역할](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우에 SQL Server 2008 및 SQL Server 2012 및 SQL Server 2014를 비롯 하 여 최신 버전을 사용할 수 있습니다.  
  
7.  **검토 옵션** 페이지에서 구성 선택 사항을 확인하고 **다음**을 클릭합니다.  
  
8.  에 **Pre\-필수 검사** 페이지에서 모든 필수 구성 요소 검사가 성공적으로 완료 하 고 클릭 **구성**합니다.  
  
9. 에 **결과** 페이지에서 결과 검토 하 고 구성이 성공적으로 완료 되 고 있는지 여부를 확인 하 고 클릭 **페더레이션 서비스 배포를 완료 하는 데 필요한 다음 단계**합니다. 자세한 내용은 [AD FS 설치 완료의 다음 단계](https://go.microsoft.com/fwlink/p/?LinkId=286704)합니다. **닫기**를 클릭하여 마법사를 종료합니다.  
  
### <a name="BKMK_3"></a>Windows PowerShell을 통해 새 페더레이션 서버 팜의 첫 번째 페더레이션 서버를 구성 하려면  
새 / 기존 gMSA 계정 또는 기존 도메인 사용자 계정을 사용 하 여 새 페더레이션 서버 팜을 만들 수 있습니다.  
  
-   **새 gMSA 계정을 사용 하 여 새 페더레이션 서버를 만들려면 다음을 수행 합니다.**  
  
    > [!IMPORTANT]  
    > 새 페더레이션 서버 팜의 첫 번째 페더레이션 서버를 만들려면 도메인 관리자 권한이 있어야 합니다.  
  
    1.  페더레이션 서버로 구성할 컴퓨터에서 필요한 SSL 인증서를 가져왔는지 확인 합니다 **로컬 컴퓨터\\My Store** 디렉터리입니다. Windows PowerShell 명령 창에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서의 지문을으로 나열 됩니다는 **로컬 컴퓨터\\My Store** 디렉터리입니다.  
  
    2.  도메인 컨트롤러에서 Windows PowerShell 명령 창을 열고 KDS 루트 키를 도메인에서 만들어졌는지 여부를 확인 하려면 다음 명령을 실행: `Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`합니다. 이 만들지 않은 경우 출력 정보가 표시 되도록, 키를 만들려면 다음 명령을 실행: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`합니다.  
  
    3.  페더레이션 서버로 구성할 컴퓨터에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > `$` 이전 명령의 끝에 기호가 필요 합니다.  
  
        에 대 한 값을 가져오려면 `<certificate_thumbprint>`실행 `dir Cert:\LocalMachine\My`를 선택한 다음 SSL 인증서의 지문입니다. 변수의 `<federation_service_name>` 이름은 페더레이션 서비스의 예를 들어 **fs.contoso.com**합니다.  
  
        > [!NOTE]  
        > 이 명령은 실행 하는 첫 번째에 없는 경우 추가 `OverwriteConfiguration` 매개 변수입니다.  
  
        > [!NOTE]  
        > 이전 명령에는 WID 팜을 만듭니다. SQL Server 서버 팜을 만들려면 하려는 경우 이미 설치 되었으며 작동 하는 SQL Server 인스턴스에 있어야 합니다.  
        >   
        > SQL Server의 인스턴스를 사용 하는 새 팜에서 첫 번째 페더레이션 서버를 만들려면 다음 명령을 사용할 수 있습니다: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"` 여기서 **< SQL\_호스트\_이름 >** 있는 SQL 서버의 이름 서버에서을 실행 하 고 **< SQL\_인스턴스\_이름 >** SQL Server 인스턴스의 이름입니다. 사용 하 여 SQL Server의 기본 인스턴스를 사용 하는 경우는 **SQLConnectionString** 의 값 "**데이터 원본\=< SQL\_호스트\_이름 >; Integrated Security\=True** ".  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용하여 구성 데이터를 저장하려면 SQL Server 2008 이상(SQL Server 2012 포함)을 사용하면 됩니다.  
  
-   **기존 도메인 사용자 계정을 사용 하 여 새 페더레이션 서버를 만들려면 다음을 수행 합니다.**  
  
    1.  페더레이션 서버로 구성할 컴퓨터에서 필요한 SSL 인증서를 가져왔는지 확인 합니다 **로컬 컴퓨터\\My Store** 디렉터리입니다. Windows PowerShell 명령 창에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서의 지문을으로 나열 됩니다는 **로컬 컴퓨터\\My Store** 디렉터리입니다.  
  
    2.  페더레이션 서버로 구성할 컴퓨터에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행: `$fscred = Get-Credential`합니다. 도메인 사용자 계정 자격 증명을 입력 형식 도메인의 페더레이션 서비스 계정에 대 한 사용 하려는\\사용자 이름입니다.  
  
    3.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행합니다.  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        에 대 한 값을 가져옵니다 **< 인증서\_지문 >** 실행 `dir Cert:\LocalMachine\My`를 선택한 다음 SSL 인증서의 지문입니다. 변수의 **< 페더레이션\_service\_이름 >** fs.contoso.com 예를 들어, 페더레이션 서비스의 이름입니다.  
  
        > [!NOTE]  
        > 이 명령은 실행 하는 첫 번째에 없는 경우 추가 `OverwriteConfiguration` 매개 변수입니다.  
  
        > [!NOTE]  
        > 이전 명령에는 WID 팜을 만듭니다. SQL Server 팜을 만들려면 하려는 경우 이미 설치 되었으며 작동 하는 SQL Server 인스턴스에 있어야 합니다.  
        >   
        > 다음 명령을 사용 하 여 SQL Server의 인스턴스를 사용 하는 새 팜에서 첫 번째 페더레이션 서버를 만들려면: `Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` 여기서 **SQL\_호스트\_이름** 은 SQL Server에는 서버의 이름 를 실행 하 고 **SQL\_인스턴스\_이름** SQL Server 인스턴스의 이름입니다. 사용 하 여 SQL Server의 기본 인스턴스를 사용 하는 경우는 **SQLConnectionString** 의 값 "**데이터 원본\=< SQL\_호스트\_이름 >; Integrated Security\=True** ".  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우에 SQL Server 2008 및 SQL Server 2012 및 SQL Server 2014를 비롯 하 여 최신 버전을 사용할 수 있습니다.  
  
## <a name="BKMK_2"></a>기존 페더레이션 서버 팜에 페더레이션 서버 추가  
  
> [!IMPORTANT]  
> 완료 한 것으로 확인 [3 단계: AD FS 역할 서비스 설치](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)이 단원의 절차를 시작 하기 전에, 합니다.  
  
> [!IMPORTANT]  
> 얻었다고 올바른 SSL 서버 인증 인증서가이 절차를 완료 하기 전에 확인 합니다.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Active Directory Federation Service 구성 마법사를 통해 기존 페더레이션 서버 팜에 페더레이션 서버를 추가 하려면  
  
1.  서버 관리자 **대시보드** 페이지에서 **알림** 플래그를 클릭한 다음 **이 서버에 페더레이션 서비스를 구성하십시오.** 을 클릭합니다.  
  
    **Active Directory Federation Service 구성 마법사** 가 열립니다.  
  
2.  에 **시작** 페이지에서 **페더레이션 서버 팜에 페더레이션 서버 추가**를 클릭 하 고 **다음**합니다.  
  
3.  에 **AD DS에 연결** 페이지에서,이 컴퓨터가 가입 되어 있는 AD 도메인과 클릭에 대 한 도메인 관리자 권한을 사용 하 여 계정을 지정 **다음**합니다.  
  
4.  에 **팜 지정** 페이지에서 WID를 사용 하는 팜에서 기본 페더레이션 서버의 이름을 입력 하거나 SQL Server를 사용 하는 기존 페더레이션 서버 팜에 데이터베이스 인스턴스 이름과 데이터베이스 호스트 이름을 지정 합니다.  
  
    > [!WARNING]  
    > Windows Server® 2012 R2, SQL Server의 기본 인스턴스를 지정 하는 방법이 있습니다. 사용자 인터페이스를 사용 하지 않도록이 문제를 해결 합니다. 단계를 사용 하는 대신 [Windows PowerShell을 통해 새 페더레이션 서버 팜의 첫 번째 페더레이션 서버를 구성 하려면](Configure-a-Federation-Server.md#BKMK_3)합니다.  
  
    > [!IMPORTANT]  
    > AD FS 팜을 만들고 SQL Server를 사용하여 구성 데이터를 저장하려면 SQL Server 2008 이상(SQL Server 2012 포함)을 사용하면 됩니다.  
  
5.  에 **SSL 인증서 지정** 페이지에서 SSL 인증서와 이전에 얻은 키를 포함 하는.pfx 파일을 가져옵니다. 이 인증서는 필수 서비스 인증 인증서입니다. [2 단계: AD FS에 대 한 SSL 인증서를 등록](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md),이 인증서를 받을 있고 페더레이션 서버로 구성할 컴퓨터에 복사 합니다. 마법사를 통해.pfx 파일을 가져오려면 클릭 **가져올** 파일의 위치를 찾습니다. 메시지가 표시 되 면.pfx 파일에 대 한 암호를 입력 합니다.  
  
6.  에 **서비스 계정 지정** 페이지에서 팜의 첫 번째 페더레이션 서버를 만들 때 구성 된 동일한 서비스 계정을 지정 합니다. 기존 그룹 관리 서비스 계정 또는 기존 도메인 사용자 계정을 사용할 수 있습니다.  
  
    > [!IMPORTANT]  
    > 지정 하는 계정은이 팜의 기본 페더레이션 서버에서 사용한 계정과 동일한 계정 이어야 합니다.  
  
7.  **검토 옵션** 페이지에서 구성 선택 사항을 확인하고 **다음**을 클릭합니다.  
  
8.  에 **Pre\-필수 검사** 페이지에서 모든 필수 구성 요소 검사가 성공적으로 완료 하 고 클릭 **구성**합니다.  
  
9. 에 **결과** 페이지에서 결과 검토 하 고 구성이 성공적으로 완료 되 고 있는지 여부를 확인 하 고 클릭 **페더레이션 서비스 배포를 완료 하는 데 필요한 다음 단계**합니다. 자세한 내용은 [AD FS 설치 완료의 다음 단계](https://go.microsoft.com/fwlink/p/?LinkId=286704)합니다. **닫기**를 클릭하여 마법사를 종료합니다.  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Windows PowerShell을 통해 기존 페더레이션 서버 팜에 페더레이션 서버를 추가 하려면  
기존 gMSA 계정 또는 기존 도메인 사용자 계정을 사용 하 여 기존 팜에 페더레이션 서버를 추가할 수 있습니다.  
  
-   기존 gMSA 계정을 사용 하 여 페더레이션 서버 팜에 연결 하려는 경우 다음을 수행 합니다.  
  
    1.  페더레이션 서버로 구성할 컴퓨터에서 필요한 SSL 인증서를 가져왔는지 확인 합니다 **로컬 컴퓨터\\My Store** 디렉터리입니다. Windows PowerShell 명령 창에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서의 지문을으로 나열 됩니다는 **로컬 컴퓨터\\My Store** 디렉터리입니다.  
  
    2.  페더레이션 서버로 구성할 컴퓨터에서 Windows PowerShell 명령 창을 열고 다음 명령을 실행 합니다.  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>` AD 도메인과 해당 도메인의 gMSA 계정 이름 됩니다. `<first_federation_server_hostname>` 이 기존 팜의 기본 페더레이션 서버의 호스트 이름이입니다.  
  
        에 대 한 값을 가져올 수 있습니다 `<certificate_thumbprint>` 실행 하 여 `dir Cert:\LocalMachine\My` 이전 단계에서 합니다.  
  
        > [!NOTE]  
        > 이 명령은 실행 하는 첫 번째에 없는 경우 추가 `OverwriteConfiguration` 매개 변수입니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 팜 노드를 만듭니다. SQL Server를 실행 하는 컴퓨터의 서버 팜에 노드를 만들려는 경우에 이미 설치 되었으며 작동 하는 SQL Server 인스턴스에 있어야 합니다.  
        >   
        > 다음 명령을 사용 하 여 SQL Server의 인스턴스를 사용 하는 기존 팜에 페더레이션 서버를 추가 하려면: `Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` 여기서 **SQL\_호스트\_이름** 은 SQL Server에는 서버의 이름 를 실행 하 고 **SQL\_인스턴스\_이름** SQL Server 인스턴스의 이름입니다. 사용 하 여 SQL Server의 기본 인스턴스를 사용 하는 경우는 **SQLConnectionString** 의 값 "**데이터 원본\=< SQL\_호스트\_이름 >; Integrated Security\=True** ".  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우에 SQL Server 2008 및 SQL Server 2012 및 SQL Server 2014를 비롯 하 여 최신 버전을 사용할 수 있습니다.  
  
-   기존 도메인 사용자 계정을 사용 하 여 페더레이션 서버 팜에 연결 하려는 경우 다음을 수행 합니다.  
  
    1.  페더레이션 서버로 구성할 컴퓨터에서 Windows PowerShellcommand 창을 열고 다음 명령을 실행: `$fscred = get-credential`합니다. 도메인 사용자 계정 자격 증명을 입력 형식 도메인의 페더레이션 서비스 계정에 대 한 사용 하려는\\사용자 이름입니다.  
  
    2.  페더레이션 서버로 구성할 컴퓨터에서 필요한 SSL 인증서를 가져왔는지 확인 합니다 **로컬 컴퓨터\\My Store** 디렉터리입니다. Windows PowerShellcommand 창에서 다음 명령을 실행 하 여 SSL 인증서를 가져왔는지 확인할 수 있습니다: `dir Cert:\LocalMachine\My`합니다. 인증서의 지문을으로 나열 됩니다는 **로컬 컴퓨터\\My Store** 디렉터리입니다.  
  
    3.  동일한 Windows PowerShell 명령 창에서 다음 명령을 실행 합니다.  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > 이 명령은 실행 하는 첫 번째에 없는 경우 추가 `OverwriteConfiguration` 매개 변수입니다.  
  
        > [!NOTE]  
        > 이전 명령은 WID 팜 노드를 만듭니다. SQL Server를 실행 하는 컴퓨터의 서버 팜에 노드를 만들려는 경우에 이미 설치 되었으며 작동 하는 SQL Server 인스턴스에 있어야 합니다. 다음 명령을 사용 하 여 SQL Server의 인스턴스를 사용 하 여 기존 팜에 페더레이션 서버를 추가 하려면: `Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"` 여기서 **SQL\_호스트\_이름** 는 서버의 이름인 SQL 인스턴스의 서버에서을 실행 하 고 **SQL\_인스턴스\_이름** SQL Server 인스턴스의 이름입니다. 사용 하 여 SQL Server의 기본 인스턴스를 사용 하는 경우는 **SQLConnectionString** 의 값 "**데이터 원본\=< SQL\_호스트\_이름 >; Integrated Security\=True** ".  
  
        > [!IMPORTANT]  
        > AD FS 팜을 만들고 SQL Server를 사용 하 여 구성 데이터를 저장 하려는 경우에 SQL Server 2008 및 SQL Server 2012 및 SQL Server 2014를 비롯 하 여 최신 버전을 사용할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목 

[AD FS 배포](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 배포 가이드](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[페더레이션 서버 팜 배포](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

