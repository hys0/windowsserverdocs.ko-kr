---
title: Windows Server Essentials에서 Office 365 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.topic: article
ms.assetid: 3f8485e4-e10f-4f38-8a5e-d5227abd0d84
author: nnamuhcs
ms.author: daveba
ms.openlocfilehash: bd7787b853395bf461165802251de8b2be5d5a39
ms.sourcegitcommit: 2082335e1260826fcbc3dccc208870d2d9be9306
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2019
ms.locfileid: "69980263"
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Windows Server Essentials에서 Office 365 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 서버를 Microsoft Office 365와 통합 하는 경우 Windows Server Essentials 대시보드에서 온-프레미스 리소스와 함께 Office 365 서비스 및 온라인 계정을 관리할 수 있습니다. 이 항목에서는 Office 365와 서버를 통합 하 여 얻을 수 있는 기능,이를 수행 하는 방법 및 Office 365 통합을 관리 하 고 문제를 해결 하는 방법에 대해 알아봅니다.  
  
  
  
> [!IMPORTANT]
>   Office 365 통합은 단일 도메인 컨트롤러 환경 에서만 지원 됩니다. 또한 Office 365 통합 마법사는 도메인 컨트롤러에서 실행 해야 합니다.  
  
## <a name="in-this-topic"></a>항목 내용  
  
