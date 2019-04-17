---
title: 확장 파일 서버에 대 한 응용 프로그램 데이터 개요
description: Windows Server 201 R2, Windows Server 2012 및 Windows Server 2016 확장 파일 서버 기능의 개요를 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 04e25e9c69062611d9d14c220614f148ac5de770
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082478"
---
# <a name="scale-out-file-server-for-application-data-overview"></a>확장 파일 서버에 대 한 응용 프로그램 데이터 개요

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

확장 파일 서버는 파일 기반 서버 응용 프로그램 저장소에 대 한 지속적으로 사용할 수 있는 확장 파일 공유를 제공 하는데 사용 되는 기능입니다. 확장 파일 공유 같은 클러스터의 여러 노드에서 동일한 폴더를 공유 하는 기능을 제공 합니다. 이 시나리오에 대 한 계획 및 확장 파일 서버를 배포 하는 방법에 중점을 둡니다.

배포 및 다음 방법 중 하나를 사용 하 여 클러스터 된 파일 서버를 구성할 수 있습니다.

- **응용 프로그램 데이터에 대 한 확장 파일 서버** Windows Server 2012에서 도입 된이 클러스터 된 파일 서버 기능 및 파일 공유, Hyper-v 가상 컴퓨터 파일과 같은 서버 응용 프로그램 데이터를 저장 하 고 비슷한 수준의 안정성, 가용성, 관리 효율성 및 높은 얻을 수 있습니다. 저장 영역 네트워크에서 기대할 수 있는 성능을 제공 합니다. 모든 파일 공유는 동시에 모든 노드에서 온라인 합니다. 이러한 종류의 클러스터 된 파일 서버와 연결 된 파일 공유는 확장 파일 공유 라고 합니다. 이 액티브 / 액티브 라고도 합니다. SMB를 통해 서버 메시지 블록 (SMB) 또는 Microsoft SQL Server를 통해 어느 Hyper-v를 배포할 때 권장 되는 파일 서버 형식입니다.
- **일반적으로 사용에 대 한 파일 서버** 장애 조치 클러스터링 도입 이후 Windows 서버에서 지원 되는 클러스터 된 파일 서버의 연속입니다. 클러스터 된 파일 서버 및 따라서 모든 공유 클러스터 된 파일 서버에 연결 된이 유형의 한번에 한 노드에서 온라인 합니다. 이것은 라고도 액티브 / 패시브 또는 이중 활성 합니다. 이러한 종류의 클러스터 된 파일 서버와 연결 된 파일 공유 클러스터 된 파일 공유 라고 합니다. 정보 근로자 시나리오를 배포할 때 권장 되는 파일 서버 형식입니다.

## <a name="scenario-description"></a>시나리오 설명

확장 파일 공유와 클러스터의 여러 노드에서 동일한 폴더를 공유할 수 있습니다. 예: 서버 메시지 블록 (SMB) 확장을 사용 하는 4 노드 파일 서버 클러스터를가 Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 컴퓨터 파일 공유 노드를 4 개 중 하나에서 액세스할 수 있습니다. 이 작업을 수행 하 여 Windows Server 장애 조치 클러스터링의 새로운 기능 및 Windows 파일 서버 프로토콜의 기능을 활용 하 여 SMB 3.0 합니다. 파일 서버 관리자가 확장 파일 공유 및 서버 응용 프로그램을 지속적으로 사용할 수 있는 파일 서비스를 제공할 수 있으며 단순히 더 많은 서버를 온라인 상태로 전환 하 여 신속 하 게 증가 요청에 응답할 수 있습니다. 프로덕션 환경에서 수행할 수는 이러한 모든 아니며 서버 응용 프로그램을 완전히 투명 하 게 합니다.

확장 파일 서버에 의해 제공 되는 주요 이점은 다음과 같습니다.

