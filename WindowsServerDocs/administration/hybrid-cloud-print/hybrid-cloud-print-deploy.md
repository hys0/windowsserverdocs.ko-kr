---
title: Windows Server 하이브리드 클라우드 인쇄 배포
description: Microsoft 하이브리드 클라우드 인쇄를 설정 하는 방법
ms.prod: windows-server
ms.technology: windows server 2016
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247c5e9
ms.topic: how-to
author: msjimwu
ms.author: coreyp
manager: dongill
ms.date: 3/15/2018
ms.openlocfilehash: fe1f2b11921950ea725cb996ce58e75033aaae4a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470208"
---
# <a name="deploy-windows-server-hybrid-cloud-print"></a>Windows Server 하이브리드 클라우드 인쇄 배포

>적용 대상: Windows Server 2016

IT 관리자를 위한이 항목에서는 Microsoft의 HCP (하이브리드 클라우드 인쇄) 솔루션의 종단 간 배포에 대해 설명 합니다. 이 솔루션은 인쇄 서버로 실행 되는 기존 Windows Server를 기반으로 계층을 만들고,이를 통해 Azure AD (Azure AD) 가입 및 MDM 관리 장치를 사용 하 여 조직 관리 프린터를 검색 하 고 인쇄할 Azure Active Directory 수 있습니다.

## <a name="pre-requisites"></a>필수 구성 요소

이 설치를 시작 하기 전에 획득 해야 하는 여러 구독, 서비스 및 컴퓨터가 있습니다. 다음과 같습니다.

