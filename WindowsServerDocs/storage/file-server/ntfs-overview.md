---
title: NTFS 개요
description: NTFS의 새로운를 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2e45fd1eb13044fdf0ba0f66a6e909a3f2d39bc3
ms.sourcegitcommit: 6fec3ca19ddaecbc936320d98cca0736dd8505d1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2019
ms.locfileid: "67196163"
---
# <a name="ntfs-overview"></a>NTFS 개요

>적용 대상: Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

NTFS-Windows 및 Windows Server의 최신 버전에 대 한 기본 파일 시스템, 보안 설명자, 암호화, 디스크 할당량 및 다양 한 메타 데이터를 포함 하는 기능의 전체 집합을 제공 하 고 사용할 수 있는 클러스터 공유 볼륨 (CSV) 지속적으로 제공 장애 조치 클러스터의 여러 노드에서 동시에 액세스할 수 있는 사용 가능한 볼륨입니다.

Windows Server 2012 R2에는 NTFS의 새로운 기능과 변경 된 기능에 대 한 자세한 내용은 참조 하세요 [NTFS의 새로운](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))합니다. 추가 기능 정보에 대 한 참조를 [추가 정보](#additional-information) 이 항목의 섹션입니다. 최신 ReFS (복원 파일 시스템)에 대 한 자세한 내용은 참조 하세요 [ReFS (복원 파일 시스템) 개요](../refs/refs-overview.md)합니다.

## <a name="practical-applications"></a>유용한 팁

### <a name="increased-reliability"></a>향상된 안정성

NTFS는 시스템 오류가 발생 한 후 컴퓨터를 다시 시작할 때 파일 시스템 일관성을 복원 하려면 로그 파일 및 검사점 정보를 사용 합니다. 불량 섹터 오류가 발생 한 후 동적으로 NTFS 불량 섹터를 포함, 새 클러스터를 데이터에 대 한 할당, 불량, 원래 클러스터를 표시 및 더 이상 이전 클러스터를 사용 하 여 클러스터를 다시 매핑합니다. 예를 들어, 서버 충돌 후 NTFS 데이터를 복구할 수 해당 로그 파일을 재생 하 여 합니다.

NTFS에서 지속적으로 모니터링 하 고 볼륨을 오프 라인으로 전환 하지 않고 백그라운드에서 일시적인 손상 문제를 수정 합니다. (이 기능은 이라고 [자동 NTFS 복구](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))Windows Server 2008에 도입 된). 더 큰 손상 문제에 대 한 Windows Server 2012 이상 버전에서는 Chkdsk 유틸리티를 검색 하 고 볼륨이 온라인 볼륨의 데이터 일관성을 복원 하는 데 필요한 시간에 오프 라인 시간을 제한 하는 동안 드라이브를 분석 합니다. NTFS 클러스터 공유 볼륨을 사용 하는 경우 가동 중지 시간 없이 필요 합니다. 자세한 내용은 [NTFS 상태 및 Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))(영문)를 참조하세요.

### <a name="increased-security"></a>향상 된 보안

- **액세스 제어 목록 ACL 기반 보안 파일 및 폴더에 대 한**-NTFS 파일 또는 폴더에 사용 권한을 설정할 수 있습니다 그룹 및 사용자 액세스를 제한 하거나 허용을 지정 하 고 액세스 유형을 선택 합니다.

- **BitLocker 드라이브 암호화에 대 한 지원을**-BitLocker 드라이브 암호화는 중요 한 시스템 정보 및 NTFS 볼륨에 저장 된 다른 데이터에 대 한 추가 보안을 제공 합니다. Windows Server 2012 R2 및 Windows 8.1 BitLocker 지원을 제공 x86 및 x64 기반 컴퓨터에서 신뢰할 수 있는 플랫폼 모듈 (TPM) 사용 하 여 장치 암호화를 지 원하는 독립-로 (이전에, Windows RT 장치에만 제공) 연결 하는 합니다. 장치 암호화는 Windows 기반 컴퓨터에서 데이터를 보호 하 고 악의적인 사용자가 사용자의 암호를 검색할 의존 시스템 파일에 액세스 하지 못하도록 하거나 물리적으로 PC에서 제거 하 고 설치 하 여 드라이브에 액세스 하지 못하도록 차단할 수 있습니다는 다른 하나입니다. 자세한 내용은 [BitLocker의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))합니다.

- **대규모 볼륨 지원**-NTFS 256 테라바이트 만큼 큰 볼륨을 지원할 수 있습니다. 크기는 클러스터 크기 및 클러스터 수가 영향을 받는 볼륨을 지원 합니다. 와 (2<sup>32</sup> – 1) 클러스터 (NTFS 지 클러스터의 최대 수), 볼륨 및 파일 크기가 지원 됩니다.

  |클러스터 크기|가장 큰 볼륨|가장 큰 파일|
  |---|---|---|
  |4KB (기본 크기)|16TB|16TB|
  |8KB|32TB|32TB|
  |16KB|64TB|64TB|
  |32KB|128 TB|128 TB|
  |64KB (최대 크기)|256TB|256TB|

