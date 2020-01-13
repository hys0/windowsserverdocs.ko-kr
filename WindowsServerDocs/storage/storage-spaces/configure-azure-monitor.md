---
title: Azure Monitor 이해 및 구성
description: Windows Server 2016 및 2019에서 저장소 공간 다이렉트 클러스터에 대 한 전자 메일 및 sms 경고를 구성 하는 방법 및 Azure Monitor에 대 한 자세한 설정 정보를 제공 합니다.
keywords: 스토리지 공간 다이렉트, azure monitor, 알림, 전자 메일, sms
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: 4a11ad670bdd26cdc771bb5ae357db4928995bb8
ms.sourcegitcommit: bfe9c5f7141f4f2343a4edf432856f07db1410aa
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/25/2019
ms.locfileid: "75352619"
---
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Azure Monitor를 사용 하 여 상태 관리 서비스 오류에 대 한 전자 메일 보내기

>적용 대상: Windows Server 2019, Windows Server 2016

Azure Monitor는 클라우드 및 온-프레미스 환경에서 원격 분석 데이터를 수집, 분석하고 그에 따라 조치를 취하는 포괄적인 솔루션을 제공함으로써 애플리케이션의 성능과 가용성을 최대화합니다. 이를 통해 애플리케이션을 수행하는 방법과 해당 애플리케이션 및 종속된 리소스에 영향을 주는 문제를 사전에 식별하는 방법을 파악할 수 있습니다.

이는 온-프레미스 하이퍼 수렴 형 클러스터에 특히 유용 합니다. Azure Monitor 통합을 사용 하면 클러스터에 문제가 있을 때 (또는 수집 된 데이터를 기반으로 다른 작업에 플래그를 지정 하려는 경우) 전자 메일, 텍스트 (SMS) 및 기타 경고를 구성 하 여 ping 할 수 있습니다. 아래에서는 Azure Monitor 작동 방법, Azure Monitor를 설치 하는 방법 및 알림을 보내도록 구성 하는 방법을 간략하게 설명 합니다.


## <a name="understanding-azure-monitor"></a>Azure Monitor 이해

Azure Monitor에서 수집 된 모든 데이터는 메트릭 및 로그의 두 가지 기본 형식 중 하나에 적합 합니다.

