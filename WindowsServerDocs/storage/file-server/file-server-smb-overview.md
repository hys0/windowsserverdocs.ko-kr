---
title: Windows Server의 경우 SMB 3 프로토콜을 사용 하 여 파일 공유의 개요 (영문)
description: SMB 3 프로토콜을 사용 하 여 파일 공유 및 Windows Server와 함께 사용 되는 파일에 대 한 개요입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: fc4c8b341ee78db80f862ee412400f0a930fe810
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233489"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Windows Server의 경우 SMB 3 프로토콜을 사용 하 여 파일 공유의 개요 (영문)

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

이 항목에서는 Windows Server® 2012, Windows Server 2012 R2 및 Windows Server 2016 SMB 3.0 기능을 설명-실제를 사용 하 여 가장 중요 한 기능에 대 한 새로운 또는 이전 버전 및 하드웨어에 비해이 버전의 기능을 업데이트 요구 사항입니다.

## <a name="feature-description"></a>기능 설명

SMB(서버 메시지 블록) 프로토콜은 컴퓨터의 응용 프로그램에서 파일을 읽고 쓸 수 있으며 컴퓨터 네트워크상의 서버 프로그램에서 서비스를 요청할 수 있도록 지원하는 네트워크 파일 공유 프로토콜입니다. SMB 프로토콜은 해당 TCP/IP 프로토콜이나 기타 네트워크 프로토콜상에서 사용될 수 있습니다. SMB 프로토콜을 사용하면 응용 프로그램이나 응용 프로그램의 사용자가 원격 서버에 있는 파일이나 기타 리소스를 액세스할 수 있습니다. 즉, 원격 서버의 파일을 읽고 만들며 업데이트할 수 있습니다. 또한 SMB 클라이언트 요청을 수신하도록 설정된 서버 프로그램과 통신할 수 있습니다. Windows Server 2012 SMB 프로토콜의 새 3.0 버전을 소개합니다.

## <a name="practical-applications"></a>유용한 팁

이 섹션에서는 새 SMB 3.0 프로토콜을 사용 하는 일부 새로운 실용적인 방법에 설명 합니다.

* **가상화 (SMB 통해 Hyper-V™)에 대 한 파일 저장소**입니다. Hyper-v SMB 3.0 프로토콜을 통해 파일 공유에서 구성, 가상 하드 디스크 (VHD) 파일 및 스냅숏, 등의 가상 컴퓨터 파일을 저장할 수 있습니다. 이 파일을 독립 실행형 서버와 클러스터에 대 한 공유 파일 저장소와 함께 Hyper-v를 사용 하는 클러스터 된 파일 서버에 사용할 수 있습니다.
* **SMB 통해 Microsoft SQL Server**입니다. SQL Server SMB 파일 공유에서 사용자 데이터베이스 파일을 저장할 수 있습니다. 현재이 작업은 지원 SQL Server 2008 r 2와 독립 실행형 SQL 서버에 대 한 합니다. 예정 된 버전의 SQL Server 클러스터 된 SQL 서버와 시스템 데이터베이스에 대 한 지원을 추가 합니다.
* **최종 사용자 데이터에 대 한 기존의 저장소**입니다. SMB 3.0 프로토콜 정보 근로자 (또는 클라이언트)에 대 한 향상 작업 부하를 제공합니다. 이러한 향상 된이 기능 공격 광역 네트워크 (WAN)를 통해 데이터에 액세스 하 고 도청에서 데이터를 보호 하는 경우 branch office 사용자가 발생 하는 응용 프로그램 대기 시간 감소를 포함 합니다.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

Windows Server 2012 r 2에 새로 추가 되거나 변경 된 기능에 대 한 자세한 내용은 [Windows Server의 경우 SMB의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>)을 참조 하십시오.

