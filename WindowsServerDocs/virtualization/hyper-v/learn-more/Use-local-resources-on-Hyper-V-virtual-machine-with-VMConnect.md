---
title: Use local resources on Hyper-V virtual machine with VMConnect
description: VMConnect에서 로컬 리소스를 사용 하기 위한 요구 사항에 대해 설명 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18eface5-7518-4c6b-9282-93e2e3e87492
author: KBDAzure
ms.author: kathyDav
ms.date: 12/06/2016
ms.openlocfilehash: 70bf72ec2277679820d985c9f78f10a4ea6e04df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392890"
---
# <a name="use-local-resources-on-hyper-v-virtual-machine-with-vmconnect"></a>Use local resources on Hyper-V virtual machine with VMConnect

>적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2

VMConnect (가상 컴퓨터 연결)를 사용 하면 이동식 USB 플래시 드라이브 또는 프린터와 같은 가상 컴퓨터에서 컴퓨터의 로컬 리소스를 사용할 수 있습니다. 고급 세션 모드를 사용 하면 VMConnect 창의 크기를 조정할 수도 있습니다. 이 문서에서는 호스트를 구성한 다음 가상 컴퓨터에 로컬 리소스에 대 한 액세스 권한을 부여 하는 방법을 보여 줍니다.

고급 세션 모드 및 형식 클립보드 텍스트는 최근 Windows 운영 체제를 실행 하는 가상 컴퓨터에만 사용할 수 있습니다. 아래에서 [로컬 리소스를 사용 하기 위한 요구 사항을](#requirements-for-using-local-resources)참조 \(.\) 

Ubuntu를 실행 하는 가상 컴퓨터에 대 한 참조 [Hyper-v VM에서 Ubuntu 화면 해상도 변경](https://blogs.msdn.microsoft.com/virtual_pc_guy/2014/09/19/changing-ubuntu-screen-resolution-in-a-hyper-v-vm/)합니다. 
  
## <a name="turn-on-enhanced-session-mode-on-a-hyper-v-host"></a>Hyper-v 호스트에서 고급 세션 모드 켜기  
Hyper-v 호스트에서 Windows 10 또는 Windows 8.1를 실행 하는 경우 고급 세션 모드는 기본적으로 켜져 있으므로이를 건너뛰고 다음 섹션으로 이동할 수 있습니다. 그러나 호스트에서 Windows Server 2016 또는 Windows Server 2012 r 2를 실행 하는 경우 먼저이 작업을 수행 합니다. 
  
고급 세션 모드를 설정 합니다.

1.  가상 컴퓨터를 호스트하는 컴퓨터에 연결합니다.  
  
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

로컬 리소스에는 프린터, 클립보드 및 VMConnect를 실행 하는 컴퓨터의 로컬 드라이브가 있습니다. 자세한 내용은 아래의 [로컬 리소스를 사용 하기 위한 요구 사항](#requirements-for-using-local-resources)을 참조 하세요.  
  
로컬 리소스를 선택 하려면:
  
1.  VMConnect를 엽니다.  
  
2.  연결하려는 가상 컴퓨터를 선택합니다.  
  
3.  **옵션 표시**를 클릭합니다.  
  
    ![대화 상자의 왼쪽 아래에 표시 옵션을 호출 하는 스크린 샷](media/HyperV-VMConnect-DisplayConfig.png)  
  
4.  **로컬 리소스**를 선택합니다.  
  
    ![로컬 리소스 탭을 호출 하는 스크린 샷](media/HyperV-VMConnect-DisplayConfig-LocalResources.png)  
  
5.  **기타**를 클릭합니다.  
  
    ![스크린 샷에 자세히 단추를 호출 합니다.](media/HyperV-VMConnect-DisplayConfig-LocalResourcesMore.png)  
  
6.  가상 컴퓨터에서 사용하려는 드라이브를 선택하고 **확인**을 클릭합니다.  
  
    ![로컬 리소스 및 선택할 수 있는 드라이브를 보여 주는 스크린 샷](media/HyperV-VMConnect-Settings-LocalResourcesDrives.png)  
  
7.  **이 가상 컴퓨터에 대한 이후 연결을 위해 내 설정 저장**을 선택합니다.  
  
    ![이 옵션을 선택 하려면이 확인란을 호출 하는 스크린 샷](media/HyperV-VMConnect-SaveSettings.png)  
  
8.  **연결**을 클릭합니다.  
  
## <a name="edit-vmconnect-settings"></a>VMConnect 설정 편집

Windows PowerShell 또는 명령 프롬프트에서 다음 명령을 실행하여 VMConnect에 대한 연결 설정을 쉽게 편집할 수 있습니다.  
  
`VMConnect.exe <ServerName> <VMName> /edit`  
  
## <a name="requirements-for-using-local-resources"></a>로컬 리소스 사용을 위한 요구 사항

컴퓨터의 로컬 리소스를 사용 하 여 가상 컴퓨터 수 있습니다:  
  
-   Hyper-v 호스트의 **고급 세션 모드 정책** 및 **고급 세션 모드** 설정이 켜져 있어야 합니다.  
  
-   VMConnect를 사용 하는 컴퓨터는 Windows 10, Windows 8.1, Windows Server 2016 또는 Windows Server 2012 r 2를 실행 해야 합니다.  
  
-   가상 컴퓨터에서 원격 데스크톱 서비스 사용 하도록 설정 하 고 Windows 10, Windows 8.1, Windows Server 2016 또는 Windows Server 2012 r 2를 게스트 운영 체제로 실행 해야 합니다.  
  
VMConnect를 실행 하는 컴퓨터와 가상 컴퓨터가 모두 요구 사항을 충족 하는 경우 다음 로컬 리소스를 사용할 수 있습니다.  
  
-   디스플레이 구성  
  
-   오디오
  
-   프린터  
  
-   복사 및 붙여넣기를 위한 클립보드  
  
-   스마트 카드  
  
-   USB 장치  
  
-   드라이브  
  
-   지원되는 플러그 앤 플레이 장치  
  
## <a name="why-use-a-computers-local-resources"></a>컴퓨터의 로컬 리소스를 사용 하는 이유는?
컴퓨터의 로컬 리소스를 사용 하 여 설정할 수 있습니다.  
  
-   가상 컴퓨터를 네트워크에 연결하지 않고 가상 컴퓨터의 문제를 해결하려는 경우  
  
-   RDP(원격 데스크톱 연결)를 사용하여 복사하고 붙여 넣는 것과 같은 방식으로 가상 컴퓨터에서 파일을 복사하여 붙여 넣으려는 경우  
  
-   스마트 카드를 사용하여 가상 컴퓨터에 로그인하려는 경우  
  
-   가상 컴퓨터에서 로컬 프린터로 인쇄하려는 경우  
  
-   RDP를 사용하지 않고 USB 및 사운드 리디렉션이 필요한 개발자 응용 프로그램을 테스트하고 문제를 해결하려는 경우  
  
## <a name="see-also"></a>참고 항목  
[가상 컴퓨터에 연결](https://technet.microsoft.com/library/cc742407.aspx)  
[Hyper-v에서 1 세대 또는 2 세대 가상 머신을 만들어야 하나요?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)



