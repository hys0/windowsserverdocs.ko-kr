---
title: 기능 관리
description: 시스템 정보는 다양 한 각 기능에 대해 구성할 수 있는 설정 및 이러한 설정은 특정 배포의 주소를 조정할 수 있습니다. 이 항목에서는 Windows Admin Center 또는 PowerShell에 기본 PowerShell 예제 및 이러한 설정을 조정 하는 방법을 보여 주기 위해 Windows Admin Center 스크린 샷을 제공을 통해 각 기능에 대 한 다양 한 설정을 관리 하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: 9081a0b576ab9871b47df38255047b6cbe889419
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868024"
---
# <a name="managing-capabilities"></a>기능 관리

>적용 대상: Windows Server 2019

Windows Server 2019에서 시스템 정보는 다양 한 각 기능에 대해 구성할 수 있는 설정 하 고 특정 배포의 주소를 이러한 설정을 조정할 수 있습니다. 이 항목에서는 Windows Admin Center 또는 PowerShell에 기본 PowerShell 예제 및 이러한 설정을 조정 하는 방법을 보여 주기 위해 Windows Admin Center 스크린 샷을 제공을 통해 각 기능에 대 한 다양 한 설정을 관리 하는 방법을 설명 합니다. 

>[!TIP]
>또한 시작 하 고 자신 있게 시스템 정보를 관리 하는 데 이러한 짧은 비디오를 사용할 수 있습니다. [10 분 후에 시스템 정보를 사용 하 여 시작](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

사용할 수 있지만이 섹션에서는 PowerShell 예제는 [시스템 Insights PowerShell 설명서](https://aka.ms/systeminsightspowershell) 시스템 Insights 내에서 cmdlet, 매개 변수 및 매개 변수 집합을 모두 보려면. 

## <a name="viewing-capabilities"></a>기능 보기

시작 하려면 사용 하 여 사용할 수 있는 기능을 모두 나열할 수 있습니다 합니다 **Get InsightsCapability** cmdlet: 

```PowerShell
Get-InsightsCapability
``` 
이러한 기능에도 시스템 Insights 확장에 표시 됩니다.

![사용 가능한 기능을 나열 하는 시스템 Insights의 개요 페이지](media/overview-page-contoso.png)

## <a name="enabling-and-disabling-a-capability"></a>설정 및 기능을 사용 하지 않도록 설정
각 기능을 활성화 또는 비활성화할 수 있습니다. 해당 기능 호출할 되지 못하도록 하는 기능을 사용 하지 않도록 설정 하 고 기본이 아닌 기능에 대 한 해당 기능에 대 한 모든 데이터 수집을 중지 하는 기능을 사용 하지 않도록 설정 합니다. 기본적으로 모든 기능이 활성화 되 고 사용 하 여 기능 상태를 확인할 수 있습니다 합니다 **Get InsightsCapability** cmdlet. 

를 사용 하도록 설정 하거나 기능을 사용 하지 않도록 설정 합니다 **사용 InsightsCapability** 및 **사용 안 함-InsightsCapability** cmdlet:

```PowerShell
Enable-InsightsCapability -Name "CPU capacity forecasting"
Disable-InsightsCapability -Name "Networking capacity forecasting"
``` 
이러한 설정을 전환할 수도 있습니다 Windows Admin Center 클릭에서 선택한 기능을 합니다 **을 사용 하도록 설정** 또는 **사용 하지 않도록 설정** 단추입니다.

### <a name="invoking-a-capability"></a>기능을 호출합니다.
예측을 검색 하는 기능을 실행 하는 기능을 즉시 호출 및 관리자 수 기능을 언제 든 지 클릭 하 여 호출할 합니다 **Invoke** Windows Admin Center 사용 하 여 단추는  **호출 InsightsCapability** cmdlet:

```PowerShell
Invoke-InsightsCapability -Name "CPU capacity forecasting"
```

>[!TIP]
>컴퓨터에 중요 한 작업을 사용 하 여 충돌 하지 기능을 호출 하려면 예측 끄기 업무 시간 동안 예약 하는 것이 좋습니다.

## <a name="retrieving-capability-results"></a>기능 결과 검색합니다.
가장 최근의 결과가 표시를 사용 하는 기능을가 호출 되 면 **Get InsightsCapability** 하거나 **Get InsightsCapabilityResult**합니다. 이러한 cmdlet 출력 가장 최근의 **상태** 하 고 **상태 설명을** 각 예측의 결과 설명 하는 각 기능의 합니다. **상태** 및 **상태 설명을** 필드에 추가로 나와 합니다 [이해 기능 문서](understanding-capabilities.md)합니다. 

또한 사용할 수는 **Get InsightsCapabilityResult** 예측과 연관 데이터를 검색할 마지막 30 예측 결과 보려면 cmdlet: 

```PowerShell
# Specify the History parameter to see the last 30 prediction results.
Get-InsightsCapabilityResult -Name "CPU capacity forecasting" -History

# Use the Output field to locate and then show the results of "CPU capacity forecasting."
# Specify the encoding as UTF8, so that Get-Content correctly parses non-English characters.
$Output = Get-Content (Get-InsightsCapabilityResult -Name "CPU capacity forecasting").Output -Encoding UTF8 | ConvertFrom-Json
$Output.ForecastingResults
```
자동으로 시스템 Insights 확장을 예측 기록을 표시 하 고 각 예측의 직관적이 고 충실도 높은 그래프를 제공 하는 JSON 결과의 결과 구문 분석:

![예측 그래프 및 예측 기록을 보여 주는 단일 기능 페이지](media/cpu-forecast-2.png)

### <a name="using-the-event-log-to-retrieve-capability-results"></a>이벤트 로그를 사용 하 여 기능 결과 검색 합니다.
시스템 정보 기능을 예측 완료 될 때마다 이벤트를 기록 합니다. 이러한 이벤트에 표시 되는 **-Windows-시스템-Insightsm/** 채널 및 시스템 정보 게시 각 상태에 대 한 다른 이벤트 ID:   

| 예측 상태 | 이벤트 ID |
| --------------- | --------------- |
| 확인 | 151 |
| 경고 | 148 |
| 심각 | 150 |
| Error | 149 |
| 없음 | 132 |

>[!TIP]
>사용 하 여 [Azure Monitor](https://azure.microsoft.com/services/monitor/) 하거나 [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) 이러한 이벤트를 집계 하 여 그룹 컴퓨터에 예측 결과 참조 하세요.


## <a name="setting-a-capability-schedule"></a>기능 일정 설정
주문형으로 예측 하는 것 외에도 지정 된 기능 미리 정의 된 일정에 따라 자동으로 호출 됩니다 있도록 각 기능에 대 한 주기적인 예측을 구성할 수 있습니다. 사용 된 **Get InsightsCapabilitySchedule** cmdlet 기능 일정을: 

>[!TIP]
>반환 하는 모든 기능에 대 한 정보를 확인 하려면 PowerShell에서 파이프라인 연산자를 사용 합니다 **Get InsightsCapability** cmdlet.

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilitySchedule
```

정기적인 예측은 언제 든 지 사용할 수 있지만 기본적으로 활성화 됩니다 합니다 **사용 InsightsCapabilitySchedule** 및 **사용 안 함-InsightsCapabilitySchedule** cmdlet:

```PowerShell
Enable-InsightsCapabilitySchedule -Name "Total storage consumption forecasting"
Disable-InsightsCapabilitySchedule -Name "Volume consumption forecasting"
```

각 기본 기능 매일 오전 3 시에 실행 되도록 예약 됩니다. 그러나 각 기능에 대 한 사용자 지정 일정을 만들 수 있습니다 및 시스템 Insights는 다양 한 일정 유형 사용 하 여 구성할 수 있는 지원 합니다 **집합 InsightsCapabilitySchedule** cmdlet: 

```PowerShell
Set-InsightsCapabilitySchedule -Name "CPU capacity forecasting" -Daily -DaysInterval 2 -At 4:00PM
Set-InsightsCapabilitySchedule -Name "Networking capacity forecasting" -Daily -DaysOfWeek Saturday, Sunday -At 2:30AM
Set-InsightsCapabilitySchedule -Name "Total storage consumption forecasting" -Hourly -HoursInterval 2 -DaysOfWeek Monday, Wednesday, Friday
Set-InsightsCapabilitySchedule -Name "Volume consumption forecasting" -Minute -MinutesInterval 30 
```
>[!NOTE]
>일일 데이터를 분석 하는 기본 기능을 하기 때문에 것이 좋습니다 이러한 기능에 대 한 일별 일정을 사용 하도록 합니다. 기본 기능에 자세히 알아보려면 [여기](understanding-capabilities.md)합니다.

보고 클릭 하 여 각 기능에 대 한 일정을 설정 하려면 Windows Admin Center 사용할 수도 있습니다 **설정을**합니다. 현재 일정에 표시 되는 **일정** 탭에 새 일정을 만들려면 GUI 도구를 사용할 수 있습니다.

![설정을 보여 주는 현재 일정 페이지](media/schedule-page-contoso.png)

## <a name="creating-remediation-actions"></a>수정 작업 만들기
시스템 정보를 사용 하면 기능을의 결과 기반으로 하는 사용자 지정 수정 스크립트를 시작할 수 있습니다. 각 기능에 대 한 관리자가 수동 개입이 필요 하는 대신 자동으로 수정 작업을 수행할 수 있도록 각 예측 상태에 대 한 사용자 지정 PowerShell 스크립트를 구성할 수 있습니다. 

샘플 수정 작업에는 중복 제거를 실시간으로 Vm을 마이그레이션하고 Azure File Sync 설정 실행 중 볼륨 확장, 디스크 정리를 실행 포함 됩니다.

사용 하 여 각 기능에 대 한 작업을 확인할 수는 **Get InsightsCapabilityAction** cmdlet:

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilityAction
```

새 작업 만들기 또는 삭제를 사용 하 여 기존 작업 수를 **집합 InsightsCapabilityAction** 및 **제거 InsightsCapabilityAction** cmdlet. 각 작업에 지정 된 자격 증명을 사용 하 여 실행 되는 **ActionCredential** 매개 변수입니다.

>[!NOTE]
>초기 시스템 Insights 릴리스에서 사용자 디렉터리 외부에서 수정 스크립트를 지정 해야 합니다. 이 향후 릴리스에서 수정 될 예정입니다.

```PowerShell
$Cred = Get-Credential
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning -Action "C:\Users\Public\WarningScript.ps1" -ActionCredential $Cred
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Critical -Action "C:\Users\Public\CriticalScript.ps1" -ActionCredential $Cred

Remove-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning
```

사용 하 여 수정 작업을 설정 하려면 Windows Admin Center 사용할 수도 있습니다는 **작업** 내에서 탭의 **설정** 페이지:

![사용자 수정 작업을 지정할 수 있는 설정 페이지](media/actions-page-contoso.png)


## <a name="see-also"></a>참조
시스템 정보에 대 한 자세한 내용은 다음 리소스를 사용 합니다.

- [시스템 Insights 개요](overview.md)
- [이해 기능](understanding-capabilities.md)
- [추가 및 기능 개발](adding-and-developing-capabilities.md)
- [System Insights FAQ](faq.md)