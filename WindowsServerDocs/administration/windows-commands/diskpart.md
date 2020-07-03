---
title: diskpart
description: 컴퓨터의 드라이브를 관리 하는 데 도움이 되는 diskpart 명령 인터프리터에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: storage
author: jasongerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 87fc3a2e91b2f5ac22e87485d9258ef369ff0da0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929304"
---
# <a name="diskpart"></a>diskpart

> 적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2, Windows Server 2008

Diskpart 명령 인터프리터를 사용 하면 컴퓨터의 드라이브 (디스크, 파티션, 볼륨 또는 가상 하드 디스크)를 관리할 수 있습니다.

**Diskpart** 명령을 사용 하려면 먼저을 나열 하 고 개체를 선택 하 여 포커스를 제공 해야 합니다. 개체에 포커스가 있으면 사용자가 입력 하는 모든 diskpart 명령이 해당 개체에 대해 작동 합니다.

## <a name="list-available-objects"></a>사용 가능한 개체 나열

다음을 사용 하 여 사용 가능한 개체를 나열 하 고 개체의 번호 또는 드라이브 문자를 결정할 수 있습니다.

- `list disk`-컴퓨터의 모든 디스크를 표시 합니다.

- `list volume`-컴퓨터의 모든 볼륨을 표시 합니다.

- `list partition`-컴퓨터에 포커스가 있는 디스크의 파티션을 표시 합니다.

- `list vdisk`-컴퓨터의 모든 가상 디스크를 표시 합니다.

**목록** 명령을 실행 하면 포커스가 있는 개체 옆에 별표 (*)가 나타납니다.

## <a name="determine-focus"></a>포커스 결정

개체를 선택 하면 다른 개체를 선택할 때까지 해당 개체에 포커스가 남아 있습니다. 예를 들어 포커스가 디스크 0에 설정 되어 있고 디스크 2에서 볼륨 8을 선택 하는 경우 포커스는 디스크 0에서 디스크 2, 볼륨 8로 이동 합니다.

일부 명령은 자동으로 포커스를 변경 합니다. 예를 들어 새 파티션을 만들 때 포커스는 자동으로 새 파티션으로 전환 됩니다.

선택한 디스크의 파티션에만 포커스를 제공할 수 있습니다. 파티션에 포커스가 있으면 관련 볼륨 (있는 경우)도 포커스를 가집니다. 볼륨이 포커스가 있는 후에는 볼륨이 단일 특정 파티션에 매핑되는 경우에도 관련 디스크와 파티션이 포커스를 가집니다. 그렇지 않은 경우에는 디스크에 집중 하 고 파티션이 손실 됩니다.

## <a name="syntax"></a>구문

Diskpart 명령 인터프리터를 시작 하려면 명령 프롬프트에서 다음을 입력 합니다.

```
diskpart <parameter>
```

> [!IMPORTANT]
> Diskpart를 실행 하려면 로컬 **관리자** 그룹 또는 비슷한 권한이 있는 그룹에 있어야 합니다.

### <a name="parameters"></a>매개 변수

Diskpart 명령 인터프리터에서 다음 명령을 실행할 수 있습니다.

