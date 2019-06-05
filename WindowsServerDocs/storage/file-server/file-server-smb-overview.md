---
title: 파일 공유는 SMB 3 프로토콜을 사용 하 여 Windows Server의 개요
description: SMB 3 프로토콜을 사용 하 여 파일 공유 및 Windows Server를 사용 하 여 파일 서비스에 대해 간략히 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc4c8b341ee78db80f862ee412400f0a930fe810
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845054"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>파일 공유는 SMB 3 프로토콜을 사용 하 여 Windows Server의 개요

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

Windows Server® 2012, Windows Server 2012 R2 및 Windows Server 2016에서 SMB 3.0 기능에 설명, 유용한 팁 가장 중요 한 기능에 대 한 새로운 사용 하거나 이전 버전 및 하드웨어에 비해 이번이 버전에서 기능 업데이트 요구 사항입니다.

## <a name="feature-description"></a>기능 설명

SMB(서버 메시지 블록) 프로토콜은 컴퓨터의 응용 프로그램에서 파일을 읽고 쓸 수 있으며 컴퓨터 네트워크상의 서버 프로그램에서 서비스를 요청할 수 있도록 지원하는 네트워크 파일 공유 프로토콜입니다. SMB 프로토콜은 해당 TCP/IP 프로토콜이나 기타 네트워크 프로토콜상에서 사용될 수 있습니다. SMB 프로토콜을 사용하면 응용 프로그램이나 응용 프로그램의 사용자가 원격 서버에 있는 파일이나 기타 리소스를 액세스할 수 있습니다. 즉, 원격 서버의 파일을 읽고 만들며 업데이트할 수 있습니다. 또한 SMB 클라이언트 요청을 수신하도록 설정된 서버 프로그램과 통신할 수 있습니다. Windows Server 2012의 새로운 SMB 프로토콜 버전 3.0을 소개합니다.

## <a name="practical-applications"></a>유용한 팁

이 섹션에서는 새로운 SMB 3.0 프로토콜에 대한 몇 가지 새롭고 유용한 방법에 대해 설명합니다.

* **가상화용 파일 저장소(SMB를 통한 Hyper-V™)** . Hyper-V는 SMB 3.0 프로토콜을 통한 파일 공유에 구성, VHD(가상 하드 디스크) 파일 및 스냅샷 등의 가상 컴퓨터 파일을 저장할 수 있습니다. 이 방법은 Hyper-V를 클러스터의 공유 파일 저장소와 함께 사용하는 클러스터된 파일 서버와 독립 실행형 파일 서버에 모두 사용할 수 있습니다.
* **SMB를 통한 Microsoft SQL Server**. SQL Server는 SMB 파일 공유에 사용자 데이터베이스 파일을 저장할 수 있습니다. 현재 이 방법은 독립 실행형 SQL 서버용 SQL Server 2008 R2에서만 지원됩니다. 후속 버전의 SQL Server에서는 클러스터된 SQL 서버와 시스템 데이터베이스에 대한 지원이 추가됩니다.
* **기존의 최종 사용자 데이터용 저장소**. SMB 3.0 프로토콜을 사용하면 정보 근로자(또는 클라이언트)의 워크로드 환경을 개선할 수 있습니다. 즉, 지점 사용자가 WAN(광역 네트워크)을 통해 데이터에 액세스할 때 경험하게 되는 응용 프로그램 대기 시간을 단축하고 도청 공격으로부터 데이터를 보호할 수 있습니다.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

