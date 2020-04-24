---
title: Nano 서버 문제 해결
description: 복구 콘솔, 응급 관리 서비스, 커널 디버깅
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.topic: article
ms.assetid: e427c66f-9571-4b8c-b65d-e7370d91544d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: f134680792eda33343bb6743708b37cf4f9e5faa
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826456"
---
# <a name="troubleshooting-nano-server"></a>Nano 서버 문제 해결

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

이 항목에는 Nano 서버 설치를 연결, 진단 및 복구하는 데 사용할 수 있는 도구에 대한 정보가 포함됩니다.  
  
## <a name="using-the-nano-server-recovery-console"></a>Nano 서버 복구 콘솔 사용 
 
Nano 서버에는 네트워크가 잘못 구성되어 Nano 서버로의 연결을 방해해도 Nano 서버에 액세스할 수 있도록 해주는 복구 콘솔이 포함됩니다. 복구 콘솔을 사용하여 네트워크를 수정한 후 일반적인 원격 관리 도구를 사용할 수 있습니다.  
  
모니터와 키보드가 연결된 가상 머신 또는 물리적 컴퓨터에서 Nano 서버를 부팅하면 전체 화면으로 텍스트 모드 로그온 프롬프트가 표시됩니다. 관리자 계정으로 이 프롬프트에 로그인하면 Nano 서버의 컴퓨터 이름 및 IP 주소가 표시됩니다. 이러한 명령을 사용하여 이 콘솔에서 탐색할 수 있습니다.  
  
-   화살표 키를 사용하여 스크롤  
  
-   탭 키를 사용하여 **>** (으)로 시작하는 텍스트로 이동한 후 Enter 키를 눌러 선택합니다.  
  
-   한 화면 또는 페이지로 뒤로 돌아가려면 ESC 키를 누릅니다. 홈 페이지에 있는 경우 ESC 키를 누르면 로그오프됩니다.  
  
-   일부 화면에는 화면의 마지막 줄에 추가 기능이 표시됩니다. 예를 들어 네트워크 어댑터를 살펴보는 경우 F4 키는 네트워크 어댑터를 비활성화합니다.  
  
복구 콘솔을 통해 방화벽 규칙은 물론 네트워크 어댑터 및 TCP/IP 설정을 보고 구성할 수 있습니다.
> [!NOTE]
> 복구 콘솔은 기본적인 키보드 기능만 지원합니다. 키보드 표시등, 10-키 섹션, 키보드 레이아웃 전환(예: caps lock 및 number lock)은 지원되지 않습니다. 영어 키보드 및 문자 집합만 지원됩니다.

## <a name="accessing-nano-server-over-a-serial-port-with-emergency-management-services"></a>응급 관리 서비스로 직렬 포트를 통해 Nano 서버 액세스  
EMS(응급 관리 서비스)를 사용하면 직렬 포트를 통한 터미널 에뮬레이터로 기본적인 문제 해결을 수행하고 네트워크 상태를 가져오며 콘솔 세션(CMD/PowerShell 포함)을 열 수 있습니다. 따라서 서버 문제를 해결하는 데 키보드 및 모니터가 필요하지 않습니다. EMS에 대한 자세한 내용은 [응급 관리 서비스 기술 참조](https://technet.microsoft.com/library/cc784411(v=ws.10).aspx)를 참조하세요.

Nano 서버 이미지에서 나중에 필요할 때 준비되도록 EMS를 사용하도록 설정하려면 이 cmdlet을 실행합니다.  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\EnablingEMS.vhdx   -EnableEMS   -EMSPort 3   -EMSBaudRate 9600`  
  
이 예에 있는 cmdlet은 9600bps 전송 속도로 직렬 포트 3에서 EMS를 사용하도록 설정합니다. 이러한 매개 변수를 포함하지 않으면 기본값은 포트 1 및 115200bps입니다. VHDX 미디어에 대해 이 cmdlet을 사용하려면 Hyper-V 기능 및 해당 Windows PowerShell 모듈을 포함해야 합니다.

## <a name="kernel-debugging"></a>커널 디버깅  
다양한 방법으로 커널 디버깅을 지원하도록 Nano 서버 이미지를 구성할 수 있습니다. VHDX 이미지로 커널 디버깅을 사용하려면 Hyper-V 기능 및 해당 Windows PowerShell 모듈을 포함해야 합니다. 일반적인 원격 커널 디버깅에 대한 자세한 내용은 [네트워크 케이블을 통해 커널 모드 디버깅 수동 설정](https://msdn.microsoft.com/library/windows/hardware/hh439346%28v=vs.85%29.aspx) 및 [WinDbg를 사용하는 원격 디버깅](https://msdn.microsoft.com/library/windows/hardware/hh451173%28v=vs.85%29.aspx)을 참조하세요.  
  
### <a name="debugging-using-a-serial-port"></a>직렬 포트를 사용하여 디버깅  
이 예의 cmdlet으로는 직렬 포트를 사용하여 이미지를 디버깅할 수 있습니다.  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingSerial   -DebugMethod Serial   -DebugCOMPort 1   -DebugBaudRate 9600`  
  
이 예에서는 9600bps 전송 속도로 포트 2를 통해 직렬 디버깅을 사용하도록 설정합니다. 이러한 매개 변수를 지정하지 않으면 기본값은 포트 2 및 115200bps입니다. EMS 및 커널 디버깅을 모두 사용하려면 두 가지 별도의 직렬 포트를 사용하도록 구성해야 합니다.  
  
### <a name="debugging-over-a-tcpip-network"></a>TCP/IP 네트워크를 통한 디버깅  
이 예의 cmdlet을 사용하여 TCP/IP 네트워크를 통해 이미지를 디버깅할 수 있습니다.  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000`  
  
이 cmdlet을 통해 IP 주소가 192.168.1.100인 컴퓨터만 연결이 허용되고 모두 포트 64000을 통해 통신하도록 커널 디버깅을 사용할 수 있습니다. -DebugRemoteIP 및 -DebugPort 매개 변수는 필수이며 포트 번호는 49152보다 큽니다. 이 cmdlet은 포트를 통해 통신하는 데 필요한 결과 VHD와 함께 파일에 암호화 키를 생성합니다. 또는 다음 예와 같이 -DebugKey 매개 변수로 고유한 키를 지정할 수 있습니다.  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000   -DebugKey 1.2.3.4`  
  
### <a name="debugging-using-the-ieee1394-protocol-firewire"></a>IEEE1394 프로토콜을 사용하여 디버깅(Firewire)  
IEEE1394를 통해 디버깅을 사용하도록 설정하려면 다음 예의 cmdlet을 사용하세요.  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingFireWire   -DebugMethod 1394   -DebugChannel 3`  
  
-DebugChannel 매개 변수는 필수 항목입니다.  
  
### <a name="debugging-using-usb"></a>USB를 사용하여 디버깅  
이 cmdlet으로 USB를 통해 디버깅을 사용하도록 설정할 수 있습니다.  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingUSB   -DebugMethod USB   -DebugTargetName KernelDebuggingUSBNano`  
  
원격 디버거를 결과 Nano 서버에 연결하는 경우 -DebugTargetName 매개 변수에 설정된 대로 대상 이름을 지정합니다.    