---
title: PowerShell_ise
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 65d8b9e7b7952ec64cd24e8106802cf66de693c6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372193"
---
# <a name="powershell_ise"></a>PowerShell_ise



Windows PowerShell ISE (통합 스크립팅 환경)는 그래픽 지원 환경에서 스크립트 및 모듈을 읽고, 쓰고, 실행 하 고, 디버그 하 고, 테스트할 수 있는 그래픽 호스트 응용 프로그램입니다. IntelliSense, 표시 명령, 코드 조각, 탭 완성, 구문 색 지정, 시각적 디버깅 및 상황에 맞는 도움말과 같은 주요 기능을 통해 풍부한 스크립팅 환경을 제공 합니다.

**PowerShell_ISE** 도구는 Windows PowerShell ISE 세션을 시작 합니다. **PowerShell_ISE**를 사용 하는 경우 선택적 매개 변수를 사용 하 여 Windows PowerShell ISE에서 파일을 열거나 프로필 또는 다중 스레드 아파트를 사용 하 여 Windows PowerShell ISE 세션을 시작할 수 있습니다.

**PowerShell_ISE** 는 windows powershell 2.0에서 도입 되었으며 windows powershell 3.0에서 크게 확장 되었습니다.

## <a name="using-powershell_iseexe"></a>PowerShell_ISE 사용

다음과 같이 **PowerShell_ISE** 를 사용 하 여 Windows PowerShell 세션을 시작 하 고 종료할 수 있습니다.
- Windows PowerShell ISE 세션을 시작 하려면 Windows PowerShell의 명령 프롬프트 창에서 또는 시작 메뉴에서 다음을 입력 합니다.  
  ```
  PowerShell_Ise
  ```  
- 스크립트 (ps1), 스크립트 모듈 (.psm1), 모듈 매니페스트 (. psd1), XML 파일 또는 지원 되는 기타 Windows PowerShell ISE 파일을 열려면 다음 명령 형식을 사용 합니다.  
  ```
  PowerShell_Ise <FilePath>
  ```  
  Windows PowerShell 3.0에서는 다음과 같이 선택적 **파일** 매개 변수를 사용할 수 있습니다.  
  ```
  PowerShell_Ise -File <FilePath>
  ```  
- Windows PowerShell 프로필 없이 Windows PowerShell ISE 세션을 시작 하려면 **Noprofile** 매개 변수를 사용 합니다. **Noprofile** 매개 변수는 Windows PowerShell 3.0에서 도입 되었습니다.  
  ```
  PowerShell_Ise -NoProfile
  ```  
- 명령 프롬프트 창에서 **PowerShell_ISE** 도움말 파일을 보려면 다음 명령 형식을 사용 합니다.  
  ```
  PowerShell_Ise -help, -?, /?
  ```  
  **PowerShell_ISE** 명령줄 매개 변수의 전체 목록은 [about_PowerShell_Ise](https://go.microsoft.com/fwlink/?LinkId=256512)를 참조 하세요.

## <a name="start-windows-powershell-ise-in-other-ways"></a>다른 방법으로 Windows PowerShell ISE 시작

Windows PowerShell ISE를 시작 하는 다른 방법에 대 한 자세한 내용은 [Windows PowerShell 시작](https://go.microsoft.com/fwlink/?LinkID=135259)을 참조 하세요.

## <a name="remarks"></a>설명

Windows PowerShell은 Windows Server 운영 체제의 Server Core 설치 옵션에서 실행 됩니다. 그러나 Windows PowerShell ISE에는 그래픽 사용자 인터페이스가 필요 하기 때문에 Server Core 설치에서 실행 되지 않습니다.

## <a name="additional-references"></a>추가 참조

windows powershell을 사용 하는 [about_PowerShell_Ise](https://go.microsoft.com/fwlink/?LinkId=256512)
[about_PowerShell .exe](https://go.microsoft.com/fwlink/?LinkID=113439) 를 [

windows](https://go.microsoft.com/fwlink/?LinkID=107116) [powershell을 사용 하 여 스크립팅을](https://technet.microsoft.com/scriptcenter/dd742419) 참조 하세요.