---
title: 소프트웨어 인벤토리 로깅 문제 해결
description: 일반적인 소프트웨어 인벤토리 로깅 배포 문제를 해결 하는 방법을 설명 합니다.
ms.prod: windows-server
ms.technology: manage-software-inventory-logging
ms.topic: article
author: brentfor
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 5a02caf63bbd02705aebb8306a7b50a32f3d6c82
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851416"
---
# <a name="troubleshoot-software-inventory-logging"></a>소프트웨어 인벤토리 로깅 문제 해결 

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

## <a name="understanding-sil"></a>SIL 이해

SIL 문제 해결을 시작 하기 전에 해당 구성 요소와 작동 방식을 잘 알고 있어야 합니다. 다음 비디오에서는 SIL 및 SIL 집계의 개요와이를 사용 하 여 인벤토리 데이터를 전달 하 고 보고 하는 방법을 보여 줍니다.

1. [소프트웨어 인벤토리 로깅 소개 (SIL) (10:57)](https://channel9.msdn.com/Blogs/Regular-IT-Guy/An-Introduction-to-Software-Inventory-Logging-SIL)

2. [소프트웨어 인벤토리 로깅: SIL 집계 설정 (14:34)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Setting-up-SIL-Aggregator)

3. [소프트웨어 인벤토리 로깅: SIL 전달 사용 (7:20)](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Enabling-SIL-Forwarding)

## <a name="how-sil-data-flow-works"></a>SIL 데이터 흐름의 작동 방식

SIL 프레임 워크에는 두 가지 주요 구성 요소와 두 개의 통신 채널이 있습니다. 성공적인 SIL 배포에는 두 가지 채널을 통한 데이터 흐름 및 두 구성 요소 간의 데이터 흐름이 필요 합니다 (이는 가상화 된 또는 클라우드 환경 전용 물리적 환경에는 통신 채널 중 하나만 필요 함). 올바르게 배포 하려면 SIL의 구성 요소 및 데이터 흐름을 이해 해야 합니다. 위의 개요 비디오를 시청 한 후에는 두 채널을 통한 데이터 흐름과 구성 요소를 보여 주는 아키텍처 다이어그램이 표시 됩니다. 주황색 화살표는 WinRM을 통한 원격 쿼리를 나타내고 녹색 파선 화살표는 각 WS 끝 노드의 SIL에서 SIL 집계에 대 한 HTTPS 게시를 표시 합니다.

![](../media/software-inventory-logging/image1.png)

SIL에 문제가 발생 하는 경우에는 채널을 통한 데이터 흐름과 구성 요소 간의 중단에 관련 된 것일 수 있습니다. 다음은 세 가지 문제를 해결 하기 위한 문제 해결 단계에 따른 데이터 흐름과 관련 된 가장 일반적인 문제입니다.

-   **데이터 흐름 문제 1** – SilReport cmdlet (또는 일반적으로 데이터가 누락 된 데이터) **을 사용 하는 경우 보고서에 데이터가 없습니다** .

-   **데이터 흐름 문제 2** – 보고서에서 **알 수 없는 호스트에 서버가 너무 많습니다** .

-   **데이터 흐름 문제 3** -물리적 호스트에 있는 vm이 보고서에서 **알 수 없는 OS로 나열** 되 고/또는 SIL를 실행 하는 Windows server에서 **get-sildata** 를 사용할 때 생성 되는 오류가 발생 합니다.

## <a name="troubleshooting-data-flow-issues"></a>데이터 흐름 문제 해결

시작 하기 전에 SIL 집계가 **set-silaggregator** cmdlet으로 시작 된 시간을 알아야 합니다.

>[!IMPORTANT]
>SQL 데이터 큐브가 현지 시스템 시간 오전 3 시에 처리 될 때까지 보고서에는 데이터가 없습니다. 큐브가 데이터를 처리할 때까지 문제 해결 단계를 진행 하지 마십시오.

큐브를 마지막으로 처리 한 시간 보다 최신 이거나 큐브를 처리 하기 전에 (새 설치의 경우) 보고서의 데이터 또는 보고서의 누락 된 데이터 문제를 해결 하는 경우 다음 단계에 따라 SQL 데이터 큐브를 실시간으로 처리 합니다.

1. SQL Server 관리자로 로그인 하 고 명령 프롬프트에서 **SSMS** 를 실행 합니다.
2. 데이터베이스 엔진에 연결합니다.
3. **SQL Server 에이전트** 확장 한 다음 **작업**을 확장 합니다.
4. **SILStagingRefresh** 를 마우스 오른쪽 단추로 클릭 한 다음 **작업 시작 단계**를 선택 합니다.
5. **시작** 을 클릭 하 고 새로 고침 진행률 표시줄이 완료 될 때까지 기다립니다.
6. 관리자 권한으로 PowerShell을 열고 **silreport-openreport** cmdlet을 실행 합니다.

그래도 보고서에 데이터가 없으면 세 가지 데이터 흐름 문제를 해결 하는 과정을 진행 합니다.

### <a name="data-flow-issue-1"></a>데이터 흐름 문제 1 

#### <a name="no-data-in-the-report-when-using-the-publish-silreport-cmdlet-or-data-is-generally-missing"></a>SilReport cmdlet을 사용 하는 경우 보고서에 데이터가 없습니다. (또는 데이터가 일반적으로 누락 됨)

데이터가 누락 된 경우 SQL 데이터 큐브가 아직 처리 되지 않았기 때문일 수 있습니다. 최근에 처리 했 고 누락 된 데이터가 큐브 처리 전에 집계에서 도착 한 것으로 판단 되는 경우 데이터의 경로를 역순으로 따릅니다. 문제를 해결 하려면 고유한 호스트와 고유한 VM을 선택 하세요. 역방향의 데이터 경로는 **SIL agent/task를 실행**하는 **SILA 로컬 디렉터리** &lt; **원격 물리적 호스트** 또는 WS VM &lt; **SILA Report** &lt; **SILA database** 입니다.

#### <a name="check-to-see-if-data-is-in-the-database"></a>데이터가 데이터베이스에 있는지 확인 하십시오.

데이터를 확인 하는 방법에는 **Powershell** 또는 **SSMS**의 두 가지가 있습니다.

>[!Important]
>SILA가 데이터베이스에 데이터를 삽입 한 후 큐브가 한 번 이상 처리 된 경우이 데이터는 보고서에 반영 되어야 합니다. 데이터베이스에 데이터가 없는 경우 실제 호스트를 폴링하는 작업이 실패 하거나 HTTPS 또는 둘 다를 통해 수신 되지 않습니다.

 #### <a name="powershell"></a>PowerShell

1. 관리자 권한으로 PowerShell을 열고 **add-silvmhost** cmdlet을 실행 한 다음 **set-silaggregator**를 실행 합니다.

    >[!NOTE]
    >**Set-silaggregator** 의 출력은 항상 Excel 보고서의 **Windows Server 세부 정보 탭** 을 모방 합니다. 다른 결과가 필요 하지 않습니다.

2. **Add-silvmhost** 실행
   - 나열 된 호스트가 없으면 **add-silvmhost** cmdlet을 사용 하 여 호스트를 추가 합니다.
   - 호스트가 **알 수 없음**으로 표시 되 면 문제 2로 이동 합니다. 
   d-호스트가 나열 되지만 **최근 폴링** 열 아래에 **datetime** 이 없으면 아래의 **문제 2** 로 이동 합니다.

**기타 관련 명령**

**Set-silaggregator-Computername &lt;데이터&gt;를 푸시하는 알려진 서버의 fqdn** : 큐브를 처리 하기 전에도 데이터베이스에서 컴퓨터 (VM)에 대 한 정보를 생성 합니다. 따라서이 cmdlet을 사용 하 여 데이터베이스에서 데이터를 확인 하는 데 사용할 수 있습니다 .이 섹션의 시작 부분에 설명 된 대로 실시간으로 큐브를 새로 고치지 않은 경우에는 HTTPS를 통해 HTTPS, 이전 또는 없이 SIL 데이터를 푸시하는 Windows 서버에 대 한 데이터베이스의 데이터를 확인 하는 데 사용할 수 있습니다.

**Set-silaggregator-VmHostName &lt;add-silvmhost cmdlet&gt;를 사용할 때 최근 폴링 열 아래에 값이 있는 폴링 된 실제 호스트의 fqdn** 입니다. 그러면 큐브가 처리 되기 전에도 데이터베이스에서 실제 호스트에 대 한 정보가 생성 됩니다.

#### <a name="ssms"></a>SSMS

n**폴링 중인 호스트의 데이터를 확인 합니다.**
 
1. **SSMS** 를 열고 **데이터베이스 엔진**에 연결 합니다.
2. **데이터베이스**를 확장 하 고 **선택 트리에서 softwareinventorylogging** 데이터베이스를 확장 하 고 **테이블**을 확장 한 다음 **hostinfo** 테이블을 마우스 오른쪽 단추로 클릭 하 고 상위 1000 행을 선택 합니다. 

    테이블에 하나 이상의 호스트에 대 한 데이터가 있는 경우 해당 호스트에 대 한 폴링이 하나 이상 성공 했습니다.

   **HTTPS를 통해 데이터를 푸시한 Vm 또는 독립 실행형 서버에서 데이터를 확인 합니다.** 

3. **SSMS** 를 열고 **데이터베이스 엔진**에 연결 합니다.
   a2. **데이터베이스**를 확장 하 고 **선택 트리에서 softwareinventorylogging** 데이터베이스를 확장 한 다음 **테이블**을 확장 하 고 **VMInfo** 테이블을 마우스 오른쪽 단추로 클릭 한 다음 상위 1000 행을 선택 합니다. 

    >[!NOTE] 
    >고유 VM에 대 한 각 행은 HTTPS를 통해 성공적으로 푸시되 고 SIL 집계에 의해 처리 되는 처리 된 **bmil** 파일 하나를 나타냅니다. Bmil 파일은 SIL에서 사용 하는 소유 파일 이며, 각 SIL 인스턴스에서 각각 하나씩 생성 됩니다 .이는 SIL 및 SILA가 가상 환경에서 사용 되는 경우에만 필요 합니다. 그렇지 않으면 HTTPS 트래픽만 필요 하며 필요 합니다.

   큐브를 처리 한 후에는 SIL 보고서에 데이터베이스의 모든 데이터를 반영 해야 합니다.

### <a name="data-flow-issue-2"></a>데이터 흐름 문제 2
#### <a name="too-many-servers-under-unknown-host"></a>알 수 없는 호스트에 서버가 너무 많음

이는 SIL 집계가 가상 컴퓨터를 호스트 하는 실제 호스트를 성공적으로 폴링하는 경우 가상 환경에서 발생할 수 있습니다.

1. 관리자 권한으로 **PowerShell** 을 열고 **add-silvmhost** cmdlet을 실행 합니다.

    -   호스트가 **알 수 없음**으로 표시 되는 경우 **add-silvmhost** cmdlet이 올바르게 작동 하지 않습니다. 일반적으로 이러한 호스트에 대 한 액세스를 위해 추가 된 잘못 된 자격 증명 (즉, 알 수 없음) 때문입니다. 하지만 자격 증명이 확인 되 면 **add-silvmhost** cmdlet의 **hosttype** 및 **hypervisortype** 의 자동 검색에서 플랫폼을 인식할 수 없음을 의미할 수 있습니다. 이러한 상황에 사용할 수 있는 고급 문제 해결 단계가 있지만 여기서 다루지 않습니다 (EventViewer SIL 집계 채널 확인).

    -   호스트가 나열 되 고 **hosttype** 및 **hypervisortype** 이 **알 수**없는 값으로 나열 된 경우 (예: Windows 및 HyperV, Ubuntu 및 Xen 등 이지만 **최근 폴링** 열 아래에는 **datetime** 이 없으므로 폴링이 아직 발생 하지 않았습니다.

        -   폴링을 수행할 호스트를 추가한 후 1 시간을 기다려야 합니다 (이 간격을 기본값으로 설정 했다고 가정 하 고 **set-silaggregator** cmdlet을 사용 하 여 확인할 수 있음).

        -   호스트가 추가 된 후 1 시간이 었으 면 폴링 작업이 실행 중인지 확인 합니다. **작업 스케줄러**의 **Microsoft** &gt; **Windows** 에서 **소프트웨어 인벤토리 로깅 집계** 를 선택 하 고 작업 기록을 확인 합니다.

    -   호스트가 나열 되지만 **RecentPoll**, **HostType**또는 **hypervisortype**에 대 한 값이 없는 경우이는 대부분 무시 될 수 있습니다. 이는 HyperV 환경 에서만 발생 합니다. 이 데이터는 실제로 Windows Server VM에서 제공 되며 HTTPS를 통해 실행 중인 실제 호스트를 식별 합니다. 이는 보고 되는 특정 VM을 식별 하는 데 유용할 수 있지만 **SilAggregatorData** cmdlet을 사용 하 여 데이터베이스를 마이닝 해야 합니다.

호스트가 올바르게 폴링 되 면 SILA 데이터베이스에서 이러한 물리적 호스트에 대 한 데이터를 볼 수 있습니다. 여기에는 **최근 폴링**아래에 **datetime** 이 있습니다. 위의 문제 1 섹션에서는이 데이터를 검색 하는 단계를 제공 합니다.

### <a name="data-flow-issue-3"></a>데이터 흐름 문제 3
#### <a name="too-many-physical-hosts-with-vms-listed-as-unknown-os"></a>Vm이 알 수 없는 OS로 나열 된 물리적 호스트가 너무 많음

1. 이러한 호스트 중 하나에 있는 Windows Server 끝 노드 (VM) 하나를 선택 하 고 관리자 권한으로 로그인 합니다.
2. 관리자 권한으로 PowerShell을 엽니다.
3. **Set-sillogging** cmdlet을 사용 하 여 **set-sillogging** 가 실행 중인지 확인 합니다.
   - 실행 중인 경우 **get-sildata**를 사용 하 여 SIL 데이터를 수동으로 푸시합니다.

   - 오류가 있는 경우:
     - **Targeturi** 의 항목에 **https://** 이 있는지 확인 합니다.
     - 모든 필수 구성 요소가 충족 되는지 확인 
     - Windows Server에 필요한 모든 업데이트가 설치 되어 있는지 확인 합니다 (SIL에 대 한 필수 구성 요소 참조). **Get-silwindowsupdate \*3060, \*3000** cmdlet을 사용 하 여이를 확인 하는 것이 가장 빠른 방법입니다 (WS 2012 R2에만 해당).
     - 집계를 사용 하 여 인증 하는 데 사용 되는 인증서가 **set-sillogging**를 사용 하 여 인벤토리 할 로컬 서버의 올바른 저장소에 설치 되어 있는지 확인 합니다.
     - SIL 집계에서 집계를 사용 하 여 인증 하는 데 사용 되는 인증서의 인증서 지문을 **set-silaggregator** **– addcertificatethumbprint** cmdlet을 사용 하 여 목록에 추가 해야 합니다.
     - 엔터프라이즈 인증서를 사용 중인 경우 SIL을 사용하도록 설정된 서버가 인증서를 만든 도메인에 가입되어 있거나 루트 인증 기관을 통해 인증 가능한지를 확인합니다. 데이터를 집계로 전달/푸시하려는 로컬 컴퓨터의 인증서를 신뢰할 수 없는 경우 이 작업이 실패하고 오류가 발생합니다.

     위의 모든 작업을 확인 하 고 확인 한 후에도 문제가 지속 되 면 다음을 수행 합니다.

     - SIL 집계를 설치 하는 데 사용 된 인증서가 정상 상태이 고 SIL 집계 서버 자체의 이름과 일치 하는지 확인 합니다. 또한 기업 인증서를 사용하여 SIL Aggregator를 설치한다면 인증서가 생성된 도메인에 Aggregator가 연결돼야 합니다(만약 다른 컴퓨터가 성공적으로 동일한 SIL Aggregator로 전달된다면 이러한 절차는 불필요합니다).

     -  마지막으로, 전달/푸시를 시도 하는 서버에서 캐시 된 SIL 파일에 대 한 다음 위치를 확인할 수 있습니다. **\Windows\System32\Logfiles\SIL**. **Set-sillogging** 이 시작 되 고 1 시간 이상 실행 중 이거나 **게시-get-sildata** 가 최근에 실행 되었으며이 디렉터리에 파일이 없는 경우 집계에 대 한 로깅이 성공한 것입니다.

오류가 없고 콘솔에 출력이 없는 경우 Windows Server end 노드에서 HTTPS를 통해 SIL 집계로 데이터 푸시/게시를 완료 했습니다. 전달 되는 데이터의 경로를 따르려면 관리자 권한으로 SIL 집계에 로그인 하 고 도착 한 데이터 파일을 검사 합니다. **Program Files (x86)** &gt; **Microsoft SIL 수집기** &gt; SILA directory로 이동 합니다. 실시간으로 도착 하는 데이터 파일을 볼 수 있습니다.

>[!NOTE] 
>**Get-sildata** cmdlet을 사용 하 여 둘 이상의 데이터 파일을 전송할 수 있습니다. 끝 노드의 SIL는 최대 30 일 동안 실패 한 푸시를 캐시 합니다. 다음에 성공한 푸시 모든 데이터 파일은 처리를 위해 집계로 이동 합니다. 이러한 방식으로 새로 설정 된 SIL 집계는 자체 설치 전에 끝 노드의 데이터를 표시할 수 있습니다.

>[!NOTE] 
>낮은 트래픽 상황과만 관련 된 SILA 디렉터리의 데이터 파일을 처리할 때 SILA 규칙은 다음과 같습니다. 트래픽이 높으면 항상 실시간으로 처리를 트리거합니다. 기본 동작은 100 파일이 디렉터리에 도착 한 후 또는 15 분 후에 처리를 개시 한다는 것입니다. 소규모 환경에서 종단 간 문제를 해결 하는 경우 15 분 정도 기다려야 하는 경우가 많습니다.

이러한 파일이 처리 되 면 데이터베이스에 데이터가 표시 됩니다.
