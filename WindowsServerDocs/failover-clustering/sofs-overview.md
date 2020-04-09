---
title: 애플리케이션 데이터를 위한 스케일 아웃 파일 서버 개요
description: Windows Server 201 R2 및 Windows Server 2012의 스케일 아웃 파일 서버 기능에 대 한 개요입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
manager: lizross
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 78f95f25d365b1b30a9e4e2d311128b8c7cb13b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827416"
---
# <a name="scale-out-file-server-for-application-data-overview"></a>애플리케이션 데이터를 위한 스케일 아웃 파일 서버 개요

>적용 대상: Windows Server 2012 R2, Windows Server 2012

스케일 아웃 파일 서버는 파일 기반 서버 응용 프로그램 스토리지에 계속 사용할 수 있는 스케일 아웃 파일 공유를 제공하도록 설계된 기능입니다. 스케일 아웃 파일 공유는 같은 클러스터의 여러 노드에서 동일한 폴더를 공유하는 기능을 제공합니다. 이 시나리오는 스케일 아웃 파일 서버를 계획 및 배포하는 방법에 중점을 둡니다.

다음 방법 중 하나를 사용하여 클러스터된 파일 서버를 배포 및 구성할 수 있습니다.

- **응용 프로그램 데이터에 대 한 스케일 아웃 파일 서버** 이 클러스터 된 파일 서버 기능은 Windows Server 2012에 도입 되었으며,이 기능을 사용 하면 Hyper-v 가상 컴퓨터 파일과 같은 서버 응용 프로그램 데이터를 파일 공유에 저장 하 고, 저장 영역 네트워크에서 제공 되는 것과 비슷한 수준의 안정성, 가용성, 관리 효율성 및 고성능을 얻을 수 있습니다. 모든 파일 공유는 모든 노드에서 동시에 온라인 상태입니다. 이런 종류의 클러스터된 파일 서버와 연결된 파일 공유는 스케일 아웃 파일 공유라고 불립니다. 이는 때에 따라 활성-활성이라고도 불립니다. SMB(서버 메시지 블록)를 통해 Hyper-V를 배포하거나 SMB를 통해 Microsoft SQL Server를 배포하는 경우에 권장되는 파일 서버 유형입니다.
- **일반 용도의 파일 서버** 이는 장애 조치(failover) 클러스터링이 도입된 이후 Windows Server에서 지원되는 클러스터된 파일 서버의 연장선 상에 있습니다. 이 종류의 클러스터된 파일 서버 및 클러스터된 파일 서버와 연결된 모든 공유는 한 번에 한 노드에서 온라인 상태입니다. 활성-수동 또는 이중-활성으로 불리는 경우도 있습니다. 이러한 종류의 클러스터된 파일 서버와 연결된 파일 공유는 클러스터된 파일 공유라 불립니다. 정보 근로자 시나리오를 배포하는 경우에 권장되는 파일 서버 유형입니다.

## <a name="scenario-description"></a>시나리오 설명

스케일 아웃 파일 공유를 사용하면 클러스터의 여러 노드에서 동일한 폴더를 공유할 수 있습니다. 예를 들어 SMB (서버 메시지 블록) 스케일 아웃을 사용 하는 4 개 노드 파일 서버 클러스터를 사용 하는 경우 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 컴퓨터는 네 개 노드 중 하나에서 파일 공유에 액세스할 수 있습니다. 이는 새로운 Windows Server 장애 조치(failover) 클러스터링 기능 및 Windows 파일 서버 프로토콜, SMB 3.0의 기능을 활용하여 달성됩니다. 파일 서버 관리자는 스케일 아웃 파일 공유 및 지속적으로 사용할 수 있는 파일 서비스를 서버 애플리케이션에 제공하여 더 많은 서버를 온라인 상태로 전환하는 방법을 통해 늘어나는 수요에 재빠르게 대응할 수 있습니다. 이 모든 과정이 프로덕션 환경에서 서버 애플리케이션에 완전히 투명하게 실행됩니다.

스케일 아웃 파일 서버에서 제공하는 주요 이점은 다음과 같습니다.