-   [Office 365를 서버와 통합 해야 하는 이유는 무엇 인가요?](#BKMK_IntegrationOverview)  
  
-   [Office 365 통합 설정](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Office 365 통합 관리](#BKMK_ManageIntegration)  
  
-   [Office 365 통합 문제 해결](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a>Office 365를 서버와 통합 해야 하는 이유는 무엇 인가요?  
 Office 365을 Windows Server Essentials 서버와 통합 하는 데는 여러 가지 좋은 이유가 있습니다. 일부 리소스를 사내에서 관리 하지만 다른 서비스에 Office 365를 사용 하는 경우 두 위치에서 작업 하는 대신 온-프레미스 리소스와 함께 대시보드에서 Office 365 서비스 및 리소스를 관리할 수 있습니다.  
  
- 사용자에 게 Office 365에 대 한 액세스 권한을 제공 하는 온라인 계정을 사용자 계정과 함께 관리 합니다.  
  
  -   사용자에 대한 Microsoft Online Services 계정을 단일 단계로 만들거나 서버에서 기존 온라인 계정에 대한 사용자 계정을 만듭니다. 새로운 또는 기존 사용자 계정에 온라인 계정을 추가할 수도 있습니다.  
  
       대시보드에서 온라인 계정을 만들 때 사용자는 서버에서 사용 하는 것과 동일한 암호를 사용 하 여 Office 365에 로그인 합니다. 해당 사용자 계정의 암호를 변경하면 온라인 암호도 변경됩니다. 또한 온라인 계정 암호는 항상 사용자 계정에 대해 설정한 보안 요구 사항을 충족합니다.  
  
  -   사용자 계정의 수명 주기 내내 사용자 계정과 함께 온라인 계정을 관리합니다. 사용자 계정을 비활성화하면 온라인 계정도 비활성화됩니다. 사용자 계정을 제거하면 온라인 계정도 제거됩니다.  
  
  -   Windows Server Essentials 서버에서 전자 메일에 대 한 Exchange Online 메일 그룹도 관리 합니다.  
  
- 사용자 지정 인터넷 도메인을 Office 365 구독에 연결 하 여 조직의 인터넷 도메인 (예: contoso.com)에서 전자 메일을 보내고 받습니다.  
  
- 대시보드에서 구독 및 Office 365 통합을 관리 합니다.  
  
- 구독이 SharePoint Online 라이브러리를 포함 하는 경우 Office 365을 Windows Server Essentials 서버와 통합 하면 다음을 수행할 수 있습니다.  
  
  - 대시보드에서 SharePoint Online 라이브러리를 만들고 관리 합니다.  
  
    > [!NOTE]
    >  또한 My Server 2012 R2 앱을 사용 하 여 노트북, 모바일 장치 또는 Windows phone에서 SharePoint Online 라이브러리의 문서로 작업할 수 있습니다. 이 기능은 Windows Server Essentials에만 사용할 수 있습니다. 자세한 내용은 [My Server 앱 사용](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)을 참조 하세요.  
  
  - 대시보드에서 SharePoint Online 팀 사이트에 대 한 사용 권한을 변경 하거나 대시보드에서 팀 사이트를 열어 다른 변경 작업을 수행 합니다.  
  
    자세한 내용은 [SharePoint Online 관리](Manage-SharePoint-Online-in-Windows-Server-Essentials.md)를 참조 하세요.  
  
- Exchange Online을 구독 하는 경우 Office 365을 Windows Server Essentials 서버와 통합 하면 사용자가 회사 메일 서버에 연결 하는 데 사용 하는 모바일 장치를 관리할 수 있습니다.  
  
  -   모바일 장치가 회사 메일 서버에 연결될 때 암호 보호가 필요합니다. 최소 암호 길이, 허용할 실패한 로그인 시도 수, 로그인 시도 사이에 필요한 최소 시간을 설정합니다.  
  
  -   장치 모델의 보안 문제에 대해 알고 있으면 모바일 장치에서 Exchange Online에 연결하지 못하도록 합니다.  
  
  -   모바일 장치를 분실하거나 도난당하면 다음에 장치가 켜져 있을 때 장치를 지워서 모든 중요한 회사 데이터를 삭제합니다.  
  
- Office 365 통합은 Office 365 서비스 및 리소스에 연결 하는 새로운 방법을 제공 합니다.  
  
  -   Windows Server Essentials 실행 패드에서 Office 365 서비스를 엽니다. 자세한 내용은 [빠른 시작 가이드 Microsoft Office 365를 사용 하는 방법을](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)참조 하세요.  
  
  -   My Server 2012 R2 앱을 사용 하 여 노트북, 모바일 장치 또는 Windows phone에서 SharePoint Online 라이브러리의 문서를 사용할 수 있습니다. 자세한 내용은 [My Server 앱 사용](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)을 참조 하세요. 이 기능은 Windows Server Essentials 에서만 사용할 수 있습니다.  
  
##  <a name="BKMK_Configure"></a>Office 365 통합 설정  
 서버 설치를 완료 한 후 언제 든 지 서버를 Office 365와 통합할 수 있습니다. 아직 Office 365 구독이 없는 경우 구매 하거나 무료 평가판 구독에 등록할 수 있습니다.  
  
 다음 작업을 수행합니다.  
  
-   [1단계: Office 365 통합 요구 사항 확인](#BKMK_StepOne_VERIFY)  
  
-   [2단계: 서버를 Microsoft Office 365와 통합](#BKMK_StepTwo)  
  
-   [3단계: Office 365에 조직의 인터넷 도메인 이름 연결 (선택 사항)](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a> 1단계: Office 365 통합 요구 사항 확인  
 시작하기 전에 서버가 이러한 요구 사항을 충족해야 합니다.  
  
-   서버에는 다음 운영 체제가 설치되어 있을 수 있습니다.  Windows server essentials, Windows Server Essentials 또는 windows server Essentials Experience 역할이 설치 된 windows server 2012 R2 Standard 또는 Windows Server 2012 R2 Datacenter 운영 체제  
  
-   환경에는 도메인 컨트롤러가 하나만 있을 수 있으며 도메인 컨트롤러에서 Office 365 통합을 수행 해야 합니다.  
  
-   서버에서 인터넷에 연결할 수 있어야 합니다.  
  
-   Office 365 통합을 시작 하기 전에 서버에 중요 업데이트와 중요 한 업데이트를 모두 설치 해야 합니다.  
  
-   조직의 인터넷 도메인을 메일 주소에서 사용 하 고 SharePoint Online 리소스와 함께 사용 하려면 통합 하는 동안 도메인을 Office 365에 연결할 수 있도록 도메인 이름을 등록 해야 합니다. 자세한 내용은 [도메인 이름 구매 방법](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)을 참조하세요.  
  
> [!NOTE]
>  Office 365을 미리 구독할 필요가 없습니다. Office 365 통합 중에 구독을 구매 하거나 무료 평가판에 등록할 수 있습니다. Office 365에 대 한 계획 및 가격 책정을 보려면 [비즈니스에 대 한 office 365 요금제를 비교](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text)하세요.  
  
###  <a name="BKMK_StepTwo"></a> 2단계: 서버를 Microsoft Office 365와 통합  
 도메인 컨트롤러에서 다음 절차를 수행 하 여 Windows Server Essentials 서버를 Office 365와 통합 합니다.  
  
> [!NOTE]
>  Windows Server Essentials 나 Windows Server Essentials가 있는지에 관계 없이 절차는 동일 하지만 홈 페이지의 다른 곳에서 시작 합니다. Windows Server Essentials에서 **서비스** 탭의 Office 365 및 기타 Microsoft Online Services와 서버를 통합 합니다. Windows Server Essentials에서 Office 365 통합은 **전자 메일** 탭에서 수행 됩니다.  
  
##### <a name="to-integrate-the-server-with-office-365"></a>서버를 Office 365와 통합하려면  
  
1. 관리자 권한으로 서버에 로그인 하 고 Windows Server Essentials 대시보드를 엽니다.  
  
2. **홈** 페이지에서 **서비스** (Windows Server Essentials에서 **전자 메일**클릭)를 클릭 하 고 **Microsoft Office 365 통합**을 클릭 한 다음 **Microsoft Office 365 통합 설정**을 클릭 합니다.  
  
    Microsoft Office 365와 통합 마법사가 표시됩니다.  
  
3. **시작** 페이지에서 다음 작업의 하나를 수행합니다.  
  
   -   Office 365에 대 한 구독이 없는 경우 **다음**을 클릭 하 고 지침에 따라 office 365를 구독 하거나 평가판 구독에 등록 합니다.  
  
        마법사로 돌아가려면 먼저 Office 365에 로그인 해야 합니다. 하지만 Office 365 포털의 **여기서 시작** 섹션에서 작업을 수행할 필요가 없습니다.  
  
   -   서버와 통합 하려는 Office 365에 대 한 구독이 이미 있는 경우 **office 365에 대 한 구독이 이미**있음을 선택 하 고 **다음**을 클릭 합니다.  
  
4. 지시에 따라 마법사를 완료합니다.  
  
   마법사가 성공적으로 완료 되 면 대시보드에 다음과 같이 변경 된 것을 알 수 있습니다.  
  
-   통합 및 Office 365 구독을 관리 하는 데 사용 되는 새로운 **office 365** 페이지가 있습니다.  
  
-   사용자 페이지 에서 사용자에 게 Office 365에 대 한 액세스 권한을 부여 하는 Microsoft online Services 계정을 만들고 관리할 수 있는 **온라인 계정** 탭이 표시 됩니다. Exchange Online을 사용 하는 경우 Windows Server Essentials 서버가 있으면 **메일 그룹** 탭도 표시 됩니다.  
  
-   Windows Server Essentials 서버의 **저장소** 페이지에는 sharepoint Online 라이브러리를 관리 하 고 팀 사이트에 대 한 사용 권한을 변경 하기 위한 **sharepoint 라이브러리** 탭이 있습니다. Office 365에 대 한 모든 비즈니스 계획에는 이러한 기본 SharePoint Online 기능이 포함 되어 있습니다.  
  
###  <a name="BKMK_StepThree"></a>3 단계: Office 365에 조직의 인터넷 도메인 이름 연결 (선택 사항)  
 조직에 주소가 지정 된 전자 메일의 고유한 인터넷 도메인과 SharePoint Online 리소스의 Url을 사용 하려는 경우 사용자 지정 도메인을 Office 365 구독에 연결할 수 있습니다. Windows Server Essentials 서버를 Office 365와 통합 하는 경우 대시보드에서이 작업을 수행할 수 있습니다.  
  
 온라인 계정을 대량으로 만들 때 도메인을 사용할 수 있도록 사용자에 대 한 온라인 계정을 만들기 전에이 작업을 수행 하는 것이 가장 쉽습니다.  
  
 Office 365에 등록할 때 도메인 이름을 얻습니다 (예: *contoso*. onmicrosoft.com). 다른 도메인 이름을 사용 하는 경우를 예로 들 수 있습니다. contoso.com? 도메인 이름을 아직 소유 하 고 있지 않은 경우 도메인 이름을 구입 하 고 일부 DNS 레코드를 변경 해야 합니다.  
  
 Office 365에서 사용할 사용자 지정 도메인 설정에는 다음 4 가지 작업이 포함 됩니다.  
  
1. **도메인 이름을 구매합니다.** 즉, 도메인 등록 기관 또는 DNS 호스팅 공급자에 등록합니다.  
  
   -   Office 365에서 작동 하는 도메인 이름을 선택 합니다. 두 번째 수준 도메인 이름 (예: buycontoso.com? 이지만 세 번째 수준 도메인 이름 (예: marketing.contoso.com)을 사용할 수 있습니다. Office 365에서 사용할 도메인을 선택 하는 방법에 대 한 자세한 내용은 [도메인](https://technet.microsoft.com/library/office-365-domains.aspx)을 참조 하세요.  
  
   -   Office 365에 필요한 DNS (도메인 이름 서버) 레코드를 허용 하는 도메인 등록 기관에서 구매 하세요. 필요한 DNS 레코드를 허용하는 도메인 등록 기관을 확인하려면 [도메인 이름 구매 방법](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)을 참조하세요. 다른 등록 기관에 도메인을 이미 등록 한 경우에는 걱정할 필요가 없습니다. 도메인을 Office 365에 연결할 때 도메인을 다른 등록자에 게 전송할 수 있습니다.  
  
2. **Office 365 서비스에서 도메인 이름을 사용하도록 허용하는 DNS 레코드를 구성합니다.** 가장 쉬운 방법은 3 단계에서 Office 365 구독에 도메인을 연결할 때 마법사에서 DNS 레코드를 자동으로 구성할 수 있도록 하는 것입니다. 사용자가 직접 수행 하 [는 경우 Office 365 통합에 대 한 DNS 레코드를 수동으로 구성 하는 방법](#BKMK_ManuallyConfigureDNS)을 참조 하세요.  
  
3. **Office 365 구독에 사용자 지정 인터넷 도메인을 연결 합니다.** **Office 365에 도메인 연결** 작업을 사용 합니다.  
  
4. **Office 365 서비스에서 새 도메인 이름을 사용 하 고 있는지 확인 합니다.**  
  
   **Office 365에 도메인 연결** 작업을 사용 하기 전에 1 단계와 2 단계를 완료 하면 마법사에서 도메인 이름을 office 365에 연결할 수 있습니다. 또는 마법사를 사용하여 1 및 2단계를 일부 또는 모두 수행할 수 있습니다.  
  
##### <a name="to-link-your-organizations-internet-domain-to-office-365"></a>Office 365에 조직의 인터넷 도메인을 연결 하려면  
  
1.  대시보드에서 **Office 365** 페이지를 열고 **Office 365에 도메인 연결**을 클릭합니다.  
  
2.  지시에 따라 마법사를 완료합니다.  
  
     이 마법사는 Office 365에서 사용할 새 인터넷 도메인 이름 또는 기존 인터넷 도메인 이름을 등록, 구성 및 연결 하기 위한 일부 또는 모든 단계를 지원할 수 있습니다.  
  
     마법사 페이지에서 도움말 링크를 클릭하여 작업을 완료하는 데 필요한 정보를 확인합니다. 또는 프로세스 개요 및 요구 사항에 대해서는 [Windows Server Essentials에서 원격 웹 액세스 관리](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx) 의 도메인 이름 설정 섹션을 참조 하세요.  
  
    > [!NOTE]
    >  마법사를 사용하여 새 도메인 이름을 등록하려면 마법사와의 원활한 통합을 제공하려고 Microsoft와 파트너 관계를 맺은 도메인 이름 서비스 공급자의 하나를 사용해야 합니다. 도메인 이름 등록 기관을 찾으려면 [도메인 이름 구매 방법](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)을 참조하세요.  
  
3.  마법사에서 도메인 이름이 서버에서 관리 되지 않음을 감지한 경우 구성을 완료 하려면 필요한 DNS 레코드를 수동으로 구성 해야 합니다. 자세한 지침은 이 항목의 후반부에서 [Office 365 통합에 대한 DNS 레코드를 수동으로 구성하는 방법](#BKMK_ManuallyConfigureDNS)을 참조하세요.  
  
4.  도메인이 Office 365에서 사용 중인지 확인 합니다.  
  
     마법사가 완료 되 고 나면 도메인 이름 등록 기관이 DNS 레코드를 확인 하는 동안 약간의 대기 시간입니다. 이는 자동으로 수행 됩니다. 아무것도 수행할 필요가 없습니다. 그러나 일반적으로는 약 1 시간 정도 걸리며 약간 더 긴 경우도 있습니다. 도메인 확인이 완료 되 면 **Office 365** 페이지에 조직의 도메인이 나열 됩니다.  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a>Office 365 통합에 대 한 DNS 레코드를 수동으로 구성 하는 방법  
 Office 365에 도메인 연결 마법사에서 도메인 이름이 서버에서 관리되지 않음을 감지할 경우 구성을 완료하려면 필요한 DNS(도메인 이름 서버) 레코드를 수동으로 구성해야 합니다. 이 경우 **%username%\NewDNSRecords_ (n) .txt**에서 구성 해야 하는 DNS 레코드의 목록을 찾을 수 있습니다. 여기서 *(n)* 은 임의의 숫자입니다.  
  
 다음 표에서는 추가해야 하는 DNS 레코드에 대해 설명합니다. 입력 방법은 도메인 이름 등록 기관에 따라 달라질 수 있습니다. 의문 사항이 있으면 도메인 이름 등록 기관에 도움을 요청하세요.  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>Office 365에 인터넷 도메인 이름을 연결하는 데 필요한 DNS 레코드  
  
|서비스|필요한 DNS 레코드|용도|  
|-------------|--------------------------|-------------|  
|(여러 서비스)|MX| Office 365에서는이 레코드를 사용 하 여 특정 도메인 이름을 소유 하 고 있는지 확인 합니다. 이 MX 레코드는 메일 메시지 라우팅을 충돌하지 않습니다.|  
|Exchange Online|MX|메일 메시지 라우팅을 제공합니다. **중요:**  전자 메일을 마이그레이션할 경우 새 MX 레코드에 기본 설정을 영(**0**)으로 할당하지 마세요. 레코드 값이 현재 MX 레코드에 할당된 값보다 큰지 확인합니다. 전자 메일 마이그레이션이 완료 되 고 메일 서버를 Office 365로 변경할 준비가 되 면 도메인 이름 등록 기관에서 새 MX 레코드의 기본 설정 값을 다시 설정 하도록 합니다.|  
|Exchange Online|별칭(CNAME)|사용자가 Exchange Online과 Outlook 데스크톱 클라이언트 또는 모바일 전자 메일 클라이언트 사이의 연결을 손쉽게 설정하도록 도와주는 데 사용되는 자동 검색 레코드입니다. **참고:**  조직의 고유한 도메인 이름 (예 http://mail.contoso.com) https://outlook.com/owa/office365.com):)을 사용 하 여 Outlook 웹 액세스에 액세스 하려는 경우 별칭 (CName) 레코드를 다음과 같이 구성할 수 있습니다. **유형 = CNAME, TTL = 01:00:00, HostName = mail, Address = office365**|  
|Exchange Online|TXT|Office 365 전자 메일 서버에서 사용 하는 도메인에 도메인 대신 전자 메일을 보낼 수 있는 권한이 outlook.com 지정 합니다. 이 레코드를 만들어 아웃바운드 메일에 스팸으로 플래그가 지정되지 않도록 합니다.|  
|Lync Online|SRV|Windows Live 또는 Yahoo!와 같은 기타 인스턴트 메시징 서비스와의 페더레이션을 사용하도록 도와줍니다.|  
|Lync Online|SRV|사용자가 Lync 데스크톱 클라이언트와 Microsoft Lync Online 사이의 연결을 손쉽게 설정하도록 도와주는 데 사용되는 자동 검색 레코드입니다.|  
  
> [!IMPORTANT]
>  도메인 확인이 완료 된 후에는 Office 365 포털에서 DNS 레코드를 추가 하거나 추가로 변경 하지 마세요.  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a> 다음 단계  
  
-   사용자에 대한 Microsoft Online Services 계정을 만듭니다.  
  
     Office 365 서비스를 사용 하려면 사용자에 게 네트워크 사용자 계정과 연결 된 Microsoft Online Services 계정이 있어야 합니다. 대시보드에서 쉽게 만들 수 있습니다. 새 Office 365 구독을 사용 중인 경우 기존 사용자 계정에 대 한 온라인 계정을 일괄적으로 만들 수 있습니다. 이미 사용 중인 Office 365 구독과 새 서버를 통합 하는 경우 기존 온라인 계정에서 사용자 계정을 가져올 수 있습니다. 절차는 [사용자에 대 한 온라인 계정 관리](Manage-Online-Accounts-for-Users.md)를 참조 하세요.  
  
> [!NOTE]
>  Windows Server Essentials의 대시보드에서 Microsoft Online Services 계정을 Office 365 계정 이라고 합니다. 계정은 동일하고 용어만 변경됩니다.  
  
##  <a name="BKMK_ManageIntegration"></a>Office 365 통합 관리  
 서버를 Office 365와 통합 하 고 나면 대시보드의 **office 365** 페이지에 office 365 구독에 대 한 정보가 표시 되 고 다음과 같은 작업을 사용할 수 있습니다.  
  
-   [Office 365 구독을 관리](#BKMK_ManageO365) 하 시겠습니까? 구독을 관리 하는 데 사용 하는 관리자 계정을 변경 합니다. Office 365 관리 대시보드를 열어 구독을 관리 합니다.  
  
-   [Office 365에 조직의 인터넷 도메인을 연결 합니다](#BKMK_StepThree) . 자신의 도메인에 주소가 지정 된 전자 메일을 보내고 받을 수 있도록 하려면 Office 365에 도메인을 연결 하면 됩니다. (앞 [에서 설명한 3 단계: Office 365](#BKMK_StepThree)에 조직의 도메인을 연결 합니다.  
  
-   [Office 365 통합을 사용 하지 않도록 설정](#BKMK_Disable) 하 시겠습니까? 대시보드에서 Office 365 서비스, 구독 및 온라인 계정을 관리 하지 않으려면 Office 365 통합을 사용 하지 않도록 설정할 수 있습니다. Office 365 포털에서 서비스를 계속 사용할 수 있습니다.  
  
###  <a name="BKMK_ManageO365"></a>Office 365 구독 관리  
 서버에서 작업 하는 동안 Office 365 구독을 변경 해야 하는 경우 대시보드의 **office 365** 페이지에서 office 365의 구독을 열 수 있습니다. 서버에서 Office 365 서비스를 변경 하는 데 사용 하는 관리자 계정을 변경할 수도 있습니다.  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>Office 365 관리 대시보드에서 구독을 열려면  
  
1.  Windows Server Essentials 대시보드에서 **Office 365** 페이지를 엽니다.  
  
2.  **구성 작업**에서 **Office 365 관리**를 클릭합니다.  
  
3.  구독을 관리 하는 데 사용 하는 Microsoft 온라인 계정으로 Office 365에 로그인 합니다.  
  
     Office 365 관리자 대시보드가 열립니다.  
  
##### <a name="to-change-the-office-365-administrator-account"></a>Office 365 관리자 계정을 변경하려면  
  
1.  대시보드에서 **Office 365**를 클릭합니다.  
  
2.  **구성 작업**에서 **Office 365 관리자 계정 변경**을 클릭합니다. 관리자 계정 변경 마법사가 나타납니다. Windows Server Essentials에서 마법사의 이름은 Office 365 관리자 계정으로 설정 됩니다.  
  
3.  Office 365 구독에 연결 하는 데 사용 하려는 계정에 대 한 자격 증명을 입력 하 고 **다음**을 클릭 합니다.  
  
4.  **닫기**를 클릭합니다. 대시보드가 다시 시작됩니다.  
  
###  <a name="BKMK_Disable"></a>Office 365 통합 사용 안 함  
 대시보드에서 Office 365 서비스 및 온라인 계정을 관리 하지 않으려는 경우 Office 365 통합을 사용 하지 않도록 설정할 수 있습니다. Office 365 구독은 활성 상태로 유지 되 고 대시보드에서 변경한 모든 구성이 계속 적용 됩니다. 예를 들어, Office 365 구독에 연결 된 도메인 이름으로 주소가 지정 된 전자 메일을 받게 됩니다. 전자 메일을 잃지 않으며 모바일 장치에 대해 설정한 컨트롤이 Exchange Online에서 계속 사용 됩니다.  
  
 앞으로는 office 365에서 Office 365 구독, 서비스 및 리소스를 관리 하 고, 사용자는 Office 365에서 온라인 계정에 대 한 암호를 관리 해야 합니다. 암호 동기화가 더 이상 수행 되지 않고 사용자 계정을 사용 하지 않도록 설정 하거나 제거 해도 사용자의 온라인 계정에는 영향을 주지 않습니다.  
  
 Office 365 통합 소프트웨어는 로컬 서버에 설치 되므로 통합 서비스가 Office 365에 연결할 수 없는 경우에도이 기능을 사용 하지 않도록 설정할 수 있습니다.  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>서버와의 Office 365 통합을 사용하지 않도록 설정하려면  
  
1.  대시보드에서 **Office 365**를 클릭합니다.  
  
2.  **Office 365 통합 사용 안 함**을 클릭합니다. Office 365 사용 안 함 마법사가 나타납니다.  
  
3.  지시에 따라 마법사를 완료합니다.  
  
> [!NOTE]
>  Office 365 통합을 다시 사용 하도록 설정 하려면 대시보드 **홈** 페이지의 **서비스** 탭에서 **office 365와 통합** 작업을 사용 합니다. 자세한 내용은 2 단계: [ 이 항목의 앞부분에 나오는 Microsoft Office 365](#BKMK_StepTwo)와 Windows Server Essentials 서버를 통합 합니다.  
  
##  <a name="BKMK_Troubleshoot"></a>Office 365 통합 문제 해결  
 이 섹션에서는 Windows Server Essentials에서 Office 365 통합 기능을 사용 하는 경우 발생할 수 있는 일반적인 문제를 해결 하는 데 도움이 되는 정보를 제공 합니다.  
  
###  <a name="BKMK_AcctsNotCreated"></a>일부 Microsoft Online Services 계정이 만들어지지 않았습니다.  
 **설명**  
  
 대시보드에서 하나 이상의 Microsoft Online Services 계정을 만들려는 시도가 실패 했습니다.  
  
 **해결 방법**  
  
1.  마법사 완료 페이지에서 링크를 클릭하여 제대로 완료되지 않은 각 계정 만들기 요청에 대한 세부 정보가 포함된 결과 파일을 엽니다. 예를 들어 결과에는 요청된 계정의 이름을 가진 Microsoft Online Services 계정이 이미 있음을 알리는 정보가 표시될 수 있습니다.  
  
2.  권장 작업을 수행하여 각 오류를 해결합니다.  
  
3.  이 문제가 지속되면 서버를 다시 시작하고 온라인 계정을 다시 만들어 보세요.  
  
###  <a name="BKMK_ProblemUninstalling"></a>Office 365 통합을 제거 하는 동안 문제가 발생 했습니다.  
 **설명**  
  
 Office 365 통합을 사용 하지 않도록 설정 하려고 할 때 알 수 없는 오류가 발생 했습니다.  
  
 **해결 방법**  
  
1.  컴퓨터가 인터넷에 연결되어 있는지 확인하고 다시 시도합니다.  
  
2.  오류가 다시 발생하면 서버를 다시 시작하고 다시 시도합니다.  
  
## <a name="see-also"></a>참조  
  
-   [Windows Server Essentials에 대 한 서비스 통합 개요-1 부](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials에 대 한 서비스 통합 개요-2 부](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [Microsoft Office 365를 사용 빠른 시작 가이드](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)
