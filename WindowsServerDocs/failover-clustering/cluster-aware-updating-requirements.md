---
ms.assetid: 75cc1d24-fa2f-45bd-8f3b-1bbd4a1aead0
title: 클러스터 인식 업데이트 요구 사항 및 모범 사례
ms.prod: windows-server
ms.topic: article
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: 클러스터 인식 업데이트를 사용 하 여 Windows Server를 실행 하는 클러스터에 업데이트를 설치 하기 위한 요구 사항
ms.openlocfilehash: 501969fad2455195bca485bd8124911d6d75378e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361316"
---
# <a name="cluster-aware-updating-requirements-and-best-practices"></a>클러스터 인식 업데이트 요구 사항 및 모범 사례

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션에서는 CAU ( [클러스터 인식 업데이트](cluster-aware-updating.md) )를 사용 하 여 Windows Server를 실행 하는 장애 조치 (failover) 클러스터에 업데이트를 적용 하는 데 필요한 요구 사항 및 종속성을 설명 합니다.

> [!NOTE]  
> **Microsoft.windowsupdateplugin**이외의 플러그 인 @ no__t-0을 사용 하는 경우 클러스터 환경에서 업데이트를 적용할 준비가 되었는지 독립적으로 확인 해야 할 수 있습니다. 비 @ no__t-0Microsoft no__t-1in를 사용 하는 경우 자세한 내용은 게시자에 게 문의 하십시오. 플러그 @ no__t-0ins에 대 한 자세한 내용은 [플러그 인 @ no__t-2의 작동 방식](cluster-aware-updating-plug-ins.md)을 참조 하세요.   

