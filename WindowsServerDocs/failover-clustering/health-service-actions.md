---
title: 작업 상태 관리 서비스
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: a4ef08a4ca552211b64d11677153775d6b18b4fa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827626"
---
# <a name="health-service-actions"></a>작업 상태 관리 서비스

> 적용 대상: Windows Server 2019, Windows Server 2016

상태 관리 서비스는 스토리지 공간 다이렉트를 실행 하는 클러스터에 대 한 일상적인 모니터링 및 운영 환경을 개선 하는 Windows Server 2016의 새로운 기능입니다.

## <a name="actions"></a>작업  

다음 섹션에서는 상태 관리 서비스에서 자동화되는 워크플로를 설명합니다. 동작이 실제로 자율적으로 수행되는지 확인하거나 해당 진행률 또는 결과를 추적하기 위해 상태 관리 서비스에서 "동작"을 생성합니다. 로그와 달리 동작은 완료되는 즉시 사라지며, 주로 성능이나 용량에 영향을 줄 수 있는 진행 중인 활동(예: 복원력 복원 또는 데이터 리밸런싱)에 대한 정보를 제공합니다.  

### <a name="usage"></a>사용법  

하나의 새 PowerShell cmdlet에 모든 동작이 표시됩니다.  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>검사  

Windows Server 2016에서 **StorageHealthAction** cmdlet은 다음 정보를 반환할 수 있습니다.  

-   실패했거나 연결이 끊어졌거나 응답하지 않는 실제 디스크를 사용 중지하는 중  

-   대체 실제 디스크를 사용하도록 스토리지 풀을 전환하는 중  

-   데이터의 전체 복원력을 복원하는 중  

-   스토리지 풀을 리밸런싱하는 중  

## <a name="see-also"></a>참고 항목

- [Windows Server 2016의 상태 관리 서비스](health-service-overview.md)
- [MSDN의 개발자 설명서, 샘플 코드 및 API 참조](https://msdn.microsoft.com/windowshealthservice)
