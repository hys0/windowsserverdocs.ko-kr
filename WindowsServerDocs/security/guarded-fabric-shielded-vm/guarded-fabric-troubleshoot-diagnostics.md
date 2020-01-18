---
title: 보호 된 패브릭 진단 도구를 사용 하 여 문제 해결
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 07691d5b-046c-45ea-8570-a0a85c3f2d22
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/14/2020
ms.openlocfilehash: c69fc70282ff61ecce25f6413244d7ba3a5ba3bc
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265825"
---
# <a name="troubleshooting-using-the-guarded-fabric-diagnostic-tool"></a>보호 된 패브릭 진단 도구를 사용 하 여 문제 해결

>적용 대상: Windows Server 2019, Windows Server (반기 채널), Windows Server 2016

이 항목에서는 보호 된 Fabric 진단 도구를 사용 하 여 보호 된 패브릭 인프라의 배포, 구성 및 진행 중인 작업에서 일반적인 오류를 식별 하 고 수정 하는 방법을 설명 합니다. 여기에는 HGS (호스트 보호 서비스), 모든 보호 된 호스트 및 지원 서비스 (예: DNS 및 Active Directory)가 포함 됩니다. 진단 도구를 사용 하 여 장애 조치 (failover) 된 패브릭의 심사를 통해 첫 번째 단계를 수행 하 여 중단을 해결 하 고 잘못 구성 된 자산을 식별할 수 있는 시작 지점을 관리자에 게 제공할 수 있습니다. 이 도구는 보호 된 패브릭을 운영 하는 소리를 대체 하지 않으며 일상적인 작업 중에 발생 하는 가장 일반적인 문제를 신속 하 게 확인 하는 데에만 사용 됩니다.

이 문서에 사용 된 cmdlet에 대 한 전체 설명서는 [HgsDiagnostics 모듈 참조](https://docs.microsoft.com/powershell/module/hgsdiagnostics/?view=win10-ps)에서 찾을 수 있습니다.

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)]

## <a name="quick-start"></a>빠른 시작

로컬 관리자 권한으로 Windows PowerShell 세션에서 다음을 호출 하 여 보호 된 호스트나 HGS 노드를 진단할 수 있습니다.

```PowerShell
Get-HgsTrace -RunDiagnostics -Detailed
```

그러면 현재 호스트의 역할이 자동으로 검색 되어 자동으로 검색 될 수 있는 관련 문제를 진단 합니다.  이 프로세스 중에 생성 된 모든 결과는 `-Detailed` 스위치가 있기 때문에 표시 됩니다.

이 항목의 나머지 부분에서는 여러 호스트를 한 번에 진단 하 고 복잡 한 노드 간 구성 오류를 검색 하는 등의 작업을 수행 하기 위한 `Get-HgsTrace`의 고급 사용에 대 한 자세한 연습을 제공 합니다.

## <a name="diagnostics-overview"></a>진단 개요

보호 된 패브릭 진단은 Server Core를 실행 하는 호스트를 포함 하 여 보호 된 가상 머신 관련 도구 및 기능이 설치 된 모든 호스트에서 사용할 수 있습니다.  현재 진단은 다음과 같은 기능/패키지에 포함 되어 있습니다.

1. 호스트 보호자 서비스 역할
2. 호스트 보호 Hyper-V 지원
3. 패브릭 관리를 위한 VM 보호 도구
4. RSAT(원격 서버 관리 도구)

