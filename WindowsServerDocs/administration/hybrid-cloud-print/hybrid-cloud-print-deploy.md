---
title: Windows Server 하이브리드 클라우드 인쇄를 배포 합니다.
description: Microsoft 하이브리드 클라우드 인쇄를 설정 하는 방법
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: Windows Server 2016
ms.tgt_pltfrm: na
ms.topic: ''
ms.assetid: fc239aec-e719-47ea-92fc-d82a7247c5e9
author: msjimwu
ms.author: coreyp
manager: dongill
ms.date: 3/15/2018
ms.openlocfilehash: 6e9833489277c84739d489da34d352db8f565663
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881844"
---
# <a name="deploy-windows-server-hybrid-cloud-print-with-pre-authentication"></a>사전 인증을 사용한 Windows Server 하이브리드 클라우드 인쇄 배포

>적용 대상: Windows Server 2016

이 항목에서는 IT 관리자에 게 Microsoft 하이브리드 클라우드 인쇄 솔루션의 종단 간 배포를 설명 합니다. 인쇄 서버와 Azure Active Directory에 가입 하 고 MDM 관리 수 있도록 실행 하는 기존 Windows 서버 기반으로이 솔루션 계층을 검색 하 고 조직에 인쇄 장치 프린터를 관리 합니다.

## <a name="pre-requisites"></a>필수 구성 요소

구독, 서비스 및이 설치를 시작 하기 전에 확보 해야 하는 컴퓨터의 여러 가지가 있습니다. 이러한 속성은 다음과 같습니다.

