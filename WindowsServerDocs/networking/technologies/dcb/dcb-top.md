---
title: DCB(데이터 센터 브리징)
description: 이 항목에서는 Windows Server 2016의 데이터 센터 브리징에 대 한 소개 정보를 확인할 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: da58f312-bd3b-4bb6-98ca-6177869dd6ad
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5401f0409ce46e5b7a6da32e1e0a914581956279
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312741"
---
# <a name="data-center-bridging-dcb"></a>DCB\) \(데이터 센터 브리징

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 데이터 센터 브리징 \(DCB\)에 대 한 소개 정보를 사용할 수 있습니다.

DCB은 데이터 센터에서 수렴 된 패브릭을 사용할 수 있도록 하는 IEEE\) 표준 \(IEEE 표준으로, 저장소, 데이터 네트워킹, 클러스터에서 IPC\)를 \(하는 통신\-프로세스 및 관리 트래픽이 모두 동일한 이더넷 네트워크 인프라를 공유 합니다.

>[!NOTE]
>이 항목 외에도 다음과 같은 DCB 설명서를 사용할 수 있습니다.
>
>- [Windows Server 2016 또는 Windows 10에서 DCB 설치](dcb-install.md)
>- [데이터 센터 브리징 관리 (DCB)](dcb-manage.md)

DCB는 특정 유형의 네트워크 트래픽에 대 한 하드웨어\-기반 대역폭 할당을 제공 하며, 우선 순위\-기반 흐름 제어를 사용 하 여 이더넷 전송 안정성을 향상 시킵니다.

트래픽이 운영 체제를 우회 하 고 수렴 형 네트워크 어댑터로 오프 로드 되는 경우 하드웨어\-기반 대역폭 할당은 필수입니다 .이 네트워크 어댑터는 인터넷 소규모 컴퓨터 시스템 인터페이스 \(iSCSI\)를 지원 하 고, 이더넷을 통한 원격 직접 메모리 \(액세스는 RDMA를 통한 RDMA\), 이더넷 \(FCoE\)을 통해 파이버 채널을 지원할 수 있습니다.

파이버 채널 등의 상위 계층 프로토콜에서 무손실 기본 전송을 사용 하는 경우 우선 순위\-기반 흐름 제어를 사용 하는 것이 중요 합니다.

## <a name="dcb-protocols-and-management-options"></a>DCB 프로토콜 및 관리 옵션

DCB는 다음 프로토콜 집합으로 구성 됩니다. 

- 향상 된 전송 서비스\) \(802.1 P 및 802.1 Q 표준을 기반으로 하는 IEEE 802.1 Qaz
- PFS\)\(우선 순위 흐름 제어, IEEE 802.1 Qbb 
- DCB Exchange Protocol \(DCBX\), IEEE 802.1 AB는 802.1 Qaz standard에서 확장 된 것입니다.

DCBX 프로토콜을 사용 하면 스위치에 DCB을 구성할 수 있습니다. 그러면 Windows Server 2016를 실행 하는 컴퓨터와 같은 최종 장치를 자동으로 구성할 수 있습니다.

스위치에서 DCB를 관리 하는 것을 선호 하는 경우 DCB를 Windows Server 2016에 기능으로 설치할 필요가 없지만,이 방법에는 몇 가지 제한 사항이 포함 되어 있습니다.

DCBX은 호스트 네트워크 어댑터에 대 한 필수 클래스 크기 및 PFC 활성화만 알릴 수 있으므로 일반적으로 Windows Server 호스트에는 DCB가 설치 되어 있어야 트래픽이 클래스에 매핑됩니다.

Windows 응용 프로그램은 일반적으로 DCBX 교환에 참여 하도록 설계 되지 않습니다. 따라서 호스트는 네트워크 스위치와 별도로 구성 해야 하지만 동일한 설정을 사용 해야 합니다.

스위치에서 DCB 관리를 선택 하는 경우 Windows PowerShell 명령을 사용 하 여 Windows Server 2016의 구성을 볼 수 있습니다.

##  <a name="important-dcb-functionality"></a>중요 한 DCB 기능

아래 DCB에서 제공하는 기능이 요약되어 있습니다.

1. DCB\-가능 네트워크 어댑터와 DCB\-지원 스위치 간의 상호 운용성을 제공 합니다.

2. 네트워크 어댑터에서 우선 순위\-기반 흐름 제어를 설정 하 여 Windows Server 2016를 실행 하는 컴퓨터와 인접 스위치 간에 무손실 이더넷 전송을 제공 합니다.

3. 는 TC\) \(트래픽 컨트롤에 대역폭을 백분율로 할당 하는 기능을 제공 합니다. 여기서 TC는 802.1 p 트래픽 클래스 \(우선 순위\) 표시기로 구분 되는 하나 이상의 트래픽 클래스로 구성 될 수 있습니다.

4. 서버 관리자 또는 네트워크 관리자가 애플리케이션에서 사용하는 알려진 프로토콜, 알려진 TCP/UDP 포트 또는 NetworkDirect 포트를 기반으로 특정 트래픽 클래스나 우선 순위에 해당 애플리케이션을 할당할 수 있도록 합니다.

5. Windows Server 2016 WMI(Windows Management Instrumentation) \(WMI\) 및 Windows PowerShell을 통한 DCB 관리 기능을 제공 합니다. 자세한 내용은이 항목의 뒷부분에 나오는 [DCB 용 Windows PowerShell 명령](#bkmk_wps) 및 다음 항목을 참조 하세요.
    - [시스템 제공 DCB 구성 요소](https://msdn.microsoft.com/windows/hardware/drivers/network/system-provided-dcb-components)
    - [데이터 센터 브리징에 대 한 NDIS QoS 요구 사항](https://msdn.microsoft.com/windows/hardware/drivers/network/ndis-qos-requirements-for-data-center-bridging)

6. 그룹 정책 Windows Server 2016를 통한 DCB 관리를 제공 합니다.

7. 는 Windows Server 2016 QoS\) 솔루션 \(공존을 지원 합니다.

>[!NOTE]
>수렴 된 이더넷 \(RoCE\) 버전의 RDMA를 통해 RDMA를 사용 하기 전에 DCB를 사용 하도록 설정 해야 합니다. 인터넷 광역 RDMA 프로토콜 \(iWARP\) 네트워크에는 필요 하지 않지만 테스트는 모든 이더넷\-기반 RDMA 기술이 DCB 보다 잘 작동 하는 것으로 확인 되었습니다. 따라서 iWARP RDMA 배포에 DCB를 사용 하는 것이 좋습니다. 자세한 내용은 [RDMA (원격 직접 메모리 액세스) 및 스위치 포함 된 팀 (SET)](../../../virtualization/hyper-v-virtual-switch/RDMA-and-Switch-Embedded-Teaming.md)을 참조 하세요.

##  <a name="practical-applications-of-dcb"></a>DCB의 실용적인 응용 프로그램

많은 조직에는 저장소 서비스에 대 한 파이버 채널 \(FC\) 저장소 영역 네트워크 \(SAN\) 설치를 포함 합니다. FC SAN을 설치하려면 서버에는 특수한 네트워크 어댑터가, 네트워크에는 FC 스위치가 필요합니다. 이러한 조직에서는 일반적으로 이더넷 네트워크 어댑터 및 스위치도 사용 합니다.

대부분의 경우 FC 하드웨어는 이더넷 하드웨어 보다 배포 하는 데 더 많은 비용이 많이 들기 때문에 자본 지출을 크게 증가 합니다. 또한 별도의 이더넷 및 FC SAN 네트워크 어댑터 및 스위치 하드웨어에 대 한 요구 사항에는 데이터 센터에 추가 공간, 전력 및 냉각 용량이 필요 하며,이로 인해 운영 지출을 추가로 진행 됩니다.

비용 측면에서 보면 대부분의 조직에서 FC 기술을 이더넷\-기반 하드웨어 솔루션과 병합 하 여 저장소 및 데이터 네트워킹 서비스를 모두 제공 하는 것이 유리 합니다.

### <a name="using-dcb-for-an-ethernet-based-converged-fabric-for-storage-and-data-networking"></a>저장소 및 데이터 네트워킹용 이더넷\-기반 수렴 패브릭에 대해 DCB 사용

이미 규모가 많은 FC SAN을 보유 하 고 있지만 FC 기술에 대 한 추가 투자를 제외 하려는 조직의 경우 DCB를 사용 하 여 저장소 및 데이터 네트워킹에 대 한 이더넷 기반 수렴 형 패브릭을 구축할 수 있습니다. DCB 수렴 된 패브릭을 통해 TCO\)의 향후 총 \(소유 비용을 줄이고 관리를 간소화할 수 있습니다.

이미 채택 했거나 채택할 계획인 호스팅 서비스 공급자의 경우, DCB는 iscsi 트래픽에 대 한 하드웨어\-보조 대역폭 예약 기능을 제공 하 여 성능 격리를 보장할 수 있습니다. 다른 소유 솔루션과 달리 DCB는 기반으로 하는 표준\-이므로 다른 유형의 네트워크 환경에서 비교적 쉽게 배포 하 고 관리할 수 있습니다.

DCB의 Windows Server 2016\-기반 구현에서는 Oem\)\(여러 원본 장비 제조업체에서 수렴 된 패브릭 솔루션을 제공할 때 발생할 수 있는 많은 문제를 완화 합니다.

여러 Oem에서 제공 하는 소유 솔루션의 구현은 서로 상호 운용할 수 없으며 관리 하기 어렵고 일반적으로 소프트웨어 유지 관리 일정이 서로 다릅니다. 

이와 대조적으로 Windows Server 2016 DCB 표준\-기반으로 하며 다른 유형의 네트워크에서 DCB를 배포 하 고 관리할 수 있습니다.

## <a name="windows-powershell-commands-for-dcb"></a><a name="bkmk_wps"></a>DCB 용 Windows PowerShell 명령

Windows Server 2016 및 Windows Server 2012 r 2에 대 한 Windows PowerShell 명령 DCB 있습니다. Windows server 2016에서 Windows Server 2012 r 2에 대 한 모든 명령을 사용할 수 있습니다.

### <a name="windows-server-2016-windows-powershell-commands-for-dcb"></a>DCB 용 windows Server 2016 Windows PowerShell 명령

Windows Server 2016에 대 한 다음 항목에서는 모든 데이터 센터 브리징 \(DCB\) 서비스 품질 \(QoS\)\-특정 cmdlet에 대 한 Windows PowerShell cmdlet 설명 및 구문을 제공 합니다. 또한 cmdlet의 첫 부분에 있는 동사를 기준으로 알파벳 순서에 따라 cmdlet을 나열합니다.

- [DcbQoS 모듈](https://technet.microsoft.com/itpro/powershell/windows/dcbqos/dcbqos)

### <a name="windows-server-2012-r2-windows-powershell-commands-for-dcb"></a>DCB 용 windows Server 2012 R2 Windows PowerShell 명령

Windows Server 2012 r 2의 다음 항목에서는 모든 데이터 센터 브리징 \(DCB\) 서비스 품질 \(QoS\)\-특정 cmdlet에 대 한 Windows PowerShell cmdlet 설명 및 구문을 제공 합니다. 또한 cmdlet의 첫 부분에 있는 동사를 기준으로 알파벳 순서에 따라 cmdlet을 나열합니다.

- [Windows PowerShell의 DCB (데이터 센터 브리징) QoS (서비스 품질) Cmdlet](https://technet.microsoft.com/library/hh967440.aspx)
