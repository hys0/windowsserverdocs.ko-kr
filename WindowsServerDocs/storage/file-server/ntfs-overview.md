---
title: NTFS 개요
description: NTFS에 대 한 설명입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: e43d0520f97f28af54f794daf7ad263bc9928fac
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867348"
---
# <a name="ntfs-overview"></a>NTFS 개요

>적용 대상: Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

NTFS-최신 버전의 Windows 및 Windows Server에 대 한 주 파일 시스템은 보안 설명자, 암호화, 디스크 할당량 및 다양 한 메타 데이터를 비롯 한 전체 기능 집합을 제공 하며, CSV (클러스터 공유 볼륨)와 함께 사용 하 여 지속적으로 제공할 수 있습니다. 장애 조치 (failover) 클러스터의 여러 노드에서 동시에 액세스할 수 있는 사용 가능한 볼륨입니다.

NTFS의 새로운 기능 및 변경 된 기능에 대 한 자세한 내용은 Windows Server 2012 r 2에서 제공 되는 [ntfs의 새로운](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))기능을 참조 하십시오. 추가 기능 정보는이 항목의 [추가 정보](#additional-information) 섹션을 참조 하세요. 최신 ReFS (복원 파일 시스템)에 대해 자세히 알아보려면 [refs (복원 파일 시스템) 개요](../refs/refs-overview.md)를 참조 하세요.

## <a name="practical-applications"></a>유용한 팁

### <a name="increased-reliability"></a>향상된 안정성

NTFS는 시스템 오류가 발생 한 후 컴퓨터를 다시 시작할 때 해당 로그 파일 및 검사점 정보를 사용 하 여 파일 시스템의 일관성을 복원 합니다. 불량 섹터 오류가 발생 한 후 NTFS는 잘못 된 섹터를 포함 하는 클러스터를 동적으로 다시 매핑 하 고, 데이터에 대 한 새 클러스터를 할당 하 고, 원래 클러스터를 불량으로 표시 하 고, 이전 클러스터를 더 이상 사용 하지 않습니다. 예를 들어 서버가 충돌 한 후 NTFS는 해당 로그 파일을 재생 하 여 데이터를 복구할 수 있습니다.

NTFS는 볼륨을 오프 라인으로 전환 하지 않고 백그라운드에서 일시적 손상 문제를 지속적으로 모니터링 하 고 해결 합니다 .이 기능은 Windows Server 2008에 도입 된 [자체 복구 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))라고 합니다. 손상 문제가 큰 경우, Windows Server 2012 이상에서 Chkdsk 유틸리티는 볼륨이 온라인 상태일 때 드라이브를 검색 하 고 분석 하 여 볼륨의 데이터 일관성을 복원 하는 데 필요한 시간으로 오프 라인 시간을 제한 합니다. NTFS를 클러스터 공유 볼륨에 사용 하는 경우 가동 중지 시간이 필요 하지 않습니다. 자세한 내용은 [NTFS 상태 및 Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))(영문)를 참조하세요.

### <a name="increased-security"></a>보안 강화

- **파일 및 폴더에 대 한 ACL (Access Control 목록) 기반 보안**-NTFS를 사용 하 여 파일이 나 폴더에 대 한 사용 권한을 설정 하 고, 액세스를 제한 하거나 허용 하려는 그룹 및 사용자를 지정 하 고, 액세스 유형을 선택할 수 있습니다.

- **BitLocker 드라이브 암호화 지원**-BitLocker 드라이브 암호화는 중요 한 시스템 정보 및 NTFS 볼륨에 저장 된 기타 데이터에 대 한 추가 보안을 제공 합니다. Windows Server 2012 R2 및 Windows 8.1부터 BitLocker는 연결 된 독립 실행형 (이전에는 Windows RT 장치 에서만 사용할 수 있음)을 지 원하는 신뢰할 수 있는 플랫폼 모듈 (TPM)를 사용 하 여 x86 및 x64 기반 컴퓨터에서 장치 암호화를 지원 합니다. 장치 암호화는 Windows 기반 컴퓨터의 데이터를 보호 하는 데 도움이 되며, 악의적인 사용자가 사용 하는 시스템 파일에 액세스 하 여 사용자의 암호를 검색 하거나, PC에서 물리적으로 제거 하 여 드라이브에 액세스할 수 없도록 차단 하는 데 도움이 됩니다. 다른 항목입니다. 자세한 내용은 [BitLocker의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))을 참조 하세요.

- **대용량 볼륨에 대 한 지원**-NTFS는 256 테라바이트의 크기의 볼륨을 지원할 수 있습니다. 지원 되는 볼륨 크기는 클러스터 크기와 클러스터 수의 영향을 받습니다. (2<sup>32</sup> – 1) 클러스터 (NTFS에서 지 원하는 최대 클러스터 수)를 사용 하는 경우 다음 볼륨 및 파일 크기가 지원 됩니다.

  |클러스터 크기|최대 볼륨|가장 큰 파일|
  |---|---|---|
  |4kb (기본 크기)|16TB|16TB|
  |8KB|32 TB|32 TB|
  |16KB|64TB|64TB|
  |32 KB|128 TB|128 TB|
  |64 KB (최대 크기)|256TB|256TB|

