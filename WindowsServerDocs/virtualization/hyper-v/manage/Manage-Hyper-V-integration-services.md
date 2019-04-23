---
title: Hyper-v 통합 서비스 관리
description: Integration services를 켜거나 끄고 필요한 경우 설치 하는 방법을 설명 합니다.
ms.technology: compute-hyper-v
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.date: 12/20/2016
ms.topic: article
ms.prod: windows-server-threshold
ms.service: na
ms.assetid: 9cafd6cb-dbbe-4b91-b26c-dee1c18fd8c2
ms.openlocfilehash: b049efc61d5060791574f20fcdd8b369a26f0507
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890254"
---
>적용 대상: Windows 10, Windows Server 2016, Windows Server 2019

# <a name="manage-hyper-v-integration-services"></a>Hyper-v 통합 서비스 관리

Hyper-v 통합 서비스 가상 머신 성능을 향상 하 고 Hyper-v 호스트와의 양방향 통신을 활용 하 여 편의 기능을 제공 합니다. 이러한 서비스의 대부분은 이지만 나머지는 가상 장치 드라이버 등의 가상 컴퓨터의 기능에 중요 한 상당수, 예: 게스트 파일 복사 합니다. 이 서비스의 설정 및 드라이버는 경우에 따라 "통합 구성 요소" 라고도 합니다. 지정된 된 가상 컴퓨터에 대 한 개별 편의 서비스 작동 하는 여부를 제어할 수 있습니다. 수동으로 처리 드라이버 구성 요소를 사용 하는 것이 없습니다.

각 통합 서비스에 대 한 자세한 내용은 참조 하세요 [Hyper-v Integration Services](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services)합니다.

>[!IMPORTANT]
>작동 하는 데 사용 하려는 각 서비스 호스트와 게스트 모두에서 활성화 되어야 합니다. "Hyper-v 게스트 서비스 인터페이스"를 제외한 모든 통합 서비스는 Windows 게스트 운영 체제에서 기본적으로 켜져 있습니다. 서비스를 설정 하 고 해제 개별적으로 합니다. 다음 섹션에서는 그 방법을 보여줍니다.

## <a name="turn-an-integration-service-on-or-off-using-hyper-v-manager"></a>통합 서비스를 켜거나 끄려면 Hyper-v 관리자를 사용 하 여

1. 가운데 창에서 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 클릭 **설정을**합니다.
  
2. 왼쪽된 창에서를 **설정** 창 아래에 있는 **Management**, 클릭 **Integration Services**합니다.
  
Integration Services 창에는 Hyper-v 호스트에서 사용할 수 있는 모든 통합 서비스를 나열 하 고 호스트 하는 데 가상 컴퓨터를 활성화 하는지 여부입니다.

### <a name="turn-an-integration-service-on-or-off-using-powershell"></a>통합 서비스를 켜거나 끄려면 PowerShell을 사용 하 여

