---
title: Windows Server에서 SMB 3 프로토콜을 사용하여 파일 공유 개요
description: Windows Server에서 파일 공유 및 파일 서비스에 SMB 3 프로토콜 사용에 대한 개요입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 01/10/2020
ms.localizationpriority: medium
ms.openlocfilehash: aafcfcd4d0f2f14836c5b7dee2bdbccbf99fa887
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "78169623"
---
# <a name="overview-of-file-sharing-using-the-smb-3-protocol-in-windows-server"></a>Windows Server에서 SMB 3 프로토콜을 사용하여 파일 공유 개요

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 토픽에서는 Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012에서 제공하는 SMB 3 기능의 유용한 사용 방법을 살펴보고, 이전 버전과 비교하여 이번 버전에서 가장 눈에 띄는 새로운 기능이나 업데이트된 기능과 하드웨어 요구 사항에 대해 알아봅니다. SMB는 스토리지 공간 다이렉트, 스토리지 복제본 등의 [SDDC(소프트웨어 정의 데이터 센터)](../../sddc.md) 솔루션에 사용되는 패브릭 프로토콜이기도 합니다. SMB 버전 3.0은 Windows Server 2012에서 도입되었으며 이후 릴리스에서 점진적으로 개선되었습니다.

## <a name="feature-description"></a>기능 설명

SMB(서버 메시지 블록) 프로토콜은 컴퓨터의 애플리케이션에서 파일을 읽고 쓸 수 있으며 컴퓨터 네트워크상의 서버 프로그램에서 서비스를 요청할 수 있도록 지원하는 네트워크 파일 공유 프로토콜입니다. SMB 프로토콜은 해당 TCP/IP 프로토콜이나 기타 네트워크 프로토콜상에서 사용될 수 있습니다. SMB 프로토콜을 사용하면 애플리케이션이나 애플리케이션의 사용자가 원격 서버에 있는 파일이나 기타 리소스를 액세스할 수 있습니다. 즉, 원격 서버의 파일을 읽고 만들며 업데이트할 수 있습니다. 또한 SMB는 SMB 클라이언트 요청을 수신하도록 설정된 서버 프로그램과 통신할 수 있습니다. SMB는 스토리지 공간 다이렉트, 스토리지 복제본 등의 SDDC(소프트웨어 정의 데이터 센터) 컴퓨팅 기술에 사용되는 패브릭 프로토콜이기도 합니다. 자세한 내용은 [Windows Server 소프트웨어 정의 데이터 센터](../../sddc.md)를 참조하세요.

## <a name="practical-applications"></a>유용한 팁

이 섹션에서는 새로운 SMB 3.0 프로토콜에 대한 몇 가지 새롭고 유용한 방법에 대해 설명합니다.

* **가상화용 파일 스토리지(SMB를 통한 Hyper-V™)** . Hyper-V는 SMB 3.0 프로토콜을 통한 파일 공유에 구성, VHD(가상 하드 디스크) 파일 및 스냅샷 등의 가상 머신 파일을 저장할 수 있습니다. 이 방법은 Hyper-V를 클러스터의 공유 파일 스토리지와 함께 사용하는 클러스터된 파일 서버와 독립 실행형 파일 서버에 모두 사용할 수 있습니다.
* **SMB를 통한 Microsoft SQL Server**. SQL Server는 SMB 파일 공유에 사용자 데이터베이스 파일을 저장할 수 있습니다. 현재 이 방법은 독립 실행형 SQL 서버용 SQL Server 2008 R2에서만 지원됩니다. 후속 버전의 SQL Server에서는 클러스터된 SQL 서버와 시스템 데이터베이스에 대한 지원이 추가됩니다.
* **기존의 최종 사용자 데이터용 스토리지**. SMB 3.0 프로토콜을 사용하면 정보 근로자(또는 클라이언트)의 워크로드 환경을 개선할 수 있습니다. 즉, 지점 사용자가 WAN(광역 네트워크)을 통해 데이터에 액세스할 때 경험하게 되는 애플리케이션 대기 시간을 단축하고 도청 공격으로부터 데이터를 보호할 수 있습니다.

