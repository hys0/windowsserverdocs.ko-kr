---
title: 기능 추가 및 개발
description: 시스템 정보를 사용 하면 모든 OS 업데이트를 요구 하지 않고 시스템 Insights에 새로운 예측 기능을 추가할 수 있습니다. 이 통해 Microsoft 및 제 삼자에 게 제공 하는 중요 한 시나리오를 해결 하기 위해 새 기능 중간 릴리스를 포함 하 여 개발자. 새로운 기능 사용자 지정 데이터를 수집 및 분석을 지정 하 고 기존 시스템 Insights 관리 평면와도 통합.
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
ms.openlocfilehash: 8caddead774ac69a38906f3c0a0d2eaf005c1d28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817484"
---
# <a name="adding-and-developing-new-capabilities"></a>추가 및 새 기능 개발

>적용 대상: Windows Server 2019

시스템 정보를 사용 하면 모든 OS 업데이트를 요구 하지 않고 시스템 Insights에 새로운 예측 기능을 추가할 수 있습니다. 이 통해 Microsoft 및 제 삼자에 게 제공 하는 중요 한 시나리오를 해결 하기 위해 새 기능 중간 릴리스를 포함 하 여 개발자. 

새 기능이 통합 하 고 기존 시스템 Insights 인프라를 확장할 수 있습니다.

- 새로운 기능 수 **성능 카운터 또는 시스템 이벤트를 지정**는 수집, 로컬로 유지 되며 기능이 호출 될 때 분석을 위한 기능을 반환 합니다.  
- 새로운 기능 수 **기존 Windows Admin Center 및 PowerShell 관리 평면 활용할**합니다. 뿐만 아니라 새로운 기능 정보 시스템에서에서 검색할 수는, 사용자 지정 일정 수정 작업에서 얻을 수 있습니다. 

## <a name="manage-new-capabilities"></a>새로운 기능 관리
- [에 대해 알아봅니다](add-remove-update-capabilities.md) 추가, 제거 및 PowerShell을 사용 하 여 기능을 업데이트 하는 방법입니다. 

## <a name="develop-a-capability"></a>기능 개발
사용 하는 데 다음 리소스를 사용자 고유의 사용자 지정 기능을 작성 하기 시작 합니다.
- [에 대해 알아봅니다](data-sources.md) 수집할 수 있습니다 하는 데이터 원본에 대 한 합니다.
- [다운로드](https://www.nuget.org/packages/Microsoft.WindowsServer.SystemInsights/) 클래스 및 기능을 작성 해야 하는 인터페이스를 포함 하는 시스템 Insights NuGet 패키지.
- [방문](https://aka.ms/systeminsights-api) 시스템 Insights 클래스 및 인터페이스에 대해 자세히 알아보려면 API 설명서입니다. 
- [사용 하 여](https://aka.ms/systeminsights-samplecapability) 수 있도록 시스템 Insights 샘플 기능 시작 합니다. 이 기능을 등록, 수집, 데이터 원본을 지정할 시스템 데이터 분석을 시작 하는 방법을 보여줍니다.

>[!NOTE]
>이 시험판 기능입니다. 새 기능을 추가 하 고 피드백을 통합 하는 대로 변경 될 수는 있습니다.

## <a name="see-also"></a>참조
시스템 정보에 대 한 자세한 내용은 다음 리소스를 사용 합니다.

- [시스템 Insights 개요](overview.md)
- [이해 기능](understanding-capabilities.md)
- [관리 기능](managing-capabilities.md)
- [추가, 제거 및 기능 업데이트](add-remove-update-capabilities.md)
- [System Insights FAQ](faq.md)