---
title: Windows Server Essentials에서 Office 365 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f8485e4-e10f-4f38-8a5e-d5227abd0d84
0author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b45bddb657b96c7cc5f9291a6c887b9d0801974b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860504"
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Windows Server Essentials에서 Office 365 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 서버에 Microsoft Office 365와 통합 하면 Windows Server Essentials 대시보드에서 온-프레미스 리소스와 함께 Office 365 서비스 및 온라인 계정을 관리할 수 있습니다. 이 항목에서는 초보 Office 365를 사용 하 여 서버를 통합 하 여 얻을 수 있는 이점를 수행 하는 방법 및 관리 하 고 Office 365 통합 문제를 해결 하는 방법을 확인 합니다.  
  
  
  
> [!IMPORTANT]
>   Office 365 통합은 단일 도메인 컨트롤러 환경 에서만 지원 됩니다. 또한 Office 365 통합 마법사는 도메인 컨트롤러에서 실행 해야 합니다.  
  
## <a name="in-this-topic"></a>이 항목의 내용  
  
-   [내 서버를 사용 하 여 Office 365를 통합 해야는 이유](#BKMK_IntegrationOverview)  
  
-   [Office 365 통합 설정](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Office 365 통합 관리](#BKMK_ManageIntegration)  
  
-   [Office 365 통합 문제 해결](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a> 내 서버를 사용 하 여 Office 365를 통합 해야는 이유  
 Windows Server Essentials 서버를 사용 하 여 Office 365를 통합 하는 좋은 이유는 여러 가지가 있습니다. 일부 리소스를 사내에서 관리 하지만 경우 Office 365를 사용 하 여 다른 서비스에 대 한 안내는 두 위치에서 작업 하는 대신 온-프레미스 리소스와 함께 대시보드에서 Office 365 서비스 및 리소스를 관리 하 수 있습니다.  
  
-   사용자 계정과 함께 Office 365에 대 한 사용자 액세스를 제공 하는 온라인 계정을 관리 합니다.  
  
    -   사용자에 대한 Microsoft Online Services 계정을 단일 단계로 만들거나 서버에서 기존 온라인 계정에 대한 사용자 계정을 만듭니다. 새로운 또는 기존 사용자 계정에 온라인 계정을 추가할 수도 있습니다.  
  
         대시보드에서 온라인 계정을 만들 때 사용자 로그인 Office 365에 서버에서 사용 하는 동일한 암호를 사용 합니다. 해당 사용자 계정의 암호를 변경하면 온라인 암호도 변경됩니다. 또한 온라인 계정 암호는 항상 사용자 계정에 대해 설정한 보안 요구 사항을 충족합니다.  
  
    -   사용자 계정의 수명 주기 내내 사용자 계정과 함께 온라인 계정을 관리합니다. 사용자 계정을 비활성화하면 온라인 계정도 비활성화됩니다. 사용자 계정을 제거하면 온라인 계정도 제거됩니다.  
  
    -   Windows Server Essentials 서버에서 전자 메일에 대 한 Exchange Online 메일 그룹도 관리 합니다.  
  
-   보내고 Office 365 구독에 사용자 지정 인터넷 도메인을 연결 하 여 조직의 인터넷 도메인 (예: contoso.com)에서 전자 메일을 받습니다.  
  
-   대시보드에서 구독 및 Office 365 통합을 관리 합니다.  
  
-   SharePoint Online 라이브러리를 포함 하는 구독의 경우 Windows Server Essentials 서버를 사용 하 여 Office 365 통합 수 있습니다.  
  
    -   대시보드에서 SharePoint Online 라이브러리를 만들고 설정 합니다.  
  
        > [!NOTE]
        >  초보 수도 My Server 2012 R2 앱을 사용 하 여 랩톱, 모바일 장치 또는 Windows phone에서 SharePoint Online 라이브러리의 문서를 사용 하 여 작동 합니다. 이 기능은 Windows Server Essentials에 사용할 수만 있습니다. 자세한 내용은 [Use the My Server App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)합니다.  
  
    -   대시보드에서 SharePoint Online 팀 사이트에 대 한 권한을 변경 하거나 다른 변경 하려면 대시보드에서 팀 사이트를 엽니다.  
  
     자세한 내용은 [SharePoint Online 관리](Manage-SharePoint-Online-in-Windows-Server-Essentials.md)합니다.  
  
-   Exchange Online을 구독할 경우 Windows Server Essentials 서버를 사용 하 여 Office 365 통합을 사용 사용자가 회사 전자 메일 서버에 연결 하는 데 사용할 수 있는 모바일 장치를 관리할 수 있습니다.  
  
    -   모바일 장치가 회사 메일 서버에 연결될 때 암호 보호가 필요합니다. 최소 암호 길이, 허용할 실패한 로그인 시도 수, 로그인 시도 사이에 필요한 최소 시간을 설정합니다.  
  
    -   장치 모델의 보안 문제에 대해 알고 있으면 모바일 장치에서 Exchange Online에 연결하지 못하도록 합니다.  
  
    -   모바일 장치를 분실하거나 도난당하면 다음에 장치가 켜져 있을 때 장치를 지워서 모든 중요한 회사 데이터를 삭제합니다.  
  
-    Office 365 통합에는 Office 365 서비스 및 리소스에 연결 하는 새로운 방법을 제공 합니다.  
  
    -   Windows Server Essentials 실행 패드에서 Office 365 서비스를 엽니다. 정보를 참조 하세요 [Quick Start Guide to Using Microsoft Office 365](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)합니다.  
  
    -   랩톱, 모바일 장치 또는 Windows phone에서 SharePoint Online 라이브러리의 문서 작업에 My Server 2012 R2 앱을 사용 합니다. 정보를 참조 하세요 [Use the My Server App](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)합니다. 이 기능은 Windows Server Essentials에서 사용할 수만 있습니다.  
  
##  <a name="BKMK_Configure"></a> Office 365 통합 설정  
 서버 설치를 완료 한 후 언제 든 지 Office 365를 사용 하 여 서버를 통합할 수 있습니다. 인할 이미 Office 365 구독이 있는 경우 하나를 구매 하거나 무료 평가판 구독에 등록할 수 있습니다.  
  
 다음 작업을 수행합니다.  
  
-   [1단계: Office 365 통합 요구 사항 확인](#BKMK_StepOne_VERIFY)  
  
-   [2단계: Microsoft Office 365와 서버 통합](#BKMK_StepTwo)  
  
-   [3 단계: S 조직의 인터넷 도메인 이름 (선택 사항) Office 365에 연결](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a> 1 단계: Office 365 통합 요구 사항 확인  
 시작하기 전에 서버가 이러한 요구 사항을 충족해야 합니다.  
  
-   서버에는 다음 운영 체제가 설치되어 있을 수 있습니다.  Windows Server Essentials, Windows Server Essentials 또는 Windows Server Essentials Experience 역할이 설치 된 Windows Server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter 운영 체제입니다.  
  
-   환경에 하나 이상의 도메인 컨트롤러가 하나만 사용할 수 있습니다 하 고 도메인 컨트롤러에서 Office 365 통합을 수행 해야 합니다.  
  
-   서버에서 인터넷에 연결할 수 있어야 합니다.  
  
-   Office 365 통합을 시작 하기 전에 서버에서 모든 중대 및 중요 업데이트를 설치 해야 합니다.  
  
-   조직의 인터넷 도메인과 SharePoint Online 리소스를 사용 하 여 전자 메일 주소에 사용 하려는 경우 안내를 통합 하는 동안 Office 365에 도메인을 연결할 수 있도록 도메인 이름을 등록 해야 합니다. 자세한 내용은 [도메인 이름 구매 방법](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)을 참조하세요.  
  
> [!NOTE]
>  Office 365를 미리 구독할 t 필요를 하지 있습니다. 초보 구독을 구입 하거나 Office 365 통합 중에 무료 평가판에 등록 하는 일을 할 수 있습니다. D 하려는 경우 계획 및 Office 365에 대 한 가격 책정을 살펴보세요 [기업 위한 Office 365 계획 비교](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text)합니다.  
  
###  <a name="BKMK_StepTwo"></a> 2 단계: Microsoft Office 365와 서버 통합  
 Office 365를 사용 하 여 Windows Server Essentials 서버를 통합 하는 도메인 컨트롤러에서 다음 절차를 수행 합니다.  
  
> [!NOTE]
>  프로시저 s 동일한 Windows Server Essentials 또는 Windows Server Essentials를 안내 하지만 홈 페이지의 다른 위치에서 시작 있는지 여부입니다. Windows Server Essentials에서 Office 365 및 기타 Microsoft Online Services 사용 하 여 서버 통합을 **Services** 탭 합니다. Windows Server Essentials에서 Office 365 통합을 수행 합니다 **전자 메일** 탭 합니다.  
  
##### <a name="to-integrate-the-server-with-office-365"></a>서버를 Office 365와 통합하려면  
  
1.  관리자로 서버에 로그인 하 고 Windows Server Essentials 대시보드를 엽니다.  
  
2.  에 **홈** 페이지에서 **Services** (Windows Server Essentials에서 클릭 **전자 메일**), 클릭 **Microsoft Office 365와 통합**, 클릭 하 고 **Microsoft Office 365 통합 설정**합니다.  
  
     Microsoft Office 365와 통합 마법사가 표시됩니다.  
  
3.  **시작** 페이지에서 다음 작업의 하나를 수행합니다.  
  
    -   Don t Office 365 구독이 있는 경우 클릭 **다음**, 평가판 구독에 Office 365 또는 기호를 구독에 대 한 지침을 따릅니다.  
  
         안내 하 고 마법사로 돌아갑니다 전에 Office 365에 로그인 해야 합니다. 작업을 수행 해야 하는 t 하지 않지만 합니다 **여기서 시작** Office 365 포털의 섹션입니다.  
  
    -   선택 된 서버와 통합 하려는 Office 365를 구독에 이미 있는 경우 **Office 365에 대 한 구독을 이미가지고**를 클릭 하 고 **다음**합니다.  
  
4.  지시에 따라 마법사를 완료합니다.  
  
 마법사를 성공적으로 완료 되 면 초보 대시보드에 다음 변경 내용을 확인 합니다.  
  
-   여기서 s는 새 **Office 365** 통합 및 Office 365 구독 관리에 사용 되는 페이지입니다.  
  
-   에 **사용자** 페이지에서 모든 참조는 **온라인 계정을** 만들고 Office 365에 사용자 액세스를 부여 하는 Microsoft Online Services 계정을 관리할 수 있는 탭입니다. 온라인 교환 다시 사용 하는 경우 Windows Server Essentials 서버에 있고 안내도 참조 하세요.를 **배포 그룹** 탭 합니다.  
  
-   **저장소** Windows Server Essentials 서버에 대 한 페이지에는 **SharePoint 라이브러리** SharePoint Online 라이브러리를 관리 및 팀 사이트에 대 한 권한을 변경에 대 한 탭 합니다. 모든 비즈니스 계획에 Office 365 용 SharePoint Online이 기본 기능을 포함합니다.  
  
###  <a name="BKMK_StepThree"></a> 3 단계: S 조직의 인터넷 도메인 이름 (선택 사항) Office 365에 연결  
 조직 및 SharePoint Online 리소스에 대 한 Url로 주소가 지정 된 전자 메일에서 자체 인터넷 도메인을 사용 하려는 경우에 Office 365 구독에 사용자 지정 도메인을 연결할 수 있습니다. Office 365를 사용 하 여 Windows Server Essentials 서버를 통합 하면 대시보드에서이 수행할 수 있습니다.  
  
 이 온라인 만들기 전에이 작업을 수행 하는 가장 쉬운 s 대량-온라인 계정을 만들 때 도메인을 사용할 수 있도록 사용자에 대 한 계정입니다.  
  
 Office 365에 등록할 때 도메인 이름을 얻으려면? 예를 들어 *contoso*. onmicrosoft.com입니다. D 대신 사용 하는 경우 다른 도메인 이름을? 예를 들어 contoso.com 단순히? 할 수 있습니다. 초보는 도메인 이름 구입 인할 경우 이미 하나 및 일부 DNS 레코드를 변경 해야 합니다.  
  
 Office 365를 사용 하 여 사용 하도록 사용자 지정 도메인 설정 4 개 작업이 포함 됩니다.  
  
1.  **도메인 이름을 구매합니다.** 즉, 도메인 등록 기관 또는 DNS 호스팅 공급자에 등록합니다.  
  
    -   Office 365를 사용 하 여 작동 하는 도메인 이름을 선택 합니다. 두 번째 수준 도메인 이름을 사용할 수 있습니다? 예를 들어 buycontoso.com? 번째 수준 도메인 이름이 아닌? 예를 들어 marketing.contoso.com 합니다. Office 365에서 사용할 도메인을 선택 하는 방법에 대 한 자세한 내용은 참조 하세요. [도메인](https://technet.microsoft.com/library/office-365-domains.aspx)합니다.  
  
    -   Office 365에 필요한 도메인 이름 서버 (DNS) 레코드를 허용 하는 도메인 등록 기관에서 구매 합니다. 필요한 DNS 레코드를 허용하는 도메인 등록 기관을 확인하려면 [도메인 이름 구매 방법](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)을 참조하세요. 다른 등록 기관에 도메인을 이미 등록 한 경우 하지 걱정; Office 365에 도메인을 연결 하면 다른 등록 기관에 도메인을 전송할 수 있습니다.  
  
2.  **Office 365 서비스에서 도메인 이름을 사용하도록 허용하는 DNS 레코드를 구성합니다.** 가장 쉬운 방법은 3 단계에서 Office 365 구독에 도메인을 연결 하면 DNS 레코드를 구성 마법사를 통해 하는 것입니다. D 대신 이렇게 하면 해당 사용자가 직접 참조 [Office 365 통합에 대 한 레코드를 수동으로 DNS를 구성 하는 방법](#BKMK_ManuallyConfigureDNS)합니다.  
  
3.  **Office 365 구독에 사용자 지정 인터넷 도메인을 연결 합니다.** Ll 사용 하 여 **Office 365에 도메인 연결** 작업 합니다.  
  
4.  **Office 365 서비스에 새 도메인 이름을 사용 하는 것을 확인 합니다.**  
  
 사용 하기 전에 1 및 2 단계를 완료 하는 경우는 **Office 365에 도메인 연결** 태스크인 마법사는 Office 365에 도메인 이름을 연결할 수 있습니다. 또는 마법사를 사용하여 1 및 2단계를 일부 또는 모두 수행할 수 있습니다.  
  
##### <a name="to-link-your-organization-s-internet-domain-to-office-365"></a>Office 365에 조직의의 인터넷 도메인을 연결 하려면  
  
1.  대시보드에서 **Office 365** 페이지를 열고 **Office 365에 도메인 연결**을 클릭합니다.  
  
2.  지시에 따라 마법사를 완료합니다.  
  
     마법사 도움이 등록, 구성 및 Office 365에서 사용 하려면 새 또는 기존 인터넷 도메인 이름을 연결 하는 단계 중 일부나 전부를 사용 하 여 됩니다.  
  
     마법사 페이지에서 도움말 링크를 클릭하여 작업을 완료하는 데 필요한 정보를 확인합니다. 설정의 도메인 이름 섹션을 참조 하거나 [Windows Server Essentials에서 원격 웹 액세스 관리](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx) 프로세스 개요 및 요구 사항에 대 한 합니다.  
  
    > [!NOTE]
    >  마법사를 사용하여 새 도메인 이름을 등록하려면 마법사와의 원활한 통합을 제공하려고 Microsoft와 파트너 관계를 맺은 도메인 이름 서비스 공급자의 하나를 사용해야 합니다. 도메인 이름 등록 기관을 찾으려면 [도메인 이름 구매 방법](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)을 참조하세요.  
  
3.  발견 되지 않으면 사용자 도메인 이름 서버에서 관리 되는, 경우에 초보 구성을 완료 하려면 필요한 DNS 레코드를 수동으로 구성 해야 합니다. 자세한 지침은 이 항목의 후반부에서 [Office 365 통합에 대한 DNS 레코드를 수동으로 구성하는 방법](#BKMK_ManuallyConfigureDNS)을 참조하세요.  
  
4.  Office 365에서 도메인 사용 되 고 있는지 확인 합니다.  
  
     여기서 s 도메인 이름 등록 기관이 DNS 레코드를 확인 하는 동안 마법사를 완료 한 후 거의 대기 합니다. 자동으로 이런 don t 아무 작업도 수행 해야 합니다. 일반적으로 약 1 시간 소요 되지만? 및 경우에 따라 약간 더 오래입니다. 도메인 확인이 완료 되는 **Office 365** 페이지의 조직의 도메인이 나열 됩니다.  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a> Office 365 통합에 대 한 DNS 레코드를 수동으로 구성 하는 방법  
 Office 365에 도메인 연결 마법사에서 도메인 이름이 서버에서 관리되지 않음을 감지할 경우 구성을 완료하려면 필요한 DNS(도메인 이름 서버) 레코드를 수동으로 구성해야 합니다. 이런 경우 초보 찾을 구성 해야 하는 DNS 레코드 목록을 **%username%\NewDNSRecords_ (n).txt**, 여기서 *(n)* 은 임의 숫자입니다.  
  
 다음 표에서는 추가해야 하는 DNS 레코드에 대해 설명합니다. 입력 방법은 도메인 이름 등록 기관에 따라 달라질 수 있습니다. 의문 사항이 있으면 도메인 이름 등록 기관에 도움을 요청하세요.  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>Office 365에 인터넷 도메인 이름을 연결하는 데 필요한 DNS 레코드  
  
|서비스|필요한 DNS 레코드|용도|  
|-------------|--------------------------|-------------|  
|(여러 서비스)|MX| Office 365이이 레코드를 사용 하 여 특정 도메인 이름일 소유 하 고 있는지 확인 합니다. 이 MX 레코드는 메일 메시지 라우팅을 충돌하지 않습니다.|  
|Exchange Online|MX|메일 메시지 라우팅을 제공합니다. **중요:**  전자 메일을 마이그레이션할 경우 새 MX 레코드에 기본 설정을 영(**0**)으로 할당하지 마세요. 레코드 값이 현재 MX 레코드에 할당된 값보다 큰지 확인합니다. 전자 메일 마이그레이션이 완료 되 고 Office 365 전자 메일 서버를 변경할 준비가 경우 도메인 이름 등록자에서 새 MX 레코드의 기본 설정 값을 다시 설정 합니다.|  
|Exchange Online|별칭(CNAME)|사용자가 Exchange Online과 Outlook 데스크톱 클라이언트 또는 모바일 전자 메일 클라이언트 사이의 연결을 손쉽게 설정하도록 도와주는 데 사용되는 자동 검색 레코드입니다. **참고:**  조직 s 자신만 도메인 이름을 사용 하 여 Outlook Web Access에 액세스 하려는 경우 (예를 들어 http://mail.contoso.com) 표준 URL 대신 (https://outlook.com/owa/office365.com), 별칭 (CName) 레코드를 다음과 같이 구성할 수 있습니다. **Type=CNAME, TTL=01:00:00, HostName=mail, Address=mail.office365.com**|  
|Exchange Online|TXT|Office 365 전자 메일 서버를 사용 하는 도메인 outlook.com에 사용자 도메인 대신 전자 메일을 보낼 권한이 지정 합니다. 이 레코드를 만들어 아웃바운드 메일에 스팸으로 플래그가 지정되지 않도록 합니다.|  
|Lync Online|SRV|Windows Live 또는 Yahoo!와 같은 기타 인스턴트 메시징 서비스와의 페더레이션을 사용하도록 도와줍니다.|  
|Lync Online|SRV|사용자가 Lync 데스크톱 클라이언트와 Microsoft Lync Online 사이의 연결을 손쉽게 설정하도록 도와주는 데 사용되는 자동 검색 레코드입니다.|  
  
> [!IMPORTANT]
>  도메인 확인이 완료 된 후, 추가 하거나 Office 365 포털에서 DNS 레코드를 추가로 변경 하지 마세요.  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a> 다음 단계  
  
-   사용자에 대한 Microsoft Online Services 계정을 만듭니다.  
  
     Office 365 서비스를 사용 하려면 사용자에 게 네트워크 사용자 계정과 연관 된 Microsoft Online Services 계정이 있어야 합니다. 대시보드에서 쉽게 만들 수 있습니다. 하는 경우 새 Office 365 구독을 사용 하 여 다시를 대량으로 만들 수 있습니다 온라인 계정을 기존 사용자 계정에 대 한 합니다. 경우는 이미 사용 하 여 다시 사용자 계정을 가져올 수 있습니다 사용자 기존 온라인에서 Office 365 구독과 새 서버를 통합 된 계정입니다. 절차를 참조 하세요 [사용자에 대 한 온라인 계정 관리](Manage-Online-Accounts-for-Users.md)합니다.  
  
> [!NOTE]
>  In Windows Server Essentials 대시보드에서 Microsoft Online Services 계정을 Office 365 계정 이라고 합니다. 계정은 동일하고 용어만 변경됩니다.  
  
##  <a name="BKMK_ManageIntegration"></a> Office 365 통합 관리  
 Office 365를 사용 하 여 서버를 통합 하면 합니다 **Office 365** 대시보드에서 페이지는 Office 365 구독에 대 한 정보를 표시 하 고 이러한 작업을 사용할 수 있도록 합니다.  
  
-   [Office 365 구독 관리](#BKMK_ManageO365) ? 구독을 관리 하는 데는 관리자 계정을 변경 합니다. Office 365 관리 대시보드에서 구독 관리를 엽니다.  
  
-   [Office 365에 조직의의 인터넷 도메인 연결](#BKMK_StepThree) ? 사용자가 도메인으로 주소가 지정 된 전자 메일을 주고받을 수 하려는 경우 Office 365에 도메인을 연결할 수 있습니다. (앞에서 설명한 [3 단계: Office 365에 조직의의 도메인 연결](#BKMK_StepThree).)  
  
-   [Office 365 통합 사용 안 함](#BKMK_Disable) ? T don을 대시보드에서 Office 365 서비스, 구독 및 온라인 계정을 관리 하려면 Office 365 통합을 비활성화할 수 있습니다. 서비스를 Office 365 포털에서 사용할 수 있습니다.  
  
###  <a name="BKMK_ManageO365"></a> Office 365 구독 관리  
 구독에서 Office 365에서 열면 다시 서버에서 작업 하는 동안 Office 365 구독을 변경 해야 할 경우는 **Office 365** 대시보드의 페이지입니다. 또한 Office 365 서비스를 변경 하는 서버 관리자 계정을 변경할 수 있습니다.  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>Office 365 관리 대시보드에서 구독을 열려면  
  
1.  Windows Server Essentials 대시보드를 엽니다는 **Office 365** 페이지입니다.  
  
2.  **구성 작업**에서 **Office 365 관리**를 클릭합니다.  
  
3.  구독을 관리 하는 데 사용할 수 있는 Microsoft 온라인 계정으로 Office 365에 로그인 합니다.  
  
     Office 365 관리 대시보드가 열립니다.  
  
##### <a name="to-change-the-office-365-administrator-account"></a>Office 365 관리자 계정을 변경하려면  
  
1.  대시보드에서 **Office 365**를 클릭합니다.  
  
2.  **구성 작업**에서 **Office 365 관리자 계정 변경**을 클릭합니다. 관리자 계정 변경 마법사가 나타납니다. (Windows Server essentials에서는 마법사 이름이 Office 365 관리자 계정 설정 합니다.)  
  
3.  사용 하 여 Office 365 구독에 연결 하 고 클릭 하려는 계정의 자격 증명 입력 **다음**합니다.  
  
4.  **닫기**를 클릭합니다. 대시보드가 다시 시작됩니다.  
  
###  <a name="BKMK_Disable"></a> Office 365 통합 사용 안 함  
 T 하지는 않으려는 경우 대시보드에서 Office 365 서비스 및 온라인 계정을 관리 하려면, Office 365 통합 기능을 해제할 수 있습니다. Office 365 구독을 활성 상태로 유지 되 고 대시보드에서 변경한 모든 구성 변경 내용을 적용 합니다. 예를 들어, 초보 메일이 Office 365 구독에 연결 된 도메인 이름으로 배달 합니다. 성공 하면 t 손실 모든 전자 메일 및 모바일 장치에 설정 하는 컨트롤은 여전히 Exchange Online을 사용 합니다.  
  
 앞으로 Office 365 구독, 서비스 및 Office 365에서 리소스 관리는 및 사용자가 Office 365에서 온라인 계정에 대 한 암호를 관리 해야 합니다. 암호 동기화가 더 이상 발생 하 고 사용 하지 않도록 설정 또는 사용자 계정을 제거 하는 사용자가 온라인 계정에 영향을 주지 않습니다.  
  
 Office 365 통합 소프트웨어는 로컬 서버에 설치 되어 통합 서비스를 Office 365에 연결 될 수 없더라도 기능을 비활성화할 수 있습니다.  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>서버와의 Office 365 통합을 사용하지 않도록 설정하려면  
  
1.  대시보드에서 **Office 365**를 클릭합니다.  
  
2.  **Office 365 통합 사용 안 함**을 클릭합니다. Office 365 사용 안 함 마법사가 나타납니다.  
  
3.  지시에 따라 마법사를 완료합니다.  
  
> [!NOTE]
>  Office 365 통합을 다시 활성화 하려면 사용 합니다 **Office 365와 통합** 작업을 **서비스** s 대시보드 탭 **홈** 페이지. 자세한 내용은 [2 단계: Microsoft Office 365와 Windows Server Essentials 서버 통합](#BKMK_StepTwo)이 항목의 앞부분에 나오는.  
  
##  <a name="BKMK_Troubleshoot"></a> Office 365 통합 문제 해결  
 이 섹션에서는 Windows Server Essentials에서 Office 365 통합 기능을 사용 하는 경우 발생할 수 있는 일반적인 문제를 해결 하는 데 유용한 정보를 제공 합니다.  
  
###  <a name="BKMK_AcctsNotCreated"></a> 일부 Microsoft Online Services 계정이 만들어지지 않습니다.  
 **설명**  
  
 하나 이상의 Microsoft Online Services 계정을 대시보드 않았습니다 t에서 만들기 성공 하려고 했습니다.  
  
 **해결 방법**  
  
1.  마법사 완료 페이지에서 링크를 클릭하여 제대로 완료되지 않은 각 계정 만들기 요청에 대한 세부 정보가 포함된 결과 파일을 엽니다. 예를 들어 결과에는 요청된 계정의 이름을 가진 Microsoft Online Services 계정이 이미 있음을 알리는 정보가 표시될 수 있습니다.  
  
2.  권장 작업을 수행하여 각 오류를 해결합니다.  
  
3.  이 문제가 지속되면 서버를 다시 시작하고 온라인 계정을 다시 만들어 보세요.  
  
###  <a name="BKMK_ProblemUninstalling"></a> Office 365 통합을 제거 하는 문제가 발생 했습니다.  
 **설명**  
  
 Office 365 통합을 사용 하지 않도록 설정 하려고 했습니다. 알 수 없는 오류가 발생 했습니다.  
  
 **해결 방법**  
  
1.  컴퓨터가 인터넷에 연결되어 있는지 확인하고 다시 시도합니다.  
  
2.  오류가 다시 발생하면 서버를 다시 시작하고 다시 시도합니다.  
  
## <a name="see-also"></a>참조  
  
-   [Windows Server Essentials-1 부에 대 한 서비스 통합 개요](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials-2 부에 대 한 서비스 통합 개요](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Microsoft Office 365를 사용 하 여 빠른 시작 가이드](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)
