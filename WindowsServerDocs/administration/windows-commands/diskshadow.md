---
title: diskshadow
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e962537d-b759-4368-b6f1-e8391cf7b221
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b2c5648235a1c856c6aef09621e2381e74d08d70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869184"
---
# <a name="diskshadow"></a>diskshadow

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

diskshadow.exe는 볼륨 섀도 복사본 서비스에서 제공 하는 기능을 노출 하는 도구 \(VSS\)합니다. 기본적으로 diskshadow는 diskraid 또는 DiskPart와 유사한 대화형 명령 인터프리터를 사용합니다. diskshadow는 스크립트 가능한 모드를도 포함 되어 있습니다.  
  
> [!NOTE]  
> 로컬 Administrators 그룹 또는 이와 동등한 그룹의 멤버 자격에는 diskshadow를 실행 하는 데 필요한 최소입니다.  
  
diskshadow 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.  
  
## <a name="syntax"></a>구문  
대화형 모드에 대 한 diskshadow 명령 인터프리터를 시작 하려면 명령 프롬프트에서 다음을 입력 합니다.  
  
```  
diskshadow  
```  
  
스크립트 모드의 경우 다음을 입력 위치 *script.txt* diskshadow 명령이 포함 된 스크립트 파일은:  
  
```  
diskshadow -s script.txt  
```  
  
## <a name="diskshadow-commands"></a>diskshadow 명령  
Diskshadow 명령 인터프리터에서 또는 스크립트 파일을 통해 다음 명령을 실행할 수 있습니다.  
  
|매개 변수|설명|  
|-------|--------|  
|[set_2](set_2.md)|상황에 맞는, 옵션, 세부 정보 표시 모드 및 섀도 복사본 만들기에 대 한 메타 데이터 파일을 설정 합니다.|  
|[복원 시뮬레이션](simulate-restore.md)|실행 하지 않고 컴퓨터에 복원 세션에서 기록기 참여 테스트 **PreRestore** 또는 **PostRestore** 작성기에는 이벤트입니다.|  
|[메타 데이터를 로드](load-metadata.md)|변환할 수 있는 섀도 복사본을 가져오기 전에 메타 데이터.cab 파일을 로드 하거나 복원 하는 경우 기록기 메타 데이터를 로드 합니다.|  
|[writer](writer.md)|기록기 또는 구성 요소를 포함 또는 백업 또는 복원 프로시저에서 기록기 또는 구성 요소를 제외를 확인 합니다.|  
|[add_1](add_1.md)|볼륨 섀도 복사 되는 볼륨의 집합에 추가 하거나 별칭 환경에 별칭을 추가 합니다.|  
|[create_1](create_1.md)|현재 컨텍스트 및 옵션 설정을 사용 하 여 섀도 복사본 생성 프로세스를 시작 합니다.|  
|[exec](exec.md)|로컬 컴퓨터의 파일을 실행 합니다.|  
|[백업 시작](begin-backup.md)|전체 백업 세션을 시작합니다.|  
|[최종 백업](end-backup.md)|문제와 전체 백업 세션을 종료 한 **Backupcomplete** 필요한 경우 적절 한 기록기 상태와 이벤트입니다.|  
|[복원을 시작합니다](begin-restore.md)|복원 세션 및 문제는 **PreRestore** 관련 된 작성기에는 이벤트입니다.|  
|[복원 종료](end-restore.md)|복원 세션을 종료 시킵니다 문제는 **PostRestore** 관련 된 작성기에는 이벤트입니다.|  
|[reset](reset.md)|diskshadow를 기본 상태로 다시 설정합니다.|  
|[list](list.md)|작성자, 섀도 복사본 또는 시스템에 있는 현재 등록 된 섀도 복사본 공급자를 나열 합니다.|  
|[그림자를 삭제 합니다.](delete-shadows.md)|섀도 복사본을 삭제 합니다.|  
|[import](import.md)|시스템에 로드 된 메타 데이터 파일에서 전송 가능한 섀도 복사본을 가져옵니다.|  
|[mask](mask.md)|사용 하 여 가져온 하드웨어 섀도 복사본을 제거 합니다 **가져올** 명령입니다.|  
|[expose](expose.md)|드라이브 문자, 공유 또는 탑재 지점으로 영구 섀도 복사본을 노출합니다.|  
|[unexpose](unexpose.md)|사용 하 여 노출 된 섀도 복사본 unexposes 합니다 **노출** 명령입니다.|  
|[break_2](break_2.md)|Vss에서 섀도 복사본 볼륨을 분리합니다.|  
|[revert](revert.md)|지정된 된 섀도 복사본으로 볼륨을 되돌립니다.|  
|[exit_1](exit_1.md)|diskshadow를 종료합니다.|  
  
## <a name="remarks"></a>설명  
  
-   만 최소한 **추가** 하 고 **만듭니다** 섀도 복사본을 만드는 데 필요한 합니다. 그러나이 컨텍스트 및 옵션 설정을 상실 하 게 됩니다, 복사 백업 되며 백업 실행 스크립트가 없는 상태로 섀도 복사본을 만듭니다.  
  
## <a name="BKMK_examples"></a>예제  
이것이 샘플 일련의 백업 섀도 복사본을 통해 생성 되는 명령입니다. 해당 script.dsh, 파일에 저장 하 고 실행할 수 diskshadow를 사용 하 여 \/s script.dsh  
  
다음을 가정 합니다.  
  
-   기존 디렉터리 c:를 호출 해야\\diskshadowdata 합니다.  
  
-   시스템 볼륨이 c: 및 데이터 볼륨은 d:입니다.  
  
-   C:에서 backupscript.cmd 파일이\\diskshadowdata 합니다.  
  
-   Backupscript.cmd 파일 섀도 데이터 p: 및 q: 백업 드라이브에 복사를 수행 합니다.  
  
이러한 명령을 수동으로 입력 하거나 스크립팅할 수 수 있습니다.  
  
```  
#diskshadow script file  
set context persistent nowriters  
set metadata c:\diskshadowdata\example.cab  
set verbose on  
begin backup  
add volume c: alias Systemvolumeshadow  
add volume d: alias Datavolumeshadow  
  
create  
  
expose %Systemvolumeshadow% p:  
expose %Datavolumeshadow% q:  
exec c:\diskshadowdata\backupscript.cmd  
end backup  
#End of script  
```  
  
#### <a name="additional-references"></a>추가 참조  
[명령줄 구문 키](command-line-syntax-key.md)  
  

