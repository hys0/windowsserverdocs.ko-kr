---
title: 데이터 센터 브리지 (DCB)
description: Windows Server 2016의 데이터 센터 브리지에 대 한 정보도 대 한이 항목을 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3d465e855adc387d7136919ac11fbab56c792c34
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="data-center-bridging-dcb"></a>데이터 센터 \(DCB\) 브리지

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에 대 한 데이터 센터 브리지 \(DCB\) 안내 정보 사용할 수 있습니다.

DCB 수렴 패브릭 저장소, 데이터, 클러스터 Inter\ 프로세스 통신 \(IPC\) 네트워킹과 관리 교통 모두 동일한 이더넷 네트워크 인프라를 공유 되는 데이터 센터에 사용할 수 있는 전기 연구소 및 전자 제품 엔지니어 \(IEEE\) 표준 제품군입니다.

>[!NOTE]
>이 항목 외에 다음과 같은 DCB 설명서는
>
>- [Windows 10 또는 Windows Server 2016 DCB 설치](dcb-install.md)
>- [데이터 센터 브리지 (DCB) 관리](dcb-manage.md)

DCB은 대역폭 hardware\ 기반 할당 특정 종류의 네트워크 교통량을 제공 하며 흐름 priority\ 기반 제어를 사용 하 여 이더넷 전송 안정성을 개선 합니다.

교통 운영 체제를 무시 하 고 수 지원 인터넷 작은 컴퓨터 시스템 인터페이스 \(iSCSI\), 원격 직접 메모리 액세스 \(RDMA\) 위로, 이더넷 또는 파이버 채널 이더넷 \(FCoE\) 위로 집약된 네트워크 어댑터에 오프 대역폭 Hardware\ 기반 할당 필수입니다.

위 계층 프로토콜 파이버 채널 등 가정 무손실 기본 전송 하는 경우 흐름 Priority\ 기반 제어 반드시 필요 합니다.

## <a name="dcb-protocols-and-management-options"></a>DCB 프로토콜 및 관리 옵션

DCB은 프로토콜 다음 집합으로 구성 됩니다. 

- 향상 된 전송 서비스 \(ETS\) – IEEE 802.1Qaz, 표준 802.1 P 켜고 802.1 q 빌드는
- 우선 순위 흐름 \(PFS\) IEEE 802.1Qbb 제어 
- DCB 교환 프로토콜 \(DCBX\), IEEE 802.1AB,으로 표준 802.1Qaz에 추가 합니다.

DCBX 프로토콜 Windows Server 2016을 실행 하는 컴퓨터 같은 종료 디바이스를 자동으로 구성할 수 스위치 DCB 구성할 수 있습니다.

DCB 스위치를 관리 하는 것을 선호 하는 경우 필요가 DCB 기능 Windows Server 2016 따라 설치이 이렇게 몇 가지 제한 사항이 포함 되어 있지만 합니다.

하지만 DCBX ETS 클래스 크기와 PFC 구현 지원의 호스트 네트워크 어댑터를 알려줄만 수을 하기 때문에, Windows Server 호스트 일반적으로 필요 교통 ETS 클래스 매핑됩니다 되도록 DCB가 설치 되어 있는지 합니다.

Windows 응용 프로그램은 일반적으로 없도록 DCBX 거래소에 참여할 수 있습니다. 이 때문 호스트 구성 해야 별도로 같은 설정으로 만들어졌지만 보너스 네트워크 스위치가에서 합니다.

스위치를 DCB 관리할 선택 않으면를 Windows PowerShell 명령을 사용 하 여 Windows Server 2016에 구성을 계속 볼 수 있습니다.

##  <a name="important-dcb-functionality"></a>중요 한 DCB 기능

다음은 DCB에서 제공 하는 기능을 요약 하는 목록입니다.

1. DCB\ 가능 네트워크 어댑터와 DCB\ 가능 스위치 간의 상호 운용성을 제공합니다.

2. 네트워크 어댑터에 흐름 priority\ 기반 컨트롤을 켜서 Windows Server 2016 및 해당 이웃 스위치를 실행 하는 컴퓨터 간에 무손실 이더넷 전송을 제공 합니다.

3. 802.1 p 교통 클래스 \(priority\) 표시기가 구분 클래스 트래픽 하나 이상의 TC 수 디코더의 비율로 교통 제어 \(TC\)에 대역폭 할당할 수가 있습니다.

4. 서버 관리자 또는 네트워크 관리자 신청서 특정 교통 클래스 또는 유명 프로토콜, 유명 TCP/UDP 포트 또는 응용 프로그램에서 사용 되는 NetworkDirect 포트에 따라 우선 순위를 지정할 수 있습니다.

