---
title: DiskPart 명령
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 7155dbf34f9986b3ebdd8b549b6a861cf7fcfe3a
ms.sourcegitcommit: 23a6e83b688119c9357262b6815c9402c2965472
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2019
ms.locfileid: "69560439"
---
# <a name="diskpart-commands"></a>DiskPart 명령

적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, windows server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2, Windows Server 2008

DiskPart 명령은 PC의 드라이브 (디스크, 파티션, 볼륨 또는 가상 하드 디스크)를 관리 하는 데 도움이 됩니다. DiskPart 명령을 사용 하려면 먼저을 나열 하 고 개체를 선택 하 여 포커스를 제공 해야 합니다. 개체에 포커스가 있으면 사용자가 입력 하는 모든 DiskPart 명령이 해당 개체에 대해 작동 합니다.

사용 가능한 개체를 나열 하 고 **list disk, list volume, list partition**및 **list vdisk** 명령을 사용 하 여 개체의 번호 또는 드라이브 문자를 결정할 수 있습니다. **디스크 목록, vdisk 목록** 및 **볼륨 나열** 명령이 컴퓨터의 모든 디스크 및 볼륨을 표시 합니다. 그러나 **파티션 나열** 명령은 포커스가 있는 디스크의 파티션만 표시 합니다. **목록** 명령을 사용 하면 포커스가 있는 개체 옆에 별표\*()가 나타납니다.

개체를 선택 하면 다른 개체를 선택할 때까지 해당 개체에 포커스가 남아 있습니다. 예를 들어 포커스가 디스크 0에 설정 되어 있고 디스크 2에서 볼륨 8을 선택 하는 경우 포커스는 디스크 0에서 디스크 2, 볼륨 8로 이동 합니다. 일부 명령은 자동으로 포커스를 변경 합니다. 예를 들어 새 파티션을 만들 때 포커스는 자동으로 새 파티션으로 전환 됩니다.

선택한 디스크의 파티션에만 포커스를 제공할 수 있습니다. 파티션에 포커스가 있으면 관련 볼륨 (있는 경우)도 포커스를 가집니다. 볼륨에 포커스가 있을 때 볼륨이 단일 특정 파티션에 매핑되는 경우에도 관련 디스크와 파티션이 포커스를 가집니다. 그렇지 않은 경우에는 디스크에 집중 하 고 파티션이 손실 됩니다.

## <a name="diskpart-commands"></a>DiskPart 명령

DiskPart 명령 인터프리터를 시작 하려면 명령 프롬프트에서 다음을 입력 합니다.

`diskpart`

> [!IMPORTANT]
> DiskPart를 실행 하려면 최소한 로컬 **Administrators** 그룹의 구성원 이거나 이와 동등한 자격이 필요 합니다. 

Diskpart 명령 인터프리터에서 다음 명령을 실행할 수 있습니다.

  - [활성](active.md)  
      
  - [추가](add.md)  
      
  - [할당](assign.md)  
      
  - [연결 vdisk](attach-vdisk.md)  
      
  - [특성](attributes.md)  
      
  - [자동 탑재](automount.md)  
      
  - [Break](break.md)  
      
  - [청소할](clean.md)  
      
  - [Compact vdisk](compact-vdisk.md)  
      
  - [변환할지](convert.md)  
      
  - [만들기](create.md)  
      
  - [Delete](delete.md)  
      
  - [분리 vdisk](detach-vdisk.md)  
      
  - [Detail](detail.md)  
      
  - [끝내기](exit.md)  
      
  - [Vdisk 확장](expand-vdisk.md)  
      
  - [넘으면](extend.md)  
      
  - [파일 시스템](filesystems.md)  
      
  - [형식](format.md)  
      
  - [GPT](gpt.md)  
      
  - [도움말](help.md)  
      
  - [가져오기](import.md)  
      
  - [라](inactive.md)  
      
  - [목록](list.md)  
      
  - [Merge vdisk](merge-vdisk.md)  
      
  - [라인인](offline.md)  
      
  - [온라인](online.md)  
      
  - [확보](recover.md)  
      
  - [남은](rem.md)  
      
  - [제거](remove.md)  
      
  - [복구한](repair.md)  
      
  - [검사](rescan.md)  
      
  - [그대로](retain.md)  
      
  - [산마리노](san.md)  
      
  - [Select](select.md)  
      
  - [집합 id](set-id.md)  
      
  - [축소할](shrink.md)  
      
  - [Uniqueid](uniqueid.md)  
      

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[Windows PowerShell의 저장소 Cmdlet](https://docs.microsoft.com/powershell/module/storage/)
