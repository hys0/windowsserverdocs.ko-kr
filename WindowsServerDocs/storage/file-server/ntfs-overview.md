---
title: NTFS 개요
description: NTFS 란 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/06/2018
ms.localizationpriority: medium
ms.openlocfilehash: 556110fe7bed1aed002ef6d985324ff5171e770e
ms.sourcegitcommit: 5ed023a2ef3a9002daf41c7717feb1df186d2a14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/02/2019
ms.locfileid: "9122106"
---
# NTFS 개요

>적용 대상: Windows 10, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

NTFS-최신 버전의 Windows 및 Windows Server에 대 한 기본 파일 시스템-보안 설명자, 암호화, 디스크 할당량, 풍부한 메타 데이터를 포함 하 여 기능의 전체 집합을 제공 하 고 지속적으로 제공 하기 위해 사용 하 여 클러스터 공유 볼륨 (CSV)을 사용할 수 장애 조치 클러스터의 여러 노드에서 동시에 액세스할 수 있는 사용 가능한 볼륨입니다.

Windows Server 2012 r 2의 NTFS의 새로운 기능과 변경 된 기능에 대 한 자세한 내용은 [NTFS의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11))을 참조 하세요. 추가 기능 정보에 대 한이 항목의 [추가 정보](#additional-information) 섹션을 참조 하세요. 새로운 ReFS (복원 파일 시스템)에 대 한 자세한 내용은 [ReFS (복원 파일 시스템) 개요](../refs/refs-overview.md)를 참조 하세요.

## 유용한 팁

### 향상 된 안정성

NTFS는 시스템 오류가 발생 한 후 컴퓨터를 다시 시작할 때 파일 시스템의 일관성을 복원 하려면 로그 파일과 검사점 정보를 사용 합니다. 불량 섹터 오류가 발생 한 후 동적으로 NTFS 불량 섹터 포함, 데이터에 대 한 새 클러스터를 할당 하 고, 불량 섹터, 원래 클러스터를 표시 하 고 더 이상 기존 클러스터를 사용 하 여 클러스터를 다시 매핑합니다. 예를 들어 서버 충돌 후 NTFS 데이터를 복구할 수는 로그 파일을 재생 합니다.

NTFS는 지속적으로 모니터링 하 고 (이 기능은 [자동 복구 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)), Windows Server 2008에 도입 된 명칭)는 볼륨을 오프 라인으로 전환 하지 않고도 백그라운드에서 임시 손상 문제를 해결 합니다. 더 큰 손상 문제에 대 한 Windows Server 2012 이상, Chkdsk 유틸리티를 검사 하 고 볼륨이 온라인 시간 오프 라인으로 볼륨의 데이터 일관성을 복원 하는 데 필요한 시간을 제한 하는 동안 드라이브를 분석 합니다. NTFS 클러스터 공유 볼륨을 사용 하는 경우에 작동이 중단 되지 필요 합니다. 자세한 내용은 [NTFS 상태 및 Chkdsk를](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))참조 하세요.

### 향상 된 보안

- **파일 및 폴더에 대 한 액세스 제어 목록 ACL 기반 보안**-NTFS 파일 또는 폴더에 사용 권한을 설정할 수 있습니다 그룹과 사용자가 제한 하거나, 허용 하려는 액세스를 지정 하 고 액세스 유형을 선택 합니다.