Windows Server 2012 R2의 새로운 기능과 변경 된 기능에 대 한 자세한 내용은 [What's New in Windows Server에서 SMB](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>)합니다.

Windows Server 2012 및 Windows Server 2016에서 SMB는 다음 표에 설명 하는 여러 새로운 개선 사항 및 새로운 SMB 3.0 프로토콜을 포함 합니다.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>기능</p></th>
<th><p>새로운 기능 또는 업데이트된 기능</p></th>
<th><p>요약</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SMB 투명 장애 조치(Failover)</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>관리자는 서버 응용 프로그램에서 이러한 파일 공유에 데이터를 저장하는 것을 인터럽트하지 않고도 클러스터된 파일 서버의 노드에서 하드웨어 또는 소프트웨어 유지 관리 작업을 수행할 수 있습니다. 또한 클러스터 노드에서 하드웨어 또는 소프트웨어 오류가 발생하면 SMB 클라이언트는 이러한 파일 공유에 데이터를 저장하는 응용 프로그램을 인터럽트하지 않고 다른 클러스터 노드로 투명하게 다시 연결합니다.</p></td>
</tr>
<tr class="even">
<td><p>SMB 스케일 아웃</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>CSV(클러스터 공유 볼륨) 버전 2를 사용할 경우 관리자는 파일 서버 클러스터의 모든 노드 전반에서 직접 I/O를 사용하여 데이터 파일에 대한 동시 액세스가 가능한 파일 공유를 만들 수 있습니다. 이 기능을 통해 네트워크 대역폭의 사용률과 파일 서버 클라이언트의 부하 분산 효과를 향상시키고 서버 응용 프로그램의 성능을 최적화할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMB 다중 채널</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>SMB 3.0 클라이언트와 SMB 3.0 서버 사이에 여러 경로가 있는 경우 네트워크 대역폭과 네트워크 내결함성을 집계할 수 있습니다. 이 기능을 통해 서버 응용 프로그램은 사용 가능한 모든 네트워크 대역폭을 완벽하게 활용할 수 있으며 네트워크 오류에 탄력적으로 대처할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>SMB 다이렉트</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>RDMA 기능을 갖추고, 대기 시간은 아주 적으면서 최대 속도로 작동할 수 있는 반면 CPU 소모량은 거의 없는 네트워크 어댑터를 사용할 수 있습니다. Hyper-V 또는 Microsoft SQL Server 등의 워크로드에 이 기능을 사용하면 원격 파일 서버가 로컬 저장소와 비슷한 역할을 할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>서버 응용 프로그램의 성능 카운터</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>새로운 SMB 성능 카운터는 공유별 처리량, 대기 시간 및 IOPS(초당 I/O) 정보를 자세히 분석하여 관리자들이 데이터가 저장된 SMB 3.0 파일 공유 성능을 분석할 수 있습니다. 이러한 카운터는 특히, Hyper-V 및 SQL Server와 같이 파일을 원격 파일 서버에 저장하는 서버 응용 프로그램을 위해 만들어졌습니다.</p></td>
</tr>
<tr class="even">
<td><p>성능 최적화</p></td>
<td><p>업데이트됨</p></td>
<td><p>SMB 3.0 클라이언트와 SMB 3.0 서버 모두 SQL Server OLTP와 같은 서버 응용 프로그램에서 일반적으로 쓰이는 소량의 임의 읽기/쓰기 I/O에 최적화되었습니다. 또한 대량의 최대 전송 단위(MTU)가 기본적으로 켜져 있어 SQL Server 데이터 웨어하우스, 데이터베이스 백업이나 복원, 가상 하드 디스크 배포나 복사 등의 대형 순차 전송 성능이 눈에 띄게 향상되었습니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMB별 Windows PowerShell Cmdlet</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>관리자는 명령줄에서 SMB용 Windows PowerShell cmdlet을 사용하여 종단 간 방식으로 파일 서버에서 파일 공유를 관리할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>SMB 암호화</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>SMB 데이터에 대한 엔드투엔드 암호화 기능을 제공하며, 신뢰할 수 없는 네트워크에서 발생하는 도청으로부터 데이터를 보호합니다. 새로운 배포 비용이 발생하지 않고 인터넷 프로토콜 보안(IPsec), 특수 하드웨어 또는 WAN 가속기가 필요하지 않습니다. 이 기능은 공유 단위별로 구성하거나 전체 파일 서버용으로 구성할 수 있으며 신뢰할 수 없는 네트워크에서 데이터가 전송되는 다양한 시나리오에서 사용할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMB 디렉터리 임대</p></td>
<td><p>단추를 사용하여 새</p></td>
<td><p>지점에서의 응용 프로그램 응답 시간이 향상됩니다. 디렉터리 임대를 사용하면 라이브 상태가 더 길어진 디렉터리 캐시로부터 메타데이터가 검색되므로 클라이언트에서 서버로의 왕복 시간이 단축됩니다. 서버의 디렉터리 정보가 변경되면 클라이언트에게 통보되므로 캐시 일관성이 유지됩니다. <em>홈폴더</em> (공유 비포함 읽기/쓰기) 및 <em>게시</em> (공유 포함 읽기 전용) 시나리오에 사용할 수 있습니다.</p></td>
</tr>
</tbody>
</table>

## <a name="hardware-requirements"></a>하드웨어 요구 사항

SMB 투명 장애 조치(Failover)의 요구 사항은 다음과 같습니다.

* 장애 조치 클러스터 구성 된 두 개 이상의 노드를 사용 하 여 Windows Server 2012 또는 Windows Server 2016을 실행 합니다. 클러스터는 유효성 검사 마법사에 포함된 클러스터 유효성 테스트를 통과해야 합니다.
* 파일 공유는 CA(Continuous Availability) 속성이 기본값으로 설정되어 만들어져야 합니다.
* 파일 공유를 CSV 볼륨 경로에 만들어야 SMB 스케일 아웃에 도달할 수 있습니다.
* 클라이언트 컴퓨터는 Windows® 8 또는 Windows Server 2012에서 지속적인 가용성을 지 원하는 업데이트 된 SMB 클라이언트를 포함 하는 둘 다 실행 되어야 합니다.

>[!NOTE]
>하위 수준 클라이언트는 CA 속성이 있는 파일 공유에 연결할 수 있지만 이러한 클라이언트에 대 한 투명 한 장애 조치 지원 되지 않습니다.

SMB 다중 채널의 요구 사항은 다음과 같습니다.

* Windows Server 2012를 실행 하는 두 개 이상의 컴퓨터는 필요 합니다. 이 기술은 추가 기능을 설치할 필요 없이 기본적으로 작동됩니다.
* 권장 네트워크 구성에 대한 자세한 내용은 이 개요 항목의 마지막 부분에 있는 참고 항목을 참조하세요.

SMB 다이렉트의 요구 사항은 다음과 같습니다.

* Windows Server 2012를 실행 하는 두 개 이상의 컴퓨터는 필요 합니다. 이 기술은 추가 기능을 설치할 필요 없이 기본적으로 작동됩니다.
* RDMA 기능이 있는 네트워크 어댑터가 필요합니다. 현재 이러한 어댑터는 iWARP, Infiniband 또는 RoCE(RDMA over Converged Ethernet) 유형으로 제공됩니다.

## <a name="more-information"></a>자세한 정보

다음은 SMB 및 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 관련된 기술에 대 한 웹의 추가 리소스를 제공합니다.

* [Windows Server에서 저장소](../storage.md)
* [응용 프로그램 데이터용 스케일 아웃 파일 서버](../../failover-clustering/sofs-overview.md)
* [직접 SMB 사용 하 여 파일 서버의 성능 향상](smb-direct.md)
* [SMB를 통한 Hyper-v 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [SMB 다중 채널 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [서버 응용 프로그램에 대 한 빠르고 효율적인 파일 서버 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: 문제 해결 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)