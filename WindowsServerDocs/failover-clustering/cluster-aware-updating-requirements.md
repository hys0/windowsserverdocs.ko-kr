---
ms.assetid: 75cc1d24-fa2f-45bd-8f3b-1bbd4a1aead0
title: "클러스터 인식 업데이트 요구 사항 및 모범 사례"
ms.prod: windows-server-threshold
ms.topic: article
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 4/28/2017
description: "클러스터 인식 업데이트를 사용 하 여 업데이트를 설치 하는 Windows Server 실행 클러스터에서 요구 사항"
ms.openlocfilehash: 8517466d58345077af446c1b2c1e2aeb3b17aaa1
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="cluster-aware-updating-requirements-and-best-practices"></a>클러스터 인식 업데이트 요구 사항 및 모범 사례

>에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 섹션의 요구 사항 및 사용 하는 데 필요한 종속성 설명 [클러스터 인식 업데이트](cluster-aware-updating.md) (CAU) Windows Server 실행 장애 조치 클러스터에 업데이트를 적용 하 합니다.
  
> [!NOTE]  
> 개별적으로 확인 하지 클러스터 환경에서 plug\ 이외의 사용 하는 경우 업데이트를 적용 준비가 되었는지 해야 할 수도 있습니다 **Microsoft.WindowsUpdatePlugin**합니다. plug\ non\ Microsoft를 사용 하는 경우 자세한 내용은 게시자에 게 문의 합니다. Plug\ 기능에 대 한 자세한 내용은 참조 [Plug\ 기능의 작동 방식을](cluster-aware-updating-plug-ins.md)합니다.   
  