## <a name="new-and-changed-functionality"></a>새로운 기능 및 변경된 기능

다음 섹션에서는 SMB 3 및 후속 업데이트에 추가된 기능에 대해 설명합니다.

## <a name="features-added-in-windows-server-2019-and-windows-10-version-1809"></a>Windows Server 2019 및 Windows 10 버전 1809에 추가된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| 지속적으로 사용할 수 없는 파일 공유의 디스크에 대한 쓰기를 요구하는 기능 | 새로 만들기 | 파일 공유에 쓰면 소프트웨어 및 하드웨어 스택을 거쳐 실제 디스크에 쓰기가 수행된 후 쓰기 작업이 완료된다는 확신을 심어주기 위해, `NET USE /WRITETHROUGH` 명령 또는 `New-SMBMapping -UseWriteThrough` PowerShell cmdlet을 사용하여 파일 공유에 대한 쓰기를 설정할 수 있습니다. 쓰기를 사용하면 약간의 성능 저하가 있습니다. 자세한 내용은 블로그 게시물 [Controlling write-through behaviors in SMB(SMB의 쓰기 동작 제어)](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-write-through-behaviors-in-smb/bc-p/1083417#M677)를 참조하세요. |

## <a name="features-added-in-windows-server-version-1709-and-windows-10-version-1709"></a>Windows Server 버전 1709 및 Windows 10 버전 1709에 추가된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| 파일 공유에 게스트로 액세스할 수 없음 | 새로 만들기 | SMB 클라이언트에서 더 이상 다음을 허용하지 않습니다. 원격 서버에 게스트 계정으로 액세스. 잘못된 자격 증명이 입력되면 게스트 계정으로 대체됩니다. 자세한 내용은 [Windows에서는 기본적으로 SMB2에서 게스트 액세스 사용 안 함](https://support.microsoft.com/help/4046019/guest-access-in-smb2-disabled-by-default-in-windows-10-and-windows-ser)을 참조하세요. | 
| SMB 글로벌 매핑 | 새로 만들기 | 컨테이너를 포함하여 로컬 호스트의 모든 사용자가 액세스할 수 있는 드라이브 문자에 원격 SMB 공유를 매핑합니다. 이는 데이터 볼륨에서 컨테이너 I/O를 사용하도록 설정하여 원격 탑재 지점을 트래버스하는 데 필요합니다. 컨테이너에 대해 SMB 글로벌 매핑을 사용할 때 컨테이너 호스트의 모든 사용자가 원격 공유에 액세스할 수 있습니다. 컨테이너 호스트에서 실행되는 모든 애플리케이션 또한 매핑된 원격 공유에 액세스할 수 있습니다. 자세한 내용은 [CSV(클러스터 공유 볼륨), 스토리지 공간 다이렉트, SMB 글로벌 매핑을 통한 컨테이너 스토리지 지원](https://techcommunity.microsoft.com/t5/failover-clustering/container-storage-support-with-cluster-shared-volumes-csv/ba-p/372140)을 참조하세요. |
| SMB 언어 제어 | 새로 만들기 | 이제 레지스트리 값을 설정하여 사용되는 최소 SMB 버전(언어) 및 최대 SMB 버전을 제어할 수 있습니다. 자세한 내용은 [Controlling SMB Dialects(SMB 언어 제어)](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)를 참조하세요. |

## <a name="features-added-in-smb-311-with-windows-server-2016-and-windows-10-version-1607"></a>Windows Server 2016 및 Windows 10 버전 1607에서 SMB 3.11에 추가된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| SMB 암호화     |   업데이트됨      | AES-GCM(Advanced Encryption Standard-Galois/Counter Mode)을 사용하는 SMB 3.1.1 암호화는 SMB 서명 또는 AES-CCM을 사용하는 이전 SMB 암호화보다 빠릅니다.   |
| 디렉터리 캐싱 | 새로 만들기 | SMB 3.1.1은 향상된 디렉터리 캐싱 기능을 포함하고 있습니다. 이제 Windows 클라이언트는 훨씬 큰 디렉터리 약 500000개 항목을 캐시할 수 있습니다. Windows 클라이언트는 왕복을 줄이고 성능을 향상하기 위해 1MB 버퍼로 디렉터리 쿼리를 시도합니다. |
| 사전 인증 무결성 | 새로 만들기 |  SMB 3.1.1에서 사전 인증 무결성은 SMB의 연결 설정 및 인증 메시지를 변조하는 가로채기 공격자로부터 향상된 보호 기능을 제공합니다. 자세한 내용은 [Windows 10의 SMB 3.1.1 사전 인증 무결성](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10)을 참조하세요. |
| SMB 암호화 기능 향상 | 새로 만들기 | SMB 3.1.1은 AES-128-CCM 및 AES-128-GCM 옵션을 사용하여 연결마다 암호화 알고리즘을 협상하는 메커니즘을 제공합니다. AES-128-GCM은 새 Windows 버전의 기본값이지만, 이전 버전은 AES-128-CCM을 계속 사용합니다. |
| 롤링 클러스터 업그레이드 지원 | 새로 만들기 | 업그레이드 중인 클러스터에 다른 최대 버전의 SMB를 지원하는 것으로 SMB를 표시할 수 있도록 [롤링 클러스터 업그레이드](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)를 사용합니다. SMB가 다른 버전(언어)의 프로토콜을 사용하여 통신할 수 있도록 허용하는 방법에 대한 자세한 내용은 블로그 게시물 [Controlling SMB Dialects(SMB 언어 제어)](https://techcommunity.microsoft.com/t5/storage-at-microsoft/controlling-smb-dialects/ba-p/860024)를 참조하세요. |
| Windows 10에서 SMB 다이렉트 클라이언트 지원 | 새로 만들기 | 이제 Windows 10 Enterprise, Windows 10 Education 및 Windows 10 Pro for Workstations에 SMB 다이렉트 클라이언트 지원이 포함됩니다. |
| FileNormalizedNameInformation API 호출 기본 지원 | 새로 만들기 | 파일의 정규화된 이름을 쿼리하는 기본 지원이 추가됩니다. 자세한 내용은 [FileNormalizedNameInformation](https://docs.microsoft.com/openspecs/windows_protocols/ms-fscc/20bcadba-808c-4880-b757-4af93e41edf6)을 참조하세요. |

자세한 내용은 블로그 게시물 [Windows Server 2016 기술 개요 2의 SMB 3.1.1의 새 기능](https://docs.microsoft.com/archive/blogs/josebda/whats-new-in-smb-3-1-1-in-the-windows-server-2016-technical-preview-2)을 참조하세요.

## <a name="features-added-in-smb-302-with-windows-server-2012-r2-and-windows-81"></a>Windows Server 2012 R2 및 Windows 8.1에서 SMB 3.02에 추가된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| 스케일 아웃 파일 서버 클라이언트의 자동 균형 다시 맞추기     |   새로 만들기      | 스케일 아웃 파일 서버의 확장성 및 관리 효율성을 향상시킵니다. SMB 클라이언트 연결은 서버 단위가 아니라 파일 공유 단위로 추적되며, 클라이언트는 파일 공유에서 사용하는 볼륨에 대한 최상의 액세스를 제공하는 클러스터 노드로 리디렉션됩니다. 따라서 파일 서버 노드 간의 리디렉션 트래픽이 감소하므로 효율성이 향상됩니다. 클라이언트는 초기 연결 후 클러스터 스토리지가 다시 구성된 경우에 리디렉션됩니다.    |
| WAN을 통한 성능   | 업데이트됨  | Windows 8.1 및 Windows 10은 파일 탐색기를 사용하여 원격 머신의 한 위치에서 동일한 서버의 다른 복사본으로의 원격 복사할 때 SMB 지원을 통해 향상된 CopyFile SRV_COPYCHUNK를 제공합니다. 네트워크를 통해 적은 양의 메타데이터만 복사됩니다(파일 데이터 16MiB당 1/2KiB 전송). 따라서 성능이 크게 향상됩니다. 이는 OS 수준 및 파일 탐색기 수준에서 SMB의 탁월한 장점입니다. |
| SMB 다이렉트     |   업데이트됨      | I/O가 적은 작업(예: 가상 컴퓨터의 OLTP(온라인 트랜잭션 처리) 데이터베이스)을 호스팅할 때 효율성을 높여 소규모 I/O 작업의 성능을 향상시킵니다. 이러한 성능 향상은 40Gbps 이더넷 및 56Gbps InfiniBand와 같은 고속 네트워크 인터페이스를 사용할 때 명확하게 나타납니다.  |
| SMB 대역폭 제한 | 새로 만들기 | 이제 [Set-SmbBandwidthLimit](https://docs.microsoft.com/powershell/module/smbshare/set-smbbandwidthlimit)를 사용하여 VirtualMachine(SMB 트래픽을 통한 Hyper-V), LiveMigration(SMB를 통한 Hyper-V 실시간 마이그레이션 트래픽) 또는 기본값(그 외의 모든 SMB 트래픽 유형)의 세 가지 범주로 대역폭 제한을 설정할 수 있습니다.

Windows Server 2012 R2의 새 SMB 기능 및 변경된 기능에 대한 자세한 내용은 [Windows Server에서 제공되는 SMB의 새로운 기능](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)>)을 참조하세요.

## <a name="features-added-in-smb-30-with-windows-server-2012-and-windows-8"></a>Windows Server 2012 및 Windows 8에서 SMB 3.0에 추가된 기능

| 기능  | 새로운 기능 또는 업데이트된 기능  | 요약  |
| --------- | --------- | --------- |
| SMB 투명 장애 조치(Failover)     |   새로 만들기    | 관리자는 서버 애플리케이션에서 이러한 파일 공유에 데이터를 저장하는 것을 인터럽트하지 않고도 클러스터된 파일 서버의 노드에서 하드웨어 또는 소프트웨어 유지 관리 작업을 수행할 수 있습니다. 또한 클러스터 노드에서 하드웨어 또는 소프트웨어 오류가 발생하면 SMB 클라이언트는 이러한 파일 공유에 데이터를 저장하는 애플리케이션을 인터럽트하지 않고 다른 클러스터 노드로 투명하게 다시 연결합니다.        |
| SMB 스케일 아웃     |   새로 만들기      | 스케일 아웃 파일 서버에서 여러 SMB 인스턴스 지원 CSV(클러스터 공유 볼륨) 버전 2를 사용할 경우 관리자는 파일 서버 클러스터의 모든 노드 전반에서 직접 I/O를 사용하여 데이터 파일에 대한 동시 액세스가 가능한 파일 공유를 만들 수 있습니다. 이 기능을 통해 네트워크 대역폭의 사용률과 파일 서버 클라이언트의 부하 분산 효과를 향상시키고 서버 애플리케이션의 성능을 최적화할 수 있습니다.  |
| SMB 다중 채널     |   새로 만들기      |  SMB 클라이언트와 서버 사이에 여러 경로가 있는 경우 네트워크 대역폭과 네트워크 내결함성을 집계할 수 있습니다. 이 기능을 통해 서버 애플리케이션은 사용 가능한 모든 네트워크 대역폭을 완벽하게 활용할 수 있으며 네트워크 오류에 탄력적으로 대처할 수 있습니다.<br><br>SMB 3의 SMB 다중 채널은 이전 버전의 SMB에 비해 성능이 크게 향상되었습니다. |
| SMB 다이렉트     |   새로 만들기      | RDMA 기능을 갖추고, 대기 시간은 아주 적으면서 최대 속도로 작동할 수 있는 반면 CPU 소모량은 거의 없는 네트워크 어댑터를 사용할 수 있습니다. Hyper-V 또는 Microsoft SQL Server 등의 워크로드에 이 기능을 사용하면 원격 파일 서버가 로컬 스토리지와 비슷한 역할을 할 수 있습니다.<br><br>SMB 3의 SMB 다이렉트는 이전 버전의 SMB에 비해 성능이 크게 향상되었습니다.  |
| 서버 애플리케이션의 성능 카운터     |   새로 만들기      |  새로운 SMB 성능 카운터는 공유별 처리량, 대기 시간 및 IOPS(초당 I/O) 정보를 자세히 분석하여 관리자들이 데이터가 저장된 SMB 파일 공유 성능을 분석할 수 있습니다. 이러한 카운터는 특히, Hyper-V 및 SQL Server와 같이 파일을 원격 파일 서버에 저장하는 서버 애플리케이션을 위해 만들어졌습니다.      |
| 성능 최적화    |  업데이트됨   | SMB 클라이언트와 SMB 서버 모두 SQL Server OLTP 같은 서버 애플리케이션에서 일반적으로 쓰이는 소량의 임의 읽기/쓰기 I/O에 최적화되었습니다. 또한 대량의 최대 전송 단위(MTU)가 기본적으로 켜져 있어 SQL Server 데이터 웨어하우스, 데이터베이스 백업이나 복원, 가상 하드 디스크 배포나 복사 등의 대형 순차 전송 성능이 눈에 띄게 향상되었습니다. |
| SMB별 Windows PowerShell Cmdlet     |   새로 만들기      |  관리자는 명령줄에서 SMB용 Windows PowerShell cmdlet을 사용하여 종단 간 방식으로 파일 서버에서 파일 공유를 관리할 수 있습니다.   |
| SMB 암호화     |   새로 만들기      | SMB 데이터에 대한 엔드투엔드 암호화 기능을 제공하며, 신뢰할 수 없는 네트워크에서 발생하는 도청으로부터 데이터를 보호합니다. 새로운 배포 비용이 발생하지 않고 인터넷 프로토콜 보안(IPsec), 특수 하드웨어 또는 WAN 가속기가 필요하지 않습니다. 이 기능은 공유 단위별로 구성하거나 전체 파일 서버용으로 구성할 수 있으며 신뢰할 수 없는 네트워크에서 데이터가 전송되는 다양한 시나리오에서 사용할 수 있습니다. |
| SMB 디렉터리 임대     |  새로 만들기 | 지점에서의 애플리케이션 응답 시간이 향상됩니다. 디렉터리 임대를 사용하면 라이브 상태가 더 길어진 디렉터리 캐시로부터 메타데이터가 검색되므로 클라이언트에서 서버로의 왕복 시간이 단축됩니다. 서버의 디렉터리 정보가 변경되면 클라이언트에게 통보되므로 캐시 일관성이 유지됩니다. 디렉터리 임대는 홈폴더(공유 비포함 읽기/쓰기) 및 게시(공유 포함 읽기 전용) 시나리오에 사용할 수 있습니다.    |
| WAN을 통한 성능   | 새로 만들기   | 디렉터리 편의적 잠금(oplocks) 및 oplock 임대는 SMB 3.0에 도입되었습니다. 일반적인 사무실/클라이언트 워크로드의 경우 oplock/임대를 사용하면 네트워크 왕복이 약 15% 감소하는 것으로 보입니다.<br><br>SMB 3에서 SMB의 Windows 구현은 클라이언트의 캐싱 동작을 개선하고 더 높은 처리량을 푸시하도록 개선되었습니다.<br><br>SMB 3에서는 네트워크를 통해 훨씬 많은 데이터를 푸시할 수 있도록 CopyFile() API와 Robocopy 같은 관련 도구의 성능이 개선되었습니다. |
| 보안 언어 협상 | 새로 만들기 | 언어 협상을 다운그레이드하려는 메시지 가로채기 공격을 차단합니다. 이것은 도청자가 클라이언트와 서버 간에 초기에 협상된 언어와 기능을 다운그레이드하는 것을 방지하는 개념입니다. 자세한 내용은 [SMB3 보안 언어 협상](https://docs.microsoft.com/archive/blogs/openspecification/smb3-secure-dialect-negotiation)을 참조하세요. 이 기능은 SMB 3.1.1에서 제공하는 [Windows 10의 SMB 3.1.1 사전 인증 무결성](https://docs.microsoft.com/archive/blogs/openspecification/smb-3-1-1-pre-authentication-integrity-in-windows-10) 기능으로 대체되었습니다. |


## <a name="hardware-requirements"></a>하드웨어 요구 사항

SMB 투명 장애 조치(Failover)의 요구 사항은 다음과 같습니다.

* Windows Server 2012 또는 Windows Server 2016을 실행하는 장애 조치(failover) 클러스터에 노드가 두 개 이상 구성되어야 합니다. 클러스터는 유효성 검사 마법사에 포함된 클러스터 유효성 테스트를 통과해야 합니다.
* 파일 공유는 CA(Continuous Availability) 속성이 기본값으로 설정되어 만들어져야 합니다.
* 파일 공유를 CSV 볼륨 경로에 만들어야 SMB 스케일 아웃에 도달할 수 있습니다.
* 클라이언트 컴퓨터에서 Windows® 8 또는 Windows Server 2012를 실행하고 있어야 하고, 두 제품 모두 지속적인 가용성을 지원하는 업데이트된 SMB 클라이언트를 포함하고 있어야 합니다.

> [!NOTE]
> 하위 수준 클라이언트는 CA 속성이 있는 파일 공유에 연결할 수 있지만, 이러한 클라이언트에는 투명한 장애 조치(failover)가 지원되지 않습니다.

SMB 다중 채널의 요구 사항은 다음과 같습니다.

* Windows Server 2012를 실행하는 두 대 이상의 컴퓨터. 이 기술은 추가 기능을 설치할 필요 없이 기본적으로 작동됩니다.
* 권장 네트워크 구성에 대한 자세한 내용은 이 개요 항목의 마지막 부분에 있는 참고 항목을 참조하세요.

SMB 다이렉트의 요구 사항은 다음과 같습니다.

* Windows Server 2012를 실행하는 두 대 이상의 컴퓨터. 이 기술은 추가 기능을 설치할 필요 없이 기본적으로 작동됩니다.
* RDMA 기능이 있는 네트워크 어댑터가 필요합니다. 현재 이러한 어댑터는 iWARP, Infiniband 또는 RoCE(RDMA over Converged Ethernet) 유형으로 제공됩니다.

## <a name="more-information"></a>자세한 정보

다음 목록은 Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 SMB 및 관련 기술에 대한 웹의 추가 리소스입니다.

* [Windows Server의 스토리지](../storage.md)
* [애플리케이션 데이터를 위한 스케일 아웃 파일 서버](../../failover-clustering/sofs-overview.md)
* [SMB 다이렉트를 사용하여 파일 서버의 성능 향상](smb-direct.md)
* [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
* [SMB 다중 채널 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn610980(v%3dws.11)>)
* [서버 애플리케이션을 위한 신속하고 효율적인 파일 서버 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
* [SMB: 문제 해결 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn659439(v%3dws.11)>)
