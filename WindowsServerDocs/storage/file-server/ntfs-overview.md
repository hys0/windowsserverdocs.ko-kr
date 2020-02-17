---
title: NTFS 개요
description: NTFS에 대한 설명입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 06/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: b98877d0a94ff8033b65bf74d0118e2a5f1ea092
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402079"
---
# <a name="ntfs-overview"></a>NTFS 개요

>적용 대상: Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

Windows 및 Windows Server 최신 버전을 위한 기본 파일 시스템인 NTFS는 보안 설명자, 암호화, 디스크 할당량, 풍부한 메타데이터를 포함한 전체 기능 집합을 제공합니다. 또한 NTFS를 CSV(클러스터 공유 볼륨)와 함께 사용하면 장애 조치(failover) 클러스터의 여러 노드에서 동시에 액세스할 수 있는 지속적으로 사용 가능한 볼륨을 제공할 수 있습니다.

Windows Server 2012 R2에서 NTFS의 새로운 기능과 변경된 기능을 자세히 알아보려면 [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))을 참조하세요. 추가 기능에 대한 정보는 이 문서에서 [추가 정보](#additional-information) 섹션을 참조하세요. 최신 ReFS(복원 파일 시스템)에 대해 자세히 알아보려면 [ReFS(복원 파일 시스템) 개요](../refs/refs-overview.md)를 참조하세요.

## <a name="practical-applications"></a>유용한 팁

### <a name="increased-reliability"></a>향상된 안정성

NTFS는 자체 로그 파일과 검사점 정보를 사용하여 시스템 장애 후 컴퓨터를 다시 시작할 때 파일 시스템의 일관성을 복원합니다. 불량 섹터 오류가 발생한 후, NTFS는 불량 섹터가 포함된 클러스터를 동적으로 다시 매핑하고, 데이터에 새 클러스터를 할당하며, 원래 클러스터를 불량으로 표시하고, 이전 클러스터를 더 이상 사용하지 않습니다. 예를 들어 서버가 충돌한 후 NTFS는 자체 로그 파일을 재생하여 데이터를 복구할 수 있습니다.

NTFS는 볼륨을 오프라인으로 전환하지 않고 백그라운드에서 일시적인 손상 문제를 지속적으로 모니터링하고 해결합니다. (이 기능은 Windows Server 2008에 도입된 [자동 복구 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))라고 합니다.) 손상 문제가 큰 경우, Chkdsk 유틸리티는, Windows Server 2012 이상에서, 볼륨이 온라인 상태일 때 드라이브를 검색하고 분석하여, 오프라인 시간을 볼륨에서 데이터 일관성을 복원하는 데 필요한 시간으로 제한합니다. NTFS를 클러스터 공유 볼륨과 함께 사용하면 가동 중지 시간이 필요하지 않습니다. 자세한 내용은 [NTFS 상태 및 Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))(영문)를 참조하세요.

### <a name="increased-security"></a>보안 강화

- **파일 및 폴더에 대한 ACL(액세스 제어 목록) 기반 보안**—NTFS를 사용하면 파일이나 폴더에 대한 권한을 설정하고, 액세스를 제한하거나 허용할 그룹 및 사용자를 지정하고, 액세스 유형을 선택할 수 있습니다.

- **BitLocker 드라이브 암호화 지원**—BitLocker 드라이브 암호화는 NTFS 볼륨에 저장된 중요한 시스템 정보 및 기타 데이터에 대한 추가 보안을 제공합니다. Windows Server 2012 R2 및 Windows 8.1부터 BitLocker는 연결된 대기를 지원하는 TPM(신뢰할 수 있는 플랫폼 모듈)로 x86 및 x64 기반 컴퓨터에 디바이스 암호화를 지원합니다(이전에는 Windows RT 디바이스에서만 사용 가능). 디바이스 암호화는 Windows 기반 컴퓨터의 데이터를 보호하고, 악의적인 사용자가 시스템 파일에 액세스하여 사용자의 암호를 검색하거나 드라이브를 PC에서 물리적으로 분리하여 다른 PC에에 설치하지 못하도록 차단하는 데 유용합니다. 자세한 내용은 [BitLocker의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))을 참조하세요.

- **대규모 볼륨 지원**—NTFS는 최대 256테라바이트 크기의 볼륨을 지원할 수 있습니다. 지원되는 볼륨 크기는 클러스터 크기와 클러스터 수에 영향을 받습니다. (2<sup>32</sup> – 1) 클러스터(NTFS가 지원하는 최대 클러스터 수)를 사용하면 다음과 같은 볼륨 및 파일 크기가 지원됩니다.

  |클러스터 크기|최대 볼륨|최대 파일|
  |---|---|---|
  |4KB(기본 크기)|16TB|16TB|
  |8KB|32TB|32TB|
  |16KB|64TB|64TB|
  |32KB|128TB|128TB|
  |64KB(최대 크기)|256TB|256TB|

>[!IMPORTANT]
>서비스 및 앱으로 인해 파일과 볼륨 크기에 추가 제한이 있을 수 있습니다. 예를 들어, 이전 버전 기능을 사용하거나 VSS(볼륨 섀도 복사본 서비스) 스냅샷을 사용하는 백업 앱을 사용하는 경우(SAN 또는 RAID 엔클로저를 사용하지 않으면) 볼륨 크기 제한은 64TB입니다. 하지만 워크로드 및 스토리지 성능에 따라 더 작은 볼륨 크기를 사용해야 할 수도 있습니다.

