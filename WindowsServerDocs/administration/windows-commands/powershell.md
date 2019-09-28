---
title: PowerShell
description: 명령 프롬프트에서 PowerShell 콘솔을 여는 방법에 대해 알아봅니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2c43c71fce9bb25efcf3f03284160d5534475a8a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372203"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell은 시스템 관리를 위해 특별히 설계 된 작업 기반 명령줄 셸 및 스크립트 언어입니다. .NET Framework를 기반으로 제작된 Windows PowerShell을 사용하면 IT 전문가와 고급 사용자가 Windows 운영 체제 및 Windows에서 실행되는 응용 프로그램의 관리를 쉽게 제어하고 자동화할 수 있습니다.

**PowerShell** 명령줄 도구는 명령 프롬프트 창에서 Windows powershell 세션을 시작 합니다. **PowerShell .exe**를 사용 하는 경우 선택적 매개 변수를 사용 하 여 세션을 사용자 지정할 수 있습니다. 예를 들어 특정 실행 정책이 나 Windows PowerShell 프로필을 제외 하는 세션을 시작할 수 있습니다. 그렇지 않으면 세션이 Windows PowerShell 콘솔에서 시작 된 세션과 동일 합니다.

## <a name="using-powershellexe"></a>PowerShell 사용

**Powershell .exe** 명령줄 도구를 사용 하 여 명령 프롬프트 창에서 Windows powershell 세션을 시작할 수 있습니다.

- 명령 프롬프트 창에서 Windows PowerShell 세션을 시작 하려면 `PowerShell`을 입력 합니다. Windows PowerShell 세션에 있음을 나타내기 위해 **PS** 접두사가 명령 프롬프트에 추가 됩니다.

- 특정 실행 정책으로 세션을 시작 하려면 **set-executionpolicy** 매개 변수를 사용 합니다.

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Windows PowerShell 프로필을 사용 하지 않고 Windows PowerShell 세션을 시작 하려면 **Noprofile** 매개 변수를 사용 합니다.

    ```
    PowerShell.exe -NoProfile
    ```
  
- 세션을 시작 하려면 **set-executionpolicy** 매개 변수를 사용 합니다.

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```
  
- PowerShell .exe 도움말 파일을 보려면 다음 명령 형식을 사용 합니다.  
    
    ```
    PowerShell.exe -help, -?, /?
    ```

- 명령 프롬프트 창에서 Windows PowerShell 세션을 종료 하려면 `exit`을 입력 합니다. 일반적인 명령 프롬프트는를 반환 합니다.

**PowerShell .exe** 명령줄 매개 변수의 전체 목록은 [about_PowerShell](https://go.microsoft.com/fwlink/?LinkID=113439)를 참조 하세요.

## <a name="other-ways-to-start-windows-powershell"></a>Windows PowerShell을 시작 하는 다른 방법

Windows PowerShell을 시작 하는 다른 방법에 대 한 자세한 내용은 [Windows Powershell 시작](https://go.microsoft.com/fwlink/?LinkID=135259)을 참조 하세요.

## <a name="remarks"></a>설명

Windows PowerShell은 Windows Server 운영 체제의 Server Core 설치 옵션에서 실행 됩니다. 그러나 [Windows POWERSHELL ISE (통합 스크립팅 환경)](https://technet.microsoft.com/library/hh849182)와 같은 그래픽 사용자 인터페이스가 필요한 기능과 [Out-GridView](https://go.microsoft.com/fwlink/?LinkID=113364) 및 [Show 명령](https://go.microsoft.com/fwlink/?LinkID=217448) cmdlet은 Server Core 설치에서 실행 되지 않습니다.

## <a name="additional-references"></a>추가 참조

[about_PowerShell](https://go.microsoft.com/fwlink/?LinkID=113439)
[about_PowerShell_Ise](https://go.microsoft.com/fwlink/?LinkId=256512)@no__t[windows powershell을 사용 하 여](https://technet.microsoft.com/scriptcenter/dd742419) windows[powershell](https://go.microsoft.com/fwlink/?LinkID=107116)@no__t 5 스크립팅 참고 항목