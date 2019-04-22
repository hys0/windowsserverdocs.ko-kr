---
ms.assetid: 75cc1d24-fa2f-45bd-8f3b-1bbd4a1aead0
title: 클러스터 인식 업데이트 요구 사항 및 모범 사례
ms.prod: windows-server-threshold
ms.topic: article
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 08/06/2018
description: 클러스터 인식 업데이트를 사용 하 여 Windows Server를 실행 하는 클러스터에 업데이트를 설치 하는 것에 대 한 요구 사항입니다.
ms.openlocfilehash: 379c3caa39b09e8a912150f2423190e143991c05
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819734"
---
# <a name="cluster-aware-updating-requirements-and-best-practices"></a>클러스터 인식 업데이트 요구 사항 및 모범 사례

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션에서는 요구 사항 및 사용 하는 데 필요한 종속성을 설명 [Cluster-aware Updating](cluster-aware-updating.md) (CAU) Windows Server를 실행 하는 장애 조치 클러스터에 업데이트를 적용 합니다.
  
> [!NOTE]  
> 독립적으로 확인 클러스터 환경이 업데이트를 적용할 준비가 된 플러그 인을 사용 하는 경우는 해야 할 수 있습니다\-보다 다른 **Microsoft.WindowsUpdatePlugin**합니다. 비 사용 하는 경우\-Microsoft 플러그\-, 자세한 내용은 게시자에 게 문의 합니다. 플러그 인에 대 한 자세한 내용은\-기능을 참조 하세요 [연결 하는 방법\-기능 작동](cluster-aware-updating-plug-ins.md)합니다.   
  
