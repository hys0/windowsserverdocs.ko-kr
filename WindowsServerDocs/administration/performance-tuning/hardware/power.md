---
title: 서버 하드웨어에 대 한 전원 고려 사항
description: 서버 하드웨어에 대 한 전원 고려 사항
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Qizha;TristanB
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 5fe91888188796c96d5da80e8f9bd3ed627b9d43
ms.sourcegitcommit: 08eba714d3ceb5f2dfb5486d6b990da1aa4dcbdd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65564736"
---
# <a name="server-hardware-power-considerations"></a>서버 하드웨어에 대 한 전원 고려 사항

엔터프라이즈 및 데이터 센터 환경에서 에너지 효율성 증가 중요성을 인식 하는 것이 반드시 합니다. 고성능 및 낮은 에너지 사용량이 많습니다 충돌 하는 목표, 있지만 서버 구성 요소를 신중 하 게 선택 하 여 올바른 균형을 얻을 수 있습니다. 다음 섹션에서는 전원 특징 및 기능 서버 하드웨어 구성 요소에 대 한 지침을 보여 줍니다.

## <a name="processor-recommendations"></a>프로세서 추천 사항

빈도, 전압, 캐시 크기 및 프로세스 기술 운영 프로세서의 에너지 소비를 영향을 줍니다. 프로세서 (TDP) 등급 다른 모델을 기준으로 에너지 소비량의 기본 표시를 제공 하는 지점 열 디자인을가지고 있습니다.

일반적으로 성능 목표를 충족 하는 가장 낮은 TDP 프로세서를 선택 합니다. 또한 최신 세대의 프로세서는 일반적으로 더 많은 에너지 효율적인 및 모든 수준의 성능에 더 나은 전원 관리를 사용 하도록 설정 하는 Windows 전원 관리 알고리즘에 대 한 자세한 전원 상태 노출 될 수 있습니다. 또는 Microsoft는 하드웨어 제조업체와 협력에서을 개발 하는 새 "협조적" 전원 관리 기술 중 일부를 사용할 수 있습니다.

협조적 전원 관리 기술에 대 한 자세한 내용은에서 공동 작업 프로세서 성능 제어 라는 섹션을 참조 합니다 [고급 구성 및 전원 인터페이스 사양](http://www.uefi.org/sites/default/files/resources/ACPI_5_1release.pdf)합니다.


## <a name="memory-recommendations"></a>메모리 권장 사항
메모리 총 시스템 전원의 증가 비율을 차지합니다. 다양 한 요인 메모리 기술, 오류 수정 코드 (ECC), 버스 빈도, 용량, 밀도 및 순위 번호와 같은 메모리 DIMM, 에너지 소비를 영향을 줍니다. 따라서 많은 양의 메모리를 구입 하기 전에 예상된 된 전원 등급을 비교 하는 것이 좋습니다.

이제 성능이 낮은 메모리를 사용할 수 있지만 성능 및 비용 장단점을 고려해 야 합니다. 서버 페이징 수는 경우 페이징 디스크 에너지 비용에 고려해 야 합니다.


## <a name="disks-recommendations"></a>디스크 권장 사항
더 높은 RPM 증가 에너지 소비를 의미합니다. SSD 드라이브는 회전 드라이브 보다 더 많은 전력 효율성. 또한 2.5 인치 드라이브는 일반적으로 3.5 인치 드라이브 보다 전원을 해야합니다.

## <a name="network-and-storage-adapter-recommendations"></a>네트워크 및 스토리지 어댑터 추천 사항
일부 어댑터는 유휴 기간 동안 에너지 사용을 줄입니다. 10gb 네트워크 어댑터 및 고대역폭 (4 ~ 8 Gb) 저장소 링크에 대 한 중요 고려 사항입니다. 이러한 장치는 많은 에너지를 사용할 수 있습니다.


## <a name="power-supply-recommendations"></a>전원 공급 장치 권장 사항
성능에 영향을 주지 않고 에너지 소비를 줄일 수 있는 좋은 방법은 전원 공급 장치 효율성을 개선 합니다. 고품질 전원 공급 장치 서버 매년 많은 kilowatt-hours를 저장할 수 있습니다.


## <a name="fan-recommendations"></a>팬 권장 사항
팬, 전원 공급 장치 등은 시스템 성능에 영향을 주지 않고 에너지 사용량을 줄일 수 있는 영역입니다. 변수 속도 팬 시스템 부하가 감소 제거 그렇지 않은 경우 불필요 한 에너지 소비와 RPM을 줄일 수 있습니다.


## <a name="usb-devices-recommendations"></a>USB 장치 권장 사항
기본적으로 USB 장치용 Windows Server 2016 수 있도록 선택적 일시 중단합니다. 그러나 잘못 작성 된 장치 드라이버 상당한 여백으로 시스템 에너지 효율 계속 중단 될 수 있습니다. 잠재적인 문제를 방지 하려면 USB 장치를 분리, BIOS에서 비활성화 또는 USB 장치는 필요 하지 않은 서버를 선택 합니다.


## <a name="remotely-managed-power-strip-recommendations"></a>원격으로 관리 되는 전원 줄무늬 권장 사항
전원 줄무늬 서버 하드웨어의 필수적인 부분 아니지만 데이터 센터에서 큰 차이 할 수 있습니다. 측정값 표시에서는 연결 하지만, 서비스가 표면적으로 전원이 볼륨 서버 성능의 최대 30 와트를 소비 여전히 필요할 수 있습니다.

전력 낭비를 방지 하려면 각 랙은을 프로그래밍 방식으로 특정 서버 전원 연결을 끊으려면 서버에 대 한 원격으로 관리 되는 전원 스트립을 배포할 수 있습니다.

## <a name="processor-terminology"></a>프로세서 용어
이 항목 전체에서 사용 되는 프로세서 용어는 다음 그림에서 사용할 수 있는 구성 요소의 계층 구조를 반영 합니다. 구성 요소 중 가장 작은 세분성으로 가장 큰에서 사용 되는 용어는 다음과 같습니다.

-   프로세서 소켓
-   NUMA 노드(NUMA node)
-   Core
-   논리 프로세서

![프로세서 용어](../media/perftune-guide-figure-1.png)

## <a name="see-also"></a>관련 항목
- [서버 하드웨어에 대 한 성능 고려 사항](index.md)
- [전원 및 성능 튜닝](power/power-performance-tuning.md)
- [프로세서 전원 관리 튜닝](power/processor-power-management-tuning.md)
- [분산 전원 계획에 추천되는 매개 변수](power/recommended-balanced-plan-parameters.md)