- Azure AD premium 구독.

  Azure에 대 한 평가판 구독을 보려면 [azure 구독 시작](https://azure.microsoft.com/trial/get-started-active-directory/) 을 참조 하세요.

- MDM 서비스 (예: Intune).

  Intune에 대 한 평가판 구독 [Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) 를 참조 하세요.

- Active Directory를 실행 하는 Windows Server 2016 이상 컴퓨터

  Active Directory를 설정 하는 방법에 대 한 도움말은 단계별 [: Windows Server 2016의 Active Directory 설정](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/) 을 참조 하세요.

- 인쇄 서버로 실행 되는 도메인에 가입 된 전용 Windows Server 2016 이상 컴퓨터

- 커넥터 서버로 실행 되는 전용 도메인에 가입 된 Windows Server 2016 이상 컴퓨터

  자세한 내용은 [Azure AD 응용 프로그램 프록시 커넥터 이해](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connectors) 를 참조 하세요.

- 프린터를 게시 하기 위한 Windows 10이 하 버전의 Windows 10 크리에이터 업데이트 이상 컴퓨터입니다.

- 공용 도메인 이름입니다.

  Azure (onmicrosoft.com)에서 만든 도메인 이름을 사용 하거나 고유한 도메인 이름을 구입할 수*있습니다.* [Azure Active Directory 포털을 사용 하 여 사용자 지정 도메인 이름 추가](https://docs.microsoft.com/azure/active-directory/fundamentals/add-custom-domain)를 참조 하세요.

## <a name="deployment-steps"></a>배포 단계

다음 단계는 일반적인 하이브리드 클라우드 인쇄 배포를 위한 것입니다.

### <a name="step-1---install-azure-ad-connect"></a>1 단계-Azure AD Connect 설치

1. Azure AD connect는 Azure AD를 온-프레미스 AD와 동기화 합니다. Active Directory Windows Server 컴퓨터에서 express 설정을 사용 하 여 Azure AD Connect 소프트웨어를 다운로드 하 고 설치 합니다. [Express 설정을 사용 하 여 Azure AD Connect 시작을](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express)참조 하세요.

### <a name="step-2---install-application-proxy"></a>2 단계-응용 프로그램 프록시 설치

1. 응용 프로그램 프록시를 사용 하면 조직의 사용자가 클라우드에서 온-프레미스 응용 프로그램에 액세스할 수 있습니다. 커넥터 서버에 응용 프로그램 프록시를 설치 합니다.
    - 설치 지침은 [자습서: Azure Active Directory에서 응용 프로그램 프록시를 통해 원격 액세스를 위한 온-프레미스 응용 프로그램 추가](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-add-on-premises-application)를 참조 하세요.
    - 조직에 복잡 한 네트워크 토폴로지가 있는 경우 전용 커넥터 그룹을 권장 합니다. [커넥터 그룹을 사용 하 여 별도의 네트워크와 위치에 응용 프로그램 게시](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-connector-groups)를 참조 하세요.

### <a name="step-3---register-and-configure-applications"></a>3 단계-응용 프로그램 등록 및 구성

HCP 서비스와 인증 된 통신을 사용 하도록 설정 하려면 3 개의 응용 프로그램을 만들어야 합니다. 2 개의 HCP 서비스를 나타내는 2 개의 웹 응용 프로그램과 해당 서비스와 통신 하는 네이티브 응용 프로그램 1 개를 만들어야 합니다.

1. 웹 앱을 등록 하려면 Azure Portal 로그인 합니다.
    - Azure Active Directory에서 **앱 등록**  >  **새 등록**으로 이동 합니다.

    ![AAD 앱 등록 1](../media/hybrid-cloud-print/AAD-AppRegistration.png)

    - 검색 서비스에 대 한 앱 이름을 입력 합니다. **등록** 을 클릭 하 여 완료 합니다.

    ![AAD 앱 등록 2](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria.png)

    - 엔터프라이즈 클라우드 인쇄 서비스에 대해 반복 합니다.
    - 네이티브 앱에 대해 반복 합니다.
    - 이 세 가지 응용 프로그램은 **앱 등록**아래에 표시 되어야 합니다.

    ![AAD 앱 등록 3](../media/hybrid-cloud-print/AAD-AppRegistration-AllApps.png)

2. 두 웹 응용 프로그램에 대 한 API를 노출 합니다.
    - **앱 등록** 블레이드에서 계속 하는 동안 Mopria 검색 서비스 앱을 클릭 하 고 **API**표시를 선택한 다음 응용 프로그램 ID URI 옆의 **설정** 을 클릭 합니다.

    ![AAD 노출 API 1](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI.png)

    - 응용 프로그램 ID URI의 기본값을 변경 하지 않고 **저장** 을 클릭 합니다. 이 값은 지금 설정 해야 하며 나중에 변경 될 예정입니다.

    ![AAD 노출 API 2](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-Save.png)

    - **범위 추가**를 클릭 합니다.

    ![AAD 노출 API 3](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-AddScope.png)

    - 범위 이름을 제공 하 고, 관리자와 사용자가 동의할 수 있도록 하 고, 동의 설명을 입력 한 다음, **범위 추가** 를 클릭 하 여 완료 합니다.

    ![AAD 노출 API 4](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-ExposeAPI-ScopeName.png)

    - 엔터프라이즈 클라우드 인쇄 서비스에 대해 반복 합니다. 다른 범위 이름 및 동의 설명을 사용 합니다.

    ![AAD 노출 API 5](../media/hybrid-cloud-print/AAD-AppRegistration-ECP-ExposeAPI-ScopeName.png)

3. API 사용 권한 추가
    - 앱 등록 블레이드로 돌아갑니다. 네이티브 앱을 클릭 하 고 API 권한을 선택 합니다. **권한 추가**를 클릭합니다.

    ![AAD API 권한 1](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission.png)

    - **내 조직에서 사용**하는 api로 전환 하 고 검색 상자를 사용 하 여 이전에 추가 된 검색 서비스를 찾습니다. 검색 결과에서 서비스를 클릭 합니다.

    ![AAD API 권한 2](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria.png)

    - **위임 된 권한**을 선택 합니다. API 범위 옆의 확인란을 선택 합니다. **권한 추가**를 클릭 합니다.

    ![AAD API 권한 3](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Mopria-Add.png)

    - 을 반복 하 여 엔터프라이즈 클라우드 인쇄 서비스에 사용 권한을 추가 합니다.

    ![AAD API 권한 4](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-ECP-Add.png)

    - API 권한 블레이드에 반환 된 후에는 **전체 관리자 동의 ...** 를 클릭 하기 전에 10 초 동안 기다립니다.

    ![AAD API 권한 5](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent.png)

    - 메시지가 표시 되 면 **예** 를 클릭 합니다.

    ![AAD API 권한 6](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-GrantConsent-Yes.png)

    - API 권한의 상태 열에 녹색 확인 표시가 표시 되는지 확인 합니다.

    ![AAD API 권한 7](../media/hybrid-cloud-print/AAD-AppRegistration-APIPermission-Verify.png)

4. 웹 응용 프로그램에 대 한 응용 프로그램 프록시 구성
    - **Azure Active Directory**  >  **Enterprise 응용 프로그램**  >  **모든 응용 프로그램**으로 이동 합니다. 검색 서비스를 검색 하 고 클릭 합니다.

    ![AAD 앱 프록시 1](../media/hybrid-cloud-print/AAD-EnterpriseApp-AllApps.png)

    - **응용 프로그램 프록시**를 클릭 합니다. 형식을 사용 하 여 내부 Url을 입력 `https://<fully qualified domain name of the Print Server>/mcs/` 합니다. **저장** 을 클릭 하 여 완료 합니다.

    ![AAD 앱 프록시 2](../media/hybrid-cloud-print/AAD-EnterpriseApp-Mopria-AppProxy.png)

    - 엔터프라이즈 클라우드 인쇄 서비스에 대해 반복 합니다. 내부 URL은 `https://<fully qualified domain name of the Print Server>/ecp/` 입니다.

    ![AAD 앱 프록시 3](../media/hybrid-cloud-print/AAD-EnterpriseApp-ECP-AppProxy.png)

    - **Azure Active Directory**  >  **앱 등록**로 이동 합니다. Monode.js a 검색 서비스를 클릭 합니다. **개요**에서 응용 프로그램 ID URI는 **응용 프로그램 프록시**의 기본값에서 외부 URL로 변경 되었습니다. URI는 인쇄 서버를 설치 하는 동안, 클라이언트 MDM 정책에서, 프린터를 게시 하는 데 사용 됩니다.

    ![AAD 앱 프록시 4](../media/hybrid-cloud-print/AAD-AppRegistration-Mopria-Overview.png)

5. 응용 프로그램에 사용자 할당
    - **Azure Active Directory**  >  **Enterprise 응용 프로그램**  >  **모든 응용 프로그램**으로 이동 합니다. 검색 서비스를 검색 하 고 클릭 합니다.
    - **사용자 및 그룹** 을 클릭 하 고 사용자를 할당 하거나 **속성** 을 클릭 하 고 **사용자 할당 필요?** 를 **아니요** 로 변경 합니다.
    - 엔터프라이즈 클라우드 인쇄 서비스에 대해 반복 합니다.

6. 네이티브 앱에서 리디렉션 URI 구성
    - **Azure Active Directory**  >  **앱 등록**로 이동 합니다. 네이티브 앱을 클릭 합니다. **개요** 로 이동 하 여 **응용 프로그램 (클라이언트) ID**를 복사 합니다.

    ![AAD 리디렉션 URI 1](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Overview.png)

    - **인증**으로 이동 합니다. **유형** 드롭다운 상자를로 변경 하 `Public...` 고 아래 형식을 사용 하 여 두 개의 리디렉션 uri를 입력 합니다 `<NativeClientAppID>` . 여기서은 이전 단계에서 가져온 것입니다.

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/<NativeClientAppID>`

        `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

    ![AAD 리디렉션 URI 2](../media/hybrid-cloud-print/AAD-AppRegistration-Native-Authentication.png)

    - **저장** 을 클릭 하 여 완료 합니다.

### <a name="step-4---setup-the-print-server"></a>4 단계-인쇄 서버 설정

1. 인쇄 서버에 사용할 수 있는 Windows 업데이트 모두 설치 되어 있는지 확인 합니다. 참고: 빌드 17763.165 이상에서 서버 2019을 패치 해야 합니다.
    - 다음 서버 역할을 설치 합니다.
        - 인쇄 서버 역할
        - IIS(인터넷 정보 서비스)
    - 서버 역할을 설치 하는 방법에 대 한 자세한 내용은 역할 [및 기능 추가 마법사를 사용 하 여 역할, 역할 서비스 및 기능 설치](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw) 를 참조 하세요.

    ![인쇄 서버 역할](../media/hybrid-cloud-print/PrintServer-Roles.png)

2. 하이브리드 클라우드 인쇄 PowerShell 모듈을 설치 합니다.
    - 관리자 권한 PowerShell 명령 프롬프트에서 다음 명령을 실행 합니다.

        `find-module -Name PublishCloudPrinter`컴퓨터가 PowerShell 갤러리에 연결할 수 있는지 확인 하려면 (PSGallery)

        `install-module -Name PublishCloudPrinter`

    > 참고: ' PSGallery '는 신뢰할 수 없는 리포지토리입니다. 라는 메시지가 표시 될 수 있습니다.  ' Y '를 입력 하 여 설치를 계속 합니다.

    ![인쇄 서버 게시 클라우드 프린터](../media/hybrid-cloud-print/PrintServer-PublishCloudPrinter.png)

3. 하이브리드 클라우드 인쇄 솔루션을 설치 합니다.
    - 동일한 승격 된 PowerShell 명령 프롬프트에서 디렉터리를 아래 (따옴표 필요)로 변경 합니다.

        `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`

    - 실행

        `.\CloudPrintDeploy.ps1 -AzureTenant <Azure Active Directory domain name> -AzureTenantGuid <Azure Active Directory ID>`

    - Azure Active Directory 도메인 이름을 찾으려면 아래 스크린샷을 참조 하세요.

    ![인쇄 서버 AAD 도메인 이름을 가져오는 방법](../media/hybrid-cloud-print/PrintServer-GetAADDomainName.png)

    - Azure Active Directory ID를 찾으려면 아래 스크린샷을 참조 하세요.

    ![인쇄 서버 클라우드 인쇄 배포](../media/hybrid-cloud-print/PrintServer-GetAADId.png)

    - CloudPrintDeploy 스크립트의 출력은 다음과 같습니다.

    ![인쇄 서버 클라우드 인쇄 배포](../media/hybrid-cloud-print/PrintServer-CloudPrintDeploy.png)

    - 로그 파일을 확인 하 여 오류가 있는지 확인 합니다.`C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0\CloudPrintDeploy.log`

4. 관리자 권한 명령 프롬프트에서 **Regitedit** 를 실행 합니다. Computer \ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CloudPrint\EnterpriseCloudPrintService.로 이동 합니다.
    - AzureAudience Enterprise Cloud 인쇄 앱의 응용 프로그램 ID URI로 설정 되었는지 확인 합니다.
    - AzureTenant이 Azure AD 도메인 이름으로 설정 되어 있는지 확인 합니다.

    ![인쇄 서버 ECP 레지스트리 키](../media/hybrid-cloud-print/PrintServer-RegEdit-ECP.png)

5. Computer \ HKEY_LOCAL_MACHINE \SOFTWARE\Microsoft\Windows\CurrentVersion\CloudPrint\MopriaDiscoveryService.로 이동 합니다.
    - AzureAudience 검색 서비스 앱의 응용 프로그램 ID URI 인지 확인 합니다.
    - AzureTenant이 Azure AD 도메인 이름 인지 확인 합니다.
    - URL이 검색 서비스 앱의 응용 프로그램 ID URI 인지 확인 합니다.

    ![인쇄 서버 Mopria 레지스트리 키](../media/hybrid-cloud-print/PrintServer-RegEdit-Mopria.png)

6. 권한 상승 Powershell 명령 프롬프트에서 **iisreset** 을 실행 합니다. 이렇게 하면 이전 단계에서 만든 레지스트리 변경 내용이 적용 됩니다.

7. SSL을 지원 하도록 IIS 끝점을 구성 합니다.
    - SSL 인증서는 자체 서명 된 인증서 또는 신뢰할 수 있는 CA (인증 기관)에서 발급 한 인증서 일 수 있습니다.
    - 자체 서명 된 인증서를 사용 하는 경우 **클라이언트 컴퓨터로 인증서를 가져왔는지 확인**합니다.
    - 타사 공급자에 도메인을 등록 하는 경우 SSL 인증서를 사용 하 여 IIS 끝점을 구성 해야 합니다. 자세한 내용은이 [가이드](https://www.sslsupportdesk.com/microsoft-server-2016-iis-10-10-5-ssl-installation/) 를 참조 하세요.

8. SQLite 패키지를 설치 합니다.
   - 관리자 권한 PowerShell 명령 프롬프트를 엽니다.
   - 다음 명령을 실행 하 여 시스템. SQLite nuget 패키지를 다운로드 합니다.

        `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`

   - 다음 명령을 실행 하 여 패키지를 설치 합니다.

        `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

   > 참고:-requiredversion 옵션을 해제 하 여 최신 버전을 다운로드 하 고 설치 하는 것이 좋습니다.

    ![인쇄 서버 Mopria 레지스트리 키](../media/hybrid-cloud-print/PrintServer-InstallSQLite.png)

9. SQLite dll을 MopriaCloudService Webapp bin 폴더 (C:\inetpub\wwwroot\MopriaCloudService\bin)에 복사 합니다.
    - 아래의 PowerShell 스크립트를 포함 하는 ps1 파일을 만듭니다.
    - $Version 변수를 이전 단계에서 설치한 SQLite 버전으로 변경 합니다.
    - 관리자 권한 PowerShell 명령 프롬프트에서 ps1 파일을 실행 합니다.

    ```powershell
    $source = \Program Files\PackageManagement\NuGet\Packages
    $core = System.Data.SQLite.Core
    $linq = System.Data.SQLite.Linq
    $ef6 = System.Data.SQLite.EF6
    $version = x.x.x.x
    $target = C:\inetpub\wwwroot\MopriaCloudService\bin

    xcopy /y $source\$core.$version\lib\net46\System.Data.SQLite.dll $target\
    xcopy /y $source\$core.$version\build\net46\x86\SQLite.Interop.dll $target\x86\
    xcopy /y $source\$core.$version\build\net46\x64\SQLite.Interop.dll $target\x64\
    xcopy /y $source\$linq.$version\lib\net46\System.Data.SQLite.Linq.dll $target\
    xcopy /y $source\$ef6.$version\lib\net46\System.Data.SQLite.EF6.dll $target\
    ```

10. 다음 섹션에서 SQLite 버전 x. x. x를 포함 하도록 c:\inetpub\wwwroot\MopriaCloudService\web.config 파일을 업데이트 합니다. `<runtime>/<assemblyBinding>` 이는 이전 단계에서 사용 되는 버전과 동일 합니다.

    ```xml
    ...
    <dependentAssembly>
    assemblyIdentity name=System.Data.SQLite culture=neutral publicKeyToken=db937bc2d44ff139 /
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.Core culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.EF6 culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    <dependentAssembly>
    <assemblyIdentity name=System.Data.SQLite.Linq culture=neutral publicKeyToken=db937bc2d44ff139 />
    <bindingRedirect oldVersion=0.0.0.0-x.x.x.x newVersion=x.x.x.x />
    </dependentAssembly>
    ...
    ```

11. SQLite 데이터베이스를 만듭니다.
    - 에서 SQLite Tools 바이너리를 다운로드 하 여 설치 `https://www.sqlite.org/` 합니다.
    - 디렉터리로 이동 `c:\inetpub\wwwroot\MopriaCloudService\Database` 합니다.
    - 다음 명령을 실행 하 여이 디렉터리에 데이터베이스를 만듭니다.

        `sqlite3.exe MopriaDeviceDb.db .read MopriaSQLiteDb.sql`

    - 파일 탐색기에서 MopriaDeviceDb. db 파일 속성을 열어 보안 탭에 있는 데이터베이스에 게시할 수 있는 사용자 또는 그룹을 추가 합니다. 사용자 또는 그룹은 온-프레미스 Active Directory에 존재 하 고 Azure AD와 동기화 되어야 합니다.
    - 솔루션을 라우팅할 수 없는 도메인 (예: *mydomain*)에 배포 하는 경우 Azure AD 도메인 (예: onmicrosoft.com 또는 타사 공급 업체에서 구매한 항목)을 온-프레미스 ACTIVE DIRECTORY에 UPN 접미사로 추가 해야 *합니다.* 따라서 프린터를 게시 하는 정확히 동일한 사용자 (예 admin@: onmicrosoft.com)를 데이터베이스 파일의 보안 설정에 추가할*수 있습니다.* [디렉터리 동기화를 위해 라우팅 불가능 도메인 준비](https://docs.microsoft.com/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization)를 참조 하세요.

    ![인쇄 서버 Mopria 레지스트리 키](../media/hybrid-cloud-print/PrintServer-SQLiteDB.png)

### <a name="step-5-optional---configure-pre-authentication-with-azure-ad"></a>5 단계 \[ 선택 사항 \] -Azure AD를 사용 하 여 사전 인증 구성

1. [응용 프로그램 프록시를 사용 하 여 앱에 Single Sign-On에 대 한 Kerberos 제한 위임](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-configure-single-sign-on-with-kcd)문서를 검토 합니다.

2. 온-프레미스 Active Directory를 구성 합니다.
    - Active Directory 컴퓨터에서 서버 관리자를 열고 **도구**  >  **Active Directory 사용자 및 컴퓨터**로 이동 합니다.
    - **컴퓨터** 노드로 이동 하 여 커넥터 서버를 선택 합니다.
    - 마우스 오른쪽 단추를 클릭 하 고 **속성**  ->  **위임**   탭을 선택 합니다.
    -  **지정한 서비스에 대 한 위임용 으로만이 컴퓨터 트러스트를**선택 합니다.
    -  **모든 인증 프로토콜 사용**을 선택 합니다.
    -  **이 계정이 위임 된 자격 증명을 제공할 수 있는 서비스**입니다.
        - 인쇄 서버 컴퓨터의 SPN (서비스 사용자 이름)을 추가 합니다.
        - 서비스 유형에 대 한 호스트를 선택 합니다.
    ![Active Directory 위임](../media/hybrid-cloud-print/AD-Delegation.png)

3. IIS에서 Windows 인증을 사용 하도록 설정 했는지 확인 합니다.
    - 인쇄 서버에서 서버 관리자 > 도구 > IIS (인터넷 정보 서비스) 관리자를 엽니다.
    - 사이트로 이동 합니다.
    - **인증**을 두 번 클릭 합니다.
    - **Windows 인증** 을 클릭 하 고 **작업**아래에서 **사용** 을 클릭 합니다.
    ![인쇄 서버 IIS 인증](../media/hybrid-cloud-print/PrintServer-IIS-Authentication.png)

4. Single Sign-on을 구성 합니다.
    - Azure Portal에서 **Azure Active Directory**  >  **Enterprise 응용 프로그램**  >  **모든 응용 프로그램**으로 이동 합니다.
    - MopriaDiscoveryService 앱을 선택 합니다.
    - **응용 프로그램 프록시**로 이동 합니다. 사전 인증 방법을 **Azure Active Directory**로 변경 합니다.
    - **Single Sign-On**으로 이동합니다. Single Sign-On 방법으로 Windows 통합 인증을 선택 합니다.
    - **내부 응용 프로그램 spn** 을 인쇄 서버 컴퓨터의 spn으로 설정 합니다.
    - **위임 된 로그인 id** 를 사용자 계정 이름으로 설정 합니다.
    - EntperiseCloudPrint 앱에 대해 반복 합니다.
    ![AAD Single Sign-on IWA](../media/hybrid-cloud-print/AAD-SingleSignOn-IWA.png)

### <a name="step-6---configure-the-required-mdm-policies"></a>6 단계-필요한 MDM 정책 구성

1. MDM 공급자에 로그인 합니다.
2. 엔터프라이즈 클라우드 인쇄 정책 그룹을 찾고 아래 지침에 따라 정책을 구성 합니다.
    - CloudPrintOAuthAuthority = `https://login.microsoftonline.com/<Azure AD Directory ID>` 입니다. 디렉터리 ID는 Azure Active Directory > 속성에서 찾을 수 있습니다.
    - CloudPrintOAuthClientId = \( \) 네이티브 앱의 응용 프로그램 클라이언트 ID 값입니다. Azure Active Directory > 앱 등록에서이를 검색 하 > 네이티브 앱 > 개요를 선택할 수 있습니다.
    - Cloud프린터 검색 끝점 = Moapp.config의 외부 URL 검색 서비스 앱입니다. Azure Active Directory > 엔터프라이즈 응용 프로그램에서이를 찾을 수 > 응용 프로그램 프록시 > Mopria 검색 서비스 앱을 선택 합니다. **이는 정확히 동일 하지만 후행/를 포함 하지 않아야 합니다**.
    - MopriaDiscoveryResourceId = Mocea 검색 서비스 앱의 응용 프로그램 ID URI입니다. 이는 Azure Active Directory > > 앱 등록에서 찾을 수 있으며, 검색 서비스 앱 > 개요를 선택 합니다. **후행/와 정확히 동일 해야 합니다**.
    - CloudPrintResourceId = 엔터프라이즈 클라우드 인쇄 앱의 응용 프로그램 ID URI입니다. Azure Active Directory > 앱 등록에서이를 찾을 수 > Enterprise Cloud 인쇄 앱 > 개요를 선택 합니다. **후행/와 정확히 동일 해야 합니다**.
    - Discoverymax프린터 Limit = \<a positive integer\> 입니다.

> 참고: Microsoft Intune 서비스를 사용 하는 경우 클라우드 프린터 범주에서 이러한 설정을 찾을 수 있습니다.

|Intune 표시 이름                     |정책                         |
|----------------------------------------|-------------------------------|
|프린터 검색 URL                   |Cloud프린터 검색 끝점  |
|프린터 액세스 기관 URL            |CloudPrintOAuthAuthority       |
|Azure Native client 앱 GUID            |CloudPrintOAuthClientId        |
|인쇄 서비스 리소스 URI              |CloudPrintResourceId           |
|쿼리할 최대 프린터 수 (모바일 전용)  |Discoverymax프린터 제한       |
|프린터 검색 서비스 리소스 URI  |MopriaDiscoveryResourceId      |

> 참고: 클라우드 인쇄 정책 그룹을 사용할 수 없지만 MDM 공급자가 OMA-URI 설정을 지 원하는 경우 동일한 정책을 설정할 수 있습니다.  추가 정보는 [이](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority) 에 대 한 정보를 참조 하세요.

    - OMA-URI 값
        - CloudPrintOAuthAuthority =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority
            - 값 =https://login.microsoftonline.com/<Azure AD Directory ID>
        - CloudPrintOAuthClientId =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId
            - 값 = <Azure AD 네이티브 앱의 응용 프로그램 ID>
        - Cloud프린터 Discoveryendpoint =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint
            - 값 = Moapp.config의 외부 URL (정확히 동일 해야 하지만 뒤에 오는/는 제외)
        - MopriaDiscoveryResourceId =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId
            - 값 = Mopria 검색 서비스 앱의 응용 프로그램 ID URI
        - CloudPrintResourceId =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId
            - 값 = 엔터프라이즈 클라우드 인쇄 앱의 응용 프로그램 ID URI
        - Discoverymax프린터 Limit =./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit
            - 값 = 양의 정수

### <a name="step-7---publish-the-shared-printer"></a>7 단계-공유 프린터 게시

1. 인쇄 서버에 원하는 프린터를 설치 합니다.
2. 프린터 속성 UI를 통해 프린터를 공유 합니다.
3. 액세스 권한을 부여 하려면 원하는 사용자 집합을 선택 합니다.
4. 변경 내용을 저장 하 고 프린터 속성 창을 닫습니다.
5. Windows 10이 하 버전의 생성자 업데이트를 준비 합니다. 컴퓨터를 Azure AD에 가입 하 고 온-프레미스 Active Directory와 동기화 된 사용자로 로그인 하 고 MopriaDeviceDb. db 파일에 대 한 적절 한 사용 권한이 부여 되었습니다.
6. Windows 10 컴퓨터에서 관리자 권한 Windows PowerShell 명령 프롬프트를 엽니다.
    - 다음 명령을 실행합니다.
        - `find-module -Name PublishCloudPrinter`컴퓨터가 PowerShell 갤러리에 연결할 수 있는지 확인 하려면 (PSGallery)
        - `install-module -Name PublishCloudPrinter`

            > 참고: ' PSGallery '는 신뢰할 수 없는 리포지토리입니다. 라는 메시지가 표시 될 수 있습니다.  ' Y '를 입력 하 여 설치를 계속 합니다.

        - `Publish-CloudPrinter`
        - Printer = 공유 프린터 이름입니다. 이 이름은 인쇄 서버에서 열린 프린터 속성의 **공유** 탭에 표시 된 공유 이름과 정확히 일치 해야 합니다.

        ![인쇄 서버 프린터 속성](../media/hybrid-cloud-print/PrintServer-PrinterProperties.png)

        - 제조업체 = 프린터 제조업체입니다.
        - 모델 = 프린터 모델입니다.
        - OrgLocation = 프린터 위치를 지정 하는 JSON 문자열입니다 (예:).

            `{attrs: [{category:country, vs:USA, depth:0}, {category:organization, vs:Microsoft, depth:1}, {category:site, vs:Redmond, WA, depth:2}, {category:building, vs:Building 1, depth:3}, {category:floor_number, vs:1, depth:4}, {category:room_name, vs:1111, depth:5}]}`

        - Sddl = 프린터에 대 한 권한을 나타내는 SDDL 문자열입니다.
            - 인쇄 서버에 관리자로 로그온 한 후 게시할 프린터에 대해 다음 PowerShell 명령을 실행 `(Get-Printer PrinterName -full).PermissionSDDL` 합니다.
            - 위의 명령에서 결과에 **O:ba** 를 접두사로 추가 합니다. 예를 들어 이전 명령에서 반환 된 문자열이 G:DUD: (A; OICI; FA;;;) 인 경우 WD), SDDL = O:BAG: DUD: (A; O:BAG; FA;;;) WD).
        - DiscoveryEndpoint = Azure Portal에 로그인 한 다음 엔터프라이즈 응용 프로그램에서 문자열을 가져옵니다. > Mopria 검색 서비스 앱 > 응용 프로그램 프록시 > 외부 URL입니다. 후행/를 생략 합니다.
        - PrintServerEndpoint = Azure Portal에 로그인 한 다음 엔터프라이즈 응용 프로그램 > 엔터프라이즈 클라우드 인쇄 앱 > 응용 프로그램 프록시 > 외부 URL에서 문자열을 가져옵니다. 후행/를 생략 합니다.
        - AzureClientId = 등록 된 네이티브 응용 프로그램의 응용 프로그램 ID입니다.
        - AzureTenantGuid = Azure AD 테 넌 트의 디렉터리 ID입니다.
        - DiscoveryResourceId = Mopria 검색 서비스 응용 프로그램의 응용 프로그램 ID URI입니다.

    - 모든 필수 매개 변수 값은 명령줄에도 입력할 수 있습니다. 구문은 다음과 같습니다.

        `Publish-CloudPrinter -Printer <string> -Manufacturer <string> -Model <string> -OrgLocation <string> -Sddl <string> -DiscoveryEndpoint <string> -PrintServerEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        명령 샘플:

        `Publish-CloudPrinter -Printer HcpTestPrinter -Manufacturer Manufacturer1 -Model Model1 -OrgLocation '{attrs: [{category:country, vs:USA, depth:0}, {category:organization, vs:MyCompany, depth:1}, {category:site, vs:MyCity, State, depth:2}, {category:building, vs:Building 1, depth:3}, {category:floor_name, vs:1, depth:4}, {category:room_name, vs:1111, depth:5}]}' -Sddl O:BAG:DUD:(A;OICI;FA;;;WD) -DiscoveryEndpoint https://mopriadiscoveryservice-contoso.msappproxy.net/mcs -PrintServerEndpoint https://enterprisecloudprint-contoso.msappproxy.net/ecp -AzureClientId dbe4feeb-cb69-40fc-91aa-73272f6d8fe1 -AzureTenantGuid 8de6a14a-5a23-4c1c-9ae4-1481ce356034 -DiscoveryResourceId https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/`

    - 다음 명령을 사용 하 여 프린터가 게시 되었는지 확인 합니다.

        `Publish-CloudPrinter -Query -DiscoveryEndpoint <string> -AzureClientId <string> -AzureTenantGuid <string> -DiscoveryResourceId <string>`

        명령 샘플:

        `Publish-CloudPrinter -Query -DiscoveryEndpoint https://mopriadiscoveryservice-contoso.msappproxy.net/mcs -AzureClientId dbe4feeb-cb69-40fc-91aa-73272f6d8fe1 -AzureTenantGuid 8de6a14a-5a23-4c1c-9ae4-1481ce356034 -DiscoveryResourceId https://mopriadiscoveryservice-contoso.msappproxy.net/mcs/`

## <a name="verify-the-deployment"></a>배포 확인

MDM 정책이 구성 된 Azure AD 조인 장치에서 다음을 수행 합니다.
- 웹 브라우저를 열고 msappproxy.net/mcs/services로 이동 합니다 https://mopriadiscoveryservice- *tenant-name*.
- 이 끝점의 기능 집합을 설명 하는 JSON 텍스트가 표시 되어야 합니다.
- **설정**  >  **장치**  >  **프린터 & 스캐너**로 이동 합니다.
    - **프린터 또는 스캐너 추가**를 클릭 합니다.
    - 클라우드 프린터 검색 (또는 최신 Windows 10 컴퓨터에서 내 조직의 프린터 검색) 링크를 확인 해야 합니다.
    - 링크를 클릭 합니다.
    - 검색 위치 선택 링크를 클릭 합니다.
        - 장치 위치 계층이 표시 됩니다.
    - 위치를 선택 하 고 **확인** 을 클릭 한 다음 **검색** 단추를 클릭 하 여 프린터를 찾습니다.
    - 프린터를 선택 하 고 **장치 추가** 단추를 클릭 합니다.
    - 프린터를 성공적으로 설치한 후 즐겨 찾는 앱에서 프린터로 인쇄 합니다.

> 참고: EcpPrintTest 프린터를 사용 하는 경우 인쇄 서버 컴퓨터의 C: \\ ecpprinttest \\ ecpprinttest .xps 위치에서 출력 파일을 찾을 수 있습니다.

## <a name="troubleshooting"></a>문제 해결

다음은 HCP 배포 중에 발생 하는 일반적인 문제입니다.

|오류 |권장되는 단계 |
|------|------|
|CloudPrintDeploy PowerShell 스크립트 실패 | <ul><li>Windows Server에 최신 업데이트가 있는지 확인 합니다.</li><li>WSUS (Windows Server Update Services)를 사용 하는 경우 [wsus/SCCM을 사용 하는 경우 필요에 따라 기능을 설정 하 고 언어 팩을 사용 하도록 설정 하는 방법](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs)을 참조 하세요.</li></ul> |
|SQLite를 설치 하지 못했습니다. 메시지: ' System.web ' 패키지에 대 한 종속성 루프가 검색 되었습니다. | Install-Package system.object-providername nuget-SkipDependencies<br>EF6-providername nuget-SkipDependencies을 설치 합니다.<br>설치-패키지 시스템.. n a m.<br><br>패키지를 성공적으로 다운로드 한 후에는 모두 동일한 버전 인지 확인 합니다. 그렇지 않으면-requiredversion 매개 변수를 위의 명령에 추가 하 고 동일한 버전으로 설정 합니다. |
|프린터를 게시 하지 못했습니다. | <ul><li>통과 인증 인증의 경우 프린터를 게시 하는 사용자에 게 게시 데이터베이스에 대 한 적절 한 권한이 부여 되었는지 확인 합니다.</li><li>Azure AD 사전 인증의 경우 IIS에서 Windows 인증이 사용 되도록 설정 되어 있는지 확인 합니다. 5.3 단계를 참조 하세요. 또한 먼저 통과 인증을 시도 합니다. 통과 인증 인증을 사용할 경우 응용 프로그램 프록시와 관련 된 문제일 수 있습니다. [응용 프로그램 프록시 문제 및 오류 메시지 문제 해결을](https://docs.microsoft.com/azure/active-directory/manage-apps/application-proxy-troubleshoot)참조 하세요. 통과로 전환 하면 Single Sign-On 설정이 다시 설정 됩니다. 5 단계를 다시 방문 하 여 Azure AD 사전 인증을 다시 설정 합니다.</li></ul> |
|인쇄 작업이 프린터 상태로 전송 되는 상태로 유지 됩니다. | <ul><li>커넥터 서버에서 TLS 1.2를 사용 하도록 설정 했는지 확인 합니다. 2.1 단계에서 연결 된 문서를 참조 하세요.</li><li>커넥터 서버에서 HTTP2이 사용 되지 않도록 설정 되어 있는지 확인 합니다. 2.1 단계에서 연결 된 문서를 참조 하세요.</li></ul> |

다음은 문제 해결에 도움이 될 수 있는 로그의 위치입니다.

|구성 요소 |로그 위치 |
|------|------|
|Windows 10 클라이언트 | <ul><li>이벤트 뷰어를 사용 하 여 Azure AD 작업 로그를 확인 합니다. **시작** 을 클릭 하 고 이벤트 뷰어를 입력 합니다. Microsoft > Windows > AAD > 작업 > 응용 프로그램 및 서비스 로그로 이동 합니다.</li><li>피드백 허브를 사용 하 여 로그를 수집 합니다. [피드백 허브 앱을 사용 하 여 Microsoft로 사용자 의견 보내기](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) 를 참조 하세요.</li></ul> |
|커넥터 서버 | 이벤트 뷰어를 사용 하 여 응용 프로그램 프록시의 로그를 확인 합니다. **시작** 을 클릭 하 고 이벤트 뷰어를 입력 합니다. 응용 프로그램 및 서비스 로그 > Microsoft > AadApplicationProxy > 커넥터 > 관리자로 이동 합니다. |
|인쇄 서버 | Moapp.config에 대 한 로그 검색 서비스 앱 및 엔터프라이즈 클라우드 인쇄 앱은 C:\inetpub\logs\LogFiles\W3SVC1.에서 찾을 수 있습니다. |
