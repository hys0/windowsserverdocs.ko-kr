---
title: Hyper-v Integration Services 관리
description: Integration services를 설정 및 해제 하 고 필요한 경우 설치 하는 방법을 설명 합니다.
ms.technology: compute-hyper-v
author: KBDAzure
ms.author: kathydav
manager: dongill
ms.date: 12/20/2016
ms.topic: article
ms.prod: windows-server
ms.service: na
ms.assetid: 9cafd6cb-dbbe-4b91-b26c-dee1c18fd8c2
ms.openlocfilehash: 39d57afbd8c4df78764c5975d4cc3d48848475c1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392769"
---
>적용 대상: Windows 10, Windows Server 2016, Windows Server 2019

# <a name="manage-hyper-v-integration-services"></a>Hyper-v Integration Services 관리

Hyper-v Integration Services Hyper-v 호스트와 양방향 통신을 활용 하 여 가상 컴퓨터 성능을 향상 시키고 편리한 기능을 제공 합니다. 이러한 서비스 중 상당수는 게스트 파일 복사와 같은 편리 하며, 다른 서비스는 가상 머신 기능 (예: 가상 장치 드라이버)에 중요 합니다. 이 서비스 및 드라이버 집합을 "통합 구성 요소" 라고도 합니다. 특정 가상 컴퓨터에 대해 개별 사용자 서비스의 작동 여부를 제어할 수 있습니다. 드라이버 구성 요소는 수동으로 서비스 하기 위한 것이 아닙니다.