- **BitLocker 드라이브 암호화에 대 한 지원**-BitLocker 드라이브 암호화는 중요 한 시스템 정보 및 NTFS 볼륨에 저장 된 다른 데이터에 대 한 추가 보안을 제공 합니다. Windows Server 2012 R2 및 Windows 8.1 부터는 BitLocker는 지원 x86 및 x64 기반 컴퓨터와는 신뢰할 수 있는 플랫폼 모듈 (TPM)에서 장치 암호화에 대 한 지원 스탠드 방어 해 (이전에, Windows RT 디바이스에 대해서만 제공) 연결을 합니다. 장치 암호화는 Windows 기반 컴퓨터에서 데이터를 보호 하 고 악의적인 사용자가 사용자의 암호를 검색 하에 의존 하는 시스템 파일에 액세스 하지 못하도록 또는 물리적으로 PC에서 제거 하 고에 설치 하 여 드라이브에 액세스 하지 못하도록 차단 하는 데 도움이 다른 것입니다. 자세한 내용은 [이란 BitLocker의 새로운 기능](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn306081(v%3dws.11))을 참조 하세요.

- **대규모 볼륨 지원**-NTFS 볼륨 크게 256 테라바이트를 지원할 수 있습니다. 볼륨 크기는 클러스터 크기와 클러스터의 수가 받지 지원 됩니다. 사용 하 여 (2<sup>32</sup> – 1) 클러스터 (NTFS 지 클러스터의 최대 수), 다음 볼륨 및 파일 크기 지원 됩니다.

  |클러스터 크기|큰 볼륨|가장 큰 파일|
  |---|---|---|
  |4KB (기본값)|16TB|16TB|
  |8KB|32TB|32TB|
  |16 KB|64TB|64TB|
  |32KB|128TB|128TB|
  |64KB (최대 크기)|256TB|256TB|

>[!IMPORTANT]
>서비스 및 앱 파일 및 볼륨 크기에 대 한 추가 제한을 적용 될 수 있습니다. 예를 들어, 볼륨 크기 제한은 볼륨 섀도 복사본 서비스 (VSS) 스냅숏을 사용 하 여 이전 버전 기능 또는 하는 백업 앱을 사용 하는 경우 64TB (및 SAN 또는 RAID 인클로저를 사용 하지 않는). 그러나 워크 로드와 저장소의 성능에 따라 더 작은 볼륨 크기를 사용 해야 합니다.

### 대용량 파일에 대 한 요구 사항 서식 지정

큰.vhdx 파일의 적절 한 확장을 허용 하려면 볼륨을 포맷할에 대 한 새로운 권장 있습니다. 데이터 중복 제거와 함께 사용할 또는 1TB 보다 큰.vhdx 파일 등 매우 큰 파일을 호스팅할는 볼륨을 포맷할 때 다음 매개 변수를 사용 하 여 Windows PowerShell에서 **볼륨 포맷** cmdlet을 사용 합니다.

|매개 변수|설명|
|---|---|
|-AllocationUnitSize 64KB|64KB NTFS 할당 단위 크기를 설정합니다.|
|-UseLargeFRS|큰 파일 레코드 세그먼트 (FRS)을 지원 합니다. 이 범위까지 허용 되는 각 볼륨에 파일의 수를 늘릴 필요 합니다. 큰 FRS 레코드에 대 한 제한 약 1.5 백만 범위에서 약 6 백만 범위를 증가합니다.|

예를 들어 다음 cmdlet 형식 D 드라이브는 NTFS 볼륨으로 활성화 FRS 64KB의 할당 단위 크기와 합니다.

```PowerShell
Format-Volume -DriveLetter D -FileSystem NTFS -AllocationUnitSize 64KB -UseLargeFRS
```

또한 **형식의** 명령을 사용할 수 있습니다. 시스템 명령 프롬프트에서 **/L** 형식 FRS 대용량 **/A:64 k** 64KB 할당 단위 크기를 설정 하며, 다음 명령을 입력 합니다.

```PowerShell
format /L /A:64k
```

### 최대 파일 이름 및 경로

NTFS 긴 파일 이름 및 다음 최대 값을 가진 확장 길이 경로 지원합니다.

