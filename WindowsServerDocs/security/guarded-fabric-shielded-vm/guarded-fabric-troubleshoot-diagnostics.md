---
title: 보호 된 패브릭 진단 도구를 사용 하 여 문제 해결
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 07691d5b-046c-45ea-8570-a0a85c3f2d22
manager: dongill
author: huu
ms.technology: security-guarded-fabric
ms.openlocfilehash: c102fa0503e6aac279235e1243b55e0e3cf81e1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812414"
---
# <a name="troubleshooting-using-the-guarded-fabric-diagnostic-tool"></a>보호 된 패브릭 진단 도구를 사용 하 여 문제 해결

>적용 대상: Windows Server, Windows Server 2016, Windows Server (반기 채널) 2019

이 항목에서는 보호 된 패브릭 진단 도구를 식별 하 여 배포, 구성 및 보호 된 패브릭 인프라의 진행 중인 작업의 일반적인 오류 해결의 사용을 설명 합니다. 호스트 보호자 서비스 (HGS), 보호 된 모든 호스트 및 DNS와 Active Directory와 같은 지원 서비스가 포함 됩니다. 중단을 해결 하 고 잘못 구성 된 자산에 대 한 관리자 시작 지점을 제공 하는 실패 한 보호 된 패브릭 분류에 첫 번째 단계를 수행 하는 진단 도구를 사용할 수 있습니다. 도구 보호 된 패브릭 운영의 사운드 이해도 대 한 대체 아니며 일상적인 작업 중 발생 하는 가장 일반적인 문제를 신속 하 게 확인 하는 역할만 합니다.

