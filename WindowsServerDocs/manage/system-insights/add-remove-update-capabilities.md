---
title: 기능 추가, 제거 및 업데이트
description: System Insights를 사용 하면 기존 데이터 컬렉션 및 관리 기능을 활용 하는 새로운 기능을 만들 수 있습니다. 이러한 기능의 추가, 제거 및 업데이트를 관리 하는 플랫폼 지원도 있어야 합니다. 이 항목에서는 System Insights에서 기능을 추가, 제거 및 업데이트 하는 고급 기능에 대해 설명 합니다.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 0a760f25de79bc89b2aa67aec6bb1e3a493c1310
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856266"
---
# <a name="adding-removing-and-updating-capabilities"></a>기능 추가, 제거 및 업데이트

>적용 대상: Windows Server 2019

System Insights를 사용 하면 기존 데이터 컬렉션 및 관리 기능을 활용 하는 새로운 기능을 만들 수 있습니다. 그러나 이러한 기능을 만든 후에는 이러한 기능에 대 한 추가, 제거 및 업데이트를 관리 하는 플랫폼 지원도 동일 해야 합니다. 

이 항목에서는 System Insights에서 기능을 추가, 제거 및 업데이트 하는 고급 기능에 대해 설명 합니다. 

## <a name="adding-a-capability"></a>기능 추가
System Insights를 사용 하면 **InsightsCapability** cmdlet을 사용 하 여 언제 든 지 새로운 기능을 추가할 수 있습니다. **InsightsCapability** 는 기능 이름 및 기능 라이브러리를 지정 해야 합니다. 기능 라이브러리에는 기능 설명, 데이터 원본 및 예측 논리가 포함 되어 있습니다.

```PowerShell
Add-InsightsCapability -Name Sample capability -Library C:\SampleCapability.dll
```

기능이 System Insights에 추가 된 후 PowerShell 또는 Windows 관리 센터를 사용 하 여 기능을 즉시 호출 하 고 관리할 수 있습니다. 

## <a name="updating-a-capability"></a>기능 업데이트
또한 System Insights를 사용 하면 **InsightsCapability** cmdlet을 사용 하 여 기능을 업데이트할 수 있습니다.

```PowerShell
Update-InsightsCapability -Name Sample capability -Library C:\SampleCapabilityv2.dll
```

기능을 업데이트 하면 기능 설명, 데이터 원본 및 해당 기능과 관련 된 예측 논리를 변경할 수 있는 새 기능 라이브러리를 지정할 수 있습니다. 중요 한 점은 기능을 업데이트 하면 사용자 지정 일정, 작업 및 기록 예측 결과를 포함 하 여 해당 기능에 대 한 모든 구성 및 기록 정보가 유지 됩니다. 

## <a name="removing-a-capability"></a>기능 제거
**InsightsCapability** cmdlet을 사용 하 여 시스템 정보에서 기능을 제거할 수도 있습니다. 

```PowerShell
Remove-InsightsCapability -Name Sample capability 
```
>[!NOTE]
>기본 예측 기능은 제거할 수 없습니다.

기능을 제거 하면 해당 기능과 모든 관련 정보 (일정, 수정 작업 및 과거 예측 결과 포함)가 영구적으로 삭제 됩니다. 

>[!TIP]
>기능과 관련 된 모든 정보를 영구적으로 삭제 하는 것에 대해 걱정 하는 경우 기능을 제거 하는 대신 사용 하지 않도록 설정 하는 것이 

## <a name="see-also"></a>참고 항목
시스템 정보에 대 한 자세한 내용을 보려면 다음 리소스를 사용 하세요.

- [시스템 정보 개요](overview.md)
- [기능 이해](understanding-capabilities.md)
- [기능 관리](managing-capabilities.md)
- [기능 추가 및 개발](adding-and-developing-capabilities.md)
- [시스템 정보 FAQ](faq.md)