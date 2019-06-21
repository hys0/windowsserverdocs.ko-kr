---
title: 서버를 모니터링 하 고 Windows Admin Center Azure Monitor를 사용 하 여 경고를 구성 합니다.
description: Azure Monitor와 통합 되어 Windows Admin Center (프로젝트 브라 티)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/24/2019
ms.openlocfilehash: 8f7baba465071cc95ab7492037ff25c5cd58219e
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280431"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>서버를 모니터링 하 고 Windows Admin Center Azure Monitor를 사용 하 여 경고를 구성 합니다.

[Azure Windows Admin Center 통합에 대해 알아봅니다.](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview) 는 솔루션 수집, 분석 및 다양 한 Windows 서버 및 Vm, 온-프레미스를 비롯 한 리소스를 클라우드에서 로부터 원격 분석 데이터는 역할입니다. Azure Monitor는 Azure Vm 및 기타 Azure 리소스에서 데이터를 끌어오고, 하지만이 문서에서는 온-프레미스 서버 및 특히 Windows Admin Center 사용 하 여 Vm을 사용 하 여 Azure Monitor의 작동 원리에 중점을 둡니다. 하이퍼 수렴 형 클러스터에 대 한 전자 메일 경고를 보려면 Azure Monitor를 사용 하는 방법을 알아보려면 싶다면 읽어보세요 [상태 서비스 오류에 대 한 전자 메일을 보내도록 Azure Monitor를 사용 하 여](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor)입니다.

## <a name="how-does-azure-monitor-work"></a>Azure Monitor는 어떻게 작동 하나요?
![img](../media/azure-monitor-diagram.png) 온-프레미스 Windows 서버에서 생성 된 데이터는 Azure Monitor에서 Log Analytics 작업 영역에서 수집 됩니다. 작업 영역 내에서 다양 한 모니터링 솔루션을 설정할 수 있습니다.-특정 시나리오에 대 한 통찰력을 제공 하는 논리를 설정 합니다. 예를 들어 Azure 업데이트 관리, Azure Security Center에서 Vm에 대 한 Azure Monitor와 작업 영역 내에서 사용할 수 있는 모든 모니터링 솔루션입니다. 

Log Analytics 작업 영역에서 모니터링 솔루션을 사용 하도록 설정 하면 보고 하는 모든 서버 작업 영역을 데이터 수집을 시작 해당 솔루션에 관련 솔루션 작업 영역에서 모든 서버에 대 한 정보를 생성할 수 있도록 합니다. 

온-프레미스 서버에서 원격 분석 데이터를 수집 하 고 Log Analytics 작업 영역에 푸시를 Azure Monitor 하려면 Microsoft 모니터링 에이전트 나 MMA를 설치 합니다. 특정 모니터링 솔루션에는 또한 보조는 에이전트가 필요합니다. 예를 들어, Vm에 대 한 Azure Monitor는 또한이 솔루션을 제공 하는 추가 기능에 대 한은 ServiceMap 에이전트에 따라 다릅니다. 

Azure 업데이트 관리와 같은 일부 솔루션도 Azure 및 비 Azure 환경에서 리소스를 중앙에서 관리할 수 있도록 하는 Azure Automation에 따라 달라 집니다. 예를 들어 Azure 업데이트 관리를 사용 하 여 Azure Automation 예약 하 고 Azure portal에서 중앙에서 다중 컴퓨터 환경에서 업데이트 설치를 오케스트레이션 합니다.


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>Windows Admin Center 사용 하려면 어떻게 Azure Monitor를 사용 하 여?

WAC, 내에서 두 가지 모니터링 솔루션 설정할 수 있습니다.

- [Azure 업데이트 관리](azure-update-management.md) (에서 업데이트 도구)
- Vm (server 설정)에 대 한 azure Monitor, 또는 가상 머신 정보

이러한 도구 중 하나에서 Azure Monitor를 사용 하 여 시작할 수 있습니다. Log Analytics 작업 영역 (및 Azure Automation 계정에 필요한 경우) WAC는 자동으로 프로 비전 하기 전에 Azure Monitor를 사용한 경험이 없는 경우 대상 서버에서 Microsoft Monitoring Agent (MMA)을 구성 합니다. 그런 다음 해당 솔루션이 작업 영역에 설치 됩니다. 

예를 들어, 먼저 Azure 업데이트 관리를 설정 하려면 Updates tool로 이동 하면 WAC 됩니다.

1. 컴퓨터에 MMA를 설치 합니다.
2. (Azure Automation 계정을 해야 있으므로 예제의) Log Analytics 작업 영역 및 Azure Automation 계정 만들기
3. 새로 만든된 작업 영역에서 업데이트 관리 솔루션을 설치 합니다.

WAC 내 다른 모니터링 솔루션에서 동일한 서버에 추가 하려는 경우 WAC는 해당 서버를 연결할 기존 작업 영역에 해당 솔루션을 설치 하기만 하면 됩니다. WAC는 또한 다른 필요한 에이전트를 설치 하 고 합니다.

다른 서버에 연결 해도 설치 (또는 WAC를 통해 수동으로 Azure Portal에서) Log Analytics 작업 영역에 이미 있는 경우 서버에 MMA 에이전트를 설치 수 및 기존 작업 영역을 대상에 연결 해야 합니다. 서버 작업 영역에 연결 하면 자동으로 데이터를 수집 하 고 해당 작업 영역에 설치 된 솔루션이 보고를 시작 합니다.

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>Azure 가상 컴퓨터 (즉,에 대 한 모니터링 가상 머신 insights)
>적용 대상: Windows Admin Center 미리 보기

