---
title: 스토리지 복제본 개요
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 4/26/2019
ms.assetid: e9b18e14-e692-458a-a39f-d5b569ae76c5
ms.openlocfilehash: 400af7c4fb5db6e6740b1140688602c55d8ca0a9
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85469808"
---
# <a name="storage-replica-overview"></a>스토리지 복제본 개요

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

저장소 복제본은 재해 복구를 위해 서버 또는 클러스터 간에 볼륨을 복제할 수 있게 해 주는 Windows Server 기술입니다. 또한 모든 노드가 동기화 상태로 유지 되는 두 사이트에 걸쳐 있는 스트레치 장애 조치 (failover) 클러스터를 만들 수 있습니다.

스토리지 복제본은 동기 및 비동기 복제를 지원합니다.

* **동기 복제**는 오류 중에 파일 시스템 수준에서 데이터가 손실되지 않도록 크래시 일관성이 있는 볼륨을 사용하여 대기 시간이 짧은 네트워크 사이트 내의 데이터를 미러링합니다.
* **비동기 복제**는 대기 시간이 더 긴 네트워크 링크를 통해 대도시 범위를 넘어 사이트 간 데이터를 미러링하지만 오류 시 두 사이트가 동일한 데이터 복사본을 보유하지 않을 수 있습니다.

## <a name="why-use-storage-replica"></a>스토리지 복제본을 사용하는 이유

저장소 복제본은 Windows Server에서 재해 복구 및 준비 기능을 제공 합니다. Windows Server는 서로 다른 랙, 층, 빌딩, 캠퍼스, 지방 및 도시에서 데이터를 동기적으로 보호할 수 있는 기능을 제공 하는 데이터 손실 없이 안심할 수 있는 기능을 제공 합니다. 재해가 발생 한 후 모든 데이터는 손실 가능성이 없는 다른 곳에 있습니다. 이는 재해가 발생하기 *전*에도 마찬가지입니다. 스토리지 복제본은 몇 분간의 경고가 발생하는 경우 재해가 발생하기 전에 데이터 손실 없이 워크로드를 안전한 위치로 전환할 수 있는 기능을 제공합니다.

스토리지 복제본을 사용하면 여러 데이터 센터를 더욱 효율적으로 활용할 수 있습니다. 클러스터를 확장하거나 복제하면 가까운 지역의 사용자 및 애플리케이션에서 보다 신속하게 데이터에 액세스할 수 있도록 여러 데이터 센터에서 워크로드를 실행할 수 있을 뿐만 아니라 부하 분산 및 컴퓨팅 리소스 사용의 효율성도 향상됩니다. 재해로 인해 하나의 데이터 센터가 오프라인 상태가 된 경우 이 데이터 센터의 일반 워크로드를 일시적으로 다른 사이트로 이동할 수 있습니다.

스토리지 복제본을 사용하면 저사양 재해 복구 솔루션에서 제공된 DFS 복제본과 같은 기존 파일 복제 시스템을 해제할 수 있습니다. DFS 복제본은 낮은 대역폭 네트워크에서는 매우 효율적이지만 대기 시간이 매우 깁니다(종종 몇 시간 또는 며칠). 이는 네트워크 정체를 방지하기 위한 인위적인 스로틀과 파일 닫기에 대한 요구 사항 때문입니다. 이러한 디자인 특징을 가진 DFS 복제본에서는 가장 자주 사용되고 가장 새로운 파일을 복제하기 어렵습니다. 스토리지 복제본은 파일 수준 아래에서 작동하며 이러한 제한 사항이 없습니다.

또한 범위가 더 넓고 대기 시간이 더 긴 네트워크에 대해 비동기 복제도 지원합니다. 검사점을 기반으로 하지 않고 대신 지속적으로 복제 하므로 변경의 델타가 스냅숏 기반 제품 보다 훨씬 더 낮습니다. 뿐만 아니라 스토리지 복제본은 파티션 계층에서 작동하므로 Windows Server 또는 백업 소프트웨어에 의해 생성된 모든 VSS 스냅샷을 복제합니다. 따라서 지정 시간 복구에 애플리케이션 일치 데이터 스냅샷을 사용하고, 특히 구조화되지 않은 사용자 데이터를 비동기식으로 복제할 수 있습니다.

