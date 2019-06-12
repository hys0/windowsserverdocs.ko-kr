---
title: 이해 및 Azure Monitor를 구성 합니다.
description: Azure Monitor에 새로운 기능 및 Windows Server 2016 및 2019에 저장소 공간 다이렉트 클러스터에 대 한 전자 메일 및 sms 경고를 구성 하는 방법에 대 한 설치 정보를 자세히 설명 합니다.
keywords: 저장소 공간 다이렉트를 azure monitor, 알림, 전자 메일, sms
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: 908e4a7a75606905caebfa4b79168b3976982e6d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447589"
---
---
# <a name="use-azure-monitor-to-send-emails-for-health-service-faults"></a>Azure 모니터를 사용 하 여 상태 서비스 오류에 대 한 전자 메일 보내기

>적용 대상: Windows Server 2019, Windows Server 2016

Azure Monitor를 수집, 분석 및 클라우드 로부터 원격 분석 데이터 역할에 대 한 포괄적인 솔루션을 제공 함으로써 응용 프로그램의 성능과 가용성을 최대화 하 고 온-프레미스 환경입니다. 응용 프로그램을 수행 하는 방법을 이해 하도록 도와 하 고 사전에 및 종속 리소스에 영향을 주는 문제를 식별 합니다.

온-프레미스 하이퍼 수렴 형 클러스터에 대해 특히 유용합니다. 통합 Azure Monitor를 통해 전자 메일, 텍스트 (SMS) 및 클러스터를 사용 하 여 (또는 수집 된 데이터에 따라 다른 활동 플래그를 적용 하도록 하려는 경우)에 문제가 발생 하는 경우이 ping 할 다른 경고를 구성할 수 있습니다. 아래 Azure Monitor의 작동 원리, Azure Monitor를 설치 하는 방법 및 알림을 보내도록 구성 하는 방법을 간략하게 설명 됩니다.


## <a name="understanding-azure-monitor"></a>Azure Monitor를 이해합니다.

두 가지 기본 유형 중 하나에 적합 한 Azure Monitor에서 수집한 모든 데이터: 메트릭 및 로그 합니다.