>[!IMPORTANT]
>서비스 및 앱은 파일 및 볼륨 크기를 추가로 제한할 수 있습니다. 예를 들어 볼륨 크기 제한은 이전 버전 기능을 사용 하는 경우 64 TB이 고, 볼륨 섀도 복사본 서비스 (VSS) 스냅숏을 사용 하는 백업 앱 인 경우 SAN 또는 RAID 인클로저를 사용 하지 않습니다. 그러나 사용자의 작업 및 저장소 성능에 따라 더 작은 볼륨 크기를 사용 해야 할 수도 있습니다.

### <a name="formatting-requirements-for-large-files"></a>대량 파일의 서식 지정 요구 사항

대용량 .vhdx 파일의 적절 한 확장을 허용 하기 위해 볼륨 포맷에 대 한 새로운 권장 사항이 있습니다. 데이터 중복 제거에 사용 되는 볼륨의 형식을 지정 하거나 1TB 보다 큰 .vhdx 파일과 같이 매우 큰 파일을 호스트 하는 경우 Windows PowerShell에서 다음 매개 변수를 사용 하 여 **Format-Volume** cmdlet을 사용 합니다.

|매개 변수|설명|
|---|---|
|-AllocationUnitSize 64KB|64 KB NTFS 할당 단위 크기를 설정 합니다.|
|-UseLargeFRS|에서는 많은 FRS (파일 레코드 세그먼트)를 지원할 수 있습니다. 이는 볼륨에서 파일당 허용 되는 익스텐트 수를 늘리는 데 필요 합니다. 대량 FRS 레코드의 경우이 한도가 약 150만 익스텐트에서 600만 익스텐트까지 늘어납니다.|

예를 들어 다음 cmdlet은 FRS를 사용 하도록 설정 하 고 할당 단위 크기가 64 KB 인 NTFS 볼륨으로 D 드라이브를 포맷 합니다.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

**Format** 명령을 사용할 수도 있습니다. 시스템 명령 프롬프트에서 다음 명령을 입력 합니다. 여기서 **/l** 은 큰 FRS 볼륨의 형식을 지정 하 고 **/a: 64K** 는 64 KB 할당 단위 크기를 설정 합니다.

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>최대 파일 이름 및 경로

NTFS는 긴 파일 이름 및 확장 길이 경로를 지원 하며, 최대 값은 다음과 같습니다.

- **이전 버전과의 호환성을 제공 하는 긴 파일 이름에 대 한 지원**-파일 이름 및 확장명에 대해 8.3 제한을 적용 하는 파일 시스템과의 호환성을 제공 하는 긴 파일 이름 (유니코드)을 디스크에 8.3 저장할 수 있습니다. 필요한 경우 (성능상의 이유로) Windows Server 2008 R2, Windows 8 및 최신 버전의 Windows 운영 체제에서 개별 NTFS 볼륨에 대해 8.3 별칭을 선택적으로 사용 하지 않도록 설정할 수 있습니다.
  Windows Server 2008 R2 이상 시스템에서는 운영 체제를 사용 하 여 볼륨의 형식을 지정할 때 짧은 이름이 기본적으로 사용 하지 않도록 설정 됩니다. 응용 프로그램 호환성을 위해 시스템 볼륨에 짧은 이름을 계속 사용할 수 있습니다.

- **확장 길이 경로 지원**-대부분의 Windows API 함수에는 최대\_경로 설정으로 정의 된 260 문자 경로 제한을 초과 하 여 대략 32767 자의 확장 길이 경로를 허용 하는 유니코드 버전이 있습니다. 자세한 파일 이름 및 경로 형식 요구 사항과 확장 길이 경로 구현에 대 한 지침은 [파일 이름 지정, 경로 및 네임 스페이스](https://msdn.microsoft.com/library/windows/desktop/aa365247)를 참조 하세요.

- **클러스터 된 저장소**-장애 조치 (failover) 클러스터에서 사용 하는 경우 NTFS는 CSV (클러스터 공유 볼륨) 파일 시스템과 함께 사용 될 때 여러 클러스터 노드에서 동시에 액세스할 수 있는 지속적으로 사용 가능한 볼륨을 지원 합니다. 자세한 내용은 [장애 조치 (Failover) 클러스터에서 클러스터 공유 볼륨 사용](../../failover-clustering/failover-cluster-csvs.md)을 참조 하세요.

### <a name="flexible-allocation-of-capacity"></a>유연한 용량 할당

볼륨의 공간이 제한 되는 경우 NTFS는 서버의 저장소 용량을 사용 하는 다음과 같은 방법을 제공 합니다.

- 디스크 할당량을 사용 하 여 개별 사용자에 대 한 NTFS 볼륨의 디스크 공간 사용을 추적 하 고 제어할 수 있습니다.
- 파일 시스템 압축을 사용 하 여 저장할 수 있는 데이터의 양을 최대화 합니다.
- 동일한 디스크 또는 다른 디스크에서 할당 되지 않은 공간을 추가 하 여 NTFS 볼륨의 크기를 늘립니다.
- 드라이브 문자가 부족 하거나 기존 폴더에서 액세스할 수 있는 추가 공간을 만들어야 하는 경우 로컬 NTFS 볼륨의 빈 폴더에 볼륨을 탑재 합니다.

## <a name="additional-information"></a>추가 정보

- [ReFS 및 NTFS에 대 한 클러스터 크기 권장 사항](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [ReFS (복원 파일 시스템) 개요](../refs/refs-overview.md)
- [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)
- [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2, Windows 7)
- [NTFS 상태 및 Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))
- [자동 복구 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) (Windows Server 2008에 도입 됨)
- [트랜잭션 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (Windows Server 2008에 도입 됨)
- [Windows Server의 스토리지](../storage.md)