Windows Server 2012 및 Windows Server 2016 SMB는 다음 표에 새 SMB 3.0 프로토콜 및 설명 하는 새로운 향상 시키는 많은 포함 합니다.

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
<td><p>SMB 투명 장애 조치</p></td>
<td><p>신규</p></td>
<td><p>이 파일 공유에 데이터를 저장 하는 서버 응용 프로그램을 중단 하지 않고 클러스터 된 파일 서버에 노드 하드웨어 또는 소프트웨어 유지 관리를 수행 하려면 관리자가 있습니다. 또한 클러스터 노드에서 하드웨어 또는 소프트웨어 오류가 발생 하는 경우 SMB 클라이언트 투명 하 게 다시 연결을 다른 클러스터 노드로이 파일 공유에 데이터를 저장 하는 서버 응용 프로그램을 중단 하지 않고 합니다.</p></td>
</tr>
<tr class="even">
<td><p>SMB 스케일 아웃</p></td>
<td><p>신규</p></td>
<td><p>클러스터 공유 볼륨 (CSV) 버전 2 사용 하 여 관리자는 파일 서버 클러스터의 모든 노드를 통해 직접 I/O와 데이터 파일에 대 한 동시 액세스를 제공 하는 파일 공유를 만들 수 있습니다. 네트워크 대역폭 사용률을 개선 하 고 파일 서버 클라이언트의 부하 분산을 제공 하 고 서버 응용 프로그램에서 성능을 최적화 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMB 다중 채널</p></td>
<td><p>신규</p></td>
<td><p>여러 경로 SMB 3.0 클라이언트와 SMB 3.0 서버 간에 사용할 수 있는 경우 네트워크 대역폭 및 네트워크 내결함성을의 집계 수 있습니다. 이렇게 하면 모든 사용 가능한 네트워크 대역폭을 완전 하 게 활용 하 고 네트워크 오류에 유연 하 게 하려면 서버 응용 프로그램입니다.</p></td>
</tr>
<tr class="even">
<td><p>SMB 다이렉트</p></td>
<td><p>신규</p></td>
<td><p>RDMA 기능이 있어야 하 고 최고 속도로 거의 CPU를 사용 하는 동안 매우 낮은 대기 시간으로 작동할 수 있는 네트워크 어댑터의 사용을 지원 합니다. Hyper-v 또는 Microsoft SQL Server와 같은 작업을에 대 한이 로컬 저장소와 유사 하 게 원격 파일 서버를 통해 했습니다.</p></td>
</tr>
<tr class="odd">
<td><p>서버 응용 프로그램에 대 한 성능 카운터</p></td>
<td><p>신규</p></td>
<td><p>카운터를 제공 하는 새로운 SMB 성능, 세부 당-정보를 공유 처리량, 대기 시간 및 I/O에 대 한 IOPS (초당), 관리자가 자신의 데이터가 저장 된 SMB 3.0 파일 공유의 성능을 분석할 수 있도록 합니다. 이러한 카운터는 Hyper-v 및 SQL Server 원격 파일 공유에 파일을 저장 하는 등의 서버 응용 프로그램에 대 한 특별히 설계 되었습니다.</p></td>
</tr>
<tr class="even">
<td><p>성능 최적화</p></td>
<td><p>업데이트됨</p></td>
<td><p>SMB 3.0 클라이언트와 SMB 3.0 서버 최적화 된 작은 임의 읽기/쓰기 I/O에 대 한 SQL Server OLTP 같은 서버 응용 프로그램에서 일반적으로 합니다. 또한 큰 최대 전송 단위 (MTU) 켜져 크게 성능에 큰 순차 전송, 예: SQL Server 데이터 웨어하우스에, 데이터베이스 백업 또는 복원, 배포 또는 복사 하는 가상 하드 디스크를 강화 하는 기본적으로 합니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMB 관련 Windows PowerShell cmdlet</p></td>
<td><p>신규</p></td>
<td><p>SMB에 대 한 Windows PowerShell cmdlet, 관리자가 명령줄에서 처음부터 끝까지 파일 서버의 파일 공유를 관리할 수 있습니다.</p></td>
</tr>
<tr class="even">
<td><p>SMB 암호화</p></td>
<td><p>신규</p></td>
<td><p>SMB 데이터의 끝-암호화를 제공 하 고 신뢰할 수 없는 네트워크에서 발생 한 도청 수에서 데이터를 보호 합니다. 새 배포 비용 없이 및 인터넷 프로토콜 보안 (IPsec), 전문적인된 하드웨어 또는 WAN 가속기 필요가 없는 필요합니다. 다양 한 데이터가 신뢰할 수 없는 네트워크를 통과 하는 시나리오에 대해 사용할 수 및 당 공유 별로 또는 전체 파일 서버에 대해 구성할 수 있습니다.</p></td>
</tr>
<tr class="odd">
<td><p>SMB 디렉터리 임대</p></td>
<td><p>신규</p></td>
<td><p>지사에서 응용 프로그램 응답 시간을 향상 시킵니다. 디렉터리 임대를 사용 하 여 서버에 클라이언트에서 왕복 긴 생활에서 검색 되는 메타 데이터 이후 감소는 디렉터리 캐시 합니다. 클라이언트는 서버에 있는 디렉터리 정보 변경 될 때 알림을 받을 때문에 캐시 일관성 유지 됩니다. <em>HomeFolder</em> (읽기/쓰기 없는 공유) 및 <em>게시</em> (읽기 전용으로 공유)에 대 한 시나리오에서 작동 합니다.</p></td>
</tr>
</tbody>
</table>

