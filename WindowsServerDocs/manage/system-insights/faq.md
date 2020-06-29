---
title: 시스템 정보 FAQ
description: 시스템 정보 FAQ
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: 15aae4983ed04d4bb9e7f4d4991ae5556874453c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471798"
---
# <a name="system-insights-faq"></a>시스템 정보 FAQ

>적용 대상: Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Azure Monitor 또는 System Center Operations Manager에서 시스템 정보를 사용 하려면 어떻게 해야 하나요?

[Azure Monitor](https://azure.microsoft.com/services/monitor/) 및 [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) 는 인프라를 관리 하는 데 도움이 되도록 배포 전체에 대 한 운영 정보를 제공 합니다. 반면, System Insights는 로컬 예측 분석 기능을 소개 하는 Windows Server 기능입니다. 시스템 정보 및 Azure Monitor 또는 SCOM은 모두 장치 모집단에서 예측을 노출 하는 데 도움이 될 수 있습니다.

 System Insights는 각 예측의 결과를 이벤트 로그에 출력 하므로 Azure Monitor 또는 SCOM은 System Insights에서 만든 이벤트를 해제할 수 있습니다. 이러한 시스템은 여러 Windows 서버에서 이러한 시스템 관련 예측을 표시할 수 있으므로 서버 인스턴스 그룹에서 이러한 예측을 통합 하 여 볼 수 있습니다.

 각 예측에 대 한 채널 및 이벤트 Id는 [여기](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results)를 참조 하세요.

## <a name="how-does-system-insights-relate-to-windows-ml"></a>System Insights는 Windows ML과 어떻게 관련이 있나요?

[WINDOWS ML](https://docs.microsoft.com/windows/uwp/machine-learning/) 은 개발자가 windows 장치에서 미리 학습 된 기계 학습 모델을 가져오고 점수를 매길 수 있는 플랫폼입니다. 이러한 모델은 하드웨어 가속을 활용 하 여 로컬에서 점수가 매겨집니다.

System Insights는 PowerShell 및 Windows 관리 센터 통합을 포함 하 여 완전 한 관리 환경과 함께 로컬 예측 기능을 제공 하는 Windows Server 2019의 기능입니다.

## <a name="can-i-use-system-insights-for-my-cluster"></a>클러스터에 대 한 시스템 정보를 사용할 수 있나요?

예. System Insights는 각 개별 장애 조치 (failover) 클러스터 노드에서 독립적으로 실행 될 수 있으며, System Insights의 기본 동작은 로컬 저장소, 볼륨, CPU 및 네트워킹에서 사용량을 예측 합니다. 클러스터 된 **저장소에 대 한 예측을 사용 하도록 설정**하 여 저장소 예측 기능이 클러스터 된 볼륨 및 저장소에 대 한 사용량을 예측할 수도 있습니다.

Windows 관리 센터 또는 PowerShell에서 이러한 설정을 관리할 수 있으며,이 기능에 대 한 자세한 정보는 [여기](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/)에서 확인할 수 있습니다.


## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>기본 기능을 실행 하는 비용은 얼마 인가요?

각 기본 기능은 실행 비용이 저렴 합니다. 더 많은 데이터를 수집할 때 각 기능을 실행 하는 데 더 많은 시간이 걸리지만 일반적으로 몇 초만에 완료 해야 합니다.

## <a name="additional-references"></a>추가 참조
시스템 정보에 대 한 자세한 내용을 보려면 다음 리소스를 사용 하세요.

- [시스템 인사이트 개요](overview.md)
- [기능 이해](understanding-capabilities.md)
- [기능 관리](managing-capabilities.md)
- [기능 추가 및 개발](adding-and-developing-capabilities.md)