## <a name="BKMK_REQ_CLUS"></a>장애 조치 (Failover) 클러스터링 기능 및 장애 조치 (Failover) 클러스터링 도구 설치  
CAU를 사용하려면 장애 조치(failover) 클러스터링 기능 및 장애 조치(failover) 클러스터링 도구를 설치해야 합니다. 장애 조치 (Failover) 클러스터링 도구에는 CAU 도구 @no__t -0clusterawareupdating @ no__t @, 장애 조치 (Failover) 클러스터링 cmdlet 및 기타 CAU 작업에 필요한 구성 요소가 포함 되어 있습니다. 장애 조치(failover) 클러스터링 기능을 설치하는 단계는 [장애 조치(failover) 클러스터링 기능 및 도구 설치](create-failover-cluster.md#install-the-failover-clustering-feature)를 참조하세요.  

장애 조치 (Failover) 클러스터링 도구에 대 한 정확한 설치 요구 사항은 CAU가 장애 조치 (failover) @no__t 클러스터의 클러스터 된 역할로 업데이트 하는지 여부에 따라 다릅니다. no__t-1 업데이트 모드 @ no__t-2를 사용 하거나 원격 컴퓨터에서 업데이트 합니다. 또한 CAU의 self @ no__t-0updating 모드를 사용 하려면 CAU 도구를 사용 하 여 장애 조치 (failover) 클러스터에 CAU 클러스터 된 역할을 설치 해야 합니다.    

다음 표에는 두 가지 CAU 업데이트 모드에 대한 CAU 기능 설치 요구 사항이 요약되어 있습니다.  

|설치된 구성 요소|Self @ no__t-0updating 모드|Remote @ no__t-0updating 모드|  
|-----------------------|-----------------------|-------------------------|  
|장애 조치(failover) 클러스터링 기능|모든 클러스터 노드에 필요|모든 클러스터 노드에 필요|  
|장애 조치(failover) 클러스터링 도구|모든 클러스터 노드에 필요|-원격 @ no__t-0 컴퓨터 업데이트에 필요 합니다.<br />- [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) cmdlet을 실행 하려면 모든 클러스터 노드에 필요 합니다.|  
|CAU 클러스터된 역할|필수|필요하지 않음|  

## <a name="obtain-an-administrator-account"></a>관리자 계정 얻기  
다음 관리자 요구 사항은 CAU 기능을 사용하는 데 필요합니다.  

-   CAU 사용자 인터페이스 \(UI @ no__t 또는 클러스터 인식 업데이트 cmdlet을 사용 하 여 업데이트 작업을 미리 보거나 적용 하려면 모든 클러스터 노드에서 로컬 관리자 권한 및 사용 권한이 있는 도메인 계정을 사용 해야 합니다. 계정에 모든 노드에 대 한 충분 한 권한이 없는 경우 클러스터 인식 업데이트 창에서 이러한 작업을 수행할 때 필요한 자격 증명을 제공 하 라는 메시지가 표시 됩니다. [클러스터 인식 업데이트](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps) cmdlet을 사용 하려면 필요한 자격 증명을 cmdlet 매개 변수로 제공할 수 있습니다.  

-   클러스터 노드에 대 한 로컬 관리자 권한 및 사용 권한이 없는 계정으로 로그인 하는 경우 원격 @ no__t-0updating 모드에서 CAU를 사용 하는 경우 업데이트에 대 한 로컬 관리자 계정을 사용 하 여 CAU 도구를 관리자 권한으로 실행 해야 합니다. 코디네이터 컴퓨터를 사용 하거나 **인증 후 클라이언트 가장** 사용자 권한이 있는 계정을 사용 하 여 사용 합니다. 

-   CAU 모범 사례 분석기를 실행 하려면 클러스터 노드에 대 한 관리 권한이 있는 계정을 사용 하 고 [test-causetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) cmdlet을 실행 하거나 클러스터 업데이트를 분석 하는 데 사용 되는 컴퓨터에 대 한 로컬 관리 권한을 사용 해야 합니다. 클러스터 인식 업데이트 창을 사용한 준비. 자세한 내용은 [클러스터 업데이트 준비 테스트](#BKMK_BPA)를 참조하세요.  

## <a name="verify-the-cluster-configuration"></a>클러스터 구성 확인  
다음은 CAU를 사용하여 업데이트를 지원하기 위한 장애 조치(failover) 클러스터에 대한 일반적인 요구 사항입니다. 노드의 원격 관리에 대한 추가 구성 요구 사항은 이 항목의 뒷부분에 있는 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 에 나와 있습니다.  

-   클러스터에 쿼럼에 있도록 충분한 클러스터 노드가 온라인 상태여야 합니다.  

-   모든 클러스터 노드가 동일한 Active Directory 도메인에 있어야 합니다.  

-   DNS를 사용하여 네트워크에서 클러스터 이름을 확인해야 합니다.  

-   CAU를 remote @ no__t-0updating 모드에서 사용 하는 경우 업데이트 코디네이터 컴퓨터는 장애 조치 (failover) 클러스터 노드에 네트워크로 연결 되어야 하 고 장애 조치 (failover) 클러스터와 동일한 Active Directory 도메인에 있어야 합니다.  

-   클러스터 서비스가 모든 클러스터 노드에서 실행되어야 합니다. 기본적으로 이 서비스는 모든 클러스터 노드에 설치되며 자동으로 시작하도록 구성됩니다.  

-   CAU 업데이트 실행 중 PowerShell을 사용 하 여 @ no__t-0update 또는 post @ no__t 업데이트 스크립트를 사용 하려면 모든 클러스터 노드에 스크립트가 설치 되어 있는지, 아니면 항상 사용 가능한 네트워크 파일 공유에서 모든 노드에 액세스할 수 있는지 확인 합니다. 스크립트가 네트워크 파일 공유에 저장된 경우 Everyone 그룹에 대한 읽기 권한 폴더를 구성합니다.  

## <a name="BKMK_NODE_CONFIG"></a>원격 관리를 위한 노드 구성  
클러스터 인식 업데이트를 사용 하려면 클러스터의 모든 노드를 원격 관리에 대해 구성 해야 합니다. 기본적으로 원격 관리를 위해 노드를 구성 하기 위해 수행 해야 하는 작업은 [자동 다시 시작을 허용 하는 방화벽 규칙을 사용 하도록 설정](#BKMK_FW)하는 것입니다. 

다음 표에서는 환경이 기본값에서 달라 지므로 하는 경우 전체 원격 관리 요구 사항을 보여 줍니다.

이러한 요구 사항은 [장애 조치(failover) 클러스터링 기능 및 장애 조치(failover) 클러스터링 도구 설치](#BKMK_REQ_CLUS)에 대한 설치 요구 사항과 이 항목의 이전 섹션에 설명된 일반 클러스터링 요구 사항에 추가됩니다.  

|요구 사항|기본 상태|Self @ no__t-0updating 모드|Remote @ no__t-0updating 모드|  
|---------------|---|-----------------------|-------------------------|  
|[자동 다시 시작을 허용 하도록 방화벽 규칙 설정](#BKMK_FW)|사용 안 함|방화벽을 사용하는 경우 모든 클러스터 노드에 필요|방화벽을 사용하는 경우 모든 클러스터 노드에 필요|  
|[WMI(Windows Management Instrumentation) 사용](#BKMK_WMI)|Enabled|모든 클러스터 노드에 필요|모든 클러스터 노드에 필요|  
|[Windows PowerShell 3.0 또는 4.0 및 Windows PowerShell 원격 기능 사용](#BKMK_PS)|Enabled|모든 클러스터 노드에 필요|모든 클러스터 노드에서 다음을 실행하는 데 필요<br /><br />- [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) cmdlet<br />-업데이트 실행 중에 PowerShell pre @ no__t-0update 및 post @ no__t-1update 스크립트<br />-클러스터 인식 업데이트 창이 나 [Test @ no__t-1CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Windows PowerShell cmdlet을 사용 하 여 클러스터 업데이트 준비 테스트|  
|[4.6 또는 4.5 .NET Framework 설치](#BKMK_NET)|Enabled|모든 클러스터 노드에 필요|모든 클러스터 노드에서 다음을 실행하는 데 필요<br /><br />- [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) cmdlet<br />-업데이트 실행 중에 PowerShell pre @ no__t-0update 및 post @ no__t-1update 스크립트<br />-클러스터 인식 업데이트 창이 나 [Test @ no__t-1CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Windows PowerShell cmdlet을 사용 하 여 클러스터 업데이트 준비 테스트|  

### <a name="BKMK_FW"></a>자동 다시 시작을 허용 하도록 방화벽 규칙 설정  
업데이트를 적용 한 후 자동 다시 시작을 허용 하려면 \(if를 설치 하는 경우 restart @ no__t-1을 사용 해야 하는 경우, Windows 방화벽이 나 no__t-2Microsoft 방화벽이 클러스터 노드에서 사용 되는 경우 허용 되는 각 노드에서 방화벽 규칙을 사용 하도록 설정 해야 합니다. 다음 트래픽:  

-   프로토콜: TCP  

-   방향: 인바운드  

-   프로그램: wininit.exe  

-   포트: RPC 동적 포트  

-   프로필: Domain  

클러스터 노드에서 Windows 방화벽을 사용하는 경우 각 클러스터 노드에서 **원격 종료** Windows 방화벽 규칙 그룹을 사용하도록 설정하면 됩니다. 클러스터 인식 업데이트 창을 사용 하 여 업데이트를 적용 하 고 자체 @ no__t-0updating 옵션을 구성 하는 경우 **원격 종료** Windows 방화벽 규칙 그룹이 각 클러스터 노드에서 자동으로 사용 하도록 설정 됩니다.  

> [!NOTE]  
> Windows 방화벽에 대해 구성된 그룹 정책 설정과 충돌하는 경우에는 **Remote Shutdown** Windows 방화벽 규칙 그룹을 사용할 수 없습니다.    

다음 CAU cmdlet을 실행할 때 **– EnableFirewallRules** 매개 변수를 지정 하 여 **원격 종료** 방화벽 규칙 그룹을 사용 하도록 설정할 수도 있습니다. [Add-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole?view=win10-ps), [Invoke-CauRun](https://docs.microsoft.com/powershell/module/clusterawareupdating/Invoke-CauRun?view=win10-ps) 및 [SetCauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole?view=win10-ps).  

다음 PowerShell 예제에서는 클러스터 노드에서 자동 다시 시작을 사용 하도록 설정 하는 추가 메서드를 보여 줍니다.  

```PowerShell  
Set-NetFirewallRule -Group "@firewallapi.dll,-36751" -Profile Domain -Enabled true  
```  

### <a name="BKMK_WMI"></a>WMI(Windows Management Instrumentation) 사용 (WMI) 
WMI(Windows Management Instrumentation) \(WMI @ no__t-1을 사용 하 여 원격 관리에 대해 모든 클러스터 노드를 구성 해야 합니다. 이 기능은 기본적으로 사용됩니다.  

수동으로 원격 관리를 사용하도록 설정하려면 다음을 수행합니다.  

1.  서비스 콘솔에서 **Windows 원격 관리** 서비스를 시작하고 시작 유형을 **자동**으로 설정합니다.  

2.  [Set-wsmanquickconfig](https://docs.microsoft.com/powershell/module/Microsoft.WsMan.Management/Set-WSManQuickConfig?view=powershell-6) cmdlet을 실행 하거나 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.  

    ```PowerShell  
    winrm quickconfig -q  
    ```  

WMI 원격을 지원 하려면 클러스터 노드에서 Windows 방화벽을 사용 하는 경우 **@ no__t-3의 Windows 원격 관리 \(HTTP @ no__t-2의** 인바운드 방화벽 규칙이 각 노드에서 사용 하도록 설정 되어야 합니다.  이 규칙은 기본적으로 사용됩니다.  

### <a name="BKMK_PS"></a>Windows PowerShell 및 Windows PowerShell 원격 기능 사용  
Self @ no__t-0updating 모드와 remote @ no__t 업데이트 모드의 특정 CAU 기능을 사용 하도록 설정 하려면 PowerShell을 설치 하 고 모든 클러스터 노드에서 원격 명령을 실행할 수 있도록 설정 해야 합니다. PowerShell은 기본적으로 설치 되 고 원격 기능을 사용 하도록 설정 됩니다.  

PowerShell 원격을 사용 하도록 설정 하려면 다음 방법 중 하나를 사용 합니다.  

-   [Enable-psremoting](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enable-PSRemoting) cmdlet을 실행 합니다.  

-   Windows 원격 관리 \(WinRM @ no__t-2에 대 한 도메인 @ no__t-0level 그룹 정책 설정을 구성 합니다.  

PowerShell 원격을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 [원격 요구 사항 정보](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements?view=powershell-6)를 참조 하세요.  

### <a name="BKMK_NET"></a>4.6 또는 4.5 .NET Framework 설치  
Self @ no__t-0updating 모드 및 remote @ no__t 업데이트 모드의 특정 CAU 기능을 사용 하려면 모든 클러스터 노드에 .NET Framework 4.6 또는 .NET Framework 4.5 (Windows Server 2012 R2)을 설치 해야 합니다. 기본적으로 NET Framework가 설치 되어 있습니다.  

PowerShell을 사용 하 여 .NET Framework 4.6 (또는 4.5)을 설치 하려면 다음 명령을 사용 합니다.

```PowerShell
Install-WindowsFeature -Name NET-Framework-45-Core
```

## <a name="BKMK_BEST_PRAC"></a>클러스터 인식 업데이트 사용에 대 한 모범 사례 권장 사항 

### <a name="BKMK_BP_WUA"></a>Microsoft 업데이트 적용에 대 한 권장 사항

클러스터의 기본 **microsoft.windowsupdateplugin** 플러그 @ no__t-1in를 사용 하 여 업데이트를 적용 하기 위해 CAU를 사용 하기 시작 하는 경우 다른 방법의 사용을 중지 하 여 클러스터 노드에 Microsoft의 소프트웨어 업데이트를 설치 하는 것이 좋습니다.  

> [!CAUTION]  
> 고정 시간 일정 @ no__t-1에서 자동 @no__t으로 개별 노드를 업데이트 하는 메서드와 CAU를 결합 하면 서비스 중단 및 계획 되지 않은 가동 중지 시간을 비롯 하 여 예기치 않은 결과가 발생할 수 있습니다.  

다음과 같은 지침을 따를 것을 권장합니다.  

-   최상의 결과를 얻으려면 제어판의 자동 업데이트 설정 또는 그룹 정책을 사용하여 구성된 설정 등을 통해 클러스터 노드에서 자동 업데이트 설정을 사용하지 않도록 설정하는 것이 좋습니다.  

    > [!CAUTION]  
    > 클러스터 노드의 업데이트 자동 설치는 CAU를 통한 업데이트 설치와 충돌할 수 있으며 이로 인해 CAU 오류가 발생할 수 있습니다.  

    자동 업데이트 설치가 필요한 경우 CAU와 호환되는 다음 자동 업데이트 설정을 사용하면 관리자가 업데이트 설치 시간을 제어할 수 있으므로 충돌이 발생하지 않습니다.  

    -   업데이트를 다운로드하기 전과 설치하기 전에 알림을 제공하는 설정  

    -   업데이트를 자동으로 다운로드하고 설치 전 알림을 제공하는 설정  

    그러나 자동 업데이트가 CAU 업데이트 실행과 동시에 업데이트를 다운로드하는 경우 업데이트 실행이 완료되는 데 시간이 더 오래 걸릴 수 있습니다.  

-   업데이트 시스템을 구성 하지 않습니다 (예: Windows Server Update Services \(WSUS @ no__t-1). 고정 시간 일정 @ no__t-3에서 클러스터 노드에 업데이트를 자동 @no__t으로 적용 합니다.  

-   모든 클러스터 노드가 동일한 업데이트 원본(예: WSUS 서버, Windows 업데이트 또는 Microsoft 업데이트)을 사용하도록 균일하게 구성되어야 합니다.  

-   네트워크의 컴퓨터에 소프트웨어 업데이트를 적용하는 구성 관리 시스템을 사용하는 경우 모든 필수 또는 자동 업데이트에서 클러스터 노드를 제외합니다. 구성 관리 시스템의 예를 들면 Microsoft System Center Configuration Manager 2007 및 Microsoft System Center Virtual Machine Manager 2008이 있습니다.  

-   예를 들어 내부 소프트웨어 배포 서버에서-0for 경우 WSUS 서버 @ no__t-1은 업데이트를 포함 하 고 배포 하는 데 사용 되며, 해당 서버가 클러스터 노드에 대해 승인 된 업데이트를 올바르게 식별 하는지 확인 합니다.  

#### <a name="BKMK_PROXY"></a>지점 시나리오에서 Microsoft 업데이트 적용  
특정 지점 시나리오에서 Microsoft 업데이트 또는 Windows 업데이트를 통해 클러스터 노드에 Microsoft 업데이트를 다운로드하려면 각 노드에서 로컬 시스템 계정에 대한 프록시 설정을 구성해야 할 수 있습니다. 예를 들어 지점 클러스터에서 로컬 프록시 서버를 통해 Microsoft 업데이트 또는 Windows 업데이트에 액세스하여 업데이트를 다운로드하는 경우 이러한 구성이 필요할 수 있습니다.  

필요한 경우 각 노드에서 WinHTTP 프록시 설정을 구성 하 여 로컬 프록시 서버를 지정 하 고 로컬 주소 예외 \(, 즉 로컬 주소에 대 한 바이패스 목록 @ no__t-1을 구성 합니다. 이렇게 하려면 각 클러스터 노드의 관리자 권한 명령 프롬프트에서 다음 명령을 실행하면 됩니다.  

```  
netsh winhttp set proxy <ProxyServerFQDN >:<port> "<local>"  
```  

여기서 <*Proxyserverfqdn*>는 프록시 서버에 대 한 정규화 된 도메인 이름이 고, <*포트*>는 통신할 포트 (일반적으로 포트 443)입니다.  

예를 들어 포트 443 및 로컬 주소 예외를 사용 하 여 프록시 서버 *MyProxy.CONTOSO.com*를 지정 하는 로컬 시스템 계정에 대해 WinHTTP 프록시 설정을 구성 하려면 다음 명령을 입력 합니다.  

```  
netsh winhttp set proxy MyProxy.CONTOSO.com:443 "<local>"  
```  

### <a name="BKMK_BP_HF"></a>Microsoft.hotfixplugin 사용에 대 한 권장 사항  

-   핫픽스 루트 폴더 및 핫픽스 구성 파일의 사용 권한을 이러한 파일을 저장하는 데 사용되는 컴퓨터의 로컬 관리자로만 쓰기 액세스를 제한하도록 구성하는 것이 좋습니다. 이렇게 하면 권한 없는 사용자가 이러한 파일을 변조하여 핫픽스가 적용될 때 장애 조치(failover) 클러스터의 기능을 손상시킬 수 있는 취약점을 방지할 수 있습니다.  

-   서버 메시지 @no__t 블록에 대 한 데이터 무결성을 보장 하려면 핫픽스 루트 폴더에 액세스 하는 데 사용 되는 smb (no__t) 연결에 대 한 smb 암호화를 구성 해야 할 수 있는 경우 smb 공유 폴더에 SMB 암호화를 구성 해야 합니다. **Microsoft.HotfixPlugin**을 사용하려면 SMB 연결에 대한 데이터 무결성을 보장하도록 SMB 서명 또는 SMB 암호화를 구성해야 합니다. 

    자세한 내용은 [핫픽스 루트 폴더 및 핫픽스 구성 파일에 대 한 액세스 제한을](cluster-aware-updating-plug-ins.md#BKMK_ACL)참조 하세요.

### <a name="additional-recommendations"></a>추가 권장 사항  

-   동시에 예약될 수 있는 CAU 업데이트 실행과의 충돌을 방지하기 위해 예약된 유지 관리 기간 동안 클러스터 이름 개체 및 가상 컴퓨터 개체에 대한 암호 변경을 예약하지 마세요.  

-   권한이 없는 사용자가 이러한 파일을 변조 하지 못하도록 네트워크 공유 폴더에 저장 된 사전 @ no__t-0update 및 post @ no__t 업데이트 스크립트에 대 한 적절 한 권한을 설정 해야 합니다.  

-   Self @ no__t-0updating 모드에서 CAU를 구성 하려면 Active Directory에서 CAU 클러스터 된 역할에 대 한 가상 컴퓨터 개체 \(VCO @ no__t-2를 만들어야 합니다. CAU는 장애 조치(failover) 클러스터에 충분한 권한이 있는 경우 CAU 클러스터된 역할이 추가될 때 이 개체를 자동으로 만들 수 있습니다. 그러나 특정 조직의 보안 정책으로 인해 Active Directory에서 개체를 미리 준비해야 할 수 있습니다. 이 작업을 수행하는 절차는 [클러스터된 역할에 대한 계정 사전 준비 단계](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731002\(v=ws.10\)#steps-for-prestaging-the-cluster-name-account)를 참조하세요.  

-   IT 조직에서 업데이트 실행 설정을 저장하여 업데이트 요구 사항이 유사한 장애 조치(failover) 클러스터 간에 다시 사용하려면 업데이트 실행 프로필을 만들면 됩니다. 또한 업데이트 모드에 따라 모든 원격 업데이트 코디네이터 컴퓨터 또는 장애 조치(failover) 클러스터에서 액세스할 수 있는 파일 공유에서 업데이트 실행 프로필을 저장하고 관리할 수 있습니다. 자세한 내용은 [고급 옵션 및 CAU에 대 한 실행 프로필 업데이트](cluster-aware-updating-options.md)를 참조 하세요.  

## <a name="BKMK_BPA"></a>클러스터 업데이트 준비 테스트  
CAU 모범 사례 분석기 \(BPA @ no__t 모델을 실행 하 여 장애 조치 (failover) 클러스터 및 네트워크 환경이 CAU에서 소프트웨어 업데이트를 적용 하는 데 필요한 많은 요구 사항을 충족 하는지 테스트할 수 있습니다. 많은 테스트에서 기본 플러그 인 @ no__t-0in, **microsoft.windowsupdateplugin**를 사용 하 여 microsoft 업데이트를 적용 하기 위해 환경에서 준비를 확인 합니다.  

> [!NOTE]  
> 클러스터 환경에서 **microsoft.windowsupdateplugin**이외의 플러그 @ no__t-0을 사용 하 여 소프트웨어 업데이트를 적용할 준비가 되었는지 독립적으로 확인 해야 할 수도 있습니다. 하드웨어 제조업체에서 제공 하는 것과 같은 no @ no__t-0Microsoft 플러그 @ no__t-1in를 사용 하는 경우 자세한 내용은 게시자에 게 문의 하십시오.  

다음 두 가지 방법으로 BPA를 실행할 수 있습니다.  

1.  CAU 콘솔에서 **클러스터 업데이트 준비 상태 분석** 을 선택합니다. BPA가 준비 테스트를 완료 하면 테스트 보고서가 나타납니다. 클러스터 노드에서 문제가 발견된 경우 수정 작업을 수행할 수 있도록 구체적인 문제와 함께 해당 문제가 발생한 노드가 식별됩니다. 테스트를 완료하는 데 몇 분 정도 걸릴 수 있습니다.  

2.  [Test-causetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup) cmdlet을 실행 합니다. Windows PowerShell 용 장애 조치 (Failover) 클러스터링 모듈 (장애 조치 (Failover) 클러스터링 도구의 일부)이 설치 된 로컬 또는 원격 컴퓨터에서 cmdlet을 실행할 수 있습니다. 또한 장애 조치(failover) 클러스터의 노드에서도 이 cmdlet을 실행할 수 있습니다.  

> [!NOTE]  
> -   클러스터 노드에 대 한 관리 권한이 있는 계정을 사용 하 고, **@ no__t-1CauSetup** cmdlet을 실행 하는 데 사용 되는 컴퓨터에 대 한 로컬 관리자 권한을 사용 하 고, 클러스터 인식을 사용 하 여 클러스터 업데이트 준비를 분석 해야 합니다. 창을 업데이트 하는 중입니다. 클러스터 인식 업데이트 창을 사용 하 여 테스트를 실행 하려면 필요한 자격 증명을 사용 하 여 컴퓨터에 로그온 해야 합니다.  
> -   테스트에서는 클러스터 업데이트 준비 상태를 테스트하는 데 사용된 것과 동일한 컴퓨터에서 동일한 사용자 자격 증명으로 소프트웨어 업데이트를 미리 보고 적용하는 데 사용되는 CAU 도구를 실행하는 것으로 가정합니다.  

> [!IMPORTANT]  
> 다음과 같은 경우 클러스터에서 업데이트 준비 상태를 테스트하는 것이 좋습니다.  
>   
> -   CAU를 사용하여 소프트웨어 업데이트를 처음으로 적용하기 전  
> -   클러스터에 노드를 추가하거나 클러스터에서 클러스터 유효성 검사 마법사를 실행해야 하는 다른 하드웨어 변경을 수행한 후  
> -   업데이트 원본을 변경 하거나 업데이트 설정이 나 구성을 변경한 후에는 노드에서 업데이트를 적용 하는 것에 영향을 줄 수 있는 CAU @ no__t-1 이외의 @no__t 합니다.  

### <a name="tests-for-cluster-updating-readiness"></a>클러스터 업데이트 준비 테스트  
다음 표에는 클러스터 업데이트 준비 테스트, 몇 가지 일반적인 문제 및 해결 단계가 나와 있습니다.  


|                                                      테스트                                                      |                                                                                                                                               가능한 문제 및 영향                                                                                                                                               |                                                                                                                                                                                         해결 단계                                                                                                                                                                                         |
|----------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                     장애 조치(failover) 클러스터를 사용할 수 있어야 함                                     |                                                                                       장애 조치(failover) 클러스터 이름을 확인할 수 없거나, 하나 이상의 클러스터 노드에 액세스할 수 없습니다. BPA에서 클러스터 준비 테스트를 실행할 수 없습니다.                                                                                        |                                                                   -BPA 실행 중에 지정 된 클러스터 이름의 철자를 확인 합니다.<br />-클러스터의 모든 노드가 온라인 상태이 고 실행 중인지 확인 합니다.<br />-구성 유효성 검사 마법사가 장애 조치 (failover) 클러스터에서 성공적으로 실행 될 수 있는지 확인 합니다.                                                                    |
|                    장애 조치(failover) 클러스터 노드에서 WMI를 통해 원격 관리를 사용할 수 있어야 함                    |                                                하나 이상의 장애 조치 (failover) 클러스터 노드가 WMI(Windows Management Instrumentation) \(WMI @ no__t-1을 사용 하 여 원격 관리에 대해 사용 하도록 설정 되어 있지 않습니다. 노드에 원격 관리가 구성되지 않은 경우 CAU에서 클러스터 노드를 업데이트할 수 없습니다.                                                 |                                                                                                  모든 장애 조치(failover) 클러스터 노드에서 WMI를 통해 원격 관리를 사용할 수 있는지 확인합니다. 자세한 내용은 이 항목의 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 를 참조하세요.                                                                                                   |
|                      각 장애 조치 (failover) 클러스터 노드에서 PowerShell 원격을 사용 하도록 설정 해야 합니다.                       |                                                           PowerShell이 설치 되어 있지 않거나 하나 이상의 장애 조치 (failover) 클러스터 노드에서 원격 기능을 사용할 수 없습니다. CAU는 self @ no__t-0updating 모드에 대해 구성 하거나 원격 @ no__t-1 업데이트 모드의 특정 기능을 사용할 수 없습니다.                                                            |                                                                                             PowerShell이 모든 클러스터 노드에 설치 되어 있고 원격 기능을 사용 하도록 설정 되어 있는지 확인 합니다.<br /><br />자세한 내용은 이 항목의 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 를 참조하세요.                                                                                             |
|                                            장애 조치(failover) 클러스터 버전                                            |                                                                            장애 조치 (failover) 클러스터에 있는 하나 이상의 노드가 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하지 않습니다. CAU에서 장애 조치(failover) 클러스터를 업데이트할 수 없습니다.                                                                             |                                                                   BPA 실행 중에 지정한 장애 조치 (failover) 클러스터가 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하 고 있는지 확인 합니다.<br /><br />자세한 내용은 이 항목의 [클러스터 구성 확인](#BKMK_REQ_CLUS) 를 참조하세요.                                                                   |
| 필요한 버전의 .NET Framework 및 Windows PowerShell이 모든 장애 조치(failover) 클러스터 노드에 설치되어 있어야 함 |                                                                                              .NET Framework 4.6, 4.5 또는 Windows PowerShell이 하나 이상의 클러스터 노드에 설치 되어 있지 않습니다. 일부 CAU 기능이 작동하지 않을 수 있습니다.                                                                                              |                                                                            .NET Framework 4.6 또는 4.5 및 Windows PowerShell이 필요한 경우 모든 클러스터 노드에 설치 되어 있는지 확인 합니다.<br /><br />자세한 내용은 이 항목의 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 를 참조하세요.                                                                             |
|                           클러스터 서비스가 모든 클러스터 노드에서 실행되어야 함                           |                                                                                                            하나 이상의 노드에서 클러스터 서비스가 실행되지 않습니다. CAU에서 장애 조치(failover) 클러스터를 업데이트할 수 없습니다.                                                                                                             |                        -클러스터 서비스 \(clussvc @ no__t-1이 클러스터의 모든 노드에서 시작 되 고 자동으로 시작 되도록 구성 되어 있는지 확인 합니다.<br />-구성 유효성 검사 마법사가 장애 조치 (failover) 클러스터에서 성공적으로 실행 될 수 있는지 확인 합니다.<br /><br />자세한 내용은 이 항목의 [클러스터 구성 확인](#BKMK_REQ_CLUS) 를 참조하세요.                         |
|     장애 조치(failover) 클러스터 노드에 업데이트를 자동으로 설치하도록 자동 업데이트를 구성해서는 안 됨     |                                           하나 이상의 장애 조치(failover) 클러스터 노드에 Microsoft 업데이트를 자동으로 설치하도록 자동 업데이트가 구성되어 있습니다. CAU를 다른 업데이트 방법과 함께 사용하면 계획되지 않은 가동 중지 시간 또는 예기치 않은 결과가 발생할 수 있습니다.                                            |                                                     Windows 업데이트 기능이 하나 이상의 클러스터 노드에서 자동 업데이트에 대해 구성된 경우 자동 업데이트가 업데이트를 자동으로 설치하도록 구성되어 있지 않은지 확인합니다.<br /><br />자세한 내용은 [Microsoft 업데이트 적용에 대한 권장 사항](#BKMK_BP_WUA)를 참조하세요.                                                     |
|                          장애 조치(failover) 클러스터 노드에서 동일한 업데이트 원본을 사용해야 함                          |                                                    하나 이상의 장애 조치(failover) 클러스터 노드가 Microsoft 업데이트에 대해 나머지 노드와 다른 업데이트 원본을 사용하도록 구성되어 있습니다. CAU에서 클러스터 노드에 업데이트를 균일하게 적용하지 못할 수 있습니다.                                                    |                                                                        모든 클러스터 노드가 동일한 업데이트 원본(예: WSUS 서버, Windows 업데이트 또는 Microsoft 업데이트)을 사용하도록 균일하게 구성되어 있는지 확인합니다.<br /><br />자세한 내용은 [Microsoft 업데이트 적용에 대한 권장 사항](#BKMK_BP_WUA)를 참조하세요.                                                                         |
|       장애 조치(failover) 클러스터의 각 노드에 원격 종료를 허용하는 방화벽 규칙이 설정되어 있어야 함       |                 하나 이상의 장애 조치(failover) 클러스터 노드에 원격 종료를 허용하는 방화벽 규칙이 설정되어 있지 않거나, 그룹 정책 설정이 이 규칙의 사용을 차단합니다. 노드를 자동으로 다시 시작해야 하는 업데이트를 적용하는 업데이트 실행이 제대로 완료되지 않을 수 있습니다.                  |                                                                    클러스터 노드에서 Windows 방화벽 또는 비 @ no__t-0Microsoft 방화벽을 사용 하는 경우 원격 종료를 허용 하는 방화벽 규칙을 구성 합니다.<br /><br />자세한 내용은 이 항목의 [자동 다시 시작을 허용하도록 방화벽 규칙 설정](#BKMK_FW) 를 참조하세요.                                                                    |
|          각 장애 조치(failover) 클러스터 노드의 프록시 서버 설정이 로컬 프록시 서버로 설정되어야 함          |                             하나 이상의 장애 조치(failover) 클러스터 노드에 잘못된 프록시 서버 구성이 있습니다.<br /><br />로컬 프록시 서버를 사용하는 경우 클러스터에서 Windows 업데이트 또는 Microsoft 업데이트에 액세스할 수 있도록 각 노드의 프록시 서버 설정을 올바르게 구성해야 합니다.                              |                                            각 클러스터 노드의 WinHTTP 프록시(필요한 경우) 설정이 로컬 프록시 서버로 설정되어 있는지 확인합니다. 환경에서 프록시 서버를 사용하지 않는 경우에는 이 경고를 무시해도 됩니다.<br /><br />자세한 내용은 이 항목에서 [지점 시나리오에서 업데이트 적용](#BKMK_PROXY)을 참조하세요.                                            |
|        셀프 @ no__t-0updating 모드를 사용 하려면 CAU 클러스터 된 역할이 장애 조치 (failover) 클러스터에 설치 되어 있어야 합니다.        |                                                                                                   CAU 클러스터된 역할이 이 장애 조치(failover) 클러스터에 설치되어 있지 않습니다. 이 역할은 cluster self @ no__t-0updating에 필요 합니다.                                                                                                   |      Self @ no__t-0updating 모드에서 CAU를 사용 하려면 다음 방법 중 하나로 장애 조치 (failover) 클러스터에 CAU 클러스터 된 역할을 추가 합니다.<br /><br />- [Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole) PowerShell cmdlet을 실행 합니다.<br />-클러스터 인식 업데이트 창의 **cluster self @ no__t-1updating 옵션 구성** 작업을 선택 합니다.      |
|         셀프 @ no__t-0updating 모드를 사용 하도록 설정 하려면 장애 조치 (failover) 클러스터에서 CAU 클러스터 된 역할을 사용 하도록 설정 해야 합니다.         | CAU 클러스터된 역할을 사용할 수 없습니다. 예를 들어 CAU 클러스터 된 역할이 설치 되어 있지 않거나 [Disable @ no__t-1CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole) PowerShell cmdlet을 사용 하 여 사용 하지 않도록 설정 되었습니다. 이 역할은 cluster self @ no__t-0updating에 필요 합니다. | Self @ no__t-0updating 모드에서 CAU를 사용 하려면 다음 방법 중 하나로이 장애 조치 (failover) 클러스터에서 CAU 클러스터 된 역할을 사용 하도록 설정 합니다.<br /><br />- [Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole) PowerShell cmdlet을 실행 합니다.<br />-클러스터 인식 업데이트 창의 **cluster self @ no__t-1updating 옵션 구성** 작업을 선택 합니다. |
|      셀프 @ no__t-1updating 모드에 대해 구성 된 CAU 플러그 @ no__t-0in은 모든 장애 조치 (failover) 클러스터 노드에 등록 해야 합니다.      |                                                              이 장애 조치 (failover) 클러스터의 노드 하나 이상에서 CAU 클러스터 된 역할은 셀프 @ no__t-1 업데이트 옵션에 구성 된 모듈의 CAU 플러그 @ no__t-0에 액세스할 수 없습니다. Self @ no__t-0updating 실행이 실패할 수 있습니다.                                                              |           -CAU 플러그 인 @ no__t-1in를 제공 하는 제품에 대 한 설치 절차를 수행 하 여 구성 된 CAU 플러그 인 @ no__t-0in이 모든 클러스터 노드에 설치 되어 있는지 확인 합니다.<br />- [Register @ no__t-1CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) PowerShell cmdlet을 실행 하 여 필요한 클러스터 노드에 플러그 인 @ no__t-2를 등록 합니다.           |
|                모든 장애 조치 (failover) 클러스터 노드에는 동일한 등록 된 CAU 플러그 인 @ no__t-0ins 집합이 있어야 합니다.                 |                                                                             업데이트 실행에 사용 하도록 구성 된 플러그 @ no__t-1in가 모든 클러스터 노드에서 사용할 수 없는 것으로 변경 되 면 self @ no__t-0updating 실행에 실패할 수 있습니다.                                                                              |           -CAU 플러그 인 @ no__t-1in를 제공 하는 제품에 대 한 설치 절차를 수행 하 여 구성 된 CAU 플러그 인 @ no__t-0in이 모든 클러스터 노드에 설치 되어 있는지 확인 합니다.<br />- [Register @ no__t-1CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) PowerShell cmdlet을 실행 하 여 필요한 클러스터 노드에 플러그 인 @ no__t-2를 등록 합니다.           |
|                               구성된 업데이트 실행 옵션이 유효해야 함                                |                                                                          이 장애 조치 (failover) 클러스터에 대해 구성 된 self @ no__t-0updating 예약 및 업데이트 실행 옵션이 완전 하지 않거나 유효 하지 않습니다. Self @ no__t-0updating 실행이 실패할 수 있습니다.                                                                           |                                                            올바른 self @ no__t-0updating 일정 및 업데이트 실행 옵션 집합을 구성 합니다. 예를 들어 [Set @ no__t-1CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole) PowerShell cmdlet을 사용 하 여 CAU 클러스터 된 역할을 구성할 수 있습니다.                                                            |
|                  둘 이상의 장애 조치(failover) 클러스터 노드가 CAU 클러스터된 역할의 소유자여야 함                  |                                                                                        CAU 클러스터 된 역할에 이동할 수 있는 소유자 노드가 없으므로 self @ no__t-0updating 모드로 시작 된 업데이트 실행이 실패 합니다.                                                                                         |                                                                                                                장애 조치(failover) 클러스터링 도구를 사용하여 모든 클러스터 노드가 CAU 클러스터된 역할의 가능한 소유자로 구성되어 있는지 확인합니다. 이는 기본 구성입니다.                                                                                                                |
|                  모든 장애 조치(failover) 클러스터 노드에서 Windows PowerShell 스크립트에 액세스할 수 있어야 함                  |                                                                        CAU 클러스터 된 역할의 모든 가능한 소유자 노드에서 구성 된 Windows PowerShell 사전 @ no__t-0update 및 post @ no__t 업데이트 스크립트에 액세스할 수 있는 것은 아닙니다. Self @ no__t-0updating 실행이 실패 합니다.                                                                        |                                                                                                                    CAU 클러스터 된 역할의 모든 가능한 소유자 노드에 구성 된 PowerShell 사전 @ no__t-0update 및 post @ no__t 업데이트 스크립트에 액세스할 수 있는 권한이 있는지 확인 하십시오.                                                                                                                     |
|                   모든 장애 조치(failover) 클러스터 노드에서 동일한 Windows PowerShell 스크립트를 사용해야 함                   |                                                     CAU 클러스터 된 역할의 모든 가능한 소유자 노드에서 지정 된 Windows PowerShell 사전 @ no__t-0update 및 post @ no__t 업데이트 스크립트의 동일한 복사본을 사용 하는 것은 아닙니다. Self @ no__t-0updating 실행이 실패 하거나 예기치 않은 동작이 표시 될 수 있습니다.                                                     |                                                                                                                                   CAU 클러스터 된 역할의 모든 가능한 소유자 노드가 동일한 PowerShell pre @ no__t-0update 및 post @ no__t 업데이트 스크립트를 사용 하는지 확인 합니다.                                                                                                                                   |
|         업데이트 실행에 대해 지정된 WarnAfter 설정이 StopAfter 설정보다 작아야 함         |                                                                           지정된 CAU 업데이트 실행 제한 시간 값으로 인해 경고 제한 시간이 무효화됩니다. 경고 이벤트 로그가 생성되기 전에 업데이트 실행이 취소될 수도 있습니다.                                                                            |                                                                                                                                      업데이트 실행 옵션에서 **WarnAfter** 옵션 값을 **StopAfter** 옵션 값보다 작은 값으로 구성합니다.                                                                                                                                       |

## <a name="see-also"></a>참조  

-   [클러스터 인식 업데이트 개요](cluster-aware-updating.md)