| 명령 | 설명 |
| ------- | ----------- |
| [active](active.md) | 포커스가 있는 디스크의 파티션을 활성으로 표시 합니다. |
| [add](add.md) | 지정한 디스크에 포커스가 있는 단순 볼륨을 미러링합니다. |
| [assign](assign.md) | 포커스가 있는 볼륨 드라이브 문자 또는 탑재 지점을 지정합니다. |
| [연결 vdisk](attach-vdisk.md) | 연결 (라고도 마운트 또는 표면) 가상 하드 디스크 (VHD) 로컬 하드 디스크 드라이브와 호스트 컴퓨터에 표시 되도록 합니다. |
| [attributes](attributes.md) | 표시 설정 하거나 디스크 또는 볼륨의 특성을 지웁니다. |
| [automount](automount.md) | 자동 탑재 기능을 사용 하지 않도록 설정 하거나 사용 합니다. |
| [break](break.md) | 포커스가 있는 미러 볼륨을 두 개의 단순 볼륨으로 나눕니다. |
| [clean](clean.md) | 포커스가 있는 디스크에서 모든 파티션 또는 볼륨 형식을 제거 합니다. |
| [compact vdisk](compact-vdisk.md) | 동적 확장 VHD (가상 하드 디스크) 파일의 실제 크기를 줄입니다. |
| [convert](convert.md) | 변환 파일 할당 테이블 (FAT) 및 FAT32 볼륨을 NTFS 파일 시스템으로 기존 파일 및 디렉터리를 그대로입니다. |
| [create](create.md) | 하나 이상의 디스크 또는 가상 하드 디스크 (VHD)에 있는 볼륨으로 디스크에 파티션을 만듭니다. |
| [delete](delete.md) | 파티션 또는 볼륨을 삭제합니다. |
| [detach vdisk](detach-vdisk.md) | 선택한 VHD (가상 하드 디스크)가 호스트 컴퓨터의 로컬 하드 디스크 드라이브로 나타나지 않도록 합니다. |
| [detail](detail.md) | 선택한 디스크, 파티션, 볼륨 또는 VHD (가상 하드 디스크)에 대 한 정보를 표시 합니다. |
| [exit](exit.md) | Diskpart 명령 인터프리터를 종료 합니다. |
| [expand vdisk](expand-vdisk.md) | 가상 하드 디스크 (VHD)을 지정 하는 크기로 확장 합니다. |
| [extend](extend.md) | 포커스가 있는 볼륨 또는 파티션을 파일 시스템과 함께 디스크의 사용 가능한 공간 (할당 되지 않은)으로 확장 합니다. |
| [filesystems](filesystems.md) | 포커스가 있는 볼륨의 현재 파일 시스템에 대 한 정보를 표시 하 고 볼륨을 포맷에 대해 지원 되는 파일 시스템을 나열 합니다. |
| [format](format.md) | Windows 파일을 수락 하도록 디스크를 포맷 합니다. |
| [gpt](gpt.md) | 기본 gpt (GUID 파티션 테이블) 디스크에 포커스가 있는 파티션에 gpt 특성을 할당 합니다. |
| [help](help.md) | 지정한 명령에 사용할 수 있는 명령 또는 자세한 도움말 정보 목록을 표시합니다. |
| [import](import.md) | 로컬 컴퓨터의 디스크 그룹에 외부 디스크 그룹을 가져옵니다. |
| [inactive](inactive.md) | 기본 MBR (마스터 부트 레코드) 디스크에서 포커스가 있는 시스템 파티션 또는 부팅 파티션을 비활성으로 표시 합니다. |
| [list](list.md) | 디스크의 디스크, 디스크의 파티션, 디스크의 볼륨 또는 Vhd (가상 하드 디스크)의 목록을 표시 합니다. |
| [merge vdisk](merge-vdisk.md) | 차이점 보관용 가상 하드 디스크 (VHD) VHD 해당 부모와 함께 병합합니다. |
| [offline](offline.md) | 온라인 디스크 또는 볼륨을 오프 라인 상태로 됩니다. |
| [online](online.md) | 오프 라인 디스크나 볼륨을 온라인 상태로 됩니다. |
| [recover](recover.md) | 디스크 그룹에 있는 모든 디스크의 상태를 새로 고치고, 잘못 된 디스크 그룹의 디스크를 복구 하 고, 오래 된 데이터를 가진 RAID-5 볼륨 및 미러 볼륨을 다시 동기화 합니다. |
| [rem](rem.md) | 스크립트에 주석을 추가 하는 방법을 제공 합니다. |
| [remove](remove.md) | 볼륨에서 드라이브 문자 또는 탑재 지점을 제거합니다. |
| [repair](repair.md) | 실패 한 디스크 영역을 지정 된 동적 디스크로 바꿔 포커스가 있는 RAID-5 볼륨을 복구 합니다. |
| [rescan](rescan.md) | 컴퓨터에 추가 된 새 디스크를 찾습니다. |
| [retain](retain.md) | 시스템 볼륨 나 기존의 동적 단순 볼륨으로 부팅을 사용 하도록 준비 합니다. |
| [san](san.md) | 운영 체제에 대 한 san (저장 영역 네트워크) 정책을 표시 하거나 설정 합니다. |
| [선택](select.md) | 디스크, 파티션, 볼륨 또는 가상 하드 디스크 (VHD)에 포커스를 이동합니다. |
| [set id](set-id.md) | 포커스가 있는 파티션에 대 한 파티션 형식 필드를 변경 합니다. |
| [축소](shrink.md) | 지정한 양만큼 선택한 볼륨의 크기를 줄입니다. |
| [uniqueid](uniqueid.md) | 포커스가 있는 디스크에 대 한 GPT (GUID 파티션 테이블) 식별자 또는 MBR (마스터 부트 레코드) 서명을 표시 하거나 설정 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [디스크 관리 개요](https://docs.microsoft.com/windows-server/storage/disk-management/overview-of-disk-management)

- [Windows PowerShell의 스토리지 Cmdlet](https://docs.microsoft.com/powershell/module/storage/)
