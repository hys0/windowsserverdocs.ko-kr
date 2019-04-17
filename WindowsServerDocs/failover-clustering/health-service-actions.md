---
title: "건강 서비스 작업"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: efdf8f04e68fcbdc7051e78d6725cb919e740ffa
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-actions"></a>건강 서비스 작업

> Windows Server 2016 적용 됩니다.

상태 서비스는 Storage Spaces Direct 실행 클러스터에 대 한 작동 경험과 일상적인 모니터링 개선 하는 Windows Server 2016의 새로운 기능입니다.

## <a name="actions"></a>작업  

다음 섹션 어떤 의료 서비스에 의해 자동 워크플로에 대해 설명 합니다. 작업 자율적, 촬영 되 고 실제로 하거나 상태 서비스의 진행률 또는 결과 추적, "작업" 생성 확인 합니다. 로그 달리 작업을 완료 하 고 주로 성능 또는 (예: 복구를 복원 하거나 데이터 재조정) 용량 영향을 줄 수 있는 지속적인 활동에 대 한 정보를 제공 하기 위한 것 후 곧 사라집니다.  

### <a name="usage"></a>사용  

새 PowerShell cmdlet 모든 작업을 표시합니다.  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>검사  

Windows Server 2016에는 **Get StorageHealthAction** cmdlet에 다음과 같은 정보를 돌아갈 수 있습니다.  

-   손실, 실패 한 연결이 또는 응답 하지 않는 하 여 실제 디스크를 더 이상 사용  

-   교체 실제 디스크를 사용 하 여 저장소 풀 전환  

-   데이터를 전체 복구 복원  

-   저장소 풀 재조정  

## <a name="see-also"></a>참조 하십시오

- [Windows Server 2016에에서 상태 서비스](health-service-overview.md)
- [개발자 문서, 샘플 코드 및 msdn API 참조](https://msdn.microsoft.com/windowshealthservice)
