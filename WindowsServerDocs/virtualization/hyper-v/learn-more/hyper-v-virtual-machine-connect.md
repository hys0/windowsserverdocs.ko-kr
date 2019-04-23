---
title: Hyper-v 가상 컴퓨터 연결
description: 가상 컴퓨터에 대 한 원격 액세스를 제공 하는 가상 머신 연결에 설명 합니다. 가상 컴퓨터에 송신 Ctrl-Alt-삭제와 같은 일반적인 작업을 수행 하는 방법에 대 한 세부 정보를 포함 합니다.
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
ms.openlocfilehash: e1f3260fdbbd82a97c3b0949936afc6a04ec5e5a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887844"
---
# <a name="hyper-v-virtual-machine-connection"></a>Hyper-v 가상 컴퓨터 연결

>적용 대상: Windows Server 2016, Windows 10, Windows 8.1, Windows Server 2012 R2, Windows Server 2012, Windows 8

가상 컴퓨터 연결 \(VMConnect\) 설치 하거나 가상 컴퓨터에서 게스트 운영 체제와 상호 작용할 수 있도록 가상 컴퓨터에 연결 하는 데 사용할 수 있는 도구입니다. VMConnect를 사용 하 여 수행할 수 있는 작업 중 일부는 다음과 같습니다.  
  
-   시작 하 고 가상 컴퓨터 종료  
  
-   DVD 이미지에 연결 \(.iso 파일\) 또는 USB 플래시 드라이브  
  
-   검사점 만들기  
  
-   가상 컴퓨터의 설정 수정  
    
## <a name="tips-for-using-vmconnect"></a>VMConnect를 사용 하기 위한 팁  
VMConnect를 사용 하 여에 대 한 다음 정보를 유용할 수 있습니다.  
  
