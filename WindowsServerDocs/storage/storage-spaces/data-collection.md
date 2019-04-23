---
title: 저장소 공간 다이렉트를 사용 하 여 진단 데이터 수집
description: 저장소 공간 다이렉트 데이터 수집 도구를 실행 하 고 사용 하는 방법의 특정 예제를 사용 하 여 이해 합니다.
keywords: 이벤트 채널, Get SDDCDiagnosticInfo, 문제 해결, 데이터 수집, 저장소 공간
ms.assetid: ''
ms.prod: windows-server-threshold
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 10/24/2018
ms.localizationpriority: ''
ms.openlocfilehash: eaa7d92fe6f77697614cacf1405a25e5a42e14b7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880274"
---
# <a name="collect-diagnostic-data-with-storage-spaces-direct"></a>저장소 공간 다이렉트를 사용 하 여 진단 데이터 수집

> 적용 대상: Windows Server 2019, Windows Server 2016

저장소 공간 다이렉트 및 장애 조치 클러스터 문제를 해결 하는 데 필요한 데이터를 수집 하는 데 사용할 수 있는 다양 한 진단 도구가 있습니다. 이 문서에서는 중점적 **Get SDDCDiagnosticInfo** -클러스터를 진단 하는 데 관련 된 모든 정보를 수집 하는 하나의 터치 도구입니다.

<!-- The health summary report is a great start to understanding the status of your system to start diagnosing an issue. -->

로그 및 기타 정보를 지정 하는 **Get SDDCDiagnosticInfo** 는 조밀한 아래 문제 해결 정보를 문제는 에스컬레이션 된 고 수 하는 고급 문제 해결 하는 데 도움이 됩니다. 분류에 대 한 Microsoft에 보낼 데이터가 필요 합니다.

<!--
## Collecting live dumps

Windows will trigger the collection of a ``` LiveDump ``` when there are known resources that are hanging in kernel calls. ``` RHS ``` will trigger ```LiveDump``` collection if both the resource type and cluster ``` DumpPolicy ``` are set to 1. For physical disk it is set out of the box
-->

## <a name="installing-get-sddcdiagnosticinfo"></a>Get-SDDCDiagnosticInfo 설치

합니다 **Get SDDCDiagnosticInfo** PowerShell cmdlet (즉, **Get-PCStorageDiagnosticInfo**, 이전의 **테스트 StorageHealth**)에 대 한 로그를 수집 하 고 수행할 수 저장소 공간 (장애 조치 클러스터링 (클러스터, 리소스, 네트워크, 노드)에 대 한 상태 검사 실제 디스크, 엔클로저, 가상 디스크)를 클러스터 공유 볼륨, SMB 파일 공유 및 중복 제거 합니다. 

아래 윤곽선은 모두 스크립트를 설치 하는 두 가지 방법 있습니다.

### <a name="powershell-gallery"></a>PowerShell 갤러리

