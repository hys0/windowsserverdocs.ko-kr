---
title: PowerShell_ise
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03c765b276a2e61247661e132dd49434b444530c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817284"
---
# <a name="powershellise"></a>PowerShell_ise



Windows PowerShell 통합 스크립팅 환경 (ISE)는 읽기, 쓰기, 실행, 디버그 및 그래픽 기반 환경에서 스크립트 및 모듈을 테스트할 수 있는 그래픽 호스트 응용 프로그램입니다. IntelliSense와 같은 주요 기능 Show-command, 조각, 탭 완성, 구문 색 지정, 시각적 디버깅 및 풍부한 스크립팅 환경을 제공 하는 상황에 맞는 도움말입니다.

합니다 **PowerShell_ISE.exe** 도구는 Windows PowerShell ISE 세션을 시작 합니다. 사용 하는 경우 **PowerShell_ISE.exe**, Windows PowerShell ISE에서 파일을 열려면 또는 프로필이 없는 또는 다중 스레드 아파트를 사용 하 여 Windows PowerShell ISE 세션을 시작 하는 선택적 매개 변수를 사용할 수 있습니다.

**PowerShell_ISE.exe** Windows PowerShell 2.0에서 도입 되었으며 Windows PowerShell 3.0에서 크게 확장 되었습니다.

## <a name="using-powershelliseexe"></a>PowerShell_ISE.exe를 사용 하 여

사용할 수 있습니다 **PowerShell_ISE.exe** 시작 하 고 다음과 같이 Windows PowerShell 세션을 종료 합니다.
-   시작 메뉴 또는 Windows PowerShell에서 명령 프롬프트 창에서 Windows PowerShell ISE 세션을 시작 하려면 다음을 입력 합니다.  
    ```
    PowerShell_Ise
    ```  
-   Windows PowerShell ISE에서 스크립트 (.ps1), 스크립트 모듈 (.psm1), 모듈 매니페스트 (.psd1), XML 파일 또는 다른 지원 되는 파일을 열고 다음 명령 형식을 사용 합니다.  
    ```
    PowerShell_Ise <FilePath>
    ```  
    Windows PowerShell 3.0에서 사용할 수는 선택적 **파일** 다음과 같은 매개 변수:  
    ```
    PowerShell_Ise -File <FilePath>
    ```  
-   Windows PowerShell 프로필 없이 Windows PowerShell ISE 세션을 시작 하려면 사용 합니다 **NoProfile** 매개 변수입니다. (합니다 **NoProfile** 매개 변수는 Windows PowerShell 3.0에서 도입 되었습니다.)  
    ```
    PowerShell_Ise -NoProfile
    ```  
-   보려는 합니다 **PowerShell_ISE.exe** 명령 프롬프트 창에서 파일을 다음 명령 형식을 사용 하 여 도움말:  
    ```
    PowerShell_Ise -help, -?, /?
    ```  
전체 목록은 합니다 **PowerShell_ISE.exe** 명령줄 매개 변수를 참조 하십시오 [about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512)합니다.

## <a name="start-windows-powershell-ise-in-other-ways"></a>다른 방법으로 Windows PowerShell ISE를 시작 합니다.

Windows PowerShell ISE를 시작 하는 다른 방법에 대 한 정보를 참조 하세요 [Windows PowerShell 시작](https://go.microsoft.com/fwlink/?LinkID=135259)합니다.

## <a name="remarks"></a>설명

Windows Server 운영 체제의 Server Core 설치 옵션에서 Windows PowerShell 실행 됩니다. 그러나 Windows PowerShell ISE는 그래픽 사용자 인터페이스를 필요로 하므로 Server Core 설치에서 실행 되지 않습니다.

## <a name="additional-references"></a>추가 참조

[about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512)
[about_PowerShell.exe](https://go.microsoft.com/fwlink/?LinkID=113439)
[Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
[Windows를 사용 하 여 스크립팅 PowerShell](https://technet.microsoft.com/scriptcenter/dd742419) 참고