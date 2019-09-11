---
title: Windows Server 하이브리드 클라우드 인쇄-통과 인증 배포
description: 통과 인증을 사용 하 여 Microsoft 하이브리드 클라우드 인쇄를 설정 하는 방법
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
ms.openlocfilehash: 8d4d842b917a52f2c6852cf5c3ed261c0be2cc1c
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866861"
---
# <a name="deploy-windows-server-hybrid-cloud-print-with-passthrough-authentication"></a>통과 인증을 사용 하 여 Windows Server 하이브리드 클라우드 인쇄 배포

>적용 대상: Windows Server 2016

IT 관리자를 위한이 항목에서는 Microsoft 하이브리드 클라우드 인쇄 솔루션의 종단 간 배포에 대해 설명 합니다. 이 솔루션은 인쇄 서버로 실행 되는 기존 Windows Server를 기반으로 하며, 연결 된 Azure Active Directory 및 MDM 관리 장치에서 조직 관리 프린터를 검색 하 고 인쇄할 수 있도록 합니다.

## <a name="pre-requisites"></a>필수 구성 요소

이 설치를 시작 하기 전에 획득 해야 하는 여러 구독, 서비스 및 컴퓨터가 있습니다. 이러한 속성은 다음과 같습니다.

-   Azure AD premium 구독
    
    Azure에 대 한 평가판 구독을 보려면 [azure 구독 시작](https://azure.microsoft.com/trial/get-started-active-directory/)을 참조 하세요. 

-   MDM 서비스 (예: Intune)
    
    Intune에 대 한 평가판 구독은 [Microsoft Intune](https://www.microsoft.com/en-us/cloud-platform/microsoft-intune)를 참조 하세요.

-   Active Directory으로 실행 되는 Windows Server

    단계별 [참고: Active Directory 설정에 대 한 도움말을](https://blogs.technet.microsoft.com/canitpro/2017/02/22/step-by-step-setting-up-active-directory-in-windows-server-2016/)보려면 Windows Server 2016에서 Active Directory를 설정 합니다.

-   인쇄 서버로 실행 되는 도메인에 가입 된 Windows Server 2016
    
    Windows Server에서 역할 및 역할 서비스를 설치 하는 방법에 대 한 자세한 내용은 역할 [및 기능 추가 마법사를 사용 하 여 역할, 역할 서비스 및 기능 설치](https://docs.microsoft.com/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#BKMK_installarfw)를 참조 하세요.

-   Azure AD 연결
    
    Azure AD Connect 설정에 대 한 도움말은 [Azure AD Connect의 사용자 지정 설치](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-custom)를 참조 하세요.

-   별도의 도메인에 가입 된 Windows Server 컴퓨터에서 프록시 커넥터 Azure 애플리케이션
    
    Azure 애플리케이션 프록시 커넥터 설정에 대 한 도움말은 [응용 프로그램 프록시 시작 및 커넥터 설치](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable)를 참조 하세요.

-   공용 도메인 이름
    
    Azure에서 만든 도메인 이름을 사용 하거나 고유한 도메인 이름을 구입할 수 있습니다.

## <a name="deployment-steps"></a>배포 단계

이 가이드에서는 5 개 (5) 설치 단계에 대해 설명 합니다.

- 1단계: Azure AD와 온-프레미스 AD 간에 동기화 Azure AD Connect 설치
- 2단계: 인쇄 서버에 하이브리드 클라우드 인쇄 패키지 설치
- 3단계: 통과 인증을 사용 하 여 AAP (Azure 애플리케이션 프록시 설치)
- 4단계: 필요한 MDM 정책 구성
- 5단계: 공유 프린터 게시

### <a name="step-1---install-azure-ad-connect-to-sync-between-azure-ad-and-on-premises-ad"></a>1 단계-Azure AD와 온-프레미스 AD 간 동기화를 위한 Azure AD Connect 설치
1. Windows Server Active Directory 컴퓨터에서 Azure AD Connect 소프트웨어를 다운로드 합니다.
2. Azure AD Connect 설치 패키지를 시작 하 고 **빠른 설정 사용** 을 선택 합니다.
3. 설치 과정에서 요청 된 정보를 입력 하 고 **설치** 를 클릭 합니다.

### <a name="step-2---install-hybrid-cloud-print-package-on-the-print-server"></a>2 단계-인쇄 서버에 하이브리드 클라우드 인쇄 패키지 설치

1. 하이브리드 클라우드 인쇄 PowerShell 모듈 설치
   - 관리자 권한 PowerShell 명령 프롬프트에서 다음 명령을 실행 합니다.
      - `find-module -Name "PublishCloudPrinter"`컴퓨터가 PowerShell 갤러리에 연결할 수 있는지 확인 하려면 (PSGallery)
      - `install-module -Name "PublishCloudPrinter"`

     > 참고: ' PSGallery '는 신뢰할 수 없는 리포지토리입니다. 라는 메시지가 표시 될 수 있습니다.  ' Y '를 입력 하 여 설치를 계속 합니다.

2. 하이브리드 클라우드 인쇄 솔루션 설치
    - 동일한 승격 PowerShell 명령 프롬프트에서 디렉터리를로 변경 합니다.`C:\Program Files\WindowsPowerShell\Modules\PublishCloudPrinter\1.0.0.0`
    - 실행 <br>
        `CloudPrintDeploy.ps1 -AzureTenant <Domain name used by Azure AD Connect> -AzureTenantGuid <Azure AD Directory ID>`
3. SSL을 지원 하도록 2 개의 IIS 끝점 구성
   -   SSL 인증서는 자체 서명 된 인증서 이거나 일부 신뢰할 수 있는 CA (인증 기관)에서 발급 한 인증서 일 수 있습니다.
   -  자체 서명 된 인증서를 사용 하는 경우 클라이언트 컴퓨터로 인증서를 가져왔는지 확인 합니다.
4. SQLite 패키지 설치
   - 관리자 권한 PowerShell 명령 프롬프트를 엽니다.
   - 다음 명령을 실행 하 여 시스템. SQLite nuget 패키지를 다운로드 합니다. <br>
       `Register-PackageSource -Name nuget.org -ProviderName NuGet -Location https://www.nuget.org/api/v2/ -Trusted -Force`
   - 다음 명령을 실행 하 여 패키지를 설치 합니다.<br>
   `Install-Package system.data.sqlite [-requiredversion x.x.x.x] -providername nuget`

   > 참고: "-Requiredversion" 옵션을 종료 하 여 최신 버전을 다운로드 하 고 설치 하는 것이 좋습니다.

5. SQLite dll을 \<MopriaCloudService Webapp bin\> 폴더 (**C:\\inetpub\\\\wwwroot\\MopriaCloudService bin**)에 복사 합니다. <br>
   - SQLite 이진\\파일은 "Program Files\\PackageManagement\\NuGet\\패키지"에 있어야 합니다.

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

   > 참고: x. x. x. x는 위에 설치 된 SQLite 버전입니다.

6. `c:\inetpub\wwwroot\MopriaCloudService\web.config` 다음 \<런타임assemblybinding\<섹션에서 SQLite 버전 x. x. x를 포함 하도록 파일을 업데이트 합니다.\> \>/

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
    -  에서 SQLite Tools 바이너리를 다운로드 하 여 설치 합니다.<https://www.sqlite.org/>
    -  **\\C: inetpub\\wwwroot\\MopriaCloudService데이터베이스디렉터리로이동합니다.\\**
    -  다음 명령을 실행 하 여이 디렉터리에 데이터베이스를 만듭니다.`sqlite3.exe MopriaDeviceDb.db ".read MopriaSQLiteDb.sql"`
    -  파일 탐색기에서 MopriaDeviceDb. db 파일 속성을 열어 보안 탭에서 데이터베이스에 게시할 수 있는 사용자/그룹을 추가 합니다.
        - 필요한 관리 사용자 그룹을 추가 하는 것이 좋습니다.
8. OAuth2 인증을 지원 하기 위해 Azure AD에 2 개의 웹 앱 등록
   - Azure AD 테 넌 트 관리 포털에 전역 관리자로 로그인 합니다.
     1. "앱 등록" 탭으로 이동 하 여 인쇄 끝점 추가
        - 응용 프로그램 추가를 선택 하 고 "새 응용 프로그램 등록"을 선택 합니다.
        - 적절 한 이름을 입력 하 고 "웹 앱/a p i"를 선택 합니다.
        - 로그온 URL = "<http://MicrosoftEnterpriseCloudPrint/CloudPrint>"
     2. 검색 끝점에 대해 반복
        - 로그온 URL = "<http://MopriaDiscoveryService/CloudPrint>"
     3. Native client 응용 프로그램에 대해 반복
        -   앱 이름을 제공 하는 경우 "네이티브 클라이언트 응용 프로그램"을 "응용 프로그램 유형"으로 선택 해야 합니다.
        -   리디렉션 URI = "https://\<\>/RedirectUrl"
     4. Native Client 앱 "설정"으로 이동
        -   이후 설치 단계에 사용할 "응용 프로그램 ID" 값을 복사 합니다.
        -   "필요한 권한"을 선택 합니다.
            1.  "추가"를 클릭 합니다.
            2.  "API 선택"을 클릭 합니다.
            3.  앱 끝점을 만들 때 정의한 이름으로 인쇄 끝점 및 검색 끝점을 검색 합니다.
            4.  끝점 2 개 추가
            5.  각 앱 끝점에 대 한 "위임 된 권한" 옵션이 설정 되어 있는지 확인 합니다.
            6.  맨 아래에 있는 "완료" 단추를 클릭 했는지 확인 합니다.
            7.  두 끝점을 모두 추가한 후에는 "권한 부여"를 클릭 합니다.  요청을 승인 하 라는 메시지가 표시 되 면 "예"를 선택 합니다.
        -   "리디렉션 URI"로 이동 하 여 목록에 다음 리디렉션 Uri를 추가 합니다.`ms-appx-web://Microsoft.AAD.BrokerPlugin/\<NativeClientAppID\>`
            `ms-appx-web://Microsoft.AAD.BrokerPlugin/S-1-15-2-3784861210-599250757-1266852909-3189164077-45880155-1246692841-283550366`

### <a name="step-3---install-azure-application-proxy-aap-with-passthrough-authentication"></a>3 단계-통과 인증을 사용 하 여 AAP (Azure 애플리케이션 프록시 설치)
1. AAD (Azure AD) 테 넌 트 관리 포털에 로그인 합니다.
    - AAD 메뉴 목록에서 "응용 프로그램 프록시"를 선택 합니다.
    - 화면 위쪽에서 "응용 프로그램 프록시 사용"을 클릭 합니다.
    - WAP (웹 응용 프로그램 프록시) 역할을 하는 도메인에 가입 된 Windows Server 컴퓨터에 "응용 프로그램 프록시 커넥터"를 다운로드 합니다.
2. WAP 컴퓨터에서 관리자로 로그인 하 고 "응용 프로그램 프록시 커넥터"를 설치 합니다.
    - 설치 하는 동안 응용 프로그램 프록시 커넥터에서 AAP를 사용 하도록 설정 하려는 Azure 개념에 자격 증명을 제공 합니다.
    - WAP 컴퓨터가 온-프레미스 Active Directory 도메인에 가입 되어 있는지 확인 합니다.
3. AAD 테 넌 트 관리 포털로 돌아가서 응용 프로그램 프록시를 추가 합니다.
   - **엔터프라이즈 응용 프로그램** 탭으로 이동 합니다.
   - **새 응용 프로그램** 을 클릭 합니다.
   - **온-프레미스 응용 프로그램** 을 선택 하 고 필드를 입력 합니다.
       - 이름: 원하는 모든 이름
       - 내부 URL: WAP 컴퓨터가 액세스할 수 있는 Momachine.config a 검색 클라우드 서비스에 대 한 내부 URL입니다.
       - 외부 URL: 조직에 맞게 구성
       - 사전 인증 방법: 통과

     >   참고: 위의 설정을 모두 찾지 못한 경우 사용 가능한 설정이 포함 된 프록시를 추가한 다음 방금 만든 응용 프로그램 프록시를 선택 하 고 **응용 프로그램 프록시** 탭으로 이동 하 여 위의 정보를 모두 추가 합니다.

4. 엔터프라이즈 클라우드 인쇄 서비스에 대해 위의 3 단계를 반복 하 고 엔터프라이즈 클라우드 인쇄 서비스에 대 한 내부 URL을 제공 합니다.

    >   참고: 아래에&lt;언급 된 https://서비스-&gt;컴퓨터-엔드포인트/mcs url은 mopria 클라우드 서비스 및/또는 엔터프라이즈 클라우드 인쇄 서비스에 대해 설정 하는 외부 url 이어야 합니다.


### <a name="step-4---configure-the-required-mdm-policies"></a>4 단계-필요한 MDM 정책 구성
- MDM 공급자에 로그인 합니다.
- 엔터프라이즈 클라우드 인쇄 정책 그룹을 찾고 아래 지침에 따라 정책을 구성 합니다.
  - Cloudprintoauthauthority = https://login.microsoftonline.com/\<Azure AD 디렉터리 ID\>
  - CloudPrintOAuthClientId = "응용 프로그램 ID"는 Azure AD 관리 포털에 등록 한 네이티브 웹 앱의 값입니다.
  - Cloud프린터 검색 끝점 = 3.3 단계에서 만든 검색 서비스 Azure 애플리케이션 프록시의 외부 URL (반드시 정확히 동일 하지만 뒤에는 포함 되지 않음)
  - MopriaDiscoveryResourceId = 2.8 단계에 등록 된 검색 끝점에 대 한 웹 앱/a p i의 "앱 ID URI"입니다.  앱의 설정 > 속성에서 찾을 수 있습니다.
  - CloudPrintResourceId = 2.8 단계에 등록 된 인쇄 끝점에 대 한 웹 앱/a p i의 "앱 ID URI"입니다. 앱의 설정 > 속성에서 찾을 수 있습니다.
  - Discoverymax프린터 limit = \<양의 정수\>

>   참고: Microsoft Intune 서비스를 사용 하는 경우 "클라우드 프린터" 범주에서 이러한 설정을 찾을 수 있습니다.

|Intune 표시 이름                     |정책                         |
|----------------------------------------|-------------------------------|
|프린터 검색 URL                   |Cloud프린터 검색 끝점  |
|프린터 액세스 기관 URL            |CloudPrintOAuthAuthority       |
|Azure native client 앱 GUID            |CloudPrintOAuthClientId        |
|인쇄 서비스 리소스 URI              |CloudPrintResourceId           |
|쿼리할 최대 프린터 수 (모바일 전용)  |Discoverymax프린터 제한       |
|프린터 검색 서비스 리소스 URI  |MopriaDiscoveryResourceId      |


>   참고: 클라우드 인쇄 정책 그룹을 사용할 수 없지만 MDM 공급자가 OMA-URI 설정을 지 원하는 경우 동일한 정책을 설정할 수 있습니다.  추가 정보는이 <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-enterprisecloudprint#enterprisecloudprint-cloudprintoauthauthority">문서</a> 를 참조 하세요.

- OMA-URI
    - `CloudPrintOAuthAuthority = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthAuthority`
        - 값 = `https://login.microsoftonline.com/` \<Azure AD 디렉터리 ID\>
    - `CloudPrintOAuthClientId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintOAuthClientId`
        - 값 = \<Azure AD 네이티브 앱의 응용 프로그램 ID\>
    - `CloudPrinterDiscoveryEndPoint = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrinterDiscoveryEndPoint`
        - Value = 3.3 단계에서 생성 된 검색 서비스 Azure 애플리케이션 프록시의 외부 URL (반드시 정확히 동일 하지만 후행/는 제외)
    - `MopriaDiscoveryResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/MopriaDiscoveryResourceId`
        - Value = 2.8 단계에 등록 된 검색 끝점에 대 한 웹 앱/a p i의 "앱 ID URI"입니다.  앱의 설정 > 속성에서 찾을 수 있습니다.
    - `CloudPrintResourceId = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/CloudPrintResourceId`
        - Value = 2.8 단계에 등록 된 인쇄 끝점에 대 한 웹 앱/a p i의 "앱 ID URI"입니다. 앱의 설정 > 속성에서 찾을 수 있습니다.
    - `DiscoveryMaxPrinterLimit = ./Vendor/MSFT/Policy/Config/EnterpriseCloudPrint/DiscoveryMaxPrinterLimit`
        - 값 = \<양의 정수\>
  
### <a name="step-5---publish-desired-shared-printers"></a>5 단계-원하는 공유 프린터 게시
1. 인쇄 서버에 원하는 프린터 설치
2. 프린터 속성 UI를 통해 프린터 공유
3. 액세스 권한을 부여 하려면 원하는 사용자 집합을 선택 하십시오.
4. 변경 내용을 저장 하 고 프린터 속성 창을 닫습니다.
5. Windows 10의 컴퓨터 작성자 업데이트 컴퓨터에서 관리자 권한 Windows PowerShell 명령 프롬프트를 엽니다.
   1. 다음 명령을 실행 합니다.
      - `find-module -Name "PublishCloudPrinter"`컴퓨터가 PowerShell 갤러리에 연결할 수 있는지 확인 하려면 (PSGallery)
      - `install-module -Name "PublishCloudPrinter"`

        >   참고: ' PSGallery '는 신뢰할 수 없는 리포지토리입니다. 라는 메시지가 표시 될 수 있습니다.  ' Y '를 입력 하 여 설치를 계속 합니다.

      - 게시-CloudPrinter
        - Printer = 정의 된 공유 프린터 이름
        - 제조업체 = 프린터 제조업체
        - 모델 = 프린터 모델
        - OrgLocation = 프린터 위치를 지정 하는 JSON 문자열입니다 (예:).`{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"Microsoft", "depth":1}, {"category":"site", "vs":"Redmond, WA", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}`
        - Sddl = 프린터에 대 한 권한을 나타내는 SDDL 문자열입니다. 프린터 속성 보안 탭을 적절 하 게 수정한 다음 명령 프롬프트에서 다음 명령을 실행 하 여이를 가져올 수 있습니다.`(Get-Printer PrinterName -full).PermissionSDDL`
            (. "G:DUD: (A; OICI; FA;;; WD) "

          > 참고: 값을 SDDL 설정으로 **`O:BA`** 설정 하기 전에 위의 명령 프롬프트 명령에서 결과에 접두사를 추가 해야 합니다.  예: SDDL =`O:BAG:DUD:(A;OICI;FA;;;WD)`

        - Discoveryendpoint = https://&lt;서비스-컴퓨터-끝점&gt;/mcs
        - Printserverendpoint = https://&lt;서비스-컴퓨터-엔드포인트&gt;/ecp
        - AzureClientId = 위에서 등록 된 네이티브 웹 앱 값의 응용 프로그램 ID
        - AzureTenantGuid = Azure AD 테 넌 트의 디렉터리 ID
        - DiscoveryResourceId = [선택 사항] 프록시 된 모바일 서비스의 응용 프로그램 ID 검색 클라우드 서비스

        > 참고: 모든 필수 매개 변수 값은 명령줄에도 입력할 수 있습니다.<br>
        **게시-CloudPrinter** PowerShell 명령 구문: <br>
        Publish-cloudprinter-프린터 \<문자열\> -제조업체 \<\> 문자열-모델 \<문자열\> -OrgLocation \<string\> -Sddl \<문자열 \<\> \<\> -discoveryendpoint \<문자열\> -printserverendpoint 문자열-azureclientid string-AzureTenantGuid\> \<string \<[-discoveryresourceid문자열\>]\> <br>
        샘플 명령:`publish-cloudprinter -Printer EcpPrintTest -Manufacturer Microsoft -Model FilePrinterEcp -OrgLocation '{"attrs": [{"category":"country", "vs":"USA", "depth":0}, {"category":"organization", "vs":"MyCompany", "depth":1}, {"category":"site", "vs":"MyCity, State", "depth":2}, {"category":"building", "vs":"Building 1", "depth":3}, {"category":"floor\_number", "vn":1, "depth":4}, {"category":"room\_name", "vs":"1111", "depth":5}]}' -Sddl "O:BAG:DUD:(A;OICI;FA;;;WD)" -DiscoveryEndpoint https://<services-machine-endpoint>/mcs -PrintServerEndpoint https://<services-machine-endpoint>/ecp -AzureClientId <Native Web App ID> -AzureTenantGuid <Azure AD Directory ID> -DiscoveryResourceId <Proxied Mopria Discovery Cloud Service App ID>`


## <a name="verifing-the-deployment"></a>배포 확인
MDM 정책이 구성 된 Azure AD 조인 장치에서 다음을 수행 합니다.
- 웹 브라우저를 열고 https://&lt;&gt;/mcs/services로 이동 합니다.
- 이 끝점의 기능 집합을 설명 하는 JSON 텍스트가 표시 되어야 합니다.
- "OS 설정-\> 장치-\> 프린터 & 스캐너"로 이동 합니다.
    - "클라우드 프린터 검색" 링크가 표시 됩니다.
    - 링크를 클릭 합니다.
    - "검색 위치를 선택 하세요." 링크를 클릭 합니다.
        - 장치 위치 계층이 표시 됩니다.
    - 위치를 선택 하 고 **확인** 을 클릭 한 다음 **검색** 단추를 클릭 하 여 프린터를 찾습니다.
    - 프린터를 선택 하 고 **장치 추가** 단추를 클릭 합니다.
    - 프린터를 성공적으로 설치한 후 즐겨 찾는 앱에서 프린터로 인쇄 합니다.

>   참고: "Ecpprinttest" 프린터를 사용 하는 경우 "C:\\ecpprinttest\\ecpprinttest .xps" 위치의 인쇄 서버 컴퓨터에서 출력 파일을 찾을 수 있습니다.