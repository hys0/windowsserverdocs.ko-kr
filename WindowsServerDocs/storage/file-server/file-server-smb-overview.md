---
title: Windows Server에서 SMB 3 프로토콜을 사용 하 여 파일 공유 개요
description: 파일 공유 및 Windows Server의 파일 서비스에 대 한 SMB 3 프로토콜 사용에 대 한 개요입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: 416145a8c4ec20eaf46cf4b5ac88a0cdf38bdf33
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919883"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Windows Server에서 SMB 3 프로토콜을 사용 하 여 파일 공유 개요

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012의 SMB 3 기능에 대해 설명 합니다 .이 기능은 이전 버전과 비교 하 여이 버전에서 가장 중요 한 새로운 기능 또는 업데이트 된 기능을 사용 하는 데 유용 합니다. 하드웨어 요구 사항 SMB는 스토리지 공간 다이렉트, 저장소 복제본 등의 [SDDC (소프트웨어 정의 데이터 센터)](../../sddc.md) 솔루션에서 사용 하는 패브릭 프로토콜 이기도 합니다. SMB 버전 3.0은 Windows Server 2012에서 도입 되었으며 이후 릴리스에서는 증분 방식으로 개선 되었습니다.

## <a name="feature-description"></a>기능 설명

SMB(서버 메시지 블록) 프로토콜은 컴퓨터의 응용 프로그램에서 파일을 읽고 쓸 수 있으며 컴퓨터 네트워크상의 서버 프로그램에서 서비스를 요청할 수 있도록 지원하는 네트워크 파일 공유 프로토콜입니다. SMB 프로토콜은 해당 TCP/IP 프로토콜이나 기타 네트워크 프로토콜상에서 사용될 수 있습니다. SMB 프로토콜을 사용하면 응용 프로그램이나 응용 프로그램의 사용자가 원격 서버에 있는 파일이나 기타 리소스를 액세스할 수 있습니다. 즉, 원격 서버의 파일을 읽고 만들며 업데이트할 수 있습니다. Smb는 SMB 클라이언트 요청을 수신 하도록 설정 된 서버 프로그램과 통신할 수도 있습니다. SMB는 스토리지 공간 다이렉트, 저장소 복제본과 같은 SDDC (소프트웨어 정의 데이터 센터) 컴퓨팅 기술에서 사용 하는 패브릭 프로토콜입니다. 자세한 내용은 [Windows Server 소프트웨어 정의 데이터 센터](../../sddc.md)를 참조 하세요.

## <a name="practical-applications"></a>유용한 팁

이 섹션에서는 새로운 SMB 3.0 프로토콜에 대한 몇 가지 새롭고 유용한 방법에 대해 설명합니다.

* **가상화용 파일 스토리지(SMB를 통한 Hyper-V™)** . Hyper-V는 SMB 3.0 프로토콜을 통한 파일 공유에 구성, VHD(가상 하드 디스크) 파일 및 스냅샷 등의 가상 머신 파일을 저장할 수 있습니다. 이 방법은 Hyper-V를 클러스터의 공유 파일 스토리지와 함께 사용하는 클러스터된 파일 서버와 독립 실행형 파일 서버에 모두 사용할 수 있습니다.
* **SMB를 통한 Microsoft SQL Server**. SQL Server는 SMB 파일 공유에 사용자 데이터베이스 파일을 저장할 수 있습니다. 현재 이 방법은 독립 실행형 SQL 서버용 SQL Server 2008 R2에서만 지원됩니다. 후속 버전의 SQL Server에서는 클러스터된 SQL 서버와 시스템 데이터베이스에 대한 지원이 추가됩니다.
* **기존의 최종 사용자 데이터용 스토리지**. SMB 3.0 프로토콜을 사용하면 정보 근로자(또는 클라이언트)의 워크로드 환경을 개선할 수 있습니다. 즉, 지점 사용자가 WAN(광역 네트워크)을 통해 데이터에 액세스할 때 경험하게 되는 애플리케이션 대기 시간을 단축하고 도청 공격으로부터 데이터를 보호할 수 있습니다.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

다음 섹션에서는 SMB 3 및 후속 업데이트에 추가 된 기능에 대해 설명 합니다.