## <a name="hardware-requirements"></a>하드웨어 요구 사항

SMB 투명 장애 조치에는 다음 요구 사항이 있습니다.

* 구성 된 두 개 이상의 노드가 포함 된 Windows Server 2012 또는 Windows Server 2016를 실행 하는 장애 조치 클러스터 합니다. 클러스터는 유효성 검사 마법사에 포함 된 클러스터 유효성 검사 테스트를 전달 해야 합니다.
* 기본값은 지속적인 가용성 (CA) 속성을 사용 파일 공유를 만들어야 합니다.
* SMB 스케일 아웃 달성할 CSV 볼륨 경로에서 파일 공유를 만들어야 합니다.
* Windows® 8 또는 Windows Server 2012, 지속적인 가용성을 지 원하는 업데이트 된 SMB 클라이언트를 포함 하는 두 클라이언트 컴퓨터를 실행 해야 합니다.

>[!NOTE]
>하위 수준 클라이언트 CA 속성에 있는 파일 공유에 연결할 수 있지만 이러한 클라이언트에 대해 투명 하 게 장애 조치 지원 되지 않습니다.

SMB 다중 채널에는 다음 요구 사항이 있습니다.

* Windows Server 2012를 실행 하는 적어도 두 컴퓨터는 필요 합니다. 없음 추가 기능을 설치할 필요가-기술이 기본적으로 켜져 있습니다.
* 권장된 네트워크 구성에 대 한 자세한 내용은이 개요 항목의 끝에 참고 항목 섹션을 참조 하십시오.

SMB 직접에 다음 요구 사항이 있습니다.

* Windows Server 2012를 실행 하는 적어도 두 컴퓨터는 필요 합니다. 없음 추가 기능을 설치할 필요가-기술이 기본적으로 켜져 있습니다.
* RDMA 기능이 네트워크 어댑터는 필요 합니다. 이러한 어댑터 세가지 다른 종류에서 사용할 수 있는 현재: iWARP, Infiniband 또는 RoCE (RDMA over Ethernet 수렴).

## <a name="more-information"></a>자세한 정보

다음 목록에는 웹에 있는 SMB 및 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016 관련된 기술에 대 한 추가 리소스를 제공합니다.

* [WindowsServer의 저장소](../storage.md)
* [응용 프로그램 데이터에 대 한 확장 파일 서버](../../failover-clustering/sofs-overview.md)
* [직접 SMB와 파일 서버의 성능 향상](smb-direct.md)
* [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [SMB 다중 채널 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [서버 응용 프로그램에 대 한 빠르고 효율적인 파일 서버를 배포합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: 문제해결 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)