>[!IMPORTANT]
>서비스 및 앱에는 파일 및 볼륨 크기에 추가 제한을 적용할 수 있습니다. 예를 들어, 이전 버전 기능 또는 백업 하는 앱을 사용 하는 경우 64TB의 볼륨 섀도 복사본 서비스 (VSS) 스냅숏이 사용 하 여 볼륨 크기 제한 됩니다 (및 SAN 또는 RAID 엔클로저를 사용 하지 않는). 그러나 워크 로드 및 저장소의 성능에 따라 더 작은 볼륨 크기를 사용 해야 합니다.

### <a name="formatting-requirements-for-large-files"></a>큰 파일에 대 한 형식 지정 요구 사항

큰.vhdx 파일의 적절 한 확장을 허용 하려면 볼륨 포맷에 대 한 새로운 권장 사항이 있습니다. 데이터 중복 제거를 사용 하 여 사용할 또는 1TB 보다 큰.vhdx 파일 등의 매우 큰 파일을 호스트 하는 볼륨을 포맷할 때 사용 합니다 **Format-volume** 다음 매개 변수를 사용 하 여 Windows PowerShell cmdlet.

|매개 변수|설명|
|---|---|
|-AllocationUnitSize 64KB|64KB NTFS 할당 단위 크기를 설정합니다.|
|-UseLargeFRS|큰 파일 레코드 세그먼트 FRS ()을 지원 합니다. 이 볼륨에서 파일 당 허용 되는 익스텐트의 수를 늘릴 필요 합니다. 큰 FRS 레코드에 대 한 한도 약 6 백만 익스텐트를 약 1.5 백만 익스텐트에서 증가합니다.|

예를 들어, 다음 cmdlet D 드라이브는 NTFS 볼륨으로 사용 되는 FRS 및 64kb 할당 단위 크기를 사용 하 여 합니다.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

사용할 수도 있습니다는 **형식** 명령입니다. 시스템 명령 프롬프트에서 다음 명령을 입력 위치 **/L** 큰 FRS 볼륨을 포맷 하 고 **/A:64 k** 64KB 할당 단위 크기를 설정 합니다:

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>최대 파일 이름 및 경로

NTFS는 긴 파일 이름 및 최대 값을 갖는 확장 길이의 경로 지원합니다.

- **이전 버전과 호환성을 사용 하 여 긴 파일 이름에 대 한 지원**-NTFS 긴 파일 이름을 파일 이름 및 확장명에는 8.3 제한을 적용 하는 파일 시스템과 호환성을 제공 별칭 (유니코드)의 디스크에는 8.3을 저장할 수 있습니다. (성능상의 이유로) 필요한 경우에 Windows Server 2008 R2, Windows 8 및 Windows 운영 체제의 최신 버전의 개별 NTFS 볼륨에서 8.3 별칭을 선택적으로 해제할 수 있습니다.
  Windows Server 2008 R2 및 이상 시스템에서 운영 체제를 사용 하 여 볼륨은 포맷 하는 경우 짧은 이름은 기본적으로 비활성화 됩니다. 응용 프로그램 호환성에 대 한 짧은 이름은 계속 사용할 수 있습니다 시스템 볼륨.

- **확장 길이의 경로 대 한 지원을**-여러 Windows API 함수에는 약 32,767 문자의 길이 확장 경로 허용 하는 유니코드 버전-최대 정의한 경로가 260 자 제한을 초과\_경로 설정 합니다. 자세한 파일 이름 및 경로 형식 요구 사항 및 확장 길이의 경로 구현 하기 위한 지침을 참조 하세요 [파일 이름 지정, 경로 및 네임 스페이스](https://msdn.microsoft.com/library/windows/desktop/aa365247)합니다.

- **저장소 클러스터**-장애 조치 클러스터를 사용 하는 경우 NTFS 클러스터 공유 볼륨 (CSV) 파일 시스템을 함께 사용 하는 경우에 동시에 여러 클러스터 노드에서 액세스할 수 있는 지속적으로 사용 가능한 볼륨을 지원 합니다. 자세한 내용은 [장애 조치 클러스터에서 사용 하 여 클러스터 공유 볼륨](../../failover-clustering/failover-cluster-csvs.md)합니다.

### <a name="flexible-allocation-of-capacity"></a>유연한 용량 할당

볼륨에 공간이 제한 된 NTFS 서버의 저장소 용량을 사용 하려면 다음과 같은 방법으로 제공 합니다.

- 디스크 할당량을 사용 하 여 추적 하 고 개별 사용자에 대 한 NTFS 볼륨의 디스크 공간 사용을 제어 합니다.
- 저장할 수 있는 데이터의 양이 최대화 하기 위해 파일 시스템 압축을 사용 합니다.
- 동일한 디스크 또는 다른 디스크에서 할당 되지 않은 공간을 추가 하 여 NTFS 볼륨의 크기를 늘립니다.
- 드라이브 문자 부족 또는 기존 폴더에서 액세스할 수 있는 추가 공간을 만들어야 하는 경우 로컬 NTFS 볼륨의 빈 폴더에 볼륨을 탑재 합니다.

## <a name="additional-information"></a>추가 정보

- [NTFS 및 ReFS에 대 한 클러스터 크기 권장 사항](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [Resilient File System (ReFS) 개요](../refs/refs-overview.md)
- [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)
- [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2, Windows 7)
- [NTFS 상태 및 Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))
- [자동 NTFS 복구](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) (Windows Server 2008에 도입 됨)
- [트랜잭션 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (Windows Server 2008에 도입 됨)
- [Windows Server에서 저장소](../storage.md)