|이 작업을 수행 하는 중...|이 작업을 수행 하는 중...|  
|---------------|------------|  
|마우스 클릭 또는 가상 컴퓨터에 키보드 입력을 보내기|가상 머신 창에서 아무 곳 이나 클릭 합니다. 마우스 포인터를 실행 중인 가상 컴퓨터에 연결할 때 작은 점으로 나타날 수 있습니다.|  
|마우스 클릭 또는 키보드 입력이 물리적 컴퓨터를 반환 합니다.|CTRL 키를 누르고\+ALT\+가상 머신 창 외부에서 왼쪽 화살표 및로 마우스 포인터를 이동 합니다. 이 마우스 릴리스 키 조합을 Hyper에서 변경할 수 있습니다\-Hyper V 설정을\-V 관리자입니다.|  
|CTRL 보낼\+ALT\+가상 컴퓨터에 키 조합 삭제|선택 **동작** > **Ctrl\+Alt\+삭제** CTRL 키 조합을 사용 하거나\+ALT\+종료 합니다.|  
|전체 창 모드에서 전환\-화면 모드|선택 **뷰** > **전체 화면 모드**합니다. 창 모드로 다시 전환 하려면 CTRL 키를 누르고\+ALT\+중단 합니다.|  
|문제 해결에 대 한 컴퓨터의 현재 상태를 캡처하기 위해 검사점 만들기|선택 **동작** > **검사점** CTRL 키 조합을 사용 하 여 또는\+명사.|  
|가상 컴퓨터의 설정 변경|선택 **파일** > **설정을**합니다.|  
|DVD 이미지에 연결 \(.iso 파일도\) 또는 가상 플로피 디스크 \(.vfd 파일\)|선택 **미디어**합니다.<br /><br />가상 플로피 디스크가 2 세대 가상 컴퓨터에 대 한 지원 되지 않습니다. 자세한 내용은 [Hyper-v에 1 또는 2 세대 가상 컴퓨터를 만들 해야?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)합니다.|  
|호스트의 로컬 리소스를 사용 하 여 하이퍼에서\-V 가상 머신에서 USB 플래시 드라이브와 같은|Hyper-v 호스트에서 고급 세션 모드를 켜고 VMConnect를 사용 하 여 가상 컴퓨터에 연결할 연결 하기 전에 사용 하려는 로컬 리소스를 선택 합니다. 특정 단계를 참조 하세요 [하이퍼에서 로컬 리소스를 사용\-VMConnect 사용 하 여 V 가상 머신에서](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)합니다.|  
|저장 된 가상 컴퓨터에 대해 VMConnect 설정 변경|Windows PowerShell 또는 명령 프롬프트에서 다음 명령을 실행 합니다.<br /><br />`VMConnect.exe <ServerName> <VMName> \/edit`|  
|VMConnect 사용자 다른 사용자의 VMConnect 세션 장악 하지 못하도록 방지|[Hyper-v 호스트에서 고급 세션 모드 켜기](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#BKMK_OVER)합니다.<br /><br />고급 세션 모드 켜져 필요 하지는 보안 및 개인 정보 위험이 따를 수 있습니다. 사용자 연결 되어에 로그온 하는 경우 VMConnect와 다른 권한 있는 사용자를 통해 가상 머신을 동일한 가상 컴퓨터에 연결, 세션 두 번째 사용자를 통해 수행 될 및 첫 번째 사용자 세션이 손실 됩니다. 두 번째 사용자는 첫 번째 사용자의 바탕 화면, 문서 및 응용 프로그램을 볼 수 있게 됩니다.|
|Integration services 또는 VM을 Hyper-v 호스트와 통신을 허용 하는 구성 요소를 관리 합니다.| Windows 10 또는 Windows Server 2016을 실행 하는 Hyper-v 호스트에서는 VMConnect 사용 하 여 통합 서비스를 관리할 수 없습니다. 이러한 항목을 참조 하세요. <br />- [켜기/Hyper-v 호스트에서 통합 서비스 사용 안 함](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics) <br />- [켜기/Windows 가상 머신에서 통합 서비스 사용 안 함](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-windows)<br />- [켜기/Linux 가상 머신에서 통합 서비스 사용 안 함](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#manage-integration-services-from-guest-os-linux) <br />- [가상 컴퓨터에 대 한 업데이트 된 통합 서비스 유지](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/managing_ics#integration-service-maintenance)  <br />Windows Server 2012 또는 Windows Server 2012 R2를 실행 하는 호스트를 참조 하세요 [Integration Services](https://technet.microsoft.com/library/dn798297(v=ws.11).aspx)합니다.|
|VMConnect 창 크기 조정|Windows 운영 체제를 실행 하는 2 세대 가상 컴퓨터에 대 한 VMConnect 창 크기를 변경할 수 있습니다. 이렇게 하려면 Hyper-v 호스트에서 고급 세션 모드를 설정 해야 합니다. 자세한 내용은 [Hyper-v 호스트에서 고급 세션 모드 켜기](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md#BKMK_OVER)합니다. Ubuntu를 실행 하는 가상 컴퓨터에 대 한 참조 [Hyper-v VM에서 Ubuntu 화면 해상도 변경](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)합니다.|


## <a name="keyboard-shortcuts"></a>바로 가기 키  
기본적으로 키보드 입력 및 마우스 클릭이 가상 컴퓨터에 전송 됩니다. CTRL + ALT + 왼쪽 해야 하므로 다음 바로 가기 키를 사용 하기 전에 화살표입니다. 

|키 조합|설명|  
|-------------------|---------------|  
|CTRL\+ALT\+왼쪽된 화살표|마우스 릴리스|  
|CTRL\+ALT\+끝|CTRL 해당\+ALT\+가상 머신에서 삭제|  
|CTRL\+ALT\+BREAK|전체에서 전환\-창 모드를 다시 화면 모드|  
|CTRL\+O|가상 컴퓨터에 대 한 설정을 엽니다.|  
|CTRL\+S|가상 컴퓨터를 시작합니다.|  
|CTRL\+N|검사점 만들기|  
|CTRL\+E|검사점으로 되돌리려면|  
|CTRL\+C|화면 캡처를 수행 합니다.|  

## <a name="see-also"></a>관련 항목  
-   [VMConnect 사용 하 여 Hyper-v 가상 머신에서 로컬 리소스 사용](Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)  
-   [Windows Server 2016의 Hyper-v](../Hyper-V-on-Windows-Server.md)  
-   [Windows 10의 Hyper-v](https://msdn.microsoft.com/virtualization/hyperv_on_windows/windows_welcome)  
  
  