## <a name="supported-configurations"></a><a name="BKMK_SRSupportedScenarios"></a>지원되는 구성

확장 클러스터, 클러스터 간 및 서버 간 구성에서 저장소 복제본을 배포할 수 있습니다 (그림 1-3 참조).

**확장 클러스터**: 컴퓨터와 스토리지를 단일 클러스터에 구성할 수 있습니다. 일부 노드는 하나의 비대칭 스토리지 집합을 공유하고, 다른 노드는 또 다른 비대칭 스토리지 집합을 공유하며, 사이트 인식을 통해 동기식 또는 비동기식으로 복제합니다. 이 시나리오에서는 공유 SAS 스토리지가 포함된 스토리지 공간, SAN 및 iSCSI 연결 LUN을 활용할 수 있습니다. PowerShell 및 장애 조치(Failover) 클러스터 관리자 그래픽 도구로 관리되며, 자동화된 워크로드 장애 조치(failover)를 지원합니다.

![스토리지 복제본을 사용하여 뉴저지에 있는 두 노드로 스토리지를 복제하는 뉴욕의 두 클러스터 노드를 보여 주는 다이어그램](./media/Storage-Replica-Overview/Storage_SR_StretchCluster.png)

**그림 1: 스토리지 복제본을 사용하는 확장 클러스터의 스토리지 복제**

**클러스터 간**: 두 클러스터 간의 복제를 지원합니다. 클러스터 간에 동기식 또는 비동기식으로 복제합니다. 이 시나리오에서는 스토리지 공간 다이렉트, 공유 SAS 스토리지가 포함된 스토리지 공간, SAN 및 iSCSI 연결 LUN을 활용할 수 있습니다. Windows 관리 센터 및 PowerShell을 사용 하 여 관리 되며 장애 조치 (failover)를 위한 수동 작업이 필요 합니다.

![스토리지 복제본을 사용하여 라스베가스에 있는 서로 다른 클러스터로 스토리지를 복제하는 로스앤젤레스의 클러스터를 보여 주는 다이어그램](./media/Storage-Replica-Overview/Storage_SR_ClustertoCluster.png)

**그림 2: 스토리지 복제본을 사용하는 클러스터 간 스토리지 복제**

**서버 간**을 통해 공유 SAS 스토리지가 포함된 스토리지 공간, SAN 및 iSCSI 연결 LUN과 로컬 드라이브를 사용하여 두 개의 독립 실행형 서버 간에 동기식 및 비동기식으로 복제할 수 있습니다. Windows 관리 센터 및 PowerShell을 사용 하 여 관리 되며 장애 조치 (failover)를 위한 수동 작업이 필요 합니다.

![빌딩 5의 서버가 빌딩 9의 서버와 복제되는 모습을 보여 주는 다이어그램](./media/Storage-Replica-Overview/Storage_SR_ServertoServer.png)

**그림 3: 스토리지 복제본을 사용하는 서버 간 스토리지 복제**

> [!NOTE]
> 또한 하나의 컴퓨터에서 4개의 볼륨을 사용하여 서버 자체 복제를 구성할 수 있습니다. 그러나 이 시나리오는 이 가이드에서 다루지 않습니다.

## <a name="storage-replica-features"></a><a name="BKMK_SR2"> </a> 저장소 복제본 기능

* **데이터 무손실, 블록 수준 복제**. 동기 복제 시 데이터 손실 가능성이 없습니다. 비동기 복제 시 파일 잠금 가능성이 없습니다.

* **간단한 배포 및 관리**. 사용 편의성을 위해 스토리지 복제본에 디자인 위임이 있습니다. 두 서버 간에 복제 파트너 관계를 만들면 Windows 관리 센터를 활용할 수 있습니다. 확장 클러스터 배포에 친숙한 장애 조치(Failover) 클러스터 관리자의 직관적인 마법사가 사용됩니다.

* **게스트와 호스트**. 스토리지 복제본의 모든 기능이 가상화된 게스트와 호스트 기반 배포 모두에 표시됩니다. 즉, 게스트에서 Windows Server를 사용 하는 한 Windows가 아닌 가상화 플랫폼 또는 공용 클라우드에서 실행 되는 경우에도 게스트가 데이터 볼륨을 복제할 수 있습니다.

