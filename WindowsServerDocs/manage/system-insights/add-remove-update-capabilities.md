---
title: 기능 추가, 제거 및 업데이트
description: 시스템 정보를 사용 하면 기존 데이터 수집 및 관리 기능을 활용 하는 새로운 기능을 만들 수 있습니다. 플랫폼 지원 추가, 제거 및 이러한 기능의 업데이트를 관리할 수도 있는 것입니다. 이 항목에서는 추가, 제거 및 시스템 Insights의 기능을 업데이트 하는 고급 기능을 설명 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 07fb036d1c4aa4a63107594ec1f81cb5be1c7724
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880164"
---
# <a name="adding-removing-and-updating-capabilities"></a>기능 추가, 제거 및 업데이트

>적용 대상: Windows Server 2019

시스템 정보를 사용 하면 기존 데이터 수집 및 관리 기능을 활용 하는 새로운 기능을 만들 수 있습니다. 하지만 이러한 기능을 만들면 반드시 동일 하 게 있다는 것도 추가, 제거 및 이러한 기능의 업데이트를 관리 하는 플랫폼 지원 합니다. 

이 항목에서는 추가, 제거 및 시스템 Insights의 기능을 업데이트 하는 고급 기능을 설명 합니다. 

## <a name="adding-a-capability"></a>기능을 추가합니다.
시스템 정보를 사용 하면 언제 든 지 사용 하 여 새 기능을 추가 하는 **추가 InsightsCapability** cmdlet. 합니다 **추가 InsightsCapability** 기능 이름과 기능 라이브러리를 지정 해야 합니다. 기능 라이브러리 기능 설명, 데이터 원본 및 예측 논리를 포함합니다.

```PowerShell
Add-InsightsCapability -Name "Sample capability" -Library "C:\SampleCapability.dll"
```

기능을 시스템 Insights를 추가한 후 즉시 호출 고 PowerShell 또는 Windows Admin Center 사용 하 여 기능을 관리할 수 있습니다. 

## <a name="updating-a-capability"></a>기능 업데이트
시스템 Insights 있습니다 사용 하 여 기능 업데이트를 **업데이트 InsightsCapability** cmdlet.

```PowerShell
Update-InsightsCapability -Name "Sample capability" -Library "C:\SampleCapabilityv2.dll"
```

기능 업데이트를 사용 하면 기능 설명, 데이터 원본 및 해당 기능을 사용 하 여 연결 하는 예측 논리를 변경할 수 있는 새 기능 라이브러리를 지정할 수 있습니다. 모든 구성 및 사용자 지정 일정, 작업 및 기록 예측 결과 포함 하 여 해당 기능에 대 한 기록 정보 뿐만 아니라 유지 기능을 업데이트 합니다. 

## <a name="removing-a-capability"></a>기능 제거
시스템 정보를 사용 하 여 기능을 제거할 수도 있습니다는 **제거 InsightsCapability** cmdlet. 

```PowerShell
Remove-InsightsCapability -Name "Sample capability" 
```
>[!NOTE]
>기본 예측 기능을 제거할 수 없습니다.

기능 및 일정, 모든 재구성 작업 및 지난 예측 결과 포함 하 여 연결 된 모든 내용은 삭제 기능을 영구적으로 제거 합니다. 

>[!TIP]
>이러한 경우에 기능을 사용 하 여 연결 된 모든 정보를 영구적으로 삭제 하는 방법에 대 한 제거 하는 것이 아니라 기능을 사용 하지 않도록 설정 하는 것이 좋습니다. 

## <a name="see-also"></a>참조
시스템 정보에 대 한 자세한 내용은 다음 리소스를 사용 합니다.

- [시스템 Insights 개요](overview.md)
- [이해 기능](understanding-capabilities.md)
- [관리 기능](managing-capabilities.md)
- [추가 및 기능 개발](adding-and-developing-capabilities.md)
- [System Insights FAQ](faq.md)