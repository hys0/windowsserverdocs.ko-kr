---
title: Hyper-V 가상 스위치
description: 이 항목에서는 Windows Server 2016에서 Hyper-v 가상 스위치 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 17962b9bbb90a5ea1b6a4a303c64d72f74be37b5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860924"
---
# <a name="hyper-v-virtual-switch"></a>Hyper-V 가상 스위치

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 가상 컴퓨터를 연결 하는 기능을 제공 하는 Hyper-v 가상 스위치에 대 한 개요를 제공 \(Vm\) Hyper 외부 네트워크에\-조직의 인트라넷을 포함 하 여 V 호스트 와 인터넷을 추가 합니다. 

하이퍼를 실행 하는 서버에서 가상 네트워크에 연결할 수도 있습니다\-소프트웨어 정의 네트워킹 배포 하는 경우 V \(SDN\)합니다.

> [!NOTE]  
> 이 항목 외에 다음과 같은 Hyper-v 가상 스위치 설명서는 사용할 수 있습니다.  
>   
> - [Hyper-v 가상 스위치 관리](Manage-Hyper-V-Virtual-Switch.md) 
> - [원격 직접 메모리 액세스 (RDMA) 및 스위치 포함 팀 (SET)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Windows PowerShell의 네트워크 스위치 팀 Cmdlet](https://technet.microsoft.com/library/jj553812.aspx)
> - [VMM 2016의 새로운 기능](https://docs.microsoft.com/system-center/vmm/whats-new#networking)
> - [VMM 네트워킹 패브릭 설정](https://docs.microsoft.com/system-center/vmm/manage-networks)
> - [VMM 2012를 사용 하 여 네트워크를 만들기](https://social.technet.microsoft.com/wiki/contents/articles/3140.create-networks-with-vmm-2012.aspx)  
> - [Hyper-V: Vlan 및 VLAN 태그 구성](https://social.technet.microsoft.com/wiki/contents/articles/1306.hyper-v-configure-vlans-and-vlan-tagging.aspx)  
> - [Hyper-V: 제 3 자 확장이 필요한 경우 WFP 가상 스위치 확장을 활성화 해야](https://social.technet.microsoft.com/wiki/contents/articles/13071.hyper-v-the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions.aspx)
>
> 다른 네트워킹 기술에 대 한 자세한 내용은 참조 하세요. [Windows Server 2016에서 네트워킹](https://docs.microsoft.com/windows-server/networking/networking)합니다.
  
하이퍼\-소프트웨어 기반의 계층 2 이더넷 네트워크 스위치를 사용할 수 있는 V 가상 스위치는 하이퍼에서\-하이퍼를 설치할 때 관리자\-V 서버 역할입니다.

Hyper-v 가상 스위치는 가상 네트워크와 실제 네트워크에 Vm을 연결할 프로그래밍 방식으로 관리 하 고 확장할 수 있는 기능을 포함 합니다. 또한 Hyper-V 가상 스위치를 사용하여 보안, 격리 및 서비스 수준의 정책을 적용할 수 있습니다.  
  
> [!NOTE]  
> Hyper-V 가상 스위치는 이더넷만 지원하고 Infiniband 및 파이버 채널 같은 다른 유선 LAN(Local Area Network) 기술은 지원하지 않습니다.  
  
Hyper-v 가상 스위치는 테 넌 트 격리 기능, 트래픽 셰이핑, 악성 가상 컴퓨터에 대 한 보호를 포함 및 문제 해결을 간소화 합니다. 

네트워크 장치 인터페이스 사양에 대 한 기본 제공 지원을 통해 \(NDIS\) 필터 드라이버 및 Windows 필터링 플랫폼 \(WFP\) 호출 드라이버를 Hyper-v 가상 스위치 독립 소프트웨어 수 있습니다. 공급 업체 \(Isv\) 만들려면 확장 가능한 플러그 인, 향상 된 네트워킹 및 보안 기능을 제공할 수 있는 가상 스위치 확장을 호출 합니다. Hyper-V 가상 스위치에 추가된 가상 스위치 확장은 Hyper-V 관리자의 가상 스위치 관리자 기능에 나열됩니다.
  
다음 그림에서는 VM을 Hyper-v 가상 스위치에 스위치 포트를 통해 연결 된 가상 NIC에  
  
![가상 스위치 연결](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)  
  
Hyper-v 가상 스위치 기능 테 넌 트 격리, 네트워크 트래픽을 셰이핑 및 제어를 적용 하는 것에 대 한 더 많은 옵션을 제공 하 고 악성 Vm 으로부터 측정 보호를 사용 합니다.

>[!NOTE]
> Windows Server 2016에서 가상 NIC 사용 하 여 VM 정확 하 게 최대 처리량에 대 한 표시 가상 NIC 가상 NIC 속도 보려는 **네트워크 연결**원하는 가상 NIC 아이콘을 마우스 오른쪽 단추로 클릭 한 다음 클릭 **상태**합니다. 가상 NIC **상태** 대화 상자가 열립니다. **연결**에 값 **속도** 서버에 설치 된 실제 NIC의 속도 일치 합니다.
  
## <a name="bkmk_apps"></a>Hyper-v 가상 스위치에 대 한 사용

다음은 Hyper-v 가상 스위치에 대 한 일부 사용 사례 시나리오입니다.

**통계 표시**: 호스트된 클라우드 공급업체의 개발자는 Hyper-V 가상 스위치의 현재 상태를 표시하는 관리 패키지를 구현합니다. 관리 패키지는 WMI를 사용하여 스위치 전반의 현재 성능, 구성 설정 및 개별 포트 네트워크 통계를 쿼리할 수 있습니다. 그러면 스위치 상태가 표시되어 관리자가 상태를 즉시 확인할 수 있습니다.  
  
**리소스 추적**: 호스팅 업체는 구성원의 등급에 따라 가격이 책정된 호스팅 서비스를 판매합니다. 다양한 구성원 등급에는 여러 네트워크 성능 수준이 포함됩니다. 관리자는 네트워크 가용성의 균형을 맞추는 방식으로 SLA에 따라 리소스를 할당합니다. 관리자는 가상 머신 큐 (VMQ) 또는 IOV 채널에 할당 된 가상 머신 (VM)의 수 및 할당 된 대역폭의 현재 사용량 같은 정보에 프로그래밍 방식으로 추적 합니다. 이 프로그램에서는 이중 항목 추적이나 리소스에 할당된 VM당 리소스뿐만 아니라 사용 중인 리소스에 대해서도 정기적으로 기록합니다.  
  
**스위치 확장 순서 관리**: 기업은 트래픽을 Hyper-V 호스트 확장을 설치해 트래픽을 모니터링하고 침입 검색을 보고합니다. 유지 관리 작업 중 일부 확장이 업데이트될 수 있으며 이로 인해 확장의 순서가 변경됩니다. 업데이트 후 확장의 순서를 다시 지정하도록 간단한 스크립트 프로그램이 실행됩니다.  
  
**VLAN ID를 관리 확장 전달**: 주요 스위치 업체에서는 모든 네트워킹 정책에 적용되는 전달 확장을 구축하고 있습니다. 관리되는 한 가지 요소는 VLAN(Virtual Local Area Network) ID입니다. 가상 스위치는 VLAN에 대한 제어를 전달 확장으로 넘깁니다. 프로그래밍 방식으로 스위치 업체의 설치는 Windows Management Instrumentation (WMI) 응용 프로그래밍 인터페이스 (API)에서는 투명성이 켜진는 호출 된 Hyper-v 가상 스위치로 전달 하 고 VLAN 태그 작업도 발생 하지 않도록 명령 합니다.  
  
## <a name="bkmk_func"></a>Hyper-v 가상 스위치 기능
 
몇 가지 주요 기능이 다음 Hyper-V 가상 스위치에 포함되어 있습니다.  
  
-   **ARP/ND 침입 (스푸핑) 방지**: 다른 VM의 IP 주소를 훔치기 위해 ARP(주소 확인 프로토콜) 스푸핑을 사용하는 악성 VM으로부터 보호할 수 있습니다. IPv6에 대한 ND(네트워크 환경 검색) 스푸핑을 이용한 공격을 방지할 수 있습니다.  
  
-   **DHCP 가드 보호**: man-in-the-middle 공격에서 DHCP(Dynamic Host Configuration Protocol) 서버로 이용되는 악성 VM으로부터 보호할 수 있습니다.  
  
-   **포트 Acl**: MAC(미디어 Access Control) 또는 IP(인터넷 프로토콜) 주소/범위를 바탕으로 트래픽 필터링이 제공되므로 Virtual Network 격리를 설정할 수 있습니다.  
  
-   **VM에 대 한 트렁크 모드**: 관리자가 특정 VM을 가상 어플라이언스로 설정한 다음 다양한 VLAN에서 비롯된 트래픽이 해당 VM으로 향하도록 할 수 있습니다.  
  
-   **네트워크 트래픽 모니터링**: 관리자가 네트워크 스위치를 트래버스하고 있는 트래픽을 검토할 수 있습니다.  
  
-   **격리 된 (개인) VLAN**: 관리자가 여러 VLAN의 트래픽을 격리할 수 있으므로 격리된 테넌트 커뮤니티를 더욱 편리하게 설정할 수 있습니다.  
  
다음은 Hyper-V 가상 스위치를 더욱 효과적으로 사용할 수 있도록 해주는 기능입니다.  
  
-   **대역폭 제한 및 버스트 지원**: 대역폭 최소량을 통해 예약된 대역폭의 양을 보장합니다. 대역폭 최대량은 VM이 사용할 수 있는 최대 대역폭의 양을 정의합니다.  
  
-   **알림 ECN (explicit) 표시 지원**:  ECN 표시, 라고도 센터 DCTCP (Data), 실제 스위치 있으며 트래픽 흐름 스위치의 버퍼 리소스가 있도록 하는 운영 체제 자원이 소모는 결과에서 트래픽 처리량이 늘어납니다.  
  
-   **진단**: 진단을 통해 가상 스위치를 통과하는 패킷과 이벤트를 손쉽게 추적하고 모니터링할 수 있습니다.