- **액티브 / 액티브 파일 공유**합니다. 모든 클러스터 노드가 수락한 SMB 클라이언트 요청을 처리할 수 있습니다. 동시에 모든 클러스터 노드를 통해 액세스할 수 있는 콘텐츠를 공유 하 여 파일을 만들어서 SMB 3.0 클러스터 및 클라이언트 위해 협력 하는 서비스와 함께 계획 된 유지 관리 및 계획 되지 않은 실패 하는 동안 다른 클러스터 노드로 투명 하 게 장애 조치를 제공 하려면 중단 합니다.
- **향상 된 대역폭**입니다. 최대 공유 대역폭은 모든 파일 서버 클러스터 노드의 총 대역폭입니다. 이전 버전의 Windows Server에서는 달리 총 대역폭을 단일 클러스터 노드의 대역폭을 제한 더 이상 하지만 백업 저장소 시스템의 기능 제약 조건을 정의 하는 대신, 합니다. 노드를 추가 하 여 총 대역폭을 늘릴 수 있습니다.
- **0 가동 중지 시간으로 CHKDSK**합니다. Windows Server 2012에서 CHKDSK 크게 파일 시스템은 복구에 대 한 오프 라인 시간을 단축 하 크게 향상 됩니다. 오프 라인 단계를 제거 하 여 추가로이 한 단계를 수행 하는 클러스터 된 공유 볼륨 (Csv). CSV 파일 시스템 (CSVFS)는 파일 시스템에서 열린 핸들을 사용한 응용 프로그램에 영향을 주지 없이 CHKDSK를 사용할 수 있습니다.
- **클러스터 공유 볼륨 캐시**합니다. Windows Server 2012의 Csv 크게 향상 시킬 수 있는 특정 시나리오에서 성능을 등의 가상 데스크톱 VDI (인프라)는 읽기 캐시에 대 한 지원을 소개 합니다.
- **관리를 단순화할**합니다. 확장 파일 서버와 확장 파일 서버를 만들고 필요한 Csv 및 파일 공유를 추가 합니다. 각각 별도 클러스터 디스크 여러 클러스터 된 파일 서버를 만들고 다음 각 클러스터 노드에 대 한 작업을 확인 하는 배치 정책을 개발할 필요는 나타나지 않습니다.
- **자동 확장 파일 서버는 클라이언트의 재 분산**합니다. 확장성 및 관리 효율성 확장 파일 서버에 대 한 Windows Server 2012 r 2의 향상 자동 재 분산 합니다. 파일 공유 당 추적 SMB 클라이언트 연결 (대신 서버당), 파일 공유에서 사용 하는 볼륨에 대 한 최상의 액세스와 클러스터 노드 클라이언트는 다음 리디렉션할 하 고 있습니다. 이 파일 서버 노드 간에 리디렉션 트래픽 감소 하 여 효율성을 향상 시킵니다. 클라이언트는 초기 연결 하 고 클러스터 저장소를 다시 구성 하는 경우에 따라 리디렉션됩니다.

## <a name="in-this-scenario"></a>이 시나리오에서

다음 항목은 확장 파일 서버를 배포 하기 위해 사용할 수 있습니다.

- [확장 파일 서버에 대 한 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134258(v%3dws.11)>)

  - [1 단계: 확장 파일 서버에는 저장소에 대 한 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134181%28v%3dws.11%29>)
  - [2 단계: 확장 파일 서버에 네트워크에 대 한 계획](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134253%28v%3dws.11%29>)

- [확장 파일 서버를 배포 합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831359%28v%3dws.11%29>)

  - [1 단계: 확장 파일 서버에 대 한 필수 구성 요소를 설치 합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831478%28v%3dws.11%29>)
  - [2 단계: 확장 파일 서버를 구성 합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831718%28v%3dws.11%29>)
  - [단계 3: 확장 파일 서버를 사용 하도록 Hyper-v를 구성 합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831463%28v%3dws.11%29>)
  - [4 단계: 확장 파일 서버를 사용 하 여 Microsoft SQL Server를 구성 합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831815%28v%3dws.11%29>)

## <a name="when-to-use-scale-out-file-server"></a>확장 파일 서버를 사용 하는 경우

하지 사용 해야 확장 파일 서버 작업 부하에 많은 파일 열기, 등의 메타 데이터 작업을 생성 하는 경우 파일을 닫고, 새 파일 만들기 또는 기존 파일 이름바꾸기. 일반적인 정보 근로자의 메타 데이터 작업을 많이 발생 합니다. 관심 있는 확장성 및 제공 하는 간단 하 고만 확장 파일 서버와 지원 되는 기술을 필요로 하는 경우에 확장 파일 서버를 사용 해야 합니다.

다음 표에서 SMB 3.0, 일반적인 Windows 파일 시스템, 파일 서버 데이터 관리 기술 및 일반적인 작업의 기능을 보여줍니다. 전통적인 클러스터 된 파일 서버 (로 알려져 일반적으로 사용에 대 한 파일 서버)를 요구 하는 경우 또는 기술이 확장 파일 서버와 사용할 수 있는지 여부를 확인할 수 있습니다.