각 통합 서비스에 대 한 자세한 내용은 [hyper-v Integration Services](https://docs.microsoft.com/virtualization/hyper-v-on-windows/reference/integration-services)를 참조 하세요.

> [!IMPORTANT]
> 사용 하려는 각 서비스는 호스트와 게스트 모두에서 작동 하도록 설정 해야 합니다. "Hyper-V 게스트 서비스 인터페이스"를 제외한 모든 통합 서비스는 Windows 게스트 운영 체제에 기본적으로 설정 되어 있습니다. 서비스는 개별적으로 설정 및 해제할 수 있습니다. 다음 섹션에서는 방법을 보여 줍니다.

## <a name="turn-an-integration-service-on-or-off-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 통합 서비스 설정 또는 해제

1. 가운데 창에서 가상 머신을 마우스 오른쪽 단추로 클릭 하 고 **설정**을 클릭 합니다.
  
2. **설정** 창의 왼쪽 창에 있는 **관리**에서 **Integration Services**를 클릭 합니다.
  
Integration Services 창에는 Hyper-v 호스트에서 사용할 수 있는 모든 통합 서비스와 호스트에서 가상 컴퓨터를 사용할 수 있도록 설정 되어 있는지 여부가 표시 됩니다.

### <a name="turn-an-integration-service-on-or-off-using-powershell"></a>PowerShell을 사용 하 여 통합 서비스 설정 또는 해제

PowerShell에서이 작업을 수행 하려면 [enable-vmintegrationservice](https://technet.microsoft.com/library/hh848500.aspx) 및 [enable-vmintegrationservice](https://technet.microsoft.com/library/hh848488.aspx)를 사용 합니다.

다음 예에서는 "demovm" 이라는 가상 컴퓨터에 대해 게스트 파일 복사 통합 서비스를 설정 및 해제 하는 방법을 보여 줍니다.

1. 실행 중인 integration services 목록 가져오기:
  
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

1. 게스트 서비스 인터페이스 설정:

   ``` PowerShell
   Enable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
   ```

1. 게스트 서비스 인터페이스가 사용 되는지 확인 합니다.

   ```
   Get-VMIntegrationService -VMName "DemoVM" 
   ``` 

1. 게스트 서비스 인터페이스를 해제 합니다.

    ```
    Disable-VMIntegrationService -VMName "DemoVM" -Name "Guest Service Interface"
    ```
   
## <a name="checking-the-guests-integration-services-version"></a>게스트의 integration services 버전을 확인 하는 중
일부 기능은 제대로 작동 하지 않을 수 있으며, 게스트의 통합 서비스가 최신이 아닌 경우에는 전혀 작동 하지 않을 수 있습니다. Windows에 대 한 버전 정보를 가져오려면 게스트 운영 체제에 로그온 하 고 명령 프롬프트를 연 후 다음 명령을 실행 합니다.

```
REG QUERY "HKLM\Software\Microsoft\Virtual Machine\Auto" /v IntegrationServicesVersion
```

이전 게스트 운영 체제에는 사용 가능한 서비스가 모두 포함 되지 않습니다. 예를 들어 Windows Server 2008 R2 게스트에는 "Hyper-V 게스트 서비스 인터페이스"을 사용할 수 없습니다.

## <a name="start-and-stop-an-integration-service-from-a-windows-guest"></a>Windows 게스트에서 통합 서비스 시작 및 중지
Integration service가 완벽 하 게 작동 하려면 호스트에서 사용 하도록 설정 하는 것 외에도 해당 서비스가 게스트 내에서 실행 되어야 합니다. Windows 게스트에서 각 통합 서비스는 표준 Windows 서비스로 나열 됩니다. 제어판 또는 PowerShell에서 서비스 애플릿을 사용 하 여 이러한 서비스를 중지 하 고 시작할 수 있습니다.

> [!IMPORTANT]
> 통합 서비스를 중지 하면 가상 컴퓨터를 관리 하는 호스트의 기능에 심각한 영향을 줄 수 있습니다. 제대로 작동 하려면 사용 하려는 각 통합 서비스를 호스트와 게스트 모두에서 사용 하도록 설정 해야 합니다.
> 모범 사례로, 위의 지침을 사용 하 여 Hyper-v에서 integration services를 제어 해야 합니다. Hyper-v에서 해당 상태를 변경 하면 게스트 운영 체제의 일치 서비스가 자동으로 중지 되거나 시작 됩니다.
> 게스트 운영 체제에서 서비스를 시작 하지만 Hyper-v에서 서비스를 사용할 수 없는 경우 서비스는 중지 됩니다. Hyper-v에서 사용 되는 게스트 운영 체제에서 서비스를 중지 하는 경우 Hyper-v에서 서비스를 다시 시작 합니다. 게스트에서 서비스를 사용 하지 않도록 설정 하는 경우 Hyper-v에서 서비스를 시작할 수 없습니다.

### <a name="use-windows-services-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows 서비스를 사용 하 여 Windows 게스트 내에서 통합 서비스 시작 또는 중지

1. 관리자 권한으로 ```services.msc```을 실행 하거나 제어판에서 서비스 아이콘을 두 번 클릭 하 여 서비스 관리자를 엽니다.

    ![Windows 서비스 창을 보여 주는 스크린샷](media/HVServices.png) 

1. "Hyper-v"로 시작 하는 서비스를 찾습니다. 

1. 시작 하거나 중지할 서비스를 마우스 오른쪽 단추로 클릭 합니다. 원하는 작업을 클릭 합니다.

### <a name="use-windows-powershell-to-start-or-stop-an-integration-service-within-a-windows-guest"></a>Windows PowerShell을 사용 하 여 Windows 게스트 내에서 통합 서비스 시작 또는 중지

1. Integration services 목록을 가져오려면 다음을 실행 합니다.

    ```
    Get-Service -Name vm*
    ```

1.  출력은 다음과 유사 하 게 표시 됩니다.

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

1. [시작 서비스](https://technet.microsoft.com/library/hh849825.aspx) 또는 [서비스 중지](https://technet.microsoft.com/library/hh849790.aspx)를 실행 합니다. 예를 들어 Windows PowerShell Direct를 해제 하려면 다음을 실행 합니다.

    ```
    Stop-Service -Name vmicvmsession
    ```

## <a name="start-and-stop-an-integration-service-from-a-linux-guest"></a>Linux 게스트에서 통합 서비스 시작 및 중지 

Linux 통합 서비스는 일반적으로 Linux 커널을 통해 제공됩니다. Linux integration services 드라이버의 이름은 **라고**입니다.

1. **라고** 가 로드 되었는지 확인 하려면 다음 명령을 사용 합니다.

   ``` BASH
   lsmod | grep hv_utils
   ``` 
  
2. 출력은 다음과 유사 하 게 표시 됩니다.  
  
    ``` BASH
    Module                  Size   Used by
    hv_utils               20480   0
    hv_vmbus               61440   8 hv_balloon,hyperv_keyboard,hv_netvsc,hid_hyperv,hv_utils,hyperv_fb,hv_storvsc
    ```

3. 필요한 디먼 실행 중인지 확인 하려면 다음 명령을 사용 합니다.
  
    ``` BASH
    ps -ef | grep hv
    ```
  
4. 출력은 다음과 유사 하 게 표시 됩니다. 
  
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

5. 사용할 수 있는 디먼을 보려면 다음을 실행합니다.

    ``` BASH
    compgen -c hv_
    ```
  
6. 출력은 다음과 유사 하 게 표시 됩니다.
  
    ``` BASH
    hv_vss_daemon
    hv_get_dhcp_info
    hv_get_dns_info
    hv_set_ifconfig
    hv_kvp_daemon
    hv_fcopy_daemon     
    ```
  
   나열 될 수 있는 Integration service 디먼는 다음과 같습니다. 이러한 항목이 없는 경우 시스템에서 지원 되지 않거나 설치 되지 않았을 수 있습니다. 자세한 내용은 [Windows에서 hyper-v에 대해 지원 되는 Linux 및 FreeBSD virtual machines](https://technet.microsoft.com/library/dn531030.aspx)를 참조 하세요.  
   - **hv_vss_daemon**: 이 디먼은 라이브 Linux 가상 머신 백업을 만드는 데 필요 합니다.
   - **hv_kvp_daemon**: 이 데몬에는 내장 및 외부 키 값 쌍을 설정 하 고 쿼리할 수 있습니다.
   - **hv_fcopy_daemon**: 이 디먼은 호스트와 게스트 간에 서비스를 복사 하는 파일을 구현 합니다.  

### <a name="examples"></a>예

이 예에서는 `hv_kvp_daemon` 이라는 KVP 디먼을 중지 하 고 시작 하는 방법을 보여 줍니다.

1. 프로세스 ID \(PID @ no__t-1을 사용 하 여 디먼의 프로세스를 중지 합니다. PID를 찾으려면 출력의 두 번째 열을 확인 하거나 `pidof`을 사용 합니다. Hyper-v 디먼을 루트로 실행 하므로 루트 권한이 필요 합니다.

    ``` BASH
    sudo kill -15 `pidof hv_kvp_daemon`
    ```

1. 모든 `hv_kvp_daemon` 프로세스가 사라졌는지 확인 하려면 다음을 실행 합니다.

    ```
    ps -ef | hv
    ```

1. 디먼을 다시 시작 하려면 디먼을 루트로 실행 합니다.

    ``` BASH
    sudo hv_kvp_daemon
    ``` 

1. @No__t-0 프로세스가 새 프로세스 ID와 함께 나열 되는지 확인 하려면 다음을 실행 합니다.

    ```
    ps -ef | hv
    ```

## <a name="keep-integration-services-up-to-date"></a>Integration services를 최신 상태로 유지

가상 컴퓨터에 대 한 최상의 성능과 최신 기능을 얻으려면 통합 서비스를 최신 상태로 유지 하는 것이 좋습니다. 이는 Windows 업데이트에서 중요 한 업데이트를 가져오도록 설정 된 경우 대부분의 Windows 게스트에 대해 기본적으로 발생 합니다. 현재 커널을 사용 하는 Linux 게스트는 커널을 업데이트할 때 최신 통합 구성 요소를 받게 됩니다.

**Windows 10 호스트에서 실행되는 가상 컴퓨터:**

> [!NOTE]
> 이미지 파일 vmguest .iso는 더 이상 필요 하지 않기 때문에 Windows 10의 Hyper-v에 포함 되지 않습니다.

| 게스트  | 업데이트 메커니즘 | 참고 |
|:---------|:---------|:---------|
| Windows 10 | Windows 업데이트 | |
| Windows 8.1 | Windows 업데이트 | |
| Windows 8 | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows 7 | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows Vista(SP 2) | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| - | | |
| Windows Server 2016 | Windows 업데이트 | |
| Windows Server, 반기 채널 | Windows 업데이트 | |
| Windows Server 2012 R2 | Windows 업데이트 | |
| Windows Server 2012 | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows Server 2008 R2(SP 1) | Windows 업데이트 | 데이터 교환 통합 서비스가 필요합니다.* |
| Windows Server 2008(SP 2) | Windows 업데이트 | 확장 지원은 Windows Server 2016 에서만 지원 됩니다 ([자세히 읽기](https://support.microsoft.com/lifecycle?p1=12925)). |
| Windows Home Server 2011 | Windows 업데이트 | 는 Windows Server 2016에서 지원 되지 않습니다 ([자세한 내용은 참조](https://support.microsoft.com/lifecycle?p1=15820)). |
| Windows Small Business Server 2011 | Windows 업데이트 | 일반 지원에는 포함되지 않습니다([자세히 알아보기](https://support.microsoft.com/lifecycle?p1=15817)). |
| - | | |
| Linux 게스트 | 패키지 관리자 | Linux 용 Integration services는 배포판에 기본 제공 되지만 선택적 업데이트를 사용할 수 있습니다. ******** |

\* 데이터 교환 통합 서비스를 사용 하도록 설정할 수 없는 경우 [다운로드 센터](https://support.microsoft.com/kb/3071740) 에서 캐비닛 (cab) 파일로 해당 게스트에 대 한 통합 서비스를 사용할 수 있습니다. Cab 적용에 대 한 지침은이 [블로그 게시물](https://blogs.technet.com/b/virtualization/archive/2015/07/24/integration-components-available-for-virtual-machines-not-connected-to-windows-update.aspx)에서 확인할 수 있습니다.

**Windows 8.1 호스트에서 실행되는 가상 컴퓨터:**

| 게스트  | 업데이트 메커니즘 | 참고 |
|:---------|:---------|:---------|
| Windows 10 | Windows 업데이트 | |
| Windows 8.1 | Windows 업데이트 | |
| Windows 8 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows 7 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Vista(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows XP(SP 2, SP 3) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| - | | |
| Windows Server 2016 | Windows 업데이트 | |
| Windows Server, 반기 채널 | Windows 업데이트 | |
| Windows Server 2012 R2 | Windows 업데이트 | |
| Windows Server 2012 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Server 2008 R2 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Server 2008(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Home Server 2011 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Small Business Server 2011 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Server 2003 R2(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Server 2003(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| - | | |
| Linux 게스트 | 패키지 관리자 | Linux 용 Integration services는 배포판에 기본 제공 되지만 선택적 업데이트를 사용할 수 있습니다. ** |


**Windows 8 호스트에서 실행되는 가상 컴퓨터:**

| 게스트  | 업데이트 메커니즘 | 참고 |
|:---------|:---------|:---------|
| Windows 8.1 | Windows 업데이트 | |
| Windows 8 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows 7 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Vista(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows XP(SP 2, SP 3) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| - | | |
| Windows Server 2012 R2 | Windows 업데이트 | |
| Windows Server 2012 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Server 2008 R2 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요.|
| Windows Server 2008(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Home Server 2011 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Small Business Server 2011 | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Server 2003 R2(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| Windows Server 2003(SP 2) | 통합 서비스 디스크 | 아래 [지침](#install-or-update-integration-services)을 참조 하세요. |
| - | | |
| Linux 게스트 | 패키지 관리자 | Linux 용 Integration services는 배포판에 기본 제공 되지만 선택적 업데이트를 사용할 수 있습니다. ** |

Linux 게스트에 대 한 자세한 내용은 [Windows에서 hyper-v에 대해 지원 되는 linux 및 FreeBSD virtual machines](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows)를 참조 하세요.

## <a name="install-or-update-integration-services"></a>Integration services 설치 또는 업데이트

Windows Server 2016 및 Windows 10 이전 호스트의 경우 게스트 운영 체제에서 통합 서비스를 수동으로 설치 하거나 업데이트 해야 합니다. 
  
1.  Hyper-V 관리자를 엽니다. 서버 관리자 도구 메뉴에서 **Hyper-v 관리자**를 클릭 합니다.  
  
2.  가상 컴퓨터에 연결합니다. 가상 머신을 마우스 오른쪽 단추로 클릭 하 고 **연결**을 클릭 합니다.  
  
3.  가상 컴퓨터 연결의 작업 메뉴에서 **통합 서비스 설치 디스크 삽입**을 클릭합니다. 이렇게 하면 DVD 드라이브에 설치 디스크가 로드됩니다. 게스트 운영 체제에 따라 수동으로 설치를 시작 해야 할 수도 있습니다.  
  
4.  설치를 마치고 나면 모든 통합 서비스를 사용할 수 있습니다.

이러한 단계는 온라인 가상 컴퓨터에 대 한 Windows PowerShell 세션 내에서 자동화 하거나 완료할 수 없습니다. 오프 라인 VHDX 이미지에 적용할 수 있습니다. [이 블로그 게시물을 참조](https://blogs.technet.microsoft.com/virtualization/2013/04/18/how-to-install-integration-services-when-the-virtual-machine-is-not-running/)하세요.
