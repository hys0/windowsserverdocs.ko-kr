---
title: Hyper-v 가상 컴퓨터 연결
description: 가상 컴퓨터에 대 한 원격 액세스를 제공 하는 가상 컴퓨터 연결에 대해 설명 합니다. 일반 작업을 수행 하는 방법에 대 한 세부 정보를 포함 합니다. 예를 들어, 가상 컴퓨터에 Ctrl + Alt-Delete를 보냅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: deae35b9-7647-42b8-b6bf-45645a44c9c4
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 04f3bc581a0065c62ba8878473e45f714ce8a069
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872113"
---
# <a name="hyper-v-virtual-machine-connection"></a>Hyper-v 가상 컴퓨터 연결

>적용 대상: Windows Server 2016, Windows 10, Windows 8.1, Windows Server 2012 R2, windows Server 2012, Windows 8

가상 컴퓨터 연결 \(VMConnect\) 는 가상 컴퓨터에 연결 하는 데 사용 하는 도구입니다 .이 도구를 사용 하 여 가상 컴퓨터에서 게스트 운영 체제를 설치 하거나 조작할 수 있습니다. VMConnect를 사용 하 여 수행할 수 있는 작업에는 다음이 포함 됩니다.  
  
-   가상 컴퓨터 시작 및 종료  
  
-   DVD 이미지 \(.iso 파일\) 또는 USB 플래시 드라이브에 연결  
  
-   검사점 만들기  
  
-   가상 컴퓨터의 설정 수정  
    
## <a name="tips-for-using-vmconnect"></a>VMConnect 사용에 대 한 팁  
VMConnect 사용에 도움이 되는 다음 정보를 찾을 수 있습니다.  
  
