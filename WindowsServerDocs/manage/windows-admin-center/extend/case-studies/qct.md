---
title: Windows Admin Center SDK 사례 연구-QCT
description: Windows Admin Center SDK 사례 연구-QCT
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 2e0ed4a122a3cb26ce4c6e05ee3b808dd6fe2d07
ms.sourcegitcommit: 214e827934e7b3e8987e9e0ab2cf00047d332c89
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67153603"
---
# <a name="qct-management-suite-extension"></a>QCT Management Suite 확장

## <a name="a-simple-path-to-server-infrastructure-management"></a>서버 인프라 관리에 대 한 간단한 경로

Windows Admin Center 대 한 QCT Management Suite 확장 시스템 구성을 모니터링 및 관리의 서버 상태에 대 한 투명 대시보드의 단일 창이 제공 [QCT Azure Stack HCI 시스템 certified](https://go.qct.io/solutions/enterprise-private-cloud/qxstack-windows-server-cloud-ready-appliances/windows-server-software-defined-solution-wssd/) : [QuantaGrid D52BQ 2U](https://www.qct.io/product/index/Server/rackmount-server/2U-Rackmount-Server/QuantaGrid-D52BQ-2U), [QuantaGrid D52T 1ULH](https://www.qct.io/product/index/Storage/Storage-Server/1U-Storage-Server/QuantaGrid-D52T-1ULH) 하 고 [QuantaPlex T21P 4U](https://www.qct.io/product/index/Storage/Storage-Server/4U-Storage-Server/QuantaPlex-T21P-4U)합니다.

고객의 고충 기존 모니터링 및 관리와 관련 하 여 기반의 QCT 단독, 보완 기능을 제공 함수를 시스템 이벤트 로그의 개요를 포함 하는 드라이버 및 전반적인을 향상 시키기 위해 하드웨어 구성 요소 상태를 모니터링 합니다. 관리 환경입니다.

![QCT 확장](../../media/extend-case-study-qct/D52T_DarkMode_Disk-Detail-General.PNG)

QCT Management Suite 아래 주요 기능을 사용 하 여 Windows Admin Center 기능을 확장 합니다.
- **한 번의 클릭 전용 하드웨어 관리** -직관적인 사용자 인터페이스를 모델 이름, 프로세서, 메모리 및 BIOS를 포함 하 여 하드웨어 정보를 표시 합니다. IT 관리자에는 간단한 원클릭 UI 사용 하 여 BMC 다시 시작할 수 있습니다.

![QCT 확장](../../media/extend-case-study-qct/D52T_Overview.PNG)

- **디스크 매핑 및 효율적인 서비스 지원에 대해 식별 LED** -QCT Management Suite 마법사 UI 디자인 디스크 프로필의 개요 및 효율적인 대체에 대 한 선택한 디스크의 LED 간단한 컨트롤을 사용 하 여 선택한 각 디스크의 슬롯을 표시 합니다.

![QCT 확장](../../media/extend-case-study-qct/T21P_disk_mapping.png)

- 하드웨어 이벤트 로그 및 상태에 대 한 모니터링 도구를 사용 하기 쉬운입니다.

![QCT 확장](../../media/extend-case-study-qct/D52T_event_log.PNG)

- **예측 디스크 관리** -S.M.A.R.T 정보와 조직 전체로 오류가 발생 하기 전에 작업을 수행할 수 있는 비정상 알림을 사용 하 여 시스템 조건을 평가 합니다.

![QCT 확장](../../media/extend-case-study-qct/T21P_SMART.PNG)

QCT Management Suite에 대 한 Windows Admin Center 대 한 자세한 정보:
- [QCT Management Suite 웹 페이지](https://go.qct.io/solutions/enterprise-private-cloud/qxstack-windows-server-cloud-ready-appliances/)
- [QCT Management Suite 데이터 시트](https://go.qct.io/wp-content/uploads/2019/04/WAC-data-sheet_v04222019.pdf)