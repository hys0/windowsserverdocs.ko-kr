---
title: DCB(데이터 센터 브리징)
description: Windows Server 2016의 데이터 센터 브리징에 대 한 기본 정보에 대 한이 항목에서는 사용할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7cb488192a873743db27d9c1d09c5912bc810bb8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834184"
---
# <a name="data-center-bridging-dcb"></a>데이터 센터 브리징 \(DCB\)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 사용 하 여 데이터 센터 브리징에 대 한 기본적인 자세한 \(DCB\)합니다.

DCB는 Institute of Electrical and Electronics Engineers 모음인 \(IEEE\) 는 저장소, 데이터 네트워킹, 클러스터 간 데이터 센터에서 수렴 된 패브릭을 사용할 수 있는 표준\-프로세스 통신 \(IPC\), 및 관리 트래픽이 모두 동일한 이더넷 네트워크 인프라를 공유 합니다.

>[!NOTE]
>이 항목 외에 다음 DCB 문서 수
>
>- [Windows Server 2016 또는 Windows 10에서 DCB를 설치 합니다.](dcb-install.md)
>- [관리 데이터 센터 브리징 (DCB)](dcb-manage.md)

DCB는 하드웨어\-는 특정 유형의 네트워크 트래픽에 대역폭 할당을 기반으로 하 고 우선 순위 사용 하 여 이더넷 전송 안정성을 개선\-기반 흐름 제어 합니다.

하드웨어\-기반된 대역폭 할당을 반드시 트래픽을 운영 체제를 바이패스 하 고 Internet Small Computer System Interface 지 수렴 형된 네트워크 어댑터에 오프 로드 된 경우 \(iSCSI\), 원격 직접 메모리 액세스 \(RDMA\) 이더넷 또는 Fiber Channel over Ethernet 위에 \(FCoE\)합니다.

우선 순위\-기반된 흐름 제어 파이버 채널 등 상위 계층 프로토콜에서 무손실 기본 전송을 가정 필수적입니다.

## <a name="dcb-protocols-and-management-options"></a>DCB 프로토콜 및 관리 옵션

DCB은 프로토콜 집합으로 구성 됩니다. 

- 전송 서비스 향상 \(ETS\) – 기반으로 하 여 802.1p 고 802.1Q 표준 IEEE 802.1Qaz,
- 우선 순위 흐름 제어 \(PFS\), IEEE 802.1Qbb 
- DCB 교환 프로토콜 \(DCBX\), IEEE 802.1AB, 표준 802.1Qaz의 확장으로 합니다.

DCBX 프로토콜을 사용 하면 Windows Server 2016을 실행 하는 컴퓨터 같은 최종 장치를 자동으로 구성할 수 있는 스위치에 DCB를 구성할 수 있습니다.

하지만 스위치에서 DCB를 관리 하려는 경우 필요가 없습니다 Windows Server 2016의 기능으로 DCB를 설치이 방법은 몇 가지 제한 사항이 포함 되어 있습니다.

하므로 DCBX ETS 클래스 크기 및 PFC 사용의 호스트 네트워크 어댑터를 알릴 수 있습니다만, 단, Windows Server 호스트 일반적으로 필요 트래픽을 ETS 클래스에 매핑되는 DCB가 설치 되어 있는지 합니다.

Windows 응용 프로그램은 일반적으로 DCBX 교환에 참여 하도록 설계 되지 않았습니다. 이 인해 호스트 별도로 구성 해야 네트워크 스위치에서 하지만 동일한 설정을 사용 하 여 합니다.

스위치에서 DCB를 관리 하려는 경우 Windows PowerShell 명령을 사용 하 여 Windows Server 2016에서 구성을 여전히 볼 수 있습니다.

##  <a name="important-dcb-functionality"></a>중요 한 DCB 기능

아래 DCB에서 제공하는 기능이 요약되어 있습니다.

1. DCB 간의 상호 운용성을 제공\-가능 네트워크 어댑터와 DCB\-가능 스위치입니다.

2. 우선 순위 설정 하 여 Windows Server 2016와 인접 스위치를 실행 하는 컴퓨터 간에 무손실 이더넷 전송을 제공\-네트워크 어댑터에 대해 흐름 제어를 기반으로 합니다.

3. 트래픽 제어 대역폭을 할당할 수 있는 기능도 \(TC\) the TC는 802.1p 트래픽 클래스에 의해 구별 하는 트래픽의 하나 또는 그 이상의 클래스가 구성 될 수 있는 백분율순 \(우선 순위\) 표시기입니다.

4. 서버 관리자 또는 네트워크 관리자가 응용 프로그램에서 사용하는 알려진 프로토콜, 알려진 TCP/UDP 포트 또는 NetworkDirect 포트를 기반으로 특정 트래픽 클래스나 우선 순위에 해당 응용 프로그램을 할당할 수 있도록 합니다.