- **활성-활성 파일 공유**. 모든 클러스터 노드는 SMB 클라이언트 요청을 수락 하 고 제공할 수 있습니다. 모든 클러스터 노드를 통해 파일 공유 콘텐츠에 동시에 액세스할 수 있도록 만드는 방법으로 SMB 3.0 클러스터 및 클라이언트는 서비스 중단을 수반하는 예기치 않은 실패 및 계획된 유지 보수가 발생할 때 투명한 장애 조치(failover)를 대체 클러스터 노드에 제공할 수 있도록 협력합니다.
- **증가 된 대역폭**. 최대 공유 대역폭은 모든 파일 서버 클러스터 노드의 총 대역폭입니다. Windows Server의 이전 버전과는 다르게 총 대역폭은 더 이상 단일 클러스터 노드의 대역폭으로 제한되지 않으며 오히려 지원 스토리지 시스템의 기능이 제약 조건을 정의합니다. 노드를 추가하면 총 대역폭을 높일 수 있습니다.
- **CHKDSK에서 가동 중지 시간을 0으로 바꿉니다**. Windows Server 2012의 CHKDSK는 복구를 위해 파일 시스템이 오프 라인 상태가 되는 시간을 크게 단축 하도록 크게 향상 되었습니다. CSV(클러스터된 공유 볼륨)는 오프라인 단계를 제거하여 이를 한 단계 더 발전시킵니다. CSVFS(CSV 파일 시스템)는 파일 시스템에서 열린 핸들로 애플리케이션에 영향을 주지 않으면서 CHKDSK를 사용할 수 있습니다.
- **클러스터 된 공유 볼륨 캐시**. Windows Server 2012의 Csv는 VDI (가상 데스크톱 인프라)와 같은 특정 시나리오에서 성능을 크게 향상 시킬 수 있는 읽기 캐시 지원을 소개 합니다.
- **관리가 간편해 집니다**. 스케일 아웃 파일 서버를 사용 하 여 스케일 아웃 파일 서버를 만든 다음 필요한 Csv 및 파일 공유를 추가 합니다. 더 이상 클러스터 디스크가 따로 있는 클러스터된 파일 서버를 여러 개 만든 뒤 배치 정책을 세워서 각 클러스터 노드의 작업을 확인할 필요가 없습니다.
- **스케일 아웃 파일 서버 클라이언트의 자동 균형 재조정**. Windows Server 2012 r 2에서 자동 리 밸런스는 스케일 아웃 파일 서버의 확장성 및 관리 효율성을 향상 시킵니다. SMB 클라이언트 연결은 서버 단위가 아니라 파일 공유 단위로 추적되며, 클라이언트는 파일 공유에서 사용하는 볼륨에 대한 최상의 액세스를 제공하는 클러스터 노드로 리디렉션됩니다. 따라서 파일 서버 노드 간의 리디렉션 트래픽이 감소하므로 효율성이 향상됩니다. 클라이언트는 초기 연결 후 클러스터 스토리지가 다시 구성된 경우에 리디렉션됩니다.

## <a name="in-this-scenario"></a>이 시나리오의 내용

다음 항목은 스케일 아웃 파일 서버를 배포하는 데 도움이 됩니다.

- [스케일 아웃 파일 서버 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134258(v%3dws.11)>)

  - [1 단계: 스케일 아웃 파일 서버의 저장소 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134181%28v%3dws.11%29>)
  - [2 단계: 스케일 아웃 파일 서버에서 네트워킹 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134253%28v%3dws.11%29>)

- [스케일 아웃 파일 서버 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831359%28v%3dws.11%29>)

  - [1 단계: 스케일 아웃 파일 서버에 대 한 필수 구성 요소 설치](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831478%28v%3dws.11%29>)
  - [2 단계: 스케일 아웃 파일 서버 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831718%28v%3dws.11%29>)
  - [3 단계: 스케일 아웃 파일 서버을 사용 하도록 Hyper-v 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831463%28v%3dws.11%29>)
  - [4 단계: 스케일 아웃 파일 서버를 사용 하도록 Microsoft SQL Server 구성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831815%28v%3dws.11%29>)

## <a name="when-to-use-scale-out-file-server"></a>스케일 아웃 파일 서버를 사용하는 경우

사용자의 작업 부하로 수많은 메타데이터 작업이 생성된다면 스케일 아웃 파일 서버를 사용해서는 안 됩니다. 이러한 메타데이터 작업에는 파일 여닫기, 새로운 파일 만들기, 기존 파일 이름 변경하기 등이 있습니다. 일반적인 정보 산업 근로자는 수많은 메타데이터 작업을 생성합니다. 스케일 아웃 파일 서버는 스케일 아웃 파일 서버가 제공하는 확장성과 간결성을 원하며 스케일 아웃 파일 서버로 지원되는 기술만 필요한 경우에 사용할 수 있습니다.

다음 표에서는 SMB 3.0, 일반적인 Windows 파일 시스템, 파일 서버 데이터 관리 기술 및 일반적인 작업의 기능을 보여 줍니다. 기술이 스케일 아웃 파일 서버로 지원되는지 여부 또는 기존의 클러스터된 파일 서버(일반 용도로 파일 서버라고도 함)가 필요한지 여부를 확인할 수 있습니다.