### <a name="formatting-requirements-for-large-files"></a>대용량 파일에 대한 포맷 요구 사항

대용량 .vhdx 파일을 적절하게 확장할 수 있도록, 볼륨 포맷에 대한 새로운 권장 사항이 있습니다. 데이터 중복 제거에 사용될 볼륨을 포맷하거나 매우 큰 파일(예: 1TB보다 큰 .vhdx 파일)을 호스팅하는 경우, Windows PowerShell에서 다음 매개 변수와 함께 **Format-Volume** cmdlet을 사용합니다.

|매개 변수|설명|
|---|---|
|-AllocationUnitSize 64KB|64KB NTFS 할당 단위 크기를 설정합니다.|
|-UseLargeFRS|대용량 FRS(파일 레코드 세그먼트)를 지원할 수 있습니다. 볼륨에서 파일당 허용되는 익스텐트 수를 늘리는 데 필요합니다. 대용량 FRS 레코드의 경우 한도가 약 150만 개의 익스텐트에서 약 600만 개의 익스텐트로 증가합니다.|

예를 들어, 다음 cmdlet은 FRS를 사용하도록 설정하고 할당 단위 크기가 64KB인 D 드라이브를 NTFS 볼륨으로 포맷합니다.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

**format** 명령을 사용할 수도 있습니다. 시스템 명령 프롬프트에서 다음 명령을 입력합니다. 여기서 **/L**은 대용량 FRS 볼륨을 포맷하고 **/A:64k**는 64KB 할당 단위 크기를 설정합니다.

```PowerShell
format /L /A:64k
```

### <a name="maximum-file-name-and-path"></a>최대 파일 이름 및 경로

NTFS는 긴 파일 이름과 확장된 길이의 경로를 지원하며, 최댓값은 다음과 같습니다.

- **긴 파일 이름을 이전 버전과의 호환성과 함께 지원**—NTFS는 긴 파일 이름을 허용하며, 파일 이름과 확장명에 8.3 제한을 부과하는 파일 시스템과의 호환성을 제공하기 위해 디스크에 8.3 별칭을 유니코드로 저장합니다. 필요한 경우(성능상의 이유로) Windows Server 2008 R2, Windows 8 및 최신 버전 Windows 운영 체제의 개별 NTFS 볼륨에서 8.3 앨리어싱을 선택적으로 비활성화할 수 있습니다.
  Windows Server 2008 R2 이상 시스템에서는 운영 체제를 사용하여 볼륨을 포맷하면 짧은 이름이 기본적으로 비활성화됩니다. 애플리케이션 호환성을 위해 시스템 볼륨에서는 짧은 이름을 계속 사용할 수 있습니다.

- **확장 길이 경로 지원**—다수의 Windows API 함수에는 약 32,767자의 확장 길이 경로를 허용하는 유니코드 버전이 있으며 이것은 MAX\_PATH 설정에 의해 정의된 260자 경로 제한을 초과합니다. 자세한 파일 이름 및 경로 형식 요구 사항과 확장 길이 경로를 구현하는 지침은 [파일 이름 지정, 경로 및 네임스페이스](https://msdn.microsoft.com/library/windows/desktop/aa365247)를 참조하세요.

- **클러스터된 스토리지**—장애 조치(failover) 클러스터에 사용되는 경우, NTFS는 CSV(클러스터 공유 볼륨) 파일 시스템과 함께 사용하면 여러 클러스터 노드에서 동시에 액세스할 수 있는 지속적으로 사용 가능한 볼륨을 지원합니다. 자세한 내용은 [장애 조치(failover) 클러스터의 클러스터 공유 볼륨 사용](../../failover-clustering/failover-cluster-csvs.md)을 참조하세요.

### <a name="flexible-allocation-of-capacity"></a>유연한 용량 할당

볼륨의 공간이 제한된 경우 NTFS는 서버의 스토리지 용량을 처리할 수 있는 다음과 같은 방법을 제공합니다.

- 디스크 할당량을 사용하여 NTFS 볼륨에서 개별 사용자의 디스크 공간 사용량을 추적하고 제어합니다.
- 파일 시스템 압축을 사용하여 저장할 수 있는 데이터 양을 최대화합니다.
- 동일한 디스크 또는 다른 디스크에서 할당되지 않은 공간을 추가하여 NTFS 볼륨의 크기를 늘립니다.
- 드라이브 문자가 부족하거나 기존 폴더에서 액세스할 수 있는 추가 공간을 만들어야 하는 경우 로컬 NTFS 볼륨의 빈 폴더에 볼륨을 마운트합니다.

## <a name="additional-information"></a>추가 정보

- [ReFS 및 NTFS에 대한 클러스터 크기 권장 사항](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Cluster-size-recommendations-for-ReFS-and-NTFS/ba-p/425960)
- [ReFS(복원 파일 시스템) 개요](../refs/refs-overview.md)
- [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))(Windows Server 2012 R2)
- [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10))(Windows Server 2008 R2, Windows 7)
- [NTFS 상태 및 Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))
- [자동 복구 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10))(Windows Server 2008에 도입됨)
- [트랜잭션 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10))(Windows Server 2008에 도입됨)
- [Windows Server의 스토리지](../storage.md)