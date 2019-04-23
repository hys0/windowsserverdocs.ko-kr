---
title: PowerShell
description: 명령 프롬프트에서 PowerShell 콘솔을 여는 방법을 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: c8070268fdf58fbbb71c159a7360b488222ef740
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852184"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell 작업 기반 명령줄 셸이자 스크립팅 언어 시스템 관리를 위해 특별히 설계 된 경우 .NET Framework를 기반으로 제작된 Windows PowerShell을 사용하면 IT 전문가와 고급 사용자가 Windows 운영 체제 및 Windows에서 실행되는 응용 프로그램의 관리를 쉽게 제어하고 자동화할 수 있습니다.

합니다 **PowerShell.exe** 명령줄 도구 명령 프롬프트 창에서 Windows PowerShell 세션을 시작 합니다. 사용 하는 경우 **PowerShell.exe**, 선택적 매개 변수를 사용 하 여 세션을 사용자 지정할 수 있습니다. 예를 들어 특정 실행 정책 또는 Windows PowerShell 프로필을 제외 하는 하나를 사용 하는 세션을 시작할 수 있습니다. 그렇지 않으면 세션이 Windows PowerShell 콘솔에서 시작 되는 모든 세션으로 동일 합니다.

## <a name="using-powershellexe"></a>PowerShell.exe를 사용 하 여

사용할 수는 **PowerShell.exe** 명령 프롬프트 창에서 Windows PowerShell 세션을 시작 하려면 명령줄 도구입니다.

- 명령 프롬프트 창에서 Windows PowerShell 세션을 시작 하려면 입력 `PowerShell`합니다. A **PS** 있음을 나타내는 Windows PowerShell 세션에서 명령 프롬프트에 접두사가 추가 됩니다.
- 특정 실행 정책을 사용 하 여 세션을 시작 하려면 사용 합니다 **ExecutionPolicy** 매개 변수입니다.  
    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```  
- Windows PowerShell 프로필 없이 Windows PowerShell 세션을 시작 하려면 사용 합니다 **NoProfile** 매개 변수입니다.  
    ```
    PowerShell.exe -NoProfile
    ```  
- 세션을 시작 하려면 사용 합니다 **ExecutionPolicy** 매개 변수입니다.  
    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```  
- PowerShell.exe 도움말 파일을 보려면 다음 명령 형식을 사용 합니다.  
    ```
    PowerShell.exe -help, -?, /?
    ```  
- 명령 프롬프트 창에서 Windows PowerShell 세션을 종료 하려면 입력 `exit`합니다. 일반적인 명령 프롬프트가 반환 됩니다.

전체 목록은 합니다 **PowerShell.exe** 명령줄 매개 변수를 참조 하십시오 [about_PowerShell.Exe](https://go.microsoft.com/fwlink/?LinkID=113439)합니다.

## <a name="other-ways-to-start-windows-powershell"></a>Windows PowerShell을 시작 하는 다른 방법

Windows PowerShell을 시작 하는 다른 방법에 대 한 정보를 참조 하세요 [Windows PowerShell 시작](https://go.microsoft.com/fwlink/?LinkID=135259)합니다.

## <a name="remarks"></a>설명

Windows Server 운영 체제의 Server Core 설치 옵션에서 Windows PowerShell 실행 됩니다. 그러나 기능 필요한 그래픽 사용자 인터페이스를 합니다 [Windows PowerShell 통합 스크립팅 환경 (ISE)](https://technet.microsoft.com/library/hh849182), 및 [Out-gridview](https://go.microsoft.com/fwlink/?LinkID=113364) 고 [Show-command](https://go.microsoft.com/fwlink/?LinkID=217448)cmdlet을 Server Core 설치에서 실행 되지 않습니다.

## <a name="additional-references"></a>추가 참조

[about_PowerShell.Exe](https://go.microsoft.com/fwlink/?LinkID=113439)
[about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512)
[Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
[Windows를 사용 하 여 스크립팅 PowerShell](https://technet.microsoft.com/scriptcenter/dd742419) 참고