|이 작업을 수행 하는 중...|수행할 작업|  
|---------------|------------|  
|마우스 클릭 또는 키보드 입력을 가상 머신으로 보내기|가상 컴퓨터 창에서 아무 곳 이나 클릭 합니다. 마우스 포인터는 실행 중인 가상 컴퓨터에 연결할 때 작은 점으로 표시 될 수 있습니다.|  
|물리적 컴퓨터에 마우스 클릭 또는 키보드 입력 반환|Ctrl\+ALT\+왼쪽 화살표를 누르고 마우스 포인터를 가상 머신 창 외부로 이동 합니다. 이 마우스 릴리스 키 조합은 hyper-v 관리자\-\-의 hyper-v 설정에서 변경할 수 있습니다.|  
|가상 컴퓨터\+에\+CTRL ALT DELETE 키 조합을 보냅니다.|\+\+ **작업** > **ctrlalt\+Delete를 선택 하거나 키 조합 ctrl alt END를 사용 합니다.\+**|  
|창 모드에서 전체\-화면 모드로 전환|**전체 화면 모드** **보기** > 를 선택 합니다. 창 모드로 다시 전환 하려면 ctrl\+ALT\+BREAK를 누릅니다.|  
|문제 해결을 위해 컴퓨터의 현재 상태를 캡처하는 검사점 만들기|\+ **작업** > **검사점** 을 선택 하거나 CTRL N 키 조합을 사용 합니다.|  
|가상 컴퓨터의 설정 변경|**파일** > **설정**을 선택 합니다.|  
|DVD 이미지 \(.iso 파일\) 또는 가상 플로피 디스크 \(vfd 파일에 연결 합니다.\)|**미디어**를 선택 합니다.<br /><br />가상 플로피 디스크는 2 세대 가상 컴퓨터에 대해 지원 되지 않습니다. 자세한 내용은 [hyper-v에서 1 세대 또는 2 세대 가상 머신을 만들어야 하나요?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)를 참조 하세요.|  
|Hyper-v\-가상 컴퓨터 (예: USB 플래시 드라이브)에서 호스트의 로컬 리소스 사용|Hyper-v 호스트에서 고급 세션 모드를 설정 하 고, VMConnect를 사용 하 여 가상 머신에 연결 하 고, 연결 하기 전에 사용 하려는 로컬 리소스를 선택 합니다. 특정 단계는 [VMConnect를 사용 하 여 hyper-v\-가상 머신에서 로컬 리소스 사용](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)을 참조 하세요.|  
|가상 컴퓨터에 대 한 저장 된 VMConnect 설정 변경|Windows PowerShell 또는 명령 프롬프트에서 다음 명령을 실행 합니다.<br /><br />`VMConnect.exe <ServerName> <VMName> \/edit`|  
|VMConnect 사용자가 다른 사용자의 VMConnect 세션을 수행 하지 못하도록 방지|[Hyper-v 호스트에서 고급 세션 모드를 켭니다](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host).<br /><br />고급 세션 모드를 설정 하지 않으면 보안 및 개인 정보 위험에 노출 될 수 있습니다. 사용자가 VMConnect을 통해 가상 컴퓨터에 연결 되어 로그온 하 고 다른 권한 있는 사용자가 동일한 가상 컴퓨터에 연결 하는 경우 해당 세션은 두 번째 사용자에 의해 수행 되 고 첫 번째 사용자는 세션을 잃게 됩니다. 두 번째 사용자가 첫 번째 사용자의 데스크톱, 문서 및 응용 프로그램을 볼 수 있습니다.|
|VM이 Hyper-v 호스트와 통신할 수 있도록 하는 통합 서비스 또는 구성 요소를 관리 합니다.| Windows 10 또는 Windows Server 2016를 실행 하는 Hyper-v 호스트에서는 VMConnect를 사용 하 여 통합 서비스를 관리할 수 없습니다. 다음 항목을 참조 하세요. <br />- [Hyper-v 호스트에서 integration services 설정/해제](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [Windows 가상 머신에서 integration services 설정/해제](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [Linux 가상 머신에서 integration services 설정/해제](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [가상 컴퓨터에 대해 integration services를 업데이트 된 상태로 유지](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Windows Server 2012 또는 Windows Server 2012 r 2를 실행 하는 호스트의 경우 [Integration Services](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx)를 참조 하세요.|
|VMConnect 창 크기 조정|Windows 운영 체제를 실행 하는 2 세대 가상 컴퓨터에 대 한 VMConnect 창의 크기를 변경할 수 있습니다. 이렇게 하려면 Hyper-v 호스트에서 고급 세션 모드를 설정 해야 할 수 있습니다. 자세한 내용은 [hyper-v 호스트에서 고급 세션 모드 설정](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#turn-on-enhanced-session-mode-on-a-hyper-v-host)을 참조 하세요. Ubuntu를 실행 하는 가상 컴퓨터에 대 한 참조 [Hyper-v VM에서 Ubuntu 화면 해상도 변경](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)합니다.|


## <a name="keyboard-shortcuts"></a>바로 가기 키  
기본적으로 키보드 입력 및 마우스 클릭은 가상 컴퓨터로 전송 됩니다. 따라서 다음 바로 가기 키를 사용 하기 전에 CTRL + ALT + 왼쪽 화살표를 눌러야 할 수 있습니다. 

|키 조합|설명|  
|-------------------|---------------|  
|CTRL\+ALT\+왼쪽 화살표|마우스 릴리스|  
|CTRL\+ALT\+END|가상 컴퓨터의\+CTRL\+ALT DELETE에 해당 합니다.|  
|CTRL\+ALT\+구분선|전체\-화면 모드에서 창 모드로 다시 전환|  
|CTRL\+O|가상 컴퓨터에 대 한 설정을 엽니다.|  
|CTRL\+S|가상 컴퓨터를 시작 합니다.|  
|CTRL\+N|검사점 만들기|  
|CTRL\+E|검사점으로 되돌리기|  
|CTRL\+C|화면 캡처 수행|  

## <a name="see-also"></a>관련 항목  
-   [VMConnect를 사용 하 여 Hyper-v 가상 머신에서 로컬 리소스 사용](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Windows Server 2016의 hyper-v](../Hyper-V-on-Windows-Server.md)  
-   [Windows 10의 hyper-v](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
