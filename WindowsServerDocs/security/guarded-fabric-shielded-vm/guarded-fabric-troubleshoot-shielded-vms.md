---
title: 차폐 Vm 문제 해결
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 10/3/2018
ms.openlocfilehash: c80663256a2e3404666b739c0a81cd06ec3caced
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856376"
---
# <a name="troubleshoot-shielded-vms"></a>차폐 Vm 문제 해결

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

Windows Server 버전 1803부터 VMConnect (가상 컴퓨터 연결) 고급 세션 모드 및 PS Direct는 완전히 보호 된 Vm에 대해 다시 사용 하도록 설정 됩니다. 가상화 관리자는 vm에 대 한 액세스 권한을 얻기 위해 VM 게스트 자격 증명이 필요 하지만,이를 통해 호스팅 서비스 공급자는 네트워크 구성이 끊어질 때 보호 된 VM의 문제를 더 쉽게 해결할 수 있습니다.

보호 된 Vm에 대해 VMConnect 및 PS Direct를 사용 하도록 설정 하려면 Windows Server 버전 1803 이상을 실행 하는 Hyper-v 호스트로 이동 하면 됩니다. 이러한 기능을 허용 하는 가상 장치는 자동으로 다시 사용 하도록 설정 됩니다. 보호 된 VM이 이전 버전의 Windows Server를 실행 하는 호스트로 이동 하는 경우 VMConnect 및 PS Direct는 다시 사용 하지 않도록 설정 됩니다.

호스팅 서비스 공급자이 VM에 대 한 액세스 권한을 보유 하 고 있는지 걱정 하는 보안이 중요 한 고객의 경우 게스트 OS에서 다음 기능을 사용 하지 않도록 설정 해야 합니다.

- VM에서 PowerShell Direct service를 사용 하지 않도록 설정 합니다.

  ```powershell
  Stop-Service vmicvmsession
  Set-Service vmicvmsession -StartupType Disabled
  ```

- 게스트 OS가 Windows Server 2019 또는 Windows 10 버전 1809 이상인 경우에만 VMConnect 고급 세션 모드를 사용 하지 않도록 설정할 수 있습니다. VMConnect 고급 세션 콘솔 연결을 사용 하지 않도록 설정 하려면 VM에 다음 레지스트리 키를 추가 합니다.

  ```
  reg add "HKLM\Software\Microsoft\Virtual Machine\Guest" /v DisableEnhancedSessionConsoleConnection /t REG_DWORD /d 1
  ```
