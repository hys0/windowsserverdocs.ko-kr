---
title: PowerShell_ise
description: Windows PowerShell ISE (통합 스크립팅 환경) 세션을 시작 하는 PowerShell_ise 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3f983ea5b8464748d86264108a2ee8660ca0e3f2
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926051"
---
# <a name="powershell_ise"></a>PowerShell_ise

Windows PowerShell ISE (통합 스크립팅 환경)는 그래픽 지원 환경에서 스크립트 및 모듈을 읽고, 쓰고, 실행 하 고, 디버그 하 고, 테스트할 수 있는 그래픽 호스트 응용 프로그램입니다. IntelliSense, 표시 명령, 코드 조각, 탭 완성, 구문 색 지정, 시각적 디버깅 및 상황에 맞는 도움말과 같은 주요 기능을 통해 풍부한 스크립팅 환경을 제공 합니다.

## <a name="using-powershellexe"></a>PowerShell.exe 사용

**PowerShell_ISE.exe** 도구는 Windows PowerShell ISE 세션을 시작 합니다. **PowerShell_ISE.exe**를 사용 하는 경우 선택적 매개 변수를 사용 하 여 Windows PowerShell ISE에서 파일을 열거나 프로필 또는 다중 스레드 아파트를 사용 하 여 Windows PowerShell ISE 세션을 시작할 수 있습니다.

- 명령 프롬프트 창에서 Windows PowerShell ISE 세션을 시작 하려면 Windows PowerShell에서 또는 **시작** 메뉴에서 다음을 입력 합니다.

  ```powershell
  PowerShell_Ise.exe
  ```

- 스크립트 (ps1), 스크립트 모듈 (.psm1), 모듈 매니페스트 (. psd1), XML 파일 또는 지원 되는 기타 Windows PowerShell ISE 파일을 열려면 다음을 입력 합니다.

  ```powershell
  PowerShell_Ise.exe <filepath>
  ```

  Windows PowerShell 3.0에서는 다음과 같이 선택적 **파일** 매개 변수를 사용할 수 있습니다.

  ```powershell
  PowerShell_Ise.exe -file <filepath>
  ```

- Windows PowerShell 프로필 없이 Windows PowerShell ISE 세션을 시작 하려면 **Noprofile** 매개 변수를 사용 합니다. **Noprofile** 매개 변수는 Windows PowerShell 3.0에 도입 되었습니다 .에는 다음을 입력 합니다.

  ```powershell
  PowerShell_Ise.exe -NoProfile
  ```

- PowerShell_ISE.exe 도움말 파일을 보려면 다음을 입력 합니다.

    ```powershell
    PowerShell_Ise.exe -help
    PowerShell_Ise.exe -?
    PowerShell_Ise.exe /?
    ```

### <a name="remarks"></a>설명

- **PowerShell_ISE.exe** 명령줄 매개 변수의 전체 목록은 [about_PowerShell_Ise.Exe](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe)를 참조 하세요.

- Windows PowerShell을 시작 하는 다른 방법에 대 한 자세한 내용은 [Windows Powershell 시작](https://docs.microsoft.com/powershell/scripting/windows-powershell/starting-windows-powershell)을 참조 하세요.

- Windows PowerShell은 Windows Server 운영 체제의 Server Core 설치 옵션에서 실행 됩니다. 그러나 Windows PowerShell ISE에는 그래픽 사용자 인터페이스가 필요 하기 때문에 Server Core 설치에서 실행 되지 않습니다.

## <a name="additional-references"></a>추가 참조

- [about_PowerShell_Ise.exe] (https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe

- [about_PowerShell.Exe](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_exe)

- [Windows PowerShell](https://docs.microsoft.com/powershell/)