## <a name="BKMK_REQ_CLUS"></a>클러스터링 기능과 장애 클러스터링 도구 설치  
CAU 클러스터링 기능 및 장애 클러스터링 도구를 설치를 해야합니다. 장애 클러스터링 도구 CAU 도구 \(clusterawareupdating.dll\), 클러스터링 cmdlet 및 CAU 작업에 필요한 다른 구성 요소 포함 됩니다. 클러스터링 기능을 설치 단계를 참조 하세요. [장애 클러스터링 기능 및 도구를 설치](http://go.microsoft.com/fwlink/p/?LinkId=253342)합니다.  
  
장애 클러스터링 도구에 대 한 정확한 설치 요구 CAU 업데이트 장애 클러스터에 클러스터 역할을 조정 하는 있는지 여부에 따라 달라 \ (사용 하 여 self\ 업데이트 mode\) 또는 원격 컴퓨터에서 합니다. 또한 CAU self\ 업데이트 모드 CAU 도구를 사용 하 여 CAU 클러스터 역할 장애 클러스터에서의 설치를 필요 합니다.    
  
다음 표에서 CAU 기능 설치 요구 두 CAU 업데이트 모드에 대 한 요약 되어 있습니다.  
  
|구성 요소가 설치|모드 Self\ 업데이트|모드 Remote\ 업데이트|  
|-----------------------|-----------------------|-------------------------|  
|장애 조치 클러스터링 기능|필요한 모든 클러스터 노드에서|필요한 모든 클러스터 노드에서|  
|장애 클러스터링 도구|필요한 모든 클러스터 노드에서|필수 remote\ 업데이트 컴퓨터에서<br />-하는 데 필요한 모든 클러스터 노드에서 실행는 [저장 CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) cmdlet|  
|클러스터 역할 CAU|필수|필요 하지 않음|  
  
## <a name="obtain-an-administrator-account"></a>관리자 계정으로 가져오는  
다음 관리자 요구 사항은 CAU 기능을 사용 하는 데 필요한 합니다.  
  
-   CAU 사용자 인터페이스를 사용 하 여 업데이트 조치를 적용 하거나 미리 \(UI\) 또는 클러스터 인식 업데이트 cmdlet 사용 해야 일부 클러스터 노드에서 로컬 관리자 권한이 있는 도메인 계정을 합니다. 계정이 없는 경우 권한이 모든 노드에서 하는 메시지가 클러스터 인식 업데이트 창에서 이러한 작업을 수행 하는 경우 필요한 자격 증명을 제공 합니다. 사용 하는 [클러스터 인식 업데이트](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating) cmdlet, cmdlet 매개도 필요한 자격 증명을 제공할 수 있습니다.  
  
-   업데이트 Coordinator 컴퓨터 로컬 관리자 계정을 사용 하 여 나이 계정을 사용 하 여 관리자 권한으로 CAU 도구를 실행 해야 CAU 모드 remote\ 업데이트에서 사용 하면 하지 않은 로컬 관리자 권한과 클러스터 노드에서 계정으로 로그인 하는 경우는 **클라이언트 인증 후 가장** 사용자 권한을 합니다. 
  
-   모범 사례 CAU 분석기를 실행 하려면 관리자 권한이 클러스터 노드에서 및 실행 하는 데 사용 하는 컴퓨터에서 관리자 권한이 로컬 계정을 사용 해야는 [테스트 CauSetup](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/test-causetup) cmdlet 또는 클러스터 준비 클러스터 인식 업데이트 창을 사용 하 여 업데이트를 분석 하 합니다. 자세한 내용은 참조 [업데이트 준비 테스트 클러스터](#BKMK_BPA)합니다.  
  
## <a name="verify-the-cluster-configuration"></a>클러스터 구성 확인  
CAU를 사용 하 여 업데이트를 지원 하도록 장애 클러스터에 대 한 일반 요구 사항은 다음과 같습니다. 원격 management 노드가에서 대 한 추가 구성 요구 사항에 나열 된 [구성에 대 한 원격 management 노드가](#BKMK_NODE_CONFIG) 이 항목 뒷부분.  
  
-   충분 한 클러스터 노드에서 클러스터에 쿼럼이 되도록 온라인 상태 여야 합니다.  
  
-   일부 클러스터 노드에서 같은 Active Directory 도메인에 있어야 합니다.  
  
-   클러스터 이름은 DNS을 사용 하 여 네트워크를 확인 해야 합니다.  
  
-   CAU 모드 remote\ 업데이트에서 사용 되는 경우 업데이트 Coordinator 컴퓨터 장애 클러스터 노드가 네트워크 연결이 있어야 하 고 클러스터 장애 조치와 같은 Active Directory 도메인에 있어야 합니다.  
  
-   클러스터 노드에서 클러스터 서비스가 실행 해야 합니다. 기본적으로이 서비스 모든 클러스터 노드에서 설치 되 고 자동으로 시작 되도록 구성 됩니다.  
  
-   스크립트 사용 하 여 PowerShell pre\ 업데이트나 post\ 업데이트는 CAU 업데이트를 실행 하는 동안을 일부 클러스터 노드에서 스크립트 설치 되어 있는지 하거나 항상 사용 가능한 네트워크 파일 공유에서 예를 들어 모든 노드에 액세스할 수 있습니다 확인 합니다. 스크립트 파일 공유 네트워크에 저장 되는 경우 모든 사람에 대 한 권한 읽기에 대 한 폴더를 구성할 그룹 합니다.  
  
## <a name="BKMK_NODE_CONFIG"></a>원격 management 노드가 구성  
클러스터 인식 업데이트를 사용 하 여 원격 관리에 대 한 모든 노드의 클러스터를 구성 합니다. 기본적으로 유일한 작업 위해 수행 해야 할 노드 원격 관리 하는 것에 대 한 구성 [자동 다시 시작 수 있도록 방화벽 규칙 활성화](#BKMK_FW)합니다. 

다음 표에서 경우 기본에서 모델과 귀하의 환경에 완료 원격 관리 요구 사항이 나열 합니다.

설치 요구 사항에 대 한 뿐만 아니라 이러한 요구 사항은 [클러스터링 기능과 장애 클러스터링 도구 설치](#BKMK_REQ_CLUS) 일반 클러스터링이 항목의 이전 섹션에 설명 된 요구 사항 및 합니다.  
  
|요구 사항|기본 상태|모드 Self\ 업데이트|모드 Remote\ 업데이트|  
|---------------|---|-----------------------|-------------------------|  
|[허용 자동 다시 시작 하는 방화벽 규칙을 사용 하도록 설정](#BKMK_FW)|사용 안 함|방화벽을 사용 중인 경우 모든 클러스터 노드에서 필요|방화벽을 사용 중인 경우 모든 클러스터 노드에서 필요|  
|[WMI(Windows Management Instrumentation) 사용 하도록 설정](#BKMK_WMI)|사용 하도록 설정|필요한 모든 클러스터 노드에서|필요한 모든 클러스터 노드에서|  
|[3.0 또는 4.0 Windows PowerShell 및 Windows PowerShell 활성화 원격](#BKMK_PS)|사용 하도록 설정|필요한 모든 클러스터 노드에서|다음 실행 하려면 모든 클러스터 노드에서 필요 합니다.<br /><br />- [저장 CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) cmdlet<br />-업데이트를 실행 하는 동안 PowerShell pre\ 업데이트 및 업데이트 post\ 스크립트<br />-업데이트 준비 클러스터 인식 업데이트 창을 사용 하 여 클러스터의 테스트 또는 [Test\ CauSetup](http://go.microsoft.com/fwlink/p/?LinkId=242384) Windows PowerShell cmdlet|  
|[.NET Framework 4.5 또는 4.6 설치](#BKMK_NET)|사용 하도록 설정|필요한 모든 클러스터 노드에서|다음 실행 하려면 모든 클러스터 노드에서 필요 합니다.<br /><br />- [저장 CauDebugTrace](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/save-caudebugtrace) cmdlet<br />-업데이트를 실행 하는 동안 PowerShell pre\ 업데이트 및 업데이트 post\ 스크립트<br />-업데이트 준비 클러스터 인식 업데이트 창을 사용 하 여 클러스터의 테스트 또는 [Test\ CauSetup](http://go.microsoft.com/fwlink/p/?LinkId=242384) Windows PowerShell cmdlet|  

### <a name="BKMK_FW"></a>허용 자동 다시 시작 하는 방화벽 규칙을 사용 하도록 설정  
업데이트를 적용 한 후 자동 다시 시작 수 있도록 \ (경우 업데이트 설치 필요는 restart\), Windows 방화벽 또는 non\ Microsoft 방화벽을 사용 중인 클러스터 노드에서 방화벽 규칙 다음 교통 수 있도록 해 주는 각 노드에서 사용할 수 있어야 합니다.  
  
-   프로토콜: TCP  
  
-   방향: 인바인드  
  
-   프로그램: wininit.exe  
  
-   포트: RPC 동적 포트  
  
-   프로필: 도메인  
  
Windows 방화벽 클러스터 노드에서 사용 되는 경우 할 수 있는이 사용 하 여는 **원격 종료** 각 클러스터 노드에서 규칙 그룹 Windows 방화벽. Self\ 업데이트 옵션을 구성 하 고 업데이트를 적용 하 클러스터 인식 업데이트 창을 사용 하는 경우는 **원격 종료** 각 클러스터 노드에서 규칙 그룹 Windows 방화벽 자동으로 활성화 됩니다.  
  
> [!NOTE]  
> **원격 종료** Windows 방화벽을 구성 하는 그룹 정책 설정으로 충돌 하는 경우 Windows 방화벽 규칙 그룹을 사용할 수 없습니다.    
  
**원격 종료** 방화벽 규칙 그룹도 지정 하 여 사용할 수 있는 **– EnableFirewallRules** 매개 다음 CAU cmdlet 실행 될 때: [추가 CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole), [호출 CauRun](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/invoke-causcan), 및 [SetCauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole)합니다.  
  
다음 PowerShell 예제 클러스터 노드에서 자동 다시 시작 사용 하도록 설정 하는 추가 방법입니다.  
  
```PowerShell  
Set-NetFirewallRule -Group "@firewallapi.dll,-36751" -Profile Domain -Enabled true  
```  

### <a name="BKMK_WMI"></a>WMI(Windows Management Instrumentation) WMI ()를 사용 하도록 설정 
일부 클러스터 노드에서 WMI(Windows Management Instrumentation) \(WMI\)를 사용 하 여 원격 관리에 대 한 구성 합니다. 이 기본적으로 설정 됩니다.  
  
수동으로 원격 관리를 사용 하려면 다음을 수행 합니다.  
  
1.  서비스 콘솔에서 시작의 **Windows 원격 관리** 서비스 및 설정 시작 유형 **자동**합니다.  
  
2.  실행는 [설정 WSManQuickConfig](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.wsman.management/set-wsmanquickconfig) cmdlet, 또는 다음 명령 실행에서 관리자 권한 명령 프롬프트 다음과 같습니다.  
  
    ```PowerShell  
    winrm quickconfig -q  
    ```  
  
Windows 방화벽 클러스터 노드에서 사용 중인 경우 WMI 원격 지원, 인바인드 방화벽을 내 마음 대로 대 한 **Windows 원격 관리 \(HTTP\-In\)** 각 노드에서 사용할 수 있어야 합니다.  이 규칙은 기본적으로 활성화 됩니다.  
  
### <a name="BKMK_PS"></a>Windows PowerShell 및 Windows PowerShell 원격 설정  
모드 self\ 업데이트와 remote\ 업데이트 모드로 특정 CAU 기능을 사용 하려면 PowerShell 설치 하 고 해야 모든 클러스터 노드에서 원격 명령을 실행 되도록 설정 합니다. 기본적으로, PowerShell 설치 되어 원격에 대 한 사용 하도록 설정 합니다.  
  
PowerShell 원격을 사용 하려면 다음 방법 중 하나를 사용 하 여 다음과 같습니다.  
  
-   실행는 [활성화 PSRemoting](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/enable-psremoting) cmdlet 합니다.  
  
-   Windows 원격 관리 \(WinRM\) domain\ 수준 그룹 정책 설정을 구성 합니다.  
  
PowerShell 원격 설정에 대 한 자세한 내용은 참조 [about\_Remote\_Requirements](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_remote_requirements)합니다.  
  
### <a name="BKMK_NET"></a>.NET Framework 4.5 또는 4.6 설치  
클러스터 노드에서 모드 self\ 업데이트와 모드 remote\ 업데이트,.NET Framework 4.6 또는 Windows Server 2012 R2) (에서.NET Framework 4.5 특정 CAU 기능을 사용 하도록 설정 하려면 설치 되어야 합니다. .NET Framework 기본적으로 설치 됩니다.  

설치 되어 있지 않은 경우에 PowerShell를 사용 하 여.NET Framework 4.6 (또는 4.5)를 설치 하려면 다음 명령을 사용.

```PowerShell
Install-WindowsFeature -Name NET-Framework-45-Core
```

## <a name="BKMK_BEST_PRAC"></a>최적의 권장 사용 되는 클러스터 인식 업데이트 
  
### <a name="BKMK_BP_WUA"></a>Microsoft 업데이트 적용을 위한 권장 사항

좋습니다를 사용 하 여 CAU 기본적으로 업데이트를 적용 하기 시작 하면 **Microsoft.WindowsUpdatePlugin** plug\ 기능에 클러스터에 사용을 중지 다른 방법 클러스터 노드에서 Microsoft에서 소프트웨어 업데이트를 설치 합니다.  
  
> [!CAUTION]  
> 개별 노드 자동으로 업데이트 하는 방법으로 CAU 결합 \ (에 고정 된 시간 schedule\) 예기치 결과 중단 서비스 및 예상치 못한 작동 중지 포함 하 여 발생할 수 있습니다.  
  
다음이 지침을 따르면 것이 좋습니다.  
  
-   최상의 결과 사용 하지 않도록 설정 자동 업데이트 클러스터 노드에서 예를 들어 제어판에서 또는 그룹 정책을 사용 하 여 구성 되어 있는 설정에서 자동 업데이트 설정 하는 것이 좋습니다.  
  
    > [!CAUTION]  
    > 클러스터 노드에서 업데이트를 자동으로 설치 CAU 하 여 업데이트 설치에 방해가 될 수 있습니다 및 CAU 오류가 발생할 수 있습니다.  
  
    필요한 관리자가 업데이트 설치 타이밍 제어할 수 있기 때문에 다음과 같은 자동 업데이트 설정 CAU와 호환 됩니다.  
  
    -   업데이트를 다운로드 하기 전에 알리는 하 고 설치 하기 전에 알리는 설정  
  
    -   자동으로 업데이트를 다운로드 하 고 설치 하기 전에 알림 설정  
  
    그러나 자동 업데이트 CAU 업데이트 연속으로 동시에 업데이트를 다운로드 하는 경우 업데이트 실행 될 수 있습니다 시간이 더 오래 걸릴를 완료 합니다.  
  
-   Windows Server 업데이트 서비스 \(WSUS\) 적용 하려면 자동으로 업데이트와 같은 업데이트 시스템 구성 하지 않으면 \ (에 고정 된 시간 schedule\) 클러스터 노드에서 합니다.  
  
-   예를 들어, WSUS 서버, Windows 업데이트를 또는 Microsoft 업데이트 동일한 업데이트 소스를 사용 하 여 모든 클러스터 노드에서 일관 구성 되어야 합니다.  
  
-   네트워크에서 컴퓨터에 소프트웨어 업데이트를 적용 하려면 구성 관리 시스템을 사용 하는 경우 클러스터 노드에서 필요한 또는 자동 업데이트를 모두에서 제외 합니다. 구성 관리 시스템의 예로 Microsoft 시스템 Center Configuration Manager 2007 및 Microsoft 시스템 센터 가상 컴퓨터 관리자 2008 합니다.  
  
-   하는 경우 내부 소프트웨어 배포 서버 \ (예를 들어, WSUS servers\)를 포함 하 고 업데이트를 배포, 이러한 서버 올바르게 클러스터 노드에서 대해 승인 된 업데이트를 식별 하는 확인 하는 데 사용 됩니다.  
  
#### <a name="BKMK_PROXY"></a>적용 지점 시나리오에서 Microsoft 업데이트  
Microsoft 업데이트 Microsoft 업데이트 또는 Windows 업데이트에서 특정 지점 시나리오의 클러스터 노드에서 다운로드 하려면 각 노드에서 시스템 로컬 계정에 대 한 프록시 설정 구성 합니다. 예를 들어, 분기 office 클러스터 액세스 Microsoft 업데이트 또는 Windows 업데이트는 로컬 프록시 서버를 사용 하 여 업데이트를 다운로드 하는 경우이 작업을 수행 해야 할 수 있습니다.  
  
필요에 따라 로컬 프록시 서버를 지정 하 고 로컬 주소 예외 구성 각 노드에서 WinHTTP 프록시 설정을 구성 \ (즉, 로컬 addresses\에 대 한 사용 안 함 목록). 이렇게 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 각 클러스터 노드에서 실행할 수 있습니다.  
  
```  
netsh winhttp set proxy <ProxyServerFQDN >:<port> "<local>"  
```  
  
여기서 <*ProxyServerFQDN*> 프록시 서버에 대 한 정식된 도메인 이름입니다 및 <*포트*> 통신할 수 있는 포트 (일반적으로 443 포트).  
  
프록시 서버를 지정 하는 시스템 로컬 계정에 대 한 WinHTTP 프록시 설정을 구성 하는 등 *MyProxy.CONTOSO.com*, 포트 443와 로컬 주소 예외 다음 명령을 입력 합니다.  
  
```  
netsh winhttp set proxy MyProxy.CONTOSO.com:443 "<local>"  
```  
  
### <a name="BKMK_BP_HF"></a>사용 되는 Microsoft.HotfixPlugin 추천을 제공  
  
-   핫픽스 루트 폴더 및 이러한 파일을 저장 하는 데 사용 하는 컴퓨터에서만 로컬 관리자에 게 쓰기 액세스를 제한 하려면 핫픽스 구성 파일에서 사용 권한을 구성 하는 것이 좋습니다. 이 핫픽스 적용 되는 경우 장애 조치 클러스터의 기능 손상 시킬 수 있는 권한이 없는 사용자가 이러한 파일을 변조 방지할 수 있습니다.  
  
-   핫픽스 루트 폴더에 액세스 하는 데 사용 하는 서버 메시지 블록 \(SMB\) 연결에 대 한 데이터 무결성을 유지 하는 데 도움이 구성 해야 SMB 암호화 SMB 공유 폴더에서 구성 가능한 경우 합니다. **Microsoft.HotfixPlugin** SMB 로그인 또는 SMB 암호화 구성 되어 있는지 SMB 연결에 대 한 데이터 무결성을 유지 하는 데 도움이 필요 합니다. 
  
    자세한 내용은 참조 [핫픽스 루트 폴더 및 핫픽스 구성 파일에 대 한 액세스를 제한](cluster-aware-updating-plug-ins.md#BKMK_ACL)합니다.
  
### <a name="additional-recommendations"></a>자세한 내용  
  
-   CAU 업데이트를 실행 한 번에 예약할 수 있는 방해를 방지 하려면 예정된 유지 관리 작업 중 클러스터 이름 및 개체 가상 컴퓨터에 대 한 암호 변경 예약 하지 않는 합니다.  
  
-   하 여 권한 없는 사용자가 이러한 파일은 잠재적 손상을 방지 네트워크 공유 폴더에 저장 된 스크립트 pre\ 업데이트와 post\ 업데이트에 적절 한 권한이 설정 해야 합니다.  
  
-   가상 컴퓨터 개체 self\ 업데이트 모드에서는 CAU 구성 하려면 \(VCO\) CAU 클러스터 역할에 대 한 Active Directory에 만들어야 합니다. CAU 경우 만들 수이 개체 자동으로 CAU 클러스터 역할을 추가 하는 시간에 장애 클러스터에 충분 한 사용 권한을. 그러나 특정 조직의 보안 정책을 때문 해야 Active directory에서 개체 미리 준비 합니다. 이 작업을 수행 하는 절차 참조 [클러스터 역할에 대 한 계정을 미리 추가 단계](http://go.microsoft.com/fwlink/p/?LinkId=237624)합니다.  
  
-   저장 하 고 있는 클러스터 장애 조치를 통해 업데이트를 실행 설정을 다시 사용할 IT 조직에서 요구 업데이트 유사한 만들 수 있습니다 실행 프로필을 업데이트 합니다. 또한 업데이트 모드로 따라 저장 하 고 업데이트를 실행 프로필 모든 원격 업데이트 Coordinator 컴퓨터 또는 클러스터 장애 조치에 액세스할 수 있는 파일 공유에서 관리할 수 있습니다. 자세한 내용은 참조 [고급 옵션 및 업데이트를 실행 프로필을 CAU](cluster-aware-updating-options.md)합니다.  
  
## <a name="BKMK_BPA"></a>테스트 클러스터 업데이트 준비  
클러스터 장애 조치 있는지 여부를 테스트 CAU 모범 사례 분석기 \(BPA\) 모델을 실행 하 고 네트워크 환경 많은 소프트웨어 업데이트를 적용 하 여 CAU 하도록 요구 사항을 충족 합니다. 테스트 중 상당수 확인 준비 plug\에 기본 사용 하 여 Microsoft 업데이트 적용에 대 한 환경 **Microsoft.WindowsUpdatePlugin**합니다.  
  
> [!NOTE]  
> 개별적으로 확인 하지 클러스터 환경에서 plug\ 이외의 사용 하 여 소프트웨어 업데이트를 적용 준비가 되었는지 해야 할 수도 있습니다 **Microsoft.WindowsUpdatePlugin**합니다. Plug\에서, 하드웨어 제조업체에서 제공 non\ Microsoft를 사용 하는 경우 자세한 내용은 게시자에 게 문의 합니다.  
  
다음 두 가지 방법으로 BPA을 실행할 수 있습니다.  
  
1.  선택 **업데이트 준비 분석 클러스터** CAU 콘솔에서 합니다. BPA 준비 테스트를 완료 한 후 테스트 보고서에 표시 됩니다. 클러스터 노드에서 문제가 발견 되 면 특정 문제, 문제 나타나는 노드 수정 작업을 수행할 수 있도록 식별 됩니다. 테스트를 완료 하는 데 몇 분 정도 걸릴 수 있습니다.  
  
2.  실행는 [테스트 CauSetup](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/test-causetup) cmdlet 합니다. Windows PowerShell (일부 장애 클러스터링 도구)에 대 한 장애 클러스터링 모듈이 설치 되어 있는 로컬 또는 원격 컴퓨터에서 cmdlet을 실행할 수 있습니다. 장애 조치 클러스터 노드에서 cmdlet을 실행할 수도 있습니다.  
  
> [!NOTE]  
> -   관리자 권한이 클러스터 노드에서 및 실행 하는 데 사용 하는 컴퓨터에서 관리자 권한이 로컬 계정을 사용 해야는 **Test\ CauSetup** cmdlet 또는 클러스터 준비 클러스터 인식 업데이트 창을 사용 하 여 업데이트를 분석 하 합니다. 클러스터 인식 업데이트 창을 사용 하 여 테스트를 실행 하려면 필요한 자격 증명을 사용 하 여 컴퓨터에 로그온 해야 합니다.  
> -   테스트 가정 미리 소프트웨어 업데이트를 적용 하는 데 사용 되는 CAU 도구 실행 되도록 같은 컴퓨터에서와 동일한 사용자 자격 증명으로 클러스터 준비 업데이트를 테스트 하는 데 사용 됩니다.  
  
> [!IMPORTANT]  
> 클러스터 준비 다음과 같은 경우에 업데이트를 테스트 하는 것이 좋습니다.  
>   
> -   처음으로 CAU를 사용 하 여 소프트웨어 업데이트를 적용 하는 이전.  
> -   한 후에 노드에서 클러스터에 추가 하거나 클러스터 클러스터 마법사 유효성 검사를 실행 해야 하는 기타 하드웨어 변경 작업을 수행 합니다.  
> -   소스 업데이트 하거나 업데이트 설정이 나 구성 변경 후 \(other than CAU\) 있는 노드에 대 한 업데이트를 적용 영향을 줄 수 있습니다.  
  
### <a name="tests-for-cluster-updating-readiness"></a>업데이트 준비 클러스터에 대 한 테스트  
다음 표에서 클러스터 준비 테스트, 몇 가지 일반적인 문제 해결 단계를 업데이트 합니다.  
  
|테스트|가능한 문제와 영향을 줄|해상도 단계|  
|--------|-------------------------------|--------------------|  
|클러스터 장애 조치 사용할 수 있어야 합니다.|클러스터 장애 조치 이름을 나 하나 또는 여러 개의 클러스터 노드에서 액세스할 수 없습니다 확인할 수 없습니다. BPA 클러스터 준비 테스트 실행할 수 없습니다.|-클러스터 실행 BPA 중에 지정 된 이름이 올바른지를 확인 합니다.<br />-온라인 실행 되 고 모든 노드의 클러스터 되는지 확인 하십시오.<br />-는 유효성 검사 구성 마법사를 성공적으로 실행 클러스터 장애 조치를 확인 합니다.|  
|장애 클러스터 노드에서 WMI 통해 원격 관리에 사용할 수 있어야|하나 이상의 장애 클러스터 노드가 WMI(Windows Management Instrumentation) \(WMI\)를 사용 하 여 원격 관리에 대 한 사용 되지 않습니다. 원격 management 노드가 구성 되지 않은 경우 CAU 클러스터 노드에서 업데이트할 수 없습니다.|WMI 원격 관리에 대 한 모든 장애 클러스터 노드가 활성화 되어 있는지 확인 합니다. 자세한 내용은 참조 [구성에 대 한 원격 management 노드가](#BKMK_NODE_CONFIG) 이 항목의 합니다.|  
|PowerShell 원격 각 장애 클러스터 노드에서 사용 하도록 설정 되어야|PowerShell 설치 되어 있지 않으면 또는 하나 또는 여러 개의 장애 클러스터 노드에서 원격에 사용할 수 없습니다. CAU는 remote\ 업데이트 모드에 특정 기능을 사용 하거나 모드 self\ 업데이트에 대 한 구성할 수 없습니다.|PowerShell 모든 클러스터 노드에서 설치 되어 있고 원격을 사용할 수 있는지 확인 합니다.<br /><br />자세한 내용은 참조 [구성에 대 한 원격 management 노드가](#BKMK_NODE_CONFIG) 이 항목의 합니다.|  
|클러스터 장애 조치 버전|클러스터 장애 조치의에서 하나 이상의 노드 Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012를 실행 하지 마세요. CAU 클러스터 장애 조치를 업데이트할 수 없습니다.|Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 실행 BPA 때 지정 된 장애 클러스터 실행 되 고 있는지 확인 합니다.<br /><br />자세한 내용은 참조 [클러스터 구성 확인](#BKMK_REQ_CLUS) 이 항목의 합니다.|  
|모든 장애 클러스터 노드에서 필요한 버전의.NET Framework 및 Windows PowerShell가 설치 되어 있어야|.NET framework 4.6, 4.5 또는 Windows PowerShell 하나 또는 여러 개의 클러스터 노드에서 설치 되지 않습니다. 일부 CAU 기능이 작동 하지 않을 수 있습니다.|필요한 경우 모든 클러스터 노드에서.NET Framework 4.6 또는 4.5 및 Windows PowerShell 설치 되어 있는지 확인 합니다.<br /><br />자세한 내용은 참조 [구성에 대 한 원격 management 노드가](#BKMK_NODE_CONFIG) 이 항목의 합니다.|  
|클러스터 노드에서 클러스터 서비스가 실행 해야|하나 또는 여러 개의 노드에서 클러스터 서비스가 실행 되지 않습니다. CAU 클러스터 장애 조치를 업데이트할 수 없습니다.|-클러스터 서비스 \(clussvc\) 모든 노드에서 클러스터에 시작 되 고 자동으로 시작 되도록 구성 되어 있는지 확인 합니다.<br />-는 유효성 검사 구성 마법사를 성공적으로 실행 클러스터 장애 조치를 확인 합니다.<br /><br />자세한 내용은 참조 [클러스터 구성 확인](#BKMK_REQ_CLUS) 이 항목의 합니다.|  
|자동 업데이트 장애 클러스터 노드에서 업데이트를 자동으로 설치 하도록 구성 하지 않아야|하나 이상의 장애 클러스터 노드에서에서 자동 업데이트 해당 노드에서 Microsoft 업데이트를 자동으로 설치 하도록 구성 됩니다. 업데이트 다른 방법으로 CAU 결합 예기치 결과 또는 예상치 못한 작동 중지 될 수 있습니다.|기능이 Windows 업데이트를 하나 또는 여러 개의 클러스터 노드에서 자동 업데이트에 대 한 구성 된 경우 자동 업데이트를 자동으로 업데이트를 설치 하지 구성 되어 있는지 확인 합니다.<br /><br />자세한 내용은 참조 [Microsoft 업데이트 적용을 위한 권장](#BKMK_BP_WUA)합니다.|  
|장애 클러스터 노드에서 해야 동일한 업데이트 소스를 사용 하 여|하나 이상의 장애 클러스터 노드가 나머지 노드의에서는 다른 Microsoft 업데이트에 대 한 업데이트 원본을 사용 하도록 구성 됩니다. 업데이트가 수 적용 되지 일관 되 게 클러스터 노드에서 CAU 하 여 합니다.|예를 들어, WSUS 서버, Windows 업데이트를 또는 Microsoft 업데이트 동일한 업데이트 소스를 사용 하 여 모든 클러스터 노드에서 구성 되어 있는지 확인 합니다.<br /><br />자세한 내용은 참조 [Microsoft 업데이트 적용을 위한 권장](#BKMK_BP_WUA)합니다.|  
|원격 종료 수 있도록 해 주는 방화벽 규칙 장애 조치 클러스터에서 노드에서 각 사용 하도록 설정 해야|하나 이상의 장애 클러스터 노드가 원격 종료할 수 있도록 방화벽 규칙 사용할 수 없거나 그룹 정책 설정에서 활성화 되 고이 규칙 수 없습니다. 한 업데이트를 실행 노드 자동으로 다시 시작 해야 하는 업데이트가 적용 되는 올바르게 완료 되지 않을 수 있습니다.|Windows 방화벽 또는 non\ Microsoft 방화벽을 사용 중인 클러스터 노드에서 종료 원격 허용 하는 방화벽 규칙을 구성 합니다.<br /><br />자세한 내용은 참조 [자동 다시 시작 수 있도록 방화벽 규칙 활성화](#BKMK_FW) 이 항목의 합니다.|  
|각 장애 클러스터 노드에서 프록시 서버 설정이 로컬 프록시 서버 설정 해야|하나 이상의 장애 클러스터 노드가 잘못 프록시 서버 구성을 했습니다.<br /><br />로컬 프록시 서버를 사용 하는 경우 각 노드에서 프록시 서버 설정이 Microsoft 업데이트 또는 Windows 업데이트에 액세스 하 고 클러스터 제대로 구성 되어야 합니다.|필요한 경우 각 클러스터 노드에서 WinHTTP 프록시 설정 하는 로컬 프록시 서버 설정 되어 있는지 확인 합니다. 프록시 서버에 사용자 환경에 없는 경우에이 경고를 무시할 수 있습니다.<br /><br />자세한 내용은 참조 [지점 시나리오에서 업데이트를 적용](#BKMK_PROXY) 이 여기에 있습니다.|  
|CAU 클러스터 역할 self\ 업데이트 모드를 사용 하도록 클러스터 장애 조치에 설치 되어야|이 장애 클러스터에 CAU 클러스터 역할 설치 되지 않습니다. 이 역할은 클러스터 self\ 업데이트에 대 한 필요 합니다.|CAU self\ 업데이트 모드에서를 사용 하려면 다음 방법 중 하나에 클러스터 장애 조치 CAU 클러스터 역할을 추가 합니다.<br /><br />-실행는 [추가 CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/add-cauclusterrole) PowerShell cmdlet 합니다.<br />-선택는 **클러스터 self\ 업데이트 옵션을 구성** 클러스터 인식 업데이트 창으로 작업 합니다.|  
|CAU 클러스터 역할에서이 사용 클러스터 장애 조치 self\ 업데이트 모드를 설정 하려면|CAU 클러스터 역할은 사용할 수 없습니다. 예를 들어, CAU 클러스터 역할 설치 되어 있지 않으면 또는 사용 하 여 사용할 수 없을 [Disable\ CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/disable-cauclusterrole) PowerShell cmdlet 합니다. 이 역할은 클러스터 self\ 업데이트에 대 한 필요 합니다.|CAU self\ 업데이트 모드에서를 사용 하려면 다음 방법 중 하나에이 장애 클러스터에서 CAU 클러스터 역할을 사용할 다음과 같습니다.<br /><br />-실행는 [활성화 CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/enable-cauclusterrole) PowerShell cmdlet 합니다.<br />-선택는 **클러스터 self\ 업데이트 옵션을 구성** 클러스터 인식 업데이트 창으로 작업 합니다.|  
|모든 장애 클러스터 노드에서 plug\에서 모드 self\ 업데이트에 대 한 구성 된 CAU 등록 되어 있어야|하나 이상의이 장애 클러스터 노드에서 클러스터 CAU 역할 self\ 업데이트 옵션에서 구성 된 모듈 plug\에서 CAU 액세스할 수 없습니다. 한 self\ 업데이트를 실행 실패할 수 있습니다.|-CAU plug\에서 제공 하는 제품에 대 한 설치 절차를 수행 하 여 모든 클러스터 노드에서 plug\에서 구성 된 CAU 설치 되어 있는지 확인 합니다.<br />-실행는 [Register\ CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) PowerShell cmdlet 필요한 클러스터 노드에서 plug\-에 등록할 수 있습니다.|  
|모든 장애 클러스터 노드에서 등록 된 CAU plug\ 기능 동일한 설정을 해야 합니다.|일부 클러스터 노드에서 사용할 수 있는 하나를 변경 된 구성 업데이트를 실행 하는 데 사용할 plug\ 기능에 self\ 업데이트를 실행 실패할 수 있습니다.|-CAU plug\에서 제공 하는 제품에 대 한 설치 절차를 수행 하 여 모든 클러스터 노드에서 plug\에서 구성 된 CAU 설치 되어 있는지 확인 합니다.<br />-실행는 [Register\ CauPlugin](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/register-cauplugin) PowerShell cmdlet 필요한 클러스터 노드에서 plug\-에 등록할 수 있습니다.|  
|구성된 업데이트를 실행 옵션 유효한 해야 합니다.|일정 self\ 업데이트 및이 장애 클러스터에 대 한 구성 업데이트를 실행 옵션 완료 되지 않은 또는 잘못 되었습니다. 한 self\ 업데이트를 실행 실패할 수 있습니다.|유효한 self\ 업데이트 일정 및 업데이트를 실행 하는 옵션을 구성 합니다. 예를 들어 사용할 수 있습니다의 [Set\ CauClusterRole](https://technet.microsoft.com/itpro/powershell/windows/cluster-aware-updating/set-cauclusterrole) 클러스터 역할 PowerShell cmdlet는 CAU 구성할 수 있습니다.|  
|두 개 이상의 장애 클러스터 노드에서 클러스터 CAU 역할의 소유자 해야 합니다.|CAU 클러스터 역할으로 이동 하려면 가능한 소유자로 노드 없기 때문에 업데이트를 실행 self\ 업데이트 모드로 시작 되지 것입니다.|장애 클러스터링 도구를 사용 하 여 모든 클러스터 노드에서 클러스터 역할은 CAU의 가능한 소유자도 구성 되어 있는지 확인 하려면. 기본 설정입니다.||  
|모든 장애 클러스터 노드가 Windows PowerShell 스크립트에 액세스할 수 있어야 합니다.|일부 가능한 소유자로 노드 CAU 클러스터 역할의 구성 된 Windows PowerShell pre\ 업데이트 및 업데이트 post\ 스크립트 액세스할 수 있습니다. 한 self\ 업데이트를 실행 하지 못합니다.|모든 가능한 소유자로 노드의 클러스터 CAU 역할 구성 된 PowerShell pre\ 업데이트 및 업데이트 post\ 스크립트 액세스할 수 있는 권한이 있는지 확인 합니다.|  
|동일한 Windows PowerShell 스크립트를 사용 하는 모든 장애 클러스터 노드에서 해야|CAU 클러스터 역할의 일부 가능한 소유자로 노드 지정 된 Windows PowerShell pre\ 업데이트와 post\ 업데이트 스크립트 같은 복사본을 사용 합니다. Self\ 업데이트 실행 되는 못하거나 예기치 않은 문제가 표시 될 수 있습니다.|모든 가능한 소유자로 노드의 클러스터 CAU 역할 동일한 PowerShell pre\ 업데이트 및 업데이트 post\ 스크립트 사용 하 여 확인 합니다.|  
|실행 업데이트에 대해 지정 WarnAfter 설정은 StopAfter 설정을 보다 작음 되어야|지정된 된 CAU 실행 업데이트 시간 제한 값 효과가 경고 시간 초과 확인합니다. 경고 이벤트 로그를 생성 하기 전에 업데이트 실행 취소할 수 있습니다.|구성 업데이트를 실행 옵션에는 **WarnAfter** 옵션은 값 보다 작은 **StopAfter** 옵션 값 합니다.|  
  
## <a name="see-also"></a>참조 하십시오  
  
-   [개요 클러스터 인식 업데이트](cluster-aware-updating.md)
  
