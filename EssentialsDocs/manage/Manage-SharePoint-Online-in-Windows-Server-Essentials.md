---
title: Windows Server Essentials에서 SharePoint Online 관리
description: Windows Server Essentials를 사용 하는 방법을 설명 합니다.
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 282f3634-6de6-4691-803c-df6c3c16660d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b9b12c138e6166684b4b9e87b794444febd3c247
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830384"
---
# <a name="manage-sharepoint-online-in-windows-server-essentials"></a>Windows Server Essentials에서 SharePoint Online 관리

>적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Windows Server Essentials 서버를 사용 하 여 Office 365를 통합 하는 경우 Office 365에 로그인 하지 않고도 대시보드에서 SharePoint Online 라이브러리 및 팀 사이트를 관리할 수 있습니다. SharePoint Online 라이브러리 및 모든 Office 365 비즈니스 계획을 사용 하 여 팀 사이트를 얻습니다. [Office 365와 서버를 통합하는 방법 찾기](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
 게다가 사용자에 게 My Server 2012 R2 앱을 사용 하 여 어디서 나 모바일 장치나 Windows phone을 사용 하 여 SharePoint Online 라이브러리의 파일에 액세스할 수 있습니다. [내 서버 앱을 어디에서 다운로드할 수 있나요?](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)  
  
 SharePoint를 아직 시도하지 않았나요? [지금 수행 가능한 작업](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)  
  
## <a name="where-on-the-dashboard-will-i-manage-my-libraries-and-team-sites"></a>대시보드의 어디에서 라이브러리 및 팀 사이트를 관리하나요?  
 사용 하 여 새 **SharePoint Online** 탭에 추가 되는 **저장소** Office 365 SharePoint Online 리소스를 관리 하는 서버와 통합할 때 대시보드의 영역입니다.  

  
## <a name="what-can-i-manage-from-the-dashboard"></a>대시보드에서 무엇을 관리할 수 있나요?  
  
### <a name="manage-your-online-libraries"></a>온라인 라이브러리 관리  
   
|-|-|  
| 라이브러리 추가 | 에 **SharePoint 라이브러리** 탭을 사용 하 여 **라이브러리 추가**합니다. 일반적인 항목을 모두 선택할 수 있습니다.<br /><br /> -팀 사이트와 라이브러리 유형을 선택 합니다.<br />-버전 제어를 사용할지 여부를 결정 합니다.<br />-액세스 권한을 할당 합니다.<br /><br /> **팁:** 사용 권한을 할당 하지 않을 경우 라이브러리가 상속 하는 어떤 팀 사이트 사용 권한에 찾으려면 **사이트 사용 권한 보기**. |  
| 라이브러리 열기 | 라이브러리의 콘텐츠를 사용 하려면 Office 365에서 열려는 해야 합니다. 라이브러리를 선택하고 **라이브러리 열기**를 클릭합니다. SharePoint Online에 로그인 하는 데 사용 하는 자격 증명에 따라 달라 집니다 콘텐츠를 사용 하 여 수행할 수 있습니다. |  
| 버전 제어 변경 하거나 액세스 권한을 | 사용할 수 있습니다 **라이브러리 속성 보기** 보기 또는 버전 제어 변경 하거나 라이브러리에 대 한 권한을 액세스 합니다. |  
| 라이브러리 삭제 | **경고:** SharePoint Online 라이브러리를 삭제하기 전에 다른 위치에 유지하려는 파일을 저장해야 합니다. SharePoint에서 라이브러리를 삭제 하면 모든 항목이 영구적으로 삭제 됩니다. 내용을 검색할 방법이 없습니다.<br /><br /> 나중에 필요할 수 있는 어떤 내용도 라이브러리에 저장 되지 않습니다 있도록를 선택한 후 라이브러리를 선택 하 고 클릭 **라이브러리 삭제**. |  
  
### <a name="manage-your-team-sites"></a>팀 사이트 관리  
 
|-|-|  
| SharePoint 팀 사이트 관리 | 합니다 **팀 사이트 관리** 작업을 통해 Office 365에 로그인 하 고 SharePoint Online 팀 사이트를 관리할 수 있습니다. 수행할 수 있는 Office 365에서 로그인 하는 온라인 계정에 따라 결정 됩니다.<br /><br /> Office 365를 닫고 대시보드로 돌아가면 때 클릭 **새로 고침** 변경 내용을 표시 합니다. | 팀 사이트 사용 권한을 보거나 변경 | 기본적으로 팀 사이트에서 사용 권한을 상속 하는 라이브러리, 이후 팀 사이트에 쉽게 액세스할 수 있도록 유용 합니다. 을 확인 하거나 팀 사이트에 대 한 사용 권한을 변경 하려면 팀 사이트 또는 해당 라이브러리를 선택 하 고 클릭 **사이트 사용 권한 보기**합니다.<br /><br /> **팁:** SharePoint 팀 사이트 사용 권한에 대한 자세한 도움말이 필요합니까? 팀 사이트 사용 권한에는 유용한 [자세한 정보](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924) 링크가 있습니다.  
  
## <a name="tips"></a>팁  
  
-   **Office 365 포털에서 변경한 최신 사항을 표시 하려면 새로 고침을 클릭 합니다.** Office 365 SharePoint Online 관리를 연 후에 표시를 새로 고칩니다 해야 합니다. 대시보드를 오랫동안 열어 두었으면 **새로 고침**을 클릭하여 최신 변경 내용이 표시되는지 확인합니다.  
  
-   **SharePoint Online에서 수행할 수 있는 작업 하는 작업은 대시보드 또는 Office 365에서 작업 하는지에 따라 달라 집니다.** 대시보드에서 SharePoint Online 변경 내용이 Office 365 통합에 대 한 관리자 계정을 사용 합니다. 하지만 사용 하는 온라인 계정에 대 한 액세스 권한에 따라 수행할 수 있는 작업을 결정 대시보드에서 Office 365에 로그인 할 때.  
  
     Office 365 통합에 대 한 관리자 계정을 알아보려면 엽니다는 **Office 365** 대시보드에서 탭 합니다.  
  
## <a name="other-things-you-might-want-to-do"></a>수행할 수 있는 기타 작업  
  
-   [My Server 앱을 사용 하 여 어디에서 나 SharePoint Online 라이브러리를 사용 하려면](../use/Use-the-My-Server-App-to-Connect-to-Windows-Server-Essentials.md)  
  
-   [SharePoint 팀 사이트에 대 한 사용 권한을 할당 하는 방법에 대 한 자세한 정보](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/introduction-control-user-access-with-permissions-HA102771919.aspx?CTT=5&origin=HA102771924)  
  
-   [SharePoint 기능을 사용 하 여 수행할 수 있는 작업 확인](https://office.microsoft.com/office365-sharepoint-online-enterprise-help/get-started-with-sharepoint-2013-HA102772778.aspx)  
  
-   [사용할 수 있는 Office 365 비즈니스 계획 살펴봅니다](https://office.microsoft.com/business/compare-office-365-for-business-plans-FX102918419.aspx?CR_CC=200061904&WT.srch=1&WT.mc_ID=PS_bing_O365Comm_what-is-office-365-for_Text)  
  
-   [서버를 사용 하 여 Office 365 통합](Manage-Office-365-in-Windows-Server-Essentials.md)  
  
-   [대시보드에서 기타 Microsoft online services 관리](Manage-Microsoft-Online-Services-in-Windows-Server-Essentials.md)
