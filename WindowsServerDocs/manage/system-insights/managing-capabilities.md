---
title: 기능 관리
description: System Insights는 각 기능에 대해 구성할 수 있는 다양 한 설정을 제공 하며, 이러한 설정을 조정 하 여 배포의 특정 요구 사항을 해결할 수 있습니다. 이 항목에서는 Windows 관리 센터 또는 PowerShell을 통해 각 기능에 대 한 다양 한 설정을 관리 하는 방법에 대해 설명 합니다. 이러한 설정을 조정 하는 방법을 설명 하는 기본 PowerShell 예제 및 Windows 관리 센터 스크린샷을 제공 합니다.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: b93365474e591ce6fde59867c42b851ec45de50c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80819736"
---
# <a name="managing-capabilities"></a>기능 관리

>적용 대상: Windows Server 2019

Windows Server 2019에서 System Insights는 각 기능에 대해 구성할 수 있는 다양 한 설정을 제공 하며, 이러한 설정을 조정 하 여 배포의 특정 요구 사항을 해결할 수 있습니다. 이 항목에서는 Windows 관리 센터 또는 PowerShell을 통해 각 기능에 대 한 다양 한 설정을 관리 하는 방법에 대해 설명 합니다. 이러한 설정을 조정 하는 방법을 설명 하는 기본 PowerShell 예제 및 Windows 관리 센터 스크린샷을 제공 합니다. 

