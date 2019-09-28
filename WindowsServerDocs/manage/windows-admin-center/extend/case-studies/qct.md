---
title: Windows 관리 센터 SDK 사례 연구-QCT
description: Windows 관리 센터 SDK 사례 연구-QCT
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/14/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 2922bcdd08fac7bf2179a0ebbad37c7151d660b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357253"
---
# <a name="qct-management-suite-extension"></a>QCT 관리 도구 모음 확장

## <a name="a-simple-path-to-server-infrastructure-management"></a>서버 인프라 관리의 간단한 경로

Windows 관리 센터 용 QCT Management Suite 확장은 시스템 구성을 모니터링 하 고 [qct AZURE STACK HCI 인증 시스템](https://go.qct.io/solutions/enterprise-private-cloud/qxstack-windows-server-cloud-ready-appliances/windows-server-software-defined-solution-wssd/) 의 서버 상태를 관리 하기 위한 투명 한 단일 창을 제공 합니다. [QUANTAGRID D52BQ](https://www.qct.io/product/index/Server/rackmount-server/2U-Rackmount-Server/QuantaGrid-D52BQ-2U), [QuantaGrid D52T-1ulh](https://www.qct.io/product/index/Storage/Storage-Server/1U-Storage-Server/QuantaGrid-D52T-1ULH) 및 [QuantaPlex T21P-4u](https://www.qct.io/product/index/Storage/Storage-Server/4U-Storage-Server/QuantaPlex-T21P-4U).

고객 불만에 따라 기존 모니터링 및 관리를 기반으로 하는 QCT는 시스템 이벤트 로그, 모니터링 드라이버 및 하드웨어 구성 요소 상태에 대 한 개요를 포함 하 여 전체 기능을 향상 시킬 수 있는 독점적인 보조 기능 및 기능을 제공 합니다. 관리 환경.

![QCT 확장](../../media/extend-case-study-qct/D52T_DarkMode_Disk-Detail-General.PNG)

QCT 관리 제품군은 다음과 같은 주요 기능을 통해 Windows 관리 센터의 기능을 확장 합니다.
- **한 번 클릭 전용 하드웨어 관리** -직관적인 사용자 인터페이스에는 모델 이름, 프로세서, 메모리 및 BIOS를 비롯 한 하드웨어 정보가 표시 됩니다. IT 관리자는 간단한 단일 클릭 UI를 사용 하 여 BMC를 다시 시작할 수 있습니다.

![QCT 확장](../../media/extend-case-study-qct/D52T_Overview.PNG)

- **효율적인 서비스 지원에 대 한 디스크 매핑 및 LED 식별** -Qct 관리 제품군 마법사 UI 디자인은 선택한 각 디스크의 슬롯과 디스크 프로필의 개요를 표시 하 고 선택한 디스크의 led 라이트 제어를 효율적으로 대체 하도록 표시 합니다.

![QCT 확장](../../media/extend-case-study-qct/T21P_disk_mapping.png)

- 하드웨어 이벤트 로그 및 상태에 대 한 사용 하기 쉬운 모니터링 도구입니다.

![QCT 확장](../../media/extend-case-study-qct/D52T_event_log.PNG)

- **예측 디스크 관리** -전체 오류가 발생 하기 전에 조직이 조치를 취할 수 있도록 하는 정보 및 비정상 알림을 사용 하 여 시스템 조건을 평가 합니다.

![QCT 확장](../../media/extend-case-study-qct/T21P_SMART.PNG)

Windows 관리 센터의 QCT Management Suite에 대해 자세히 알아보세요.
- [QCT 관리 도구 모음 웹 페이지](https://go.qct.io/solutions/enterprise-private-cloud/qxstack-windows-server-cloud-ready-appliances/)
- [QCT 관리 도구 모음 데이터 시트](https://go.qct.io/wp-content/uploads/2019/04/WAC-data-sheet_v04222019.pdf)