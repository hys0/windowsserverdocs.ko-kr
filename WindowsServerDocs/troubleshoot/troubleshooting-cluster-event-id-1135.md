---
title: 이벤트 ID가 1135 인 클러스터 문제 해결
description: 이벤트 ID 1135를 사용 하 여 클러스터 서비스 시작 문제를 해결 하는 방법을 설명 합니다.
ms.date: 05/28/2020
ms.openlocfilehash: d59f8b89e89ea7ff42aecd79670465aee8d63524
ms.sourcegitcommit: 5fac756c2c9920757e33ef0a68528cda0c85dd04
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306532"
---
# <a name="troubleshooting-cluster-issue-with-event-id-1135"></a>이벤트 ID가 1135 인 클러스터 문제 해결

이 문서는 장애 조치 (Failover) 클러스터링 환경에서 클러스터 서비스를 시작 하는 동안 기록 될 수 있는 이벤트 ID 1135를 진단 하 고 해결 하는 데 도움이 됩니다.

## <a name="start-page"></a>시작 페이지

이벤트 ID 1135은 하나 이상의 클러스터 노드가 활성 장애 조치 (failover) 클러스터 멤버 자격에서 제거 되었음을 나타냅니다. 다음 증상이 수반 될 수 있습니다.

- 활성 장애 조치 (failover) 클러스터 구성원에서 제거 되는 클러스터 Failover\nodes: [활성 장애 조치 (Failover) 클러스터 구성원에서 제거 되는 노드에 문제가](/problem-nodes-failover-cluster.md) 있음
- 이벤트 ID 1069 [이벤트 id 1069-클러스터 된 서비스 또는 응용 프로그램 가용성](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc756225(v=ws.10))
- 쿼럼 손실 이벤트 id 1177 이벤트 id 1177 [-쿼럼 및 쿼럼에 필요한 연결](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc773498(v=ws.10))
- 클러스터 서비스 중단에 대 한 이벤트 ID 1006: [이벤트 id 1006-클러스터 서비스 시작](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc773418(v=ws.10))

유효성 검사 및 네트워크 테스트는 문제를 일으킬 수 있는 구성 문제가 없는지 확인 하기 위한 초기 문제 해결 단계 중 하나로 권장 됩니다.

### <a name="check-if-installed-the-recommended-hot-fixes"></a>권장 핫 픽스를 설치 했는지 확인 합니다.

클러스터 서비스는 장애 조치 (failover) 클러스터 작업의 모든 측면을 제어 하 고 클러스터 구성 데이터베이스를 관리 하는 필수 소프트웨어 구성 요소입니다. 1135 이벤트 ID가 표시 되는 경우 아래 KB 문서에 설명 된 수정 사항을 설치 하 고 클러스터의 모든 노드를 다시 부팅 한 다음 문제가 다시 발생 하는지 확인 하는 것이 좋습니다.

