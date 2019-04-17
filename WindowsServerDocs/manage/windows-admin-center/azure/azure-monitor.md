---
title: 서버를 모니터링 하 고 Windows 관리 센터에서 Azure 모니터를 사용 하 여 알림 구성
description: Azure 모니터와 통합 되는 Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/24/2019
ms.openlocfilehash: 6ada708bf7dd8cd08e1bc2620be5244a07beac7d
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297020"
---
# 서버를 모니터링 하 고 Windows 관리 센터에서 Azure 모니터를 사용 하 여 알림 구성

[Windows Admin Center와 Azure를 통합하는 방법에 대해 알아보세요.](../plan/azure-integration-options.md)

[Azure 모니터](https://docs.microsoft.com/azure/azure-monitor/overview) 수집를 분석 하 고 다양 한 리소스를 포함 하 여 Windows 서버와 Vm을 모두 온-프레미스와 클라우드에서 원격 분석에는 솔루션입니다. 하지만 Azure 모니터 Azure Vm 및 기타 Azure 리소스에서 데이터를 가져오고,이 문서에서는 온-프레미스 서버 및 Windows Admin Center를 사용 하 여 특히 Vm을 사용 하 여 Azure 모니터 작동 방식에 중점을 둡니다. 하이퍼 수렴 형 클러스터에 대 한 전자 메일 경고를 보려면 Azure 모니터를 사용 하는 방법을 알아보려면 관심이 있다면 [상태 서비스 오류에 대 한 전자 메일을 보낼 Azure 모니터를 사용 하 여](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor)살펴보세요.

## Azure 모니터는 어떻게 작동 합니까?
![img](../media/azure-monitor-diagram.png) Azure 모니터에서 Log Analytics 작업 영역에 온-프레미스 Windows Server에서 생성 된 데이터를 수집 합니다. 작업 영역 내에서 다양 한 모니터링 솔루션을 사용 하면-특정 시나리오에 대 한 정보를 제공 하는 논리를 설정 합니다. 예를 들어, Azure 업데이트 관리, Azure Security Center 및 Vm에 대 한 Azure 모니터는 작업 영역 내에서 사용할 수 있는 모든 모니터링 솔루션입니다. 

관련 된 데이터를 수집 하기 시작 Log Analytics 작업 영역에서 모니터링 솔루션을 사용 하면 해당 작업 영역에 보고 하는 모든 서버 솔루션 솔루션 작업 영역에서 모든 서버에 대 한 정보를 생성할 수 있도록 합니다. 

온-프레미스 서버에서 원격 분석 데이터를 수집 Log Analytics 작업 영역에 푸시 하려면, Azure 모니터 필요 Microsoft Monitoring Agent 또는 MMA를 설치 합니다. 또한 특정 모니터링 솔루션과 보조 에이전트를 필요합니다. 예를 들어, Vm에 대 한 Azure 모니터가이 솔루션을 제공 하는 추가 기능에 대 한 ServiceMap 에이전트에 따라 다릅니다. 

또한 Azure 업데이트 관리와 같은 일부 솔루션 Azure 및 비 Azure 환경에서 리소스를 중앙에서 관리할 수 있는 Azure 자동화에 따라 달라 집니다. 예를 들어, Azure 업데이트 관리를 사용 하 여 Azure 자동화 예약 하 고 Azure portal에서 사용자 환경에서 컴퓨터에서 업데이트 설치 중앙에서 조정 합니다.


## 어떻게는 Windows Admin Center 사용할 수 있도록 Azure 모니터?

WAC, 내에서 두 모니터링 솔루션과 설정할 수 있습니다.

- [Azure 업데이트 관리](azure-update-management.md) (에서 업데이트 도구)
- (서버 설정)에서 Vm에 대 한 azure 모니터, 사항 가상 컴퓨터 인 사이트

시작할 수 있는 Azure 모니터를 사용 하 여 이러한 도구 중 하나입니다. Log Analytics 작업 영역 (및 자동화 Azure 계정에 필요한 경우) WAC는 자동으로 프로 비전 하기 전에 Azure 모니터를 사용한 경험이 없는 경우 설치 및 대상 서버에서 Microsoft Monitoring Agent (MMA)를 구성 합니다. 그런 다음 해당 솔루션 작업 영역으로 설치 됩니다. 

예를 들어, Azure 업데이트 관리 설정 업데이트 도구를 처음으로 WAC 내용은 다음과 같습니다.

1. 컴퓨터에는 MMA를 설치 합니다.
2. (이 경우 Azure 자동화 계정을 필요한) 이후 Log Analytics 작업 영역 및 자동화 Azure 계정 만들기
3. 새로 만든된 작업 영역에서 업데이트 관리 솔루션을 설치 합니다.

동일한 서버에서 WAC 내에서 다른 모니터링 솔루션을 추가 하려는 경우 WAC 해당 서버 연결 되어 있는 기존 작업 영역에 해당 솔루션을 간단 하 게 설치 합니다. 또한 WAC 다른 필요한 에이전트를 설치 됩니다.

다른 서버에 연결 하지만 이미 설치 (또는 WAC를 통해 수동으로 Azure Portal에서) Log Analytics 작업 영역을 경우 서버에서 MMA 에이전트를 설치 수 및 기존 작업 영역까지 연결 해야 합니다. 서버 작업 영역에 연결할 때 자동으로 데이터를 수집 하 고 해당 작업 영역에 설치 된 솔루션을 보고를 시작 합니다.

## Azure 가상 컴퓨터 (에 대 한 모니터링 가상 컴퓨터 정보)
>적용 대상: Windows Admin Center 미리 보기

설정할 때 모니터 Azure Vm에 대 한 서버 설정에서에서 Windows Admin Center Vm 솔루션을 라고도 가상 컴퓨터 정보에 대 한 Azure 모니터 수 있습니다. 이 솔루션을 사용 하면 서버 상태 및 이벤트 모니터링, 이메일 알림을 생성, 환경에는 통합된 된 서버 성능 보기 넘어갈 및 앱, 시스템 및 해당된 서버에 연결 하는 서비스를 시각화할 수 있습니다.

> [!NOTE]
> 그 이름에도 불구 하 고 VM 인 사이트 뿐 아니라 가상 컴퓨터 및 물리적 서버에 작동 합니다.

Azure 모니터를 사용 하 여 5GB의 데이터/월/고객 여유 무료, 시도해 볼 수 있습니다 쉽게이 서버 또는 우려를 가져오는 데 필요한 비용을 지불 하지 않고 2 개. Azure 모니터에 서버 온 보 딩의 참조 추가 장점에 로그온 할 사용자 환경에서 서버는 통합된 된 시스템 성능 보기는 것과 같은 읽습니다.

### **Azure 모니터와 함께 사용 하기 위해 서버를 설정**

서버 연결의 개요 페이지에서 "관리 경고" 새 단추를 클릭 하거나 서버 설정 gt_ 이동 모니터링 및 경고 합니다. 이 페이지 내에서 등록 서버 Azure 모니터를 클릭 하 여 "설정" 설정 창을 완료 합니다. 관리 센터를 처리 하는 Azure Log Analytics 작업 영역을 프로 비전 필요한 에이전트를 설치 하 고 구성 된 VM 인 사이트 솔루션을 보장 합니다. 완료 되 면 서버 성능 카운터 데이터를 보냅니다 Azure 모니터를 보고 하 고 Azure portal에서이 서버를 기반으로 전자 메일 경고를 만들 수 있습니다.

### **전자 메일 경고 만들기**

서버에 연결한 Azure 모니터, Azure Portal로 이동 지능형 하이퍼링크 설정 gt_ 모니터링 및 경고 페이지 내에서 사용할 수 있습니다. 관리 센터에는 자동으로 성능 카운터를를 쉽게 [만들](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log) 수는 새 경고 많은 미리 정의 된 쿼리 중 하나를 사용자 지정 하거나 직접 작성 하 여 수집 될 수 있습니다.

### * *는 통합된 된 보기를 여러 서버 가져오기 * *

경우 하면 온 보 딩 Azure 모니터 내에서 단일 Log Analytics 작업 영역에 여러 서버에서에서 얻을 수 있습니다 이러한 모든 서버는 통합된 된 보기 Azure 모니터에서 [가상 컴퓨터 정보 솔루션](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview) 입니다.  (온-프레미스 서버 – Azure Vm으로만 상태 탭 기능을 사용 하 여 Azure 모니터에 대 한 가상 컴퓨터 정보의 성능 및 지도 탭은 작동 않음을 note). Azure portal에서이 보려면, Azure 모니터 gt_ (아래에 있는 통찰력), 가상 컴퓨터를 이동한 다음 "Performance" 또는 "지도" 탭으로 이동 합니다.

### **앱, 시스템 및 해당된 서버에 연결 된 서비스 시각화**

때 관리 센터 onboards Azure 모니터에서 VM 인 사이트 솔루션에는 서버, 그 서비스도 [지도 서비스를](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)호출 하는 기능. 이 접근 권한이 값은 자동으로 응용 프로그램 구성 요소를 검색 하 고 Azure portal에서 멋진 세부 정보를 사용 하 여 서버 간 연결을 쉽게 시각화할 수 있도록 서비스 간의 통신을 매핑합니다. Azure 포털 gt_ Azure 모니터 gt_ 가상 컴퓨터 (아래에 있는 관련 정보) 하 고 "지도" 탭으로 이동 하 여이 찾을 수 있습니다.

> [!NOTE]
> Azure 모니터에 대 한 가상 컴퓨터 통찰력을 위한 시각화 6 공개 지역에서 현재 제공 됩니다.  최신 정보에 대 한 [Vm 설명서에 대 한 Azure 모니터](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics)를 확인 합니다.  위에서 설명한 가상 컴퓨터 정보 솔루션에서 제공 추가 이점을 지원 되는 영역 중 하나에서 Log Analytics 작업 영역을 배포 해야 합니다.

## 모니터링을 사용 하지 않도록 설정

Log Analytics 작업 영역에서 서버를 완전히 분리, MMA 에이전트를 제거 합니다. 즉,이 서버는 더 이상 데이터 보내기 작업 영역에서 해당 작업 영역에 설치 된 솔루션은 더 이상 모든 수집 하며 해당 서버에서 데이터를 처리 합니다. 하지만 이렇게 하려면 해당 작업 영역에 보고 하는 리소스는 계속 모든 자체 – 작업을 적용 되지 않습니다. WAC 내에서 MMA 에이전트를 제거 하려면 앱 & 기능으로 이동 하 고 Microsoft Monitoring Agent 찾아 제거를 클릭 합니다.

작업 영역 내에서 특정 솔루션 해제 하려는 경우 [Azure 포털에서 모니터링 솔루션을 제거](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)해야 합니다. 모니터링 솔루션을 제거 하는 인 사이트에서 만든 솔루션은 더 이상 _모든_ 해당 작업 영역에 보고 서버에 대해 생성 될 의미 합니다. 예를 들어 Vm 솔루션에 대 한 Azure 모니터를 제거 하려면 내 작업 영역에 연결 되어 있는 컴퓨터 중 하나에서 VM 또는 서버 성능에 대 한 통찰력을 더 이상 표시 됩니다 I.