---
title: PowerShell 성능 튜닝
description: PowerShell 성능 튜닝
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: landing-page
ms.author: jasonsh
author: lzybkr
ms.date: 10/16/2017
ms.openlocfilehash: 382305e2bd15ef6fcb038c3fa064bc2841eabae1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851956"
---
# <a name="performance-tuning-for-powershell"></a>Powershell 성능 튜닝

이 문서에서는 PowerShell 5.1의 성능을 최대한 높이기 위한 일반적인 지침을 설명합니다. 이 문서에서 설명하는 이슈 중 일부는 이후 버전에서 해결될 수 있습니다.

이 문서는 모범 사례를 설명하지 않습니다.

이 문서의 지침을 신중하게 적용해야 합니다.
* 성능은 종종 전혀 문제가 되지 않습니다. 10ms를 줄이든 100ms를 줄이든 별 차이가 없습니다.
* 이 문서의 일부 지침은 일부 PowerShell 사용자에게 익숙하지 않아 혼란을 줄 수 있는 이례적인 PowerShell 사용 방법을 다룹니다.

다음 토픽에서는 자세한 지침을 제공합니다.

-   [스크립트 작성 시 고려 사항](script-authoring-considerations.md)

-   [모듈 작성 시 고려 사항](module-authoring-considerations.md)