- [Windows Server 2012 R2 핫픽스](https://support.microsoft.com/help/2920151)
- [Windows Server 2012에 대 한 핫픽스](https://support.microsoft.com/help/2784261)
- [Windows Server 2008 R2 핫픽스](https://support.microsoft.com/help/2545685)

### <a name="check-if-the-cluster-service-running-on-all-the-nodes"></a>클러스터 서비스가 모든 노드에서 실행 되 고 있는지 확인 합니다.

Windows 운영 체제에 따라 다음 명령을 수행 하 여 클러스터 서비스가 계속 실행 되 고 사용 가능한 지 확인 합니다.

#### <a name="for-windows-server-2008-r2-cluster"></a>Windows Server 2008 R2 클러스터의 경우

관리자 권한 cmd 프롬프트 실행: **cluster.exe 노드/stat**  

#### <a name="for-windows-server-2012-and-windows-server-2012-r2-cluster"></a>Windows Server 2012 \ 및 Windows Server 2012 R2 클러스터의 경우

PS 명령 실행: **클러스터 노드/status**  

클러스터 서비스가 계속 실행 중 이며 모든 노드에서 사용할 수 있나요?

## <a name="solution-for-cluster-service-is-failing"></a>클러스터 서비스에 대 한 솔루션이 실패 합니다.

클러스터 서비스가 실패 하는 경우 [Windows Server 2008 및 2008 R2 장애 조치 (Failover) 클러스터 시작 스위치](/archive/blogs/askcore/windows-server-2008-and-2008r2-failover-cluster-startup-switches)문서를 사용 하 여 문제를 해결 합니다.


## <a name="several-scenarios-of-event-id-1135"></a>이벤트 ID 1135의 여러 시나리오

클러스터의 모든 노드에 대 한 시스템 이벤트 로그를 자세히 확인 하려고 합니다. 노드에 표시 되는 이벤트 ID 1135을 검토 하 고이 이벤트의 모든 인스턴스를 복사 합니다. 이렇게 하면 편리 하 게 확인 하 고 검토할 수 있습니다.

```console
Event ID 1135
Cluster node ' **NODE A** ' was removed from the active failover cluster membership. The Cluster service on this node may have stopped. This could also be due to the node having lost communication with other active nodes in the failover cluster. Run the Validate a Configuration wizard to check your network configuration. If the condition persists, check for hardware or software errors related to the network adapters on this node. Also check for failures in any other network components to which the node is connected such as hubs, switches, or bridges.
```

세 가지 일반적인 시나리오는 다음과 같습니다.

### <a name="scenario-a"></a>시나리오 A

모든 이벤트를 보고 있으며 클러스터의 모든 노드에서 노드 A의 통신이 끊어진 것을 나타냅니다.

![시나리오 a ](media/troubleshooting-cluster-event-id-1135/18647.png)
 시나리오 a ![](media/troubleshooting-cluster-event-id-1135/18648.png)

노드 A에 시스템 로그가 표시 되는 경우 클러스터의 나머지 모든 노드에 대 한 이벤트를 포함 하는 것일 수 있습니다.

#### <a name="solution"></a>해결 방법

이는 네트워크 정체로 인 한 문제 발생 시 또는 노드 A로의 통신이 손실 되었다는 것을 의미 합니다.

네트워크 구성 및 통신 문제를 검토 하 고 유효성을 검사 해야 합니다. 노드 A와 관련 된 문제를 확인 해야 합니다.

### <a name="scenario-b"></a>시나리오 B

노드의 이벤트를 확인 하 고 클러스터가 두 사이트에 분산 되어 있다고 가정해 보겠습니다. 사이트 1의 노드 A, 노드 B 및 노드 C, 사이트 2의 노드 E & 노드 E

![시나리오 B](media/troubleshooting-cluster-event-id-1135/18649.png)

노드 A, B 및 C에서 기록 된 이벤트는 노드 D & E에 연결 하기 위한 것입니다. 마찬가지로 노드 D & E에 대 한 이벤트가 표시 되 면 A, B 및 C와의 통신이 손실 된 것을 알 수 있습니다.

![시나리오 B](media/troubleshooting-cluster-event-id-1135/18650.png)

#### <a name="solution"></a>해결 방법

유사한 활동이 표시 되는 경우 이러한 사이트를 연결 하는 링크를 통해 통신 오류가 있음을 나타냅니다. 사이트 간 연결을 검토 하는 것이 좋습니다. WAN 연결을 통해 연결 하는 경우 ISP에 연결에 대 한 확인을 제안 하는 것이 좋습니다.

### <a name="scenario-c"></a>시나리오 C

노드의 이벤트를 살펴보면 노드의 이름이 특정 패턴으로 집계 되지 않는 것을 볼 수 있습니다. 클러스터가 두 사이트 간에 분산 되어 있다고 가정해 보겠습니다. 사이트 1의 노드 A, 노드 B 및 노드 C, 사이트 2의 노드 E & 노드 E

- 노드 A: 노드 B, D, E에 대 한 이벤트를 표시 합니다.
- 노드 B: 노드 C, D, E에 대 한 이벤트를 표시 합니다.
- 노드 C: 노드 A, B, E에 대 한 이벤트를 표시 합니다.
- 노드 D: 노드 A, C, E에 대 한 이벤트를 표시 합니다.
- 노드 E: 노드 B, C, D에 대 한 이벤트를 표시 합니다.
- 또는 다른 모든 조합입니다.

![시나리오 C](media/troubleshooting-cluster-event-id-1135/18651.png)

#### <a name="solution"></a>해결 방법

이러한 이벤트는 노드 간 네트워크 채널이 choked 되 고 클러스터 통신 메시지가 시기 적절 한 시간 내에 도달 하지 않는 경우에 발생할 수 있으며, 클러스터에서 노드 간의 통신을 손실 하 여 클러스터 멤버 자격에서 노드를 제거 하는 것을 느낄 수 있습니다.

## <a name="review-cluster-networks"></a>클러스터 네트워크 검토

다음 세 가지 옵션을 하나씩 확인 하 여이 문제 해결 가이드를 계속 하는 방법으로 클러스터 네트워크를 검토 하는 것이 좋습니다.

### <a name="check-for-antivirus-exclusion"></a>바이러스 백신 제외 확인

클러스터 서비스를 실행 하는 서버의 바이러스 검색에서 다음 파일 시스템 위치를 제외 합니다.

- 파일 공유 미러링 모니터 경로입니다.

- *%Systemroot%\Cluster 폴더*

다음 디렉터리와 파일을 제외 하도록 바이러스 백신 소프트웨어 내에서 실시간 검사 구성 요소를 구성 합니다.

- 기본 가상 컴퓨터 구성 디렉터리 (C:\ProgramData\Microsoft\Windows\Hyper-V)

- 사용자 지정 가상 컴퓨터 구성 디렉터리

- 기본 가상 하드 디스크 드라이브 디렉터리 (C:\Users\Public\Documents\Hyper-V\Virtual 하드 디스크)

- 사용자 지정 가상 하드 디스크 드라이브 디렉터리

- Hyper-v 복제본을 사용 하는 경우 사용자 지정 복제 데이터 디렉터리

- 스냅숏 디렉터리

- mms

    > [!NOTE]
    > 이 파일은 바이러스 백신 소프트웨어 내에서 프로세스 제외로 구성 해야 할 수 있습니다.

- Vmwp .exe

    > [!NOTE]
    > 이 파일은 바이러스 백신 소프트웨어 내에서 프로세스 제외로 구성 해야 할 수 있습니다.

또한 실시간 마이그레이션를 클러스터 공유 볼륨과 함께 사용할 경우 CSV 경로 *C:\clusterstorage* 와 모든 해당 하위 디렉터리를 제외 합니다. 장애 조치 (failover) 문제 또는 클러스터 서비스에 대 한 일반적인 문제를 해결 하 고 바이러스 백신 소프트웨어가 설치 되어 있는 경우 바이러스 백신 소프트웨어를 일시적으로 제거 하거나 소프트웨어 제조업체에 문의 하 여 바이러스 백신 소프트웨어가 클러스터 서비스와 함께 작동 하는지 확인 합니다. 대부분의 경우에는 바이러스 백신 소프트웨어를 사용 하지 않는 것 만으로는 충분 하지 않습니다. 바이러스 백신 소프트웨어를 사용 하지 않도록 설정한 경우에도 컴퓨터를 다시 시작 하면 필터 드라이버가 계속 로드 됩니다.

### <a name="check-for-network-port-configuration-in-firewall"></a>방화벽에서 네트워크 포트 구성 확인

클러스터 서비스는 서버 클러스터 작업을 제어 하 고 클러스터 데이터베이스를 관리 합니다. 클러스터는 단일 컴퓨터 역할을 하는 독립 컴퓨터의 컬렉션입니다. 관리자, 프로그래머 및 사용자는 클러스터를 단일 시스템으로 볼 수 있습니다. 소프트웨어는 클러스터의 노드 간에 데이터를 배포 합니다. 노드가 실패 하는 경우 다른 노드는 이전에 누락 된 노드에서 제공한 서비스 및 데이터를 제공 합니다. 노드가 추가 되거나 복구 될 때 클러스터 소프트웨어는 일부 데이터를 해당 노드로 마이그레이션합니다.

시스템 서비스 이름: **ClusSvc**  

|애플리케이션|프로토콜|포트|
|---|---|---|
|클러스터 서비스|UDP|3343|
|클러스터 서비스|TCP|3343 (이 포트는 노드 조인 작업을 수행 하는 동안 필요 합니다.)|
|RPC|TCP|135|
|클러스터 관리자|UDP|137|
|Kerberos|UDP\TCP|464 *|
|SMB|TCP|445|
|임의로 할당 된 많은 UDP 포트 * *|UDP|1024에서 65535 사이의 임의의 포트 번호<br/>49152에서 65535 사이의 임의의 포트 번호 * * *|
||||

> [!NOTE]
> 또한 Windows Server 2008 이상에서 Windows 장애 조치 (Failover) 클러스터에 대 한 유효성 검사를 성공적으로 수행 하려면 ICMP4, ICMP6에 대해 인바운드 및 아웃 바운드 트래픽을 허용 합니다.

- 자세한 내용은 [Windows Server 2012 장애 조치 (Failover) 클러스터 만들기 오류가 0xc000005e 오류로 인해 실패](https://support.microsoft.com/help/2830510)하는 경우를 참조 하세요.

- 이러한 포트를 사용자 지정 하는 방법에 대 한 자세한 내용은 "참조" 섹션에서 [Windows의 서비스 개요 및 네트워크 포트 요구 사항](https://support.microsoft.com/help/832017/) 을 참조 하세요.

이는 Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows Server 2008 및 Windows Vista에서의 범위입니다.

외에도 다음 명령을 실행 하 여 방화벽에서 네트워크 포트 구성을 확인 합니다. 예를 들어 다음 명령을 사용 하 여 장애 조치 (Failover) 클러스터에 사용 되는 포트 3343을 확인할 수 있습니다.

```console
netsh advfirewall firewall show rule name="Failover Clusters (UDP-In)" verbose
```

### <a name="run-the-cluster-validation-report-for-any-errors-or-warnings"></a>오류 또는 경고에 대 한 클러스터 유효성 검사 보고서를 실행 합니다.

클러스터 유효성 검사 도구는 테스트 도구 모음을 실행 하 여 하드웨어 및 설정이 장애 조치 (failover) 클러스터링과 호환 되는지 확인 합니다.

다음 지침을 따릅니다.

1. 오류 또는 경고에 대 한 클러스터 유효성 검사 보고서를 실행 합니다. 자세한 내용은 [클러스터 유효성 검사 테스트 이해: 네트워크](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771323(v=ws.11)?redirectedfrom=MSDN) 를 참조 하세요.

    ![subhatt1](media/troubleshooting-cluster-event-id-1135/18653.png)

2. 네트워크에 대 한 경고 및 오류를 확인 합니다. 자세한 내용은 [클러스터 유효성 검사 테스트 이해: 네트워크](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771323(v=ws.11)?redirectedfrom=MSDN)를 참조 하세요.

    ![범주별 네트워크 결과 ](media/troubleshooting-cluster-event-id-1135/18654.png) ![](media/troubleshooting-cluster-event-id-1135/18655.png)

#### <a name="check-the-list-network-binding-order"></a>네트워크 바인딩 순서 목록 확인

이 테스트는 네트워크가 각 노드의 어댑터에 바인딩되는 순서를 나열 합니다.

어댑터 및 바인딩 탭에서는 네트워크 서비스에서 연결에 액세스 하는 순서 대로 연결을 나열 합니다. 이러한 연결의 순서는 일반 TCP/IP 호출/패킷이 유선으로 전송 되는 순서를 반영 합니다.

네트워크 어댑터의 바인딩 순서를 변경 하려면 아래 단계를 수행 합니다.

1. **시작**, **실행**을 차례로 클릭 하 고 ncpa.cpl을 입력 한 다음 **확인**을 클릭 합니다. **네트워크 연결** 창의 **LAN 및 고속 인터넷** 섹션에서 사용 가능한 연결을 볼 수 있습니다.

2. **고급** 메뉴에서 **고급 설정**을 클릭 한 다음 **어댑터 및 바인딩** 탭을 클릭 합니다.

3. **연결** 영역에서 목록에서 위로 이동 하려는 연결을 선택 합니다. 화살표 단추를 사용 하 여 연결을 이동 합니다. 일반적으로 네트워크와 통신 하는 카드 (도메인 연결, 다른 네트워크에 라우팅 등)는 첫 번째 바운드 (목록 맨 위) 카드 여야 합니다.

클러스터 노드는 다중 홈 시스템입니다. 네트워크 우선 순위는 아웃 바운드 네트워크 연결에 대 한 DNS 클라이언트에 영향을 줍니다. 클라이언트 통신에 사용 되는 네트워크 어댑터는 바인딩 순서의 맨 위에 있어야 합니다. 라우팅되지 않은 네트워크는 낮은 우선 순위로 배치 될 수 있습니다. Windows Server 2012 및 Windows Server2012 R2에서 클러스터 네트워크 드라이버 (NETFT. SYS) 어댑터는 바인딩 순서 목록의 맨 아래에 자동으로 배치 됩니다.

#### <a name="check-the-validate-network-communication"></a>네트워크 통신 유효성 검사를 확인 합니다.

네트워크의 대기 시간으로 인해이 문제가 발생할 수도 있습니다. 노드가 노드 사이에서 손실 되지 않을 수도 있지만 제한 시간이 만료 되기 전에 노드가 충분히 빨리 이동 하지 않을 수 있습니다.

이 테스트는 테스트 된 서버가 모든 네트워크에서 허용 가능한 대기 시간과 통신할 수 있는지 확인 합니다.

예: 네트워크 통신 유효성 검사에서 네트워크 대기 시간 문제에 대 한 다음 메시지가 표시 될 수 있습니다.

```console
Succeeded in pinging network interface node003.contoso.com IP Address 192.168.0.2 from network interface node004.contoso.com IP Address 192.168.0.3 with maximum delay 500 after 1 attempt(s).
Either address 10.0.0.96 is not reachable from 192.168.0.2 or **the ping latency is greater than the maximum allowed 2000 ms** This may be expected, since network interfaces node003.contoso.com - Heartbeat Network and node004.contoso.com - Production Network are on different cluster networks
Either address 192.168.0.2 is not reachable from 10.0.0.96 or **the ping latency is greater than the maximum allowed 2000 ms** This may be expected, since network interfaces node004.contoso.com - Production Network and node003.contoso.com - Heartbeat Network for MSCS are on different cluster networks
```

다중 사이트 클러스터의 경우 제한 시간 값을 늘릴 수 있습니다. 자세한 내용은 [다중 사이트 장애 조치 (Failover) 클러스터에서 하트 비트 및 DNS 설정 구성](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd197562(v=ws.10)?redirectedfrom=MSDN)을 참조 하세요.

ISP에서 WAN 연결 문제를 확인 합니다.

다음 문제 중 하나가 발생 하는지 확인 합니다.

##### <a name="network-packets-lost-between-nodes"></a>노드 간 네트워크 패킷 손실

1. 성능을 사용 하 여 패킷 손실 확인

    노드가 노드 간 통신에서 손실 되 면 하트 비트가 실패 합니다. 성능 모니터를 사용 하 여 "Network Interface\Packets Received 버렸습니다" 카운터를 살펴보면 이것이 문제 인지 쉽게 확인할 수 있습니다. 이 카운터를 추가한 후 평균, 최소 및 최대 수를 확인 하 고 0 보다 큰 값 이면 수신 버퍼를 어댑터에 맞게 조정 해야 합니다.

    ![카운터 추가](media/troubleshooting-cluster-event-id-1135/18652.png)

    VmWare 가상화 플랫폼에서 네트워크 패킷이 손실 된 경우 "VmWare 가상화 플랫폼에 설치 된 클러스터" 섹션을 참조 하세요.

2. NIC 드라이버 업그레이드

    이 문제는 오래 된 NIC 드라이버 \ 통합 구성 요소 (IC) \VmTools 또는 잘못 된 NIC 어댑터 때문에 발생할 수 있습니다.
    실제 컴퓨터의 노드 간에 네트워크 패킷이 손실 된 경우 네트워크 어댑터 드라이버를 업데이트 하십시오. 이전 또는 최신 네트워크 카드 드라이버 및/또는 펌웨어
    때때로 네트워크 카드나 스위치의 단순한 잘못 된 구성으로 인해 하트 비트가 손실 될 수도 있습니다.

##### <a name="cluster-installed-in-the-vmware-virtualization-platform"></a>VmWare 가상화 플랫폼에 설치 된 클러스터

VMware 환경의 경우 VMware 어댑터 문제를 확인 합니다. 

트래픽이 급증 하는 동안 패킷이 삭제 된 경우이 문제가 발생할 수 있습니다. 트래픽 필터링이 발생 하지 않았는지 확인 합니다 (예: 메일 필터 사용). 이러한 가능성을 제거 하 고 나면 게스트 운영 체제의 버퍼 수를 점차적으로 늘리고 확인 합니다.

버스트 트래픽 삭제를 줄이려면 다음 단계를 수행 합니다.

1. Windows 키 + R을 사용 하 여 실행 상자를 엽니다.
2. Devmgmt.msc를 입력 하 고 **enter**키를 누릅니다.
3. **네트워크 어댑터** 확장  
4. Vmxnet3를 마우스 오른쪽 단추로 클릭 **하 고 속성을 클릭 합니다.**  
5. **고급** 탭을 클릭합니다.
6. **작은 Rx 버퍼** 를 클릭 하 고 값을 늘립니다. 기본값은 512이 고 최대값은 8192입니다.
7. **Rx 링 #1** 크기를 클릭 하 고 값을 늘립니다. 기본값은 1024이 고 최대값은 4096입니다.

VMware 환경에 대 한 vmware 어댑터 문제를 확인 하려면 다음 Url을 확인 하세요.

- [노드가 VMWARE ESX의 장애 조치 (Failover) 클러스터 멤버 자격에서 제거 되 고 있나요?](/archive/blogs/askcore/nodes-being-removed-from-failover-cluster-membership-on-vmware-esx)

- [ESXi의 VMXNET3 vNIC 게스트 운영 체제 수준에서 큰 패킷 손실](https://kb.vmware.com/s/article/2039495)

##### <a name="noticed-any-network-congestion"></a>네트워크 정체 발견

네트워크 정체 때문에 네트워크 연결 문제가 발생할 수도 있습니다.

네트워크가 밀리초 단위 및 공급 업체 권장 사항으로 구성 되었는지 확인 하 고 [Windows 장애 조치 (Failover) 클러스터 네트워크 구성](/archive/blogs/askcore/configuring-windows-failover-cluster-networks)을 참조 하세요.

##### <a name="check-the-network-configuration"></a>네트워크 구성 확인

그래도 작동 하지 않으면 클러스터 GUI에서 분할 된 네트워크를 확인 하거나 하트 비트 NIC에서 NIC 팀을 사용 하도록 설정 했는지 확인 하세요.

클러스터 GUI에 분할 된 네트워크가 표시 되는 경우 문제 해결을 위해 ["분할 된" 클러스터 네트워크](/archive/blogs/askcore/partitioned-cluster-networks) 를 참조 하세요.

하트 비트 NIC에서 NIC 팀을 사용 하도록 설정한 경우 팀 공급 업체의 권장 사항에 따라 팀 소프트웨어 기능을 선택 합니다.

##### <a name="upgrade-the-nic-drivers"></a>NIC 드라이버 업그레이드

이 문제는 오래 된 NIC 드라이버 또는 잘못 된 NIC 어댑터 때문에 발생할 수 있습니다.

실제 컴퓨터의 노드 간에 네트워크 패킷이 손실 된 경우 네트워크 어댑터 드라이버를 업데이트 합니다. 이전 또는 최신 네트워크 카드 드라이버 및/또는 펌웨어

때때로 네트워크 카드나 스위치의 단순한 잘못 된 구성으로 인해 하트 비트가 손실 될 수도 있습니다.

##### <a name="check-the-network-configuration"></a>네트워크 구성 확인

그래도 작동 하지 않는 경우 클러스터 GUI에서 분할 된 네트워크를 확인 했는지 아니면 하트 비트 NIC에서 NIC 팀을 사용 하도록 설정 했는지 확인 합니다.