* **SMB3 기반**. 스토리지 복제본은 Windows Server 2012에서 처음 출시된 SMB 3의 검증되고 성숙된 기술을 사용합니다. 따라서 RoCE, iWARP 및 InfiniBand RDMA 네트워크 카드의 SMB 다이렉트 지원 및 다중 채널과 같은 SMB의 모든 고급 특성을 스토리지 복제본에서 사용할 수 있습니다.

* **보안**. 많은 공급업체의 제품과 달리 스토리지 복제본에는 업계 최고의 보안 기술이 내재되어 있습니다. 패킷 서명, AES-128-GCM 전체 데이터 암호화, Intel AES-NI 암호화 가속 지원, 사전 인증 무결성 가로채기 공격 방지 등이 여기에 포함됩니다. 스토리지 복제본은 노드 간의 모든 인증에 Kerberos AES256을 활용합니다.

* **고성능 초기 동기화**. 저장소 복제본은 데이터의 하위 집합이 이전 복사본, 백업 또는 배송 된 드라이브의 대상에 이미 존재 하는 시드 된 초기 동기화를 지원 합니다. 초기 복제는 서로 다른 블록을 복사 하 여 초기 동기화 시간을 단축 하 고 데이터가 제한 된 대역폭을 사용 하는 것을 방지할 수 있습니다. 스토리지 복제본은 체크섬 계산 및 집계를 차단하므로 초기 동기화 성능이 스토리지 및 네트워크의 속도에 의해서만 제한됩니다.

* **일관성 그룹**. 쓰기 순서를 지정 하면 Microsoft SQL Server 같은 응용 프로그램이 여러 복제 된 볼륨에 쓸 수 있으며 데이터가 대상 서버에 순차적으로 기록 되는 것을 알 수 있습니다.

* **사용자 위임**. 복제된 노드의 기본 제공 Administrators 그룹의 구성원이 아닌 사용자에게 복제 관리 권한을 위임할 수 있으므로 관련 없는 영역에 대한 액세스를 제한할 수 있습니다.

* **네트워크 제약 조건**. 애플리케이션, 백업 및 관리 소프트웨어 대역폭을 제공하기 위해 스토리지 복제본을 서버 및 복제된 볼륨별로 개별 네트워크로 제한할 수 있습니다.

* **씬 프로비저닝**. 여러 상황에서 거의 즉각적인 초기 복제 시간을 제공하도록 스토리지 공간 및 SAN 디바이스의 씬 프로비전이 지원됩니다.

저장소 복제본에는 다음과 같은 기능이 포함 되어 있습니다.

| 기능 | 세부 정보 |
| ----------- | ----------- |
| Type | 호스트 기반 |
| 동기 | Yes |
| 비동기 | Yes |
| 스토리지 하드웨어에 독립적 | Yes |
| 복제 단위 | 볼륨(파티션) |
| Windows Server stretch cluster 만들기 | Yes |
| 서버 간 복제 | Yes |
| 클러스터 간 복제 | Yes |
| 전송 | SMB3 |
| 네트워크 | TCP/IP 또는 RDMA |
| 네트워크 제약 조건 지원 | Yes |
| RDMA* | iWARP, InfiniBand, RoCE v2 |
| 복제 네트워크 포트 방화벽 요구 사항 | 단일 IANA 포트(TCP 445 또는 5445) |
| 다중 경로/다중 채널 | 예(SMB3) |
| Kerberos 지원 | 예(SMB3) |
| OTW(Over The Wire) 암호화 및 서명|예(SMB3) |
| 볼륨별 장애 조치(failover) 허용 | Yes |
| 씬 프로비전된 스토리지 지원 | Yes |
| Windows 제공 관리 UI | PowerShell, 장애 조치(failover) 클러스터 관리자 |

*추가 장거리 장비 및 케이블 연결이 필요할 수 있음

## <a name="storage-replica-prerequisites"></a><a name="BKMK_SR3"></a>저장소 복제본 필수 조건