1. [메트릭](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-collection#metrics) 시간에서 특정 지점에서 시스템의 일부 측면을 설명 하는 숫자 값입니다. 이들은 간단 하 고 거의 실시간 시나리오를 지원할 수입니다. Azure portal에서 해당 개요 페이지에서 Azure Monitor에서 수집 된 데이터 표시 됩니다.

![메트릭 탐색기에서 메트릭 수집의 이미지](media/configure-azure-monitor/metrics.png)

2. [로그](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/data-collection#logs) 여러 종류의 다른 각 형식에 대 한 속성 집합을 사용 하 여 레코드를 구성 하는 데이터를 포함 합니다. 이벤트 및 추적과 같은 원격 분석으로 저장 됩니다 로그 또한 성능 데이터를 모두 결합 되는 분석 되도록 합니다. Azure Monitor에서 수집한 로그 데이터를 사용 하 여 분석할 수 있습니다 [쿼리](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/log-query-overview) 를 신속 하 게 검색 하 고, 통합 및, 수집 된 데이터를 분석 합니다. 만들고 사용 하 여 쿼리를 테스트할 수 있습니다 [Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/log-query/portals) Azure portal 및 다음에서 직접 이러한 도구를 사용 하 여 데이터를 분석 또는 사용에 대 한 쿼리를 저장할 [시각화](https://docs.microsoft.com/en-us/azure/azure-monitor/visualizations) 또는 [경고 규칙](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/alerts-overview)합니다.

![log analytics에서 수집 된 로그의 이미지](media/configure-azure-monitor/logs.png)

에서는 이러한 경고를 구성 하는 방법에 자세한 내용은 아래의 세부 정보를 해야 합니다.

## <a name="configuring-health-service"></a>상태 관리 서비스를 구성합니다.

가장 먼저 수행 해야 하는 경우 클러스터 구성 아시다시피, 합니다 [Health Service](../../failover-clustering/health-service-overview.md) 일상적인 모니터링 및 저장소 공간 다이렉트를 실행 하는 클러스터에 대 한 운영 경험이 향상 됩니다. 

위에서 말한 것 처럼 Azure Monitor에서 클러스터에서 실행 되는 각 노드의 로그를 수집 합니다. 따라서 이런 경우에 이벤트 채널을 쓸 Health Service를 구성 해야 합니다.

```
Event Channel: Microsoft-Windows-Health/Operational
Event ID: 8465
```

상태 서비스를 구성 하려면:

```PowerShell
get-storagesubsystem clus* | Set-StorageHealthSetting -Name "Platform.ETW.MasTypes" -Value "Microsoft.Health.EntityType.Subsystem,Microsoft.Health.EntityType.Server,Microsoft.Health.EntityType.PhysicalDisk,Microsoft.Health.EntityType.StoragePool,Microsoft.Health.EntityType.Volume,Microsoft.Health.EntityType.Cluster"
```

이벤트에 기록 되 고 시작 하려고 할 상태 설정을 설정 하려면 위의 cmdlet을 실행 하는 경우는 *Microsoft-Windows-상태/Operational* 이벤트 채널입니다.

## <a name="configuring-log-analytics"></a>Log Analytics 구성

이제가 있는 경우 설치 클러스터에 적절 한 로깅을 올바르게 log analytics를 구성 하려면 다음 단계가입니다.

개요를 제공 [Azure Log Analytics](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/agent-windows) 상세한 분석 및 상관 관계를 단일 저장소로 데이터 센터 또는 다른 클라우드 환경의 실제 또는 가상 Windows 컴퓨터에서 직접 데이터를 수집할 수 있습니다.

를 지원 되는 구성을 이해 하려면 검토 [지원 되는 Windows 운영 체제](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) 하 고 [네트워크 방화벽 구성](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)합니다.

Azure 구독이 없으면 만듭니다는 [무료 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) 시작 하기 전에 합니다.

### <a name="login-in-to-azure-portal"></a>Azure Portal에 로그인

Azure portal에 로그인 [ https://portal.azure.com ](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)합니다.

### <a name="create-a-workspace"></a>작업 영역 만들기

아래에 나열 된 단계에 대 한 자세한 내용은 참조는 [Azure Monitor 설명서](https://docs.microsoft.com/en-us/azure/azure-monitor/learn/quick-collect-windows-computer)합니다.

1. Azure 포털에서 클릭 **모든 서비스**합니다. 리소스 목록에서 입력 **Log Analytics**합니다. 사용자의 입력에 따라 입력을 시작 하면 목록이 필터링 됩니다. 선택 **Log Analytics**합니다.<br><br> 

   ![Azure Portal](media/configure-azure-monitor/azure-portal-01.png)<br><br>

2. 클릭 **만들기**, 다음 항목에 대 한 옵션을 선택 합니다.

   * 새 이름을 입력 **Log Analytics 작업 영역**와 같은 *DefaultLAWorkspace*합니다. 
   * 선택 된 **구독** 기본으로 선택이 적합 하지 않은 경우 드롭다운 목록에서 선택 하 여 연결할 합니다.
   * 에 대 한 **리소스 그룹**, 하나 이상의 Azure virtual machines를 포함 하는 기존 리소스 그룹을 선택 합니다. <br><br>

      ![Log Analytics 리소스 블레이드 만들기](media/configure-azure-monitor/create-loganalytics-workspace-02.png) <br><br>  

3. 필요한 정보를 제공한 후 합니다 **Log Analytics 작업 영역** 창 클릭 **확인**합니다.  

정보가 확인 되 고 만들어진 하는 동안 진행 상황을 추적할 수 있습니다 **알림을** 합니다. 

### <a name="obtain-workspace-id-and-key"></a>작업 영역 ID 및 키 가져오기
작업 영역 ID 및 키 필요는 Microsoft 모니터링 에이전트에 대 한 Windows를 설치 하기 전에 Log Analytics 작업 영역에 대 한 합니다.  에이전트를 구성 하 고 Log Analytics와 성공적으로 통신할 수 있는지 확인 하려면 설치 마법사에서이 정보가 필요 합니다.  

1. Azure 포털에서 클릭 **모든 서비스** 왼쪽 위 모서리에서 찾을 수 있습니다. 리소스 목록에서 입력 **Log Analytics**합니다. 사용자의 입력에 따라 입력을 시작 하면 목록이 필터링 됩니다. 선택 **Log Analytics**합니다.
2. Log Analytics 작업 영역 목록에서 선택 *DefaultLAWorkspace* 이전에 생성 합니다.
3. 선택 **고급 설정**합니다.<br><br> ![Log Analytics 고급 설정](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br>  
4. 선택 **연결 된 원본**를 선택한 후 **Windows 서버**합니다.   
5. 오른쪽에 값 **작업 영역 ID** 하 고 **Primary Key**합니다. 둘 다를 일시적으로 저장-복사 하 고 모두 당분간 즐겨 찾는 편집기에 붙여 넣습니다.   

## <a name="installing-the-agent-on-windows"></a>Windows에 에이전트 설치
다음 단계를 설치 하 고 Microsoft Monitoring Agent를 구성 합니다. **클러스터의 각 서버에이 에이전트를 설치 및 Windows 시작 시 실행 되도록 에이전트를 지정 해야 합니다.**

1. 에 **Windows 서버** 페이지에서 적절 한 선택 **Windows 에이전트 다운로드** Windows 운영 체제의 프로세서 아키텍처에 따라 다운로드 하는 버전입니다.
2. 컴퓨터에 에이전트를 설치 하려면 설치 프로그램을 실행 합니다.
2. **시작** 페이지에서 **다음**을 클릭합니다.
3. 에 **사용 약관** 페이지에서 라이선스를 읽고 클릭 **동의**합니다.
4. 에 **대상 폴더** 페이지를 변경 하거나 기본 설치 폴더를 유지 하 고 클릭 **다음**합니다.
5. 에 **에이전트 설치 옵션** 페이지에서 Azure Log Analytics에 에이전트를 연결 하 여 클릭 **다음**합니다.   
6. 에 **Azure Log Analytics** 페이지에서 다음을 수행 합니다.
   1. 붙여넣기 합니다 **작업 영역 ID** 하 고 **작업 영역 키 (기본 키)** 앞에서 복사한 합니다.    
    a. 컴퓨터를 Log Analytics 서비스에 프록시 서버를 통해 통신 해야 하는 경우 클릭 **고급** URL을 입력 하 고 포트 번호는 프록시 서버.  프록시 서버에 인증이 필요한 경우 사용자 이름 및 프록시 서버를 사용 하 여 인증을 클릭 한 다음 암호를 입력 **다음**합니다.  
7. 클릭 **다음** 필요한 구성 설정 제공을 완료 합니다.<br><br> ![작업 영역 ID 및 기본 키를 붙여 넣습니다.](media/configure-azure-monitor/log-analytics-mma-setup-laworkspace.png)<br><br>
8. 에 **설치할 준비가** 페이지에서 선택 내용을 검토 하 고 클릭 **설치**합니다.
9. 에 **구성이 성공적으로 완료** 페이지에서 클릭 **마침**합니다.

완료 되 면 합니다 **Microsoft Monitoring Agent** 나타나는 **제어판**합니다. 구성을 검토 하 고 하 고 에이전트가 Log Analytics에 연결 되어 있는지 확인 합니다. 에 연결 하는 경우는 **Azure Log Analytics** 탭에서 에이전트가 라는 메시지를 표시 합니다. **Microsoft Monitoring Agent가 Microsoft Log Analytics 서비스에 연결 했습니다.** 

![Log Analytics에 대 한 MMA 연결 상태](media/configure-azure-monitor/log-analytics-mma-laworkspace-status.png)

를 지원 되는 구성을 이해 하려면 검토 [지원 되는 Windows 운영 체제](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#supported-windows-operating-systems) 하 고 [네트워크 방화벽 구성](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/log-analytics-agent#network-firewall-requirements)합니다.

## <a name="collecting-event-and-performance-data"></a>이벤트 및 성능 데이터 수집

Log Analytics는 좀 더 긴 기간의 분석 및 보고를 지정 하는 성능 카운터 확인 하 고 Windows 이벤트 로그에서 이벤트를 수집 하 고 특정 조건이 검색 되 면 작업을 수행할 수 있습니다.  시작 하려면 Windows 이벤트 로그에서 몇 가지 일반적인 성능 카운터 이벤트의 컬렉션을 구성 하려면 다음이 단계를 따릅니다.  

1. Azure 포털에서 클릭 **더 많은 서비스** 왼쪽 아래 모서리에서 찾을 수 있습니다. 리소스 목록에서 입력 **Log Analytics**합니다. 사용자의 입력에 따라 입력을 시작 하면 목록이 필터링 됩니다. 선택 **Log Analytics**합니다.
2. 선택 **고급 설정**합니다.<br><br> ![Log Analytics 고급 설정](media/configure-azure-monitor/log-analytics-advanced-settings-01.png)<br><br> 
3. 선택 **데이터**를 선택한 후 **Windows 이벤트 로그**합니다.  
4. 여기에서 더하기 기호 클릭 이름을 아래에 입력 하 여 Health Service 이벤트 채널을 추가 **+** 합니다.  
   ```
   Event Channel: Microsoft-Windows-Health/Operational
   ```
5. 테이블의 심각도 확인 **오류** 하 고 **경고**합니다.   
6. 클릭 **저장할** 구성을 저장 하려면 페이지의 맨 위에 있는 합니다.
7. 선택 **Windows 성능 카운터** Windows 컴퓨터의 성능 카운터 수집을 사용 하도록 설정 합니다. 
8. 새 Log Analytics 작업 영역에 대 한 Windows 성능 카운터를 처음 구성할 때 몇 가지 공용 카운터를 신속 하 게 만드는 옵션이 제공 됩니다. 각 옆에 확인란과 함께 나열 됩니다.<br> ![기본 Windows 성능 카운터 선택](media/configure-azure-monitor/windows-perfcounters-default.png)<br> 클릭 **선택한 성능 카운터 추가**합니다.  추가 되며 10 초의 수집 샘플 간격으로 미리 설정 합니다.  
9. 클릭 **저장할** 구성을 저장 하려면 페이지의 맨 위에 있는 합니다.

## <a name="creating-alerts-based-on-log-data"></a>로그 데이터를 기반으로 하는 경고 만들기

만든 경우 것이 훨씬를 클러스터 해야 보낼 로그 및 성능 카운터 Log Analytics로 합니다. 다음 단계는 자동으로 정기적으로 로그 검색을 실행 하는 경고 규칙을 만드는 것입니다. 로그 검색 결과가 특정 조건과 일치 하는 경우 다음 경고가 발생 하는 전자 메일 또는 텍스트 알림을 전송 하는 합니다. 이 살펴보겠습니다 아래.

### <a name="create-a-query"></a>쿼리 만들기

로그 검색 포털을 열어 시작 합니다.   

1. Azure 포털에서 클릭 **모든 서비스**합니다. 리소스 목록에서 입력 **모니터**합니다. 사용자의 입력에 따라 입력을 시작 하면 목록이 필터링 됩니다. 선택 **모니터**합니다.
2. 모니터 탐색 메뉴에서 선택 **Log Analytics** 한 다음 작업 영역을 선택 합니다.

일부 데이터를 사용 하려면를 검색 하는 가장 빠른 방법은 테이블의 모든 레코드를 반환 하는 간단한 쿼리입니다. 검색 상자에 다음 쿼리를 입력 하 고 검색 단추를 클릭 합니다.  

```
Event
```

기본 목록 보기에 데이터가 반환 됩니다 하 고 반환 된 총 레코드 수를 볼 수 있습니다.

![단순 쿼리](media/configure-azure-monitor/log-analytics-portal-eventlist-01.png)

화면 왼쪽에서 직접 수정 하지 않고 쿼리에 필터링을 추가할 수 있는 필터 창이입니다.  레코드 형식에 대 한 몇 가지 레코드 속성이 표시 됩니다 하 고 검색 결과 범위를 좁히려면 하나 이상의 속성 값을 선택할 수 있습니다.

옆의 확인란을 선택 **오류** 아래에서 **EVENTLEVELNAME** 하거나 결과 오류 이벤트를 제한 하려면 다음을 입력 합니다.

```
Event | where (EventLevelName == "Error")
```

![Filter](media/configure-azure-monitor/log-analytics-portal-eventlist-02.png)

관심 이벤트에 대 한 적절 한 쿼리를 만든 후 다음 단계를 위해 저장 합니다.

### <a name="create-alerts"></a>경고 만들기
이제 경고를 만드는 예를 살펴보겠습니다.

1. Azure 포털에서 클릭 **모든 서비스**합니다. 리소스 목록에서 입력 **Log Analytics**합니다. 사용자의 입력에 따라 입력을 시작 하면 목록이 필터링 됩니다. 선택 **Log Analytics**합니다.
2. 왼쪽 창에서 선택 **경고** 을 클릭 한 다음 **새 경고 규칙** 새 경고를 만들려면 페이지 위쪽에서.<br><br> ![새 경고 규칙 만들기](media/configure-azure-monitor/alert-rule-02.png)<br>
3. 첫 번째 단계에 대 한 아래 합니다 **경고 만들기** 로그 기반 경고 신호 이므로 리소스로 Log Analytics 작업 영역을 선택 하려는 섹션입니다.  특정을 선택 하 여 결과 필터링 **구독** 둘 이상 이전에 만든 Log Analytics 작업 영역을 포함 하는 경우 드롭다운 목록에서.  필터를 **리소스 종류** 를 선택 하 여 **Log Analytics** 드롭 다운 목록에서.  마지막으로 선택 합니다 **리소스** **DefaultLAWorkspace** 을 클릭 한 다음 **수행**합니다.<br><br> ![경고 1 단계 작업 만들기](media/configure-azure-monitor/alert-rule-03.png)<br>
4. 섹션 **경고 조건과**, 클릭 **조건 추가** 에 저장 된 쿼리를 선택 하 고 경고 규칙을 따르는 논리를 지정 합니다.
5. 다음 정보를 사용 하 여 경고를 구성 합니다.  
   a. **에 따라** 드롭 다운 목록에서 **미터법**합니다.  메트릭 측정은 지정 된 임계값을 초과 하는 값을 사용 하 여 쿼리에서 각 개체에 대 한 경고를 만듭니다.  
   b. 에 대 한 합니다 **조건**를 선택 **보다 큰** thershold를 지정 합니다.  
   c. 경고를 트리거할 때를 정의 합니다. 예를 들어 선택할 수 있습니다 **연속 위반** 드롭다운 목록에서 선택 하 고 **보다 큰** 값 3입니다.  
   d. 아래 섹션에 따라 평가 수정 합니다 **기간** 값을 **30** 분 및 **빈도** 5. 규칙은 5 분 마다 실행 되며 현재 시간에서 지난 30 분 이내에 생성 된 레코드를 반환 합니다.  더 광범위 한 창에 기간 설정 데이터 대기 시간, 가능성에 대 한 계정 및 쿼리는 경고가 발생 하지 않습니다 방지 거짓 부정에 데이터를 반환 하면 합니다.  
6. 클릭 **수행** 경고 규칙을 완료 합니다.<br><br> ![경고 신호를 구성 합니다.](media/configure-azure-monitor/alert-signal-logic-02.png)<br> 
7. 경고의 이름을 이제 두 번째 단계를 진행 합니다 **경고 규칙 이름** 와 같은 필드 **모든 오류 이벤트에 대 한 경고**합니다.  지정를 **설명을** 선택한 경고에 대 한 세부 사항을 자세히 **위험 (심각도 0)** 에 대 한 합니다 **심각도** 제공 하는 옵션의 값입니다.
8. 경고 생성 규칙을 즉시 활성화 하려면에 대 한 기본값을 그대로 **활성화 규칙을 만들면**합니다.
9. 세 번째이자 마지막 단계 지정는 **작업 그룹**, 동일한 작업 경고가 트리거되고 정의한 각 규칙에 사용할 수 있습니다 각 시간에 수행 되는 확인 하는 합니다. 다음 정보를 사용 하 여 새 작업 그룹을 구성 합니다.  
   a. 선택 **새 작업 그룹** 하며 **작업 그룹 추가** 창이 나타납니다.  
   b. 에 대 한 **작업 그룹 이름**와 같은 이름을 **IT 운영-알림** 및 **약식 이름** 와 같은 **itops n**합니다.  
   c. 기본 값을 확인 **구독** 하 고 **리소스 그룹** 올바릅니다. 그러지 않으면 드롭다운 목록에서 올바른 항목을 선택 합니다.   
   d. 작업 섹션에서 이름을 동작의 경우와 같은 **전자 메일 보내기** 아래에서 **동작 유형** 선택 **이메일/S/푸시/음성** 드롭 다운 목록에서. 합니다 **전자 메일/S/푸시/음성** 추가 정보를 제공 하기 위해 오른쪽 속성 창에서 열립니다.  
   e. 에 **전자 메일/S/푸시/음성** 창 선택 하 고 기본 설정을 설정 합니다. 예를 들어, 사용 하도록 설정 **전자 메일** 유효한 전자 메일 메시지를 전달할 SMTP 주소를 제공 합니다.  
   f. **확인** 을 클릭하여 변경 내용을 저장합니다.<br><br> 

    ![새 작업 그룹 만들기](media/configure-azure-monitor/action-group-properties-01.png)

10. 클릭 **확인** 작업 그룹을 완료 합니다. 
11. 클릭 **경고 규칙 만들기** 경고 규칙을 완료 합니다. 실행을 즉시 시작 합니다.<br><br> ![새 경고 규칙 만들기 완료](media/configure-azure-monitor/alert-rule-01.png)<br> 

### <a name="test-alerts"></a>테스트 경고

참조에 대 한 경고 예제의 모양은 다음과 같습니다.

![경고 전자 메일 예](media/configure-azure-monitor/warning.png)

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트 개요](storage-spaces-direct-overview.md)
- 자세한 내용은 읽기를 [Azure Monitor 설명서](https://docs.microsoft.com/en-us/azure/azure-monitor/learn/tutorial-viewdata)합니다.
