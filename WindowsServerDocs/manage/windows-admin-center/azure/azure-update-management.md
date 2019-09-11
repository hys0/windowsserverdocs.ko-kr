---
title: Windows 관리 센터를 사용 하 여 Azure 업데이트 관리로 운영 체제 업데이트 관리
description: Windows 관리 센터 (Project Honolulu)를 사용 하 여 OS 업데이트를 관리 하는 Azure 업데이트 관리를 설정 합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: ff67355697051a6c36a5143de96a6aec44bf35ca
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865423"
---
# <a name="use-windows-admin-center-to-manage-operating-system-updates-with-azure-update-management"></a>Windows 관리 센터를 사용 하 여 Azure 업데이트 관리로 운영 체제 업데이트 관리

[Windows 관리 센터와 Azure의 통합에 대해 자세히 알아보세요.](../plan/azure-integration-options.md)

Azure 업데이트 관리는 Azure Automation의 솔루션으로,이 솔루션을 사용 하 여 여러 컴퓨터에 대 한 업데이트 및 패치를 서버 별로 사용 하지 않고 단일 장소에서 관리할 수 있습니다. Azure 업데이트 관리를 사용하면 사용 가능한 업데이트의 상태를 신속하게 평가하고 필요한 업데이트 설치를 예약하며 배포 결과를 검토하여 업데이트가 성공적으로 적용되는지 확인할 수 있습니다. 이는 컴퓨터가 Azure Vm이 고 다른 클라우드 공급자에서 호스트 되거나 온-프레미스에 호스트 되는 경우에 발생할 수 있습니다. [Azure 업데이트 관리에 대해 자세히 알아보세요.](https://docs.microsoft.com/azure/automation/automation-update-management)

Windows 관리 센터를 사용 하면 쉽게 설정 하 고 Azure 업데이트 관리를 사용 하 여 관리 되는 서버를 최신 상태로 유지할 수 있습니다. Azure 구독에 Log Analytics 작업 영역이 아직 없는 경우 Windows 관리 센터에서 자동으로 서버를 구성 하 고 사용자가 지정한 구독 및 위치에서 필요한 Azure 리소스를 만듭니다. 기존 Log Analytics 작업 영역을 사용 하는 경우 Windows 관리 센터에서 Azure 업데이트 관리의 업데이트를 사용 하도록 서버를 자동으로 구성할 수 있습니다.  

시작 하려면 서버 연결의 업데이트 도구로 이동 하 여 "지금 설정"을 선택 하 고 관련 Azure 리소스에 대 한 기본 설정을 제공 합니다. 

Azure 업데이트 관리에서 관리 하도록 서버를 구성한 후에는 업데이트 도구에 제공 된 하이퍼링크를 사용 하 여 Azure 업데이트 관리에 액세스할 수 있습니다. 

[Azure 업데이트 관리 사용을 중지 하 여 서버를 업데이트 하는 방법을 알아봅니다.](azure-monitor.md#disabling-monitoring)

Azure 업데이트 관리를 설정 하기 전에 [azure에 Windows 관리 센터 게이트웨이를 등록](../configure/azure-integration.md) 해야 합니다.

