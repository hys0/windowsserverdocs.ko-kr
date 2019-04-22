---
ms.assetid: 07d6b251-c492-4d9f-bcc4-031023695b24
title: 데이터 중복 제거 설치 및 사용
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 05/09/2017
description: Windows Server에 데이터 중복 제거를 설치하는 방법, 워크로드가 중복 제거 대상인지 확인하는 방법, 볼륨에서 중복 제거를 사용하도록 설정하는 방법을 설명합니다.
ms.openlocfilehash: 153b064b158028c696bad4eeb00764d3e10822e1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814904"
---
# <a name="install-and-enable-data-deduplication"></a>데이터 중복 제거 설치 및 사용
> 적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 [데이터 중복 제거](overview.md)를 설치하고, 중복 제거에 대한 워크로드를 평가하고, 특정 볼륨에서 데이터 중복 제거를 사용하도록 설정하는 방법을 설명합니다.

> [!Note]  
> 장애 조치(Failover) 클러스터에서 데이터 중복 제거를 실행할 계획이라면 해당 클러스터의 모든 노드에 데이터 중복 제거 서버 역할이 설치되어 있어야 합니다.

## <a id="install-dedup"></a>데이터 중복 제거 설치
> [!Important]  
> [KB4025334](https://support.microsoft.com/kb/4025334)에는 중요한 안정성 문제 해결을 포함하여 데이터 중복 제거에 대한 수정 사항 롤업이 포함되어 있으므로 Windows Server 2016에서 데이터 중복 제거를 사용할 때 이 업데이트를 설치하는 것이 좋습니다.

### <a id="install-dedup-via-server-manager"></a>서버 관리자를 사용 하 여 데이터 중복 제거 설치
1. 역할 및 기능 추가 마법사에서 **서버 역할**을 선택하고 **데이터 중복 제거**를 선택합니다.  
![서버 관리자를 통해 데이터 중복 제거 설치: 서버 역할에서 데이터 중복 제거를 선택 합니다.](media/install-dedup-via-server-manager-1.png)
2. **설치** 단추가 활성화될 때까지 **다음**을 클릭한 후 **설치**를 클릭합니다.  
![서버 관리자를 통해 데이터 중복 제거 설치: 설치 클릭](media/install-dedup-via-server-manager-2.png)

### <a id="install-dedup-via-powershell"></a>PowerShell을 사용 하 여 데이터 중복 제거 설치
데이터 중복 제거를 설치하려면 관리자 권한으로 다음 PowerShell 명령을 실행합니다.  
`Install-WindowsFeature -Name FS-Data-Deduplication`

Nano Server 설치에 데이터 중복 제거를 설치하려면

1. [Nano Server 시작](../../get-started/getting-started-with-nano-server.md)에 설명된 대로 설치된 저장소를 사용하여 Nano Server 설치를 만듭니다.
2. Nano Server가 아닌 다른 모드에서 Windows Server 2016을 실행하는 서버 또는 RSAT([원격 서버 관리 도구](https://www.microsoft.com/download/details.aspx?id=45520))가 설치된 Windows PC에서 Nano Server 인스턴스를 명확히 참조('MyNanoServer'를 Nano Server 인스턴스의 실제 이름으로 바꿈)하여 데이터 중복 제거를 설치합니다.  
    ```PowerShell
    Install-WindowsFeature -ComputerName <MyNanoServer> -Name FS-Data-Deduplication
    ```  
    <br />
    **-- OR --**
    <br />
    PowerShell 원격 작업을 사용하여 Nano Server 인스턴스에 원격으로 연결한 후 DISM을 사용하여 데이터 중복 제거를 설치합니다.  
    
    ```PowerShell
    Enter-PSSession -ComputerName MyNanoServer 
    dism /online /enable-feature /featurename:dedup-core /all
    ```

## <a id="enable-dedup"></a>데이터 중복 제거를 사용 하도록 설정
### <a id="enable-dedup-candidate-workloads"></a>데이터 중복 제거할 워크 로드를 결정
데이터 중복 제거는 중복된 데이터에서 사용되는 디스크 공간을 줄여 서버 응용 프로그램의 데이터 소비 비용을 효과적으로 최소화할 수 있습니다. 중복 제거를 사용하도록 설정하기 전에 저장소에서 최대 성능을 확보할 수 있도록 워크로드의 특성을 이해해야 합니다. 고려할 두 가지 등급의 워크로드가 있습니다.

* 중복 제거 효과가 매우 높은 데이터 집합과 데이터 중복 제거의 사후 처리 모델과 일치하는 리소스 소비 패턴이 둘 다 있는 것으로 검증된 *권장 워크로드*. 이러한 워크로드에서는 항상 [데이터 중복 제거를 사용](install-enable.md#enable-dedup-lights-on)하는 것이 좋습니다.
    * 팀 공유, 사용자 홈 폴더, 작업 폴더 및 소프트웨어 개발 공유 등과 같이 공유 역할을 하는 GPFS(일반용 파일 서버)
    * VDI(가상 데스크톱 인프라) 서버
    * [Microsoft DPM(Data Protection Manager)](https://technet.microsoft.com/library/hh758173.aspx)과 같은 가상화된 백업 응용 프로그램
* 중복 제거의 효과가 있을 수 있지만 중복 제거에 적합한 대상이 아닐 때도 있는 워크로드. 예를 들어, 다음 워크로드는 중복 제거에 효과적일 수 있지만 먼저 중복 제거의 이점을 평가해야 합니다.
    * 일반용 Hyper-V 호스트
    * SQL Server
    * LOB(기간 업무) 서버

### <a id="enable-dedup-evaluating-sometimes-workloads"></a>데이터 중복 제거에 대 한 워크 로드 평가
> [!Important]  
> 권장 워크로드를 실행 중인 경우 이 섹션을 건너뛰고 [데이터 중복 제거 사용](install-enable.md#enable-dedup-lights-on)으로 이동할 수 있습니다.

워크로드가 중복 제거에 효과적인지 확인하려면 다음 질문에 대답합니다. 워크로드에 대해 잘 모를 경우 워크로드에서 작동 방식을 확인할 수 있도록 테스트 데이터 집합에서 파일럿 데이터 중복 제거 배포를 수행하는 것이 좋습니다.

1. **데이터 집합 내 워크 로드의 중복 제거의 이점을 활용할 수 있을 정도로 충분히 중복 있습니까?**  
    워크로드 데이터 중복 제거를 사용하기 전에 데이터 중복 제거 절감 평가 도구 또는 DDPEval을 사용하여 워크로드의 데이터 집합이 어느 정도 중복되어 있는지 조사합니다. 데이터 중복 제거를 설치한 후 `C:\Windows\System32\DDPEval.exe`에서 이 도구를 찾을 수 있습니다. DDPEval은 직접 연결 볼륨(로컬 드라이브 또는 클러스터 공유 볼륨 포함) 및 매핑되거나 매핑되지 않은 네트워크 공유에 대해 최적화 가능성을 평가할 수 있습니다.  
    &nbsp;   
    DDPEval.exe를 실행하면 다음과 유사한 출력이 반환됩니다.  
    &nbsp;  
    `Data Deduplication Savings Evaluation Tool`  
    `Copyright 2011-2012 Microsoft Corporation.  All Rights Reserved.`    
    &nbsp;   
    `Evaluated folder: E:\Test`     
    `Processed files: 34`  
    `Processed files size: 12.03MB`  
    `Optimized files size: 4.02MB`  
    `Space savings: 8.01MB`  
    `Space savings percent: 66`  
    `Optimized files size (no compression): 11.47MB`  
    `Space savings (no compression): 571.53KB`  
    `Space savings percent (no compression): 4`  
    `Files with duplication: 2`  
    `Files excluded by policy: 20`  
    `Files excluded by error: 0`  

2. **해당 데이터 집합 표시에 내 워크 로드의 I/O 패턴은 어떤? 어떤 성능 내 워크 로드에 대 한 합니까?**  
     데이터 중복 제거는 파일을 디스크에 쓸 때가 아니라 정기적으로 파일을 최적화합니다. 따라서 중복 제거된 볼륨에 대해 예상되는 워크로드의 읽기 패턴을 조사해야 합니다. 데이터 중복 제거는 파일 내용을 청크 저장소로 이동하고 가능한 한 많은 파일로 청크 저장소를 구성하려고 하기 때문에 파일의 순차적 범위에 적용했을 때 읽기 작업이 가장 효율적으로 수행됩니다.  

    일반적으로 데이터베이스 형태의 워크로드는 순차적 읽기 패턴보다 임의 읽기 패턴에 더 가깝습니다. 데이터베이스는 데이터베이스 레이아웃이 실행될 수 있는 가능한 모든 쿼리에 최적 상태임을 보장하지 않기 때문입니다. 청크 저장소의 섹션은 볼륨의 도처에 존재할 수 있으므로 데이터베이스 쿼리를 위해 청크 저장소의 데이터 범위에 액세스하면 추가 대기 시간이 발생할 수 있습니다. 고성능 워크로드는 이 추가 대기 시간에 특히 민감하지만 다른 데이터베이스 형태의 워크로드는 그렇지 않습니다.

    > [!Note]  
    > 이러한 문제는 주로 기존 회전 저장소 미디어(하드 디스크 드라이브 또는 HDD라고도 함)로 구성된 볼륨의 저장소 워크로드에 적용됩니다. 모든 플래시 저장소 인프라(반도체 드라이브 또는 SSD라고도 함)는 임의 I/O 패턴의 영향을 덜 받습니다. 플래시 미디어의 특성상 미디어의 모든 위치에 대해 액세스 시간이 동일하기 때문입니다. 따라서 중복 제거에서는 기존 회전 저장소 미디어와 달리 모든 플래시 미디어에 저장된 워크로드의 데이터 집합을 읽을 때 대기 시간이 동일하지 않습니다.

3. **서버에서 내 워크 로드의 리소스 요구 사항은 무엇입니까?**  
    데이터 중복 제거는 사후 처리 모델을 사용하므로 해당 [최적화 및 다른 작업](understand.md#job-info)을 완료하려면 주기적으로 충분한 시스템 리소스가 필요합니다. 따라서 야간이나 주말과 같이 유휴 시간이 있는 워크로드는 중복 제거에 매우 효과적이지만, 연중무휴 24시간 실행되는 워크로드는 그렇지 않습니다. 유휴 시간이 없는 워크로드도 서버의 리소스 요구 사항이 크지 않은 경우에는 중복 제거에 효과적일 수 있습니다.

### <a id="enable-dedup-lights-on"></a>데이터 중복 제거를 사용 하도록 설정
데이터 중복 제거를 사용하기 전에 워크로드와 가장 유사한 [사용 유형](understand.md#usage-type)을 선택해야 합니다. 데이터 중복 제거에 포함되는 세 가지 사용 유형이 있습니다.

* [기본](understand.md#usage-type-default) - 일반용 파일 서버에 맞게 특별히 조정됩니다.
* [Hyper-V](understand.md#usage-type-hyperv) - VDI 서버에 맞게 특별히 조정됩니다.
* [백업](understand.md#usage-type-backup) - [Microsoft DPM](https://technet.microsoft.com/library/hh758173.aspx)과 같은 가상화된 백업 응용 프로그램에 맞게 특별히 조정됩니다.

#### <a id="enable-dedup-via-server-manager"></a>서버 관리자를 사용 하 여 데이터 중복 제거를 사용 하도록 설정
1. 서버 관리자에서 **파일 및 저장소 서비스**를 선택합니다.  
![File and Storage Services를 클릭 합니다.](media/enable-dedup-via-server-manager-1.PNG)
2. **파일 및 저장소 서비스**에서 **볼륨**을 선택합니다.  
![볼륨 클릭](media/enable-dedup-via-server-manager-2.png)
3. 원하는 볼륨을 마우스 오른쪽 단추로 클릭하고 **데이터 중복 제거 구성**을 선택합니다.  
![데이터 중복 제거 구성 클릭](media/enable-dedup-via-server-manager-3.png)
4. 드롭다운 상자에서 원하는 **사용 유형**을 선택하고 **확인**을 선택합니다.  
![드롭다운에서 원하는 사용 유형을 아래로 선택](media/enable-dedup-via-server-manager-4.png)
5. 권장 워크로드를 실행 중인 경우 이것으로 작업이 완료되었습니다. 다른 워크로드의 경우 [기타 고려 사항](#enable-dedup-sometimes-considerations)을 참조하세요.

> [!Note]  
> 이 작업을 수행하는 이유를 포함하여, 파일 확장명 또는 폴더를 제외시키는 방법과 중복 제거 일정을 선택하는 방법에 대한 자세한 내용은 [데이터 중복 제거 구성](advanced-settings.md)에서 확인할 수 있습니다.

#### <a id="enable-dedup-via-powershell"></a>PowerShell을 사용 하 여 데이터 중복 제거를 사용 하도록 설정
1. 관리자 컨텍스트로 다음 PowerShell 명령을 실행합니다.  
    ```PowerShell
    Enable-DedupVolume -Volume <Volume-Path> -UsageType <Selected-Usage-Type>
    ```

2. 권장 워크로드를 실행 중인 경우 이것으로 작업이 완료되었습니다. 다른 워크로드의 경우 [기타 고려 사항](#enable-dedup-sometimes-considerations)을 참조하세요.

> [!Note]  
> [`Enable-DedupVolume`  ](https://technet.microsoft.com/library/hh848441.aspx)을 비롯한 데이터 중복 제거 PowerShell cmdlet은 CIM 세션을 통해 `-CimSession` 매개 변수를 추가하여 원격으로 실행할 수 있습니다. 이는 Nano Server 인스턴스에 대해 원격으로 데이터 중복 제거 PowerShell cmdlet을 실행하는 데 특히 유용합니다. 새 CIM 세션을 만들려면 [`New-CimSession`](https://technet.microsoft.com/library/jj590760.aspx)을 실행합니다.

#### <a id="enable-dedup-sometimes-considerations"></a>기타 고려 사항
> [!Important]  
> 권장 워크로드를 실행 중인 경우에는 이 섹션을 건너뛸 수 있습니다.

* 데이터 중복 제거의 사용 유형에서는 권장 워크로드에 대한 의미 있는 기본값을 제공하지만 모든 워크로드에 유용한 시작점도 제공합니다. 권장 워크로드가 아닌 다른 워크로드의 경우 [데이터 중복 제거의 고급 설정](advanced-settings.md)을 수정하여 중복 제거 성능을 향상시킬 수 있습니다.
* 서버에서 워크로드의 리소스 요구 사항이 높은 경우 [해당 워크로드에 대해서는 예상되는 유휴 시간 동안 실행되도록 데이터 중복 제거 작업을 예약](advanced-settings.md#modifying-job-schedules-change-schedule)해야 합니다. 예상되는 작업 시간 동안 데이터 중복 제거를 실행하면 VM이 소진될 수 있기 때문에 이는 하이퍼 수렴형 호스트에서 중복 제거를 실행할 때 특히 중요합니다.
* 워크로드의 리소스 요구 사항이 높지 않거나, 워크로드 요청에 응답하는 것보다 최적화 작업을 완료하는 것이 더 중요한 경우 [메모리, CPU 및 데이터 중복 제거 작업의 우선 순위를 조정할 수 있습니다](advanced-settings.md#modifying-job-schedules).

## <a id="faq"></a>질문과 대답 (FAQ)
**X 워크 로드에 대 한 데이터 집합에서 데이터 중복 제거를 실행 하려고 합니다. 가능 합니까?**  
[데이터 중복 제거와 상호 운용되지 않는 것으로 알려진](interop.md) 워크로드 외에는 모든 워크로드에서 데이터 중복 제거의 데이터 무결성이 완전히 지원됩니다. Microsoft는 성능을 위해 권장 워크로드도 지원합니다. 다른 워크로드의 성능은 서버에서 수행하고 있는 작업에 따라 크게 달라집니다. 워크로드에 대한 데이터 중복 제거가 성능에 미치는 영향, 이 워크로드에 대한 중복 제거 허용 여부를 결정해야 합니다.

**중복 제거 된 볼륨에 대 한 볼륨 크기 조정 요구 사항은 무엇입니까?**  
Windows Server 2012 및 Windows Server 2012 R2에서는 데이터 중복 제거가 볼륨의 변동을 따를 수 있도록 볼륨 크기를 신중하게 조정해야 했습니다. 이는 일반적으로 변동률이 높은 워크로드에 대한 중복 제거된 볼륨의 평균 최대 크기는 1~2TB이고, 권장되는 절대 최대 크기는 10TB였음을 의미합니다. Windows Server 2016에서는 이러한 제한 사항이 제거되었습니다. 자세한 내용은 [데이터 중복 제거의 새로운 기능](whats-new.md#large-volume-support)을 참조하세요.

**일정 또는 권장된 워크 로드에 대 한 다른 데이터 중복 제거 설정을 수정 해야 합니까?**  
아니요. 제공된 [사용 유형](understand.md#usage-type)은 권장 워크로드에 적합한 기본값을 제공하기 위해 만든 것입니다.

**데이터 중복 제거에 대 한 메모리 요구 사항은 무엇입니까?**  
데이터 중복 제거에는 최소한 300MB 외에 추가로 논리 데이터의 TB당 50MB가 있어야 합니다. 예를 들어 10TB 볼륨을 최적화하는 경우 중복 제거에 최소 800MB의 메모리가 할당되어야 합니다(`300 MB + 50 MB * 10 = 300 MB + 500 MB = 800 MB`). 데이터 중복 제거는 이처럼 적은 메모리로 볼륨을 최적화할 수 있지만 이러한 제한된 리소스를 사용하면 데이터 중복 제거 작업의 속도가 느려집니다.

최적의 경우, 데이터 중복 제거에는 논리 데이터 1TB당 1GB의 메모리가 있어야 합니다. 예를 들어 10TB 볼륨을 최적화하는 경우 데이터 중복 제거에 10GB의 메모리를 할당하는 것이 가장 적절합니다(`1 GB * 10`). 이 비율을 유지하면 데이터 중복 제거 작업의 성능이 극대화됩니다.

**데이터 중복 제거에 대 한 저장소 요구 사항은 무엇입니까?**  
Windows Server 2016에서는 데이터 중복 제거에서 최대 64TB의 볼륨 크기를 지원할 수 있습니다. 자세한 내용은 [데이터 중복 제거의 새로운 기능](whats-new.md#large-volume-support)을 참조하세요.