1. [메트릭](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#metrics)은 시간상 특정 지점에서 시스템의 일부 측면을 설명하는 숫자 값입니다. 메트릭은 간단하며 실시간에 가까운 시나리오를 지원할 수 있습니다. Azure Portal의 개요 페이지에서 Azure Monitor에 의해 수집 된 데이터가 표시 됩니다.

![메트릭 탐색기의 메트릭 수집 이미지](media/configure-azure-monitor/metrics.png)

2. [로그](https://docs.microsoft.com/azure/azure-monitor/platform/data-collection#logs)에는 각 형식에 대해 다양한 속성 집합이 포함된 레코드로 구성된 다양한 데이터 형식이 포함됩니다. 이벤트 및 추적과 같은 원격 분석은 분석을 위해 모두 결합될 수 있도록 성능 데이터 외에도 로그로 저장됩니다. Azure Monitor로 수집한 로그 데이터는 수집된 데이터를 신속하게 검색, 통합 및 분석하는 [쿼리](https://docs.microsoft.com/azure/azure-monitor/log-query/log-query-overview)로 분석할 수 있습니다. Azure Portal에서 [Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/portals)를 사용하여 쿼리를 만들고 테스트한 다음, 이러한 도구를 사용하여 데이터를 직접 분석하거나 [시각화](https://docs.microsoft.com/azure/azure-monitor/visualizations) 또는 [경고 규칙](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-overview)에 사용하기 위해 쿼리를 저장할 수 있습니다.

![log analytics의 로그 수집 이미지](media/configure-azure-monitor/logs.png)

이러한 경고를 구성 하는 방법에 대 한 자세한 내용은 아래를 참조 하세요.

## <a name="onboarding-your-cluster-using-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 클러스터 온 보 딩

Windows 관리 센터를 사용 하 여 클러스터를 Azure Monitor로 등록할 수 있습니다.

![Azure Monitor "에 대 한 온 보 딩 클러스터의 Gif](media/configure-azure-monitor/onboarding.gif)

이 온 보 딩 흐름 중에 아래 단계가 내부적으로 발생 합니다. 수동으로 클러스터를 설정 하려는 경우 자세히 구성 하는 방법에 대해 자세히 설명 합니다. 

### <a name="configuring-health-service"></a>상태 관리 서비스 구성

가장 먼저 해야 할 일은 클러스터를 구성 하는 것입니다. 사용자가 알 수 있듯이 [상태 관리 서비스](../../failover-clustering/health-service-overview.md) 스토리지 공간 다이렉트를 실행 하는 클러스터에 대 한 일상적인 모니터링 및 운영 환경을 개선 하 고 있습니다. 

위에서 설명한 것 처럼 Azure Monitor는 클러스터에서 실행 되는 각 노드에서 로그를 수집 합니다. 따라서 다음과 같이 이벤트 채널에 쓰도록 상태 관리 서비스를 구성 해야 합니다.

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

상태 관리 서비스를 구성 하려면 다음을 실행 합니다.

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

위의 cmdlet을 실행 하 여 상태 설정을 설정 하면 이벤트를 *Microsoft-Windows-상태/운영* 이벤트 채널에 기록 하기 시작 합니다.

### <a name="configuring-log-analytics"></a>Log Analytics 구성

클러스터에 대 한 적절 한 로깅을 설정 했으므로 다음 단계는 log analytics를 올바르게 구성 하는 것입니다.

개요를 제공 하기 위해 [Azure Log Analytics](https://docs.microsoft.com/azure/azure-monitor/platform/agent-windows) 데이터 센터 또는 다른 클라우드 환경의 물리적 또는 가상 Windows 컴퓨터에서 데이터를 자세한 분석 및 상관 관계를 위해 단일 리포지토리로 직접 수집할 수 있습니다.

지원되는 구성을 이해하려면 [지원되는 Windows 운영 체제](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) 및 [네트워크 방화벽 구성](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)을 검토합니다.

Azure 구독이 아직 없는 경우 시작하기 전에 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.

#### <a name="login-in-to-azure-portal"></a>Azure Portal에 로그인

Azure Portal([https://portal.azure.com](https://azure.microsoft.com/free/?WT.mc_id=A261C142F))에 로그인합니다.

#### <a name="create-a-workspace"></a>작업 영역 생성

아래 나열 된 단계에 대 한 자세한 내용은 [Azure Monitor 설명서](https://docs.microsoft.com/azure/azure-monitor/learn/quick-collect-windows-computer)를 참조 하세요.

1. Azure Portal에서 **모든 서비스**를 클릭합니다. 리소스 목록에서 **Log Analytics**를 입력합니다. 입력을 시작하면 입력 내용에 따라 목록이 필터링됩니다. **Log Analytics**를 선택합니다.<br><br> 

   ![Azure Portal](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. **만들기**를 클릭하고 다음 항목에 대한 옵션을 선택합니다.

   * 새 **Log Analytics 작업 영역**의 이름(예: *DefaultLAWorkspace*)을 지정합니다. 
   * 기본으로 선택된 값이 적절하지 않으면 드롭다운 목록에서 선택하여 연결할 **구독**을 선택합니다.
   * **리소스 그룹**에 대해 하나 이상의 Azure Virtual Machines를 포함하는 기존 리소스 그룹을 선택합니다. <br><br>

      ![Log Analytics 리소스 블레이드 만들기](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>  

3. **Log Analytics 작업 영역** 창에서 필요한 정보를 제공한 후에 **확인**을 클릭합니다.  

정보가 확인되고 작업 영역이 만들어지는 동안 메뉴의 **알림**에서 진행 상황을 추적할 수 있습니다. 

#### <a name="obtain-workspace-id-and-key"></a>작업 영역 ID 및 키 가져오기
Windows용 Microsoft Monitoring Agent를 설치하기 전에 Log Analytics 작업 영역에 대한 작업 영역 ID 및 키가 필요합니다.  이 정보는 에이전트를 적절히 구성하고 Log Analytics와 성공적으로 통신할 수 있는지 확인하기 위해 설치 마법사에서 필요합니다.  

1. Azure Portal의 왼쪽 위 모서리에 있는 **모든 서비스**를 클릭합니다. 리소스 목록에서 **Log Analytics**를 입력합니다. 입력을 시작하면 입력 내용에 따라 목록이 필터링됩니다. **Log Analytics**를 선택합니다.
2. Log Analytics 작업 영역 목록에서 이전에 만든 *DefaultLAWorkspace*를 선택합니다.
3. **고급 설정**을 선택합니다.<br><br> ![Log Analytics 고급 설정](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>  
4. **연결된 원본**을 선택한 다음 **Windows 서버**를 선택합니다.   
5. **작업 영역 ID** 및 **기본 키**의 오른쪽에 값이 있습니다. 두 파일을 모두 임시로 저장-복사 하 여 해당 시간 동안 즐겨 사용 하는 편집기에 붙여 넣습니다.   

### <a name="installing-the-agent-on-windows"></a>Windows에 에이전트 설치
다음 단계에서는 Microsoft Monitoring Agent를 설치 하 고 구성 합니다. **클러스터의 각 서버에이 에이전트를 설치 하 고 Windows 시작 시 에이전트를 실행 하도록 지정 합니다.**

1. **Windows 서버** 페이지에서 적절한 **Windows 에이전트 다운로드** 버전을 선택하여 Windows 운영 체제의 프로세서 아키텍처에 따라 다운로드합니다.
2. 설치를 실행하여 컴퓨터에 에이전트를 설치합니다.
2. **시작** 페이지에서 **다음**을 클릭합니다.
3. **사용 조건** 페이지에서 라이선스를 읽고 **동의함**을 클릭합니다.
4. **대상 폴더** 페이지에서 기본 설치 폴더를 변경 또는 유지하고 **다음**을 클릭합니다.
5. **에이전트 설치 옵션** 페이지에서 Azure Log Analytics에 에이전트를 연결하도록 선택한 다음, **다음**을 클릭합니다.   
6. **Azure Log Analytics** 페이지에서 다음을 수행합니다.
   1. 앞에서 복사한 **작업 영역 ID** 및 **작업 영역 키(기본 키)** 를 붙여넣습니다.    
    a. 컴퓨터가 프록시 서버를 통해 Log Analytics 서비스와 통신해야 하는 경우 **고급**을 클릭하고 프록시 서버의 URL 및 포트 번호를 제공합니다.  프록시 서버에 인증이 필요한 경우 사용자 이름과 암호를 입력하여 프록시 서버로 인증한 후 **다음**을 클릭합니다.  
7. 필요한 구성 설정 제공을 완료한 후 **다음**을 클릭합니다.<br><br> ![작업 영역 ID 및 기본 키 붙여넣기](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png)<br><br>
8. **설치 준비** 페이지에서 선택 항목을 검토한 다음 **설치**를 클릭합니다.
9. **구성 완료** 페이지에서 **마침**을 클릭합니다.

완료되면 Microsoft Monitoring Agent 가 제어판의 단계를 수행하여 에이전트를 설치합니다. 구성을 검토하고 에이전트가 Log Analytics에 연결되었는지 확인할 수 있습니다. 연결되면 **Azure Log Analytics** 탭에서 에이전트에 **Microsoft Monitoring Agent가 Microsoft Operations Management Suite 서비스에 성공적으로 연결되었습니다.** 와 같은 메시지가 표시됩니다. 

![Log Analytics에 대한 MMA 연결 상태](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

지원되는 구성을 이해하려면 [지원되는 Windows 운영 체제](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) 및 [네트워크 방화벽 구성](https://docs.microsoft.com/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)을 검토합니다.

## <a name="setting-up-alerts-using-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 경고 설정

Windows 관리 센터에서 Log Analytics 작업 영역에 있는 모든 서버에 적용 되는 기본 경고를 구성할 수 있습니다. 

![경고 설정의 Gif "](media/configure-azure-monitor/setup1.gif)

다음은 옵트인 (opt in) 할 수 있는 경고 및 해당 기본 조건입니다.

| 경고 이름                | 기본 조건                                  |
|---------------------------|----------------------------------------------------|
| CPU 사용률           | 10 분 동안 85% 초과                            |
| 디스크 용량 사용률 | 10 분 동안 85% 초과                            |
| 메모리 사용률        | 10 분 동안 사용 가능한 메모리 100 MB 미만   |
| 하트비트                 | 5 분 동안 비트 2 개 미만                   |
| 시스템 치명적 오류     | 클러스터 시스템 이벤트 로그의 모든 중요 한 경고 |
| 상태 관리 서비스 경고      | 클러스터의 모든 health service 오류            |

Windows 관리 센터에서 경고를 구성 하면 Azure의 log analytics 작업 영역에서 경고를 볼 수 있습니다.

![경고 설정의 Gif "](media/configure-azure-monitor/setup2.gif)

이 온 보 딩 흐름 중에 아래 단계가 내부적으로 발생 합니다. 수동으로 클러스터를 설정 하려는 경우 자세히 구성 하는 방법에 대해 자세히 설명 합니다. 

### <a name="collecting-event-and-performance-data"></a>이벤트 및 성능 데이터 수집

Log Analytics는 Windows 이벤트 로그에서 이벤트를 수집하고, 좀 더 긴 기간의 분석 및 보고를 위해 지정한 성능 카운터를 수집할 수 있으며 특정 조건이 검색되면 작업을 수행할 수 있습니다.  다음 단계에 따라 Windows 이벤트 로그의 이벤트 수집과 시작할 몇 가지 일반 성능 카운터를 구성합니다.  

1. Azure Portal의 왼쪽 아래 모서리에 있는 **추가 서비스**를 클릭합니다. 리소스 목록에서 **Log Analytics**를 입력합니다. 입력을 시작하면 입력 내용에 따라 목록이 필터링됩니다. **Log Analytics**를 선택합니다.
2. **고급 설정**을 선택합니다.<br><br> ![Log Analytics 고급 설정](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br> 
3. **데이터**를 선택한 후 **Windows 이벤트 로그**를 선택합니다.  
4. 여기에서 아래 이름을 입력 하 고 더하기 기호 **+** 클릭 하 여 상태 관리 서비스 이벤트 채널을 추가 합니다.  
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. 표에서 심각도 **오류** 및 **경고**를 선택합니다.   
6. 페이지 맨 위에서 **저장**을 클릭하여 구성을 저장합니다.
7. **Windows 성능 카운터**를 선택하여 Linux 컴퓨터의 성능 카운터 수집을 사용하도록 설정합니다. 
8. 새 Log Analytics 작업 영역에 대한 Windows 성능 카운터를 처음으로 구성하는 경우, 몇 가지 공용 카운터를 신속하게 만드는 옵션이 제공됩니다. 각 항목은 옆에 확인란과 함께 나열됩니다.<br> ![선택된 기본 Windows 성능 카운터](media/configure-azure-monitor/windows-perfcounters-default.png)<br> **선택한 성능 카운터 추가**를 클릭합니다.  해당 성능 카운터가 추가되고, 10초의 수집 샘플 간격으로 미리 설정됩니다.  
9. 페이지 맨 위에서 **저장**을 클릭하여 구성을 저장합니다.

## <a name="creating-alerts-based-on-log-data"></a>로그 데이터를 기반으로 경고 만들기

지금까지 만든 경우 클러스터에서 로그 및 성능 카운터를 Log Analytics 전송 해야 합니다. 다음 단계는 일정 한 간격으로 로그 검색을 자동으로 실행 하는 경고 규칙을 만드는 것입니다. 로그 검색 결과가 특정 조건과 일치 하는 경우 전자 메일 또는 텍스트 알림을 보내는 경고가 발생 합니다. 아래에서 살펴보겠습니다.

### <a name="create-a-query"></a>쿼리 만들기

로그 검색 포털을 열어서 시작합니다.   

1. Azure Portal에서 **모든 서비스**를 클릭합니다. 리소스 목록에 **모니터**를 입력합니다. 입력을 시작하면 입력 내용에 따라 목록이 필터링됩니다. **모니터**를 선택합니다.
2. 모니터 탐색 메뉴에서 **Log Analytics**를 선택한 다음, 작업 영역을 선택합니다.

사용할 데이터를 가장 빠르게 검색할 수 있는 방법은 테이블의 모든 레코드를 반환하는 단순 쿼리를 사용하는 것입니다. 검색 상자에 다음 쿼리를 입력 하 고 검색 단추를 클릭 합니다.  

```
Event
```

기본 목록 보기에 데이터가 반환되며, 반환된 총 레코드 수를 확인할 수 있습니다.

![단순 쿼리](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

화면 왼쪽에 있는 필터 창에서는 쿼리를 직접 수정하지 않고 쿼리에 필터링을 추가할 수 있습니다.  해당 레코드 종류에 대해 몇 가지 레코드 속성이 표시되며, 하나 이상의 속성 값을 선택하여 검색 결과를 좁힐 수 있습니다.

**EVENTLEVELNAME** 아래에서 **오류** 옆의 확인란을 선택 하거나 다음을 입력 하 여 결과를 오류 이벤트로 제한 합니다.

```
Event | where (EventLevelName == "Error")
```

![Filter](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

관심 있는 이벤트에 대 한 approriate 쿼리를 만든 후 다음 단계를 위해 해당 쿼리를 저장 합니다.

### <a name="create-alerts"></a>경고 만들기
이제 경고를 만드는 예를 살펴보겠습니다.

1. Azure Portal에서 **모든 서비스**를 클릭합니다. 리소스 목록에서 **Log Analytics**를 입력합니다. 입력을 시작하면 입력 내용에 따라 목록이 필터링됩니다. **Log Analytics**를 선택합니다.
2. 왼쪽 창에서 **경고**를 선택한 다음, 페이지의 위쪽에서 **새 경고 규칙**을 클릭하여 새 경고를 만듭니다.<br><br> ![새 경고 규칙 만들기](media/configure-azure-monitor/alert-rule-02.png)<br>
3. 첫 번째 단계로 **경고 만들기** 섹션 아래에서 리소스로 Log Analytics 작업 영역을 선택하려고 합니다. 이는 로그 기반 경고 신호이기 때문입니다.  이전에 만든 Log Analytics 작업 영역을 포함 하는 두 개 이상 있는 경우 드롭다운 목록에서 특정 **구독** 을 선택 하 여 결과를 필터링 합니다.  드롭다운 목록에서 **Log Analytics**를 선택하여 **리소스 종류**를 필터링합니다.  마지막으로 **리소스** **defaultlaworkspace** 를 선택 하 고 **완료**를 클릭 합니다.<br><br> ![경고 만들기 1단계 작업](media/configure-azure-monitor/alert-rule-03.png)<br>
4. **경고 조건**섹션 아래에서 **조건 추가** 를 클릭 하 여 저장 된 쿼리를 선택한 다음 경고 규칙이 따르는 논리를 지정 합니다.
5. 다음 정보로 경고를 구성합니다.  
   a. **기준** 드롭다운 목록에서 **미터법**을 선택합니다.  메트릭 측정값은 쿼리에서 지정된 임계값을 초과하는 값을 포함한 각 개체에 대해 경고를 만듭니다.  
   b. **조건**에 대해 **보다 큼** 을 선택 하 고이를 지정 합니다.  
   c. 그런 다음 경고를 트리거할 시기를 정의 합니다. 예를 들어 **연속 위반** 을 선택 하 고 드롭다운 목록에서 값 3 **보다 크게** 를 선택할 수 있습니다.  
   d. 평가 기준 섹션에서 **기간** 값을 **30** 분으로 수정 하 고 **Frequency** 를 5로 수정 합니다. 규칙이 5분마다 실행되고 현재 시간 이전 30분 내에 만들어진 레코드를 반환합니다.  기간을 더 넓은 기간으로 설정하면 잠재적인 데이터 대기 시간이 발생할 수 있으므로 경고가 발생하지 않는 거짓 부정을 방지하기 위해 쿼리에서 데이터를 반환하도록 합니다.  
6. **완료**를 클릭하여 경고 규칙을 완료합니다.<br><br> ![경고 신호 구성](media/configure-azure-monitor/alert-signal-logic-02.png)<br> 
7. 이제 두 번째 단계로 이동 하 여 경고 **규칙 이름** 필드에 경고 이름을 입력 합니다 (예: **모든 오류 이벤트에 대 한 경고**).  경고에 대한 세부 사항을 자세히 설명하는 **설명**을 지정하고 **심각도** 값에 제공된 옵션에서 **위험(Sev 0)** 을 선택합니다.
8. 생성 시 경고 규칙을 즉시 활성화하려면 **규칙을 만들면 바로 사용**에 기본값을 적용합니다.
9. 세 번째 및 마지막 단계는 경고가 트리거되는 각 시간마다 동일한 작업이 수행되고 정의한 각 규칙에 대해 사용할 수 있는지 확인하는 **작업 그룹**을 지정합니다. 다음 정보로 새 작업 그룹을 구성합니다.  
   a. **새 작업 그룹**을 선택하면 **작업 그룹 추가** 창이 나타납니다.  
   b. **동작 그룹 이름**에 **IT 운영 팀 - 알림**과 같은 이름 및 **itops-n**과 같은 **약식 이름**을 지정합니다.  
   c. **구독** 및 **리소스 그룹**에 대한 기본값이 올바른지 확인합니다. 올바르지 않은 경우 드롭다운 목록에서 올바른 값을 선택합니다.   
   d. 작업 섹션 아래에서 **이메일 보내기**와 같은 작업에 대한 이름을 지정하고 **작업 유형** 아래의 드롭다운 목록에서 **이메일/SMS/푸시/음성**을 선택합니다. **이메일/SMS/푸시/음성** 속성 창이 추가 정보를 제공하기 위해 오른쪽에 열립니다.  
   e. **이메일/SMS/푸시/음성** 창에서 기본 설정을 선택 하 고 설정 합니다. 예를 들어 **전자 메일** 을 사용 하도록 설정 하 고 메시지를 배달 하는 데 유효한 전자 메일 SMTP 주소를 제공 합니다.  
   f. **확인** 을 클릭하여 변경 내용을 저장합니다.<br><br> 

    ![새 작업 그룹 만들기](media/configure-azure-monitor/action-group-properties-01.png)

10. **확인**을 클릭하여 작업 그룹을 완료합니다. 
11. **경고 규칙 만들기**를 클릭하여 경고 규칙을 완료합니다. 그 즉시 실행이 시작됩니다.<br><br> ![새 경고 규칙 만들기 완료](media/configure-azure-monitor/alert-rule-01.png)<br> 

## <a name="see-alerts"></a>경고 참조

참조를 위해 Azure에서 예제 경고는 다음과 같습니다.

![Azure에서 경고의 Gif "](media/configure-azure-monitor/alert.gif)

다음은 Azure Monitor에서 전송 하는 전자 메일의 예입니다.

![경고 전자 메일 예제](media/configure-azure-monitor/warning.png)

## <a name="see-also"></a>참고 항목

- [스토리지 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- 자세한 내용은 [Azure Monitor 설명서](https://docs.microsoft.com/azure/azure-monitor/learn/tutorial-viewdata)를 참조 하세요.
- [다른 Azure 하이브리드 서비스에 연결](../../manage/windows-admin-center/azure/index.md)하는 방법에 대 한 개요는이 내용을 참조 하세요.