* AD DS(Active Directory 도메인 서비스) 포리스트
* SAS JBOD가 포함된 스토리지 공간, 스토리지 공간 다이렉트, 파이버 채널 SAN, 공유 VHDX, iSCSI 대상 또는 로컬 SAS/SCSI/SATA 스토리지. SSD 이상이 복제 로그 드라이브에 권장됨 로그 저장소는 데이터 저장소 보다 더 빠른 것을 권장 합니다. 로그 볼륨은 다른 작업에 사용 하면 안 됩니다.
* 각 서버에 하나 이상의 동기 복제용 이더넷/TCP 연결(RDMA 권장)
* 최소 2GB의 RAM과 서버당 두 개의 코어.
* 동기 복제를 위해 IO 쓰기 워크로드가 포함된 충분한 대역폭 및 평균 5ms 이하 왕복 대기 시간을 지원하는 서버 간의 네트워크. 비동기 복제에는 권장 대기 시간이 없습니다.
* Windows Server, Datacenter Edition 또는 Windows Server Standard Edition. Windows Server Standard Edition에서 실행 되는 저장소 복제본에는 다음과 같은 제한 사항이 있습니다.

  * Windows Server 2019 이상을 사용 해야 합니다.
  * 저장소 복제본은 볼륨 수를 제한 없이 단일 볼륨을 복제 합니다.
  * 볼륨 크기는 무제한이 아니라 최대 2tb입니다.

##  <a name="background"></a><a name="BKMK_SR4"> </a> 배경

이 섹션에는 개괄적인 업계 용어, 동기 및 비동기 복제 및 주요 동작에 대한 정보가 포함됩니다.

### <a name="high-level-industry-terms"></a>업계 최고 수준의 용어

DR(재해 복구)은 비즈니스를 계속 운영할 수 있도록 사이트 재해로부터 복구하기 위한 대비책을 가리킵니다. 데이터 DR은 별도의 물리적 위치에 있는 프로덕션 데이터의 여러 복사본을 의미합니다. 예를 들어 노드의 절반이 각각 다른 사이트에 있는 확장 클러스터가 여기에 해당합니다. DP(재해 대비)는 허리케인과 같은 예정된 재해가 발생하기 전에 워크로드를 미리 다른 위치로 이동하기 위한 대비책을 가리킵니다.

SLA(서비스 수준 계약)는 계획된 중단 및 계획되지 않은 중단 동안 비즈니스 애플리케이션의 가용성과 가동 중지 시간 및 데이터 손실에 대한 허용 범위를 정의합니다. RTO(복구 시간 목표)는 허용할 수 있는 데이터 액세스 불능 시간을 정의합니다. RPO(복구 지점 목표)는 손실을 수용할 수 있는 데이터의 양을 정의합니다.

### <a name="synchronous-replication"></a>동기 복제

동기 복제는 IO가 완료되기 전에 애플리케이션이 한 번에 두 곳에 데이터를 쓸 수 있도록 합니다. 이 복제는 네트워크 및 스토리지 투자가 필요할 뿐만 아니라 애플리케이션 성능이 저하되는 위험이 있으므로 업무에 중요한 데이터에 보다 적합합니다.

애플리케이션 쓰기가 원본 데이터 복사본에서 발생하는 경우 원래 스토리지에서 IO를 즉시 인식하지 못합니다. 대신 해당 데이터 변경 내용이 원격 대상 복사본에 복제되고 승인을 반환합니다. 그런 다음에야 애플리케이션에 IO 승인이 수신됩니다. 따라서 원격 사이트와 원본 사이트의 지속적인 동기화가 보장되며, 네트워크에서 스토리지 IO가 연장됩니다. 원본 사이트 오류 시, 애플리케이션은 원격 사이트로 장애 조치(failover)하고 데이터 무손실을 보장하면서 작업을 재개할 수 있습니다.

| Mode | 다이어그램 | 단계 |
| -------- | ----------- | --------- |
| **동기**<p>데이터 무손실<p>RPO | ![스토리지 복제본을 통해 동기 복제에서 데이터가 기록되는 방식을 보여 주는 다이어그램](./media/Storage-Replica-Overview/Storage_SR_SynchronousV2.png) | 1. 응용 프로그램이 데이터를 씁니다.<br />2. 로그 데이터가 기록 되 고 데이터가 원격 사이트에 복제 됩니다.<br />3. 로그 데이터가 원격 사이트에 기록 됩니다.<br />4. 원격 사이트에서 승인<br />5. 응용 프로그램 쓰기가 승인 됨<p>t 및 t1 : 데이터가 볼륨에 플러시되고 로그가 항상 기록됨 |

### <a name="asynchronous-replication"></a>비동기 복제