<table>
<thead>
<tr class="header">
<th>기술 영역</th>
<th>특징</th>
<th>일반 사용 하 여 파일 서버 클러스터</th>
<th>파일 서버를 수평 확장</th>
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
<td>SMB 투명 장애 조치</td>
<td>예 (지속적인 가용성 활성화 된 경우)</td>
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
<td>복원 파일 시스템 (<a href="https://docs.microsoft.com/windows-server/storage/refs/refs-overview">ReFS</a>)</td>
<td>저장소와 권장 직접 간격 줄로 설정</td>
<td>저장소와 권장 직접 간격 줄로 설정</td>
</tr>
<tr class="even">
<td>파일 시스템</td>
<td>클러스터 공유 볼륨 파일 시스템 (CSV)</td>
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
<td>데이터 중복 제거 (Windows Server 2012)</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>데이터 중복 제거 (Windows Server 2012 R2)</td>
<td>예</td>
<td>예 (VDI에만 해당)</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>DFS Namespace (DFSN) 루트 서버 루트</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>DFS Namespace (DFSN) 폴더 대상 서버</td>
<td>예</td>
<td>예</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>DFS 복제 (DFSR)</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>파일 서버 리소스 관리자 (화면 및 할당량)</td>
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
<td>동적 액세스 제어 (클레임 기반 액세스를 단락의 첫 문자)</td>
<td>예</td>
<td>아니요</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>폴더 리디렉션</td>
<td>예</td>
<td>권장 되지 않음 *</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>오프 라인 파일 (클라이언트 쪽 캐싱)</td>
<td>예</td>
<td>권장 되지 않음 *</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>로밍 사용자 프로필</td>
<td>예</td>
<td>권장 되지 않음 *</td>
</tr>
<tr class="odd">
<td>파일 관리</td>
<td>홈 디렉터리</td>
<td>예</td>
<td>권장 되지 않음 *</td>
</tr>
<tr class="even">
<td>파일 관리</td>
<td>작업 폴더</td>
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
<td>권장 하지 않음</td>
<td>예</td>
</tr>
<tr class="odd">
<td>응용 프로그램</td>
<td>Microsoft SQL Server</td>
<td>권장 하지 않음</td>
<td>예</td>
</tr>
</tbody>
</table>

\ \ * 폴더 리디렉션, 오프 라인 파일, 로밍 사용자 프로필 또는 홈 디렉터리 생성 (하지 않고 버퍼링) 디스크에 즉시 써야 하는 쓰기 작업 수가 많음 지속적으로 사용할 수 있는 파일 공유를 사용 하는 경우에 비해으로 성능 감소 일반 목적의 파일 공유 합니다. 지속적으로 사용할 수 있는 파일 공유도 파일 서버 리소스 관리자 및 Windows XP를 실행 하는 Pc와 호환 되지 않습니다. 또한 오프 라인 파일 수 하지 사용자가 오프 라인 파일의 항상 오프 라인 모드를 사용 하 여 아직 없는 사용자를 실망 수 있는 프로그램 공유에 대 한 액세스를 잃어버린 후 3-6 분에 대 한 오프 라인 모드로 전환 됩니다.

## <a name="practical-applications"></a>유용한 팁

확장 파일 서버는 서버 응용 프로그램 저장소에 대 한 이상적입니다. 확장 파일 공유에 해당 데이터를 저장할 수 있는 서버 응용 프로그램의 몇가지 예는 다음과 같습니다.

