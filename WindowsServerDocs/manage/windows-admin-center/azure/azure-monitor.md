---
title: Windows 관리 센터에서 서버를 모니터링 하 고 Azure Monitor를 사용 하 여 경고 구성
description: Windows 관리 센터 (Project Honolulu)는 Azure Monitor와 통합 됩니다.
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 03/24/2019
ms.openlocfilehash: 28108a79bbdc654f6437a698c158a3f74d4423ba
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371131"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>Windows 관리 센터에서 서버를 모니터링 하 고 Azure Monitor를 사용 하 여 경고 구성

[Windows 관리 센터와 Azure의 통합에 대해 자세히 알아보세요.](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) 은 온-프레미스와 클라우드 모두에서 Windows 서버 및 vm을 비롯 한 다양 한 리소스에서 원격 분석을 수집 하 고 분석 하 고 작동 하는 솔루션입니다. Azure Monitor는 Azure Vm 및 기타 Azure 리소스에서 데이터를 끌어올 것 이지만,이 문서에서는 Azure Monitor Windows 관리 센터에서 온-프레미스 서버와 Vm을 사용 하는 방법을 집중적으로 설명 합니다. Azure Monitor를 사용 하 여 하이퍼 수렴 형 클러스터에 대 한 전자 메일 경고를 가져오는 방법에 대 한 자세한 내용은 [Azure Monitor를 사용 하 여 상태 관리 서비스 오류에 대](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor)한 전자 메일 보내기를 참조 하세요.