-   Azure AD premium 구독
    
    참조 [Azure 구독 시작](https://azure.microsoft.com/trial/get-started-active-directory/), 평가판 Azure 구독에 대 한 합니다. 

-   Intune과 같은 MDM 서비스
    
    참조 [Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune), Intune에 대 한 평가판 구독에 대 한 합니다.

-   Windows Server Active Directory 실행

    참조 [단계별: Windows Server 2016의 Active Directory 설정](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/), Active Directory 설정 도움말에 대 한 합니다.

-   도메인 가입 인쇄 서버로 실행 중인 Windows Server 2016
    
    참조 [추가 역할 및 기능 마법사를 사용 하 여 역할, 역할 서비스 및 기능 설치](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw), Windows Server에서 역할 및 역할 서비스를 설치 하는 방법에 대 한 정보에 대 한 합니다.

-   Azure AD 연결
    
    참조 [Azure AD Connect의 사용자 지정 설치](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom), Azure AD Connect를 설정 하는 도움말에 대 한 합니다.

-   Azure 응용 프로그램 프록시 커넥터는 별도 도메인에 가입 된 Windows Server 컴퓨터
    
    참조 [커넥터를 설치 하 고 응용 프로그램 프록시를 사용 하 여 시작](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable), Azure 응용 프로그램 프록시 커넥터를 설정 하는 도움말에 대 한 합니다.

-   연결 하는 공용 도메인 이름
    
    Azure에서 생성 된 도메인 이름을 사용 하거나 고유한 도메인 이름을 구입 수 있습니다.

## <a name="deployment-steps"></a>배포 단계

이 가이드는 다섯 (5) 설치 단계를 설명합니다.

- 1단계: Azure AD 간의 동기화 할 Azure AD Connect를 설치 하 고 온-프레미스 AD
- 2단계: 인쇄 서버에 하이브리드 클라우드 인쇄 패키지 설치
- 3단계: Install Azure 응용 프로그램 프록시 (AAP) kerberos 제한 위임 (KCD)
- 4단계: 필요한 MDM 정책을 구성 합니다.
- 5단계: 공유 프린터를 게시 합니다.

### <a name="step-1---install-azure-ad-connect-to-sync-between-azure-ad-and-on-premises-ad"></a>1 단계-Azure AD Connect 설치를 Azure AD 간의 동기화 및 온-프레미스 AD
1. Windows Server Active Directory 컴퓨터에서 Azure AD Connect 소프트웨어를 다운로드 합니다.
2. Azure AD Connect 설치 패키지를 실행 하 고 선택 **기본 설정 사용**
3. 설치 프로세스에서 요청 된 정보를 입력 하 고 클릭 **설치**

### <a name="step-2---install-hybrid-cloud-print-package-on-the-print-server"></a>2 단계-인쇄 서버에서 패키지 설치 하이브리드 클라우드 인쇄

1. 하이브리드 클라우드 인쇄 PowerShell 모듈 설치
    -  관리자 권한 PowerShell 명령 프롬프트에서 다음 명령을 실행합니다
        - `find-module -Name "PublishCloudPrinter"` PowerShell 갤러리 (PSGallery) 컴퓨터에 연결할 수 있는지 확인 하려면
        - `install-module -Name "PublishCloudPrinter"`

    > 참고: 메시징 표시 될 수 있습니다는 신뢰할 수 없는 리포지토리의 'PSGallery' 않다는 합니다.  설치를 계속 하려면 ' y'를 입력 합니다.

2. 하이브리드 클라우드 인쇄 솔루션 설치
    - 동일한 관리자 권한 PowerShell 명령 프롬프트에서 디렉터리를 변경 `C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`
    - 실행 <br>
        `CloudPrintDeploy.ps1 -AzureTenant <Domain name used by Azure AD Connect> -AzureTenantGuid <Azure AD Directory ID>`
3.  SSL을 지원 하도록 IIS 끝점 2 개를 구성 합니다.
    -   자체 서명 된 인증서 또는 일부 신뢰할 수 있는 인증 기관 (CA)에서 발급 한 SSL 인증서 일 수 있습니다.
    -  자체 서명 된 인증서를 사용 하는 경우 클라이언트 컴퓨터에 인증서를 가져올 있는지 확인
4.  SQLite 패키지 설치
    - 관리자 권한 PowerShell 명령 프롬프트를 열으십시오
    - System.Data.SQLite nuget 패키지를 다운로드 하려면 다음 명령을 실행 합니다. <br>
        `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`
    - 패키지를 설치 하려면 다음 명령을 실행 합니다.<br>
    `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

    > 참고: 다운로드 되지 않도록 최신 버전을 설치 하는 것이 좋습니다.는 "-requiredversion" 옵션입니다.

5.  SQLite dll MopriaCloudService Webapp 복사할 \<bin\> 폴더 (**c:\\inetpub\\wwwroot\\MopriaCloudService\\bin**): <br>
    - SQLite 바이너리에 있어야 합니다. "\\Program Files\\PackageManagement\\NuGet\\패키지"

            \\System.Data.SQLite.**Core**.x.x.x.x\\lib\\net46\\System.Data.SQLite.dll
            --\> \<bin\>\\System.Data.SQLite.dll  
            \\System.Data.SQLite.**Core**.x.x.x.x\\build\\net46\\x86\\SQLite.Interop.dll
            --\> \<bin\>\\**x86**\\SQLite.Interop.dll  
            \\System.Data.SQLite.**Core**.x.x.x.x\\build\\net46\\x64\\SQLite.Interop.dll
            --\> \<bin\>\\**x64**\\SQLite.Interop.dll
            \\System.Data.SQLite.**Linq**.x.x.x.x\\lib\\net46\\System.Data.SQLite.Linq.dll
            --\> \<bin\>\\System.Data.SQLite.Linq.dll  
            \\System.Data.SQLite.**EF6**.x.x.x.x\\lib\\net46\\System.Data.SQLite.EF6.dll
            --\> \<bin\>\\System.Data.SQLite.EF6.dll

    > 참고: x.x.x.x는 SQLite 버전 이상에서는 설치 된.

6.  업데이트를 `c:\inetpub\wwwroot\MopriaCloudService\web.config` SQLite 버전 x.x.x.x 다음에 포함할 파일 \<런타임\>/\<assemblyBinding\> 섹션:

        <dependentAssembly>
        assemblyIdentity name="System.Data.SQLite" culture="neutral" publicKeyToken="db937bc2d44ff139" /
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.Core" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.EF6" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>
        <dependentAssembly>
        <assemblyIdentity name="System.Data.SQLite.Linq" culture="neutral" publicKeyToken="db937bc2d44ff139" />
        <bindingRedirect oldVersion="0.0.0.0-x.x.x.x" newVersion="x.x.x.x" />
        </dependentAssembly>

7. SQLite 데이터베이스를 만듭니다.
    -  다운로드 및 설치에서 SQLite 도구 이진 파일 <https://www.sqlite.org/>
    -  로 이동 **c:\\inetpub\\wwwroot\\MopriaCloudService\\데이터베이스** 디렉터리
    -  이 디렉터리에 데이터베이스를 만들려면 다음 명령을 실행 합니다.  `sqlite3.exe MopriaDeviceDb.db ".read MopriaSQLiteDb.sql"`
    -  파일 탐색기에서 보안 탭에서 Mopria 데이터베이스에 게시할 수 있는 사용자/그룹에 추가할 MopriaDeviceDb.db 파일 속성을 엽니다.
        - 만 필요한 관리자 사용자 그룹을 추가 하는 것이 좋습니다.
8. OAuth2 인증을 지원 하도록 Azure AD를 사용 하 여 2 개의 웹 앱을 등록 합니다.
    -   Azure AD 테 넌 트 관리 포털에 전역 관리자로 로그인
        1. 인쇄 끝점을 추가 하려면 "앱 등록" 탭 이동
            -   응용 프로그램을 추가, "새 응용 프로그램 등록" 선택
            -   적절 한 이름을 제공 하 고 선택 "웹 앱 / API"
            -   Sign-on URL = "http://MicrosoftEnterpriseCloudPrint/CloudPrint"
        2.  검색 끝점에 대 한 반복
            -   Sign-on URL = "http://MopriaDiscoveryService/CloudPrint"
        3.  네이티브 클라이언트 응용 프로그램에 대 한 반복
            -   앱 이름을 제공 하는 경우 "네이티브 클라이언트 응용 프로그램"을 "응용 프로그램 종류로"를 선택 했는지 확인
            -   리디렉션 URI = "https://\<services machine 끝점\>/RedirectUrl"
        4.  네이티브 클라이언트 앱 "설정"으로 이동
            -   이후 설치 단계에 사용 되는 "응용 프로그램 ID" 값을 복사 합니다.
            -   "필요한 권한"을 선택 합니다.
                1.  "추가" 클릭
                2.  "API 선택" 클릭
                3.  앱 끝점을 만들 때 정의한 이름으로 인쇄 끝점과 검색 끝점에 대 한 검색
                4.  끝점 2 개를 추가 합니다.
                5.  각 응용 프로그램 끝점에 대 한 "위임 된 권한" 옵션이 설정 되어 있는지 확인
                6.  맨 아래에 "완료" 단추를 클릭 하 고 있는지 확인
                7.  두 끝점을 추가한 후 "권한 부여"를 클릭 합니다.  요청을 승인 하 라는 메시지가 나타나면 "예"를 선택 합니다.
            -   "리디렉션 URI"로 이동한 후 목록에 다음 리디렉션 Uri를 추가 합니다. `ms-appx-web://Microsoft.AAD.BrokerPlugin/\<NativeClientAppID\>`
                `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

### <a name="step-3---install-azure-application-proxy-aap-with-kerberos-constrained-delegation-kcd"></a>3 단계-Kerberos를 사용 하 여 Azure 응용 프로그램 프록시 (AAP) 설치 제한 위임 (KCD)
1. Azure AD (AAD) 테 넌 트 관리 포털에 로그인
    - AAD 메뉴 목록에서 "응용 프로그램 프록시"를 선택 합니다.
    - 화면 맨 위에 있는 "응용 프로그램 프록시 사용"을 클릭
    - 웹 응용 프로그램 프록시 (WAP)으로 작동 하는 도메인에 가입 된 Windows Server 컴퓨터에 "응용 프로그램 프록시 커넥터"를 다운로드 합니다.
2. WAP 컴퓨터에 설치 "응용 프로그램 프록시 커넥터"를 관리자 권한으로 로그인
    - 설치 중에 게 응용 프로그램 프록시 커넥터를 자격 증명 AAP에서 사용 하도록 설정 하려는 Azure 프로그램 개념
    - WAP 컴퓨터가 도메인에 온-프레미스 Active Directory에 가입 되어 있는지 확인
3. Active Directory 컴퓨터에서로 이동 **사용자 및 컴퓨터 도구->**
    - 응용 프로그램 프록시 커넥터를 실행 하는 컴퓨터를 선택 합니다.
    - 마우스 오른쪽 단추로 클릭 **속성-위임 >** 탭
    - 선택 **만 지정한 서비스에 대 한 위임용으로이 컴퓨터 트러스트 합니다.**
    - 선택 **모든 인증 프로토콜을 사용 합니다.**
    - 아래 **이 계정이 위임 된 자격 증명을 표시할 수 있는 서비스**
        - 서비스 (MopriaDiscoveryService 및 MicrosoftEnterpriseCloudPrint 서비스)를 실행 하는 컴퓨터의 SPN id 값을 추가
            - SPN에 대 한 자체 컴퓨터의 SPN을 즉, 입력 "HOST/\<MachineName\>.\<Domain\>"<br>
                `HOST/appServer.Contoso.com`
4. AAD 테 넌 트 관리 포털로 돌아가서 응용 프로그램 프록시를 추가 합니다.
    - 로 이동 합니다 **엔터프라이즈 응용 프로그램** 탭
    - 클릭 **새 응용 프로그램**
    - 선택 **온-프레미스 응용 프로그램** 필드를 입력 하 고
        - 이름: 원하는 이름
        - 내부 URL: 이 url은 WAP 컴퓨터에 액세스할 수 있는 Mopria 검색 클라우드 서비스에 내부 URL
        - 외부 URL: 조직에 적합 한 구성
        - 사전 인증 방법: Azure Active Directory

    >   참고: 위의 모든 설정을 찾을 수 없는, 하는 경우 사용 가능한 설정 사용 하 여 프록시 추가 다음 방금 만든 응용 프로그램 프록시를 선택 및 이동 합니다 **응용 프로그램 프록시** 탭 및 위의 모든 정보를 추가 합니다.

    - 만들어지면 돌아갑니다 **엔터프라이즈 응용 프로그램** -> **모든 응용 프로그램**, 방금 만든 새 응용 프로그램 선택
    - 로 이동 **Single sign on**, "Single sign-on 모드"는 "통합 Windows 인증"으로 설정 되어 있는지 확인
    - "내부 응용 프로그램 SPN" 위의 3.3 단계에서에서 지정한 spn 설정
    - "위임 된 로그인 Id"는 "사용자 계정 이름"으로 설정 되어 있는지 확인

5. 엔터프라이즈 클라우드 인쇄 서비스에 대 한 위의 4를 반복 하 고 엔터프라이즈 클라우드 인쇄 서비스에 내부 URL을 제공 합니다.
6. Azure AD 테 넌 트 관리 포털로 돌아가서 이동할 **앱 등록** 네이티브 클라이언트 앱 선택-> "설정" 및
    - 선택 **필요한 권한**
        - 방금 만든 2 개의 새로운 프록시 기능 추가
        - 두 응용 프로그램에 대 한 위임 된 권한 부여
        - 프록시 응용 프로그램을 모두 추가한 후 "권한 부여"를 클릭 합니다.  요청을 승인 하 라는 메시지가 나타나면 "예"를 선택 합니다.

7. Mopria 클라우드 서비스 및 엔터프라이즈 클라우드 인쇄 서비스 컴퓨터에 대해 IIS에서 Windows 인증을 사용 하도록 설정
    - Windows 인증 기능이 설치 되어 있는지 확인 합니다.
        1. 서버 관리자 열기
        2. 클릭 **관리**
        3. 클릭 **역할 및 기능 추가**
        4. 선택 **역할 기반 또는 기능 기반 설치**
        5. 서버 선택
        6. 웹 서버 (IIS)에서 웹 서버-> 보안->를 선택 **Windows 인증**
        7. 설치를 완료할 때까지 다음을 클릭합니다
    - IIS에서 Windows 인증을 사용 하도록 설정 합니다.
        1. 인터넷 정보 서비스 (IIS) 관리자를 열려면
        2. 각 서비스/사이트:
            1.  서비스/사이트를 선택 합니다.
            2.  두 번 클릭 **인증**
            3.  클릭 **Windows 인증** 클릭 **활성화** 아래의 **작업**

### <a name="step-4---configure-the-required-mdm-policies"></a>4 단계-필요한 MDM 정책을 구성 합니다.
- MDM 공급자에 로그인
- 엔터프라이즈 클라우드 인쇄 정책 그룹을 찾아 아래 지침에 따라 정책을 구성 합니다.
    - CloudPrintOAuthAuthority = https://login.microsoftonline.com/\<Azure AD Directory ID\>
    - CloudPrintOAuthClientId Azure AD 관리 포털에 등록 하는 기본 웹 앱의 "응용 프로그램 ID" 값 =
    - CloudPrinterDiscoveryEndPoint = Mopria 검색 서비스 Azure 응용 프로그램 프록시의 3.3 단계에서에서 만든 외부 URL (후행 없이 동일 하지만 정확히 있어야 /)
    - MopriaDiscoveryResourceId = Mopria 검색 서비스 Azure 응용 프로그램 프록시의 3.4 단계에서에서 만든 외부 URL (해야 똑같이 포함 후행 /)
    - CloudPrintResourceId = 엔터프라이즈 클라우드 인쇄 서비스 Azure 응용 프로그램 프록시의 3.5 단계에서에서 만든 외부 URL (해야 똑같이 포함 후행 /)
    - DiscoveryMaxPrinterLimit = \<양의 정수\>

>   참고: Microsoft Intune 서비스를 사용 하는 경우에 "클라우드 프린터" 범주 아래에서 이러한 설정을 찾을 수 있습니다.

|Intune 표시 이름                     |정책                         |
|----------------------------------------|-------------------------------|
|프린터 검색 URL                   |CloudPrinterDiscoveryEndpoint  |
|프린터 액세스 인증 기관 URL            |CloudPrintOAuthAuthority       |
|Azure 네이티브 클라이언트 앱 GUID            |CloudPrintOAuthClientId        |
|인쇄 서비스 리소스 URI              |CloudPrintResourceId           |
|(모바일 전용) 쿼리할 최대 프린터 수  |DiscoveryMaxPrinterLimit       |
|프린터 검색 서비스 리소스 URI  |MopriaDiscoveryResourceId      |

>   참고: 클라우드 인쇄 정책 그룹을 사용할 수 없는 MDM 공급자가 지 원하는 OMA URI 설정 하지만 동일한 정책을 설정할 수 있습니다.  이를 참조 하십시오 <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority">문서</a> 대 한 자세한 내용은 합니다.

- OMA-URI
    - `CloudPrintOAuthAuthority = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority`
        - Value = `https://login.microsoftonline.com/`\<Azure AD Directory ID\>
    - `CloudPrintOAuthClientId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId`
        - 값 = \<Azure AD 네이티브 앱의 응용 프로그램 ID\>
    - `CloudPrinterDiscoveryEndPoint = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint`
        - 값 = Mopria 검색 서비스 Azure 응용 프로그램 프록시의 3.3 단계에서에서 만든 외부 URL (후행 없이 동일 하지만 정확히 있어야 /)
    - `MopriaDiscoveryResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId`
        - 값 = Mopria 검색 서비스 Azure 응용 프로그램 프록시의 3.4 단계에서에서 만든 외부 URL (해야 똑같이 포함 후행 /)
    - `CloudPrintResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId`
        - 값 = 엔터프라이즈 클라우드 인쇄 서비스 Azure 응용 프로그램 프록시의 3.5 단계에서에서 만든 외부 URL (해야 똑같이 포함 후행 /)
    - `DiscoveryMaxPrinterLimit = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit`
        - 값 = \<양의 정수\>

### <a name="step-5---publish-desired-shared-printers"></a>5 단계-원하는 공유 프린터를 게시 합니다.
1. 인쇄 서버에 원하는 프린터를 설치 합니다.
2. 프린터 속성 UI를 통해 프린터를 공유 합니다.
3. 원하는 액세스 권한을 부여할 사용자 선택
4. 변경 내용을 저장 하 고 프린터 속성 창을 닫습니다
5. Windows 10 Fall Creator Update 컴퓨터에서 관리자 권한 Windows PowerShell 명령 프롬프트를 열으십시오
    1. 다음 명령을 실행 합니다.
        - `find-module -Name "PublishCloudPrinter"` PowerShell 갤러리 (PSGallery) 컴퓨터에 연결할 수 있는지 확인 하려면
        - `install-module -Name "PublishCloudPrinter"`

        >   참고: 메시징 표시 될 수 있습니다는 신뢰할 수 없는 리포지토리의 'PSGallery' 않다는 합니다.  설치를 계속 하려면 ' y'를 입력 합니다.

        - Publish-CloudPrinter
            - 프린터 = 정의 된 공유 프린터 이름
            - 제조업체는 프린터 제조업체 =
            - 모델 = 프린터 모델
            - OrgLocation = 예: 프린터 위치를 지정 하는 JSON 문자열.   `{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"Microsoft", "depth":1}, {"category":"site", "vs":"Redmond, WA", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}`
            - Sddl = 프린터에 대 한 권한을 나타내는 SDDL 문자열입니다. 이 프린터 속성 보안 탭을 적절 하 게 수정 하 고 다음 명령 프롬프트에서 다음 명령을 실행 하 여 얻을 수 있습니다. `(Get-Printer PrinterName -full).PermissionSDDL`
                예: "G:DUD:(A;OICI;FA;;;WD)"

            > 참고: 추가 해야 합니다 **`O:BA`** 접두사로 결과에 위 명령 프롬프트 명령을에서 SDDL 설정으로 값을 설정 하기 전에 합니다.  예: SDDL = `O:BAG:DUD:(A;OICI;FA;;;WD)`

            - DiscoveryEndpoint = Mopria 검색 서비스 Azure 응용 프로그램 프록시의 3.4 단계에서에서 만든 외부 URL
            - PrintServerEndpoint = 엔터프라이즈 클라우드 인쇄 서비스 Azure 응용 프로그램 프록시의 3.5 단계에서에서 만든 외부 URL
            - AzureClientId 위에서 등록 된 웹 앱을 네이티브 값의 응용 프로그램 ID =
            - AzureTenantGuid Azure AD 테 넌 트의 디렉터리 ID =
            - DiscoveryResourceId 프록시 Mopria 검색 클라우드 서비스의 [옵션] 응용 프로그램 ID =

        > 참고: 모든 필수 매개 변수 값도 명령줄에서 입력할 수 있습니다.<br>
**게시 CloudPrinter** PowerShell 명령 구문: <br>
게시 CloudPrinter-프린터 \<문자열\> -제조업체 \<문자열\> -모델 \<문자열\> -OrgLocation \<문자열\> -Sddl \<문자열\> -DiscoveryEndpoint \<문자열\> -PrintServerEndpoint \<문자열\> -AzureClientId \<문자열\> -AzureTenantGuid \<문자열\> [-DiscoveryResourceId \<문자열\>] <br>
예제 명령: `publish-cloudprinter -Printer EcpPrintTest -Manufacturer Microsoft -Model FilePrinterEcp -OrgLocation '{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"MyCompany", "depth":1}, {"category":"site", "vs":"MyCity, State", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}' -Sddl "O:BAG:DUD:(A;OICI;FA;;;WD)" -DiscoveryEndpoint https://<services-machine-endpoint>/mcs -PrintServerEndpoint https://<services-machine-endpoint>/ecp -AzureClientId <Native Web App ID> -AzureTenantGuid <Azure AD Directory ID> -DiscoveryResourceId <Proxied Mopria Discovery Cloud Service App ID>`


## <a name="verifying-the-deployment"></a>배포 확인
Azure ad 가입 장치 구성 MDM 정책이 포함 된:
- 웹 브라우저를 열고 https:// 이동할&lt;services machine 끝점 &gt; /mcs / (검색 끝점에 대 한 외부 URL)을 서비스 합니다.
- 이 끝점의 기능 집합을 설명 하는 JSON 텍스트를 표시
- 로 이동 "OS 설정-\> 장치-\> 프린터 및 스캐너"
    - "클라우드 프린터 검색" 링크를 확인 해야
    - 링크를 클릭
    - "검색 위치를 선택 하십시오" 링크를 클릭 합니다.
        - 장치 위치 계층 구조 표시
    - 위치를 선택 하 고 클릭 **확인** 을 클릭 한 다음 **검색** 프린터 찾기를 단추
    - 프린터를 선택 하 고 클릭 **장치 추가** 단추
    - 성공적인 프린터 설치 후 프린터로 인쇄할 즐겨 찾는 앱에서

>   참고: "EcpPrintTest" 프린터를 사용 하는 경우 아래에 있는 인쇄 서버 컴퓨터에서 출력 파일을 찾을 수 있습니다 "c:\\ECPTestOutput\\EcpTestPrint.xps" 위치 합니다.
