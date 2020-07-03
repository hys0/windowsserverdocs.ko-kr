---
title: PowerShell
description: Powershell 명령에 대 한 참조 문서. 명령 프롬프트에서 PowerShell 콘솔을 엽니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 8a252efe57cec1e77bd4d814ced75decb1f2ceb7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931377"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell은 시스템 관리를 위해 특별히 설계 된 작업 기반 명령줄 셸 및 스크립트 언어입니다. .NET Framework를 기반으로 제작된 Windows PowerShell을 사용하면 IT 전문가와 고급 사용자가 Windows 운영 체제 및 Windows에서 실행되는 애플리케이션의 관리를 쉽게 제어하고 자동화할 수 있습니다.

## <a name="using-powershellexe"></a>PowerShell.exe 사용

**PowerShell.exe** 명령줄 도구는 명령 프롬프트 창에서 Windows PowerShell 세션을 시작 합니다. **PowerShell.exe**를 사용 하는 경우 선택적 매개 변수를 사용 하 여 세션을 사용자 지정할 수 있습니다. 예를 들어 특정 실행 정책이 나 Windows PowerShell 프로필을 제외 하는 세션을 시작할 수 있습니다. 그렇지 않으면 세션이 Windows PowerShell 콘솔에서 시작 된 세션과 동일 합니다.

- 명령 프롬프트 창에서 Windows PowerShell 세션을 시작 하려면을 입력 `PowerShell` 합니다. Windows PowerShell 세션에 있음을 나타내기 위해 **PS** 접두사가 명령 프롬프트에 추가 됩니다.

- 특정 실행 정책으로 세션을 시작 하려면 **set-executionpolicy** 매개 변수를 사용 하 고 다음을 입력 합니다.

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Windows PowerShell 프로필을 사용 하지 않고 Windows PowerShell 세션을 시작 하려면 **Noprofile** 매개 변수를 사용 하 고 다음을 입력 합니다.

    ```powershell
    PowerShell.exe -NoProfile
    ```

- 세션을 시작 하려면 **set-executionpolicy** 매개 변수를 사용 하 고 다음을 입력 합니다.

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- PowerShell.exe 도움말 파일을 보려면 다음을 입력 합니다.

    ```powershell
    PowerShell.exe -help
    PowerShell.exe -?
    PowerShell.exe /?
    ```

- 명령 프롬프트 창에서 Windows PowerShell 세션을 종료 하려면를 입력 `exit` 합니다. 일반적인 명령 프롬프트는를 반환 합니다.

### <a name="remarks"></a>설명

- **PowerShell.exe** 명령줄 매개 변수의 전체 목록은 [about_PowerShell.Exe](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_exe)를 참조 하세요.

- Windows PowerShell을 시작 하는 다른 방법에 대 한 자세한 내용은 [Windows Powershell 시작](https://docs.microsoft.com/powershell/scripting/windows-powershell/starting-windows-powershell)을 참조 하세요.

- Windows PowerShell은 Windows Server 운영 체제의 Server Core 설치 옵션에서 실행 됩니다. 그러나 [Windows POWERSHELL ISE (통합 스크립팅 환경)](https://docs.microsoft.com/previous-versions//hh849182(v=technet.10))와 같은 그래픽 사용자 인터페이스가 필요한 기능 및- [GridView](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/out-gridview) 및 [표시 명령](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Utility/Show-Command) cmdlet은 Server Core 설치에서 실행 되지 않습니다.

## <a name="additional-references"></a>추가 참조

- [about_PowerShell.Exe](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_exe)

- [about_PowerShell_Ise.exe](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe)

- [Windows PowerShell](https://docs.microsoft.com/powershell/)