5. Windows Server 2016 Windows Management Instrumentation 통한 DCB 관리 기능을 제공 \(WMI\) 및 Windows PowerShell. 자세한 내용은 섹션을 참조 하세요 [DCB에 대 한 Windows PowerShell 명령을](#bkmk_wps) 다음 항목을 참조 하는 것 외에도이 항목의에서 뒷부분에 있습니다.
    - [시스템 제공 DCB 구성 요소](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [데이터 센터 브리징 NDIS QoS 요구 사항](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. Windows Server 2016 그룹 정책을 통한 DCB 관리 기능을 제공합니다.

7. Windows Server 2016의 서비스 품질의 공존 지원 \(QoS\) 솔루션입니다.

>[!NOTE]
>모든 RDMA over Converged Ethernet 사용 하기 전에 \(RoCE\) 버전 RDMA의 DCB를 사용 해야 합니다. 인터넷 넓은 영역 RDMA 프로토콜에 대 한 필요는 없지만 \(iWARP\) 네트워크를 테스트 하는 결정에 모든 이더넷\-DCB를 사용 하 여 더 나은 RDMA 기술은 작업을 기반으로 합니다. 이 때문에 DCB를 사용 하 여 iWARP RDMA 배포에 대해 고려해 야 합니다. 자세한 내용은 [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 된 팀 (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)합니다.

##  <a name="practical-applications-of-dcb"></a>DCB의 실제 응용 프로그램

많은 조직에는 큰 파이버 채널 \(FC\) 저장 영역 네트워크 \(SAN\) 저장소 서비스에 대 한 설치 합니다. FC SAN을 설치하려면 서버에는 특수한 네트워크 어댑터가, 네트워크에는 FC 스위치가 필요합니다. 이러한 조직은 일반적으로 사용 이더넷 네트워크 어댑터 및 스위치입니다.

대부분의 경우에서 FC 하드웨어는 대규모의 자본은 이더넷 하드웨어 보다 배포 하기 훨씬 더 비쌉니다. 또한 별도 FC SAN 및 이더넷 네트워크 어댑터 및 스위치 하드웨어 요구 사항을 추가 공간, 전원 및 냉각 기능이 추가 운영 경비가 계속 발생 하는 데이터 센터에 필요 합니다.

비용 측면에서 것이 유리한 해당 FC 기술을 이더넷 해당 병합에 많은 조직에 대 한\-기반 하드웨어 솔루션 저장소와 데이터 네트워킹 서비스를 제공 합니다.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>DCB를 사용 하 여 이더넷에 대 한\-기반의 수렴 된 패브릭을 저장소 및 데이터 네트워킹에 대 한

대규모 FC SAN을 보유 하 고 있지만 FC 기술에 추가로 투자 하지 마이그레이션하려는 조직의 경우, DCB 사용 하면 빌드를 이더넷 기반 저장소와 데이터 네트워킹에 대 한 패브릭 수렴 합니다. DCB 수렴 된 패브릭 향후의 총 소유 비용을 줄일 수 있습니다 \(TCO\) 및 관리를 간소화 합니다.

저장소 솔루션, DCB는 iSCSI 이미 채택한 했거나 도입할 예정인 호스팅 서비스 공급자에 대 한 하드웨어를 제공할 수 있습니다\-성능 격리를 보장 하려면 iSCSI 트래픽에 대 한 대역폭 예약을 지원 합니다. 다른 소유 솔루션과 달리 DCB는 표준 및\-기반-및 따라서 비교적 쉽게 배포 및 다른 유형의 네트워크 환경에서 관리 합니다.

Windows Server 2016\-DCB의 기반된 구현 시 발생할 수 있는 수렴 된 패브릭 솔루션 여러 original equipment manufacturer에서 제공 하는 문제를 대부분 방지할 \(Oem\)합니다.

여러 Oem에서 제공 하는 소유 솔루션 구현의 서로 상호 작용 하지 않고, 하기 어려울 수 있습니다 관리 하 고 일반적으로 다양 한 소프트웨어 유지 관리 일정 해야 합니다. 

반면, Windows Server 2016 DCB는 표준을\-기반, 및 배포 하 고 다른 유형의 네트워크에 DCB를 관리할 수 있습니다.

## <a name="bkmk_wps"></a>DCB에 대 한 Windows PowerShell 명령

Windows Server 2016 및 Windows Server 2012 R2에 대 한 DCB Windows PowerShell 명령이 있습니다. Windows Server 2016에서 Windows Server 2012 R2에 대 한 모든 명령을 사용할 수 있습니다.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB에 대 한 Windows Server 2016 Windows PowerShell 명령

다음 항목에서는 Windows Server 2016에 대 한 모든 데이터 센터 브리징에 대 한 Windows PowerShell cmdlet 설명과 구문을 제공 \(DCB\) 서비스 품질 \(QoS\)\-관련 cmdlet. cmdlet은 cmdlet의 시작 부분에 있는 동사에 따라 사전순으로 나열됩니다.

- [DcbQoS Module](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB에 대 한 Windows Server 2012 R2 Windows PowerShell 명령

다음 항목에서는 Windows Server 2012 R2에 대 한 모든 데이터 센터 브리징에 대 한 Windows PowerShell cmdlet 설명과 구문을 제공 \(DCB\) 서비스 품질 \(QoS\)\-관련 cmdlet. cmdlet은 cmdlet의 시작 부분에 있는 동사에 따라 사전순으로 나열됩니다.

- [데이터 센터 브리징 (DCB) 품질의 Windows PowerShell의 QoS (서비스) Cmdlet](https://technet.microsoft.com/library/hh967440.aspx)
