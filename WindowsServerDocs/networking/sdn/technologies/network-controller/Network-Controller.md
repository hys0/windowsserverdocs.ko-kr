---
title: 네트워크 컨트롤러
description: 이 항목에서는 네트워크 컨트롤러 Windows Server 2016에 대 한 개요입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 31f3fa4e-cd25-4bf3-89e9-a01a6cec7893
ms.author: pashort
author: shortpatti
ms.openlocfilehash: acb9abbd716e9930fb01431e7004abb72a7da10c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller"></a>네트워크 컨트롤러

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

새로운 Windows Server 2016 네트워크 컨트롤러, 프로그래밍 중앙 집중식 관리, 구성 하 고, 모니터, 데이터 센터에 인프라 가상 및 실제 네트워크 문제를 해결 하려면 자동화 지점의 제공 합니다. 

네트워크 컨트롤러를 사용 하 여 네트워크 디바이스 및 서비스를 수동으로 구성 수행 하는 대신 네트워크 infrastructure 구성을 자동 수 있습니다.

> [!NOTE]
> 이 항목에서는 뿐만 아니라 다음 네트워크 컨트롤러 설명서를 사용할 수 있습니다.
> - [네트워크 컨트롤러 높은 공급 일](network-controller-high-availability.md)
> - [설치 및 네트워크 컨트롤러 배포 하기 위한 준비 요구 사항](../../plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)  
> - [네트워크 컨트롤러를 사용 하 여 Windows PowerShell 배포](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)  
> - [네트워크 컨트롤러 서버 역할 서버 관리자를 사용 하 여 설치](Install-the-Network-Controller-server-role-using-Server-Manager.md)
> - [이후 Post-Deployment 네트워크 컨트롤러 단계](post-deploy-steps-nc.md)
> - [네트워크 컨트롤러 Cmdlet](https://technet.microsoft.com/library/mt576401.aspx) 

## <a name="bkmk_overview"></a>네트워크 컨트롤러 개요

네트워크 컨트롤러는 많이 사용 가능 하 고 확장 가능 하도록 만들기 서버 역할을 하 고 제공 하나 응용 프로그램 프로그래밍 인터페이스 네트워크와 통신 하도록 네트워크 컨트롤러 수 있도록 해 주는 \(API\) 및 네트워크 컨트롤러와 통신할 수 있도록 두 번째 API 합니다.

네트워크 컨트롤러 도메인 및 비 도메인 환경에 배포할 수 있습니다. 도메인 환경에서 네트워크 컨트롤러 네트워크 디바이스 및 사용자가 사용 하 여 인증 Kerberos; 비 도메인 환경 인증을 위한 인증서 배포 해야 합니다.

>[!IMPORTANT]
>네트워크 컨트롤러 서버 역할 실제 호스트에서를 배포 하지 않습니다. Hyper-v 가상 컴퓨터가에 네트워크 컨트롤러 서버 역할 설치 해야 하는 배포 하는 네트워크 컨트롤러, Hyper-v 호스트에 설치 되어 있는 \(VM\) 합니다. 네트워크 컨트롤러 Vm에서 세 가지 Hyper\ V 호스트에서를 설치한 후 Windows PowerShell 명령을 사용 하 여 네트워크 컨트롤러 호스트 추가 하 여 소프트웨어 네트워킹 정의 \(SDN\)에 대해 Hyper\ V 호스트를 설정 해야 **새로 NetworkControllerServer**합니다. 이렇게 하면 SDN 소프트웨어 부하 분산 기능을 사용할 수 있게 됩니다. 자세한 내용은 참조 [새로 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)합니다.

네트워크 컨트롤러 Southbound API를 사용 하 여 네트워크 디바이스, 서비스 및 구성 요소와 통신 합니다. Southbound api를 네트워크 컨트롤러 네트워크 디바이스 검색, 검색 및 수 있습니다 서비스 구성 모든 네트워크에 대 한 필요한 정보를 수집 합니다. 또한 Southbound API 네트워크 인프라 구성 변경 내용이 등으로 정보를 보낼 보도 네트워크 컨트롤러를 제공 합니다.

네트워크 컨트롤러 Northbound API 네트워크 컨트롤러에서 네트워크 정보를 수집 하 고 모니터링 하 고 구성 네트워크를 사용 하는 기능을 제공 합니다.

네트워크 컨트롤러 Northbound API 구성, 모니터링 하 고, 문제 해결, 그래픽 사용자 인터페이스 System Center 가상 컴퓨터 Manager 등 사용 하 여 Windows PowerShell, 표시 상태 전송 \(REST\) API 또는 응용 프로그램을 관리를 사용 하 여 새 디바이스 네트워크에 배포할 수 있습니다.

>[!NOTE]
>네트워크 컨트롤러 Northbound API 나머지 인터페이스도 구현 됩니다.

네트워크 컨트롤러를 사용 하면 구성 하 고, 모니터, 프로그램, 네트워크 infrastructure 통제 있는 문제를 해결 하기 때문에 System Center 가상 컴퓨터 Manager \(SCVMM\) System Center Operations Manager \(SCOM\) 등의 관리 응용 프로그램을 사용 하 여 네트워크 컨트롤러와 datacenter 네트워크를 관리할 수 있습니다.

Windows PowerShell, REST API, 또는 관리 응용 프로그램을 사용 하 여 네트워크 컨트롤러 다음 실제 및 가상 네트워크 infrastructure 관리에 사용할 수 있습니다.

- Hyper-v Vm 및 가상 스위치

- 방화벽 데이터 센터

- 원격 액세스 서비스 \(RAS\) 넌 게이트웨이, 가상 게이트웨이 및 게이트웨이 풀

- 부하 분산 소프트웨어가

다음 그림에서는 관리자 네트워크 컨트롤러와 직접 상호 작용 하는 관리 도구를 사용 합니다. 네트워크 컨트롤러 가상 및 물리적 인프라 관리 도구를 포함 하 여 네트워크 인프라에 대 한 정보를 제공 고 도구를 사용 하는 경우 작업 관리자가에 따라 구성 변경 합니다.  

![네트워크 컨트롤러 개요](../../../media/Network-Controller/NetController_overview.png)  

Hyper-v 가상 컴퓨터가에서 네트워크 컨트롤러 서버 역할을 실행할 수를 테스트 랩 환경에서 네트워크 컨트롤러를 배포 하는 경우 \(VM\) Hyper-v 호스트에 설치 되어 있는 합니다.

더 많은 데이터 센터에 높은 가용성에 대 한 3 개 이상의 Hyper-v 호스트에 설치 되어 있는 세 개의 Vm를 사용 하 여 클러스터를 배포할 수 있습니다. 자세한 내용은 참조 [네트워크 컨트롤러 높은 가용성](network-controller-high-availability.md)합니다.

## <a name="bkmk_features"></a>네트워크 컨트롤러 기능

다음 네트워크 컨트롤러 기능을 구성 하 고 관리 가상 및 물리적 네트워크 디바이스 및 서비스 사용 합니다.  
  
-   [방화벽 관리](#bkmk_firewall)  
  
-   [소프트웨어 부하 분산 관리](#bkmk_slb)  
  
-   [가상 네트워크 관리](#bkmk_virtual)  
  
-   [RAS 게이트웨이 관리](#bkmk_gateway)

>[!IMPORTANT]
>네트워크 컨트롤러 백업 및 복원 현재 Windows Server 2016에서 제공 되지 않습니다.
  
### <a name="bkmk_firewall"></a>방화벽 관리

네트워크 컨트롤러 기능이 구성 하 고 Vm 작업에 대 한 방화벽 액세스 제어 규칙 허용 거부 이스트/서쪽 및 사용자 데이터 센터에 북쪽/사우스 네트워크 교통 관리할 수 있습니다. 방화벽 규칙 작업 Vm vSwitch 포트에 연결 되어 및 작업 데이터 센터에 걸쳐 배포 되는 때문입니다. Northbound API를 사용 하 여 작업 VM에서에서 발신 교통량 방화벽 규칙 정의할 수 있습니다. 각 방화벽 규칙을 허용 또는 규칙 거부 된 트래픽을 기록 구성할 수 있습니다.  

자세한 내용은 참조 [Datacenter 방화벽 개요](../../../sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)합니다.

### <a name="bkmk_slb"></a>소프트웨어 부하 분산 관리

이 네트워크 컨트롤러 기능 가용성 우선과 확장성 같은 작업을 호스팅할 여러 서버를 사용할 수 있습니다.  
  
자세한 내용은 참조 [부하 분산 소프트웨어가 & #40; SLB & #41; SDN에 대 한](../../../sdn/technologies/network-function-virtualization/Software-Load-Balancing--SLB--for-SDN.md)합니다.  
  
### <a name="bkmk_virtual"></a>가상 네트워크 관리

이 네트워크 컨트롤러 기능 배포 하 고 구성할 Hyper-v 네트워크 가상화, 가상 네트워크 어댑터에 개별 Vm Hyper-v 가상 스위치를 포함 하 고 저장 및 가상 네트워크 정책 배포할 수 있습니다.

네트워크 컨트롤러 네트워크 가상화 일반 경로 캡슐화 (NVGRE) 및 가상 Extensible 네트워크 (VXLAN)을 지원합니다.

### <a name="bkmk_gateway"></a>RAS 게이트웨이 관리

네트워크 컨트롤러 기능이 배포 구성 하 고 Vm (가상 컴퓨터) RAS 게이트웨이 풀의 회원 하 여 테 넌 게이트웨이 서비스를 제공 하는 관리할 수 있습니다. 네트워크 컨트롤러 배포 Vm RAS 게이트웨이 다음 게이트웨이 기능을 실행 하는 자동으로 있습니다.

> [!NOTE]
> RAS 게이트웨이 System Center 가상 컴퓨터 Manager, Windows Server 게이트웨이 이라고 합니다.

- 추가 하 고 게이트웨이 Vm 클러스터에서 제거 하 고 필요한 백업 수준을 지정 합니다.

- 원격 테 네트워크와 받는 데이터 센터에 사이트 가상 개인 네트워크 (VPN) 게이트웨이 연결 합니다.

- 사이트에서 VPN 게이트웨이 원격 테 네트워크와 연결이 일반 경로 캡슐화 (GRE)를 사용 하 여 데이터 센터 합니다.

- 3 전달 기능을 계층입니다.

- 테두리 게이트웨이 프로토콜 (BGP) 경로 테 넌의 VM 네트워크 사이의 원격 광고주 사이트 네트워크 교통 경로 관리할 수 있습니다.

네트워크 컨트롤러 별도 게이트웨이에 거주의 서로 다른 연결 배치할 수 있습니다. 모든 게이트웨이의 연결에 대 한 단일 공개 IP 사용 하거나 연결 하위 집합에 대 한 다른 공개 ip 수 있습니다. 네트워크 컨트롤러 기록 게이트웨이 구성과 감사 및 문제 해결을 위해 사용할 수 있는 상태 변경 합니다.

에 대 한 자세한 내용은 BGP, [테두리 게이트웨이 프로토콜 & #40; BGP & #41; ](../../../../remote/remote-access/bgp/Border-Gateway-Protocol-BGP.md).

에 대 한 자세한 내용은 RAS 게이트웨이, [SDN RAS 게이트웨이](../../../sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)합니다.

## <a name="network-controller-deployment-options"></a>네트워크 컨트롤러 배포 옵션

네트워크 컨트롤러 System Center 가상 컴퓨터 Manager \(VMM\)를 사용 하 여 배포를 참조 [VMM 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)합니다.

네트워크 컨트롤러 스크립트를 사용 하 여 배포를 참조 [는 소프트웨어 정의 네트워크 인프라를 사용 하 여 스크립트 배포](../../deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)합니다.

네트워크 컨트롤러를 사용 하 여 Windows PowerShell 배포 참조 [Windows PowerShell를 사용 하 여 배포 네트워크 컨트롤러](../../deploy/Deploy-Network-Controller-using-Windows-PowerShell.md)
