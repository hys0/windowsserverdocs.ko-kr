---
title: Hyper-V 가상 스위치
description: 이 항목에서는 Windows Server 2016의 Hyper-v 가상 스위치에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 398440ac-5988-41ce-b91e-eab343a255d3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fb2ebf485b5004e457558fc16d8535662c0c5ff2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80307988"
---
# <a name="hyper-v-virtual-switch"></a>Hyper-V 가상 스위치

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 hyper-v 가상 스위치에 대 한 개요를 제공 합니다 .이 스위치를 사용 하면 가상 컴퓨터 \(Vm\)를 조직의 인트라넷과 인터넷을 포함 하 여\-Hyper-v 호스트 외부의 네트워크에 연결할 수 있습니다. 

또한 SDN\)소프트웨어 정의 네트워킹 \(배포할 때 하이퍼\-V를 실행 하는 서버의 가상 네트워크에 연결할 수 있습니다.

> [!NOTE]  
> 이 항목 외에 다음과 같은 Hyper-v 가상 스위치 설명서도 사용할 수 있습니다.  
>   
> - [Hyper-V 가상 스위치 관리](Manage-Hyper-V-Virtual-Switch.md) 
> - [RDMA(원격 직접 메모리 액세스) 및 SET(Switch Embedded Teaming)](RDMA-and-Switch-Embedded-Teaming.md)
> - [Windows PowerShell의 네트워크 스위치 팀 Cmdlet](https://technet.microsoft.com/library/jj553812.aspx)
> - [VMM 2016의 새로운 기능](https://docs.microsoft.com/system-center/vmm/whats-new#networking)
> - [VMM 네트워킹 패브릭 설정](https://docs.microsoft.com/system-center/vmm/manage-networks)
> - [VMM 2012을 사용 하 여 네트워크 만들기](https://social.technet.microsoft.com/wiki/contents/articles/3140.create-networks-with-vmm-2012.aspx)  
> - [Hyper-v: Vlan 및 VLAN 태깅 구성](https://social.technet.microsoft.com/wiki/contents/articles/1306.hyper-v-configure-vlans-and-vlan-tagging.aspx)  
> - [Hyper-v: 타사 확장 프로그램에 필요한 경우 WFP 가상 스위치 확장을 사용 하도록 설정 해야 합니다.](https://social.technet.microsoft.com/wiki/contents/articles/13071.hyper-v-the-wfp-virtual-switch-extension-should-be-enabled-if-it-is-required-by-third-party-extensions.aspx)
>
> 다른 네트워킹 기술에 대 한 자세한 내용은 [Windows Server 2016의 네트워킹](https://docs.microsoft.com/windows-server/networking/networking)을 참조 하세요.
  
하이퍼\-V 가상 스위치는 하이퍼\-V 서버 역할을 설치할 때 하이퍼\-V Manager에서 사용할 수 있는 소프트웨어 기반의 계층 2 이더넷 네트워크 스위치입니다.

Hyper-v 가상 스위치에는 가상 네트워크와 실제 네트워크에 Vm을 연결 하는 프로그래밍 방식으로 관리 및 확장 가능한 기능이 포함 되어 있습니다. 또한 Hyper-V 가상 스위치를 사용하여 보안, 격리 및 서비스 수준의 정책을 적용할 수 있습니다.  
  
> [!NOTE]  
> Hyper-V 가상 스위치는 이더넷만 지원하고 Infiniband 및 파이버 채널 같은 다른 유선 LAN(Local Area Network) 기술은 지원하지 않습니다.  
  
Hyper-v 가상 스위치는 테 넌 트 격리 기능, 트래픽 셰이핑, 악성 가상 컴퓨터에 대 한 보호 및 간소화 된 문제 해결을 포함 합니다. 

네트워크 장치 인터페이스 사양 \(NDIS\) 필터 드라이버 및 Windows 필터링 플랫폼 \(WFP\) 콜아웃 드라이버를 기본적으로 지 원하는 Hyper-v 가상 스위치를 사용 하 여 Isv \(독립 소프트웨어 공급 업체\) 가상 스위치 확장 이라고 하는 확장 가능한 플러그 인을 만들어 향상 된 네트워킹 및 보안 기능을 제공할 수 있습니다. Hyper-V 가상 스위치에 추가된 가상 스위치 확장은 Hyper-V 관리자의 가상 스위치 관리자 기능에 나열됩니다.
  
다음 그림에서 VM에는 스위치 포트를 통해 Hyper-v 가상 스위치에 연결 된 가상 NIC가 있습니다.  
  
![가상 스위치 연결](../media/Hyper-V-Virtual-Switch/Vswitch_01.jpg)  
  
Hyper-v 가상 스위치 기능을 통해 테 넌 트 격리를 적용 하 고, 네트워크 트래픽을 셰이핑 및 제어 하며, 악성 Vm에 대 한 보호 조치를 사용할 수 있습니다.

>[!NOTE]
> Windows Server 2016에서는 가상 NIC를 사용 하는 VM에 가상 NIC의 최대 처리량이 정확 하 게 표시 됩니다. **네트워크 연결**의 가상 nic 속도를 확인 하려면 원하는 가상 nic 아이콘을 마우스 오른쪽 단추로 클릭 한 다음 **상태**를 클릭 합니다. 가상 NIC **상태** 대화 상자가 열립니다. **연결**에서 **속도** 값은 서버에 설치 된 실제 NIC의 속도와 일치 합니다.
  
## <a name="uses-for-hyper-v-virtual-switch"></a><a name="bkmk_apps"></a>Hyper-v 가상 스위치에 사용

다음은 Hyper-v 가상 스위치에 대 한 몇 가지 사용 사례 시나리오입니다.

**통계 표시**: 호스팅된 클라우드 공급 업체의 개발자는 hyper-v 가상 스위치의 현재 상태를 표시 하는 관리 패키지를 구현 합니다. 관리 패키지는 WMI를 사용하여 스위치 전반의 현재 성능, 구성 설정 및 개별 포트 네트워크 통계를 쿼리할 수 있습니다. 그러면 스위치 상태가 표시되어 관리자가 상태를 즉시 확인할 수 있습니다.  
  
**리소스 추적**: 호스팅 회사는 멤버 자격 수준에 따라 가격이 책정 된 호스팅 서비스를 판매 합니다. 다양한 구성원 등급에는 여러 네트워크 성능 수준이 포함됩니다. 관리자는 네트워크 가용성의 균형을 맞추는 방식으로 SLA에 따라 리소스를 할당합니다. 관리자는 할당 된 대역폭의 현재 사용량과 VMQ (가상 머신 큐) 또는 VM (가상 머신 큐)에 할당 된 가상 머신 (VM)의 수와 같은 정보를 프로그래밍 방식으로 추적 합니다. 이 프로그램에서는 이중 항목 추적이나 리소스에 할당된 VM당 리소스뿐만 아니라 사용 중인 리소스에 대해서도 정기적으로 기록합니다.  
  
**스위치 확장 순서 관리**: 엔터프라이즈는 트래픽을 모니터링 하 고 침입 감지를 보고 하기 위해 hyper-v 호스트에 확장을 설치 했습니다. 유지 관리 작업 중 일부 확장이 업데이트될 수 있으며 이로 인해 확장의 순서가 변경됩니다. 업데이트 후 확장의 순서를 다시 지정하도록 간단한 스크립트 프로그램이 실행됩니다.  
  
**전달 확장이 VLAN ID를 관리**합니다. 주요 스위치 회사는 네트워킹에 모든 정책을 적용 하는 전달 확장을 구축 하 고 있습니다. 관리되는 한 가지 요소는 VLAN(Virtual Local Area Network) ID입니다. 가상 스위치는 VLAN에 대한 제어를 전달 확장으로 넘깁니다. 스위치 회사의 설치 프로그램은 투명성을 설정 하 여 Hyper-v 가상 스위치를 전달 하 고 VLAN 태그에 대해 아무 작업도 수행 하지 않도록 하는 WMI (WMI(Windows Management Instrumentation)) API (응용 프로그래밍 인터페이스)를 프로그래밍 방식으로 호출 합니다.  
  
## <a name="hyper-v-virtual-switch-functionality"></a><a name="bkmk_func"></a>Hyper-v 가상 스위치 기능
 
몇 가지 주요 기능이 다음 Hyper-V 가상 스위치에 포함되어 있습니다.  
  
-   **Arp/ND 손상 (스푸핑) 방지**: 다른 VM의 IP 주소를 훔 치기 위해 Arp (주소 확인 프로토콜) 스푸핑을 사용 하는 악성 VM에 대 한 보호를 제공 합니다. IPv6에 대한 ND(네트워크 환경 검색) 스푸핑을 이용한 공격을 방지할 수 있습니다.  
  
-   **Dhcp 가드 보호**: 메시지 가로채기 (man-in-the-middle) 공격을 위해 스스로를 DHCP (Dynamic Host Configuration Protocol) 서버로 나타내는 악의적인 VM 으로부터 보호 합니다.  
  
-   **포트 acl**: MAC (미디어 Access Control) 또는 IP (인터넷 프로토콜) 주소/범위를 기반으로 하는 트래픽 필터링을 제공 하 여 가상 네트워크 격리를 설정할 수 있습니다.  
  
-   **VM에 대 한 트렁크 모드**: 관리자가 특정 vm을 가상 어플라이언스로 설정한 다음 다양 한 vlan에서 해당 vm으로 트래픽을 보낼 수 있습니다.  
  
-   **네트워크 트래픽 모니터링**: 관리자가 네트워크 스위치를 통과 하는 트래픽을 검토할 수 있습니다.  
  
-   **격리 된 (개인) vlan**: 관리자가 여러 vlan에서 트래픽을 분리 하 여 격리 된 테 넌 트 커뮤니티를 더욱 쉽게 설정할 수 있습니다.  
  
다음은 Hyper-V 가상 스위치를 더욱 효과적으로 사용할 수 있도록 해주는 기능입니다.  
  
-   **대역폭 제한 및 버스트 지원**: 대역폭 최소값은 예약 된 대역폭의 양을 보장 합니다. 대역폭 최대량은 VM이 사용할 수 있는 최대 대역폭의 양을 정의합니다.  
  
-   **ECN (명시적 정체 알림) 표시 지원**: Dctcp (Data center tcp) 라고도 하는 ECN 표시를 사용 하면 스위치의 버퍼 리소스가 장애 유발 되지 않도록 물리적 스위치와 운영 체제에서 트래픽 흐름을 조정할 수 있으므로 트래픽 처리량이 증가 합니다.  
  
-   **진단**: 진단을 통해 가상 스위치를 통해 이벤트와 패킷을 쉽게 추적 하 고 모니터링할 수 있습니다.