즉, 모든 보호 된 호스트, HGS 노드, 특정 패브릭 관리 서버, [RSAT](https://www.microsoft.com/download/details.aspx?id=45520) 가 설치 된 Windows 10 워크스테이션에서 진단 도구를 사용할 수 있습니다.  보호 된 패브릭의 보호 된 호스트나 HGS 노드를 진단 하기 위해 위의 모든 컴퓨터에서 진단을 호출할 수 있습니다. 진단은 원격 추적 대상을 사용 하 여 진단을 실행 하는 컴퓨터 이외의 호스트를 찾아서 연결할 수 있습니다.

진단을 대상으로 하는 모든 호스트를 "추적 대상" 이라고 합니다.  추적 대상은 해당 호스트 이름과 역할로 식별 됩니다.  역할은 지정 된 추적 대상이 보호 된 패브릭에서 수행 하는 함수를 설명 합니다.  현재 추적 대상은 `HostGuardianService` 및 `GuardedHost` 역할을 지원 합니다.  참고 호스트는 한 번에 여러 역할을 수행할 수 있으며,이는 진단 에서도 지원 되지만 프로덕션 환경에서는 수행할 수 없습니다.  HGS 및 Hyper-v 호스트는 항상 별도로 유지 해야 합니다.

관리자는 `Get-HgsTrace`를 실행 하 여 모든 진단 작업을 시작할 수 있습니다.  이 명령은 런타임에 제공 되는 스위치 (추적 수집 및 진단)를 기반으로 하는 두 가지 기능을 수행 합니다.  이러한 두 가지 조합은 보호 된 패브릭 진단 도구 전체를 구성 합니다.  명시적으로 필수는 아니지만 대부분의 유용한 진단에는 추적 대상의 관리자 자격 증명만 수집할 수 있는 추적이 필요 합니다.  추적 수집을 실행 하는 사용자가 충분 한 권한을 보유 하지 않는 경우 권한 상승이 필요한 추적이 실패 하 고 다른 모든 사용자가 통과 하 게 됩니다.  이를 통해 권한 있는 운영자가 심사를 수행 하는 경우 부분 진단을 수행할 수 있습니다. 

### <a name="trace-collection"></a>추적 컬렉션

기본적으로 `Get-HgsTrace`는 추적만 수집 하 여 임시 폴더에 저장 합니다.  추적은 대상 호스트 이름 뒤에 이름이 지정 된 폴더 형식을 사용 하 여 호스트 구성 방법을 설명 하는 특수 형식의 파일로 채워집니다.  추적에는 추적을 수집 하기 위해 진단이 호출 된 방법을 설명 하는 메타 데이터도 포함 됩니다.  이 데이터는 진단에서 수동 진단을 수행할 때 호스트에 대 한 정보를 리하이드레이션 하는 데 사용 됩니다.

필요한 경우 추적을 수동으로 검토할 수 있습니다.  모든 형식은 사람이 읽을 수 있는 (XML) 이거나 표준 도구 (예: X509 인증서 및 Windows Crypto Shell 확장)를 사용 하 여 쉽게 검사할 수 있습니다.  그러나 추적은 수동 진단을 위해 설계 되지 않으며 `Get-HgsTrace`진단 기능을 사용 하 여 추적을 처리 하는 것이 항상 효과적입니다.

추적 컬렉션을 실행 한 결과는 지정 된 호스트의 상태를 표시 하지 않습니다.  단순히 추적이 성공적으로 수집 되었음을 나타내는 것입니다.  `Get-HgsTrace`의 진단 기능을 사용 하 여 추적이 실패 한 환경을 표시 하는지 여부를 확인 해야 합니다.

`-Diagnostic` 매개 변수를 사용 하 여 지정 된 진단을 운영 하는 데 필요한 추적 으로만 추적 컬렉션을 제한할 수 있습니다.  이렇게 하면 수집 되는 데이터의 양과 진단을 호출 하는 데 필요한 사용 권한이 줄어듭니다.

### <a name="diagnosis"></a>진단

`-Path` 매개 변수를 통해 추적 위치 `Get-HgsTrace` 제공 하 고 `-RunDiagnostics` 스위치를 지정 하 여 수집 된 추적을 진단할 수 있습니다.  또한 `-RunDiagnostics` 스위치 및 추적 대상 목록을 제공 하 여 단일 패스에서 수집 및 진단을 수행할 수 `Get-HgsTrace`.  추적 대상이 제공 되지 않으면 현재 컴퓨터는 암시적 대상으로 사용 되며, 설치 된 Windows PowerShell 모듈을 검사 하 여 역할이 유추 됩니다.

진단은 특정 실패를 담당 하는 추적 대상, 진단 집합 및 개별 진단을 나타내는 계층 형식으로 결과를 제공 합니다.  오류에는 다음에 수행 해야 할 작업에 대 한 결정을 할 수 있는 경우 수정 및 해결 권장 사항이 포함 됩니다.  기본적으로 전달 및 관련이 없는 결과는 숨겨집니다.  진단에서 테스트 된 모든 항목을 보려면 `-Detailed` 스위치를 지정 합니다.  이렇게 하면 상태에 관계 없이 모든 결과가 표시 됩니다.

`-Diagnostic` 매개 변수를 사용 하 여 실행 되는 진단 집합을 제한할 수 있습니다.  이를 통해 추적 대상에 대해 실행할 진단 클래스를 지정 하 고 다른 모든 항목을 표시 하지 않을 수 있습니다.  사용 가능한 진단 클래스의 예로는 네트워킹, 모범 사례, 클라이언트 하드웨어 등이 있습니다.  사용 가능한 진단의 최신 목록을 보려면 [cmdlet 설명서](https://technet.microsoft.com/library/mt718831.aspx) 를 참조 하세요.

> [!WARNING]
> 진단은 강력한 모니터링 및 인시던트 응답 파이프라인을 대체 하지 않습니다.  보호 된 패브릭을 모니터링 하는 데 사용할 수 있는 System Center Operations Manager 패키지와 조기에 문제를 검색 하기 위해 모니터링할 수 있는 다양 한 이벤트 로그 채널이 있습니다.  그런 다음 진단을 사용 하 여 이러한 오류를 신속 하 게 심사 하 고 조치를 세울 수 있습니다.

## <a name="targeting-diagnostics"></a>진단 대상 지정

`Get-HgsTrace`는 추적 대상에 대해 작동 합니다.  추적 대상은 보호 된 패브릭 내에서 HGS 노드나 보호 된 호스트에 해당 하는 개체입니다.  이는 패브릭에서 호스트의 역할과 같은 진단에 의해서만 필요한 정보를 포함 하는 `PSSession`에 대 한 확장으로 간주할 수 있습니다.  대상은 암시적으로 생성 하거나 (예: 로컬 또는 수동 진단) `New-HgsTraceTarget` 명령을 사용 하 여 명시적으로 생성할 수 있습니다.

### <a name="local-diagnosis"></a>로컬 진단

기본적으로 `Get-HgsTrace`는 localhost를 대상으로 합니다 (즉, cmdlet이 호출 되는 위치).  이를 암시적 로컬 대상 이라고 합니다.  암시적 로컬 대상은 `-Target` 매개 변수에 대상이 제공 되지 않고 `-Path`에서 기존 추적을 찾을 수 없는 경우에만 사용 됩니다.

암시적 로컬 대상은 역할 유추를 사용 하 여 보호 된 패브릭에서 현재 호스트가 재생 하는 역할을 결정 합니다.  이는 시스템에 설치 된 기능과 거의 일치 하는 설치 된 Windows PowerShell 모듈을 기반으로 합니다.  `HgsServer` 모듈이 있으면 추적 대상이 `HostGuardianService` 역할을 수행 하 고 `HgsClient` 모듈이 있으면 추적 대상이 `GuardedHost`역할을 수행 하 게 됩니다.  지정 된 호스트에 두 모듈이 모두 있을 수 있으며,이 경우에는 `HostGuardianService`와 `GuardedHost`모두 처리 됩니다.

따라서 로컬에서 추적을 수집 하기 위한 진단의 기본 호출은 다음과 같습니다.

```PowerShell
Get-HgsTrace
```

... 는 다음과 같습니다.

```PowerShell
New-HgsTraceTarget -Local | Get-HgsTrace
```

> [!TIP]
> 파이프라인을 통해 대상을 허용 하거나 `-Target` 매개 변수를 통해 직접 `Get-HgsTrace` 수 있습니다.  두 운영상 간에는 차이가 없습니다.

### <a name="remote-diagnosis-using-trace-targets"></a>추적 대상을 사용 하 여 원격 진단

원격 연결 정보를 사용 하 여 추적 대상을 생성 하면 원격으로 호스트를 진단할 수 있습니다.  Windows PowerShell 원격을 사용 하 여 연결할 수 있는 호스트 이름 및 자격 증명 집합만 있으면 됩니다.
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $server
```
이 예에서는 원격 사용자 자격 증명을 수집 하는 프롬프트를 생성 한 다음 `hgs-01.secure.contoso.com`에서 원격 호스트를 사용 하 여 추적 컬렉션을 완료 하는 데 진단을 실행 합니다.  결과 추적은 localhost로 다운로드 된 다음 진단 됩니다.  진단 결과는 [로컬 진단을](#local-diagnosis)수행할 때와 동일 하 게 표시 됩니다.  마찬가지로 원격 시스템에 설치 된 Windows PowerShell 모듈을 기반으로 유추 될 수 있으므로 역할을 지정할 필요가 없습니다.

원격 진단은 원격 호스트에 대 한 모든 액세스에 Windows PowerShell 원격 기능을 활용 합니다.  따라서 추적 대상이 Windows PowerShell 원격을 사용 하도록 설정 하 고 ( [Enable-psremoting 사용](https://technet.microsoft.com/library/hh849694.aspx)참조) 대상에 대 한 연결을 시작 하기 위해 localhost가 제대로 구성 되어 있어야 합니다.

> [!NOTE]
> 대부분의 경우 localhost는 동일한 Active Directory 포리스트에 속해 있어야 하 고 유효한 DNS 호스트 이름이 사용 되어야 합니다.  환경에서 보다 복잡 한 페더레이션 모델을 활용 하거나 연결에 직접 IP 주소를 사용 하려는 경우에는 WinRM 신뢰할 수 있는 [호스트](https://technet.microsoft.com/library/ff700227.aspx)를 설정 하는 등의 추가 구성을 수행 해야 할 수 있습니다.

`Test-HgsTraceTarget` cmdlet을 사용 하 여 추적 대상이 올바르게 인스턴스화되어 연결을 허용 하도록 구성 되었는지 확인할 수 있습니다.
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
$server | Test-HgsTraceTarget
```
이 명령은 `Get-HgsTrace`가 추적 대상으로 원격 진단 세션을 설정할 수 있는 경우에만 `$True`을 반환 합니다.  오류가 발생 하면이 cmdlet은 Windows PowerShell 원격 연결에 대 한 추가 문제 해결에 대 한 관련 상태 정보를 반환 합니다.

#### <a name="implicit-credentials"></a>암시적 자격 증명

추적 대상에 원격으로 연결할 수 있는 권한이 있는 사용자의 원격 진단을 수행할 때 `New-HgsTraceTarget`에 자격 증명을 제공할 필요가 없습니다.  `Get-HgsTrace` cmdlet은 연결을 열 때 cmdlet을 호출한 사용자의 자격 증명을 자동으로 다시 사용 합니다.

> [!WARNING]
> 자격 증명 다시 사용에는 몇 가지 제한 사항이 적용 됩니다. 특히 "두 번째 홉" 이라고 하는 경우를 들 수 있습니다.  이는 원격 세션 내에서 다른 컴퓨터로 자격 증명을 다시 사용 하려고 할 때 발생 합니다.  이 시나리오를 지원 하기 위해 [CredSSP를 설정](https://technet.microsoft.com/library/hh849872.aspx) 해야 하지만,이는 보호 된 패브릭 관리 및 문제 해결의 범위를 벗어납니다.

#### <a name="using-windows-powershell-just-enough-administration-jea-and-diagnostics"></a>Windows PowerShell에 충분 한 관리 (JEA) 및 진단 사용

원격 진단은 JEA 제한 Windows PowerShell 끝점의 사용을 지원 합니다. 기본적으로 원격 추적 대상은 기본 `microsoft.powershell` 끝점을 사용 하 여 연결 합니다.  추적 대상에 `HostGuardianService` 역할이 있는 경우에는 HGS가 설치 될 때 구성 된 `microsoft.windows.hgs` 끝점도 사용 하려고 시도 합니다.

사용자 지정 끝점을 사용 하려면 아래와 같이 `-PSSessionConfigurationName` 매개 변수를 사용 하 여 추적 대상을 구성 하는 동안 세션 구성 이름을 지정 해야 합니다.

```PowerShell
New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential) -PSSessionConfigurationName "microsoft.windows.hgs"
```

#### <a name="diagnosing-multiple-hosts"></a>여러 호스트 진단

한 번에 여러 추적 대상을 `Get-HgsTrace`에 전달할 수 있습니다.  여기에는 로컬 및 원격 대상이 혼합 되어 포함 됩니다.  각 대상은 차례로 추적 되 고 모든 대상의 추적이 동시에 진단 됩니다.  진단 도구는 배포에 대 한 향상 된 정보를 사용 하 여 검색 되지 않는 복잡 한 노드 간 구성을 식별할 수 있습니다.  이 기능을 사용 하려면 여러 호스트에서 동시에 추적을 제공 하거나 (수동 진단의 경우) `Get-HgsTrace`를 호출할 때 여러 호스트를 대상으로 지정 해야 합니다 (원격 진단의 경우).

다음은 두 개의 HGS 노드와 두 개의 보호 된 호스트로 구성 된 패브릭을 심사 하는 원격 진단을 사용 하 여 보호 된 호스트 중 하나를 사용 하 여 `Get-HgsTrace`를 시작 하는 예제입니다.

```PowerShell
$hgs01 = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Credential (Enter-Credential)
$hgs02 = New-HgsTraceTarget -HostName "hgs-02.secure.contoso.com" -Credential (Enter-Credential)
$gh01 = New-HgsTraceTarget -Local
$gh02 = New-HgsTraceTarget -HostName "guardedhost-02.contoso.com"
Get-HgsTrace -Target $hgs01,$hgs02,$gh01,$gh02 -RunDiagnostics
```

> [!NOTE]
> 여러 노드를 진단할 때 보호 된 전체 패브릭을 진단할 필요는 없습니다.  대부분의 경우에는 지정 된 오류 조건에 포함 될 수 있는 모든 노드를 포함 하는 것으로 충분 합니다.  일반적으로이는 보호 된 호스트의 하위 집합이 고 HGS 클러스터의 일부 노드 수입니다.

## <a name="manual-diagnosis-using-saved-traces"></a>저장 된 추적을 사용 하 여 수동 진단

경우에 따라 추적을 다시 수집 하지 않고 진단을 다시 실행 하거나 패브릭의 모든 호스트를 동시에 원격으로 진단 하는 데 필요한 자격 증명이 없을 수 있습니다.  수동 진단은 원격 추적 컬렉션을 사용 하지 않고 `Get-HgsTrace`를 사용 하 여 전체 패브릭 심사를 수행할 수 있는 메커니즘입니다.

수동 진단을 수행 하려면 먼저 패브릭에서 심사 될 각 호스트의 관리자가 준비 되어 사용자를 대신 하 여 명령을 실행할 수 있는지 확인 해야 합니다.  진단 추적 출력은 일반적으로 중요 한 정보를 노출 하지 않지만 사용자에 게이 정보를 다른 사용자에 게 노출 하는 것이 안전한 지 여부를 확인 하는 것을 책임 합니다.

> [!NOTE]
> 추적은 익명화 되지 않으며, 경우에 따라 개인 정보로 간주 되는 네트워크 구성, PKI 설정 및 기타 구성을 표시 합니다.  따라서 추적은 조직 내에서 신뢰할 수 있는 엔터티로만 전송 되 고 공개적으로 게시 되어서는 안 됩니다.

수동 진단을 수행 하는 단계는 다음과 같습니다.

1. 각 호스트 관리자가 결과 추적에 대해 실행 하려는 알려진 `-Path`와 진단 목록을 지정 하 `Get-HgsTrace`를 실행 하도록 요청 합니다.  예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```PowerShell
   Get-HgsTrace -Path C:\Traces -Diagnostic Networking,BestPractices
   ```

2. 각 호스트 관리자가 결과 추적 폴더를 패키지 하 고 사용자에 게 보내도록 요청 합니다.  이 프로세스는 전자 메일, 파일 공유 또는 조직에서 설정한 운영 정책 및 절차를 기반으로 하는 다른 메커니즘을 통해 제어할 수 있습니다.

3. 모든 수신 된 추적을 다른 내용 또는 폴더 없이 단일 폴더에 병합 합니다.

    * 예를 들어, 관리자가 HGS-01, HGS-02, RR1N2608-12, RR1N2608-13 이라는 4 개 컴퓨터에서 수집 된 추적을 보내는 경우를 가정 합니다.  각 관리자는 동일한 이름으로 폴더를 보냈습니다.  다음과 같이 표시 되는 디렉터리 구조를 조합 합니다.

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

4. 진단을 실행 하 여 `-Path` 매개 변수에 어셈블된 추적 폴더의 경로를 제공 하 고 `-RunDiagnostics` 스위치 및 관리자에 게 추적을 수집 하도록 요청한 진단을 지정 합니다.  진단은 경로 내에 있는 호스트에 액세스할 수 없어 미리 수집 된 추적만 사용 하려고 한다고 가정 합니다.  추적이 누락 되거나 손상 된 경우 진단에서 영향을 받는 테스트만 실패 하 고 정상적으로 진행 됩니다.  예를 들어 다음과 같은 가치를 제공해야 합니다.

   ```PowerShell
   Get-HgsTrace -RunDiagnostics -Diagnostic Networking,BestPractices -Path ".\FabricTraces"
   ```

### <a name="mixing-saved-traces-with-additional-targets"></a>저장 된 추적을 추가 대상과 혼합

경우에 따라 추가 호스트 추적으로 보강 하려는 미리 수집 된 추적 집합이 있을 수 있습니다.  진단의 단일 호출에서 추적 하 고 진단할 추가 대상과 미리 수집 된 추적을 혼합할 수 있습니다.

위에 지정 된 추적 폴더를 수집 및 어셈블하는 지침에 따라 미리 수집 된 추적 폴더에서 찾을 수 없는 추가 추적 대상을 사용 하 여 `Get-HgsTrace`를 호출 합니다.

```PowerShell
$hgs03 = New-HgsTraceTarget -HostName "hgs-03.secure.contoso.com" -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $hgs03 -Path .\FabricTraces
``` 

진단 cmdlet은 모든 미리 수집 된 호스트 및 추적 해야 하는 추가 호스트 하나를 식별 하 고 필요한 추적을 수행 합니다.  그러면 모든 미리 수집 된 추적 및 새로 수집 된 추적의 합계가 진단 됩니다.  결과 추적 폴더에는 이전 추적과 새 추적이 모두 포함 됩니다.

## <a name="known-issues"></a>알려진 문제

보호 된 패브릭 진단 모듈에는 Windows Server 2019 또는 Windows 10 버전 1809 이상 버전에서 실행할 때 알려진 제한 사항이 있습니다.
다음 기능을 사용 하면 잘못 된 결과가 발생할 수 있습니다.

* 호스트 키 증명
* 증명 전용 HGS 구성 (SQL Server Always Encrypted 시나리오)
* 증명 정책 기본값이 v2 인 HGS 서버에서 v1 정책 아티팩트 사용

이러한 기능을 사용 하는 경우 `Get-HgsTrace`에 오류가 발생 하는 경우에는 HGS 서버 또는 보호 된 호스트가 잘못 구성 되었음을 나타내는 것은 아닙니다.
보호 된 호스트에서 `Get-HgsClientConfiguration` 같은 다른 진단 도구를 사용 하 여 호스트가 증명을 통과 했는지 테스트 합니다.
