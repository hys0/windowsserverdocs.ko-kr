---
title: Azure 업데이트 관리를 사용 하 여 운영 체제 업데이트 관리를 사용 하 여 Windows Admin Center
description: OS를 관리 하도록 Azure 업데이트 관리를 설정 하려면 사용 하 여 Windows Admin Center (Project Honolulu)를 업데이트 합니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 07/17/2018
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 5ba81968f8baa81176ad646fb2a97961ddc49fda
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296990"
---
# Azure 업데이트 관리를 사용 하 여 운영 체제 업데이트 관리를 사용 하 여 Windows Admin Center

[Windows Admin Center와 Azure를 통합하는 방법에 대해 알아보세요.](../plan/azure-integration-options.md)

Azure 업데이트 관리 서버 단위로 아니라 단일 위치에서 업데이트 및 여러 컴퓨터에 대 한 패치를 관리할 수 있도록 Azure 자동화에서 솔루션입니다. Azure 업데이트 관리를 신속 하 게 사용 가능한 업데이트의 상태를 평가, 필요한 업데이트의 설치를 예약 하 고 사용할 수 성공적으로 적용 되는 업데이트를 확인 하려면 배포 결과 검토 합니다. 가능한 컴퓨터 Azure Vm에서 온-프레미스 또는 다른 클라우드 공급자에서 호스팅되는 있는지 여부입니다. [Azure 업데이트 관리에 대해 알아봅니다.](https://docs.microsoft.com/azure/automation/automation-update-management)

Windows Admin Center로 설정 하 고 관리 되는 서버를 최신 상태로 유지 하려면 Azure 업데이트 관리를 사용 하 여 쉽게 수 있습니다. Azure 구독에서 Log Analytics 작업 영역 없는 경우 Windows Admin Center 자동으로 서버를 구성 하 고 구독 및 사용자가 지정한 위치에 필요한 Azure 리소스를 만듭니다. 기존 Log Analytics 작업 영역에 있는 경우 Windows Admin Center Azure 업데이트 관리에서 업데이트를 사용 하 여 서버를 자동으로 구성할 수 있습니다.  

시작 하려면 서버 연결에서 업데이트 도구 이동 "지금 설정"을 선택 하 고 관련된 Azure 리소스에 대 한 기본 설정을 제공 합니다. 

Azure 업데이트 관리에서 관리할 서버를 구성한 후 업데이트 도구에 있는 하이퍼링크를 사용 하 여 Azure 업데이트 관리를 액세스할 수 있습니다. 

[Azure 업데이트 관리를 사용 하 여 서버에 업데이트를 중지 하는 방법을 알아봅니다.](azure-monitor.md#disabling-monitoring)

Note Azure 업데이트 관리를 설정 하기 전에 [Azure 사용 하 여 Windows Admin Center 게이트웨이 등록](..\configure\azure-integration.md) 을 해야 합니다.