이를 위해 PowerShell을 사용 하 여 [Enable-vmintegrationservice](https://technet.microsoft.com/library/hh848500.aspx) 하 고 [Disable-vmintegrationservice](https://technet.microsoft.com/library/hh848488.aspx)합니다.

다음 예에서는 게스트 파일 복사 통합 서비스 설정 및 해제 "demovm" 이라는 가상 컴퓨터 설정 보여 줍니다.

1. Integration services를 실행 하는 목록을 가져옵니다.
  
    ``` PowerShell
    Get-VMIntegrationService -VMName "DemoVM"
    ```
1. 출력은 다음과 유사합니다.

    ``` PowerShell
   VMName      Name                    Enabled PrimaryStatusDescription SecondaryStatusDescription
   ------      ----                    ------- ------------------------ --------------------------
   DemoVM      Guest Service Interface False   OK
   DemoVM      Heartbeat               True    OK                       OK
   DemoVM      Key-Value Pair Exchange True    OK
   DemoVM      Shutdown                True    OK
   DemoVM      Time Synchronization    True    OK
   DemoVM      VSS                     True    OK
   ```

1. 게스트 서비스 인터페이스를 켭니다.

   ``` PowerShell
   Enable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
   ```

1. 게스트 서비스 인터페이스를 사용할 수 있음을 확인 합니다.

   ```
   Get-VMIntegrationService -VMName "DemoVM" 
   ``` 

1. 게스트 서비스 인터페이스를 해제 합니다.

    ```
    Disable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
    ```
   
## <a name="checking-the-guests-integration-services-version"></a>게스트의 integration services 버전 확인
일부 기능 하지 못할 올바르게 되거나 전혀 게스트 통합 서비스가 현재 없는 경우. Windows 게스트 운영 체제에 로그온에 대 한 버전 정보를 가져오려면 명령 프롬프트를 열고이 명령을 실행:

```
REG QUERY "HKLM\Software\Microsoft\Virtual Machine\Auto" /v IntegrationServicesVersion
```
이전 버전의 게스트 운영 체제에서 사용 가능한 모든 서비스를 갖지 않습니다. 예를 들어, Windows Server 2008 R2 게스트 "Hyper-v 게스트 서비스 인터페이스"를 사용할 수 없습니다.

## <a name="start-and-stop-an-integration-service-from-a-windows-guest"></a>Windows 게스트에서 통합 서비스를 시작 및 중지
완전 하 게 작동 하는 통합 서비스에 대 한 순서 대로 해당 서비스 호스트에서 사용 하도록 설정 하는 것 외에도 게스트 내에서 실행 되어야 합니다. Windows 게스트에서 각 통합 서비스는 표준 Windows 서비스로 나열 됩니다. 이러한 서비스 중지 및 시작 하려면 제어판 또는 PowerShell에서 서비스 애플릿을 사용할 수 있습니다.

>[!IMPORTANT]
> 통합 서비스를 중지 합니다. 호스트의 가상 컴퓨터를 관리할 수에 심각한 영향을 미칠 수 있습니다. 올바르게 작동 하려면 사용 하려는 각 통합 서비스 호스트와 게스트 모두에서 사용할 수 있어야 합니다.
> 모범 사례로 위의 지침을 사용 하 여 Hyper-v 통합 서비스를 제어 해야 합니다. 게스트 운영 체제에서 일치 하는 서비스는 중지 되거나 Hyper-v에서 해당 상태를 변경 하면 자동으로 시작 됩니다.
> 게스트 운영 체제에서 서비스를 시작 하지만 Hyper-v에서 해제 되어 있는 경우 서비스가 중지 됩니다. Hyper-v에서 사용 되는 게스트 운영 체제에서 서비스를 중지 하는 경우 Hyper-v는 결국 다시 시작 합니다. 게스트 서비스를 비활성화 하면 Hyper-v가 시작할 수 없습니다.

### <a name="use-windows-services-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows 서비스를 사용 하 여 시작 하거나 Windows 게스트 내에서 통합 서비스를 중지 하려면

1. 실행 하 여 서비스 관리자를 열고 ```services.msc``` 관리자 또는 제어판의 서비스 아이콘을 두 번 클릭 합니다.

    ![Windows 서비스 창 보여 주는 스크린샷](media/HVServices.png) 

1. "Hyper-v"로 시작 하는 서비스를 찾습니다. 

1. 시작 또는 중지 하려는 서비스를 마우스 오른쪽 단추로 클릭 합니다. 원하는 작업을 클릭 합니다.


### <a name="use-windows-powershell-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows PowerShell을 사용 하 여 시작 하거나 Windows 게스트 내에서 통합 서비스를 중지 하려면

1. Integration services의 목록을 가져오려면 다음을 실행 합니다.

    ```
    Get-Service -Name vm*
    ```
1.  출력은 다음과 유사 하 게 같아야 합니다.

    ```PowerShell
    Status   Name               DisplayName
    ------   ----               -----------
    Running  vmicguestinterface Hyper-V Guest Service Interface
    Running  vmicheartbeat      Hyper-V Heartbeat Service
    Running  vmickvpexchange    Hyper-V Data Exchange Service
    Running  vmicrdv            Hyper-V Remote Desktop Virtualizati...
    Running  vmicshutdown       Hyper-V Guest Shutdown Service
    Running  vmictimesync       Hyper-V Time Synchronization Service
    Stopped  vmicvmsession      Hyper-V VM Session Service
    Running  vmicvss            Hyper-V Volume Shadow Copy Requestor
    ```

1. 중 하나를 실행할 [Start-service](https://technet.microsoft.com/library/hh849825.aspx) 하거나 [Stop-service](https://technet.microsoft.com/library/hh849790.aspx)합니다. 예를 들어, Windows PowerShell Direct를 해제 하려면 다음을 실행 합니다.

    ```
    Stop-Service -Name vmicvmsession
    ```

## <a name="start-and-stop-an-integration-service-from-a-linux-guest"></a>Linux 게스트에서 통합 서비스를 시작 및 중지 

Linux 통합 서비스는 일반적으로 Linux 커널을 통해 제공됩니다. Linux 통합 서비스 드라이버 라고 **hv_utils**합니다.

1.  확인 하려면 **hv_utils** 로드는이 명령을 사용 하 여:

    ``` BASH
    lsmod | grep hv_utils
    ``` 
  
1. 출력은 다음과 유사 하 게 같아야 합니다.  
  
    ``` BASH
    Module                  Size   Used by
    hv_utils               20480   0
    hv_vmbus               61440   8 hv_balloon,hyperv_keyboard,hv_netvsc,hid_hyperv,hv_utils,hyperv_fb,hv_storvsc
    ```

1. 필요한 디먼이 실행 하는 경우를 찾으려면이 명령을 사용 합니다.
  
    ``` BASH
    ps -ef | grep hv
    ```
  
1. 출력은 다음과 유사 하 게 같아야 합니다. 
  
    ```BASH
    root       236     2  0 Jul11 ?        00:00:00 [hv_vmbus_con]
    root       237     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    ...
    root       252     2  0 Jul11 ?        00:00:00 [hv_vmbus_ctl]
    root      1286     1  0 Jul11 ?        00:01:11 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9333     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_kvp_daemon
    root      9365     1  0 Oct12 ?        00:00:00 /usr/lib/linux-tools/3.13.0-32-generic/hv_vss_daemon
    scooley  43774 43755  0 21:20 pts/0    00:00:00 grep --color=auto hv          
    ```

1. 사용할 수 있는 디먼을 보려면 다음을 실행합니다.

    ``` BASH
    compgen -c hv_
    ```
  
1. 출력은 다음과 유사 하 게 같아야 합니다.
  
    ``` BASH
    hv_vss_daemon
    hv_get_dhcp_info
    hv_get_dns_info
    hv_set_ifconfig
    hv_kvp_daemon
    hv_fcopy_daemon     
    ```
  
 통합 서비스 디먼이 표시 될 수도 있습니다는 다음과 같습니다. 누락 된 경우 시스템에서 지원 되지 않는 또는 설치 되지 않을 수 있습니다. 자세한 내용은 참조 하십시오 [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](https://technet.microsoft.com/library/dn531030.aspx)합니다.  
  - **hv_vss_daemon**: 이 디먼은 라이브 Linux 가상 머신 백업을 만드는 데 필요 합니다.
  - **hv_kvp_daemon**: 이 디먼 설정 및 내장 및 외장 키 값 쌍을 쿼리할 수 있습니다.
  - **hv_fcopy_daemon**: 이 디먼은 호스트와 게스트 사이의 서비스를 복사 하는 파일을 구현 합니다.  

### <a name="examples"></a>예

이러한 예제를 중지 했다가 시작 이라는 KVP 데몬, 보여 `hv_kvp_daemon`합니다.

1. 프로세스 ID를 사용 하 여 \(PID\) 디먼의 프로세스를 중지 합니다. PID를 찾으려면 출력의 두 번째 열을 확인 또는 사용 하 여 `pidof`입니다. Hyper-v 데몬 루트 권한이 필요 하므로 루트로 실행 합니다.

    ``` BASH
    sudo kill -15 `pidof hv_kvp_daemon`
    ```

1. 확인 하려면 모든 `hv_kvp_daemon` 프로세스는 실행:

    ```
    ps -ef | hv
    ```

1. 디먼을 다시 시작 하려면 디먼을 루트로 실행 합니다.

    ``` BASH
    sudo hv_kvp_daemon
    ``` 

1. 확인을 `hv_kvp_daemon` 프로세스를 실행 하 여 새 프로세스 ID를 사용 하 여 나열 됩니다.

    ```
    ps -ef | hv
    ```

## <a name="keep-integration-services-up-to-date"></a>통합 서비스를 최신 상태로 유지

있습니다 최신 통합 서비스를 가상 컴퓨터에 대 한 최상의 성능 및 최신 기능을 가져오려고 하는 것이 좋습니다. 이런 대부분의 Windows 게스트에 대 한 기본적으로 Windows 업데이트에서 중요 한 업데이트를 받도록 설정 합니다. 현재 커널을 사용 하는 Linux 게스트 커널을 업데이트할 때 최신 통합 구성 요소를 받게 됩니다.

**Windows 10 호스트에서 실행되는 가상 컴퓨터:**

> [!NOTE]
> 이미지 파일 vmguest.iso 더 이상 필요 하므로 Windows 10에서 Hyper-v를 사용 하 여 포함 되지 않습니다.

| 게스트  | 업데이트 메커니즘 | 참고 |
|:---------|:---------|:---------|
| Windows 10 | Windows 업데이트 | |
| Windows 8.1 | Windows 업데이트 | |
| Windows 8 | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows 7 | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows Vista(SP 2) | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| - | | |
| Windows Server 2016 | Windows 업데이트 | |
| Windows Server 반기 채널 | Windows 업데이트 | |
| Windows Server 2012 R2 | Windows 업데이트 | |
| Windows Server 2012 | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows Server 2008 R2(SP 1) | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows Server 2008(SP 2) | Windows 업데이트 | 추가 지원은 Windows Server 2016 에서만 가능 ([자세히](https://support.microsoft.com/lifecycle?p1=12925)). |
| Windows Home Server 2011 | Windows 업데이트 | Windows Server 2016에서 지원 되지 것입니다 ([자세히](https://support.microsoft.com/lifecycle?p1=15820)). |
| Windows Small Business Server 2011 | Windows 업데이트 | 일반 지원에는 포함되지 않습니다([자세히 알아보기](https://support.microsoft.com/lifecycle?p1=15817)). |
| - | | |
| Linux 게스트 | 패키지 관리자 | 용 Linux integration services는 배포판에 기본 제공 되지만 선택적 업데이트가 제공 될 수 있습니다. ******** |

\* 이러한 게스트에 대 한 통합 서비스에서 사용할 데이터 교환 통합 서비스를 사용할 수 없는 경우는 [다운로드 센터](https://support.microsoft.com/kb/3071740) 캐비닛 (cab) 파일로. Cab 파일을 적용 하는 것에 대 한 지침은이 사용 가능한 [블로그 게시물](https://blogs.technet.com/b/virtualization/archive/2015/07/24/integration-components-available-for-virtual-machines-not-connected-to-windows-update.aspx)합니다.

**Windows 8.1 호스트에서 실행되는 가상 컴퓨터:**

| 게스트  | 업데이트 메커니즘 | 참고 |
|:---------|:---------|:---------|
| Windows 10 | Windows 업데이트 | |
| Windows 8.1 | Windows 업데이트 | |
| Windows 8 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows 7 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Vista(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows XP(SP 2, SP 3) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| - | | |
| Windows Server 2016 | Windows 업데이트 | |
| Windows Server 반기 채널 | Windows 업데이트 | |
| Windows Server 2012 R2 | Windows 업데이트 | |
| Windows Server 2012 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Server 2008 R2 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Server 2008(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Home Server 2011 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Small Business Server 2011 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Server 2003 R2(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Server 2003(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| - | | |
| Linux 게스트 | 패키지 관리자 | 용 Linux integration services는 배포판에 기본 제공 되지만 선택적 업데이트가 제공 될 수 있습니다. ** |


**Windows 8 호스트에서 실행되는 가상 컴퓨터:**

| 게스트  | 업데이트 메커니즘 | 참고 |
|:---------|:---------|:---------|
| Windows 8.1 | Windows 업데이트 | |
| Windows 8 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows 7 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Vista(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows XP(SP 2, SP 3) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| - | | |
| Windows Server 2012 R2 | Windows 업데이트 | |
| Windows Server 2012 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Server 2008 R2 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래.|
| Windows Server 2008(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Home Server 2011 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Small Business Server 2011 | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Server 2003 R2(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| Windows Server 2003(SP 2) | 통합 서비스 디스크 | 참조 [지침](#install-or-update-integration-services)아래. |
| - | | |
| Linux 게스트 | 패키지 관리자 | 용 Linux integration services는 배포판에 기본 제공 되지만 선택적 업데이트가 제공 될 수 있습니다. ** |

Linux 게스트에 대 한 자세한 내용은 참조 하세요. [Windows의 Hyper-v에 대 한 지원 되는 Linux 및 FreeBSD 가상 컴퓨터](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)합니다.

## <a name="install-or-update-integration-services"></a>설치 또는 통합 서비스 업데이트

호스트에 대 한 Windows 10 및 Windows Server 2016 보다 이전 해야 수동으로 설치 하거나 게스트 운영 체제에서 통합 서비스를 업데이트 합니다. 
  
1.  Hyper-V 관리자를 엽니다. 서버 관리자의 도구 메뉴에서 클릭 **Hyper-v 관리자**합니다.  
  
2.  가상 컴퓨터에 연결합니다. 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 클릭 **Connect**합니다.  
  
3.  가상 컴퓨터 연결의 작업 메뉴에서 **통합 서비스 설치 디스크 삽입**을 클릭합니다. 이렇게 하면 DVD 드라이브에 설치 디스크가 로드됩니다. 게스트 운영 체제에 따라 설치를 수동으로 시작 해야 합니다.  
  
4.  설치를 마치고 나면 모든 통합 서비스를 사용할 수 있습니다.

이러한 단계 자동화 하거나 온라인 가상 머신에 대 한 Windows PowerShell 세션 내에서 수행 될 수 없습니다. 오프 라인 VHDX 이미지를 적용할 수 있습니다. [이 블로그 게시물 참조](https://blogs.technet.microsoft.com/virtualization/2013/04/18/how-to-install-integration-services-when-the-virtual-machine-is-not-running/)합니다.
