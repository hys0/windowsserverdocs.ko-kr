---
title: VMConnect를 사용하여 Hyper-V 가상 머신에서 로컬 리소스 사용
description: VMConnect에서 로컬 리소스를 사용하기 위한 요구 사항을 설명합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: kbdazure
ms.author: kathydav
ms.date: 12/06/2016
ms.openlocfilehash: 40dd4076a4d1a57c8a1e999669e589dadeb88cbe
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "81650121"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>VMConnect를 사용하여 Hyper-V 가상 머신에서 로컬 리소스 사용

>적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2

VMConnect(Virtual Machine Connection)를 사용하면 이동식 USB 플래시 드라이브 또는 프린터와 같은 가상 머신에서 컴퓨터의 로컬 리소스를 사용할 수 있습니다. 고급 세션 모드를 사용하면 VMConnect 창의 크기를 조정할 수도 있습니다. 이 문서에서는 호스트를 구성한 다음, 가상 머신에 로컬 리소스에 대한 액세스 권한을 부여하는 방법을 설명합니다.

고급 세션 모드 및 형식 클립보드 텍스트는 최근 Windows 운영 체제를 실행하는 가상 머신에서만 사용할 수 있습니다. \(아래 [로컬 리소스 사용을 위한 요구 사항](#requirements-for-using-local-resources)을 참조하세요.\) 

Ubuntu를 실행 하는 가상 컴퓨터에 대 한 참조 [Hyper-v VM에서 Ubuntu 화면 해상도 변경](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)합니다. 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>Hyper-V 호스트에서 고급 세션 모드 켜기  
Hyper-V 호스트에서 Windows 10 또는 Windows 8.1을 실행하는 경우 고급 세션 모드가 기본적으로 켜져 있으므로 이를 건너뛰고 다음 섹션으로 이동할 수 있습니다. 그러나 호스트에서 Windows Server 2016 또는 Windows Server 2012 R2를 실행하는 경우 먼저 이 작업을 수행합니다. 
  
고급 세션 모드 켜기:

1.  가상 머신을 호스트하는 컴퓨터에 연결합니다.  
  
2.  Hyper-v 관리자에서 호스트의 컴퓨터 이름을 선택 합니다.  
  
    ![호스트 컴퓨터 이름을 보여 주는 스크린 샷 왼쪽된 창에서 Hyper-v 관리자 아래에 나열 합니다.](media/Hyper-V-HyperVManager-HostNameSelected.png)  
  
3.  **Hyper-V 설정**을 선택합니다.  
  
    ![오른쪽 창에서 작업에서 Hyper-v 설정 옵션을 보여 주는 스크린 샷](media/HyperV-ActionsHyperVSettings.png)  
  
4.  **서버**에서 **고급 세션 모드 정책**을 선택합니다.  
  
    ![보안 섹션에서 고급 세션 모드 정책 옵션을 보여 주는 스크린 샷](media/Hyper-V-Settings-ServerEnhancedSessionModePolicy.png)  
  
5.  **고급 세션 모드 허용** 확인란을 선택합니다.  
  
    ![허용을 보여 주는 스크린 샷 고급 세션 모드 정책에 대 한 세션 모드 확인란 향상.](media/Hyper-V-Settings-EnhancedSessionModePolicyCheckBox.png)  
  
6.  **사용자**에서 **고급 세션 모드**를 선택합니다.  
  
    ![사용자 섹션에서 고급 세션 모드 옵션을 보여 주는 스크린 샷 ](media/Hyper-V-Settings-UserEnhancedSessionMode.png)  
  
7.  **고급 세션 모드 허용** 확인란을 선택합니다.  
  
8.  **확인**을 클릭합니다.  
  
## <a name="choose-a-local-resource"></a>로컬 리소스 선택

로컬 리소스에는 프린터, 클립보드 및 VMConnect를 실행하는 컴퓨터의 로컬 드라이브가 있습니다. 자세한 내용은 아래 [로컬 리소스 사용을 위한 요구 사항](#requirements-for-using-local-resources)을 참조하세요.  
  
로컬 리소스를 선택하려면 다음을 수행합니다.
  
1.  VMConnect를 엽니다.  
  
2.  연결하려는 가상 머신을 허용하려면.  
  
3.  **옵션 표시**를 클릭합니다.  
  
    ![대화 상자의 왼쪽 아래에 표시 옵션을 호출 하는 스크린 샷](media/HyperV-VMConnect-DisplayConfig.png)  
  
4.  **로컬 리소스**를 선택합니다.  
  
    ![로컬 리소스 탭을 호출 하는 스크린 샷](media/HyperV-VMConnect-DisplayConfig-LocalResources.png)  
  
5.  **기타**를 클릭합니다.  
  
    ![스크린 샷에 자세히 단추를 호출 합니다.](media/HyperV-VMConnect-DisplayConfig-LocalResourcesMore.png)  
  
6.  가상 머신에서 사용하려는 드라이브를 선택하고 **확인**을 클릭합니다.  
  
    ![로컬 리소스 및 선택할 수 있는 드라이브를 보여 주는 스크린 샷](media/HyperV-VMConnect-Settings-LocalResourcesDrives.png)  
  
7.  **이 가상 머신에 대한 이후 연결을 위해 내 설정 저장**을 허용하려면.  
  
    ![이 옵션을 선택 하려면이 확인란을 호출 하는 스크린 샷](media/HyperV-VMConnect-SaveSettings.png)  
  
8.  **연결**을 클릭합니다.  
  
## <a name="edit-vmconnect-settings"></a>VMConnect 설정 편집

Windows PowerShell 또는 명령 프롬프트에서 다음 명령을 실행하여 VMConnect에 대한 연결 설정을 쉽게 편집할 수 있습니다.  
  
`VMConnect.exe <ServerName> <VMName> /edit`  
  
> [!Note]
> 관리자 권한 명령 프롬프트가 필요할 수 있습니다.
  
## <a name="requirements-for-using-local-resources"></a>로컬 리소스 사용을 위한 요구 사항

컴퓨터의 로컬 리소스를 사용하여 가상 머신을 사용할 수 있습니다:  
  
-   Hyper-V 호스트에는 **고급 세션 모드 정책** 및 **고급 세션 모드** 설정이 켜져 있어야 합니다.  
  
-   VMConnect를 사용하는 컴퓨터에서는 Windows 10, Windows 8.1, Windows Server 2016 또는 Windows Server 2012 R2를 실행해야 합니다.  
  
-   가상 머신은 원격 데스크톱 서비스를 사용하도록 설정하고 Windows 10, Windows 8.1, Windows Server 2016 또는 Windows Server 2012 R2를 게스트 운영 체제로 실행해야 합니다.  
  
VMConnect를 실행하는 컴퓨터와 가상 머신이 모두 요구 사항을 충족하는 경우 다음 로컬 리소스 중 하나를 사용할 수 있습니다.  
  
-   디스플레이 구성  
  
-   오디오
  
-   프린터  
  
-   복사 및 붙여넣기를 위한 클립보드  
  
-   스마트 카드  
  
-   USB 디바이스  
  
-   드라이브  
  
-   지원되는 플러그 앤 플레이 디바이스  
  
## <a name="why-use-a-computers-local-resources"></a>컴퓨터의 로컬 리소스를 사용 하는 이유는?
컴퓨터의 로컬 리소스를 사용 하 여 설정할 수 있습니다.  
  
-   가상 머신을 네트워크에 연결하지 않고 가상 머신의 문제를 해결하려는 경우  
  
-   RDP(원격 데스크톱 연결)를 사용하여 복사하고 붙여넣는 것과 같은 방식으로 가상 머신에서 파일을 복사하여 붙여넣으려는 경우  
  
-   스마트 카드를 사용하여 가상 머신에 로그인하려는 경우  
  
-   가상 머신에서 로컬 프린터로 인쇄하려는 경우  
  
-   RDP를 사용하지 않고 USB 및 사운드 리디렉션이 필요한 개발자 애플리케이션을 테스트하고 문제를 해결하려는 경우  
  
## <a name="see-also"></a>참고 항목  
[Virtual Machine에 연결](https://technet.microsoft.com/library/cc742407.aspx)  
[1세대 또는 2세대 가상 머신을 Hyper-V에서 만들어야 하나요?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)