## <a name="how-does-azure-monitor-work"></a>Azure Monitor 작동 방법
온-프레미스 Windows 서버에서 생성 된 img](../media/azure-monitor-diagram.png) 데이터 ![Azure Monitor의 Log Analytics 작업 영역에서 수집 됩니다. 작업 영역 내에서 특정 시나리오에 대 한 정보를 제공 하는 논리 집합 등 다양 한 모니터링 솔루션을 사용 하도록 설정할 수 있습니다. 예를 들어 Azure 업데이트 관리, Azure Security Center 및 VM용 Azure Monitor는 작업 영역 내에서 사용할 수 있는 모든 모니터링 솔루션입니다. 

Log Analytics 작업 영역에서 모니터링 솔루션을 사용 하도록 설정 하면 해당 작업 영역에 보고 하는 모든 서버에서 해당 솔루션과 관련 된 데이터를 수집 하기 시작 하므로 솔루션이 작업 영역에 있는 모든 서버에 대 한 정보를 생성할 수 있습니다. 

온-프레미스 서버에서 원격 분석 데이터를 수집 하 고 Log Analytics 작업 영역에 푸시 하려면 Microsoft Monitoring Agent 또는 MMA를 설치 해야 Azure Monitor. 또한 특정 모니터링 솔루션에는 보조 에이전트가 필요 합니다. 예를 들어 VM용 Azure Monitor는이 솔루션에서 제공 하는 추가 기능에 대해 ServiceMap 에이전트에 따라서도 달라 집니다. 

Azure 업데이트 관리와 같은 일부 솔루션은 Azure 및 비 Azure 환경에서 리소스를 중앙에서 관리할 수 있는 Azure Automation에도 종속 됩니다. 예를 들어 Azure 업데이트 관리는 Azure Automation를 사용 하 여 사용자 환경의 컴퓨터에 대 한 업데이트 설치를 예약 하 고 Azure Portal에서 중앙 집중식으로 오케스트레이션 합니다.


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>Windows 관리 센터에서 Azure Monitor를 사용 하도록 설정 하는 방법

WAC 내에서 다음과 같은 두 가지 모니터링 솔루션을 사용 하도록 설정할 수 있습니다.

- [Azure 업데이트 관리](azure-update-management.md) (업데이트 도구)
- VM용 Azure Monitor (서버 설정),. k Virtual Machines insights

이러한 도구 중 하나에서 Azure Monitor를 사용 하 여 시작할 수 있습니다. 이전에 Azure Monitor을 사용한 적이 없는 경우 WAC는 Log Analytics 작업 영역 (및 필요한 경우 Azure Automation 계정)을 자동으로 프로 비전 하 고 대상 서버에 Microsoft Monitoring Agent (MMA)를 설치 하 고 구성 합니다. 그런 다음 해당 솔루션을 작업 영역에 설치 합니다. 

예를 들어, 먼저 업데이트 도구로 이동 하 여 Azure 업데이트 관리를 설정 하는 경우 WAC는 다음을 수행 합니다.

1. 컴퓨터에 MMA 설치
2. 이 경우 Azure Automation 계정이 필요 하므로 Log Analytics 작업 영역 및 Azure Automation 계정 만들기
3. 새로 만든 작업 영역에 업데이트 관리 솔루션을 설치 합니다.

WAC 내에서 동일한 서버의 다른 모니터링 솔루션을 추가 하려는 경우 WAC는 해당 서버가 연결 된 기존 작업 영역에 해당 솔루션을 설치 하기만 하면 됩니다. WAC는 추가로 필요한 에이전트를 추가로 설치 합니다.

다른 서버에 연결 하지만 이미 Log Analytics 작업 영역을 설정 하는 경우 (예를 들어 WAC 또는 Azure Portal에서 수동으로) 서버에 MMA 에이전트를 설치 하 고 기존 작업 영역에 연결할 수도 있습니다. 서버를 작업 영역에 연결 하면 자동으로 데이터 수집을 시작 하 고 해당 작업 영역에 설치 된 솔루션에 대 한 보고를 시작 합니다.

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>가상 컴퓨터에 대 한 Azure Monitor ( Virtual Machine insights)
>적용 대상: Windows 관리 센터 미리 보기

서버 설정에서 VM용 Azure Monitor를 설정 하는 경우 Windows 관리 센터에서 Virtual Machine insights 라고도 하는 VM용 Azure Monitor 솔루션을 사용 하도록 설정 합니다. 이 솔루션을 사용 하면 서버 상태 및 이벤트를 모니터링 하 고, 메일 경고를 만들고, 사용자 환경에서 서버 성능에 대 한 통합 보기를 가져오고, 지정 된 서버에 연결 된 앱, 시스템 및 서비스를 시각화할 수 있습니다.

> [!NOTE]
> VM insights는 이름에도 불구 하 고 물리적 서버와 가상 컴퓨터에도 작동 합니다.

Azure Monitor의 무료 5gb 데이터/월/고객 허용 기간을 사용 하면 요금을 지불 하지 않아도 서버 또는 2에 대해이를 쉽게 수행할 수 있습니다. 사용자 환경의 서버에서 시스템 성능에 대 한 통합 보기를 제공 하는 것과 같이 Azure Monitor에 서버를 온 보 딩 하는 추가 혜택을 확인 하세요.

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Azure Monitor와 함께 사용할 서버 설정**

서버 연결의 개요 페이지에서 새로 만들기 단추 "경고 관리"를 클릭 하거나 서버 설정 > 모니터링 및 경고로 이동 합니다. 이 페이지에서 "설정"을 클릭 하 고 설정 창을 완료 하 여 Azure Monitor에 서버를 등록 합니다. 관리 센터는 Azure Log Analytics 작업 영역을 프로 비전 하 고, 필요한 에이전트를 설치 하 고, VM insights 솔루션을 구성 하는 작업을 담당 합니다. 완료 되 면 서버는 Azure Monitor에 성능 카운터 데이터를 전송 하 여 Azure Portal에서이 서버를 기반으로 전자 메일 경고를 보고 만들 수 있습니다.

### <a name="create-email-alerts"></a>**전자 메일 알림 만들기**

서버를 Azure Monitor 연결 하면 설정 > 모니터링 및 경고 페이지에서 지능형 하이퍼링크를 사용 하 여 Azure Portal로 이동할 수 있습니다. 관리 센터는 성능 카운터를 자동으로 수집할 수 있도록 하므로 미리 정의 된 많은 쿼리 중 하나를 사용자 지정 하거나 직접 작성 하 여 [새 경고를 쉽게 만들](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log) 수 있습니다.

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>\* * 여러 서버에서 통합 보기 가져오기 * *

Azure Monitor 내에서 단일 Log Analytics 작업 영역에 여러 서버를 등록 하는 경우 Azure Monitor 내에서 [Virtual Machines Insights 솔루션](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) 의 모든 서버에 대 한 통합 보기를 가져올 수 있습니다.  Azure Monitor에 대 한 Virtual Machines Insights의 성능 및 맵 탭만 온-프레미스 서버에서 작동 하며, 상태 탭은 Azure Vm 에서만 작동 합니다. Azure Portal에서이를 보려면 Azure Monitor > Virtual Machines (정보)로 이동 하 여 "성능" 또는 "맵" 탭으로 이동 합니다.

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**지정 된 서버에 연결 된 앱, 시스템 및 서비스 시각화**

관리 센터에서 서버를 Azure Monitor 내에서 VM insights 솔루션으로 보드 아웃 하면 [서비스 맵](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)이라는 기능이 켜 집니다. 이 기능은 응용 프로그램 구성 요소를 자동으로 검색 하 고 서비스 간 통신을 매핑하여 Azure Portal에서 매우 자세한 정보를 가진 서버 간의 연결을 쉽게 시각화할 수 있습니다. Azure Portal > Azure Monitor > Virtual Machines (정보)로 이동 하 고 "Maps" 탭으로 이동 하 여 찾을 수 있습니다.

> [!NOTE]
> Azure Monitor에 대 한 Virtual Machines Insights에 대 한 시각화는 현재 6 개의 공용 지역에 제공 됩니다.  최신 정보는 [VM용 Azure Monitor 설명서](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics)를 확인 하세요.  위에서 설명한 Virtual Machines Insights 솔루션에서 제공 하는 추가 혜택을 얻으려면 지원 되는 지역 중 하나에 Log Analytics 작업 영역을 배포 해야 합니다.

## <a name="disabling-monitoring"></a>모니터링 사용 안 함

Log Analytics 작업 영역에서 서버를 완전히 분리 하려면 MMA 에이전트를 제거 합니다. 즉,이 서버는 더 이상 작업 영역에 데이터를 전송 하지 않으며 해당 작업 영역에 설치 된 모든 솔루션이 더 이상 해당 서버에서 데이터를 수집 및 처리 하지 않습니다. 그러나 작업 영역 자체에는 영향을 주지 않습니다 .이 작업 영역에 보고 하는 모든 리소스는이 작업을 계속 수행 합니다. WAC 내에서 MMA agent를 제거 하려면 앱 & 기능으로 이동 하 Microsoft Monitoring Agent를 찾은 다음 제거를 클릭 합니다.

작업 영역 내에서 특정 솔루션을 해제 하려면 [Azure Portal에서 모니터링 솔루션을 제거](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)해야 합니다. 모니터링 솔루션을 제거 하면 해당 솔루션에 의해 생성 된 정보는 해당 작업 영역에 보고 하는 _모든_ 서버에 대해 더 이상 생성 되지 않습니다. 예를 들어 VM용 Azure Monitor 솔루션을 제거 하면 내 작업 영역에 연결 된 컴퓨터에서 VM 또는 서버 성능에 대 한 정보가 더 이상 표시 되지 않습니다.