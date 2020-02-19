---
title: 스토리지 공간 다이렉트를 사용 하 여 진단 데이터 수집
description: 데이터 수집 도구를 사용 하 여 이러한 도구를 실행 하 고 사용 하는 방법에 대 한 구체적인 예제를 이해 스토리지 공간 다이렉트.
keywords: 저장소 공간, 데이터 수집, 문제 해결, 이벤트 채널, SDDCDiagnosticInfo
ms.assetid: ''
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 10/24/2018
ms.localizationpriority: ''
ms.openlocfilehash: 0d64e6188b24b5a1ec45242c3d99366fdde5a623
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465217"
---
# <a name="collect-diagnostic-data-with-storage-spaces-direct"></a>스토리지 공간 다이렉트를 사용 하 여 진단 데이터 수집

> 적용 대상: Windows Server 2019, Windows Server 2016

스토리지 공간 다이렉트 및 장애 조치 (Failover) 클러스터 문제를 해결 하는 데 필요한 데이터를 수집 하는 데 사용할 수 있는 다양 한 진단 도구가 있습니다. 이 문서에서는 클러스터를 진단 하는 데 도움이 되는 모든 관련 정보를 수집 하는 **SDDCDiagnosticInfo** -a touch tool에 초점을 둡니다.

**SDDCDiagnosticInfo** 에 대 한 로그 및 기타 정보가 조밀한 경우 아래에 표시 된 문제 해결에 대 한 정보는 에스컬레이션 된 고급 문제를 해결 하는 데 유용 하며, 심사를 위해 데이터를 Microsoft로 전송 해야 할 수 있습니다.

## <a name="installing-get-sddcdiagnosticinfo"></a>SDDCDiagnosticInfo 설치

