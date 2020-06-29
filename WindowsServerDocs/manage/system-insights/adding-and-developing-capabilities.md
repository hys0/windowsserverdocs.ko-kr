---
title: 기능 추가 및 개발
description: System Insights를 사용 하면 OS를 업데이트할 필요 없이 시스템 정보에 새로운 예측 기능을 추가할 수 있습니다. 이를 통해 개발자는 Microsoft 및 타사를 비롯 한 새로운 기능을 만들고 제공 하 여 관심 있는 시나리오를 해결할 수 있습니다. 새 기능은 수집 및 분석을 위해 사용자 지정 데이터를 지정할 수 있으며, 기존 System Insights 관리 평면과도 통합 됩니다.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 891edb108bc2c298c70b29c596fb8d0ca0e06b7e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475190"
---
# <a name="adding-and-developing-new-capabilities"></a>새 기능 추가 및 개발

>적용 대상: Windows Server 2019

System Insights를 사용 하면 OS를 업데이트할 필요 없이 시스템 정보에 새로운 예측 기능을 추가할 수 있습니다. 이를 통해 개발자는 Microsoft 및 타사를 비롯 한 새로운 기능을 만들고 제공 하 여 관심 있는 시나리오를 해결할 수 있습니다.

새 기능은 기존 System Insights 인프라와 통합 하 고 확장할 수 있습니다.

- 새 기능은 수집 되 고 로컬로 유지 되며 기능이 호출 될 때 분석을 위해 반환 되는 **성능 카운터 또는 시스템 이벤트를 지정할**수 있습니다.
- 새 기능은 **기존 Windows 관리 센터 및 PowerShell 관리 평면을 활용할**수 있습니다. 새 기능은 System Insights에서 검색할 수 있을 뿐만 아니라 사용자 지정 일정 및 수정 작업의 이점도 있습니다.

## <a name="manage-new-capabilities"></a>새 기능 관리
- PowerShell을 사용 하 여 기능을 추가, 제거 및 업데이트 하는 방법을 [알아봅니다](add-remove-update-capabilities.md) .

## <a name="develop-a-capability"></a>기능 개발
다음 리소스를 사용 하 여 사용자 지정 기능을 작성 하는 데 도움을 받을 수 있습니다.
- 수집할 수 있는 데이터 원본에 [대해 알아봅니다](data-sources.md) .
- 기능을 작성 하는 데 필요한 클래스와 인터페이스가 포함 된 System Insights NuGet 패키지를 [다운로드](https://www.nuget.org/packages/Microsoft.WindowsServer.SystemInsights/) 합니다.
- API 설명서를 [방문](https://aka.ms/systeminsights-api) 하 여 System Insights 클래스 및 인터페이스에 대해 알아보세요.
- 시스템 정보 샘플 기능을 [사용](https://aka.ms/systeminsights-samplecapability) 하 여 시작 하는 데 도움을 받을 수 있습니다. 이는 기능을 등록 하 고, 수집할 데이터 원본을 지정 하 고, 시스템 데이터 분석을 시작 하는 방법을 보여 줍니다.

>[!NOTE]
>이는 시험판 기능입니다. 새 기능을 추가 하 고 피드백을 통합할 때 변경 될 수 있습니다.

## <a name="additional-references"></a>추가 참조
시스템 정보에 대 한 자세한 내용을 보려면 다음 리소스를 사용 하세요.

- [시스템 인사이트 개요](overview.md)
- [기능 이해](understanding-capabilities.md)
- [기능 관리](managing-capabilities.md)
- [기능 추가, 제거 및 업데이트](add-remove-update-capabilities.md)
- [시스템 정보 FAQ](faq.md)