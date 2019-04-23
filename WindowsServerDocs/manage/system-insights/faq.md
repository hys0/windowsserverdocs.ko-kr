---
title: System Insights FAQ
description: System Insights FAQ
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: 13767e1336d1ff729d1fbbe6cae3ed57d68cefc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851064"
---
# <a name="system-insights-faq"></a>System Insights FAQ

>적용 대상: Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Azure Monitor 또는 System Center Operations Manager를 사용 하 여 시스템 정보를 어떻게 사용할 수 있습니다?

[Azure Monitor](https://azure.microsoft.com/services/monitor/) 하 고 [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) 인프라를 관리할 수 있도록 배포에서 작업 정보를 제공 합니다. 시스템 정보에는 반면, 로컬 예측 분석 기능을 소개 하는 Windows Server 기능입니다. 함께 시스템 Insights 및 Azure Monitor 또는 SCOM 장치 모집단 예측 화면 유용할 수 있습니다.

 Azure Monitor 또는 SCOM Insights 시스템 이벤트 로그에 각 예측의 결과 출력 시스템 Insights에 의해 생성 되는 이벤트 해제 키 수입니다. Windows 서버, 서버 인스턴스 그룹에 걸쳐 이러한 예측의 통합된 보기를 사용할 수 있도록 수많은 이러한 시스템별 예측 발생할 수 있습니다 이러한. 
 
 각 예측에 대 한 채널 및 이벤트 Id를 참조 하세요 [여기](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results)합니다.

## <a name="how-does-system-insights-relate-to-windows-ml"></a>시스템 정보 Windows ML 어떤 관계가 있습니까?

[Windows ML](https://docs.microsoft.com/windows/uwp/machine-learning/) 는 플랫폼을 가져오고 Windows 장치에서 미리 학습 된 기계 학습 모델 점수 매기기 개발자입니다. 이러한 모델에서 하드웨어 가속을 활용 하 고 로컬로 매길 수 있습니다. 

시스템 Insights는 PowerShell 및 Windows Admin Center 통합을 포함 하는 완전 한 관리 환경 함께 로컬 예측 기능을 제공 하는 Windows Server 2019의 기능입니다. 

## <a name="can-i-use-system-insights-for-my-cluster"></a>내 클러스터에 대 한 시스템 정보를 사용할 수 있나요? 

예 시스템 Insights 독립적으로 실행할 수 없습니다 각 개별 장애 조치 클러스터 노드의 시스템 Insights 예측 사용의 기본 동작에 로컬 저장소, 볼륨, CPU 및 네트워킹에서. **클러스터 된 저장소에 대 한 예측도 설정할 수 있습니다.** 이므로 저장소 예측 기능 클러스터 된 볼륨 및 저장소에 대 한 사용량을 예측 합니다. 

Windows Admin Center 또는 PowerShell에서 이러한 설정을 관리 하 고이 기능에 대 한 자세한 정보를 사용할 수 [여기](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/)합니다.
 

## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>기본 기능을 실행 하도록 리소스 소모 정도 인가요?

각 기본 기능을 실행 하는 데 비용이 많이 드는 아닙니다. 각 기능에 더 많은 데이터를 수집 하지만 일반적으로 몇 초에서 완료 해야 하는 대로 실행 하는 데 더 걸립니다. 

## <a name="see-also"></a>참조
시스템 정보에 대 한 자세한 내용은 다음 리소스를 사용 합니다.

- [시스템 Insights 개요](overview.md)
- [이해 기능](understanding-capabilities.md)
- [관리 기능](managing-capabilities.md)
- [추가 및 기능 개발](adding-and-developing-capabilities.md)
