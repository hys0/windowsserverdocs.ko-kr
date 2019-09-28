---
title: Diskpart 스크립트 및 예제
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 319c0795-11df-47c8-b203-eadb0577ee0d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c40ce79664795297af4369e35cbda7422617e6e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377846"
---
# <a name="diskpart-scripts-and-examples"></a>Diskpart 스크립트 및 예제

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diskpart `/s`을 사용 하 여 볼륨을 만들거나 동적 디스크로 디스크를 변환 하는 것과 같은 디스크 @ no__t-1related 작업을 자동화 하는 스크립트를 실행 합니다. 이러한 작업은 부팅 볼륨이 아닌 볼륨 만들기를 지원 하지 않는 무인 설치 또는 Sysprep 도구를 사용 하 여 Windows를 배포 하는 경우에 유용 합니다.  
  
-   Diskpart 스크립트를 만들려면 실행할 Diskpart 명령이 포함 된 텍스트 파일을 만듭니다. 한 줄에 한 개의 명령만 있으면 빈 줄이 없습니다. @No__t-0으로 줄을 시작 하 여 줄을 주석으로 만들 수 있습니다.  
  
    예를 들어 다음은 디스크를 초기화 한 다음 Windows 복구 환경용 300 MB 파티션을 만드는 스크립트입니다.  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label="Windows RE tools"  
    assign letter="T"  
    ```  
  
-   DiskPart 스크립트를 실행 하려면 명령 프롬프트에서 다음 명령을 입력 합니다. 여기서 *scriptname* 은 스크립트를 포함 하는 텍스트 파일의 이름입니다.  
  
    ```  
    diskpart /s scriptname.txt  
    ```  
  
-   DiskPart의 스크립팅 출력을 파일로 리디렉션하려면 다음 명령을 입력 합니다. 여기서 *logfile* 은 diskpart가 출력을 쓰는 텍스트 파일의 이름입니다.  
  
    ```  
    diskpart /s scriptname.txt > logfile.txt  
    ```  
  
> [!IMPORTANT]  
> **Diskpart** 명령을 스크립트의 일부로 사용 하는 경우 단일 diskpart 스크립트의 일부로 모든 diskpart 작업을 함께 수행 하는 것이 좋습니다. 연속 되는 DiskPart 스크립트를 실행할 수 있지만 연속 스크립트에서 **diskpart** 명령을 다시 실행 하기 전에 이전 실행을 완전히 종료 하기 위해 각 스크립트 사이에 15 초가 이상 허용 되어야 합니다. 그렇지 않으면 후속 스크립트가 실패할 수 있습니다. DiskPart 스크립트와 함께 배치 파일에 `timeout /t 15` 명령을 추가 하 여 연속 DiskPart 스크립트 사이에 일시 중지를 추가할 수 있습니다.  
  
DiskPart가 시작 되 면 명령 프롬프트에 DiskPart 버전 및 컴퓨터 이름이 표시 됩니다. 기본적으로 스크립팅된 태스크를 수행 하는 동안 DiskPart에 오류가 발생 하는 경우 DiskPart는 스크립트 처리를 중지 하 고 매개 변수 @ no__t-2를 지정 하지 않는 한 오류 코드 \(을 **표시 합니다.** 그러나 DiskPart **는 매개 변수를 사용** 했는지 여부에 관계 없이 구문 오류가 발생할 경우 항상 오류를 반환 합니다. **Noerr** 매개 변수를 사용 하면 총 디스크 수에 관계 없이 단일 스크립트를 사용 하 여 모든 디스크의 모든 파티션을 삭제 하는 것과 같은 유용한 작업을 수행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[샘플: Windows PE 및 DiskPart @ no__t-2를 사용 하 여 UEFI @ no__t-0gpt @ no__t 기반 하드 드라이브 파티션을 구성 합니다.  
[샘플: Windows PE 및 DiskPart @ no__t-2를 사용 하 여 BIOS @ no__t-0MBR @ no__t 기반 하드 디스크 파티션을 구성 합니다.  
[Windows PowerShell의 저장소 Cmdlet](https://technet.microsoft.com/library/hh848705.aspx)  
  