- 인터넷 정보 서비스 (IIS) 웹 서버 및 저장할 수 구성 데이터의 웹사이트에 대 한 확장 파일 공유에. 자세한 내용은 [공유 구성](http://www.iis.net/learn/manage/managing-your-configuration-settings/shared-configuration_264)을 참조 하십시오.
- Hyper-v는 구성 및 라이브 가상 디스크 확장 파일 공유에 저장할 수 있습니다. 자세한 내용은 [배포 Hyper-v SMB 통해](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)을 참조 하십시오.
- SQL Server 확장 파일 공유에 라이브 데이터베이스 파일을 저장할 수 있습니다. 자세한 내용은 [저장소 옵션으로 공유를 SMB 파일이 포함 된 SQL Server 설치](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option)를 참조 합니다.
- Virtual Machine Manager (VMM) 수평 파일 공유에 라이브러리 공유 (포함 하는 가상 컴퓨터 서식 파일 및 관련된 파일)을 저장할 수 있습니다. 그러나 라이브러리 서버 자체에서 확장 파일 서버 수 없으며-독립 실행형 서버 또는 수평 파일 서버 클러스터 역할을 사용 하지 않는 장애 조치 클러스터에 있어야 합니다.

라이브러리 공유로 확장 파일 공유를 사용 하는 경우 확장 파일 서버와 호환 되는 기술에만 사용할 수 있습니다. 예, 확장 파일 공유에서 호스트 되는 라이브러리 공유를 복제 하려는 DFS 복제를 사용할 수 없습니다. 확장 파일 서버에 최신 소프트웨어 업데이트 설치는는 중요 한 이기도 합니다.

라이브러리 공유로 확장 파일 공유를 사용 하려면 먼저 라이브러리 서버 추가 (가능성이 가상 컴퓨터)는 로컬 공유 또는 없음 공유 전혀. 그런 다음 라이브러리 공유를 추가 하면 확장 파일 서버에서 호스트 되는 파일 공유를 선택 합니다. VMM 관리 하 고 라이브러리 서버에서 사용 하기 위해 단독으로 만든이 공유 해야 합니다. 또한 확장 파일 서버에 최신 업데이트를 설치 해야 합니다. VMM 라이브러리 서버 및 라이브러리 공유를 추가 하는 방법에 대 한 자세한 내용은 [VMM 라이브러리에 대 한 추가 프로필](https://docs.microsoft.com/system-center/vmm/library-profiles?view=sc-vmm-1801)을 참조 하십시오. 파일 및 저장소 서비스에 대 한 현재 사용할 수 있는 핫픽스 목록이 [Microsoft 기술 자료 문서 2899011을](https://support.microsoft.com/help/2899011/list-of-currently-available-hotfixes-for-the-file-services-technologie)참조 하십시오.

>[!NOTE]
>정보 근로자와 같은 일부 사용자가 성능에 큰 영향을 주는 작업입니다. 예는 괄호 및 닫는 파일을 새 파일 만들기 (영문) 같은 작업과 성능에 영향을 미칠 여러 사용자가 수행 하는 경우 기존 파일 이름바꾸기 합니다. 지속적인 가용성와 파일 공유를 사용 하는 경우 데이터 무결성을 제공 하지만 전체 성능에 영향을 수도 있습니다. 지속적인 가용성 확장 파일 서버에서 클러스터 노드 장애 발생 시 무결성을 보장 하는 디스크에 데이터를 통해 작성 해야 합니다. 따라서 파일 서버에 여러 큰 파일을 복사 하는 사용자는 계속 해 서 사용할 수 있는 파일 공유에 성능이 크게 저하를 이용할 수 있습니다.

## <a name="features-included-in-this-scenario"></a>이 시나리오에 포함 된 기능

다음 표에서이 시나리오에 포함 된 기능을 소개 하 고 지 원하는 방식에 대해 설명 합니다.

<table>
<thead>
<tr class="header">
<th>특징</th>
<th>이 시나리오를 지 원하는 방법을</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="failover-clustering.md">장애 조치(failover) 클러스터링</a></td>
<td>확장 파일 서버를 지원 하도록 Windows Server 2012의 다음 기능을 추가 하는 장애 조치 클러스터: 배포 된 네트워크 이름, 확장 파일 서버 리소스 유형, 클러스터 공유 볼륨 (CSV), 2 및 확장 파일 서버에 대 한 고가용성 정보 역할입니다. 이러한 기능에 대 한 자세한 내용은 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)">Windows Server 2012 [리디렉션]의 장애 조치 클러스터링의 새로운 기능</a>을 참조 하십시오.</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v%3dws.11)">서버 메시지 블록</a></td>
<td>SMB 3.0에는 다음과 같은 기능을 지원 하도록 Windows Server 2012에 확장 파일 서버 추가: SMB 투명 장애 조치, SMB 다중 채널 및 SMB 직접 합니다.<br />
<br />
Windows Server 2012 r 2에는 SMB에 새로 추가 되거나 변경 된 기능에 대해 자세한 내용은 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)">Windows Server의 경우 SMB의 새로운 기능</a>을 참조 하십시오.</td>
</tr>
</tbody>
</table>

## <a name="more-information"></a>자세한 정보

- [소프트웨어 정의 저장소 디자인 고려 사항 가이드](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt243829(v%3dws.11)>)
- [증가 함에 따라 서버, 저장소 및 네트워크 가용성](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
- [서버 응용 프로그램에 대 한 빠르고 효율적인 파일 서버를 배포합니다.](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
- [질문은를 수평 확장 또는 수평 확장이 적용 되지 않음](https://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx) (블로그 게시물)
- [폴더 리디렉션, 오프라인 파일 및 로밍 사용자 프로필](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848267(v%3dws.11)>)