Azure Monitor에 대해 설정한 Vm 서버 설정에서에서 가상 머신 insights 라고도 Vm 솔루션에 대 한 Azure Monitor Windows Admin Center 수 있습니다. 이 솔루션을 사용 하면 서버 상태 및 이벤트를 모니터링, 전자 메일 경고를 생성, 사용자 환경 전체의 서버 성능의 통합된 보기를 확인 및 앱, 시스템 및 지정된 된 서버에 연결 된 서비스를 시각화할 수 있습니다.

> [!NOTE]
> 이름과 달리 가상 컴퓨터 뿐만 아니라 실제 서버에 대 한 VM insights 작동 합니다.

Azure monitor의 데이터/월/고객 허용량 5GB 무료, 쉽게에서 사용할 수 있는이 서버 또는 요금 부과 걱정 없이 두 가지입니다. Azure Monitor에 참조 추가 혜택 온 보 딩 서버에 서버 환경에 걸쳐 통합된 시스템 성능 보기 시작 등 읽습니다.

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Azure Monitor 사용에 대 한 서버 설정**

서버 연결의 개요 페이지에서 새 "관리 경고" 단추를 클릭 하거나 서버 설정으로 이동 > 모니터링 및 경고 합니다. 이 페이지 내에서 등록을 클릭 하 여 Azure Monitor에 서버 "설정" 설정 창을 완료 합니다. 관리 센터 Azure Log Analytics 작업 영역을 프로 비전 필요한 에이전트를 설치 하 고 구성 된 VM insights 솔루션을 확인 합니다. 완료 되 면 서버 성능 카운터 데이터를 보냅니다 Azure Monitor를 살펴보고 Azure portal에서이 서버에 따라 전자 메일 경고를 만들 수 있습니다.

### <a name="create-email-alerts"></a>**전자 메일 경고 만들기**

Azure Monitor로 서버에 연결한 후 지능형 하이퍼링크 설정 내에서 사용할 수 있습니다 > 모니터링 및 경고 페이지에서 Azure Portal로 이동 합니다. 관리 센터는 자동으로 수집 하는 성능 카운터를 사용 하므로 쉽게 보관할 수 있습니다 [새 경고 만들기](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log) 많은 미리 정의 된 쿼리 중 하나를 사용자 지정 또는 자신의 코드를 작성 합니다.

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>\* * 여러 서버에 걸쳐 통합된 보기를 확인 합니다. * *

경우 있습니다 온 보 딩 Azure 모니터 내에서 단일 Log Analytics 작업 영역에 여러 서버에 가져올 수 있습니다 이러한 모든 서버에서의 통합된 보기를 [Virtual Machines Insights 솔루션](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) Azure 모니터 내에서.  (Azure Monitor에 대 한 Virtual Machines Insights의 성능 및 Maps 탭 온-프레미스 서버-Azure Vm에만 상태 탭 함수를 사용 하 여 작동는 note). 이 항목을 보려면 Azure portal에서, Azure Monitor로 이동 > (Insights)에서 가상 컴퓨터는 "Performance" 또는 "지도" 탭으로 이동 합니다.

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**앱, 시스템 및 지정된 된 서버에 연결 된 서비스를 시각화 합니다.**

경우 관리 센터 등록 서버를 Azure Monitor 내 VM insights 솔루션으로, 고도 단계인 이라는 기능 [서비스 맵](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)합니다. 이 기능은 자동으로 응용 프로그램 구성 요소를 검색 하 고 Azure portal에서 유용한 정보를 사용 하 여 서버 간 연결을 쉽게 시각화할 수 있도록 서비스 간에 통신을 매핑합니다. Azure portal로 이동 하 여이 찾을 수 있습니다 > Azure Monitor > Virtual Machines (아래 Insights) 및 "지도" 탭으로 이동 합니다.

> [!NOTE]
> Azure Monitor에 대 한 Virtual Machines Insights에 대 한 시각화는 현재 6 개 공용 지역에서 제공 됩니다.  최신 정보를 확인 합니다 [Vm 설명서에 대 한 Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics)합니다.  위에서 설명한 Virtual Machines Insights 솔루션을 제공한 추가 혜택 얻기에 대 한 지원 되는 지역 중 하나에서 Log Analytics 작업 영역을 배포 해야 합니다.

## <a name="disabling-monitoring"></a>모니터링을 사용 하지 않도록 설정

완전히 서버를 Log Analytics 작업 영역에서 연결을 끊으려면 MMA 에이전트를 제거 합니다. 즉,이 서버는 더 이상 데이터 보내기 작업 영역에서 해당 작업 영역에 설치 하는 솔루션은 더 이상 모든 수집 하 고 해당 서버에서 데이터를 처리 합니다. 그러나 작업 영역 자체-이렇게 하려면 해당 작업 영역에 보고 하는 리소스를 계속 모든 적용 되지 않습니다. WAC 내 MMA 에이전트를 제거 하려면 Microsoft Monitoring Agent 찾아 제거를 클릭 하 고 앱 및 기능을 이동 합니다.

작업 영역 내에서 특정 솔루션을 해제 하려는 경우 해야 [Azure portal에서 모니터링 솔루션을 제거](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)합니다. 모니터링 솔루션을 제거 하는 솔루션에서 만든 정보를 더 이상 자동으로 생성 됩니다 의미 _모든_ 해당 작업 영역에 보고 서버입니다. 예를 들어, Vm 솔루션에 대 한 Azure Monitor를 제거 합니까는 더 이상 보이지 내 작업 영역에 연결 된 컴퓨터 중 하나에서 VM 또는 서버 성능에 대 한 정보.