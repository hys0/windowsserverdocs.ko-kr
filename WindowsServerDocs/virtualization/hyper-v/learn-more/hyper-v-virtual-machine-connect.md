---
title: Hyper-V Virtual Machine 연결
description: 가상 머신에 대한 원격 액세스를 제공하는 Virtual Machine 연결에 대해 설명합니다. 일반 작업을 수행하는 방법에 대한 세부 정보를 포함합니다. 예를 들어, 가상 머신에 Ctrl-Alt-Delete를 보냅니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: deae35b9-7647-42b8-b6bf-45645a44c9c4
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 8de3fe607eb9dc0d140fe9f494991cb917b8994f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854016"
---
# <a name="hyper-v-virtual-machine-connection"></a>Hyper-V Virtual Machine 연결

>적용 대상: Windows Server 2016, Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2012, Windows 8

Virtual Machine 연결 \(VMConnect\)는 가상 머신에서 게스트 운영 체제를 설치하거나 이와 상호 작용할 수 있도록 가상 머신에 연결하는 데 사용하는 도구입니다. 다음은 VMConnect를 사용하여 수행할 수 있는 작업입니다.  
  
-   가상 머신 시작 및 종료  
  
-   DVD 이미지\(.iso 파일\) 또는 USB 플래시 드라이브에 연결  
  
-   검사점 만들기  
  
-   가상 컴퓨터의 설정 수정  
    
## <a name="tips-for-using-vmconnect"></a>VMConnect 사용에 대한 팁  
VMConnect 사용에 도움이 되는 다음 정보를 찾을 수 있습니다.  
  
|수행할 작업|수행해야 하는 작업|  
|---------------|------------|  
|마우스 클릭 또는 키보드 입력을 가상 머신으로 전송|가상 머신 창에서 아무 곳이나 클릭합니다. 실행 중인 가상 머신에 연결할 때 마우스 포인터가 작은 점으로 표시될 수 있습니다.|  
|마우스 클릭 또는 키보드 입력을 물리적 컴퓨터에 반환|CTRL\+ALT\+왼쪽 화살표를 누른 다음, 마우스 포인터를 가상 머신 창 외부로 이동합니다. 이 마우스 릴리스 키 조합은 Hyper\-V 관리자의 Hyper\-V 설정에서 변경할 수 있습니다.|  
|CTRL\+ALT\+DELETE 키 조합을 가상 머신으로 전송|**작업** > **Ctrl\+Alt\+Delete**를 선택하거나 키 조합 CTRL\+ALT\+END를 사용합니다.|  
|창 모드에서 전체\-화면 모드로 전환|**보기** > **전체 화면 모드**를 선택합니다. 창 모드로 다시 전환하려면 CTRL\+ALT\+BREAK을 누릅니다.|  
|문제 해결을 위해 머신의 현재 상태를 캡처하는 검사점 만들기|**작업** > **검사점**을 선택하거나 키 조합을 CTRL\+N을 사용합니다.|  
|가상 머신의 설정 변경|**파일** > **설정**을 선택합니다.|  
|DVD 이미지\(.iso 파일\) 또는 가상 플로피 디스크\(.vfd 파일\)에 연결|**미디어**를 선택합니다.<p>가상 플로피 디스크는 2세대 가상 머신에서 지원되지 않습니다. 자세한 내용은 [Hyper-V에 1세대 또는 2세대 가상 머신을 만들어야 하나요?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)를 참조하세요.|  
|Hyper\-V 가상 머신에서 호스트의 로컬 리소스 사용(예: USB 플래시 드라이브)|Hyper-V 호스트에서 고급 세션 모드를 켜고 VMConnect를 사용하여 가상 머신에 연결합니다. 연결하기 전에 사용할 로컬 리소스를 선택합니다. 특정 단계는 [VMConnect를 사용하여 Hyper\-V 가상 머신에서 로컬 리소스 사용](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)을 참조하세요.|  
|가상 머신에 대한 저장된 VMConnect 설정 변경|Windows PowerShell 또는 명령 프롬프트에서 다음 명령을 실행합니다.<p>`VMConnect.exe <ServerName> <VMName> /edit`|  
|VMConnect 사용자가 다른 사용자의 VMConnect 세션을 수행하지 못하도록 방지|[Hyper-V 호스트에서 고급 세션 모드를 켭니다](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host).<p>고급 세션 모드를 켜지 않으면 보안 및 프라이버시 위험에 노출될 수 있습니다. 사용자가 VMConnect를 통해 가상 머신에 연결되어 로그온되어 있는데 다른 권한 있는 사용자가 동일한 가상 머신에 연결한 경우 해당 세션은 두 번째 사용자에 의해 수행되고 첫 번째 사용자는 세션을 잃게 됩니다. 두 번째 사용자가 첫 번째 사용자의 데스크톱, 문서 및 애플리케이션을 볼 수 있습니다.|
|VM이 Hyper-V 호스트와 통신할 수 있도록 하는 통합 서비스 또는 구성 요소 관리| Windows 10 또는 Windows Server 2016을 실행하는 Hyper-V 호스트에서는 VMConnect를 사용하여 통합 서비스를 관리할 수 없습니다. 다음 항목을 참조하세요. <br />- [Hyper-V 호스트에서 통합 서비스 켜기/끄기](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [Windows 가상 머신에서 통합 서비스 켜기/끄기](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [Linux 가상 머신에서 통합 서비스 켜기/끄기](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [가상 머신에서 통합 서비스를 업데이트된 상태로 유지](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Windows Server 2012 또는 Windows Server 2012 R2를 실행하는 호스트의 경우 [통합 서비스](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx)를 참조하세요.|
|VMConnect 창 크기 조정|Windows 운영 체제를 실행하는 2세대 가상 머신에 대한 VMConnect 창의 크기를 변경할 수 있습니다. 이렇게 하려면 Hyper-V 호스트에서 고급 세션 모드를 켜야 합니다. 자세한 내용은 [Hyper-V 호스트에서 고급 세션 모드 켜기](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host)를 참조하세요. Ubuntu를 실행 하는 가상 컴퓨터에 대 한 참조 [Hyper-v VM에서 Ubuntu 화면 해상도 변경](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)합니다.|


## <a name="keyboard-shortcuts"></a>바로 가기 키  
기본적으로 키보드 입력 및 마우스 클릭은 가상 머신으로 전송됩니다. 따라서 다음 바로 가기 키를 사용하기 전에 CTRL + ALT + 왼쪽 화살표를 눌러야 할 수 있습니다. 

|키 조합|설명|  
|-------------------|---------------|  
|CTRL\+ALT\+왼쪽 화살표|마우스 릴리스|  
|CTRL\+ALT\+END|가상 머신에서 CTRL\+ALT\+DELETE와 동일|  
|CTRL\+ALT\+BREAK|전체\-화면 모드에서 창 모드로 다시 전환|  
|CTRL\+O|가상 머신에 대한 설정 열기|  
|CTRL\+S|가상 머신 시작|  
|CTRL\+N|검사점 만들기|  
|CTRL\+E|검사점 되돌리기|  
|CTRL\+C|화면 캡처 실행|  

## <a name="see-also"></a>참고 항목  
-   [VMConnect를 사용하여 Hyper-V 가상 머신에서 로컬 리소스 사용](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Windows Server 2016에서의 Hyper-V](../Hyper-V-on-Windows-Server.md)  
-   [Windows 10에서의 Hyper-V](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
