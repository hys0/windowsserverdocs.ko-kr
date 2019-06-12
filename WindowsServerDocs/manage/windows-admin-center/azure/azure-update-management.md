---
title: Azure 업데이트 관리를 사용 하 여 운영 체제 업데이트 관리를 사용 하 여 Windows Admin Center
description: OS를 관리 하도록 Azure 업데이트 관리를 설정 하려면 Windows Admin Center (프로젝트 브라 티)을 사용 하 여 업데이트 합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 79b18e9963fba0993a7f34b1409edba6abfd48f0
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66452546"
---
# <a name="use-windows-admin-center-to-manage-operating-system-updates-with-azure-update-management"></a>Azure 업데이트 관리를 사용 하 여 운영 체제 업데이트 관리를 사용 하 여 Windows Admin Center

[Azure Windows Admin Center 통합에 대해 알아봅니다.](../plan/azure-integration-options.md)

Azure 업데이트 관리는 서버 단위로 아닌 한 곳에서 업데이트 및 여러 컴퓨터에 대 한 패치를 관리할 수 있도록 Azure Automation에서 솔루션입니다. Azure 업데이트 관리를 사용 하 여 신속 하 게 사용 가능한 업데이트의 상태를 평가, 필수 업데이트의 설치를 예약를 성공적으로 적용 되는 업데이트를 확인 하려면 배포 결과 검토 합니다. 이것이 가능 여부 컴퓨터는 Azure Vm을 다른 클라우드 공급자 또는 온-프레미스에서 호스트 합니다. [Azure 업데이트 관리에 대해 알아보기](https://docs.microsoft.com/azure/automation/automation-update-management)

Windows Admin Center 사용 하 여 설정 하 고 관리 되는 서버를 최신 상태로 유지 하려면 Azure 업데이트 관리를 사용 하 여 쉽게 수 있습니다. Azure 구독에서 Log Analytics 작업 영역이 없는 경우 Windows Admin Center 자동으로 서버를 구성 하 고 구독 및 지정 된 위치에 필요한 Azure 리소스 만들기. 기존 Log Analytics 작업 영역에 있는 경우 Windows Admin Center Azure 업데이트 관리에서 업데이트를 사용 하 여 서버를 자동으로 구성할 수 있습니다.  

시작 하려면 서버 연결에서 Updates tool로 이동 "설정 이제"를 선택 하 고 관련된 Azure 리소스에 대 한 기본 설정을 제공 합니다. 

Azure 업데이트 관리로 관리 되는 서버를 구성한 후에 업데이트 도구에서 제공 되는 하이퍼링크를 사용 하 여 Azure 업데이트 관리를 액세스할 수 있습니다. 

[Azure 업데이트 관리를 사용 하 여 서버를 업데이트를 중지 하는 방법에 알아봅니다.](azure-monitor.md#disabling-monitoring)

따라야 하는 참고 [Azure를 사용 하 여 Windows Admin Center 게이트웨이 등록](../configure/azure-integration.md) Azure 업데이트 관리를 설정 하기 전에 합니다.