반면, 비동기 복제에서는 애플리케이션이 데이터를 쓰면 즉각적인 승인 보증 없이 해당 데이터가 원격 사이트에 복제됩니다. 이 모드는 애플리케이션 응답 시간이 더욱 빠르고 DR 솔루션이 지리적으로 작동합니다.

애플리케이션이 데이터를 쓰면, 복제 엔진이 쓰기를 캡처하고 즉시 애플리케이션을 승인합니다. 그런 다음 캡처된 데이터는 원격 위치에 복제됩니다. 원격 노드는 데이터의 복사본을 처리하고 원본 복사본을 다시 지연 승인합니다. 복제 성능이 더 이상 애플리케이션 IO 경로에 없으므로 원격 사이트의 응답성 및 거리는 중요한 요소가 아닙니다. 원본 데이터가 손실되고 데이터의 대상 복사본이 원본을 떠나지 않고 여전히 버퍼에 있는 경우 데이터가 손실될 위험이 있습니다.

RPO가 0보다 높은 비동기 복제는 복원력 및 데이터 무손실을 통해 지속적인 운영을 지원하도록 설계되었으므로 장애 조치(failover) 클러스터와 같은 HA 솔루션에 적합하지 않습니다.

| Mode | 다이어그램 | 단계 |
| -------- | ----------- | --------- |
| **비동기**<p>거의 데이터 무손실<p>(여러 요소에 따라 달라짐)<p>RPO | ![스토리지 복제본을 통해 비동기 복제에서 데이터가 기록되는 방식을 보여 주는 다이어그램](./media/Storage-Replica-Overview/Storage_SR_AsynchronousV2.png)|1. 응용 프로그램이 데이터를 씁니다.<br />2. 기록 된 로그 데이터<br />3. 응용 프로그램 쓰기가 승인 됨<br />4. 원격 사이트에 복제 된 데이터<br />5. 원격 사이트에 기록 된 로그 데이터<br />6. 원격 사이트에서 승인<p>t 및 t1 : 데이터가 볼륨에 플러시되고 로그가 항상 기록됨 |

### <a name="key-evaluation-points-and-behaviors"></a>주요 평가 지점과 동작

-   가장 빠른 스토리지의 네트워크 대역폭 및 대기 시간. 동기 복제와 관련된 물리적 제한이 있습니다. 스토리지 복제본은 로그를 사용하고 네트워크 왕복을 통해 IO 필터링 메커니즘을 구현하므로 동기 복제 시 애플리케이션 쓰기가 느려질 수 있습니다. 낮은 대기 시간, 고대역폭 네트워크 및 로그에 대 한 높은 처리량의 디스크 하위 시스템을 사용 하 여 성능 오버 헤드를 최소화 합니다.

-   Windows Server 2016에서 복제 하는 동안에는 대상 볼륨에 액세스할 수 없습니다. 복제를 구성 하면 대상 볼륨이 분리 되어 사용자의 읽기 또는 쓰기에 액세스할 수 없게 됩니다. 해당 드라이버 문자는 파일 탐색기와 같은 일반적인 인터페이스에서 볼 수 있지만 응용 프로그램에서 볼륨 자체에 액세스할 수는 없습니다. 블록 수준 복제 기술은 볼륨에서 대상의 탑재된 파일 시스템에 대한 액세스를 허용하지 않습니다. NTFS 및 ReFS는 사용자가 볼륨에 데이터를 쓰는 것을 지원하지 않으며 변경을 차단합니다.

Windows Server, 버전 1709에서 **테스트 장애 조치 (Failover)** Cmdlet은 windows server 2019에도 포함 되었습니다. 이제 백업, 테스트 등에 대 한 대상 볼륨의 읽기-쓰기 스냅숏을 일시적으로 탑재할 수 있습니다. 자세한 내용은을 참조 하세요 https://aka.ms/srfaq .

-   비동기 복제의 Microsoft 구현은 대부분의 다른 구현과 다릅니다. 비동기 복제의 업계 구현은 대부분 주기적인 차등 전송이 다른 노드로 이동하고 병합되는 스냅샷 기반 복제를 기반으로 합니다. 스토리지 복제본 비동기 복제는 대상의 직렬화된 동기 승인에 대한 요구 사항이 없다는 점을 제외하고는 동기 복제와 유사하게 작동합니다. 이는 이론적으로 스토리지 복제본이 지속적으로 복제하므로 RPO가 낮다는 것을 의미합니다. 반면, 스냅샷을 사용하여 애플리케이션 파일에서 일관성을 강제 적용하는 대신 내부 애플리케이션 일관성 보장에 의존함을 의미하기도 합니다. 스토리지 복제본은 모든 복제 모드에서 크래시 일관성을 보장합니다.

