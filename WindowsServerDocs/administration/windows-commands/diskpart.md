---
title: DiskPart
description: 컴퓨터의 드라이브를 관리 하는 데 도움이 되는 DiskPart의 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: storage
author: jasongerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 45fe66e4843b96db8e4593c0e963e4a80dbd22c2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845476"
---
# <a name="diskpart"></a>DiskPart

>적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, windows server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2, Windows Server 2008

DiskPart 명령은 컴퓨터의 드라이브 (디스크, 파티션, 볼륨 또는 가상 하드 디스크)를 관리 하는 데 도움이 됩니다. 

DiskPart 명령을 사용 하려면 먼저을 나열 하 고 개체를 선택 하 여 포커스를 제공 해야 합니다. 개체에 포커스가 있으면 사용자가 입력 하는 모든 DiskPart 명령이 해당 개체에 대해 작동 합니다.

## <a name="list-the-available-objects"></a>사용 가능한 개체 나열

다음을 사용 하 여 사용 가능한 개체를 나열 하 고 개체의 번호 또는 드라이브 문자를 결정할 수 있습니다.

- `list disk`-컴퓨터의 모든 디스크를 표시 합니다.

- `list volume`-컴퓨터의 모든 볼륨을 표시 합니다.

- `list partition`-컴퓨터에 포커스가 있는 디스크의 파티션을 표시 합니다.

- `list vdisk`-컴퓨터의 모든 가상 디스크를 표시 합니다.

**목록** 명령을 사용 하면 포커스가 있는 개체 옆에 별표 (\*)가 나타납니다.

## <a name="determine-focus"></a>포커스 결정

개체를 선택 하면 다른 개체를 선택할 때까지 해당 개체에 포커스가 남아 있습니다. 예를 들어 포커스가 디스크 0에 설정 되어 있고 디스크 2에서 볼륨 8을 선택 하는 경우 포커스는 디스크 0에서 디스크 2, 볼륨 8로 이동 합니다.

일부 명령은 자동으로 포커스를 변경 합니다. 예를 들어 새 파티션을 만들 때 포커스는 자동으로 새 파티션으로 전환 됩니다.

선택한 디스크의 파티션에만 포커스를 제공할 수 있습니다. 파티션에 포커스가 있으면 관련 볼륨 (있는 경우)도 포커스를 가집니다. 볼륨에 포커스가 있을 때 볼륨이 단일 특정 파티션에 매핑되는 경우에도 관련 디스크와 파티션이 포커스를 가집니다. 그렇지 않은 경우에는 디스크에 집중 하 고 파티션이 손실 됩니다.

## <a name="diskpart-commands"></a>DiskPart 명령

DiskPart 명령 인터프리터를 시작 하려면 명령 프롬프트에서 다음을 입력 합니다.

```
diskpart
```

> [!IMPORTANT]
> DiskPart를 실행 하려면 로컬 **관리자** 그룹 또는 비슷한 권한이 있는 그룹에 있어야 합니다. 

Diskpart 명령 인터프리터에서 다음 명령을 실행할 수 있습니다.

| 명령 | 설명 |
| ------- | ----------- |
| [활성](active.md) | 포커스가 있는 디스크의 파티션을 활성으로 표시 합니다. |
| [추가](add.md) | 지정한 디스크에 포커스가 있는 단순 볼륨을 미러링합니다. |
| [할당](assign.md) | 포커스가 있는 볼륨 드라이브 문자 또는 탑재 지점을 지정합니다. |
| [연결 vdisk](attach-vdisk.md) | 연결 (라고도 마운트 또는 표면) 가상 하드 디스크 (VHD) 로컬 하드 디스크 드라이브와 호스트 컴퓨터에 표시 되도록 합니다. |
| [특성](attributes.md) | 표시 설정 하거나 디스크 또는 볼륨의 특성을 지웁니다. |
| [자동 탑재](automount.md) | 자동 탑재 기능을 사용 하지 않도록 설정 하거나 사용 합니다. | 
| [끊어야](break.md) | 포커스가 있는 미러 볼륨을 두 개의 단순 볼륨으로 나눕니다. |
| [청소할](clean.md) | 포커스가 있는 디스크에서 모든 파티션 또는 볼륨 형식을 제거 합니다. |
| [Compact vdisk](compact-vdisk.md) | 동적 확장 VHD (가상 하드 디스크) 파일의 실제 크기를 줄입니다. |
| [변환할지](convert.md) | 변환 파일 할당 테이블 (FAT) 및 FAT32 볼륨을 NTFS 파일 시스템으로 기존 파일 및 디렉터리를 그대로입니다. |
| [만들기](create.md) | 하나 이상의 디스크 또는 가상 하드 디스크 (VHD)에 있는 볼륨으로 디스크에 파티션을 만듭니다. |
| [삭제](delete.md) | 파티션 또는 볼륨을 삭제합니다. |
| [분리 vdisk](detach-vdisk.md) | 선택한 VHD (가상 하드 디스크)가 호스트 컴퓨터의 로컬 하드 디스크 드라이브로 나타나지 않도록 합니다. |
| [Detail](detail.md) | 선택한 디스크, 파티션, 볼륨 또는 VHD (가상 하드 디스크)에 대 한 정보를 표시 합니다. |
| [종료](exit.md) | DiskPart 명령 인터프리터를 종료합니다. |
| [Vdisk 확장](expand-vdisk.md) | 
| [넘으면](extend.md) | 
| [파일 시스템](filesystems.md) | 
| [형식](format.md) | 
| [GPT](gpt.md) | 
| [도움말](help.md) | 
| [가져오기](import.md) | 
| [라](inactive.md) | 
| [목록](list.md) | 
| [Merge vdisk](merge-vdisk.md) | 
| [라인인](offline.md) | 
| [온라인](online.md) | 
| [확보](recover.md) | 
| [남은](rem.md) | 
| [제거](remove.md) | 
| [복구한](repair.md) | 
| [검사](rescan.md) | 
| [그대로](retain.md) | 
| [산마리노](san.md) | 
| [선택](select.md) | 
| [집합 id](set-id.md) | 
| [축소할](shrink.md) | 
| [Uniqueid](uniqueid.md) | 

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키] (command-line-syntax-key.md

- [디스크 관리 개요](https://docs.microsoft.com/windows-server/storage/disk-management/overview-of-disk-management)

- [Windows PowerShell의 저장소 Cmdlet](https://docs.microsoft.com/powershell/module/storage/)
