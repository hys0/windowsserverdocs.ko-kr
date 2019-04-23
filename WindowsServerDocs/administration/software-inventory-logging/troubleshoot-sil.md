---
title: 소프트웨어 인벤토리 로깅 문제 해결
description: 일반적인 소프트웨어 인벤토리 로깅 배포 문제를 해결 하는 방법에 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: manage-software-inventory-logging
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
author: brentfor
ms.author: coreyp
manager: lizapo
ms.date: 10/16/2017
ms.openlocfilehash: 6ea8a336e2c40b55e2ad6b508d89db7dcb668315
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832854"
---
# <a name="troubleshoot-software-inventory-logging"></a>소프트웨어 인벤토리 로깅 문제 해결 

>적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

##<a name="understanding-sil"></a>SIL 이해

SIL 문제 해결을 시작 하기 전에 해당 구성 요소 및 작동 방식을 이해를 해야 합니다. 다음 비디오는 SIL 및 SIL Aggregator의 개요 및 사용 하 여 전달 하는 방법 및 보고서 인벤토리 데이터를 제공 합니다.

1. [소프트웨어 인벤토리 로깅 (SIL) (10:57) 소개](https://channel9.msdn.com/Blogs/Regular-IT-Guy/An-Introduction-to-Software-Inventory-Logging-SIL)

2. [소프트웨어 인벤토리 로깅: SIL Aggregator (14:34) 설정](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Setting-up-SIL-Aggregator)

3. [소프트웨어 인벤토리 로깅: SIL 전달 (7:20)를 사용 하도록 설정](https://channel9.msdn.com/Blogs/windowsserver/Software-Inventory-Logging-Enabling-SIL-Forwarding)

##<a name="how-sil-data-flow-works"></a>SIL 데이터 흐름이 작동 하는 방법

SIL 프레임 워크에는 두 가지 주요 구성 요소 및 통신의 두 채널이 있습니다. 둘 다를 통해 데이터 흐름을 채널과 두 구성 요소 간 배포에 반드시 필요한를 성공적으로 SIL (가상화 된, 또는 클라우드 환경-순수 하 게 실제 환경만 필요 하나 통신 채널의 가정). 구성 요소 및이 올바르게 배포 하려면 SIL의 데이터 흐름을 이해 해야 합니다. 위의 개요 비디오를 시청 한 후 두 채널을 통해 구성 요소 및 데이터 흐름을 보여 주는 아키텍처 다이어그램을 표시 됩니다. 주황색 화살표는 WinRM을 통해 원격 쿼리를 나타내는 녹색 점선으로 된 화살표 HTTPS 게시를 SIL Aggregator에서 SIL을 각 WS 최종 노드에 지정 합니다.

![](../media/software-inventory-logging/image1.png)

SIL 사용 하 여 문제가 발생 하면 경우 채널을 통해 및 구성 요소 간의 데이터 흐름을 중단 하 관련 되었이 됩니다. 데이터 흐름에서 뒤에 다음 섹션에서 각 세 가지 문제를 해결 하는 문제 해결 단계와 관련 된 가장 일반적인 문제는 다음과가 같습니다.

-   **데이터 흐름 1 문제** – **게시 SilReport cmdlet을 사용 하는 경우 보고서에 데이터가 없는** (또는 일반적으로 누락 된 데이터).

-   **데이터 흐름 문제 2** – **너무 알 수 없는 호스트에서 여러 서버** 보고서에서입니다.

-   **데이터 흐름 문제 3** – **너무 알 수 없는 OS로 나열 된 실제 호스트에서 여러 Vm** 보고서 및/또는 사용 하는 경우 생성 된 오류가 **Publish-sildata** SIL을 실행 하는 Windows 서버에서.

##<a name="troubleshooting-data-flow-issues"></a>데이터 흐름 문제 해결

SIL Aggregator가 시작 하는 얼마 알아야 할 것을 시작 하기 전에 합니다 **시작 t** cmdlet.

>[!IMPORTANT]
>로컬 시스템 시간을 오전 3 시에 SQL 데이터 큐브를 처리할 때까지 보고서에 데이터가 있어야 됩니다. 문제 해결 단계 데이터 큐브가 처리 될 때까지 진행 하지 마세요.

큐브 처리 또는 큐브가 (새 설치의 경우)에 대 한 적이 처리 되기 전에 실시간으로 SQL 데이터 큐브를 처리 하려면 다음이 단계를 수행 된 마지막 시간 보다 더 최신는 보고서 (또는 보고서에서 누락 된)의 데이터를 해결 하는 경우 :

1. SQL Server의 관리자 권한으로 로그인 하 고 실행 **SSMS** 명령 프롬프트에서.
2. 데이터베이스 엔진에 연결합니다.
3. 확장 **SQL Server 에이전트** 펼친 다음 **작업**합니다.
4. 마우스 오른쪽 단추로 클릭 **SILStagingRefresh** 선택한 후 **작업 시작 단계**합니다.
5. 클릭 **시작** 새로 고침 진행률 표시줄이 완료 될 때까지 기다립니다.
6. 실행 관리자 권한으로 PowerShell을 엽니다는 **게시 silreport openreport** cmdlet.

가 여전히 데이터가 보고서의 경우 3 개의 데이터 흐름 문제 해결 진행 합니다.

###<a name="data-flow-issue-1"></a>데이터 흐름 문제 1 

####<a name="no-data-in-the-report-when-using-the-publish-silreport-cmdlet-or-data-is-generally-missing"></a>게시 SilReport cmdlet을 사용 하는 경우 보고서에 데이터가 없습니다 (또는 일반적으로 누락 된 데이터)

데이터가 누락 된 경우 SQL 데이터 큐브가 아직 처리 하지 되지 인해 것입니다. 최근에 처리 하 고 누락 된 데이터 큐브를 처리 하기 전에 수집기에 도착 했을 해야 하는 것이 생각 하는 경우 반대 순서로 데이터의 경로 따릅니다. 문제를 해결 하는 고유한 호스트 및 고유한 VM을 선택 합니다. 데이터 경로 역순에서 **SILA 보고서** &lt; **SILA 데이터베이스** &lt; **SILA 로컬 디렉터리** &lt;  **원격 물리적 호스트** 나 **SIL 에이전트/작업을 실행 하는 WS VM**합니다.

####<a name="check-to-see-if-data-is-in-the-database"></a>데이터베이스의 데이터 인지 확인 하려면 선택 합니다.

두 가지 방법으로 데이터를 확인 합니다. **Powershell** 나 **SSMS**합니다.

>[!Important]
>큐브가 한 번 이상 처리 SILA 데이터베이스에 데이터를 삽입 하므로,이 데이터를 보고서에 반영 되어야 합니다. 데이터베이스에 데이터가 없는 경우 실패 하는 물리적 호스트를 폴링 중 하나는 또는 HTTPS, 또는 둘 다를 통해 수신 되는 아무 작업도 수행 합니다.

 ####<a name="powershell"></a>PowerShell

1. 실행 관리자 권한으로 PowerShell을 엽니다는 **get silvmhost** cmdlet을 실행 한 다음 **get t**합니다.

    >[!NOTE]
    >출력 **get t** 항상 유사 합니다 **Windows 서버 세부 정보 탭** Excel 보고서. 다른 결과 예상 하지 마십시오.

2. 실행 **get silvmhost**
 - 있습니다 사용 하 여 호스트를 추가한 호스트 나열 된 경우는 **추가 silvmhost** cmdlet.
 - 으로 나열 된 호스트 **알 수 없는**문제 2로 이동 하세요. d-호스트 나와 있지만 경우 없습니다 **날짜/시간** 아래 합니다 **최근 설문 조사** 열을 이동 **문제 2** 아래.

**다른 관련된 명령**

**Get t-Computername &lt;데이터를 푸시하는 알려진 서버의 fqdn&gt;**: 큐브가 처리 전에 컴퓨터 (VM)에 대 한 정보를 데이터베이스에서 생성 됩니다. 따라서 이전 이나 오전 3 시 큐브 프로세스 없이 HTTPS (또는이 섹션의 시작 부분에서 설명한 대로 실시간으로 큐브를 새로 고칠 하지 않은 경우)를 통해 SIL 데이터를 푸시하는 Windows Server에 대 한 데이터베이스의 데이터를 확인 하려면이 cmdlet은 사용할 수 있습니다.

**Get t VmHostName &lt;폴링된 실제 호스트의 fqdn Get-silvmhost cmdlet을 사용 하는 경우 최근 설문 조사 열 아래에 있는 값이 있는 경우&gt;**: 큐브가 처리 전에 실제 호스트에 대 한 정보를 데이터베이스에서 생성 됩니다.

####<a name="ssms"></a>SSMS

n**폴링 중인 호스트에서 데이터를 확인 합니다.**
 
1. 열기 **SSMS** 에 연결 합니다 **데이터베이스 엔진**합니다.
2. 확장 **데이터베이스**를 확장 합니다 **SoftwareInventoryLogging** 데이터베이스를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭는 **HostInfo** 테이블 차례로 상위 1000 개의 행을 선택 합니다. 

    테이블에 하나 이상의 호스트에 대 한 데이터의 경우 는/those 호스트에 대 한 폴링 후 완료 됨 한 번 이상.

 **Vm 또는 HTTPS를 통해 데이터를 밀어 넣었으면는 독립 실행형 서버에서 데이터를 확인 합니다.** 

1. 열기 **SSMS** 에 연결 합니다 **데이터베이스 엔진**합니다.
a2. 확장 **데이터베이스**를 확장 합니다 **SoftwareInventoryLogging** 데이터베이스를 확장 하 고 **테이블**를 마우스 오른쪽 단추로 클릭는 **VMInfo** 테이블 차례로 상위 1000 개의 행을 선택 합니다. 

    >[!NOTE] 
    >각 행에는 고유한 VM 처리 하나 나타낼 **bmil** 파일 성공적으로 HTTPS를 통해 푸시되 고 SIL Aggregator에서 처리 합니다. Bmil 파일이 SIL 사용 되는 독점 파일, 각 만들어집니다는 가상 환경에서 SIL 및 SILA 각 SIL 된 인스턴스에서이 값은 필요한 경우 사용 합니다. 그렇지 않으면 HTTPS 트래픽만 필요한 /).

 큐브가 처리 한 후 데이터베이스의 모든 데이터를 SIL 보고서에 반영 되어야 합니다.

###<a name="data-flow-issue-2"></a>데이터 흐름 문제 2
####<a name="too-many-servers-under-unknown-host"></a>알 수 없는 호스트에서 너무 많은 서버

이 SIL Aggregator에서 가상 컴퓨터를 호스트 하는 실제 호스트 폴링하고 하지 하는 경우 가상 환경에서 발생할 수 있습니다.

1. 오픈 **PowerShell** 관리자 권한으로 실행 합니다 **get silvmhost** cmdlet.

    -   으로 나열 된 호스트 **알 수 없는**서 **추가 silvmhost** cmdlet 제대로 작동 하지 않는 – 일반적으로 이러한 호스트에 대 한 액세스에 대 한 추가 하는 잘못 된 자격 증명으로 인해 (따라서 알 수 없는). 자격 증명 확인 되 면 자동 검색을 의미할 수 있습니다 하지만 **hosttype** 및 **hypervisortype** 에 **추가 silvmhost** cmdlet을 인식할 수 없습니다.는 플랫폼입니다. 문제 해결 단계에 이러한 상황에서는 사용할 수 있는 고급는 하지만 여기서 설명 하지 않습니다 (EventViewer SIL Aggregator 채널 확인).

    -   나열 된 호스트 및 **hosttype** 하 고 **hypervisortype** 하지 않은 값과 함께 나열 됩니다 **알 수 없는**, 즉 Windows HyperV 또는 Ubuntu 및 Xen과 등 이지만 없습니다 **날짜/시간** 아래에서 **최근 설문 조사** 열을 폴링하는 것은 성공적으로 생일이 아직 합니다.

        -   발생 하도록 폴링에 대 한 호스트를 추가한 후 1 시간 대기 해야 (이 간격을 설정 하는 것으로 가정 – 기본을 확인할 수 있습니다 사용 하는 **get t** cmdlet).

        -   호스트 추가 된 시간 되었으면, 폴링 작업 실행 되 고 있는지 확인 합니다. **작업 스케줄러**를 선택 **Software Inventory Logging Aggregator** 아래의 **Microsoft** &gt; **Windows** 확인 작업의 기록입니다.

    -   호스트 나열 되어 있지만 대 한 값인 경우 **RecentPoll**를 **HostType**, 또는 **HypervisorType**를 대부분 무시 됩니다. HyperV 환경에만 전송 됩니다. 이 데이터는 HTTPS를 통해 실행 중인 실제 호스트를 식별 하는 Windows Server VM에서 실제로 가져옵니다. 이 보고 하지만 사용 하 여 데이터베이스 마이닝 필요는 특정 VM에 식별 유용할 수 있습니다 합니다 **Get SilAggregatorData** cmdlet.

호스트를 올바르게 폴링 되 면 SILA 데이터베이스에서 이러한 물리적 호스트에 대 한 데이터를 볼 수는 있는 **날짜/시간** 아래에서 **최근 설문 조사**합니다. 위의 문제 1 섹션에는이 데이터를 검색 하기 위한 단계를 제공 합니다.

###<a name="data-flow-issue-3"></a>데이터 흐름 문제 3
####<a name="too-many-physical-hosts-with-vms-listed-as-unknown-os"></a>알 수 없는 OS로 나열 된 Vm 사용 하 여 너무 많은 실제 호스트

1. 하나의 Windows Server 끝 노드 (VM)에 이러한 호스트 중 하나를 알고 있는 관리자 권한으로 로그인을 선택 합니다.
2. 관리자 권한으로 PowerShell을 엽니다.
3. 확인할 **SilLogging** 를 사용 하 여 실행 되는 **Get-sillogging** cmdlet.
 - 를 실행 하는 경우 수동으로 사용 하 여 SIL 데이터를 푸시 하려고 **Publish-sildata**합니다.

  - 오류가 있는 경우:
     - 확인 합니다 **targeturi** 가 **https://** 항목의 합니다.
     - 모든 필수 조건 충족 되는지 확인 
     - Windows Server에 대 한 모든 필수 업데이트 설치 되어 있는지 확인 (SIL에 대 한 필수 조건 참조). (WS 2012 R2에만 해당)에서 확인할 수 다음 cmdlet을 사용 하는 빠른 방법은 무엇입니까? **Get-SilWindowsUpdate \*3060, \*3000**
     - 집계를 사용 하 여 인증 하는 데 사용 되는 인증서를 사용 하 여 인벤토리를 로컬 서버에 올바른 저장소에 설치 되어 있는지 확인 **SilLogging**합니다.
     - SIL Aggregator에서 집계를 사용 하 여 인증에 사용 되는 인증서의 인증서 지문을 사용 하 여 목록에 추가 됩니다 확인 해야 합니다 **Set-silaggregator** **-AddCertificateThumbprint** cmdlet입니다.
     - 엔터프라이즈 인증서를 사용 중인 경우 SIL을 사용하도록 설정된 서버가 인증서를 만든 도메인에 가입되어 있거나 루트 인증 기관을 통해 인증 가능한지를 확인합니다. 데이터를 집계로 전달/푸시하려는 로컬 컴퓨터의 인증서를 신뢰할 수 없는 경우 이 작업이 실패하고 오류가 발생합니다.

    문제가 계속 되 되지만 위의 모든 확인 되었으며 확인:

    - SIL Aggregator를 설치 하는 데 사용한 인증서는 정상 상태이 고 SIL Aggregator 서버 자체의 이름과 일치 하는 확인 합니다. 또한 기업 인증서를 사용하여 SIL Aggregator를 설치한다면 인증서가 생성된 도메인에 Aggregator가 연결돼야 합니다(만약 다른 컴퓨터가 성공적으로 동일한 SIL Aggregator로 전달된다면 이러한 절차는 불필요합니다).

    -  마지막으로 전달/푸시 하려는 서버에서 캐시 된 SIL 파일에 대 한 다음 위치를 확인할 수 있습니다 **\Windows\System32\Logfiles\SIL**합니다. 하는 경우 **SilLogging** 에서 시작 하 고 실행 한 시간 이상, 또는 **Publish-sildata** 최근에 실행 했지만 보다도 로깅 집계에이 디렉터리에 파일이 없 및 성공 합니다.

오류가 없으면 및 콘솔에 출력이 있으면 다음는 데이터 푸시/게시 끝 노드와 Windows Server에서에서 HTTPS 통한 SIL Aggregator에 성공 했습니다. 관리자 권한으로 SIL Aggregator에 데이터에서는 로그인의 경로 따르고 도착 한 데이터 파일을 검사 합니다. 로 이동 **프로그램 파일 (x86)** &gt; **Microsoft SIL Aggregator** &gt; SILA 디렉터리입니다. 실시간으로 도착 하는 데이터 파일을 볼 수 있습니다.

>[!NOTE] 
>둘 이상의 데이터 파일을 사용 하 여 전송 된 합니다 **Publish-sildata** cmdlet. SIL 끝 노드는 최대 30 일 동안 실패 한 푸시를 캐시 합니다. 다음 성공 푸시에서 모든 데이터 파일 처리에 대 한 집계로 이동 됩니다. 이러한 방식으로 SIL Aggregator를 새로 설정 표시할 수는 자체 설치 하기 전에 최종 노드에서 데이터.

>[!NOTE] 
>SILA SILA 디렉터리에만 트래픽이 낮은 상황에서 관련 된 데이터 파일을 처리할 때 따르는 규칙 있습니다. 트래픽이 항상 실시간에서 처리를 트리거합니다. 기본 동작은 처리를 시작 하거나 100 개의 파일 디렉터리 또는 15 분 후에 도착 한 후입니다. 엔드-투-엔드는 소규모 환경에서 문제를 해결 하는 경우 15 분을 대기 하는 데 필요한 경우가 있습니다.

이러한 파일은 처리 후 데이터베이스에 데이터가 표시 됩니다.
