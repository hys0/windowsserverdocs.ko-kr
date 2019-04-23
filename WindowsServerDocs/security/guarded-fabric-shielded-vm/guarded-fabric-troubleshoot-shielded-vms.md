---
title: 보호 된 Vm 문제 해결
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 10/3/2018
ms.openlocfilehash: 13ff0dad1519d394ce74a91efbfcc9e2f237e4a5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850034"
---
# <a name="troubleshoot-shielded-vms"></a>보호 된 Vm 문제 해결

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

Windows Server 버전 1803 부터는 가상 머신 연결 (VMConnect) 고급 세션 모드 PS 직접와 완벽 하 게 보호 된 Vm에 대 한 다시 사용 하도록 설정 합니다. 여전히 가상화 관리자 VM 게스트 자격 증명을 VM에 액세스 하는데이 쉽게 해당 네트워크 구성이 손상 되 면 보호 된 VM 문제를 해결 하는 호스팅 서비스 공급자입니다.

VMConnect 및 PS 직접 보호 된 Vm에 대 한를 사용 하려면 단순히 1803 이상 Windows Server 버전을 실행 하는 Hyper-v 호스트를 이동 합니다. 이러한 기능에 대 한 허용 하는 가상 장치는 다시 자동으로 사용할 수 있습니다. 이전 버전의 Windows Server를 실행 하는 호스트를 이동 하는 보호 된 VM을 한 경우 VMConnect PS 직접 비활성화 됩니다 다시 합니다.

보안과 관련 된 호스팅 서비스 공급자가 VM에 대 한 액세스를 있고 원래 동작으로 되돌리려면 걱정을 고객에 대 한 게스트 OS에서에서 다음과 같은 기능을 비활성화 합니다.

- VM에서 PowerShell Direct를 사용 하지 않도록 설정 합니다.

  ```powershell
  Stop-Service vmicvmsession
  Set-Service vmicvmsession -StartupType Disabled
  ```

- 게스트 OS 이상 경우 VMConnect 고급 세션 모드를 비활성화할 수만 Windows Server 2019 또는 Windows 10 버전 1809 합니다. VMConnect 고급 세션 콘솔 연결을 사용 하지 않도록 설정 하려면 VM에서 다음 레지스트리 키를 추가 합니다.

  ```
  reg add "HKLM\Software\Microsoft\Virtual Machine\Guest" /v DisableEnhancedSessionConsoleConnection /t REG_DWORD /d 1
  ```
