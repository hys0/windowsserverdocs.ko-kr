---
title: Windows Server Essentials에서 SharePoint Online 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 282f3634-6de6-4691-803c-df6c3c16660d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 92552d3beff58edfffe119d1490fefd646479775
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311087"
---
# <a name="manage-sharepoint-online-in-windows-server-essentials"></a>Windows Server Essentials에서 SharePoint Online 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Office 365을 Windows Server Essentials 서버와 통합 하는 경우 office 365에 로그인 하지 않고 대시보드에서 SharePoint Online 라이브러리 및 팀 사이트를 관리할 수 있습니다. 모든 Office 365 비즈니스 요금제를 사용 하 여 SharePoint Online 라이브러리 및 팀 사이트를 가져옵니다. [Office 365와 서버를 통합하는 방법 찾기](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
 사용자는 사용자가 My Server 2012 R2 앱을 사용 하 여 모바일 장치나 Windows phone을 사용 하 여 어디서 나 SharePoint Online 라이브러리의 파일에 액세스할 수 있습니다. [내 서버 앱을 어디에서 다운로드할 수 있나요?](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)  
  
 SharePoint를 아직 시도하지 않았나요? [지금 수행 가능한 작업](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)  
  
## <a name="where-on-the-dashboard-will-i-manage-my-libraries-and-team-sites"></a>대시보드의 어디에서 라이브러리 및 팀 사이트를 관리하나요?  
 Office 365를 서버와 통합할 때 대시보드의 **저장소** 영역에 추가 되는 새 **sharepoint online** 탭을 사용 하 여 sharepoint online 리소스를 관리 합니다.  

  
## <a name="what-can-i-manage-from-the-dashboard"></a>대시보드에서 무엇을 관리할 수 있나요?  
  
### <a name="manage-your-online-libraries"></a>온라인 라이브러리 관리  
   
|-|-|  
| 라이브러리 추가 | **SharePoint 라이브러리** 탭에서 **라이브러리 추가**를 사용 합니다. 일반적인 항목을 모두 선택할 수 있습니다.<br /><br /> -팀 사이트 및 라이브러리 유형을 선택 합니다.<br />-버전 제어를 사용할지 여부를 결정 합니다.<br />-액세스 권한을 할당 합니다.<br /><br /> **팁:** 사용 권한을 할당 하지 않은 경우 라이브러리가 상속할 팀 사이트 권한을 확인 하려면 **사이트 사용 권한 보기**를 사용 합니다. |  
| 라이브러리 열기 | 라이브러리의 콘텐츠를 사용 하려면 Office 365에서 해당 라이브러리를 열어야 합니다. 라이브러리를 선택하고 **라이브러리 열기**를 클릭합니다. 콘텐츠를 사용 하 여 수행할 수 있는 작업은 SharePoint Online에 로그인 하는 데 사용 하는 자격 증명에 따라 다릅니다. |  
| 버전 제어 또는 액세스 권한 변경 | **라이브러리 속성 보기** 를 사용 하 여 라이브러리에 대 한 버전 제어 또는 액세스 권한을 보거나 변경할 수 있습니다. |  
| 라이브러리 삭제 | **경고:** SharePoint Online 라이브러리를 삭제 하기 전에 다른 위치에 유지 하려는 모든 파일을 저장 해야 합니다. SharePoint에서 라이브러리를 삭제 하면 모든 항목이 영구적으로 삭제 됩니다. 내용을 검색할 방법이 없습니다.<br /><br /> 라이브러리가 나중에 필요한 항목을 저장 하 고 있지 않은지 확인 한 후 라이브러리를 선택 하 고 **라이브러리 삭제**를 클릭 합니다.  
  
### <a name="manage-your-team-sites"></a>팀 사이트 관리  
 
|-|-|  
| SharePoint 팀 사이트 관리 | **팀 사이트 관리** 작업을 사용 하면 Office 365에 로그인 하 여 SharePoint Online 팀 사이트를 관리할 수 있습니다. Office 365에서 수행할 수 있는 작업은 로그인 하는 온라인 계정에 따라 결정 됩니다.<br /><br /> Office 365를 닫고 대시보드로 돌아가면 **새로 고침** 을 클릭 하 여 변경 내용을 표시 합니다. | 팀 사이트 사용 권한 보기 또는 변경 | 라이브러리는 기본적으로 팀 사이트에서 사용 권한을 상속 하므로 팀 사이트에 쉽게 액세스 하는 데 도움이 됩니다. 팀 사이트에 대 한 사용 권한을 보거나 변경 하려면 팀 사이트 또는 해당 라이브러리를 선택 하 고 **사이트 사용 권한 보기**를 클릭 합니다.<br /><br /> **팁:** SharePoint 팀 사이트 사용 권한 문제에 대 한 도움이 필요 하세요? 팀 사이트 사용 권한에는 유용한 [자세한 정보](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924) 링크가 있습니다.  
  
## <a name="tips"></a>팁  
  
-   **Office 365 포털의 최신 변경 내용을 보려면 새로 고침을 클릭 합니다.** SharePoint Online을 관리 하려면 Office 365를 연 후 디스플레이를 새로 고쳐야 합니다. 대시보드를 오랫동안 열어 두었으면 **새로 고침**을 클릭하여 최신 변경 내용이 표시되는지 확인합니다.  
  
-   **SharePoint Online에서 수행할 수 있는 작업은 대시보드 또는 Office 365에서 작업 하 고 있는지 여부에 따라 달라 집니다.** 대시보드에서 SharePoint Online 변경 내용은 Office 365 통합에 대 한 관리자 계정을 사용 하 여 수행 됩니다. 그러나 대시보드에서 Office 365에 로그인 하면 사용 하는 온라인 계정에 대 한 액세스 권한에 따라 수행할 수 있는 작업이 결정 됩니다.  
  
     Office 365 통합에 대 한 관리자 계정을 찾으려면 대시보드에서 **office 365** 탭을 엽니다.  
  
## <a name="other-things-you-might-want-to-do"></a>수행할 수 있는 기타 작업  
  
-   [내 서버 앱을 사용 하 여 어디서 나 SharePoint Online 라이브러리 작업](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)  
  
-   [SharePoint 팀 사이트에 대 한 사용 권한 할당에 대 한 자세한 정보](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924)  
  
-   [SharePoint 기능으로 수행할 수 있는 작업 확인](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)  
  
-   [사용할 수 있는 Office 365 비즈니스 계획 살펴보기](https://office.microsoft.com/business/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_what-is-office-365-for_Text)  
  
-   [서버와 Office 365 통합](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [대시보드에서 다른 Microsoft 온라인 서비스 관리](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