<table>
<thead>
<tr class="header">
<th>기술 영역</th>
<th>기능</th>
<th>일반 용도 파일 서버 클러스터</th>
<th>스케일 아웃 파일 서버</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SMB</td>
<td>SMB 지속적인 가용성</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB 다중 채널</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>SMB 다이렉트</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB 암호화</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>SMB 투명 장애 조치(Failover)</td>
<td>예(지속적인 가용성을 사용할 수 있는 경우)</td>
<td>예</td>
</tr>
<tr class="even">
<td>파일 시스템</td>
<td>NTFS</td>
<td>예</td>
<td>NA</td>
</tr>
<tr class="odd">
<td>파일 시스템</td>
<td><a href="https://docs.microsoft.com/windows-server/storage/refs/refs-overview">ReFS</a>(복원 파일 시스템)</td>
<td>스토리지 공간 다이렉트 권장</td>
<td>스토리지 공간 다이렉트 권장</td>
</tr>
<tr class="even">
<td>파일 시스템</td>
<td>CSV(클러스터 공유 볼륨) 파일 시스템</td>
<td>NA</td>
<td>예</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>BranchCache</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>데이터 중복 제거(Windows Server 2012)</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>데이터 중복 제거(Windows Server 2012 R2)</td>
<td>예</td>
<td>예(VDI만 해당)</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>DFSN(DFS 네임스페이스) 루트 서버 루트</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>DFSN(DFS 네임스페이스) 폴더 대상 서버</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>DFSR(DFS 복제)</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>파일 서버 리소스 관리자(화면 및 할당량)</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>파일 분류 인프라</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>동적 Access Control(클레임 기반 액세스, CAP)</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>폴더 리디렉션</td>
<td>예</td>
<td>권장 하지 않음<em></td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>오프라인 파일(클라이언트 쪽 캐싱)</td>
<td>예</td>
<td>권장되지 않음</em></td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>로밍 사용자 프로필</td>
<td>예</td>
<td>권장 하지 않음<em></td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>홈 디렉터리</td>
<td>예</td>
<td>권장되지 않음</em></td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>클라우드 폴더</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>NFS</td>
<td>NFS 서버</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="even">
<td>응용 프로그램</td>
<td>Hyper-V</td>
<td>권장되지 않음</td>
<td>예</td>
</tr>
<tr class="odd">
<td>응용 프로그램</td>
<td>Microsoft SQL Server</td>
<td>권장되지 않음</td>
<td>예</td>
</tr>
</tbody>
</table>

지속적으로 사용 가능한 파일 공유를 사용 하는 경우 폴더 리디렉션, 오프라인 파일, 로밍 사용자 프로필 또는 홈 디렉터리가 버퍼링 없이 디스크에 즉시 써야 하는 많은 쓰기를 생성 하므로 일반 용도의 파일 공유에 비해 성능이 저하 될 수 있습니다. \* 또한 지속적으로 사용 가능한 파일 공유는 파일 서버 리소스 관리자 및 Windows XP를 실행하는 PC와 호환되지 않습니다. 또한 오프라인 파일 공유에 대 한 액세스 권한을 상실 한 후 3-6 분 동안 오프 라인 모드로 전환 되지 않을 수 있습니다. 그러면 오프라인 파일의 항상 오프 라인 모드를 아직 사용 하지 않는 사용자가 불편 수 있습니다.

## <a name="practical-applications"></a>유용한 팁

스케일 아웃 파일 서버는 서버 응용 프로그램 스토리지에 적합합니다. 스케일 아웃 파일 공유에 해당 데이터를 저장할 수 있는 서버 애플리케이션의 몇 가지 예는 다음과 같습니다.