**SDDCDiagnosticInfo** PowerShell cmdlet ( **PCStorageDiagnosticInfo**(이전에는 **테스트-storagehealth**)를 사용 하 여에 대 한 로그를 수집 하 고 장애 조치 (Failover) 클러스터링 (클러스터, 리소스, 네트워크, 노드), 저장소 공간 (실제 디스크, 엔클로저, 가상 디스크), 클러스터 공유 볼륨, SMB 파일 공유 및 중복 제거에 대 한 상태 검사를 수행할 수 있습니다. 

스크립트를 설치 하는 방법에는 다음 두 가지가 있습니다.

### <a name="powershell-gallery"></a>PowerShell 갤러리

[PowerShell 갤러리](https://www.powershellgallery.com/packages/PrivateCloud.DiagnosticInfo) 은 GitHub 리포지토리의 스냅숏입니다. PowerShell 갤러리에서 항목을 설치 하려면 Windows 10, WMF (Windows Management Framework) 5.0 또는 MSI 기반 설치 관리자 (PowerShell 3 및 4 용)에서 사용할 수 있는 PowerShellGet 모듈의 최신 버전이 필요 합니다.

SDDCDiagnosticInfo이이를 사용 하므로이 프로세스 중에 최신 버전의 [Microsoft 네트워킹 진단 도구](https://www.powershellgallery.com/packages/MSFT.Network.Diag) 를 설치 합니다. 이 매니페스트 모듈은 Microsoft Core 네트워킹 제품 그룹에서 유지 관리 되는 네트워크 진단 및 문제 해결 도구를 포함 합니다.

관리자 권한으로 PowerShell에서 다음 명령을 실행 하 여 모듈을 설치할 수 있습니다.

``` PowerShell
Install-PackageProvider NuGet -Force
Install-Module PrivateCloud.DiagnosticInfo -Force
Import-Module PrivateCloud.DiagnosticInfo -Force
Install-Module -Name MSFT.Network.Diag
```

모듈을 업데이트 하려면 PowerShell에서 다음 명령을 실행 합니다.

``` PowerShell
Update-Module PrivateCloud.DiagnosticInfo
```

### <a name="github"></a>GitHub

[GitHub 리포지토리](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/) 는이 모듈의 최신 버전으로, 계속 해 서 반복 하 고 있습니다. GitHub에서 모듈을 설치 하려면 [보관 파일](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/archive/master.zip) 에서 최신 모듈을 다운로드 하 고 PrivateCloud DiagnosticInfo 디렉터리를 ```$env:PSModulePath```가 가리키는 올바른 PowerShell 모듈 경로로 추출 합니다.

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

이 모듈을 오프 라인 클러스터에서 가져와야 하는 경우 zip을 다운로드 하 여 대상 서버 노드로 이동 하 고 모듈을 설치 합니다.

## <a name="gathering-logs"></a>로그 수집 중

이벤트 채널을 사용 하도록 설정 하 고 설치 프로세스를 완료 한 후 모듈에서 SDDCDiagnosticInfo PowerShell cmdlet을 사용 하 여 가져올 수 있습니다.

- 저장소 상태 및 비정상 구성 요소에 대 한 세부 정보를 보고 합니다.
- 풀, 볼륨 및 중복 제거 된 볼륨 별로 저장소 용량 보고서
- 모든 클러스터 노드의 이벤트 로그 및 요약 오류 보고서

저장소 클러스터의 이름이 *"CLUS01"* 인 것으로 가정 합니다.

원격 저장소 클러스터에 대해 실행 하려면:

``` PowerShell
Get-SDDCDiagnosticInfo -ClusterName CLUS01
```

클러스터 된 저장소 노드에서 로컬로 실행 하려면 다음을 수행 합니다.

``` PowerShell
Get-SDDCDiagnosticInfo
```

지정 된 폴더에 결과를 저장 하려면 다음을 수행 합니다.

``` PowerShell
Get-SDDCDiagnosticInfo -WriteToPath D:\Folder 
```

실제 클러스터에서 표시 되는 방법의 예는 다음과 같습니다.

``` PowerShell
New-Item -Name SDDCDiagTemp -Path d:\ -ItemType Directory -Force
Get-SddcDiagnosticInfo -ClusterName S2D-Cluster -WriteToPath d:\SDDCDiagTemp
```

여기에서 볼 수 있듯이 스크립트는 현재 클러스터 상태에 대 한 유효성 검사도 수행 합니다.

![데이터 수집 powershell 스크린샷](media/data-collection/CollectData.png)

여기에서 볼 수 있듯이 모든 데이터는 SDDCDiagTemp 폴더에 기록 됩니다.

![파일 탐색기의 데이터 스크린샷](media/data-collection/CollectDataFolder.png)

스크립트가 완료 되 면 사용자 디렉터리에 ZIP이 생성 됩니다.

![powershell의 데이터 zip 스크린샷](media/data-collection/CollectDataResult.png)

텍스트 파일에 보고서를 생성 하겠습니다.

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

참조를 위해 [샘플 보고서](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/SDDCReport.txt) 와 [샘플 zip](https://github.com/Microsoft/WSLab/blob/dev/Scenarios/S2D%20Tools/Get-SDDCDiagnosticInfo/HealthTest-S2D-Cluster-20180522-1546.ZIP)에 대 한 링크는 다음과 같습니다.

Windows 관리 센터 (버전 1812 이상)에서이를 보려면 *진단* 탭으로 이동 합니다. 아래 스크린샷에 표시 된 것 처럼 다음을 수행할 수 있습니다. 

- 진단 도구 설치
- 업데이트 (만료 된 경우), 
- 매일 진단 실행 예약 (시스템에 미치는 영향이 적고, 일반적으로 백그라운드에서 5 분 정도 < 걸리며, 클러스터에 500mb를 초과 하지 않음)
- 직접 지원 하거나 분석 하기 위해 제공 해야 하는 경우 이전에 수집한 진단 정보를 확인 합니다.

![wac 진단 스크린샷](media/data-collection/Wac.png)

## <a name="get-sddcdiagnosticinfo-output"></a>SDDCDiagnosticInfo 출력

다음은 SDDCDiagnosticInfo의 압축 된 출력에 포함 된 파일입니다.

### <a name="health-summary-report"></a>상태 요약 보고서

상태 요약 보고서는 다음과 같이 저장 됩니다.
- 0_CloudHealthSummary .log

이 파일은 수집 된 모든 데이터를 구문 분석 한 후에 생성 되며 시스템에 대 한 간략 한 요약을 제공 하기 위한 것입니다. 다음을 포함 합니다.

- 시스템 정보
- 저장소 상태 개요 (노드 수, 온라인 리소스, 클러스터 공유 볼륨 온라인, 비정상 구성 요소 등)
- 비정상 구성 요소 (오프 라인, 실패 또는 온라인 보류 중인 클러스터 리소스)에 대 한 세부 정보
- 펌웨어 및 드라이버 정보
- 풀, 실제 디스크 및 볼륨 세부 정보
- 저장소 성능 (성능 카운터 수집)

이 보고서는 더 유용한 정보를 포함 하도록 지속적으로 업데이트 되 고 있습니다. 최신 정보는 [GITHUB 추가](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/edit/master/README.md)정보를 참조 하세요.

### <a name="logs-and-xml-files"></a>로그 및 XML 파일

이 스크립트는 다양 한 로그 수집 스크립트를 실행 하 고 출력을 xml 파일로 저장 합니다. 클러스터 및 상태 로그, MSInfo32 (시스템 정보), 필터링 되지 않은 이벤트 로그 (장애 조치 (failover) 클러스터링, 되지 않는 진단, hyper-v, 저장소 공간 등) 및 저장소 진단 정보 (작업 로그)를 수집 합니다. 수집 되는 정보에 대 한 최신 정보는 [GITHUB 추가 정보 (수집 정보)](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/blob/master/README.md#what-does-the-cmdlet-output-include)를 참조 하세요.

## <a name="how-to-consume-the-xml-files-from-get-pcstoragediagnosticinfo"></a>PCStorageDiagnosticInfo에서 XML 파일을 사용 하는 방법
**PCStorageDiagnosticInfo** cmdlet에 의해 수집 된 데이터에 제공 된 XML 파일의 데이터를 사용할 수 있습니다. 이러한 파일에는 가상 디스크, 실제 디스크, 기본 클러스터 정보 및 기타 PowerShell 관련 출력에 대 한 정보가 포함 됩니다. 

이러한 출력의 결과를 보려면 PowerShell 창을 열고 다음 단계를 실행 합니다. 

```PowerShell
ipmo storage
$d = import-clixml <filename> 
$d
```

## <a name="what-to-expect-next"></a>다음에는 어떻게 해야 하나요?
SDDC 시스템 상태를 분석 하기 위한 많은 향상 된 기능 및 새로운 cmdlet.
[여기](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/issues)에서 문제를 제출 하 여 확인 하고자 하는 내용에 대 한 피드백을 제공 합니다. 또한 [끌어오기 요청](https://github.com/PowerShell/PrivateCloud.DiagnosticInfo/pulls)을 제출 하 여 스크립트에 유용한 변경 사항을 자유롭게 적용할 수 있습니다.