## <a name="BKMK_REQ_CLUS"></a>장애 조치 클러스터링 기능 및 장애 조치 클러스터링 도구 설치  
CAU를 사용하려면 장애 조치(failover) 클러스터링 기능 및 장애 조치(failover) 클러스터링 도구를 설치해야 합니다. 장애 조치 클러스터링 도구는 CAU 도구를 포함 \(clusterawareupdating.dll\), 장애 조치 클러스터링 cmdlet 및 CAU 작업에 필요한 기타 구성 요소입니다. 장애 조치(failover) 클러스터링 기능을 설치하는 단계는 [장애 조치(failover) 클러스터링 기능 및 도구 설치](create-failover-cluster.md#install-the-failover-clustering-feature)를 참조하세요.  
  
장애 조치 클러스터링 도구에 대 한 정확한 설치 요구 사항은 CAU 클러스터 된 역할 장애 조치 클러스터로 업데이트를 조정 하는 여부에 따라 달라 집니다 \(자체를 사용 하 여\-업데이트 모드\) 또는 원격 컴퓨터에서. 자체\-CAU 도구를 사용 하 여 장애 조치 클러스터에서 CAU 클러스터 된 역할을 설치 해야 또한 CAU의 모드를 업데이트 합니다.    
  
다음 표에는 두 가지 CAU 업데이트 모드에 대한 CAU 기능 설치 요구 사항이 요약되어 있습니다.  
  
|설치된 구성 요소|자체\-업데이트 모드|원격\-업데이트 모드|  
|-----------------------|-----------------------|-------------------------|  
|장애 조치(failover) 클러스터링 기능|모든 클러스터 노드에 필요|모든 클러스터 노드에 필요|  
|장애 조치(failover) 클러스터링 도구|모든 클러스터 노드에 필요|필요한 원격\-컴퓨터를 업데이트 하는 중<br />-모든 클러스터 노드에서 실행 해야 합니다 [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) cmdlet|  
|CAU 클러스터된 역할|필수|필요하지 않음|  
  
## <a name="obtain-an-administrator-account"></a>관리자 계정 얻기  
다음 관리자 요구 사항은 CAU 기능을 사용하는 데 필요합니다.  
  
-   CAU 사용자 인터페이스를 사용 하 여 업데이트 작업을 적용 하거나 미리 \(UI\) 클러스터 인식 업데이트 cmdlet은 모든 클러스터 노드에서 로컬 관리자 권한 및 사용 권한이 있는 도메인 계정을 사용 해야 합니다. 계정에는 모든 노드에 충분 한 권한이 없는, 메시지가 표시 됩니다 Cluster-aware Updating 창에서 이러한 작업을 수행할 때 필요한 자격 증명을 제공 합니다. 사용 하는 [Cluster-aware Updating](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps) cmdlet에 필요한 자격 증명을 cmdlet 매개 변수로 제공할 수 있습니다.  
  
-   CAU를 사용 하 여 원격에서 경우\-클러스터 노드에서 로컬 관리자 권한이 없는 계정으로 로그인 하는 경우 업데이트 모드를 실행 해야 합니다 CAU 도구를 관리자 권한으로의 로컬 관리자 계정을 사용 합니다 업데이트 코디네이터 컴퓨터 또는 있는 계정을 사용 하 여 합니다 **인증 후 클라이언트 가장** 사용자 권한이 있습니다. 
  
-   CAU 모범 사례 분석기를 실행 하려면 클러스터 노드의 관리 권한 및 실행에 사용 되는 컴퓨터의 로컬 관리 권한이 있는 계정을 사용 해야 합니다 [Test-causetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) cmdlet 이나 분석 클러스터 업데이트 준비 Cluster-aware Updating 창을 사용 하 여 합니다. 자세한 내용은 [클러스터 업데이트 준비 테스트](#BKMK_BPA)를 참조하세요.  
  
## <a name="verify-the-cluster-configuration"></a>클러스터 구성 확인  
다음은 CAU를 사용하여 업데이트를 지원하기 위한 장애 조치(failover) 클러스터에 대한 일반적인 요구 사항입니다. 노드의 원격 관리에 대한 추가 구성 요구 사항은 이 항목의 뒷부분에 있는 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 에 나와 있습니다.  
  
-   클러스터에 쿼럼에 있도록 충분한 클러스터 노드가 온라인 상태여야 합니다.  
  
-   모든 클러스터 노드가 동일한 Active Directory 도메인에 있어야 합니다.  
  
-   DNS를 사용하여 네트워크에서 클러스터 이름을 확인해야 합니다.  
  
-   원격에 CAU를 사용 하면\-업데이트 코디네이터 컴퓨터의 네트워크 연결 장애 조치 클러스터 노드에 있어야 합니다. 모드 업데이트 및 장애 조치 클러스터와 동일한 Active Directory 도메인에 있어야 합니다.  
  
-   클러스터 서비스가 모든 클러스터 노드에서 실행되어야 합니다. 기본적으로 이 서비스는 모든 클러스터 노드에 설치되며 자동으로 시작하도록 구성됩니다.  
  
-   이전 PowerShell 버전을 사용 하도록\-업데이트나 게시\-CAU 업데이트 실행 중 스크립트를 업데이트, 모든 클러스터 노드에 스크립트가 설치 되어 있는지 또는 항상 사용 가능한 네트워크 파일 공유에 예를 들어 모든 노드에 액세스할 수 있는지 확인 합니다. 스크립트가 네트워크 파일 공유에 저장된 경우 Everyone 그룹에 대한 읽기 권한 폴더를 구성합니다.  
  
## <a name="BKMK_NODE_CONFIG"></a>원격 관리를 위한 노드 구성  
클러스터 인식 업데이트를 사용 하려면 모든 클러스터 노드의 원격 관리를 위해 구성 되어야 합니다. 기본적으로 태스크만 수행 해야 원격 관리에 대 한 노드를 구성할 [자동 다시 시작을 허용 하도록 방화벽 규칙 설정](#BKMK_FW)합니다. 

다음 표에서 기본값에서 달라 지므로 환경의 경우 완전 한 원격 관리 요구 사항을 나열 합니다.

이러한 요구 사항은 [장애 조치(failover) 클러스터링 기능 및 장애 조치(failover) 클러스터링 도구 설치](#BKMK_REQ_CLUS)에 대한 설치 요구 사항과 이 항목의 이전 섹션에 설명된 일반 클러스터링 요구 사항에 추가됩니다.  
  
|요구 사항|기본 상태|자체\-업데이트 모드|원격\-업데이트 모드|  
|---------------|---|-----------------------|-------------------------|  
|[자동 다시 시작을 허용 하도록 방화벽 규칙 설정](#BKMK_FW)|사용 안 함|방화벽을 사용하는 경우 모든 클러스터 노드에 필요|방화벽을 사용하는 경우 모든 클러스터 노드에 필요|  
|[Windows Management Instrumentation 사용](#BKMK_WMI)|Enabled|모든 클러스터 노드에 필요|모든 클러스터 노드에 필요|  
|[Windows PowerShell 3.0 또는 4.0 및 Windows PowerShell 원격 사용](#BKMK_PS)|Enabled|모든 클러스터 노드에 필요|모든 클러스터 노드에서 다음을 실행하는 데 필요<br /><br />- [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) cmdlet<br />PowerShell이 사전\-업데이트 및 게시\-업데이트 실행 중 스크립트 업데이트<br />-클러스터 업데이트 준비 Cluster-aware Updating 창을 사용 하 여 테스트 또는 [테스트\-CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Windows PowerShell cmdlet|  
|[.NET Framework 4.6 또는 4.5를 설치 합니다.](#BKMK_NET)|Enabled|모든 클러스터 노드에 필요|모든 클러스터 노드에서 다음을 실행하는 데 필요<br /><br />- [Save-caudebugtrace](https://docs.microsoft.com/powershell/module/clusterawareupdating/Save-CauDebugTrace?view=win10-ps) cmdlet<br />PowerShell이 사전\-업데이트 및 게시\-업데이트 실행 중 스크립트 업데이트<br />-클러스터 업데이트 준비 Cluster-aware Updating 창을 사용 하 여 테스트 또는 [테스트\-CauSetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup?view=win10-ps) Windows PowerShell cmdlet|  

### <a name="BKMK_FW"></a>자동 다시 시작을 허용 하도록 방화벽 규칙 설정  
업데이트가 적용 된 후 자동으로 다시 시작을 허용 하도록 \(업데이트의 설치 다시 시작이 필요한\)이면 Windows 방화벽 또는 비\-Microsoft 방화벽은 클러스터 노드에서 사용 되 고 방화벽 규칙에서 사용할 수 있어야 합니다 다음 트래픽을 허용 하는 각 노드:  
  
-   프로토콜: TCP  
  
-   방향: 인바운드  
  
-   프로그램: wininit.exe  
  
-   포트: RPC 동적 포트  
  
-   프로필: 도메인  
  
클러스터 노드에서 Windows 방화벽을 사용하는 경우 각 클러스터 노드에서 **원격 종료** Windows 방화벽 규칙 그룹을 사용하도록 설정하면 됩니다. 업데이트를 적용 하 고 자체를 구성 하는 클러스터 인식 업데이트 창 사용 하는 경우\-옵션을 업데이트 합니다 **원격 종료** Windows 방화벽 규칙 그룹이 각 클러스터 노드에서 자동으로 사용 됩니다.  
  
> [!NOTE]  
> Windows 방화벽에 대해 구성된 그룹 정책 설정과 충돌하는 경우에는 **Remote Shutdown** Windows 방화벽 규칙 그룹을 사용할 수 없습니다.    
  
**Remote Shutdown** 지정 하 여 방화벽 규칙 그룹도 사용 합니다 **– EnableFirewallRules** 다음 CAU cmdlet을 실행 하는 경우 매개 변수: Add-CauClusterRole, [Invoke-CauRun](https://docs.microsoft.com/powershell/module/clusterawareupdating/Invoke-CauRun?view=win10-ps) 및 [SetCauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole?view=win10-ps).  
  
다음 PowerShell 예제에서는 클러스터 노드에서 자동 다시 시작을 사용 하도록 설정 하는 추가 메서드를 보여 줍니다.  
  
```PowerShell  
Set-NetFirewallRule -Group "@firewallapi.dll,-36751" -Profile Domain -Enabled true  
```  

### <a name="BKMK_WMI"></a>Windows Management Instrumentation (WMI)를 사용 하도록 설정 
Windows Management Instrumentation을 사용 하 여 원격 관리에 대 한 모든 클러스터 노드를 구성 해야 합니다 \(WMI\)합니다. 이 기능은 기본적으로 사용됩니다.  
  
수동으로 원격 관리를 사용하도록 설정하려면 다음을 수행합니다.  
  
1.  서비스 콘솔에서 **Windows 원격 관리** 서비스를 시작하고 시작 유형을 **자동**으로 설정합니다.  
  
2.  실행 합니다 [Set-wsmanquickconfig](https://docs.microsoft.com/powershell/module/Microsoft.WsMan.Management/Set-WSManQuickConfig?view=powershell-6) 프롬프트 cmdlet을 사용 하거나 관리자 권한 명령에서 다음 명령 실행 합니다.  
  
    ```PowerShell  
    winrm quickconfig -q  
    ```  
  
Windows 방화벽을 클러스터 노드에서 사용 중인 경우 WMI 원격을 수에 대 한 인바운드 방화벽 규칙이 **Windows Remote Management \(HTTP\-에서\)**  각 노드에서 사용 하도록 설정 해야 합니다.  이 규칙은 기본적으로 사용됩니다.  
  
### <a name="BKMK_PS"></a>Windows PowerShell 및 Windows PowerShell 원격 사용  
자체를 사용 하도록 설정 하려면\-모드 및 원격의 특정 CAU 기능 업데이트\-업데이트 모드에서 PowerShell 해야 설치 하 고 모든 클러스터 노드에 원격 명령을 실행할 수 있도록 설정 합니다. 기본적으로 PowerShell가 설치 및 원격 활성화 됩니다.  
  
PowerShell 원격을 사용 하도록 설정 하려면 다음 방법 중 하나를 사용 합니다.  
  
-   실행 합니다 [Enable-psremoting](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enable-PSRemoting) cmdlet.  
  
-   도메인을 구성\-수준의 Windows 원격 관리를 위한 그룹 정책 설정을 \(WinRM\)합니다.  
  
PowerShell 원격을 사용 하도록 설정 하는 방법에 대 한 자세한 내용은 참조 하세요. [에 대 한 원격 요구 사항](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_remote_requirements?view=powershell-6)합니다.  
  
### <a name="BKMK_NET"></a>.NET Framework 4.6 또는 4.5를 설치 합니다.  
자체를 사용 하도록 설정 하려면\-모드 및 원격의 특정 CAU 기능 업데이트\-업데이트 모드,.NET Framework 4.6 또는.NET Framework 4.5 (Windows Server 2012 R2)에서 모든 클러스터 노드에 설치 해야 합니다. 기본적으로.NET Framework 설치 됩니다.  

설치 되어 있지 않은 경우 PowerShell을 사용 하 여.NET Framework 4.6 (또는 4.5)를 설치 하려면 다음 명령을 사용 합니다.

```PowerShell
Install-WindowsFeature -Name NET-Framework-45-Core
```

## <a name="BKMK_BEST_PRAC"></a>모범 사례 클러스터 인식 업데이트 사용에 대 한 권장 사항 
  
### <a name="BKMK_BP_WUA"></a>Microsoft 업데이트 적용에 대 한 권장 사항

좋습니다, CAU를 사용 하 여 기본값을 사용 하 여 업데이트를 적용 하기 시작 하면 **Microsoft.WindowsUpdatePlugin** 플러그 인\-에서는 클러스터에서 중지 다른 메서드를 사용 하 여 클러스터에서 Microsoft의 소프트웨어 업데이트를 설치 하려면 노드입니다.  
  
> [!CAUTION]  
> 개별 노드를 자동으로 업데이트 하는 메서드를 사용 하 여 CAU 결합 \(고정 된 시간 일정에 따라\) 중단을 포함 하 여 서비스 및 계획 되지 않은 가동 중지 시간을 예측할 수 없는 결과가 발생할 수 있습니다.  
  
다음과 같은 지침을 따를 것을 권장합니다.  
  
-   최상의 결과를 얻으려면 제어판의 자동 업데이트 설정 또는 그룹 정책을 사용하여 구성된 설정 등을 통해 클러스터 노드에서 자동 업데이트 설정을 사용하지 않도록 설정하는 것이 좋습니다.  
  
    > [!CAUTION]  
    > 클러스터 노드의 업데이트 자동 설치는 CAU를 통한 업데이트 설치와 충돌할 수 있으며 이로 인해 CAU 오류가 발생할 수 있습니다.  
  
    자동 업데이트 설치가 필요한 경우 CAU와 호환되는 다음 자동 업데이트 설정을 사용하면 관리자가 업데이트 설치 시간을 제어할 수 있으므로 충돌이 발생하지 않습니다.  
  
    -   업데이트를 다운로드하기 전과 설치하기 전에 알림을 제공하는 설정  
  
    -   업데이트를 자동으로 다운로드하고 설치 전 알림을 제공하는 설정  
  
    그러나 자동 업데이트가 CAU 업데이트 실행과 동시에 업데이트를 다운로드하는 경우 업데이트 실행이 완료되는 데 시간이 더 오래 걸릴 수 있습니다.  
  
-   Windows Server Update Services와 같은 업데이트 시스템을 구성 하지 마세요 \(WSUS\) 업데이트를 자동으로 적용할 \(고정된 시간 일정에 따라\) 클러스터 노드에 있습니다.  
  
-   모든 클러스터 노드가 동일한 업데이트 원본(예: WSUS 서버, Windows 업데이트 또는 Microsoft 업데이트)을 사용하도록 균일하게 구성되어야 합니다.  
  
-   네트워크의 컴퓨터에 소프트웨어 업데이트를 적용하는 구성 관리 시스템을 사용하는 경우 모든 필수 또는 자동 업데이트에서 클러스터 노드를 제외합니다. 구성 관리 시스템의 예를 들면 Microsoft System Center Configuration Manager 2007 및 Microsoft System Center Virtual Machine Manager 2008이 있습니다.  
  
-   경우 내부 소프트웨어 배포 서버 \(WSUS 서버 예를 들어\) 포함 업데이트를 배포 하 고 해당 서버 클러스터 노드에 대해 승인 된 업데이트를 올바르게 식별 하는 확인 하는 데 사용 됩니다.  
  
#### <a name="BKMK_PROXY"></a>지점 시나리오에서 Microsoft 업데이트 적용  
특정 지점 시나리오에서 Microsoft 업데이트 또는 Windows 업데이트를 통해 클러스터 노드에 Microsoft 업데이트를 다운로드하려면 각 노드에서 로컬 시스템 계정에 대한 프록시 설정을 구성해야 할 수 있습니다. 예를 들어 지점 클러스터에서 로컬 프록시 서버를 통해 Microsoft 업데이트 또는 Windows 업데이트에 액세스하여 업데이트를 다운로드하는 경우 이러한 구성이 필요할 수 있습니다.  
  
필요한 경우 로컬 프록시 서버를 지정 하 고 로컬 주소 예외를 구성 하려면 각 노드에서 WinHTTP 프록시 설정을 구성 \(즉, 로컬 주소에 대 한 무시 목록\)합니다. 이렇게 하려면 각 클러스터 노드의 관리자 권한 명령 프롬프트에서 다음 명령을 실행하면 됩니다.  
  
```  
netsh winhttp set proxy <ProxyServerFQDN >:<port> "<local>"  
```  
  
여기서 <*ProxyServerFQDN*>은 프록시 서버의 정규화 된 도메인 이름 및 <*포트*> 통신할 때 사용할 포트입니다 (일반적으로 포트 443).  
  
예를 들어, 프록시 서버를 지정 하는 로컬 시스템 계정에 대 한 WinHTTP 프록시 설정을 구성 하려면 *MyProxy.CONTOSO.com*포트 443과 로컬 주소 예외와, 다음 명령을 입력 합니다.  
  
```  
netsh winhttp set proxy MyProxy.CONTOSO.com:443 "<local>"  
```  
  
### <a name="BKMK_BP_HF"></a>Microsoft.HotfixPlugin 사용에 대 한 권장 사항  
  
-   핫픽스 루트 폴더 및 핫픽스 구성 파일의 사용 권한을 이러한 파일을 저장하는 데 사용되는 컴퓨터의 로컬 관리자로만 쓰기 액세스를 제한하도록 구성하는 것이 좋습니다. 이렇게 하면 권한 없는 사용자가 이러한 파일을 변조하여 핫픽스가 적용될 때 장애 조치(failover) 클러스터의 기능을 손상시킬 수 있는 취약점을 방지할 수 있습니다.  
  
-   서버 메시지 블록에 대 한 데이터 무결성을 보장 하는 데 \(SMB\) 핫픽스 루트 폴더에 액세스 하는 데 사용 되는 연결을 구성 해야 SMB 암호화 SMB 공유 폴더에서 구성 가능 하다 면 합니다. **Microsoft.HotfixPlugin**을 사용하려면 SMB 연결에 대한 데이터 무결성을 보장하도록 SMB 서명 또는 SMB 암호화를 구성해야 합니다. 
  
    자세한 내용은 [핫픽스 루트 폴더 및 핫픽스 구성 파일에 대 한 액세스를 제한](cluster-aware-updating-plug-ins.md#BKMK_ACL)합니다.
  
### <a name="additional-recommendations"></a>추가 권장 사항  
  
-   동시에 예약될 수 있는 CAU 업데이트 실행과의 충돌을 방지하기 위해 예약된 유지 관리 기간 동안 클러스터 이름 개체 및 가상 컴퓨터 개체에 대한 암호 변경을 예약하지 마세요.  
  
-   사전에 적절 한 권한을 설정 해야\-업데이트 및 게시\-업데이트 스크립트를 네트워크에 저장 되는 권한이 없는 사용자가 이러한 파일의 잠재적 손상을 방지 하기 위해 폴더를 공유 합니다.  
  
-   자체에서 CAU를 구성 하려면\-모드에서 가상 컴퓨터 개체를 업데이트 하는 중 \(VCO\) CAU 클러스터 된 역할 Active Directory에서 생성 되어야 합니다. CAU는 장애 조치(failover) 클러스터에 충분한 권한이 있는 경우 CAU 클러스터된 역할이 추가될 때 이 개체를 자동으로 만들 수 있습니다. 그러나 특정 조직의 보안 정책으로 인해 Active Directory에서 개체를 미리 준비해야 할 수 있습니다. 이 작업을 수행하는 절차는 [클러스터된 역할에 대한 계정 사전 준비 단계](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731002\(v=ws.10\)#steps-for-prestaging-the-cluster-name-account)를 참조하세요.  
  
-   IT 조직에서 업데이트 실행 설정을 저장하여 업데이트 요구 사항이 유사한 장애 조치(failover) 클러스터 간에 다시 사용하려면 업데이트 실행 프로필을 만들면 됩니다. 또한 업데이트 모드에 따라 모든 원격 업데이트 코디네이터 컴퓨터 또는 장애 조치(failover) 클러스터에서 액세스할 수 있는 파일 공유에서 업데이트 실행 프로필을 저장하고 관리할 수 있습니다. 자세한 내용은 [고급 옵션 및 CAU에 대 한 실행 프로필 업데이트](cluster-aware-updating-options.md)합니다.  
  
## <a name="BKMK_BPA"></a>클러스터 업데이트 준비 테스트  
CAU 모범 사례 분석기를 실행할 수 있습니다 \(BPA\) 장애 조치 클러스터 및 네트워크 환경이 다양 한 소프트웨어 업데이트를 적용 CAU에서 요구 사항을 충족 하는지 여부를 테스트 하는 모델입니다. 기본 플러그 인을 사용 하 여 Microsoft 업데이트를 적용할 준비를 위한 환경 확인 테스트는 대부분\-에서는 **Microsoft.WindowsUpdatePlugin**합니다.  
  
> [!NOTE]  
> 독립적으로 확인 클러스터 환경을 플러그 인을 사용 하 여 소프트웨어 업데이트를 적용할 준비가 되었는지 확인 해야 할 수 있습니다\-보다 다른 **Microsoft.WindowsUpdatePlugin**합니다. 비 사용 하는 경우\-Microsoft 플러그\-에서는 하드웨어 제조업체에서 제공한 것과 같은 게시자에 문의 하십시오.  
  
다음 두 가지 방법으로 BPA를 실행할 수 있습니다.  
  
1.  CAU 콘솔에서 **클러스터 업데이트 준비 상태 분석** 을 선택합니다. BPA에서 준비 테스트 완료 된 후 테스트 보고서가 나타납니다. 클러스터 노드에서 문제가 발견된 경우 수정 작업을 수행할 수 있도록 구체적인 문제와 함께 해당 문제가 발생한 노드가 식별됩니다. 테스트를 완료하는 데 몇 분 정도 걸릴 수 있습니다.  
  
2.  실행 합니다 [Test-causetup](https://docs.microsoft.com/powershell/module/clusterawareupdating/Test-CauSetup) cmdlet. 장애 조치 클러스터링에 대 한 Windows PowerShell 모듈 (장애 조치 클러스터링 도구의 일부)가 설치 된 로컬 또는 원격 컴퓨터에서 cmdlet을 실행할 수 있습니다. 또한 장애 조치(failover) 클러스터의 노드에서도 이 cmdlet을 실행할 수 있습니다.  
  
> [!NOTE]  
> -   클러스터 노드의 관리 권한 및 실행에 사용 되는 컴퓨터의 로컬 관리 권한이 있는 계정을 사용 해야 합니다 **테스트\-CauSetup** cmdlet 또는 클러스터 업데이트 준비를 분석 하려면 클러스터 인식 업데이트 창을 사용 합니다. 클러스터 인식 업데이트 창을 사용 하 여 테스트를 실행 하려면 필요한 자격 증명을 사용 하 여 컴퓨터에 로그온 해야 합니다.  
> -   테스트에서는 클러스터 업데이트 준비 상태를 테스트하는 데 사용된 것과 동일한 컴퓨터에서 동일한 사용자 자격 증명으로 소프트웨어 업데이트를 미리 보고 적용하는 데 사용되는 CAU 도구를 실행하는 것으로 가정합니다.  
  
> [!IMPORTANT]  
> 다음과 같은 경우 클러스터에서 업데이트 준비 상태를 테스트하는 것이 좋습니다.  
>   
> -   CAU를 사용하여 소프트웨어 업데이트를 처음으로 적용하기 전  
> -   클러스터에 노드를 추가하거나 클러스터에서 클러스터 유효성 검사 마법사를 실행해야 하는 다른 하드웨어 변경을 수행한 후  
> -   업데이트 원본에서 변경 하거나 업데이트 설정 또는 구성 변경 후 \(CAU 이외의\) 노드에서 업데이트의 응용 프로그램에 영향을 줄 수입니다.  
  
### <a name="tests-for-cluster-updating-readiness"></a>클러스터 업데이트 준비 테스트  
다음 표에는 클러스터 업데이트 준비 테스트, 몇 가지 일반적인 문제 및 해결 단계가 나와 있습니다.  
  
|테스트|가능한 문제 및 영향|해결 단계|  
|--------|-------------------------------|--------------------|  
|장애 조치(failover) 클러스터를 사용할 수 있어야 함|장애 조치(failover) 클러스터 이름을 확인할 수 없거나, 하나 이상의 클러스터 노드에 액세스할 수 없습니다. BPA에서 클러스터 준비 테스트를 실행할 수 없습니다.|-BPA 실행 중에 지정한 클러스터 이름의 철자를 확인 합니다.<br />-클러스터의 모든 노드가 온라인 되어 실행 중인지 확인 합니다.<br />-는 유효성 검사 구성 마법사를 성공적으로 실행할 수 장애 조치 클러스터를 확인 합니다.|  
|장애 조치(failover) 클러스터 노드에서 WMI를 통해 원격 관리를 사용할 수 있어야 함|Windows Management Instrumentation을 사용 하 여 원격 관리는 하나 이상의 장애 조치 클러스터 노드를 사용할 수 없습니다 \(WMI\)합니다. 노드에 원격 관리가 구성되지 않은 경우 CAU에서 클러스터 노드를 업데이트할 수 없습니다.|모든 장애 조치(failover) 클러스터 노드에서 WMI를 통해 원격 관리를 사용할 수 있는지 확인합니다. 자세한 내용은 이 항목의 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 를 참조하세요.|  
|각 장애 조치 클러스터 노드에서 PowerShell 원격 기능을 사용 해야|PowerShell 설치 되지 않았거나 하나 이상의 장애 조치 클러스터 노드에 원격 연결을 위해 사용할 수 없습니다. 자체 CAU를 구성할 수 없습니다\-모드를 업데이트 하거나 특정 기능을 사용 하 여 원격에서\-모드를 업데이트 합니다.|PowerShell 모든 클러스터 노드에 설치 되어 있고 원격을 지원 되는 확인 합니다.<br /><br />자세한 내용은 이 항목의 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 를 참조하세요.|  
|장애 조치(failover) 클러스터 버전|Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 장애 조치 클러스터의 노드가 하나 이상 실행 되지 않습니다. CAU에서 장애 조치(failover) 클러스터를 업데이트할 수 없습니다.|Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 BPA 실행 중 지정 된 장애 조치 클러스터 실행 되 고 있는지 확인 합니다.<br /><br />자세한 내용은 이 항목의 [클러스터 구성 확인](#BKMK_REQ_CLUS) 를 참조하세요.|  
|필요한 버전의 .NET Framework 및 Windows PowerShell이 모든 장애 조치(failover) 클러스터 노드에 설치되어 있어야 함|하나 이상의 클러스터 노드에.NET framework 4.6에서 4.5 또는 Windows PowerShell 설치 되지 않았습니다. 일부 CAU 기능이 작동하지 않을 수 있습니다.|필요한 경우 모든 클러스터 노드에.NET Framework 4.6 및 4.5 Windows PowerShell이 설치 되어 있는지 확인 합니다.<br /><br />자세한 내용은 이 항목의 [원격 관리 노드 구성](#BKMK_NODE_CONFIG) 를 참조하세요.|  
|클러스터 서비스가 모든 클러스터 노드에서 실행되어야 함|하나 이상의 노드에서 클러스터 서비스가 실행되지 않습니다. CAU에서 장애 조치(failover) 클러스터를 업데이트할 수 없습니다.|-확인 하는 클러스터 서비스가 \(clussvc\) 클러스터의 모든 노드에서 시작 되 고 자동으로 시작 되도록 구성 되어 있습니다.<br />-는 유효성 검사 구성 마법사를 성공적으로 실행할 수 장애 조치 클러스터를 확인 합니다.<br /><br />자세한 내용은 이 항목의 [클러스터 구성 확인](#BKMK_REQ_CLUS) 를 참조하세요.|  
|장애 조치(failover) 클러스터 노드에 업데이트를 자동으로 설치하도록 자동 업데이트를 구성해서는 안 됨|하나 이상의 장애 조치(failover) 클러스터 노드에 Microsoft 업데이트를 자동으로 설치하도록 자동 업데이트가 구성되어 있습니다. CAU를 다른 업데이트 방법과 함께 사용하면 계획되지 않은 가동 중지 시간 또는 예기치 않은 결과가 발생할 수 있습니다.|Windows 업데이트 기능이 하나 이상의 클러스터 노드에서 자동 업데이트에 대해 구성된 경우 자동 업데이트가 업데이트를 자동으로 설치하도록 구성되어 있지 않은지 확인합니다.<br /><br />자세한 내용은 [Microsoft 업데이트 적용에 대한 권장 사항](#BKMK_BP_WUA)를 참조하세요.|  
|장애 조치(failover) 클러스터 노드에서 동일한 업데이트 원본을 사용해야 함|하나 이상의 장애 조치(failover) 클러스터 노드가 Microsoft 업데이트에 대해 나머지 노드와 다른 업데이트 원본을 사용하도록 구성되어 있습니다. CAU에서 클러스터 노드에 업데이트를 균일하게 적용하지 못할 수 있습니다.|모든 클러스터 노드가 동일한 업데이트 원본(예: WSUS 서버, Windows 업데이트 또는 Microsoft 업데이트)을 사용하도록 균일하게 구성되어 있는지 확인합니다.<br /><br />자세한 내용은 [Microsoft 업데이트 적용에 대한 권장 사항](#BKMK_BP_WUA)를 참조하세요.|  
|장애 조치(failover) 클러스터의 각 노드에 원격 종료를 허용하는 방화벽 규칙이 설정되어 있어야 함|하나 이상의 장애 조치(failover) 클러스터 노드에 원격 종료를 허용하는 방화벽 규칙이 설정되어 있지 않거나, 그룹 정책 설정이 이 규칙의 사용을 차단합니다. 노드를 자동으로 다시 시작해야 하는 업데이트를 적용하는 업데이트 실행이 제대로 완료되지 않을 수 있습니다.|하는 경우 Windows 방화벽 또는 비\-Microsoft 방화벽은 클러스터 노드에서 사용 되 고 원격 종료를 허용 하는 방화벽 규칙을 구성 합니다.<br /><br />자세한 내용은 이 항목의 [자동 다시 시작을 허용하도록 방화벽 규칙 설정](#BKMK_FW) 를 참조하세요.|  
|각 장애 조치(failover) 클러스터 노드의 프록시 서버 설정이 로컬 프록시 서버로 설정되어야 함|하나 이상의 장애 조치(failover) 클러스터 노드에 잘못된 프록시 서버 구성이 있습니다.<br /><br />로컬 프록시 서버를 사용하는 경우 클러스터에서 Windows 업데이트 또는 Microsoft 업데이트에 액세스할 수 있도록 각 노드의 프록시 서버 설정을 올바르게 구성해야 합니다.|각 클러스터 노드의 WinHTTP 프록시(필요한 경우) 설정이 로컬 프록시 서버로 설정되어 있는지 확인합니다. 환경에서 프록시 서버를 사용하지 않는 경우에는 이 경고를 무시해도 됩니다.<br /><br />자세한 내용은 이 항목에서 [지점 시나리오에서 업데이트 적용](#BKMK_PROXY)을 참조하세요.|  
|자체를 사용 하도록 설정 하려면 장애 조치 클러스터에 CAU 클러스터 된 역할을 설치 해야\-업데이트 모드|CAU 클러스터된 역할이 이 장애 조치(failover) 클러스터에 설치되어 있지 않습니다. 이 역할은 필요에 대 한 자체 클러스터\-업데이트 합니다.|CAU를 사용 하 여 자체를\-다음 방법 중 하나에 장애 조치 클러스터에서 CAU 클러스터 된 역할을 추가 모드를 업데이트 합니다.<br /><br />-실행 합니다 [Add-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Add-CauClusterRole) PowerShell cmdlet.<br />-선택 된 **구성 클러스터 자체\-업데이트 옵션** Cluster-aware Updating 창에서 작업 합니다.|  
|자체를 사용 하도록 설정 하려면 장애 조치 클러스터에서 CAU 클러스터 된 역할을 사용할 수 있어야\-업데이트 모드|CAU 클러스터된 역할을 사용할 수 없습니다. 예를 들어 CAU 클러스터 된 역할이 설치 되지 또는 사용 하 여 비활성화 된 합니다 [사용 안 함\-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Disable-CauClusterRole) PowerShell cmdlet. 이 역할은 필요에 대 한 자체 클러스터\-업데이트 합니다.|CAU를 사용 하 여 자체를\-이 장애 조치 클러스터에서 CAU 클러스터 된 역할을 사용 하도록 설정 다음 방법 중 하나로 업데이트 모드:<br /><br />-실행 합니다 [Enable-cauclusterrole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Enable-CauClusterRole) PowerShell cmdlet.<br />-선택 된 **구성 클러스터 자체\-업데이트 옵션** Cluster-aware Updating 창에서 작업 합니다.|  
|구성 된 CAU 플러그\-에 자체\-업데이트 모드 모든 장애 조치 클러스터 노드에서 등록 해야 합니다|CAU 플러그 인이 장애 조치 클러스터의 하나 이상의 노드에서 CAU 클러스터 된 역할에 액세스할 수 없습니다\-자체에 구성 된 모듈의\-옵션을 업데이트 합니다. 자체\-업데이트 실행이 실패할 수 있습니다.|-되도록 구성 된 CAU 플러그\-에 따라이 설치 되어 모든 클러스터 노드에서 CAU 플러그 인을 제공 하는 제품의 설치 절차는\-에서 합니다.<br />-실행 합니다 [등록\-CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) PowerShell cmdlet은 플러그를 등록 하려면\-에서 필요한 클러스터 노드에 합니다.|  
|모든 장애 조치 클러스터 노드에 등록 된 CAU 플러그 인 집합이 있어야 합니다.\-기능|자체\-하는 경우 업데이트 실행에 실패할 수 있습니다 플러그\-구성 하는 업데이트 실행에 사용할 모든 클러스터 노드에서 사용할 수 없는 하나를 변경 합니다.|-되도록 구성 된 CAU 플러그\-에 따라이 설치 되어 모든 클러스터 노드에서 CAU 플러그 인을 제공 하는 제품의 설치 절차는\-에서 합니다.<br />-실행 합니다 [등록\-CauPlugin](https://docs.microsoft.com/powershell/module/clusterawareupdating/Register-CauPlugin) PowerShell cmdlet은 플러그를 등록 하려면\-에서 필요한 클러스터 노드에 합니다.|  
|구성된 업데이트 실행 옵션이 유효해야 함|자체\-업데이트 일정 및 업데이트 실행 옵션이 장애 조치 클러스터에 대해 구성 된 완전 하지 않거나 올바르지 않습니다. 자체\-업데이트 실행이 실패할 수 있습니다.|유효한 자체 구성\-일정 및 업데이트 실행 옵션 집합을 업데이트 합니다. 예를 들어 사용할 수 있습니다 합니다 [설정할\-CauClusterRole](https://docs.microsoft.com/powershell/module/clusterawareupdating/Set-CauClusterRole) CAU를 구성 하려면 PowerShell cmdlet에 클러스터 된 역할입니다.|  
|둘 이상의 장애 조치(failover) 클러스터 노드가 CAU 클러스터된 역할의 소유자여야 함|자체에서 시작 된 업데이트 실행\-CAU 클러스터 된 역할에 이동할 수 있는 소유자 노드가 없기 때문에 실패 모드를 업데이트 합니다.|장애 조치(failover) 클러스터링 도구를 사용하여 모든 클러스터 노드가 CAU 클러스터된 역할의 가능한 소유자로 구성되어 있는지 확인합니다. 이는 기본 구성입니다.||  
|모든 장애 조치(failover) 클러스터 노드에서 Windows PowerShell 스크립트에 액세스할 수 있어야 함|CAU 클러스터 된 역할의 일부 가능한 소유자 노드에서 구성 된 Windows PowerShell 이전에 액세스할 수 있습니다\-업데이트 및 게시\-스크립트를 업데이트 합니다. 자체\-실행을 업데이트 하지 못합니다.|CAU 클러스터 된 역할의 모든 가능한 소유자 노드에서 구성 된 PowerShell 사전 액세스 권한을 갖도록\-업데이트 및 게시\-스크립트를 업데이트 합니다.|  
|모든 장애 조치(failover) 클러스터 노드에서 동일한 Windows PowerShell 스크립트를 사용해야 함|지정 된 Windows PowerShell 이전 버전의 동일한 복사본을 사용 하 여 CAU 클러스터 된 역할의 일부 가능한 소유자 노드에서\-업데이트 및 게시\-스크립트를 업데이트 합니다. 자체\-실패 실행을 업데이트 하거나 예기치 않은 동작이 표시 될 수 있습니다.|CAU 클러스터 된 역할의 모든 가능한 소유자 노드에서 동일한 PowerShell 이전 버전을 사용 하는지 확인\-업데이트 및 게시\-스크립트를 업데이트 합니다.|  
|업데이트 실행에 대해 지정된 WarnAfter 설정이 StopAfter 설정보다 작아야 함|지정된 CAU 업데이트 실행 제한 시간 값으로 인해 경고 제한 시간이 무효화됩니다. 경고 이벤트 로그가 생성되기 전에 업데이트 실행이 취소될 수도 있습니다.|업데이트 실행 옵션에서 **WarnAfter** 옵션 값을 **StopAfter** 옵션 값보다 작은 값으로 구성합니다.|  
  
## <a name="see-also"></a>참조  
  
-   [클러스터 인식 업데이트 개요](cluster-aware-updating.md)