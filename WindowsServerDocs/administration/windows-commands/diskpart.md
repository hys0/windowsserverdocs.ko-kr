---
Title: DiskPart 명령
ms.prod: windows-server-threshold
ms.technology: storage
author: JasonGerend
manager: elizapo
ms.author: jgerend
ms.openlocfilehash: 3cc0667b54dba75d892795f6520664ce7a7a62a5
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192653"
---
# <a name="diskpart-commands"></a>DiskPart 명령

적용 대상: Windows 10, Windows 8.1, Windows 8, Windows 7, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2, Windows Server 2008

DiskPart 명령에는 PC의 드라이브 (디스크, 파티션, 볼륨 또는 가상 하드 디스크)를 관리할 수 있습니다. DiskPart 명령을 사용할 수 있습니다, 전에 먼저 나열 하 고 포커스를 제공 하는 개체를 선택 해야 합니다. 개체에 포커스가 있는 경우 입력 하는 DiskPart 명령을 모든 해당 개체에 대해 작동 합니다.

사용 가능한 개체를 나열 하 고 사용 하 여 개체의 숫자 또는 드라이브 문자를 확인할 수는 **목록 디스크, 볼륨 목록, 목록 파티션**, 및 **vdisk 목록** 명령입니다. 합니다 **디스크 목록, 목록 vdisk** 하 고 **볼륨 목록** 명령은 컴퓨터의 모든 디스크 및 볼륨을 표시 합니다. 그러나 합니다 **파티션 목록이** 명령 포커스가 있는 디스크에 파티션을 표시 합니다. 사용 하는 경우는 **목록을** 명령, 별표 (\*) 포커스가 있는 개체 옆에 나타납니다.

개체를 선택 하면 포커스를 다른 개체를 선택할 때까지 해당 개체에 남아 있습니다. 예를 들어 디스크 0의 포커스를 설정 하는 디스크 2의 8 볼륨을 선택 하 고 포커스는 디스크 0에서에서 2, 8 볼륨 디스크를 이동 합니다. 일부 명령은 자동으로 포커스를 변경합니다. 예를 들어 새 파티션을 만들면 포커스를 자동으로 전환 새 파티션으로 합니다.

선택된 된 된 디스크에 있는 파티션에 포커스를 제공할 수 있습니다. 파티션의 포커스가 관련된 볼륨 (있는 경우)에 게 포커스가 있습니다. 볼륨에 포커스, 관련 된 디스크 및 파티션 볼륨 단일 특정 파티션에 매핑되는 경우 포커스를 가질 수도 있습니다. 이 경우 디스크에 포커스 없고 파티션 손실 됩니다.

## <a name="diskpart-commands"></a>DiskPart 명령

명령 프롬프트에서 입력 DiskPart 명령 인터프리터를 시작 합니다.

`diskpart`

> [!IMPORTANT]
> 로컬의 멤버 자격이 **관리자** 그룹 또는 그에 해당 하는 DiskPart를 실행 하는 데 필요한 최소입니다. 

Diskpart 명령 인터프리터에 다음 명령을 실행할 수 있습니다.

  - [활성](active.md)  
      
  - [추가](add.md)  
      
  - [Assign](assign.md)  
      
  - [vdisk를 연결 합니다.](attach-vdisk.md)  
      
  - [특성](attributes.md)  
      
  - [Automount](automount.md)  
      
  - [나누기](break.md)  
      
  - [정리](clean.md)  
      
  - [vdisk를 압축 합니다.](compact-vdisk.md)  
      
  - [변환](convert.md)  
      
  - [만들기](create.md)  
      
  - [Delete](delete.md)  
      
  - [Vdisk를 분리 합니다.](detach-vdisk.md)  
      
  - [Detail](detail.md)  
      
  - [종료](exit.md)  
      
  - [vdisk를 확장 합니다.](expand-vdisk.md)  
      
  - [확장](extend.md)  
      
  - [파일 시스템](filesystems.md)  
      
  - [형식](format.md)  
      
  - [GPT](gpt.md)  
      
  - [도움말](help.md)  
      
  - [가져오기](import.md)  
      
  - [비활성](inactive.md)  
      
  - [목록](list.md)  
      
  - [Vdisk를 병합 합니다.](merge-vdisk.md)  
      
  - [오프 라인](offline.md)  
      
  - [온라인](online.md)  
      
  - [Recover](recover.md)  
      
  - [Rem](rem.md)  
      
  - [제거](remove.md)  
      
  - [복구](repair.md)  
      
  - [다시 검사](rescan.md)  
      
  - [유지](retain.md)  
      
  - [San](san.md)  
      
  - [Select](select.md)  
      
  - [집합 id](set-id.md)  
      
  - [축소](shrink.md)  
      
  - [uniqueid](uniqueid.md)  
      

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[Windows PowerShell의 저장소 Cmdlet](https://docs.microsoft.com/en-us/powershell/module/storage/)