>[!TIP]
>또한 다음과 같은 짧은 비디오를 사용 하 여 시스템 정보를 시작 하 고 안전 하 게 관리할 수 있습니다. [10 분 안에 System insights 시작](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

이 섹션에서는 PowerShell 예제를 제공 하지만 system insights [powershell 설명서](https://aka.ms/systeminsightspowershell) 를 사용 하 여 시스템 정보에서 모든 cmdlet, 매개 변수 및 매개 변수 집합을 볼 수 있습니다. 

## <a name="viewing-capabilities"></a>기능 보기

시작 하려면 **InsightsCapability** cmdlet을 사용 하 여 사용 가능한 모든 기능을 나열할 수 있습니다. 

```PowerShell
Get-InsightsCapability
``` 
이러한 기능은 System Insights 확장에도 표시 됩니다.

![사용 가능한 기능을 나열 하는 System Insights 개요 페이지](media/overview-page-contoso.png)

## <a name="enabling-and-disabling-a-capability"></a>기능 사용 및 사용 안 함
각 기능을 사용 하거나 사용 하지 않도록 설정할 수 있습니다. 기능을 사용 하지 않도록 설정 하면 해당 기능이 호출 되지 않으며 기본이 아닌 기능에 대 한 기능을 사용 하지 않도록 설정 하면 해당 기능에 대 한 모든 데이터 컬렉션이 중지 됩니다. 기본적으로 모든 기능을 사용할 수 있으며 **InsightsCapability** cmdlet을 사용 하 여 기능의 상태를 확인할 수 있습니다. 

기능을 사용 하거나 사용 하지 않도록 설정 하려면 **InsightsCapability** 및 **InsightsCapability** cmdlet을 사용 합니다.

```PowerShell
Enable-InsightsCapability -Name "CPU capacity forecasting"
Disable-InsightsCapability -Name "Networking capacity forecasting"
``` 
Windows 관리 센터에서 기능을 선택 하 고 **사용** 또는 **사용 안 함** 단추를 클릭 하 여 이러한 설정을 전환할 수도 있습니다.

### <a name="invoking-a-capability"></a>기능 호출
기능을 즉시 호출 하 여 예측을 검색 하면 관리자가 Windows 관리 센터에서 [ **호출** ] 단추를 클릭 하거나 **InsightsCapability** cmdlet을 사용 하 여 언제 든 지 기능을 호출할 수 있습니다.

```PowerShell
Invoke-InsightsCapability -Name "CPU capacity forecasting"
```

>[!TIP]
>기능 호출이 컴퓨터의 중요 한 작업과 충돌 하지 않도록 하려면 업무 외 시간에 예측 일정을 예약 하는 것이 좋습니다.

## <a name="retrieving-capability-results"></a>기능 결과 검색
기능이 호출 된 후에는 **InsightsCapability** 또는 **InsightsCapabilityResult**를 사용 하 여 최신 결과를 볼 수 있습니다. 이러한 cmdlet은 각 예측의 결과를 설명 하는 각 기능에 대 한 최신 **상태** 및 **상태 설명을** 출력 합니다. **상태** 및 **상태 설명** 필드는 [기능 이해 문서](understanding-capabilities.md)에 자세히 설명 되어 있습니다. 

또한 **InsightsCapabilityResult** cmdlet을 사용 하 여 최근 30 개의 예측 결과를 보고 예측과 관련 된 데이터를 검색할 수 있습니다. 

```PowerShell
# Specify the History parameter to see the last 30 prediction results.
Get-InsightsCapabilityResult -Name "CPU capacity forecasting" -History

# Use the Output field to locate and then show the results of "CPU capacity forecasting."
# Specify the encoding as UTF8, so that Get-Content correctly parses non-English characters.
$Output = Get-Content (Get-InsightsCapabilityResult -Name "CPU capacity forecasting").Output -Encoding UTF8 | ConvertFrom-Json
$Output.ForecastingResults
```
시스템 정보 확장은 자동으로 예측 기록을 표시 하 고 JSON 결과의 결과를 구문 분석 하 여 각 예측에 대 한 직관적이 고 충실도 그래프를 제공 합니다.

![예측 그래프 및 예측 기록을 보여 주는 단일 기능 페이지](media/cpu-forecast-2.png)

### <a name="using-the-event-log-to-retrieve-capability-results"></a>이벤트 로그를 사용 하 여 기능 결과 검색
시스템 정보는 기능이 예측을 완료할 때마다 이벤트를 기록 합니다. 이러한 이벤트는 **Microsoft-Windows-시스템-정보/관리** 채널에서 볼 수 있으며, System Insights는 각 상태에 대해 다른 이벤트 ID를 게시 합니다.   

| 예측 상태 | 이벤트 ID |
| --------------- | --------------- |
| 확인 | 151 |
| 경고 | 148 |
| 중요 | 150 |
| 오류 | 149 |
| 없음 | 132 |

>[!TIP]
>[Azure Monitor](https://azure.microsoft.com/services/monitor/) 또는 [System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807) 를 사용 하 여 이러한 이벤트를 집계 하 고 컴퓨터 그룹에서 예측 결과를 확인 합니다.


## <a name="setting-a-capability-schedule"></a>기능 일정 설정
요청 시 예측 외에도 지정 된 기능이 미리 정의 된 일정에 따라 자동으로 호출 되도록 각 기능에 대 한 주기적인 예측을 구성할 수 있습니다. **InsightsCapabilitySchedule** cmdlet을 사용 하 여 기능 일정을 확인 합니다. 

>[!TIP]
>PowerShell에서 파이프라인 연산자를 사용 하 여 **InsightsCapability** cmdlet에서 반환 되는 모든 기능에 대 한 정보를 볼 수 있습니다.

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilitySchedule
```

정기적 예측은 **InsightsCapabilitySchedule** 및 **InsightsCapabilitySchedule** cmdlet을 사용 하 여 언제 든 지 비활성화할 수 있지만 기본적으로 사용 하도록 설정 되어 있습니다.

```PowerShell
Enable-InsightsCapabilitySchedule -Name "Total storage consumption forecasting"
Disable-InsightsCapabilitySchedule -Name "Volume consumption forecasting"
```

각 기본 기능은 매일 오전 3 시에 실행 되도록 예약 됩니다. 그러나 각 기능에 대해 사용자 지정 일정을 만들 수 있으며, System Insights는 **InsightsCapabilitySchedule** cmdlet을 사용 하 여 구성할 수 있는 다양 한 일정 유형을 지원 합니다. 

```PowerShell
Set-InsightsCapabilitySchedule -Name "CPU capacity forecasting" -Daily -DaysInterval 2 -At 4:00PM
Set-InsightsCapabilitySchedule -Name "Networking capacity forecasting" -Daily -DaysOfWeek Saturday, Sunday -At 2:30AM
Set-InsightsCapabilitySchedule -Name "Total storage consumption forecasting" -Hourly -HoursInterval 2 -DaysOfWeek Monday, Wednesday, Friday
Set-InsightsCapabilitySchedule -Name "Volume consumption forecasting" -Minute -MinutesInterval 30 
```
>[!NOTE]
>기본 기능은 일일 데이터를 분석 하므로 이러한 기능에 매일 일정을 사용 하는 것이 좋습니다. 기본 기능에 대 한 자세한 내용은 [여기](understanding-capabilities.md)를 참조 하세요.

Windows 관리 센터를 사용 하 여 **설정**을 클릭 하 여 각 기능에 대 한 일정을 보고 설정할 수도 있습니다. 현재 일정이 **일정** 탭에 표시 되 고 GUI 도구를 사용 하 여 새 일정을 만들 수 있습니다.

![현재 일정을 보여 주는 설정 페이지](media/schedule-page-contoso.png)

## <a name="creating-remediation-actions"></a>수정 작업 만들기
System Insights를 사용 하면 기능 결과에 따라 사용자 지정 재구성 스크립트를 시작할 수 있습니다. 각 기능에 대해 각 예측 상태에 대해 사용자 지정 PowerShell 스크립트를 구성 하 여 관리자가 수동 작업을 요구 하지 않고 자동으로 수정 작업을 수행할 수 있도록 합니다. 

샘플 수정 작업으로는 디스크 정리 실행, 볼륨 확장, 중복 제거 실행, Vm 실시간 마이그레이션, Azure File Sync 설정 등이 있습니다.

**InsightsCapabilityAction** cmdlet을 사용 하 여 각 기능에 대 한 작업을 볼 수 있습니다.

```PowerShell
Get-InsightsCapability | Get-InsightsCapabilityAction
```

**InsightsCapabilityAction** 및 **InsightsCapabilityAction** cmdlet을 사용 하 여 새 작업을 만들거나 기존 작업을 삭제할 수 있습니다. 각 작업은 **Actioncredential** 매개 변수에 지정 된 자격 증명을 사용 하 여 실행 됩니다.

>[!NOTE]
>초기 시스템 정보 릴리스에는 사용자 디렉터리 외부에서 재구성 스크립트를 지정 해야 합니다. 이 문제는 향후 릴리스에서 수정 될 예정입니다.

```PowerShell
$Cred = Get-Credential
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning -Action "C:\Users\Public\WarningScript.ps1" -ActionCredential $Cred
Set-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Critical -Action "C:\Users\Public\CriticalScript.ps1" -ActionCredential $Cred

Remove-InsightsCapabilityAction -Name "CPU capacity forecasting" -Type Warning
```

또한 **설정** 페이지에서 **작업** 탭을 사용 하 여 수정 작업을 설정 하는 데 Windows 관리 센터를 사용할 수 있습니다.

![사용자가 수정 작업을 지정할 수 있는 설정 페이지](media/actions-page-contoso.png)


## <a name="see-also"></a>참고 항목
시스템 정보에 대 한 자세한 내용을 보려면 다음 리소스를 사용 하세요.

- [시스템 정보 개요](overview.md)
- [기능 이해](understanding-capabilities.md)
- [기능 추가 및 개발](adding-and-developing-capabilities.md)
- [시스템 정보 FAQ](faq.md)