5. Windows PowerShell 및 Windows Server 2016 WMI(Windows Management Instrumentation) \(WMI\) 통해 DCB 관리 기능을 제공 합니다. 자세한 내용은 섹션을 참조 [DCB에 대 한 Windows PowerShell 명령](#bkmk_wps) 다음 항목 외에도이 항목 뒷부분에 있습니다.
    - [시스템에서 제공한 DCB 구성 요소](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [데이터 센터 브리지 NDIS QoS 요구 사항](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Windows Server 2016 그룹 정책을 통해 DCB 관리 기능을 제공 합니다.

7. Windows Server 2016 서비스 품질 \(QoS\) 솔루션 공존을 지원합니다.

>[!NOTE]
>모든 RDMA RDMA의 수렴 이더넷 \(RoCE\) 버전을 사용 하기 전에 DCB 사용 하도록 설정 해야 합니다. 인터넷 다양 한 영역 RDMA 프로토콜 \(iWARP\) 네트워크 필요 하지 않을 모든 Ethernet\ 기반 RDMA 기술 DCB와 더 잘 작동 결정 했습니다 테스트 합니다. 이 인해 DCB iWARP RDMA 배포를 위해 사용 하 여 고려해 야 합니다. 자세한 내용은 참조 [원격 직접 메모리 액세스 (RDMA) 및 스위치 Embedded 팀 (설정)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.

##  <a name="practical-applications-of-dcb"></a>DCB의 실제 응용 프로그램

많은 조직 큰 파이버 채널 \(FC\) storage 영역 네트워크 \(SAN\) 설치 되어 저장소 서비스에 대 한 합니다. FC 산 서버 및 네트워크에 있는 스위치 FC 특별 한 네트워크 어댑터가 있어야합니다. 이러한 조직 일반적으로 사용 하 여 수도 이더넷 네트워크 어댑터와 전환 합니다.

대부분의 경우 FC 하드웨어는 배포 하는 큰 대문자 지출 결과 이더넷 하드웨어를 보다 더 비싼입니다. 또한 공간, 전원 및 냉각 추가, 지속적인 작동 지출에 해당 하는 데이터 센터의 성능을 하드웨어에 대 한 별도 이더넷 및 FC 산 네트워크 어댑터와 스위치 요구 사항이 필요 합니다.

이 비용 관점에서 저장 및 데이터 네트워킹 서비스를 제공 하기 위해 자녀가 Ethernet\ 기반 하드웨어 솔루션 FC 기술을 병합 하는 많은 조직에 대 한 유리 합니다.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>저장소 및 데이터 네트워킹 Ethernet\ 기반 집약된 패브릭 DCB 사용

이미 큰 FC 산 없지만 FC 기술에 대 한 추가 투자 떨어진 마이그레이션하려는 조직에서 DCB 만들 수 기반 이더넷 수렴 저장소 및 데이터 네트워킹 패브릭 합니다. 한 DCB 수렴 패브릭은 향후 총 소유 비용도 절감 줄일 수 \(TCO\) 관리를 간소화 하 고 있습니다.

사람을 채택 이미 또는 채택 계획인 호스팅, DCB 자신의 저장소 솔루션으로 iSCSI iSCSI 트래픽을 분리 성능 되도록 대역폭 hardware\ 지원 예약을 제공할 수 있습니다. 이며 다른 독점 솔루션 달리 DCB standards\ 기반-및 따라서 상대적으로 쉽게 배포 및 다른 유형의 네트워크 환경에서 관리할 수 있습니다.

DCB Windows Server 2016 \-based 구현 하는 많은 때 발생할 수 있는 수렴 여러 주문자 \(OEMs\)에서 패브릭 솔루션을 제공 하는 문제를 줄여 줍니다.

여러 Oem 제공한 솔루션을 소유 구현을 간의 상호 작용 하지 수, 하기 어려울 수 있습니다 관리 하 고 다른 소프트웨어 유지 관리 일정은 일반적으로 합니다. 

반면, Windows Server 2016 DCB standards\ 기반 이며 배포 하 고 다른 유형의 네트워크에서 DCB 관리할 수 있습니다.

## <a name="bkmk_wps"></a>Windows PowerShell DCB에 대 한 명령

Windows Server 2016 및 Windows Server 2012 r 2에 대 한 명령 DCB Windows PowerShell 가지가 있습니다. Windows Server 2016에 Windows Server 2012 r 2에 대 한 모든 명령을 사용할 수 있습니다.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>Windows Server 2016 Windows PowerShell DCB에 대 한 명령

Windows Server 2016에 대 한 다음 항목에 대 한 모든 데이터 센터 브리지 \(DCB\) Windows PowerShell cmdlet 설명 및 구문 제공 서비스 품질 \ (QoS\) \-specific cmdlet 합니다. Cmdlet 동사 cmdlet의 왼쪽 끝에 따라 사전순으로 나열 됩니다.

- [DcbQoS 모듈](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>Windows Server 2012 r 2 Windows PowerShell 명령을 DCB

Windows Server 2012 r 2에 대 한 다음 항목에 대 한 모든 데이터 센터 브리지 \(DCB\) Windows PowerShell cmdlet 설명 및 구문 제공 서비스 품질 \ (QoS\) \-specific cmdlet 합니다. Cmdlet 동사 cmdlet의 왼쪽 끝에 따라 사전순으로 나열 됩니다.

- [데이터 센터에서 Windows PowerShell Cmdlet 서비스의 품질 (DCB) 브리지](https://technet.microsoft.com/library/hh967440.aspx)