- **이전 버전과 호환성을 사용 하 여 긴 파일 이름에 대 한 지원**-NTFS 허용 긴 파일 이름, 파일 이름 및 확장명을 8.3 제한 하는 파일 시스템과의 호환성을 제공 하기 위해 별칭 (유니코드)에서 디스크에는 8.3을 저장 합니다. (성능상의 이유로) 필요한 경우 Windows Server 2008 R2, Windows 8 및 Windows 운영 체제의 최신 버전의 개별 NTFS 볼륨의 8.3 앨리어싱을 선택적으로 해제할 수 있습니다.
  Windows Server 2008 R2 및 이후 시스템의 짧은 이름 볼륨은 운영 체제를 사용 하 여 포맷 하는 경우에 기본적으로 비활성화 됩니다. 응용 프로그램 호환성에 대 한 짧은 이름 여전히를 사용할 시스템 볼륨에 있습니다.

- **확장 길이 경로 대 한 지원**등 여러 Windows API 함수에는 확장 길이 경로 약 32767 문자를 사용할 수 있는 유니코드 버전-MAX\_PATH 설정에 의해 정의 된 260 문자 경로 제한을 초과 합니다. 세부 파일 이름 및 경로 형식 요구 사항 및 확장 길이 경로 구현 하기 위한 지침, [파일 이름 지정, 경로 및 네임 스페이스를](https://msdn.microsoft.com/library/windows/desktop/aa365247)참조 하세요.

- **클러스터 저장소**-장애 조치 클러스터를 사용 하면 NTFS 클러스터 공유 볼륨 (CSV) 파일 시스템와 함께 사용 되는 경우에 동시에 여러 클러스터 노드에서 액세스할 수 있는 지속적으로 사용 가능한 볼륨을 지원 합니다. 자세한 내용은 [장애 조치 클러스터에서 사용 하 여 클러스터 공유 볼륨](../../failover-clustering/failover-cluster-csvs.md)을 참조 하세요.

### 유연한 용량 할당

볼륨의 공간을 제한 된 경우 NTFS 서버의 저장소 용량을 사용 하려면 다음과 같은 방법으로 제공 합니다.

- 디스크 할당량을 사용 하 여 추적 하 고 개별 사용자에 대 한 NTFS 볼륨의 디스크 공간 사용을 제어 합니다.
- 저장할 수 있는 데이터의 양을 최대화 하려면 파일 시스템 압축을 사용 합니다.
- 동일한 디스크 또는 다른 디스크의 할당 되지 않은 공간을 추가 하 여 NTFS 볼륨의 크기를 늘립니다.
- 드라이브 문자 막아 기존 폴더에서 액세스할 수 있는 추가 공간을 만드는 필요한 경우 로컬 NTFS 볼륨의 빈 폴더에 볼륨을 탑재 합니다.

## 추가 정보

|콘텐츠 유형|참조|
|---|---|
|평가|- [NTFS의 새로운 소식](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn466520(v%3dws.11)) (Windows Server 2012 R2)<br>- [NTFS의 새로운 소식](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff383236(v=ws.10)) (Windows Server 2008 R2, Windows 7)<br>- [NTFS 상태 및 Chkdsk](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831536(v%3dws.11))<br>- [NTFS 자동 복구](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc771388(v=ws.10)) (Windows Server 2008에서 도입 됨)<br>- [트랜잭션 NTFS](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc730726(v%3dws.10)) (Windows Server 2008에서 도입 됨)|
|커뮤니티 리소스|- [Windows 저장소 팀 블로그](https://blogs.msdn.microsoft.com/san/)|
|관련 기술|- [Windows Server의 저장소](../storage.md)<br>- [클러스터 공유 볼륨에 장애 조치 클러스터 사용](../../failover-clustering/failover-cluster-csvs.md)<br>- [클러스터 공유 볼륨](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#cluster-shared-volumes>) 및 [저장소 디자인](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)#storage-design>) 의 섹션 [클라우드 인프라 디자인](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831630(v%3dws.11)) <br>- [저장소 공간](../storage-spaces/overview.md)<br>- [복원 파일 시스템 (참조) 개요](../refs/refs-overview.md)