합니다 [PowerShell 갤러리](https://www.powershellgallery.com/packages/PrivateCloud.DiagnosticInfo) GitHub 리포지토리의 스냅숏입니다. Note는 최신 버전의 Windows 10에서,에 Windows WMF (Management Framework) 5.0 또는 MSI 기반 설치 관리자 (PowerShell 3 및 4)에서 사용할 수 있는 PowerShellGet 모듈이 필요 PowerShell 갤러리에서 항목을 설치 합니다.

명령을 실행 하 여 다음 PowerShell에서 관리자 권한으로 모듈을 설치할 수 있습니다.

``` PowerShell
Install-PackageProvider NuGet -Force
Install-Module PrivateCloud.DiagnosticInfo -Force
Import-Module PrivateCloud.DiagnosticInfo -Force
```

모듈을 업데이트 하려면 PowerShell에서 다음 명령을 실행 합니다.

``` PowerShell
Update-Module PrivateCloud.DiagnosticInfo
```

### <a name="github"></a>GitHub

합니다 [GitHub 리포지토리](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/) 모듈의 최신 버전 이므로 여기 반복 지속적으로 했습니다. GitHub에서 모듈을 설치 하려면에서 최신 모듈을 다운로드 합니다 [보관](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/archive/master.zip) PrivateCloud.DiagnosticInfo 디렉터리를 가리키는 올바른 PowerShell 모듈 경로 추출 하 고 ```$env:PSModulePath```

``` PowerShell
# Allowing Tls12 and Tls11 -- e.g. github now requires Tls12
# If this is not set, the Invoke-WebRequest fails with "The request was aborted: Could not create SSL/TLS secure channel."
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
$module = 'PrivateCloud.DiagnosticInfo'
Invoke-WebRequest -Uri https://github.com/PowerShell/$module/archive/master.zip -OutFile $env:TEMP\master.zip
Expand-Archive -Path $env:TEMP\master.zip -DestinationPath $env:TEMP -Force
if (Test-Path $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module) {
    rm -Recurse $env:SystemRoot\System32\WindowsPowerShell\v1.0\Modules\$module -ErrorAction Stop
    Remove-Module $module -ErrorAction SilentlyContinue
} else {
    Import-Module $module -ErrorAction SilentlyContinue
} 
if (-not ($m = Get-Module $module -ErrorAction SilentlyContinue)) {
    $md = "$env:ProgramFiles\WindowsPowerShell\Modules"
} else {
    $md = (gi $m.ModuleBase -ErrorAction SilentlyContinue).PsParentPath
    Remove-Module $module -ErrorAction SilentlyContinue
    rm -Recurse $m.ModuleBase -ErrorAction Stop
}
cp -Recurse $env:TEMP\$module-master\$module $md -Force -ErrorAction Stop
rm -Recurse $env:TEMP\$module-master,$env:TEMP\master.zip
Import-Module $module -Force

``` 

오프 라인 클러스터에서이 모듈을 가져올 경우 다운로드 zip에 대상 서버 노드를 이동 하 고 모듈을 설치 합니다.

## <a name="gathering-logs"></a>로그 수집

이벤트 채널을 사용 하도록 설정 하 고 설치 프로세스를 완료 한 후 가져오려는 모듈에서 Get-SDDCDiagnosticInfo PowerShell cmdlet을 사용할 수 있습니다.

- 저장소 상태 및 비정상 구성 요소에 대 한 세부 정보 보고서
- 저장소 풀, 볼륨 및 중복 제거 된 볼륨 용량에 대 한 보고서
- 모든 클러스터 노드 및 오류 요약 보고서에서 이벤트 로그

저장소 클러스터 이름에 있다고 가정 *"CLUS01"입니다.*

원격 저장소 클러스터에 대해 실행 합니다.

``` PowerShell
Get-SDDCDiagnosticInfo -ClusterName CLUS01
```

클러스터 된 저장소 노드에서 로컬로 실행 합니다.

``` PowerShell
Get-SDDCDiagnosticInfo
```

에 지정된 된 폴더에 결과 저장 합니다.

``` PowerShell
Get-SDDCDiagnosticInfo -WriteToPath D:\Folder 
```

실제 클러스터에서이 모양을의 예는 다음과 같습니다.

``` PowerShell
New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
Get-SddcDiagnosticInfo -ClusterName S2D-Cluster -WriteToPath d:\SDDCDiagTemp
```

알 수 있듯이 스크립트 작업이 수행 됩니다. 현재 클러스터 상태의 유효성 검사

![데이터 컬렉션 powershell 스크린샷](media/data-collection/CollectData.png)

모든 데이터를 볼 수 있듯이 SDDCDiagTemp 폴더에 기록 됩니다.

![데이터 파일 탐색기 스크린샷](media/data-collection/CollectDataFolder.png)

스크립트는 끝나면 ZIP users 디렉터리에 만들어집니다.

![데이터 zip의 powershell 스크린샷](media/data-collection/CollectDataResult.png)

텍스트 파일에 보고서를 생성 해 보겠습니다

```PowerShell
#find the latest diagnostic zip in UserProfile
    $DiagZip=(get-childitem $env:USERPROFILE | where Name -like HealthTest*.zip)
    $LatestDiagPath=($DiagZip | sort lastwritetime | select -First 1).FullName
#expand to temp directory
    New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
    Expand-Archive -Path $LatestDiagPath -DestinationPath D:\SDDCDiagTemp -Force
#generate report and save to text file
    $report=Show-SddcDiagnosticReport -Path D:\SDDCDiagTemp
    $report | out-file d:\SDDCReport.txt
    
```

참조를 위해 여기에 대 한 링크는 합니다 [예제 보고서](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/SDDCReport.txt) 하 고 [zip 샘플](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/HealthTest-S2D-Cluster-20180522-1546.ZIP)합니다.

Windows Admin Center (버전 1812에부터 해당)에서이 보기에 *진단* 탭 합니다. 아래 스크린샷에 표시 된 대로 다음을 할 수 있습니다. 

- 진단 도구를 설치 합니다.
- 업데이트 하는 (오래 된 경우) 
- 일일 진단 실행을 예약 (시스템에 미치는 영향, 일반적으로 낮은 있습니다 < 백그라운드에서 5 분 500mb를 초과 하 여 클러스터에서 사용 되지 않습니다)
- 보기를 지원 하거나 직접 분석할 수 있도록 해야 하는 경우 이전에 진단 정보를 수집 합니다.

![wac 진단 스크린샷](media/data-collection/Wac.png)

## <a name="get-sddcdiagnosticinfo-output"></a>Get-SDDCDiagnosticInfo 출력

Get-SDDCDiagnosticInfo의 압축 된 출력에 포함 된 파일은 다음과 같습니다.

### <a name="health-summary-report"></a>상태 요약 보고서

상태 요약 보고서로 저장 됩니다.
- 0_CloudHealthSummary.log

수집 하 고 시스템의 요약을 제공 하려는 모든 데이터를 구문 분석 후에이 파일이 생성 됩니다. 포함 되어 있습니다.

- 시스템 정보
- 저장소 상태 개요 (노드, 리소스 online 클러스터 공유 볼륨을 온라인, 비정상 구성 요소 등의 수입니다.)
- 비정상 (오프 라인, 실패 또는 보류 중인 온라인에 있는 클러스터 리소스) 구성 요소에 대 한 세부 정보
- 펌웨어 및 드라이버 정보
- 풀, 실제 디스크 및 볼륨 세부 정보
- 저장소 성능 (성능 카운터는 수집)

이 보고서는 지속적으로 유용한 정보를 포함 하도록 업데이트 중입니다. 최신 정보를 참조 하세요. 합니다 [GitHub 추가 정보](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/edit/master/README.md)합니다.

### <a name="logs-and-xml-files"></a>로그 및 XML 파일

스크립트 실행 스크립트를 수집 하는 다양 한 로그 및 출력을 xml 파일로 저장 합니다. 클러스터 및 상태 로그, 시스템 정보 (MSInfo32), 장애 조치 클러스터링, 디스크 진단, 하이퍼-v, 저장소 공간 등, 필터링 되지 않은 이벤트 로그 및 저장소 진단 정보 수집 (작업 로그). 수집 되는 정보에서 최신 정보를 참조 하세요. 합니다 [GitHub 추가 정보 (새로운 수집한)](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/blob/master/README.md#what-does-the-cmdlet-output-include)합니다.

<!--
## Enabling event channels

When Windows Server is installed, many event channels are enabled by default. But sometimes when diagnosing an issue, we want to be able to enable some of these event channels since it will help in triaging and diagnosing system issues.

You could enable additional event channels on each server node in your cluster as needed; however, this approach presents two problems:

1. You need to remember to enable the same event channels on every new server node that you add to your cluster.
2. When diagnosing, it can be tedious to enable specific event channels, reproduce the error, and repeat this process until you root cause.

To avoid these issues, you can enable event channels on cluster startup. The list of enabled event channels on your cluster can be configured using the public property **EnabledEventLogs**. By default, the following event channels are enabled:

```powershell
PS C:\Windows\system32> (get-cluster).EnabledEventLogs
```

Here's an example of the output:
```
Microsoft-Windows-Hyper-V-VmSwitch-Diagnostic,4,0xFFFFFFFD
Microsoft-Windows-SMBDirect/Debug,4
Microsoft-Windows-SMBServer/Analytic
Microsoft-Windows-Kernel-LiveDump/Analytic
```

The **EnabledEventLogs** property is a multistring, where each string is in the form: **channel-name, log-level, keyword-mask**. The **keyword-mask** can be a hexadecimal (prefix 0x), octal (prefix 0), or decimal number (no prefix) number that each event contains (so you can filter by it). For instance, to add a new event channel to the list and to configure both **log-level** and **keyword-mask** you can run:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2,321"
```

If you want to set the **log-level** but keep the **keyword-mask** at its default value, you can use either of the following commands:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,2,"
```

If you want to keep the **log-level** at its default value, but set the **keyword-mask** you can run the following command:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,,0xf1"
```

If you want to keep both the **log-level** and the **keyword-mask** at their default values, you can run any of the following commands:

```powershell
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,"
(get-cluster).EnabledEventLogs += "Microsoft-Windows-WinINet/Analytic,,"
```

These event channels will be enabled on every cluster node when the cluster service starts or whenever the **EnabledEventLogs** property is changed.
-->

## <a name="how-to-consume-the-xml-files-from-get-pcstoragediagnosticinfo"></a>Get-PCStorageDiagnosticInfo에서 XML 파일을 사용 하는 방법
에 의해 수집 된 데이터에서 제공 하는 XML 파일에서 데이터를 사용할 수 있습니다 합니다 **Get PCStorageDiagnosticInfo** cmdlet. 이러한 파일에 대 한 정보는 가상 디스크, 실제 디스크, 기본 클러스터 정보 및 다른 PowerShell 관련 출력 합니다. 

이러한 출력의 결과 보려면 PowerShell 창을 열고 다음 단계를 실행 합니다. 

```PowerShell
ipmo storage
$d = import-clixml <filename> 
$d
```

## <a name="what-to-expect-next"></a>예상 되는 다음?
많은 향상 된 기능 및 SDDC 시스템 상태를 분석 하는 새 cmdlet.
문제를 제출 하 여 보려는 원하는 항목에 대 한 의견 [여기](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/issues)합니다. 또한 자유롭게 기여 스크립트에 유용한 변경 내용을 제출 하 여는 [끌어오기 요청](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/pulls)합니다.