-   많은 고객이 해당 시나리오에 적절하지 않은 경우에도 DFS 복제를 재해 복구 솔루션으로 사용하고 있습니다. DFS 복제는 열려 있는 파일을 복제할 수 없으며 대역폭 사용을 최소화하도록 설계되었습니다. 따라서 성능이 저하되며 복구 지점 차이가 큽니다. 스토리지 복제본을 사용하면 이러한 유형의 재해 복구 작업 중 일부에서 DFS 복제를 사용 중지할 수 있습니다.

-   저장소 복제본은 백업 솔루션이 아닙니다. 일부 IT 환경에서는 매일 백업과 비교할 때 데이터 무손실 옵션 때문에 복제 시스템을 백업 솔루션으로 배포합니다. 스토리지 복제본은 변경 유형에 상관없이 모든 변경 내용을 볼륨의 모든 데이터 블록에 복제합니다. 사용자가 볼륨에서 모든 데이터를 삭제 하는 경우 저장소 복제본은 삭제를 다른 볼륨에 즉시 복제 하 여 두 서버에서 데이터를 영구적으로 제거 합니다. 지정 시간 백업 솔루션의 대체 솔루션으로 스토리지 복제본을 사용하지 마세요.

-   스토리지 복제본은 Hyper-V 복제본 또는 Microsoft SQL AlwaysOn 가용성 그룹이 아닙니다. 스토리지 복제본은 일반적인 용도의 스토리지 독립적인 엔진입니다. 정의상, 애플리케이션 수준 복제만큼 이상적으로 동작을 조정할 수 없습니다. 따라서 배포하도록 권장되는 기능과 특정 애플리케이션 복제 기술에 남겨 두는 것이 좋은 기능 간에 차이가 발생할 수 있습니다.

> [!NOTE]
> 이 문서에는 [알려진 문제](storage-replica-known-issues.md)와 예상되는 동작의 목록 및 [질문과 대답](storage-replica-frequently-asked-questions.md) 섹션이 포함됩니다.

### <a name="storage-replica-terminology"></a>스토리지 복제본 용어
이 가이드에서 자주 사용된 용어는 다음과 같습니다.

-   원본은 로컬 쓰기 및 아웃바운드 복제를 허용하는 컴퓨터의 볼륨입니다. "주"라고도 합니다.

-   대상은 로컬 쓰기 및 아웃바운드 복제를 허용하지 않는 컴퓨터의 볼륨입니다. "보조"라고도 합니다.

-   복제 파트너 관계는 하나 이상의 볼륨에 대해 원본 및 대상 컴퓨터 간의 동기화 관계이며, 단일 로그를 사용합니다.

-   복제 그룹은 서버 단위로 파트너 관계 내에서 볼륨과 해당 복제 구성을 함께 묶은 것입니다. 그룹을 하나 이상의 볼륨을 포함할 수 있습니다.

### <a name="whats-new-for-storage-replica"></a>저장소 복제본의 새로운 기능

Windows Server 2019의 저장소 복제본에 있는 새로운 기능 목록은 [저장소의 새로운](../whats-new-in-storage.md#storage-replica2019) 기능을 참조 하세요.

## <a name="additional-references"></a>추가 참조

- [공유 저장소를 사용 하 여 확장 클러스터 복제](stretch-cluster-replication-using-shared-storage.md)
- [서버 간 저장소 복제](server-to-server-storage-replication.md)
- [클러스터 간 저장소 복제](cluster-to-cluster-storage-replication.md)
- [저장소 복제본: 알려진 문제](storage-replica-known-issues.md)
- [스토리지 복제본: 질문과 대답](storage-replica-frequently-asked-questions.md)
- [Windows Server 2016의 스토리지 공간 다이렉트](../storage-spaces/storage-spaces-direct-overview.md)
- [Windows IT 전문가 지원](https://www.microsoft.com/itpro/windows/support)
