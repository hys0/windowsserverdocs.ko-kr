---
title: Diskpart 스크립트 및 예제
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a8bd0dfab98ca705cf64766d66285c69bd3d3129
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862794"
---
# <a name="diskpart-scripts-and-examples"></a>Diskpart 스크립트 및 예제

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diskpart를 사용 하 여 `/s` 디스크를 자동화 하는 스크립트를 실행 하려면\-관련 볼륨을 만들거나 디스크를 동적 디스크로 변환 등의 작업을 합니다. 이러한 작업을 스크립팅 하는 것은 배포할 Windows 무인된 설치 또는 Sysprep 도구를 사용 하 여 부팅 볼륨 이외의 볼륨 작성을 지원 하지 않는 경우에 유용 합니다.  
  
-   Diskpart 스크립트를 작성 하려면 줄당 하나의 명령을 빈 줄과 실행 하려는 Diskpart 명령을 포함 하는 텍스트 파일을 만듭니다. 줄을 시작할 수 있습니다 `rem` 주석 줄을 확인 합니다.  
  
    예를 들어, 여기서 s는 디스크를 초기화 하 고 다음 Windows 복구 환경 300MB 파티션을 만듭니다 스크립트:  
  
    ```  
    select disk 0  
    clean  
    convert gpt  
    create partition primary size=300  
    format quick fs=ntfs label="Windows RE tools"  
    assign letter="T"  
    ```  
  
-   DiskPart 스크립트, 명령 프롬프트를 실행 하려면 다음 명령을 입력 위치 *scriptname* 스크립트를 포함 하는 텍스트 파일의 이름입니다.  
  
    ```  
    diskpart /s scriptname.txt  
    ```  
  
-   DiskPart의 스크립트 출력을 파일로 리디렉션할 다음 명령을 입력 위치 *logfile* DiskPart에서 해당 출력을 기록 하는 위치 텍스트 파일의 이름입니다.  
  
    ```  
    diskpart /s scriptname.txt > logfile.txt  
    ```  
  
> [!IMPORTANT]  
> 사용 하는 경우는 **DiskPart** 스크립트의 일부로 명령을 완료 하는 모든 작업은 DiskPart 단일 DiskPart 스크립트의 일부로 함께 하는 것이 좋습니다. 연속 DiskPart 스크립트를 실행할 수 있지만 15 초 이상 실행 하기 전에 이전에 실행 완료 종료에 대 한 각 스크립트 간에 허용 해야 합니다 **DiskPart** 연속 스크립트 다시 명령을 합니다. 그렇지 않은 경우 연속 스크립트가 실패할 수 있습니다. 추가 하 여 연속 DiskPart 스크립트 간에 일시 중지를 추가할 수는 `timeout /t 15` DiskPart 스크립트와 함께 배치 파일을 명령 합니다.  
  
DiskPart 시작 되 면 명령 프롬프트에서 DiskPart 버전 및 컴퓨터 이름을 표시 합니다. 기본적으로 DiskPart 스크립팅된 작업을 수행 하는 동안 오류가 발생 하는 경우 DiskPart 스크립트 처리를 중지 하 고 오류 코드를 표시 \(을 지정 하지 않으면 합니다 **디스크** 매개 변수\)합니다. 그러나 DiskPart 항상 반환 오류 사용 여부에 관계 없이 구문 오류가 발생 합니다 **디스크** 매개 변수입니다. 합니다 **디스크** 매개 변수를 사용 하면 디스크의 총 수에 관계 없이 모든 디스크의 모든 파티션을 삭제 하는 단일 스크립트를 사용 하는 등 유용한 작업을 수행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
[샘플: UEFI를 구성\/gpt\-기반 하드 드라이브 파티션을 사용 하 여 Windows PE 및 DiskPart](https://technet.microsoft.com/library/hh825686.aspx)  
[샘플: BIOS를 구성\/MBR\-Windows PE 및 DiskPart를 사용 하 여 하드 디스크 파티션 기반](https://technet.microsoft.com/library/hh825677.aspx)  
[Windows PowerShell의 저장소 Cmdlet](https://technet.microsoft.com/library/hh848705.aspx)  
  