- IIS(인터넷 정보 서비스) 웹 서버는 스케일 아웃 파일 공유에 웹 사이트에 대한 구성 및 데이터를 저장할 수 있습니다. 자세한 내용은 [공유 구성](https://www.iis.net/learn/manage/managing-your-configuration-settings/shared-configuration_264)을 참조하세요.
- Hyper-V는 스케일 아웃 파일 공유에 구성 및 라이브 가상 디스크를 저장할 수 있습니다. 자세한 내용은 [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)를 참조하십시오.
- SQL Server는 스케일 아웃 파일 공유에 라이브 데이터베이스 파일을 저장할 수 있습니다. 자세한 내용은 [SMB 파일 공유와 함께 저장소로 SQL Server 설치 옵션](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option)을 참조하세요.
- VMM(Virtual Machine Manager)은 스케일 아웃 파일 공유에 가상 컴퓨터 템플릿 및 관련 파일을 포함하는 라이브러리 공유를 저장할 수 있습니다. 그러나 라이브러리 서버 자체는 스케일 아웃 파일 서버 일 수 없습니다. 즉, 스케일 아웃 파일 서버 클러스터 역할을 사용 하지 않는 독립 실행형 서버 또는 장애 조치 (failover) 클러스터에 있어야 합니다.

스케일 아웃 파일 공유를 라이브러리 공유로 사용하는 경우 스케일 아웃 파일 서버와 호환되는 기술만 사용할 수 있습니다. 예를 들어 DFS 복제를 사용 하 여 스케일 아웃 파일 공유에 호스트 된 라이브러리 공유를 복제할 수 없습니다. 또한 스케일 아웃 파일 서버에 최신 소프트웨어 업데이트가 설치되어 있어야 합니다.

스케일 아웃 파일 공유를 라이브러리 공유로 사용하려면 먼저 로컬 공유를 포함하거나 공유가 없는 라이브러리 서버(대체로 가상 컴퓨터)를 추가합니다. 그런 다음 라이브러리 공유를 추가할 때 스케일 아웃 파일 서버에서 호스트 되는 파일 공유를 선택 합니다. 이 공유는 VMM에서 관리되고 라이브러리 서버 전용으로 생성되어야 합니다. 또한 스케일 아웃 파일 서버에 최신 업데이트를 설치해야 합니다. VMM 라이브러리 서버 및 라이브러리 공유를 추가 하는 방법에 대 한 자세한 내용은 [vmm 라이브러리에 프로필 추가](https://docs.microsoft.com/system-center/vmm/library-profiles?view=sc-vmm-1801)를 참조 하세요. 파일 및 저장소 서비스에 대해 현재 사용할 수 있는 핫픽스 목록은 [Microsoft 기술 자료 문서 2899011](https://support.microsoft.com/help/2899011/list-of-currently-available-hotfixes-for-the-file-services-technologie)을 참조하세요.

>[!NOTE]
>정보 근로자와 같은 일부 사용자의 작업은 성능에 더 큰 영향을 줍니다. 예를 들어 파일 열기 및 닫기, 새 파일 만들기, 기존 파일의 이름 바꾸기와 같은 작업은 여러 사용자가 수행할 경우 성능에 영향을 줍니다. 지속적인 가용성을 사용할 수 있는 파일 공유는 데이터 무결성을 제공하지만 전반적인 성능에 영향을 줍니다. 지속적인 가용성을 위해 디스크에 데이터 동시 쓰기를 수행하여 스케일 아웃 파일 서버에서 클러스터 노드 오류가 발생할 경우 무결성을 보장해야 합니다. 따라서 사용자가 지속적으로 사용 가능한 파일 공유에서 여러 개의 큰 파일을 파일 서버에 복사할 경우 성능이 훨씬 저하될 수 있습니다.

## <a name="features-included-in-this-scenario"></a>이 시나리오에 포함된 기능

다음 표에는 이 시나리오에 포함된 기능이 나열되어 있으며, 이 기능이 시나리오를 지원하는 방법에 대한 설명이 나와 있습니다.

<table>
<thead>
<tr class="header">
<th>기능</th>
<th>이 시나리오를 지원하는 방법</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="failover-clustering.md">장애 조치 클러스터링</a></td>
<td>장애 조치 (Failover) 클러스터는 스케일 아웃 파일 서버를 지원 하기 위해 Windows Server 2012에 분산 네트워크 이름, 스케일 아웃 파일 서버 리소스 종류, CSV (클러스터 공유 볼륨) 2 및 스케일 아웃 파일 서버 고가용성 역할의 기능을 추가 했습니다. 이러한 기능에 대 한 자세한 내용은 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)">Windows Server&#39;2012 장애 조치 (Failover) 클러스터링의 새로운 기능 [리디렉션]</a>을 참조 하세요.</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v%3dws.11)">서버 메시지 블록</a></td>
<td>Smb 3.0 2012에는 스케일 아웃 파일 서버를 지원 하기 위해 SMB 투명 장애 조치 (Failover), SMB 다중 채널 및 SMB 다이렉트와 같은 기능이 추가 되었습니다.<br />
<br />
Windows Server 2012 r 2에서 제공 되는 SMB의 새로운 기능 및 변경 된 기능에 대 한 자세한 내용은 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)">Windows server에서 제공 되는 smb의 새로운&#39;</a>기능을 참조 하세요.</td>
</tr>
</tbody>
</table>

## <a name="more-information"></a>자세한 정보

- [소프트웨어 정의 저장소 디자인 고려 사항 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt243829(v%3dws.11)>)
- [서버, 저장소 및 네트워크 가용성 향상](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
- [서버 애플리케이션을 위한 신속하고 효율적인 파일 서버 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
- [규모를 확장하느냐 마느냐 그것이 문제다](https://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx) (블로그 게시물)
- [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848267(v%3dws.11)>)