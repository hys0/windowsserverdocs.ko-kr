---
title: Windows Server 하드웨어 전원 고려 사항
description: Windows Server 하드웨어 전원에 대 한 고려 사항
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: conceptual
ms.author: qizha;tristanb
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0e110fbb41f44a4c8ac6ab014eeae44e542ade41
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471688"
---
# <a name="server-hardware-power-considerations"></a>서버 하드웨어에 대한 전원 고려 사항

엔터프라이즈 및 데이터 센터 환경에서 에너지 효율성의 중요도를 높이는 것이 중요 합니다. 고성능 및 낮은 에너지 사용량은 종종 충돌 목표가 됩니다. 하지만 서버 구성 요소를 신중 하 게 선택 하 여 두 서버 간에 정확한 균형을 달성할 수 있습니다. 다음 섹션에서는 서버 하드웨어 구성 요소의 전원 특성 및 기능에 대 한 지침을 제공 합니다.

## <a name="processor-recommendations"></a>프로세서 추천 사항

주파수, 운영 전압, 캐시 크기 및 프로세스 기술은 프로세서의 에너지 소비량에 영향을 줍니다. 프로세서에는 다른 모델을 기준으로 에너지 소비량의 기본적인 표시를 제공 하는 TDP (열 디자인 지점) 등급이 있습니다.

일반적으로 성능 목표를 충족 하는 가장 낮은 TDP 프로세서를 선택 합니다. 또한 새로운 프로세서 세대는 일반적으로 더 에너지 효율적 이며, Windows 전원 관리 알고리즘의 전원 상태를 더 많이 노출 하 여 모든 수준의 성능에서 더 나은 전원 관리를 수행할 수 있습니다. 또는 Microsoft가 하드웨어 제조업체와 협력 하 여 개발한 새로운 "협조적" 전원 관리 기술 중 일부를 사용할 수 있습니다.

공동 작업 전원 관리 기술에 대 한 자세한 내용은 [고급 구성 및 전원 인터페이스 사양의](http://www.uefi.org/sites/default/files/resources/ACPI_5_1release.pdf)"공동 작업 프로세서 성능 제어" 섹션을 참조 하세요.

## <a name="memory-recommendations"></a>메모리 권장 사항

메모리 계정-전체 시스템 전력의 비율을 늘립니다. 메모리 기술, ECC (오류 수정 코드), 버스 주파수, 용량, 밀도 및 순위 수와 같은 많은 요소가 메모리 DIMM의 에너지 소비량에 영향을 줍니다. 따라서 많은 양의 메모리를 구매 하기 전에 예상 되는 전원 등급을 비교 하는 것이 좋습니다.

이제 저전력 메모리를 사용할 수 있지만 성능 및 비용 장단점을 고려해 야 합니다. 서버를 페이징 하는 경우 페이징 디스크의 에너지 비용도 고려해 야 합니다.

## <a name="disks-recommendations"></a>디스크 권장 사항

RPM이 클수록 에너지 소비가 증가 했음을 의미 합니다. SSD 드라이브는 회전 드라이브 보다 더 효율적입니다. 또한 2.5 인치 드라이브는 일반적으로 3.5 인치 드라이브 보다 더 낮은 전력이 필요 합니다.

## <a name="network-and-storage-adapter-recommendations"></a>네트워크 및 스토리지 어댑터 추천 사항

일부 어댑터는 유휴 기간 동안 에너지 소비량을 줄입니다. 이는 10gb 네트워킹 어댑터 및 고대역폭 (4-8 Gb) 저장소 링크에 대 한 중요 한 고려 사항입니다. 이러한 장치는 상당한 양의 에너지를 소비할 수 있습니다.

## <a name="power-supply-recommendations"></a>전원 공급 장치 권장 사항

전원 공급 효율성 향상은 성능에 영향을 주지 않고 에너지 소비를 줄이는 좋은 방법입니다. 높은 효율성 전원 공급 장치는 서버당 여러 kilowatt 시간을 절약할 수 있습니다.

## <a name="fan-recommendations"></a>팬 권장 사항

전원 공급 장치와 같은 팬은 시스템 성능에 영향을 주지 않고 에너지 소비를 줄일 수 있는 영역입니다. 가변 속도 팬은 시스템 부하가 감소할 때 RPM을 줄여 불필요 한 에너지 소비를 없앨 수 있습니다.

## <a name="usb-devices-recommendations"></a>USB 장치 권장 사항

Windows Server 2016는 기본적으로 USB 장치에 대 한 선택적 일시 중단을 사용 합니다. 그러나 잘못 작성 된 장치 드라이버는 여전히 많은 여백으로 시스템 에너지 효율성을 방해할 수 있습니다. 잠재적인 문제를 방지 하려면 USB 장치를 분리 하 고, BIOS에서 사용 하지 않도록 설정 하거나, USB 장치가 필요 하지 않은 서버를 선택 합니다.

## <a name="remotely-managed-power-strip-recommendations"></a>원격으로 관리 되는 전원 스트립 권장 사항

전원 스트립은 서버 하드웨어의 필수적인 부분이 아니지만 데이터 센터에서 큰 차이를 만들 수 있습니다. 측정은 전원에 연결 되어 있지만 서비스가 표면적으로 된 볼륨 서버를 표시 하지만 여전히 최대 30 와트의 전원을 요구할 수 있습니다.

전기 낭비를 방지 하기 위해 각 서버 랙에 대해 원격으로 관리 되는 전원 스트립을 배포 하 여 특정 서버에서 프로그래밍 방식으로 전원 연결을 해제할 수 있습니다.

## <a name="processor-terminology"></a>프로세서 용어

이 항목 전체에서 사용 되는 프로세서 용어는 다음 그림에서 사용할 수 있는 구성 요소의 계층 구조를 반영 합니다. 가장 큰 단위에서 가장 작은 규모의 구성 요소에 사용 되는 용어는 다음과 같습니다.

- 프로세서 소켓
- NUMA 노드(NUMA node)
- 코어
- 논리 프로세서

![프로세서 용어](../media/perftune-guide-figure-1.png)

## <a name="additional-references"></a>추가 참조

- [서버 하드웨어에 대한 성능 고려 사항](index.md)

- [전원 및 성능 튜닝](power/power-performance-tuning.md)

- [프로세서 전원 관리 튜닝](power/processor-power-management-tuning.md)

- [분산 전원 계획에 추천되는 매개 변수](power/recommended-balanced-plan-parameters.md)
