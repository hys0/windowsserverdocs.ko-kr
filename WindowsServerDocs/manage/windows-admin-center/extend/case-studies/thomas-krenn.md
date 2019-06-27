---
title: Windows Admin Center SDK 사례 연구-Thomas Krenn
description: Windows Admin Center SDK 사례 연구-Thomas Krenn
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93b8a450aa86a454ec6febd349fcaa35df590266
ms.sourcegitcommit: 3be280c8638214857dc355b201eb56a04499a5e5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2019
ms.locfileid: "67396763"
---
# <a name="thomas-krennag-extension"></a>Thomas Krenn.AG 확장

## <a name="intuitive-server-and-storage-health-management"></a>직관적인 서버와 저장소 상태 관리

Thomas Krenn.AG Windows Admin Center 확장 하도록 특별히 지정 된 항상 사용 가능한 2-노드 [S2D 마이크로 클러스터](https://www.thomas-krenn.com/en/products/application/software-defined-storage/s2d-micro-cluster.html) 어플라이언스입니다. 사용자에 게 친숙 하 고 그래픽 웹 인터페이스는 간단한 대시보드를 통해 마이크로-클러스터의 상태를 시각화 하 고 저장소 장치, 네트워크 인터페이스 또는 자세한 정보를 보려면 전체 클러스터에서 드릴 다운할 수 있습니다.

확장 호출에 대 한 첫 번째 수준의 서비스 및 지원, 일련 번호, 소프트웨어 버전, 저장소 사용률 등 일반적으로 필요한 정보에 대 한 직관적인 액세스를 제공 합니다. 이전 Windows Server 하이퍼 수렴 형 인프라를 사용한 경험이 없다고 권한이 관리자에 게 유용 하 게 설계 되었습니다.

사용할 수 있는 정보의 일부 다음과 같습니다.
- Micro-노드 및 Micro-클러스터에 대 한 일반 정보
- OS / 장치 상태를 부팅 합니다.
- 용량 HDD 및 SSD 상태 캐싱
- 클러스터 이벤트
- 네트워크 상태 및 정보

클러스터의 상태 및 일련 번호, 모델, OS 버전 및 사용률 같은 중요 한 시스템 정보를 확인 하려면 대시보드를 사용 합니다. 또한 팬, NIC 및 전체 노드 하드웨어 상태는 대시보드에 표시 됩니다.

![Thomas Krenn 확장](../../media/extend-case-study-thomas-krenn/thomas-krenn-1.png)

저장소 장치 일련 번호, 스마트-상태 및 용량 사용률을 볼 수로 다운할 수 있습니다. 부팅 장치에는 표시기를 섹터 기능과 시간에 다시 할당 SSD 상태의 가장 잘 나타내는 지표는 out wear 보여 줍니다.

![Thomas Krenn 확장](../../media/extend-case-study-thomas-krenn/thomas-krenn-2.png)

클러스터 상태 아이콘을 클러스터의 운영 세부 정보의 요약을 표시 하도록 확장 됩니다.

![Thomas Krenn 확장](../../media/extend-case-study-thomas-krenn/thomas-krenn-3.png)

전체 밤이 마이크로 클러스터의 Azure 클라우드 감시를 사용할 수 없는, 후 한눈에도 문제를 확인 하려면 충분 합니다. "알림"을 바로 클릭할 빠른 수정 하기 위해 관련 이벤트를 나열 합니다. 클러스터 이벤트 지역화 및 기본 OS 언어에 따라 결정 됩니다. 확장 자체로 영어와 독일어를 지원합니다.

![Thomas Krenn 확장](../../media/extend-case-study-thomas-krenn/thomas-krenn-4.png)

네트워크 정보도 쉽게 사용할 수 있습니다.

![Thomas Krenn 확장](../../media/extend-case-study-thomas-krenn/thomas-krenn-5.png)

고객 피드백에 따라도 구현 했습니다 "어두운 모드" Windows Admin Center v1904에서 사용할 수 있습니다. 어두운 데이터 센터에 빛나는 잘못 캐비닛에 가장 가까운 격렬 한 느낌입니다. 또한 있습니다 Windows Admin Center 더욱 특정 시각 장애가 있는 관리자에 대 한 반사를 줄여.

![Thomas Krenn 확장](../../media/extend-case-study-thomas-krenn/thomas-krenn-6.png)

Thomas Krenn 즉시 사용성 및 접근성 학습 되지 않은 관리자에 대 한 소규모 및 중간 규모 비즈니스 시장에서 하이퍼 수렴 형 인프라에 대 한 뛰어난 고객 경험을 키 수는 것을 깨달았습니다. Thomas-Krenn의 마이크로 클러스터 확장 대시보드에서 독점 하드웨어 정보를 포함 하 고 다시 그룹화 되는 중요 한 클러스터 상태 정보를 새로운 Windows Admin Center 네이티브 HCI 관리 기능을 완벽 하 게 보완 친숙 한 인터페이스입니다.

개발 프로세스 동안 노드 실패 후에 관리 효율성 확인 클러스터 자체에 고가용성 구성으로 Windows Admin Center 1904 배포 하기로 결정 했습니다. 확장에는 전체 OS와 마찬가지로 미리 설치 됩니다.

확장은 Microsoft에서 개발 중인 Windows Admin Center 1904를 사용 하 여 병렬로 구축 되었습니다. 공동 작업 및 제품 2019 년 4 월에에서 성공적으로 시작 하기 전에 공동으로 확인 된 양쪽에서 노출 하는 지속적인 피드백 문제를 닫습니다. Thomas Krenn는 완전히 지원 하 고 Windows Admin Center 1904의 새로운 기능을 구현 하는 것으로 매우 자랑 스럽게 생각 합니다.
