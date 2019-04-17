---
title: 광고 숲 복구-다중 도메인 숲 속의 단일 도메인 복구
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adfs
ms.openlocfilehash: 3a1c9d0671a732eee83aa707e061afdbbf106fa5
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>광고 숲 복구-다중 도메인 숲 속의 단일 도메인 복구

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

전체 숲 복구 보다는 여러 도메인에 있는 숲 내 도메인만 복구 해야 하는 경우가 있을 수 있습니다. 이 항목 단일 도메인 및 복구를 위한 가능한 전략을 복구 하는 사항에 설명 합니다.  
  
 단일 도메인 복구 다시 드 (GC) 서버에 대 한 특수 한 도전 과제를 제공 합니다. 예를 들어,의 첫 번째 DC (도메인 컨트롤러) 도메인에 대 한는 숲 속의 다른 모든 Gc 다음 일주일 이전에 만든 백업에서 복원 하는 경우 복원된 DC 해당 도메인에 대 한 더 많은 최신 데이터는 수 있습니다. GC 데이터 일관성을 다시 설정 하는 몇 가지 옵션이 있습니다.  
  
-   Unhost 한 다음 한 번에 복구 도메인에 제외 하 고 있는 숲 속의 모든 Gc의 도메인 복구 파티션을 유지 합니다.  
  
-   도메인에 복구 숲 복구 프로세스를 수행 하 고 다른 도메인에 있는 Gc에서 느린 개체를 제거 합니다.  
  
 다음 섹션에서는 각 옵션에 대 한 일반 고려 합니다. 다양 한 Active Directory 환경에 대 한 전체 집합이 복구를 위해 수행 해야 할 단계가 달라 집니다.  
  
## <a name="rehost-all-gcs"></a>모든 Gc 유지  

> [!WARNING]
>  모든 도메인에 대해 관리자 도메인 계정 암호 문제는 gc 로그온에 대 한 액세스를 방지 하는 경우 사용할 준비가 있어야 합니다.  

 모든 Gc 다시 호스팅할 편집할 수 있습니다 repadmin /unhost 및 repadmin /rehost 명령을 사용 하 여 (repadmin의 일부로 /experthelp). 복구 되지 않은 각 도메인에 있는 모든 GC에 repadmin 명령을 실행 합니다. 해야 하는 보장할 수 있는 모든 Gc 복구 된 도메인의 복사본을 더 이상 보관할 하지 않습니다. 이 위해 unhost 도메인 파티션 먼저 모든 도메인 컨트롤러에서 없음 복구 도메인 숲의 전체에 걸쳐 먼저 합니다. 모든 Gc 파티션을 더 이상 포함 되지 않은 한 후 다시 호스트 수 있습니다. 다시 호스팅할 예를 들어 사용자 숲 속의 사이트와 복제 구조 고려해, 전에 해당 사이트의 다른 Dc 다시 호스팅할 사이트 마다 하나의 DC rehost 완료 합니다.  
  
 이 옵션은 몇 가지 도메인 컨트롤러에만 각 도메인에 있는 작은 조직에 대 한 도움이 될 수 있습니다. 모든 Gc 다시 구성 금요일 밤에 및, 필요한 경우 모든 읽기 전용 도메인에 대 한 전체 복제 파티션을 복구 월요일 아침 하기 전에 합니다. 있지만 세계 사이트에 설명 하는 큰 도메인 복구 해야 할 경우의 모든 Gc 읽기 전용 도메인 파티션 다시 호스팅할 다른 도메인에 대 한 수 있습니다 크게 영향을 작업 시간 잠재적으로 필요 합니다.  
  
## <a name="remove-lingering-objects"></a>느린 개체를 제거  
 비슷한 숲 복구 과정을 한 DC 백업에서 복원 도메인에 있는 복구 나머지 Dc 정리 메타 데이터를 수행 하 고 AD DS 도메인을 구축 하 여를 다시 설치 해야 합니다. 숲 속의의 다른 모든 도메인 Gc에 읽기 전용 파티션을 복구 된 도메인의 느린 개체 제거할 수 있습니다.  
  
 느린 개체 정리에 대 한 소스 복구 된 도메인의 DC 해야 합니다. 원본 DC 모든 도메인 파티션에 대 한 지연 개체 없는 수를 GC 있었다면 드를 제거할 수 있습니다.  
  
 느린 물체를 제거 하는 다른 옵션은와 관련 된 아래쪽에 영향을 받지 대기업에 유용 합니다.  
  
 자세한 내용은 참조 [느린 개체를 제거를 사용 하 여 Repadmin](https://technet.microsoft.com/library/cc785298.aspx)합니다.

## <a name="next-steps"></a>다음 단계
-   [광고 숲 복구 필수](AD-Forest-Recovery-Prerequisties.md)  
-   [사용자 지정 숲 복구 계획 고안-광고 숲 복구](AD-Forest-Recovery-Devising-a-Plan.md)  
-   [광고 숲 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
-   [광고 숲 복구-복구 하는 방법을 확인](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [광고 숲 복구-초기 복구](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  
-   [광고 숲 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
-   [광고 숲 복구-Multidomain 숲 내 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [광고 숲 복구-Windows Server 2003 도메인 컨트롤러 관련 숲 복구](AD-Forest-Recovery-Windows-Server-2003.md)  