## <a name="features-added-in-windows-server-2019-and-windows-10-version-1809"></a>Windows Server 2019 및 Windows 10 버전 1809에 추가 된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| 지속적으로 사용할 수 없는 파일 공유에서 디스크에 대 한 쓰기를 요구 하는 기능 | 신규 항목 | 파일 공유에 쓰기 작업을 수행 하 여 쓰기 작업을 완료 된 것으로 반환 하기 전에 소프트웨어 및 하드웨어 스택을 실제 디스크에 모든 방식으로 제공 하는 몇 가지 추가 보증을 제공 하기 위해 `NET USE /WRITETHROUGH` 명령을 사용 하 여 `New-SMBMapping -UseWriteThrough` PowerShell cmdlet을 사용 하 여 파일 공유에 대 한 쓰기를 설정할 수 있습니다. 쓰기를 사용 하는 데 약간의 성능 저하가 있습니다. 추가 논의는 블로그 게시물 [SMB에서 쓰기 동작 제어](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-write-through-behaviors-in-smb/bc-p/1083417#M677) 를 참조 하세요. |

## <a name="features-added-in-windows-server-version-1709-and-windows-10-version-1709"></a>Windows Server, 버전 1709 및 Windows 10 버전 1709에 추가 된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| 파일 공유에 대 한 게스트 액세스를 사용할 수 없습니다. | 신규 항목 | SMB 클라이언트는 원격 서버에 대 한 게스트 계정 액세스와 같은 작업을 더 이상 허용 하지 않습니다. 잘못 된 자격 증명이 제공 된 후 게스트 계정으로 대체 합니다. 자세한 내용은 [Windows에서 기본적으로 SMB2 사용 안 함으로 설정 된 게스트 액세스](https://support.microsoft.com/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser)를 참조 하세요. | 
| SMB 글로벌 매핑 | 신규 항목 | 컨테이너를 포함 하 여 로컬 호스트의 모든 사용자가 액세스할 수 있는 드라이브 문자에 원격 SMB 공유를 매핑합니다. 이는 데이터 볼륨에서 컨테이너 i/o를 사용 하도록 설정 하 여 원격 탑재 지점을 트래버스하는 데 필요 합니다. 컨테이너에 대해 SMB 전역 매핑을 사용 하면 컨테이너 호스트의 모든 사용자가 원격 공유에 액세스할 수 있습니다. 컨테이너 호스트에서 실행 되는 모든 응용 프로그램은 매핑된 원격 공유에도 액세스할 수 있습니다. 자세한 내용은 [CSV (클러스터 공유 볼륨)를 사용한 컨테이너 저장소 지원, 스토리지 공간 다이렉트, SMB 글로벌 매핑](https://techcommunity.microsoft.com/t5/failover-clustering/container-storage-support-with-cluster-shared-volumes-csv/ba-p/372140)을 참조 하세요. |
| SMB 언어 제어 | 신규 항목 | 이제 레지스트리 값을 설정 하 여 사용 되는 최소 SMB 버전 (언어) 및 최대 SMB 버전을 제어할 수 있습니다. 자세한 내용은 [SMB 언어 제어](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)를 참조 하세요. |

## <a name="features-added-in-smb-311-with-windows-server-2016-and-windows-10-version-1607"></a>Windows Server 2016 및 Windows 10 버전 1607에서 SMB 3.11에 추가 된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| SMB 암호화     |   업데이트됨      | AES(Advanced Encryption Standard)-Galois/Counter 모드 (AES GCM)를 사용 하는 SMB 3.1.1 암호화가 SMB 서명 또는 AES-CCM을 사용 하는 이전 SMB 암호화 보다 빠릅니다.   |
| 디렉터리 캐싱 | 신규 항목 | SMB 3.1.1는 디렉터리 캐싱의 향상 된 기능을 포함 합니다. 이제 Windows 클라이언트는 훨씬 더 큰 디렉터리, 약 500K 항목을 캐시할 수 있습니다. Windows 클라이언트는 왕복을 줄이고 성능을 향상 시키기 위해 1mb 버퍼로 디렉터리 쿼리를 시도 합니다. |
| 사전 인증 무결성 | 신규 항목 |  SMB 3.1.1에서 사전 인증 무결성은 SMB의 연결 설정 및 인증 메시지를 사용 하 여 메시지 가로채기 (man-in-the-middle) 공격자 로부터 향상 된 보호 기능을 제공 합니다. 자세한 내용은 [Windows 10의 SMB 3.1.1 사전 인증 무결성](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10)을 참조 하세요. |
| SMB 암호화 기능 향상 | 신규 항목 | SMB 3.1.1는 AES-128-CCM 및 AES-128-GCM 옵션을 사용 하 여 연결당 암호화 알고리즘을 협상 하는 메커니즘을 제공 합니다. AES-128-GCM은 새 Windows 버전에 대 한 기본값 이지만 이전 버전은 AES-128-CCM을 계속 사용 합니다. |
| 롤링 클러스터 업그레이드 지원 | 신규 항목 | 업그레이드 프로세스가 진행 중인 클러스터에 대해 smb의 다른 최대 버전을 지원 하기 위해 SMB가 표시 되도록 하 여 [클러스터를 업그레이드할](../../failover-clustering/cluster-operating-system-rolling-upgrade.md) 수 있습니다. SMB가 프로토콜의 다른 버전 (언어)을 사용 하 여 통신 하도록 허용 하는 방법에 대 한 자세한 내용은 [Smb 언어 제어](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)블로그 게시물을 참조 하세요. |
| Windows 10의 SMB 다이렉트 클라이언트 지원 | 신규 항목 | 이제 windows 10 Enterprise, Windows 10 교육용 및 Windows 10 Pro for Workstation에는 SMB 다이렉트 클라이언트 지원이 포함 됩니다. |
| FileNormalizedNameInformation API 호출에 대 한 기본 지원 | 신규 항목 | 파일의 정규화 된 이름을 쿼리 하는 기본 지원을 추가 합니다. 자세한 내용은 [FileNormalizedNameInformation](https://docs.microsoft.com/openspecs/windows_protocols/ms-fscc/20bcadba-808c-4880-b757-4af93e41edf6)를 참조 하세요. |

자세한 내용은 블로그 게시물 [Windows Server 2016 Technical Preview 2에서 제공 되는 SMB 3.1.1의 새로운 기능](https://docs.microsoft.com/archive/blogs/josebda/whats-new-in-smb-3-1-1-in-the-windows-server-2016-technical-preview-2)을 참조 하세요.

## <a name="features-added-in-smb-302-with-windows-server-2012-r2-and-windows-81"></a>Windows Server 2012 R2 및 Windows 8.1와 함께 SMB 3.02에 추가 된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| 스케일 아웃 파일 서버 클라이언트의 자동 균형 다시 맞추기     |   신규 항목      | 스케일 아웃 파일 서버의 확장성 및 관리 효율성을 향상 시킵니다. SMB 클라이언트 연결은 서버 단위가 아니라 파일 공유 단위로 추적되며, 클라이언트는 파일 공유에서 사용하는 볼륨에 대한 최상의 액세스를 제공하는 클러스터 노드로 리디렉션됩니다. 따라서 파일 서버 노드 간의 리디렉션 트래픽이 감소하므로 효율성이 향상됩니다. 클라이언트는 초기 연결 후 클러스터 스토리지가 다시 구성된 경우에 리디렉션됩니다.    |
| WAN을 통한 성능   | 업데이트됨  | Windows 8.1 및 Windows 10은 원격 컴퓨터의 한 위치에서 동일한 서버의 다른 복사본으로의 원격 복사본에 대 한 파일 탐색기를 사용 하는 경우 SMB 지원 보다 향상 된 CopyFile SRV_COPYCHUNK를 제공 합니다. 네트워크를 통해 적은 양의 메타 데이터 (파일 데이터의 경우 1/2KiB/파일 데이터를 전송)를 복사 합니다. 이로 인해 성능이 크게 향상 되었습니다. 이는 SMB에 대 한 OS 수준 및 파일 탐색기 수준 구분입니다. |
| SMB 다이렉트     |   업데이트됨      | I/O가 적은 작업(예: 가상 컴퓨터의 OLTP(온라인 트랜잭션 처리) 데이터베이스)을 호스팅할 때 효율성을 높여 소규모 I/O 작업의 성능을 향상시킵니다. 이러한 향상 된 기능은 40 Gbps 이더넷 및 56 Gbps InfiniBand 같은 고속 네트워크 인터페이스를 사용 하는 경우에 분명 하 게 드러납니다.  |
| SMB 대역폭 제한 | 신규 항목 | 이제 [SmbBandwidthLimit](https://docs.microsoft.com/powershell/module/smbshare/set-smbbandwidthlimit) 을 사용 하 여 세 가지 범주인 VIRTUALMACHINE (smb 트래픽을 통한 hyper-v), LiveMigration (HYPER-V 실시간 마이그레이션 smb를 통한 트래픽) 또는 기본값 (다른 모든 유형의 smb 트래픽)으로 대역폭 제한을 설정할 수 있습니다.

Windows Server 2012 r 2의 새로운 SMB 기능 및 변경 된 기능에 대 한 자세한 내용은 [Windows server에서](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>)제공 되는 Smb의 새로운 기능을 참조 하세요.

## <a name="features-added-in-smb-30-with-windows-server-2012-and-windows-8"></a>Windows Server 2012 및 Windows 8을 사용 하 여 SMB 3.0에 추가 된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| SMB 투명 장애 조치(Failover)     |   신규 항목    | 관리자는 서버 애플리케이션에서 이러한 파일 공유에 데이터를 저장하는 것을 인터럽트하지 않고도 클러스터된 파일 서버의 노드에서 하드웨어 또는 소프트웨어 유지 관리 작업을 수행할 수 있습니다. 또한 클러스터 노드에서 하드웨어 또는 소프트웨어 오류가 발생하면 SMB 클라이언트는 이러한 파일 공유에 데이터를 저장하는 애플리케이션을 인터럽트하지 않고 다른 클러스터 노드로 투명하게 다시 연결합니다.        |
| SMB 스케일 아웃     |   신규 항목      | 스케일 아웃 파일 서버에서 여러 SMB 인스턴스 지원. CSV(클러스터 공유 볼륨) 버전 2를 사용할 경우 관리자는 파일 서버 클러스터의 모든 노드 전반에서 직접 I/O를 사용하여 데이터 파일에 대한 동시 액세스가 가능한 파일 공유를 만들 수 있습니다. 이 기능을 통해 네트워크 대역폭의 사용률과 파일 서버 클라이언트의 부하 분산 효과를 향상시키고 서버 애플리케이션의 성능을 최적화할 수 있습니다.  |
| SMB 다중 채널     |   신규 항목      |  SMB 클라이언트와 서버 간에 여러 경로를 사용할 수 있는 경우 네트워크 대역폭과 네트워크 내결함성을 집계할 수 있습니다. 이 기능을 통해 서버 애플리케이션은 사용 가능한 모든 네트워크 대역폭을 완벽하게 활용할 수 있으며 네트워크 오류에 탄력적으로 대처할 수 있습니다.<br><br>Smb 3에서 SMB 다중 채널은 이전 버전의 SMB에 비해 성능이 크게 향상 되었습니다. |
| SMB 다이렉트     |   신규 항목      | RDMA 기능을 갖추고, 대기 시간은 아주 적으면서 최대 속도로 작동할 수 있는 반면 CPU 소모량은 거의 없는 네트워크 어댑터를 사용할 수 있습니다. Hyper-V 또는 Microsoft SQL Server 등의 워크로드에 이 기능을 사용하면 원격 파일 서버가 로컬 스토리지와 비슷한 역할을 할 수 있습니다.<br><br>Smb 3의 SMB 다이렉트는 이전 버전의 SMB에 비해 성능이 크게 향상 되었습니다.  |
| 서버 애플리케이션의 성능 카운터     |   신규 항목      |  새로운 SMB 성능 카운터는 처리량, 대기 시간 및 IOPS (초당 I/o)에 대 한 세부 정보를 공유 하는 정보를 제공 하 여 관리자가 데이터가 저장 된 SMB 파일 공유의 성능을 분석할 수 있도록 합니다. 이러한 카운터는 특히, Hyper-V 및 SQL Server와 같이 파일을 원격 파일 서버에 저장하는 서버 애플리케이션을 위해 만들어졌습니다.      |
| 성능 최적화    |  업데이트됨   | SMB 클라이언트와 서버는 모두 SQL Server OLTP와 같은 서버 응용 프로그램에서 공통 되는 작은 임의 읽기/쓰기 i/o에 최적화 되었습니다. 또한 대량의 최대 전송 단위(MTU)가 기본적으로 켜져 있어 SQL Server 데이터 웨어하우스, 데이터베이스 백업이나 복원, 가상 하드 디스크 배포나 복사 등의 대형 순차 전송 성능이 눈에 띄게 향상되었습니다. |
| SMB별 Windows PowerShell Cmdlet     |   신규 항목      |  관리자는 명령줄에서 SMB용 Windows PowerShell cmdlet을 사용하여 종단 간 방식으로 파일 서버에서 파일 공유를 관리할 수 있습니다.   |
| SMB 암호화     |   신규 항목      | SMB 데이터에 대한 엔드투엔드 암호화 기능을 제공하며, 신뢰할 수 없는 네트워크에서 발생하는 도청으로부터 데이터를 보호합니다. 새로운 배포 비용이 발생하지 않고 인터넷 프로토콜 보안(IPsec), 특수 하드웨어 또는 WAN 가속기가 필요하지 않습니다. 이 기능은 공유 단위별로 구성하거나 전체 파일 서버용으로 구성할 수 있으며 신뢰할 수 없는 네트워크에서 데이터가 전송되는 다양한 시나리오에서 사용할 수 있습니다. |
| SMB 디렉터리 임대     |  신규 항목 | 지점에서의 애플리케이션 응답 시간이 향상됩니다. 디렉터리 임대를 사용하면 라이브 상태가 더 길어진 디렉터리 캐시로부터 메타데이터가 검색되므로 클라이언트에서 서버로의 왕복 시간이 단축됩니다. 서버의 디렉터리 정보가 변경되면 클라이언트에게 통보되므로 캐시 일관성이 유지됩니다. 디렉터리 임대는 비포함 (공유 없이 읽기/쓰기) 및 게시 (공유 포함 읽기 전용)에 대 한 시나리오와 함께 작동 합니다.    |
| WAN을 통한 성능   | 신규 항목   | Oplock (디렉터리 oplocks) 및 oplock 임대가 SMB 3.0에서 도입 되었습니다. 일반적인 사무실/클라이언트 워크 로드의 경우 네트워크 왕복을 약 15%까지 줄이기 위해 oplock/임대가 표시 됩니다.<br><br>SMB 3에서 SMB의 Windows 구현은 클라이언트의 캐싱 동작을 개선 하 고 더 높은 처리량을 푸시하는 기능을 개선 했습니다.<br><br>SMB 3에서는 CopyFile () API와 Robocopy와 같은 연결 된 도구에 대 한 향상 된 기능을 제공 하 여 네트워크를 통해 훨씬 더 많은 데이터를 푸시합니다. |
| 보안 언어 협상 | 신규 항목 | 언어 협상을 다운 그레이드 하려는 메시지 가로채기 (man-in-the-middle) 공격을 방지 합니다. 이 개념은 도청자가 클라이언트와 서버 간의 초기에 협상 된 언어와 기능을 다운 그레이드 하는 것을 방지 하는 것입니다. 자세한 내용은 [SMB3 Secure 언어 협상](https://docs.microsoft.com/archive/blogs/openspecification/smb3-secure-dialect-negotiation)을 참조 하세요. SMB 3.1.1의 [Windows 10 기능에서 smb 3.1.1 사전 인증 무결성](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10) 이 대체 되었습니다. |


## <a name="hardware-requirements"></a>하드웨어 요구 사항

SMB 투명 장애 조치(Failover)의 요구 사항은 다음과 같습니다.

* 두 개 이상의 노드가 구성 된 windows Server 2012 또는 Windows Server 2016를 실행 하는 장애 조치 (failover) 클러스터 클러스터는 유효성 검사 마법사에 포함된 클러스터 유효성 테스트를 통과해야 합니다.
* 파일 공유는 CA(Continuous Availability) 속성이 기본값으로 설정되어 만들어져야 합니다.
* 파일 공유를 CSV 볼륨 경로에 만들어야 SMB 스케일 아웃에 도달할 수 있습니다.
* 클라이언트 컴퓨터는 지속적인 가용성을 지 원하는 업데이트 된 SMB 클라이언트를 포함 하 여 Windows® 8 또는 Windows Server 2012를 실행 해야 합니다.

> [!NOTE]
> 하위 수준 클라이언트는 CA 속성이 있는 파일 공유에 연결할 수 있지만 이러한 클라이언트에는 투명 장애 조치 (failover)가 지원 되지 않습니다.

SMB 다중 채널의 요구 사항은 다음과 같습니다.

* Windows Server 2012를 실행 하는 컴퓨터가 두 대 이상 필요 합니다. 이 기술은 추가 기능을 설치할 필요 없이 기본적으로 작동됩니다.
* 권장 네트워크 구성에 대한 자세한 내용은 이 개요 항목의 마지막 부분에 있는 참고 항목을 참조하세요.

SMB 다이렉트의 요구 사항은 다음과 같습니다.

* Windows Server 2012를 실행 하는 컴퓨터가 두 대 이상 필요 합니다. 이 기술은 추가 기능을 설치할 필요 없이 기본적으로 작동됩니다.
* RDMA 기능이 있는 네트워크 어댑터가 필요합니다. 현재 이러한 어댑터는 iWARP, Infiniband 또는 RoCE(RDMA over Converged Ethernet) 유형으로 제공됩니다.

## <a name="more-information"></a>추가 정보

다음 목록에서는 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 SMB 및 관련 기술에 대해 웹의 추가 리소스를 제공 합니다.

* [Windows Server의 스토리지](../storage.md)
* [응용 프로그램 데이터에 대 한 스케일 아웃 파일 서버](../../failover-clustering/sofs-overview.md)
* [SMB 다이렉트를 사용 하 여 파일 서버의 성능 향상](smb-direct.md)
* [SMB를 통한 Hyper-v 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [SMB 다중 채널 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [서버 응용 프로그램을 위한 빠르고 효율적인 파일 서버 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: 문제 해결 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)
