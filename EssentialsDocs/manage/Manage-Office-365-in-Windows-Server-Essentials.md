---
title: "Windows Server Essentials의 Office 365 관리"
description: "Windows Server Essentials을 사용 하는 방법을 설명 합니다."
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="manage-office-365-in-windows-server-essentials"></a>Windows Server Essentials의 Office 365 관리

>Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials에 적용 됩니다.

Windows Server Essentials 서버에 Microsoft Office 365와 통합 하는 경우 Windows Server Essentials 대시보드에서 온-프레미스 리소스와 Office 365 서비스 및 온라인 계정을 관리할 수 있습니다. 이 항목에서 자 있습니다 알아봅니다 서버 Office 365와 통합 하 여 얻을 수 있는를 수행 하는 방법 관리 하 고 Office 365 통합 문제를 해결 하는 방법.  
  
  
  
> [!IMPORTANT]
>   Office 365 통합 단일 도메인 컨트롤러 환경에만 지원 됩니다. 또한 Office 365 통합 마법사 도메인 컨트롤러에서 실행 해야 합니다.  
  
## <a name="in-this-topic"></a>이 항목에서  
  
-   [내 서버와 Office 365을 통합 해야 하나요?](#BKMK_IntegrationOverview)  
  
-   [Office 365 통합 설정](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Configure)  
  
-   [Office 365 통합 관리](#BKMK_ManageIntegration)  
  
-   [Office 365 통합 문제 해결](Manage-Office-365-in-Windows-Server-Essentials.md#BKMK_Troubleshoot)  
  
##  <a name="BKMK_IntegrationOverview"></a>내 서버와 Office 365을 통합 해야 하나요?  
 Windows Server Essentials 서버와 Office 365 통합 하는 이유에 많이 있습니다. 일부의 리소스 사내 관리 Office 365를 사용 하 여 다른 서비스에 대 한 경우 자를 관리할 수 Office 365 서비스 및 리소스 두 곳에서 작동 하는 대신 사용자 온-프레미스 리소스와 함께 대시보드에서 합니다.  
  
-   Office 365에 함께 사용자 계정에 사용자가 액세스할 수 있도록 온라인 계정 관리 합니다.  
  
    -   한 번에 사용자를 위한 Microsoft Online Services 계정을 만들거나 온라인 하면 기존 계정에 대 한 서버에서 사용자 계정 만들기. 또한 새로운 기능이 나 기존 사용자 계정에 한 온라인 계정을 추가할 수 있습니다.  
  
         를 대시보드에서 온라인 계정을 만들 때 사용자가 로그인에 Office 365 서버에 사용 하는 동일한 암호를 사용 합니다. 사용자 계정에 대 한 암호를 변경 하 고 온라인 암호도 변경 됩니다. 및 온라인 계정 암호 항상 보안 요구 사항을 충족 사용자 계정에 대해 설정한 알 수 있습니다.  
  
    -   사용자 계정의 수명 전반에 걸쳐 사용자 계정 함께 한 온라인 계정을 관리 합니다. 사용자 계정이 비활성화 하면 온라인 계정 또한 비활성화 됩니다. 사용자 계정을 제거 하는 경우 온라인 계정도 제거 됩니다.  
  
    -   Windows Server Essentials 서버에서 메일에 메일 그룹 Exchange Online을 관리 합니다.  
  
-   Office 365 구독을 사용자 지정 인터넷 도메인에 연결 하 여 조직의 인터넷 도메인 (예를 들어 contoso.com)에서 메일 및 보냅니다.  
  
-   구독 및 Office 365 통합 대시보드에서 관리 합니다.  
  
-   구독 SharePoint Online 라이브러리에 있는 경우 Windows Server Essentials 서버와 Office 365의 통합 수 있습니다.  
  
    -   만들고 대시보드에서 SharePoint Online 라이브러리 관리 합니다.  
  
        > [!NOTE]
        >  자 사용자도 수 내 Server 2012 r 2 앱을 사용 하 여 노트북, 휴대폰, 또는 Windows phone에서 SharePoint Online 라이브러리에 있는 문서와 작동 하도록. 이 기능은 Windows Server Essentials에 사용할 수만 있습니다. 자세한 내용은 참조 [내 서버 앱을 사용 하 여](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)합니다.  
  
    -   대시보드에서 SharePoint Online 사이트 팀에 대 한 사용 권한 변경 또는 기타 변경 대시보드에서 팀 사이트를 엽니다.  
  
     자세한 내용은 참조 [SharePoint Online 관리](Manage-SharePoint-Online-in-Windows-Server-Essentials.md)합니다.  
  
-   Exchange Online에 가입 하는 경우 Windows Server Essentials 서버와 Office 365 통합 회사 메일 서버에 연결 하 여 사용자가 사용 하 여 휴대폰을 관리할 수 있습니다.  
  
    -   모바일 디바이스 회사 메일 서버에 연결할 때 암호 보호가 필요 합니다. 최소 암호 길이 설정의 로그인 시도가 실패를 허용 하 고 최소 시간 로그인 시도 사이 필요한 수 있습니다.  
  
    -   모바일 디바이스의 보안 문제를 디바이스 모델 알고 있는 경우 Exchange Online에 연결 하지 못하도록 차단 합니다.  
  
    -   모바일 디바이스를 분실 하거나 도난당 하는 경우 다음에 디바이스 켜져 회사의 중요 한 데이터를 삭제 하는 디바이스를 삭제 합니다.  
  
-    Office 365 통합 Office 365 서비스 및 리소스에 연결 하는 새로운 방법을 제공 됩니다.  
  
    -   Windows Server Essentials 실행 패드에서 Office 365 서비스를 엽니다. 자세한 내용은 참조 하십시오 [빠른 시작 가이드를 사용 하 여 Microsoft Office 365에](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)합니다.  
  
    -   내 Server 2012 r 2 앱을 사용 하 여 노트북, 휴대폰, 또는 Windows phone에서 SharePoint Online 라이브러리에 있는 문서와 작동 하도록 합니다. 자세한 내용은 참조 하십시오 [내 서버 앱을 사용 하 여](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)합니다. 이 기능은 Windows Server Essentials에서 사용할 수만 있습니다.  
  
##  <a name="BKMK_Configure"></a>Office 365 통합 설정  
 언제 든 지 서버 설치를 완료 한 후 Office 365 서버를 통합할 수 있습니다. 인할 이미 Office 365 구독, 구입 하거나 무료 평가판 구독이에 등록할 수 있습니다.  
  
 다음과 같은 작업을 수행 합니다.  
  
-   [1 단계: Office 365 통합 요구 사항 확인](#BKMK_StepOne_VERIFY)  
  
-   [2 단계: 서버 Microsoft Office 365와 통합](#BKMK_StepTwo)  
  
-   [3 단계: 조직의 인터넷 도메인 이름 (옵션) Office 365에 연결](#BKMK_StepThree)  
  
###  <a name="BKMK_StepOne_VERIFY"></a>1 단계: Office 365 통합 요구 사항 확인  
 시작 하기 전에 서버 이러한 요구 사항을 충족 하는지 확인 합니다.  
  
-   다음 운영 체제 중 하나는 서버 있을 수 있습니다: Windows Server Essentials, Windows Server Essentials 또는 Windows Server Essentials 경험 역할이 설치와 Windows Server 2012 r 2 표준 또는 Windows Server 2012 R2 Datacenter 운영 체제입니다.  
  
-   환경 도메인 컨트롤러를 가질 수 있습니다 및 도메인 컨트롤러에서 Office 365 통합 수행 해야 합니다.  
  
-   서버에서 인터넷에 연결할 수 있어야 합니다.  
  
-   Office 365 통합 시작 하기 전에 서버에 모든 중요 하 고 중요 업데이트를 설치 해야 합니다.  
  
-   조직의 인터넷 도메인 이메일 주소 및 SharePoint Online 리소스를 사용 하려는 경우 하면을 할 통합 하는 동안 도메인 Office 365에 연결할 수 있도록 도메인 이름 등록 합니다. 자세한 내용은 참조 [도메인 이름 구입 하는 방법을](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)합니다.  
  
> [!NOTE]
>  사전에 Office 365 구독을 t 필요를 하지 합니다. 자 하는 구독을 구입 하거나 Office 365 통합 하는 동안 무료 평가판에 등록할 수 있습니다. D 하려는 경우 발전해왔는지 살펴보겠습니다 계획 및 Office 365에 대 한 가격 [비즈니스에서 Office 365 계획 비교](https://office.microsoft.com/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_subscribe-to-office-365_Text)합니다.  
  
###  <a name="BKMK_StepTwo"></a>2 단계: 서버 Microsoft Office 365와 통합  
 Windows Server Essentials 서버 Office 365와 통합 하는 도메인 컨트롤러에서 다음 절차를 수행 합니다.  
  
> [!NOTE]
>  절차 s 동일한 있는지 여부 Windows Server Essentials 또는 Windows Server Essentials, 자 수 있지만 홈 페이지에서 다른 위치를 시작 합니다. Windows Server Essentials의 서버 다른 Microsoft Online Services와 Office 365 통합는 **서비스** 탭 합니다. Windows Server Essentials의 Office 365 통합에 수행 되는 **메일** 탭 합니다.  
  
##### <a name="to-integrate-the-server-with-office-365"></a>서버 Office 365와 통합  
  
1.  관리자 권한 서버에에 로그인 하 고 Windows Server Essentials 대시보드 엽니다.  
  
2.  에 **홈** 페이지, 클릭 **서비스** (Windows Server Essentials 클릭 **메일**)를 클릭 **Microsoft Office 365와 통합**, 클릭 한 다음 **Microsoft Office 365 통합 설정**합니다.  
  
     Microsoft Office 365와 통합 마법사가 나타납니다.  
  
3.  에 **시작** 페이지에서 다음 중 하나를 수행 합니다.  
  
    -   T 함에 Office 365 구독을가지고 클릭 **다음**, 구독할 Office 365 또는 기호를 평가판 구독에 대 한 지침을 따릅니다.  
  
         사용자 할 마법사를 반환 하기 전에 Office 365에 로그인 합니다. 하지만 t 필요가의 작업을 수행 하지는 **여기에서 시작** Office 365 포털의 섹션.  
  
    -   이미 서버를 선택 하 고 통합 하는 Office 365를 구독 하는 경우 **Office 365 구독을 이미**을 차례로 클릭 하 고 **다음**합니다.  
  
4.  마법사를 완료 하 고 지침을 따릅니다.  
  
 마법사 성공적으로 완료 된 후 하면 자 대시보드에 다음과 같은 변경 사항이 확인할 다음과 같습니다.  
  
-   새 s 여기 **Office 365** 페이지를 통합 하 고 Office 365 구독을 관리 하는 데 사용 됩니다.  
  
-   에 **사용자** 페이지를 참조 자는 **온라인 계정** 작성 하 고 Office 365에 사용자가 액세스할 수 있도록 하는 Microsoft Online Services 계정을 관리할 수 있는 탭 합니다. 온라인 교환를 사용 하 여 다시 하는 경우 및 Windows Server Essentials 서버는 사용자 자 또한 표시를 **메일 그룹** 탭 합니다.  
  
-   **저장소** Windows Server Essentials 서버에 페이지에는 **SharePoint 라이브러리** SharePoint Online 라이브러리 관리 하 고 팀 사이트에 대 한 권한 변경 탭 합니다. Office 365에 대 한 모든 비즈니스 계획 기본 이러한 SharePoint Online 기능이 포함 되어 있습니다.  
  
###  <a name="BKMK_StepThree"></a>3 단계: 조직의 인터넷 도메인 이름 (옵션) Office 365에 연결  
 자신의 인터넷 도메인 조직 및 SharePoint Online 리소스에 대 한 Url 사람에 게 보내는 메일을 사용 하려면 Office 365 구독을 사용자 지정 도메인을 연결할 수 있습니다. Office 365와 Windows Server Essentials 서버를 통합 하는 경우 대시보드에서이 수행할 수 있습니다.  
  
 것 대량-만들 때 온라인 계정을 도메인을 사용할 수 있도록 사용자를 위한 계정 s 온라인를 만들기 전에이 작업을 수행 하는 가장 쉬운 방법입니다.  
  
 Office 365에 가입할 때 도메인 이름 받을 수 있나요? 예를 들어, *contoso*. onmicrosoft.com 합니다. D 아니라 사용 하는 경우 다른 도메인 이름? 이렇게 말 하세요 contoso.com 간단 하 게? 할 수 있습니다. 사용자 할를 구입 하는 도메인 이름 인할 경우 이미 직접 하나 DNS 레코드 중 일부를 변경 합니다.  
  
 Office 365를 사용 하 여 사용자 지정 도메인 설정 네 가지 작업이 포함 됩니다.  
  
1.  **구입 도메인 이름입니다.** 즉, 도메인 등록 기관 또는 호스팅 공급자 DNS 등록 합니다.  
  
    -   Office 365와 함께 작동 하는 도메인 이름을 선택 합니다. 두 번째 수준 도메인 이름 사용할 수? buycontoso.com 예를 들어,? 하지만 3 수준 도메인 이름 하지? marketing.contoso.com 예를 들어, 합니다. Office 365에서 사용 하는 도메인 선택에 대 한 자세한 내용은 참조 [도메인](https://technet.microsoft.com/library/office-365-domains.aspx)합니다.  
  
    -   Office 365에 필요한 도메인 이름 (DNS) 서버 레코드 수 있도록 해 주는 도메인 관리자에서 구입 합니다. 도메인 기관 허용 필요한 DNS 레코드를 확인 하려면 [도메인 이름 구입 하는 방법을](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)합니다. 이미에 등록 한 경우 도메인 다른 등록 기관에 않거나 걱정 t; Office 365 도메인에 연결할 때 도메인 다른 관리자 전송할 수 있습니다.  
  
2.  **Office 365 서비스 도메인 이름 사용 하도록 허용 하는 DNS 레코드를 구성 합니다.** 3 단계에서 Office 365 구독 도메인에 연결할 때 DNS 레코드를 구성 하 고 마법사 하도록 하는 가장 쉬운 방법은 합니다. D 대신 이렇게 하면 사용자가 직접 경우 [DNS 수동으로 구성 하는 방법을 Office 365 통합 기록](#BKMK_ManuallyConfigureDNS)합니다.  
  
3.  **Office 365 구독을 사용자 지정 인터넷 도메인에 연결 합니다.** 자 사용은 **도메인 Office 365를 연결할** 동작 합니다.  
  
4.  **Office 365 서비스는 새 도메인 이름 사용 하 여 확인 합니다.**  
  
 사용 하기 전에 1과 2 단계를 완료 하는 경우는 **도메인 Office 365를 연결할** 작업을 마법사 도메인 이름 Office 365를 연결할 수 있습니다. 또한, 1, 2 단계 중 일부 또는 전부를 하는 데 도움이 되는 마법사를 할 수 있습니다.  
  
##### <a name="to-link-your-organization-s-internet-domain-to-office-365"></a>Office 365에 조직의 인터넷 도메인에 연결 하려면  
  
1.  대시보드에서 열고는 **Office 365** 페이지, 클릭 한 **도메인 Office 365를 연결할**합니다.  
  
2.  마법사를 완료 하 고 지침을 따릅니다.  
  
     마법사 등록 구성 하 고 Office 365에 사용 하 여 새로운 기능이 나 기존 인터넷 도메인 이름 연결 하는 단계 중 일부 또는 전부를 돕습니다.  
  
     마법사 페이지 작업을 완료 하는 데 필요한 정보를 도움말 링크를 클릭 합니다. 설정의 도메인 이름 섹션 참조 하거나 [Windows Server Essentials의 원격 Web Access 관리](https://technet.microsoft.com/library/jj628152\(d=printer\).aspx) 프로세스 개요 및 요구 합니다.  
  
    > [!NOTE]
    >  마법사 새 도메인 이름 등록할 수를 사용 하려면 도메인 이름 서비스 공급자 완벽 한 통합 마법사를 제공 하기 위해 Microsoft와 파트너 관계를 중 하나를 사용 해야 합니다. 확인 하려면 도메인 이름 등록 기관, [도메인 이름 구입 하는 방법을](https://office.microsoft.com/office365-suite-help/how-to-buy-a-domain-name-HA102819883.aspx?CTT=5&origin=HA102818660)합니다.  
  
3.  마법사에서 되지 않으면 프로그램 도메인 이름 서버에서 관리를 발견 하면 하면을 할 직접 구성을 완료 하 고 필요한 DNS 레코드를 구성 합니다. 자세한 내용은 [DNS 수동으로 구성 하는 방법을 Office 365 통합 기록](#BKMK_ManuallyConfigureDNS)이 항목 뒷부분에, 합니다.  
  
4.  도메인 Office 365에 사용 되 고 있는지 확인 합니다.  
  
     여기 s 있으며 도메인 이름 관리자 확인 DNS 레코드 마법사를 완료 한 후 작은 대기 합니다. 이 설정이 자동으로; t 함 아무것도 수행 해야 합니다. 하지만 일반적으로 약 1 시간 차지? 한 경우에 따라 약간 더 오래 합니다. 도메인 확인 완료 되 면는 **Office 365** s 조직 도메인 페이지에 나열 됩니다.  
  
####  <a name="BKMK_ManuallyConfigureDNS"></a>Office 365 통합 DNS 레코드 수동으로 구성 하는 방법  
 Office 365 마법사 링크 나만의 도메인 도메인 이름 서버 관리 하지 않는 것을 감지, 하려면 구성을 완료 수동으로 구성 해야 필요한 도메인 이름 (DNS) 서버 레코드 합니다. 자 사용자 DNS 레코드에 구성 해야 할 목록을 찾고 경우 **%username%\NewDNSRecords_ (n).txt**, 여기서 *(n)* 임의의 수입니다.  
  
 다음 표에서 설명 DNS 레코드를 추가 해야 합니다. 다른 도메인 이름 기관 입력 방법에 따라 달라질 수 있습니다. 질문이 있는 경우 도메인 이름 관리자에 게 도움 요청 합니다.  
  
### <a name="required-dns-records-for-linking-a-custom-internet-domain-name-to-office-365"></a>Office 365를 사용자 지정 인터넷 도메인 이름 연결 하는 데 필요한 DNS 레코드  
  
|서비스|필요한 DNS 레코드|목적|  
|-------------|--------------------------|-------------|  
|(여러 서비스)|MX| Office 365이 녹화를 사용 하 여 특정 도메인 이름 소유 있는지 확인 합니다. 메일 메시지 경로 MX 녹화 방해 하지 않습니다.|  
|Exchange 온라인|MX|메일 메시지 경로 제공합니다. **중요:** 마이그레이션 메일 인 경우 0 기본 설정 지정 하지 (**0**) 새 MX 기록에 있습니다. 기록에 대 한 값은 현재 MX 기록에 할당 값을 보다 큰 있는지 확인 합니다. 메일 마이그레이션을 완료 되 고 Office 365에 메일 서버를 변경 하려면 준비가, 새 MX 기록 기본 값을 다시 설정 하면 도메인 이름 관리자를 했습니다.|  
|Exchange 온라인|별칭 (CNAME)|손쉽게 사용자를 위해 사용 되는 자동 검색 기록 Exchange Online을 Outlook 데스크톱 클라이언트 하거나 모바일 메일 클라이언트 간에 연결을 설정 합니다. **참고:** Outlook Web Access 조직 s 직접 도메인 이름 (예를 들어 http://mail.contoso.com) 표준 URL (https://outlook.com/owa/office365.com) 대신 사용 하 여 액세스 하려는 구성할 수 있습니다 (CName) 별칭 기록 다음과 같은: **유형 CNAME TTL = 01 =: 00:00 호스트 메일 주소를 = mail.office365.com =**|  
|Exchange 온라인|TXT|Office 365 메일 서버를 사용 하는 도메인 outlook.com 도메인을 대표 하 여 메일을 보낼 수 있는 권한이 있는지를 지정 합니다. 이 레코드 아웃 바운드 메일 스팸 것으로 표시 되지 않도록 방지를 만듭니다.|  
|Lync 온라인|SRV|Windows Live 또는 yahoo!와 같은 다른 인스턴트 메시지 서비스 federation 수 있습니다.|  
|Lync 온라인|SRV|자동 검색 기록 쉽게 사용자를 위해 사용 되는 데스크톱 클라이언트 Lync 및 Microsoft Lync 온라인 간에 연결을 설정 합니다.|  
  
> [!IMPORTANT]
>  인증 완료 된 후 도메인, 추가 또는 Office 365 포털에서 DNS 레코드를 더 이상 변경 하지 마십시오.  
  
###  <a name="BKMK_StepFour_ACCOUNTS"></a>다음 단계  
  
-   사용자가 Microsoft Online Services 계정을 만듭니다.  
  
     Office 365 서비스를 사용 하려면 사용자가 해당 네트워크 사용자 계정과 연결 된 Microsoft Online Services 계정이 있어야 합니다. 대시보드 쉽게이 있습니다. 하는 경우 사용 하는 새로운 Office 365를 구독 하면 대량-계정을 만들 수 있습니다 온라인 기존 사용자 계정에 대 한 합니다. 하는 경우, 사용자 이미 사용 하 여 다시 가져올 수 있습니다 사용자 계정에서 기존 온라인 Office 365 구독이 새 서버 통합 된 계정 합니다. 절차 참조 하십시오 [사용자에 대 한 온라인 계정을 관리](Manage-Online-Accounts-for-Users.md)합니다.  
  
> [!NOTE]
>  Windows Server Essentials의 대시보드에서 온라인 서비스 Microsoft 계정 이라고에 Office 365 계정이 합니다. 계정은 동일 합니다. 만 용어 변경 합니다.  
  
##  <a name="BKMK_ManageIntegration"></a>Office 365 통합 관리  
 서버에 Office 365와 통합 하면는 **Office 365** 대시보드에서 페이지 Office 365 구독에 대 한 정보를 표시 하 고 이러한 작업을 사용할 수 있게 합니다.  
  
-   [Office 365 구독 정보를 관리](#BKMK_ManageO365) 있나요? 구독 관리를 사용 하는 관리자 계정을 변경 합니다. Office 365 관리자 대시보드를 구독 정보를 관리를 엽니다.  
  
-   [Office 365 조직의 인터넷 도메인 연결할](#BKMK_StepThree) 있나요? 사용자가 도메인에 게 보내는 메일을 주고받을 수 하려는 경우 도메인 Office 365를 연결할 수 있습니다. (에서 이전에 설명한 [3 단계: s 조직 도메인 Office 365를 연결할](#BKMK_StepThree).)  
  
-   [Office 365 통합 사용 안 함](#BKMK_Disable) 있나요? T 함을 대시보드에서 Office 365 서비스, 구독 및 온라인 계정 관리 하려면 Office 365 통합을 비활성화할 수 있습니다. 서비스는 Office 365 포털에 사용할 수 있습니다.  
  
###  <a name="BKMK_ManageO365"></a>Office 365 구독 정보를 관리합니다  
 Office 365의 구독을 열 수 다시 서버에서 작업 하는 동안 Office 365 구독을 변경 하려는 경우는 **Office 365** 대시보드의 페이지 합니다. Office 365 서비스를 변경 하는 서버에서 사용 하는 관리자 계정을 변경할 수 있습니다.  
  
##### <a name="to-open-your-subscription-on-the-office-365-admin-dashboard"></a>Office 365 관리자 대시보드에서 구독을 열려면  
  
1.  Windows Server Essentials 대시보드에서 열고는 **Office 365** 페이지 합니다.  
  
2.  **구성 작업**, 클릭 **Office 365 관리**합니다.  
  
3.  Office 365 구독 정보를 관리를 사용 하는 온라인 Microsoft 계정으로 로그인 합니다.  
  
     Office 365 관리자 대시보드가 열립니다.  
  
##### <a name="to-change-the-office-365-administrator-account"></a>Office 365 관리자 계정을 변경 하려면  
  
1.  클릭 하 고 대시보드에서 **Office 365**합니다.  
  
2.  **구성 작업**, 클릭 **Office 365 관리자 계정을 변경**합니다. 변경 관리자 계정 마법사가 나타납니다. (Windows Server Essentials 마법사 이름이 the Office 365 관리자 계정 설정입니다.)  
  
3.  Office 365를 구독 하 여 연결을 클릭 한 다음 사용할 계정 자격 증명 입력 **다음**합니다.  
  
4.  클릭 **닫기**합니다. 대시보드 다시 시작합니다.  
  
###  <a name="BKMK_Disable"></a>Office 365 통합 사용 안 함  
 인할 결정 대시보드에서 온라인 계정을 확인 하 고 Office 365 서비스를 관리 하려면, Office 365 통합 비활성화할 수 있습니다. Office 365 구독, 활성 상태를 유지 하 고 구성 변경 대시보드에서 내용을 적용 된 상태로 유지 합니다. 예를 들어, 사용자 자 Office 365 구독에 연결 되어 있는 도메인 이름 사람에 게 보내는 메일을 받습니다. 성공 하면 t 손실, 메일 및 모바일 디바이스용 설정한 컨트롤은 여전히 Exchange Online을 사용 합니다.  
  
 앞으로 Office 365 구독, 서비스 및 Office 365의 리소스 관리 하 고 사용자가 Office 365에서 자녀가 온라인 계정에 대 한 암호 관리 해야 합니다. 암호 동기화 더 이상 발생 마우스 사용자 계정을 제거 하거나 비활성화 합니다 사용자 s 온라인 계정에 영향을 주지 않습니다.  
  
 Office 365 통합 소프트웨어가 설치 되어 있는 로컬 서버의 하기 때문에 통합 서비스는 Office 365를 연결할 수 없는 경우에이 기능을 해제할 수 있습니다.  
  
##### <a name="to-disable-office-365-integration-with-the-server"></a>서버와 Office 365의 통합을 사용 하지 않도록 설정 하려면  
  
1.  클릭 하 고 대시보드에서 **Office 365**합니다.  
  
2.  클릭 **Office 365 통합 사용 안 함**합니다. Office 365 사용 안 함 마법사가 나타납니다.  
  
3.  마법사를 완료 하 고 지침을 따릅니다.  
  
> [!NOTE]
>  Office 365 통합 다시를 사용 하려면 사용는 **Office 365와 통합** 에서 작업의 **서비스** s 대시보드의 탭 **Home** 페이지 합니다. 자세한 내용은 [2 단계: Windows Server Essentials 서버에 Microsoft Office 365와 통합](#BKMK_StepTwo)이 항목에서 이전, 합니다.  
  
##  <a name="BKMK_Troubleshoot"></a>Office 365 통합 문제 해결  
 Windows Server Essentials의 Office 365 통합 기능을 사용 하는 경우 발생할 수 있는 일반적인 문제를 해결 하는 데 도움이 되는 정보를 제공이 합니다.  
  
###  <a name="BKMK_AcctsNotCreated"></a>일부 Microsoft Online Services 계정은 만들지 않은  
 **설명**  
  
 하나 이상의 Microsoft Online Services 계정 대시보드 너 t에서 성공 만들 수 없습니다.  
  
 **해결 방법**  
  
1.  성공적으로 완료 되지 않은 각 계정 만들기 요청에 대 한 세부 정보가 포함 된 결과 파일을 열려면 마법사 완성 페이지의 링크를 클릭 합니다. 예를 들어, 결과 수 알려는 Microsoft Online Services 계정이 이미 있는 요청한 계정 이름으로 합니다.  
  
2.  각 오류를 해결 하기 위해 권장된 조치를 취하십시오.  
  
3.  이 문제가 계속 되 면 서버를 다시 시작 하 고 온라인 계정을 다시 만들어 보세요.  
  
###  <a name="BKMK_ProblemUninstalling"></a>Office 365 통합 제거에 문제가 있었습니다.  
 **설명**  
  
 Office 365 통합 사용 하지 않도록 설정 하려고 할 때 오류가 발생 했습니다.  
  
 **해결 방법**  
  
1.  컴퓨터가 인터넷에 연결 되어 있는지 확인 한 후 다시 시도 합니다.  
  
2.  오류가 발생 다시, 서버를 다시 시작 하 고 후 다시 시도 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [Windows Server Essentials 1 부분에 대 한 서비스 통합 개요](http://blogs.technet.com/b/sbs/archive/2013/11/04/services-integration-overview-for-windows-server-2012-r2-essentials-part-1.aspx)  
  
-   [Windows Server Essentials-2에 대 한 서비스 통합 개요](http://blogs.technet.com/b/sbs/archive/2013/11/06/services-integration-overview-for-windows-server-2012-r2-essentials-part-2.aspx)  
  
-   [빠른 시작 가이드로 시작 Microsoft Office 365를 사용 하 여](../use/Quick-Start-Guide-to-Using-Microsoft-Office-365-with-Windows-Server-Essentials.md)  
  
-   [Microsoft Online Services 관리](../manage/Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials 관리](../manage/Manage-Windows-Server-Essentials.md)
