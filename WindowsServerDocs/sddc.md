---
title: Windows Server 소프트웨어 정의 데이터 센터
description: Windows Server SDDC 개요
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: SDDC
ms.tgt_pltfrm: na
ms.topic: get-started article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 08/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c8c530568d7f336ae2bd4981c02093fe580d9b7
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121462"
---
# Windows Server 소프트웨어 정의 데이터 센터

>적용 대상: WindowsServer 2016

![](media/sddc/heading.png)

## Windows Server 소프트웨어 정의 데이터 센터란 무엇입니까? ##

SDDC(소프트웨어 정의 데이터 센터)는 모든 인프라가 가상화되는 데이터 센터를 의미하는 일반적 업계 용어입니다. 가상화가 핵심이고, 이는 데이터 센터의 하드웨어 및 소프트웨어가 기존의 일대일 비율을 넘어 확장한다는 의미입니다. 하드웨어, 운영 체제 및 응용 프로그램을 에뮬레이트하는 소프트웨어 하이퍼바이저는 실제 하드웨어에서 추상화될 수 있고, 곱하여 프로세서, 메모리, I/O 및 네트워크의 탄력적 리소스 풀이 될 수도 있습니다.
 
Microsoft의 SDDC 구현에는 이 문서에 강조된 Windows Server 기술이 포함되어 있습니다. 우선 네트워킹 및 저장소가 빌드되는 가상화 플랫폼을 제공하는 Hyper-V 하이퍼바이저입니다. 가상화 인프라 고유의 어려움을 위해 개발된 보안 기술은 내부 및 외부 위협을 완화합니다. PowerShell이 Windows Server에 기본 제공되고, [System Center](https://docs.microsoft.com/system-center/) 및/또는 [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)가 추가되면서 프로비전, 배포, 구성 및 관리를 프로그래밍하고 자동화할 수 있습니다.

Windows Server 및 System Center에 기본 제공되는 기술은 Windows Server SDDC 환경의 주요 구성 요소입니다. 하지만 가상화된 플랫폼이라 해도 여전히 올바른 하드웨어가 필요합니다. **WSSD(Windows Server 소프트웨어 정의) 솔루션** 프로그램에 참여하는 Microsoft 파트너는 엔터프라이즈가 올바른 하드웨어를 취득하고 바로 설정 및 실행하도록 도울 수 있습니다.

![](media/sddc/video.png)**[이 동영상을 시청하여 Microsoft의 SDDC에 대해 알아보기](https://mva.microsoft.com/en-US/training-courses/whats-new-in-windows-server-2016-16457?l=YcsJR6sXC_1006218965)**

![](media/sddc/poster-ico.png)**[이 페이지의 포스터 크기 .pdf 파일 다운로드](https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs/media/sddc/sddc_poster_0801417_ANSI-E.pdf)**


![](media/sddc/spacer1.png)<a href="https://github.com/MicrosoftDocs/windowsserverdocs/blob/master/WindowsServerDocs//media/sddc/sddc_poster_0801417_ANSI-E.pdf"><img src="media/sddc/poster.png"></a>


## WSSD(Windows Server 소프트웨어 정의) 솔루션 ##
올바른 하드웨어 인프라에 Windows Server 소프트웨어 정의 데이터 센터를 빌드하는 것이 성공을 향한 중요한 첫 단계입니다. 그런 이유로 인해 **DataON**, **Fujitsu**, **Lenovo**, **QCT**, **SuperMicro**, **Hewlett Packard Enterprise** 및 **Dell EMC**와 파트너 관계를 구축해 Microsoft 검증 SDDC 디자인 및 배포에 대한 모범 사례를 만들었습니다. Microsoft 파트너는 Windows Server 2016에서 작동하여 고성능, 하이퍼 컨버지드, 저장소 및 네트워킹 인프라를 제공하는 다양한 WSSD(Windows Server 소프트웨어 정의) 솔루션을 제공합니다. 하이퍼 컨버지드 솔루션은 개선된 데이터 센터 인텔리전스 및 제어를 위해 컴퓨팅, 저장소 및 네트워킹을 업계 표준 서버 및 구성 요소에 통합합니다.



![](media/sddc/learn.png)**[WSSD 솔루션에 대한 자세한 정보](https://www.microsoft.com/en-us/cloud-platform/software-defined-datacenter)**

## Windows Server 가상화 기술 ##

이 항목의 나머지 부분에서는 Windows Server SDDC 기술 목록을 보여주고 각 기술에 대한 설명서 링크를 제공합니다. 아래 표에 기술이 나열되어 있습니다.

![](media/sddc/table.png)

![](media/sddc/virtualize.png)

### Windows Server, 하이퍼 컨버지드 ###

Windows Server 가상화 기술은 보안, 확장성 및 안정성을 개선하는 Hyper-V, Hyper-V Virtual Switch 및 Guarded Fabric and Shielded Virtual Machines(VMs)의 업데이트를 포함합니다. 장애 조치(failover) 클러스터링, 네트워킹 및 저장소 업데이트를 통해 Hyper-V와 함께 사용될 때 이러한 기술을 더욱 쉽게 배포 및 관리합니다.

![](media/sddc/spacer1.png)![](media/sddc/hyper-converged.png)

![](media/sddc/learn.png)**[Windows Server, 하이퍼 컨버지드에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/get-started/what-s-new-in-windows-server-2016#computevirtualizationvirtualizationmd)**
 
### Hyper-V 하이퍼바이저 ###

Hyper-V는 Windows를 위한 하이퍼바이저 기반 가상화 기술입니다. 하이퍼바이저는 가상화의 핵심입니다. 격리된 여러 운영 체제가 단일 하드웨어 플랫폼을 공유할 수 있게 해주는 프로세서 관련 가상화 플랫폼입니다.

![](media/sddc/spacer1.png)![](media/sddc/hypervisor.png)

![](media/sddc/learn.png)**[Hyper-V 하이퍼바이저에 대해 자세히 알아보기](https://www.microsoft.com/en-us/cloud-platform/server-virtualization)**

### 게스트 클러스터링(공유 VHDX 포함) ###

![](media/sddc/virtualize-line.png)

유연하고 보안이 뛰어나면서 기본 저장소 토폴로지에 바인딩되지 않는 공유 VHDX는 게스트 OS에 물리적 기본 저장소를 제공할 필요성을 없앱니다. 새로운 공유 VHDX는 온라인 크기 조정을 지원합니다.

![](media/sddc/spacer1.png)![](media/sddc/cluster.png)

- 공유 VHDX는 블록 저장소의 CSV(클러스터링된 공유 볼륨), 또는 SMB 파일 기반 저장소에 있을 수 있습니다.
- 보호: 공유 VHDX는 Hyper-V 복제본 및 호스트 수준 백업을 지원합니다.

![](media/sddc/learn.png)**[게스트 클러스터링(공유 VHDX 포함)에 대해 자세히 알아보기](https://technet.microsoft.com/library/dn281956(v=ws.11).aspx)**

### Hyper-V 복제본 ###

![](media/sddc/virtualize-line.png)

인증서를 사용하는 네트워크를 통한 통합 소프트웨어 기반 VM 복제입니다. 어느 사이트의 서버, 네트워크 또는 저장소 하드웨어에 바인딩되지 않습니다.

![](media/sddc/spacer1.png)![](media/sddc/replica.png)

다른 가상 컴퓨터 복제 기술에 대한 필요성이 없기 때문에 비용이 절감됩니다.
- 실시간 마이그레이션을 자동으로 처리합니다.
- Hyper-V Manager, PowerShell 또는 Azure Site Recovery를 통한 단순한 구성 및 관리.

![](media/sddc/learn.png)**[Hyper-V 복제본에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/virtualization/hyper-v/manage/set-up-hyper-v-replica)**

![](media/sddc/networking.png)

### 네트워크 컨트롤러 ###

![](media/sddc/networking-line.png)

데이터 센터의 가상 및 실제 네트워크 인프라의 관리, 구성, 모니터링 및 문제 해결을 위한 중앙의 프로그래밍 가능한 자동화 위치입니다.

![](media/sddc/spacer1.png)![](media/sddc/netcontroller.png)

관리자는 네트워크 컨트롤러를 직접 조작하는 관리 도구를 사용합니다. 네트워크 컨트롤러는 가상 및 실제 인프라를 포함한 네트워크 인프라에 관한 정보를 관리 도구에 제공합니다.

![](media/sddc/learn.png)**[네트워크 컨트롤러에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-controller/network-controller)**

### 데이터 센터 방화벽 ###

![](media/sddc/networking-line.png)

서비스로 배포 및 제공되었을 때 테넌트 관리자는 인터넷 및 인트라넷 네트워크의 원치 않는 트래픽으로부터 가상 네트워크를 보호하는 데 도움이 되도록 방화벽 정책을 설치 및 구성할 수 있습니다.

![](media/sddc/spacer1.png)![](media/sddc/firewall.png)

서비스 공급자 관리자 또는 테넌트 관리자는 네트워크 컨트롤러를 통해 데이터 센터 방화벽 정책을 관리할 수 있습니다.

![](media/sddc/learn.png)**[데이터 센터 방화벽에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/datacenter-firewall-overview)**

### 스위치 포함 팀 ###

![](media/sddc/networking-line.png)

SET(스위치 포함 팀)는 Hyper-V 및 [SDN(소프트웨어 정의 네트워킹)](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking) 스택을 포함하는 환경에서 사용할 수 있는 대체 NIC 팀 솔루션입니다.

![](media/sddc/spacer1.png)![](media/sddc/teaming.png)

![](media/sddc/learn.png)**[스위치 포함 팀에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/networking/sdn/technologies/set-for-sdn)**

### 소프트웨어 부하 분산 ###

![](media/sddc/networking-line.png)

SLB는 여러 서버에서 동일한 작업을 호스트할 수 있도록 하여 높은 가용성과 확장성을 제공합니다. 다른 VM 작업에 대하여 사용하는 동일한 Hyper-V Server의 SLB VM을 사용하여 부하 분산 기능을 확장합니다. SLB는 클라우드 서비스 공급자 작업을 위한 부하 분산 끝점의 신속한 생성과 삭제를 지원합니다. SLB는 클러스터당 수십 기가바이트를 지원하고, 단순 프로비전 모델을 제공하며, 확장 및 감축이 쉽습니다.

![](media/sddc/spacer1.png)![](media/sddc/balancer.png)

![](media/sddc/learn.png)**[소프트웨어 부하 분산에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/networking/sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn)**


![](media/sddc/storage.png)

### 저장소 공간 다이렉트 ###

![](media/sddc/storage-line.png)

로컬 연결 드라이브가 있는 업계 표준 서버를 사용하는 저장소 공간 다이렉트는 기존의 SAN 또는 NAS 어레이에 비해 훨씬 저렴한 비용으로 확장성이 뛰어난 고가용성 소프트웨어 정의 저장소를 제공합니다. 아키텍처는 조달 및 배포를 크게 간소화합니다.

![각 노드에는 로컬 연결 드라이브가 저장소 공간 다이렉트에 의해 클러스터 수준에서 풀링되어 있고, VM에 의해 CSV를 통해 액세스됩니다.](media/sddc/spacer1.png)![](media/sddc/ssd.png)

저장소 공간 다이렉트는 새로운 소프트웨어 저장소 버스를 도입하고, 장애 조치(Failover) 클러스터링, CSVs(클러스터 공유 볼륨), SMB(서버 메시지 블록) 3, 저장소 공간을 비롯하여 오늘날 Windows Server에서 알려진 많은 기능을 활용합니다.

![](media/sddc/learn.png)**[저장소 공간 다이렉트에 대해 자세히 알아보기](storage/storage-spaces/storage-spaces-direct-overview.md)**
### 저장소 서비스 품질 ###


![](media/sddc/storage-line.png)

Hyper-V 및 스케일 아웃 파일 서버 역할을 사용하여 가상 컴퓨터의 저장소 성능을 중앙에서 모니터링하고 관리하여 여러 가상 컴퓨터 사이의 저장소 리소스 공정성을 개선합니다.

![](media/sddc/spacer1.png)![](media/sddc/qos.png)

저장소 QoS(서비스 품질)는 SMB3 프로토콜을 사용하여 스케일 아웃 파일 서버 및 Hyper-V에서 제공되는 Microsoft 소프트웨어 정의 저장소 솔루션에 기본 제공됩니다. 새로운 정책 관리자는 중앙 저장소 성능 모니터링을 제공합니다.

![](media/sddc/learn.png)**[저장소 QoS에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/storage/storage-qos/storage-qos-overview)**

### 저장소 복제본 ###


![](media/sddc/storage-line.png)

재해 복구 및 대비는 여러 데이터 센터를 더욱 효율적으로 사용하여 여러 랙, 층, 건물, 캠퍼스, 도시 및 국가의 데이터를 동기적으로 보호하는 기능을 통해 데이터 무손실을 가능케 합니다.

![](media/sddc/spacer1.png)
![](media/sddc/storage-replica.png)

동기 복제

1. 응용 프로그램이 데이터를 씁니다.
2. 로그 데이터가 기록되고 데이터가 원격 사이트에 복제됩니다.
3. 로그 데이터가 원격 사이트에 기록됩니다.
4. 원격 사이트에서 승인합니다.
5. 응용 프로그램 쓰기가 승인됩니다.

t 및 t1: 데이터가 볼륨에 플러시되고 로그가 항상 기록됨


![](media/sddc/learn.png)**[저장소 복제본에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/storage/storage-replica/storage-replica-overview)**


![](media/sddc/security.png)


### 보호된 패브릭 ###


![](media/sddc/security-line.png)

클라우드 서비스 공급자 또는 엔터프라이즈 사설 클라우드 관리자로서 보호된 패브릭을 사용하여 VM에 대한 더욱 안전한 환경을 제공할 수 있습니다. 보호된 패브릭은 하나의 HGS(호스트 보호 서비스)(일반적으로 3노드의 클러스터)에 하나 이상의 보호된 호스트 및 보호된 가상 컴퓨터(VM) 세트로 구성됩니다.

![](media/sddc/spacer1.png)![](media/sddc/guarded-fabric.png)

![](media/sddc/learn.png)**[보호된 패브릭에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### 보호된 VM ###

![](media/sddc/security-line.png)

보호된 VM의 데이터와 상태는 검사, 도용 및 변조, 맬웨어는 물론 데이터 센터 관리자로부터 보호됩니다.

![](media/sddc/spacer1.png)![](media/sddc/shielded.png)

- 보호된 VM은 VM의 소유자로 지정된 패브릭에서만 실행됩니다.
- 보호된 VM은 BitLocker 또는 다른 수단에 의해 암호화되기 때문에 지정된 소유자만 이를 실행할 수 있습니다.
- 실행 중인 VM은 보호된 상태로 변환될 수 있습니다.

![](media/sddc/learn.png)**[보호된 VM에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-and-shielded-vms)**

### 호스트 보호 서비스 ###

![](media/sddc/security-line.png)

호스트 보호 서비스는 암호화된 가상 컴퓨터는 물론 적합한 패브릭에 대한 키를 보유합니다.

![](media/sddc/spacer1.png)![](media/sddc/guardian.png)

![](media/sddc/learn.png)**[호스트 보호 서비스에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/virtualization/guarded-fabric-shielded-vm/guarded-fabric-manage-hgs)**

### 장치 상태 증명 ###

![](media/sddc/security-line.png)

증명을 통해 운영 비용에 대한 최소한의 영향으로(또는 영향 없이) 하드웨어에서 모니터링되고 증명되는 보안 수준을 높일 수 있습니다.


![](media/sddc/spacer1.png)![](media/sddc/attestation.png)


위에 표시된 하드웨어 신뢰 모드는 TPM v2.0 하드웨어 기반 신뢰 및 키 릴리스용 코드 무결성 정책이 포함된 규정 준수를 통해 가장 높은 수준의 보증을 제공합니다.


![](media/sddc/learn.png)**[장치 상태 증명에 대해 자세히 알아보기](https://docs.microsoft.com/windows-server/security/device-health-attestation)**

![](media/sddc/management.png)

### PowerShell DSC ###

![](media/sddc/management-line.png)

Windows PowerShell DSC(필요한 상태 구성)는 개방형 표준에 따라 Windows에 기본 제공되는 구성 관리 플랫폼입니다. DSC는 확장 중은 물론, 배포 수명 주기의 각 단계(개발, 테스트, 사전 프로덕션, 프로덕션)에서 안정적이고 일관되게 작동할 수 있을 만큼 유연합니다.

![](media/sddc/spacer1.png)![](media/sddc/dsc.png)

DSC는 "연속 배포"를 지원하므로 중단 없이 구성을 계속해서 배포할 수 있습니다.

-  DSC 구성은 빠른 배포를 위해 원래 설정에서 변경된 설정만 적용합니다.
-  DSC는 온-프레미스, 공용 또는 개인 클라우드 환경에서 사용할 수 있습니다.
-  대상 시스템에 PowerShell 스크립트를 실행할 수 있는 한 모든 Microsoft 또는 타사 솔루션과 DSC를 통합할 수 있습니다.

![](media/sddc/learn.png)**[PowerShell DSC에 대해 자세히 알아보기](https://docs.microsoft.com/powershell/dsc/overview)**


### System Center VMM ###

![](media/sddc/management-line.png)

Virtual Machine Manager는 온-프레미스, 서비스 공급자 및 Azure 클라우드에 걸쳐 통합 관리 환경을 제공하도록 기존 데이터 센터를 구성, 관리 및 변형하는 데 사용되는 System Center 제품군의 일부입니다.

![](media/sddc/spacer1.png)![](media/sddc/vmm.png)

- 데이터 센터: 데이터 센터 구성 요소를 VMM의 단일 패브릭으로 구성 및 관리합니다. 
- 가상화 호스트: VMM은 Hyper-V 및 VMware 가상화 호스트와 클러스터를 추가, 프로비전 및 관리할 수 있습니다.
- 네트워킹: VMM은 가상 네트워크 및 네트워크 게이트웨이 생성 및 관리에 대한 지원을 포함하여 네트워크 가상화를 제공합니다. 
- 저장소: VMM은 로컬 및 원격 저장소를 검색, 분류, 프로비전 및 할당할 수 있습니다.

![](media/sddc/learn.png)**[System Center VMM에 대해 자세히 알아보기](https://docs.microsoft.com/system-center/vmm/)**

### Windows Admin Center ###

![](media/sddc/management-line.png)

Windows Admin Center는 Azure 또는 클라우드 종속성 없이 Windows Server의 온-프레미스 관리를 구현하는 로컬로 배포되는 브라우저 기반 관리 도구 집합입니다. Windows Admin Center는 IT 관리자에게 서버 인프라의 모든 측면에 대한 완전한 권한을 부여하며 인터넷에 연결되지 않은 개인 네트워크에서의 관리에 특히 유용합니다.

![](media/sddc/spacer1.png)![](media/sddc/architecture.png)

웹 서버를 DNS에 게시하고 회사 방화벽을 설정하면 공용 인터넷에서 Windows Admin Center에 액세스하여 Microsoft Edge 또는 Google Chrome으로 어디에서든 서버에 연결하여 관리할 수 있습니다.

![](media/sddc/learn.png)**[Microsoft Project Windows Admin Center대한 자세한 내용](manage/windows-admin-center/overview.md)**

