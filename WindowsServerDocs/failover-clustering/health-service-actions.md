---
title: 상태 서비스 작업
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: efdf8f04e68fcbdc7051e78d6725cb919e740ffa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843024"
---
# <a name="health-service-actions"></a>상태 서비스 작업

> 적용 대상: Windows Server 2016

상태 관리 서비스는 저장소 공간 다이렉트를 실행 하는 클러스터에 대 한 작업 경험과 일상적인 모니터링을 향상 시키는 Windows Server 2016의 새로운 기능입니다.

## <a name="actions"></a>동작  

다음 섹션에서는 상태 관리 서비스에서 자동화되는 워크플로를 설명합니다. 동작이 실제로 자율적으로 수행되는지 확인하거나 해당 진행률 또는 결과를 추적하기 위해 상태 관리 서비스에서 "동작"을 생성합니다. 로그와 달리 동작은 완료되는 즉시 사라지며, 주로 성능이나 용량에 영향을 줄 수 있는 진행 중인 활동(예: 복원력 복원 또는 데이터 리밸런싱)에 대한 정보를 제공합니다.  

### <a name="usage"></a>사용법  

하나의 새 PowerShell cmdlet에 모든 동작이 표시됩니다.  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>적용 범위  

Windows Server 2016에는 **Get-storagehealthaction** cmdlet에 다음 정보를 반환할 수 있습니다.  

-   실패했거나 연결이 끊어졌거나 응답하지 않는 실제 디스크를 사용 중지하는 중  

-   대체 실제 디스크를 사용하도록 저장소 풀을 전환하는 중  

-   데이터의 전체 복원력을 복원하는 중  

-   저장소 풀을 리밸런싱하는 중  

## <a name="see-also"></a>참조

- [Windows Server 2016의에서 상태 관리 서비스](health-service-overview.md)
- [개발자 설명서, 샘플 코드 및 API 참조](https://msdn.microsoft.com/windowshealthservice)