이 항목에 사용 되는 cmdlet의 설명서에서 확인할 수 있습니다 [TechNet](https://technet.microsoft.com/library/mt718834.aspx)합니다.

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

# <a name="quick-start"></a>빠른 시작

로컬 관리자 권한으로 Windows PowerShell 세션에서 다음을 호출 하 여 보호 된 호스트 또는 HGS 노드를 진단할 수 있습니다.
```PowerShell
Get-HgsTrace -RunDiagnostics -Detailed
```
이 자동으로 현재 호스트의 역할 검색를 자동으로 검색할 수 있는 모든 관련 문제를 진단 합니다.  이 프로세스 중에 생성 된 결과의 모든 있어 표시 됩니다는 `-Detailed` 전환 합니다.

이 항목의 나머지 고급 사용에 자세한 연습을 제공 합니다 `Get-HgsTrace` 에 한 번에 여러 호스트를 진단 하 고 복잡 한 노드 간 구성 오류 검색 등을 수행 합니다.

## <a name="diagnostics-overview"></a>진단 개요
보호 된 패브릭 진단 차폐 가상 컴퓨터를 사용 하 여 모든 호스트에서 사용할 수 있는 관련 도구 및 기능 설치 Server Core를 실행 하는 호스트를 포함 합니다.  현재 진단 기능/패키지를 사용 하 여 포함 됩니다.

1. 호스트 보호자 서비스 역할
2. 호스트 보호 Hyper-V 지원
3. 패브릭 관리를 위한 VM 보호 도구
4. RSAT(원격 서버 관리 도구)

즉, 진단 도구에서 모든 보호 된 호스트를 HGS 노드, 특정 패브릭 관리 서버 및 모든 Windows 10 워크스테이션에 사용할 수 있도록 [RSAT](https://www.microsoft.com/download/details.aspx?id=45520) 설치 합니다.  진단에서 모든 보호 된 호스트 또는 보호 된 패브릭;에서 HGS 노드 진단 목적으로 위의 컴퓨터 중 하나라도 호출할 수 있습니다. 진단을 원격 추적 대상을 사용 하 여를 찾은 후 진단 유틸리티를 실행 하는 컴퓨터 이외의 다른 호스트에 연결 합니다.

진단에 의해 대상으로 하는 모든 호스트 "추적 대상입니다." 라고  추적 대상 역할와 호스트 이름으로 식별 됩니다.  보호 된 패브릭의 주어진된 추적 대상 수행 기능을 설명 하는 역할입니다.  추적 지원 대상으로 하는 현재 `HostGuardianService` 고 `GuardedHost` 역할입니다.  한 번에 여러 역할을 차지 하는 호스트 수 및 프로덕션 환경에서 수행 하지 해야이 있지만 진단에 의해 지원 됩니다.  HGS 및 Hyper-v 호스트를 별도로 유지 해야 하 고 고유 항상 합니다.

관리자를 실행 하 여 진단 작업을 시작할 수 `Get-HgsTrace`입니다.  이 명령은 런타임에 제공 하는 스위치를 기반으로 하는 두 가지 고유한 기능을 수행 합니다: 컬렉션 및 진단 추적 합니다.  이 두 가지가 결합 전체 보호 된 패브릭 진단 도구를 구성 합니다.  명시적으로 필요한 경우에 가장 유용한 진단만 수집할 수 있는 관리자 자격 증명을 사용 하 여 추적 대상에서 추적 해야 합니다.  권한이 부족 하 여 추적 컬렉션을 실행 하는 사용자에서 보유 하는, 추적 권한 상승이 필요한 다른 모든 사용자를 통과 하는 동안 실패 합니다.  심사를 수행 하는 언더 권한 연산자는 이벤트 부분 진단할 수 있습니다. 

### <a name="trace-collection"></a>추적 컬렉션
기본적으로 `Get-HgsTrace` 만 추적을 수집 하 고 임시 폴더에 저장 됩니다.  추적은 호스트를 구성 하는 방법을 설명 하는 특수 한 형식의 파일을 사용 하 여 입력 대상된 호스트의 이름을 딴 폴더의 형태를 취하 합니다.  또한 추적은 추적을 수집 하려면 진단 된 호출 하는 방법을 설명 하는 메타 데이터를 포함 합니다.  이 데이터는 수동 진단을 수행 하는 경우 호스트에 대 한 정보를 리하이드레이션을 진단에서 사용 됩니다.

필요한 경우 추적은 수동으로 검토할 수 있습니다.  모든 형식의 읽을 (xml) 또는 표준 도구를 사용 하 여 쉽게 검사할 수 있습니다 (예: X509 인증서 및 암호화 Windows 셸 확장).  추적 수동 진단을 위해 설계 되지 않았습니다 하는 것이 항상 더 단의 진단 기능을 사용 하 여 추적을 처리 하는 데 효과적인 `Get-HgsTrace`합니다.

추적 컬렉션을 실행 한 결과 지정된 된 호스트의 상태에 대 한 모든 표시를 수행 하지 마세요.  단순히 추적 성공적으로 수집 된를 나타냅니다.  진단 기능을 사용 하는 데 필요한 것 `Get-HgsTrace` 추적 실패 환경을 나타내는 경우를 확인 하려면.

사용 하 여 `-Diagnostic` 매개 변수를 지정 된 진단 작동 하는 데 필요한 추적만 추적 컬렉션을 제한할 수 있습니다.  이 진단 프로그램을 실행 하는 데 필요한 권한과 함께 수집 된 데이터의 양을 줄입니다.

### <a name="diagnosis"></a>진단
제공 하 여 수집 된 추적을 진단할 수 있습니다 `Get-HgsTrace` 를 통해 추적의 위치를 `-Path` 매개 변수 및 지정 하는 `-RunDiagnostics` 전환 합니다.  또한 `Get-HgsTrace` 수행할 수 수집 및 진단 단일 패스에서 제공 하 여는 `-RunDiagnostics` 스위치 및 추적 대상 목록입니다.  추적 대상이 없습니다. 제공 된 경우 현재 컴퓨터에서 설치 된 Windows PowerShell 모듈을 검사 하 여 유추 하는 역할을 사용 하 여 암시적를 대상으로 사용 됩니다.

진단은 추적 대상, 진단 집합을 보여 주는 계층 구조 형식에는 결과 제공 하 고 개별 진단에서는 특정 오류에 대 한 책임이 있습니다.  오류 확인 수 있으면 어떤 조치 취할지 다음에 대 한 재구성 및 권장 해결 방법 포함 합니다.  기본적으로 결과 전달 하 고 무관 숨겨져 있습니다.  모든 진단 테스트를 보려면 지정 된 `-Detailed` 전환 합니다.  이렇게 하면 모든 결과 상태에 관계 없이 표시 합니다.

사용 하 여 실행 되는 진단 집합을 제한할 수 있기를 `-Diagnostic` 매개 변수입니다.  추적 대상에 대해 진단의 클래스를 실행할지 지정할 수 있습니다이 고 다른 모든 사용자를 표시 안 함.  사용 가능한 진단 클래스의 예로 네트워킹, 모범 사례 및 클라이언트 하드웨어.  참조를 [cmdlet 설명서](https://technet.microsoft.com/library/mt718831.aspx) 사용 가능한 진단의 최신 목록을 찾을 수 있습니다.

> [!WARNING]
> 진단 강력한 모니터링 및 인시던트 응답 파이프라인에 대 한 대체 않습니다.  문제를 조기에 감지를 모니터링할 수 있는 다양 한 이벤트 로그 채널 뿐만 아니라 보호 된 패브릭 모니터링에 사용 가능한 System Center Operations Manager 패키지가 있습니다.  그런 다음 진단 신속 하 게 이러한 오류를 심사 하 고 일련의 동작 설정에 사용할 수 있습니다.

## <a name="targeting-diagnostics"></a>진단 대상

`Get-HgsTrace` 추적 대상에 대해 작동합니다.  추적 대상이 HGS 노드 또는 보호 된 패브릭 내에서 보호 된 호스트에 해당 하는 개체입니다.  확장으로 생각할 수 있습니다는 `PSSession` 패브릭에서 호스트의 역할과 같은 진단만 필요한 정보를 포함 하는 합니다.  대상이 될 수 있습니다 (예: 로컬 또는 수동 진단) 암시적으로 생성 또는 명시적으로 `New-HgsTraceTarget` 명령입니다.

### <a name="local-diagnosis"></a>로컬 진단

기본적으로 `Get-HgsTrace` (즉, 여기서 cmdlet가 호출 될) 로컬 호스트를 대상으로 합니다.  이 암시적 로컬 대상 이라고 합니다.  대상이 없습니다.에서 제공 되는 경우에 암시적 로컬 대상 되는 `-Target` 매개 변수 및 없는 기존 추적에서 발견 되는 `-Path`합니다.

암시적 로컬 대상 역할 유추를 사용 하 여 현재 호스트 보호 된 패브릭에서 수행 하는 역할을 결정 합니다.  이 대략 해당 시스템에서 기능 설치 하는 설치 된 Windows PowerShell 모듈을 기반으로 합니다.  현재 상태를 `HgsServer` 모듈에는 추적 대상의 역할을 수행 하면 `HostGuardianService` 의 존재에는 `HgsClient` 모듈 추적 대상의 역할을 수행 하면 `GuardedHost`합니다.  두 모듈을 둘 다로 처리 됩니다 하는 경우에서 존재 하도록 지정된 된 호스트 수를 `HostGuardianService` 및 `GuardedHost`합니다.

따라서 로컬에서 추적을 수집 하는 것에 대 한 진단의 기본 호출 합니다.
```PowerShell
Get-HgsTrace
```
... 다음과 같습니다.
```PowerShell
New-HgsTraceTarget -Local | Get-HgsTrace
```
> [!TIP]
> `Get-HgsTrace` 대상을 통해 직접 또는 파이프라인을 통해 사용할 수는 `-Target` 매개 변수입니다.  운영상 둘 사이는 차이점이 있습니다.

### <a name="remote-diagnosis-using-trace-targets"></a>원격 진단 사용 하 여 추적 대상

원격으로 원격 연결 정보를 사용 하 여 추적 대상을 생성 하 여 호스트를 진단 하는 것이 가능 합니다.  반드시 필요한 것은 호스트 이름 및 Windows PowerShell 원격을 사용 하 여 연결할 수 있는 자격 증명 집합을 합니다.
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $server
```
이 예제에서는 원격 사용자 자격 증명을 수집 하 라는 메시지가 발생 합니다. 다음 진단은를 실행 하 여 원격 호스트에 `hgs-01.secure.contoso.com` 추적 수집을 완료 합니다.  결과 추적 localhost에 다운로드 되 고 진단 합니다.  진단 결과 수행할 때와 동일 하 게 표시 됩니다 [로컬 진단을](#local-diagnosis)합니다.  마찬가지로 원격 시스템에 설치 된 Windows PowerShell 모듈 기반의 유추할 수 있습니다. 역할을 지정 하는 데 필요한 아닙니다.

원격 진단 원격 호스트에 대 한 모든 액세스에 대 한 Windows PowerShell 원격 기능을 활용합니다.  추적 대상 있는 Windows PowerShell 원격을 사용 하는 필수 구성 요소 이므로 (참조 [PSRemoting 사용](https://technet.microsoft.com/library/hh849694.aspx)) localhost 제대로 되었는지 및 대상에 대 한 연결을 시작 하는 것에 대 한 구성 합니다.

> [!NOTE]
> 대부분의 경우에는 localhost 동일한 Active Directory 포리스트에 포함 되도록 있으며, 올바른 DNS 호스트 이름을 사용 하는 데 필요한만 합니다.  WinRM 설정 등의 추가 구성을 수행 해야 사용자 환경 활용을 더 복잡 한 페더레이션 모델 또는 연결에 대 한 직접 IP 주소를 사용 하려는 경우 [신뢰할 수 있는 호스트](https://technet.microsoft.com/library/ff700227.aspx)합니다.

추적 대상 인스턴스화하고 사용 하 여 연결을 허용 하는 것에 대 한 구성 제대로 확인할 수 있습니다는 `Test-HgsTraceTarget` cmdlet:
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
$server | Test-HgsTraceTarget
```
이 명령은 반환 `$True` 경우에 `Get-HgsTrace` 추적 대상 사용 하 여 원격 진단 세션을 설정할 수 있게 됩니다.  실패 하면이 cmdlet은 Windows PowerShell 원격 연결의 추가 문제 해결에 대 한 관련 상태 정보를 반환 합니다.

#### <a name="implicit-credentials"></a>암시적 자격 증명

자격 증명을 제공할 필요가 없는 원격 진단 추적 대상에 원격으로 연결할 충분 한 권한이 있는 사용자에서를 수행할 때 `New-HgsTraceTarget`합니다.  `Get-HgsTrace` cmdlet은 자동으로 연결을 열 때 cmdlet을 호출 하는 사용자의 자격 증명을 다시 사용 합니다.

> [!WARNING]
> "두 번째 홉." 라고 수행 하는 경우에 특히 자격 증명을 다시 사용 하려면 몇 가지 제한 사항이 적용 됩니다.  이 자격 증명에서 원격 세션 내에서 다른 컴퓨터를 다시 사용 하려고 할 때 발생 합니다.  필요가 [CredSSP 설정](https://technet.microsoft.com/library/hh849872.aspx) 있지만이 시나리오를 지원 하기 위해이 보호 된 패브릭 관리 및 문제 해결의 범위 밖에 있습니다.

#### <a name="using-windows-powershell-just-enough-administration-jea-and-diagnostics"></a>Just Enough Administration (JEA) and 진단 Windows PowerShell을 사용 하 여

원격 진단 Windows PowerShell 제한 된 JEA 끝점의 사용을 지원 합니다. 기본적으로 원격 추적 대상 기본값을 사용 하 여 연결 합니다 `microsoft.powershell` 끝점입니다.  추적 대상에는 `HostGuardianService` 역할에도 하려고 사용 하 여는 `microsoft.windows.hgs` HGS를 설치할 때 구성 된 끝점입니다.

세션 구성 이름을 사용 하 여 추적 대상 생성 하는 동안 지정 해야 사용자 지정 끝점을 사용 하려는 경우는 `-PSSessionConfigurationName` 매개 변수를 같은 아래:

```PowerShell
New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential) -PSSessionConfigurationName "microsoft.windows.hgs"
```

#### <a name="diagnosing-multiple-hosts"></a>여러 호스트를 진단합니다.

여러 추적 대상에 전달할 수 있습니다 `Get-HgsTrace` 한 번에 있습니다.  이 로컬 및 원격 대상의 조합이 포함 됩니다.  각 대상에서 추적 되 고 모든 대상에서 추적을 동시에 진단할 수는 다음입니다.  진단 도구 배포의 향상 된 기술 자료를 사용 수 없는 감지할 수 있는 복잡 한 노드 간 구성 오류를 식별할 수 있습니다.  추적 또는 동시에 (의 경우 수동 진단) 여러 호스트에서 여러 대상 호스트를 호출할 때 제공 하기만이 기능을 사용 하 여 `Get-HgsTrace` (의 경우 원격 진단).

다음은 시작에 사용 되는 보호 된 호스트 중 하나 심사 두 HGS 노드의 구성 된 패브릭 및 두 명의 보호 된 호스트에 원격 진단에 사용 하는 예제 `Get-HgsTrace`합니다.

```PowerShell
$hgs01 = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Credential (Enter-Credential)
$hgs02 = New-HgsTraceTarget -HostName "hgs-02.secure.contoso.com" -Credential (Enter-Credential)
$gh01 = New-HgsTraceTarget -Local
$gh02 = New-HgsTraceTarget -HostName "guardedhost-02.contoso.com"
Get-HgsTrace -Target $hgs01,$hgs02,$gh01,$gh02 -RunDiagnostics
```

> [!NOTE]
> 여러 노드를 진단 하는 경우 전체에 보호 된 패브릭 진단 필요가 없습니다.  대부분의 경우에서는 지정 된 오류 조건에 관련 될 수 있는 모든 노드를 포함 하는 데 충분 합니다.  이것이 일반적으로 보호 된 호스트 및 일부 HGS 클러스터에서 노드 수의 하위 집합입니다.

## <a name="manual-diagnosis-using-saved-traces"></a>저장 된 추적을 사용 하 여 수동 진단

추적을 다시 수집 하지 않고 진단 유틸리티를 다시 실행 하려는 경우에 따라 또는 원격으로 모든 패브릭에 호스트를 동시에 진단 하는 데 필요한 자격 증명이 없을 수 있습니다.  수동 진단이는 여전히 수행할 수 있습니다 사용 하 여 전체 fabric 심사 메커니즘 `Get-HgsTrace`, 원격 추적 컬렉션을 사용 하지 않습니다.

수동 진단을 수행 하기 전에 확인을 심사는 패브릭에서 각 호스트의 관리자가 준비 및 사용자를 대신해 명령을 실행 하려고 해야 합니다.  이것은 다른 사용자에 게이 정보를 노출 하는 안전한 지 확인 하려면 사용자의 책임 진단 추적 출력은 일반적으로 중요 하 게 표시 되는 모든 정보를 노출 하지 않습니다.

> [!NOTE]
> 추적은 익명으로 처리 및 네트워크 구성, PKI 설정 및 기타 구성 간주 되는 경우에 따라 개인 정보를 표시 합니다.  따라서 추적만 있어야 조직 내에서 신뢰할 수 있는 엔터티를 전송 하 고 공개적으로 게시 되지 않습니다.

수동 진단을 수행 하는 단계는 다음과 같습니다.

1. 각 호스트 관리자를 실행 하는 요청 `Get-HgsTrace` 알려진 지정 `-Path` 목록과 결과 추적에 대해 실행 하려는 진단 합니다.  예를 들어 다음과 같은 가치를 제공해야 합니다.

 ```PowerShell
 Get-HgsTrace -Path C:\Traces -Diagnostic Networking,BestPractices
 ```
2. 각 호스트 관리자 결과 traces 폴더를 패키지 하 고 사용자에 게 보낼 요청.  파일 공유 또는 운영 정책 및 조직에서 설정 하는 절차에 따라 다른 메커니즘을 통해 전자 메일을 통해이 프로세스를 구동 될 수 있습니다.

3. 다른 콘텐츠 또는 폴더를 사용 하 여 단일 폴더에 받은 모든 추적을 병합 합니다.

    * 예를 들어, 가정 했습니다 라는 4 개의 컴퓨터에서 수집 된 추적 하 여 관리자 송신 HGS-01, 02 HGS, RR1N2608-12 및 RR1N2608 13입니다.  각 관리자는 발송 폴더 같은 이름으로 합니다.  다음과 같이 표시 되는 디렉터리 구조를 어셈블할 때:

      ```
      FabricTraces
      |- HGS-01
      |  |- TargetMetadata.xml
      |  |- Metadata.xml
      |  |- [any other trace files for this host]
      |- HGS-02
      |  |- [...]
      |- RR1N2608-12
      |  |- [...]
      |- RR1N2608-13
         |- [..]
      ```

4. 어셈블된 추적 폴더의 경로를 제공 하는 진단 실행 합니다 `-Path` 매개 변수 및 지정 하는 `-RunDiagnostics` 해당 진단 추적을 수집 하려면 관리자에 게 묻는 뿐만 아니라 전환 합니다.  진단 경로 내에서 발견 된 호스트에 액세스할 수 없습니다 하 고 사전 수집 된 추적만을 사용 하려고 하므로 가정 합니다.  모든 추적 누락 되거나 손상 된 경우 진단 영향을 받는 테스트만 실패를 업데이트 하 고 정상적으로 진행 됩니다.  예를 들어 다음과 같은 가치를 제공해야 합니다.

 ```PowerShell
 Get-HgsTrace -RunDiagnostics -Diagnostic Networking,BestPractices -Path ".\FabricTraces"
 ```

### <a name="mixing-saved-traces-with-additional-targets"></a>추가 대상을 사용 하 여 추적을 저장 혼합

경우에 따라 추가 호스트 추적을 사용 하 여 보강 하려는 미리 수집 된 추적의 집합을 할 수 있습니다.  추적 및 진단의 단일 호출에서 진단 됩니다 하는 추가 대상으로 미리 수집 된 추적을 혼합 하는 것이 가능 합니다.

수집 하 여 위에서 지정한 추적 폴더를 조합 하는 지침, 호출 `Get-HgsTrace` 추가 추적 대상이 미리 수집 된 추적 폴더에서 찾을 수 없습니다.

```PowerShell
$hgs03 = New-HgsTraceTarget -HostName "hgs-03.secure.contoso.com" -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $hgs03 -Path .\FabricTraces
``` 

진단 cmdlet을 미리 수집 된 모든 호스트 및 추적 해야 하는 하나의 추가 호스트 식별 하는 하 고 필요한 추적을 수행 합니다.  다음 모든 사전 수집 하 고 새로 수집 된 추적의 합계를 진단할 수 됩니다.  결과 추적 폴더에는 이전 및 새 추적을 모두 포함 됩니다.
