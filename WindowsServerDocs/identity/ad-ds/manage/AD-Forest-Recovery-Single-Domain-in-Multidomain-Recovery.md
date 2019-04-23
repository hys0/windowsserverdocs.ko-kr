---
title: AD 포리스트 복구-다중 도메인 포리스트에서 단일 도메인 복구
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adds
ms.openlocfilehash: fae2cc40af0b43dd38d72c2622720a6bb17b0a66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863474"
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>AD 포리스트 복구-다중 도메인 포리스트에서 단일 도메인 복구

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

전체 포리스트 복구를 보다는 여러 도메인이 있는 포리스트 내의 단일 도메인만 복구 하는 데 필요한 경우가 있을 수 있습니다. 이 항목에는 단일 도메인 및 복구를 위한 가능한 전략을 복구 하기 위한 고려 사항을 다룹니다.  
  
단일 도메인 복구 GC (글로벌 카탈로그) 서버를 다시 작성 하기 위한 고유한 과제를 안고 있습니다. 예를 들어, 도메인에 대 한 첫 번째 도메인 컨트롤러 (DC) 포리스트의 다른 모든 Gc 1 주일 앞에서 만든 백업에서 복원 되 면 복원된 된 DC 보다 해당 도메인에 대 한 더 많은 최신 데이터 해야 합니다. GC 데이터 일관성을 다시 설정 하는 몇 가지 옵션이 있습니다.  
  
- Unhost 하 고 제외한 복구 된 도메인 포리스트의 모든 Gc에서 복구 된 도메인 파티션을 동시에 다시 호스트 합니다.  
- 도메인에 복구 하려면 포리스트 복구 프로세스를 수행 하 고 다른 도메인의 Gc에서 느린 개체를 제거 합니다.  
  
다음 섹션에서는 각 옵션에 대 한 일반 고려 사항을 제공합니다. 다른 Active Directory 환경에 대 한 전체 복구를 수행 해야 하는 단계 집합이 달라 집니다.  
  
## <a name="rehost-all-gcs"></a>Rehost 모든 Gc  

> [!WARNING]
> 문제가 로그온에 대 한 GC에 대 한 액세스를 방지 하는 경우 모든 도메인에 대 한 도메인 관리자 계정의 암호를 사용할 준비가 이어야 합니다.  

모든 Gc 재호스팅 수행할 수 있습니다 repadmin을 사용 하 여 / unhost 및 repadmin /rehost 명령 (repadmin /experthelp의 일부). 복구 되지 않은 각 도메인에 모든 GC에서 repadmin 명령을 실행할 것입니다. 해야 보장 될 모든 Gc 복구 된 도메인의 복사본을 더 이상 포함 되지 않은 합니다. 이 위해 unhost 도메인 파티션에 먼저 모든 도메인 컨트롤러에서 포리스트의 none-복구 도메인 전체에 걸쳐 먼저 합니다. 모든 Gc 없는 파티션에 더 이상, 후에 다시 호스트 수 있습니다. 예를 들어 포리스트, 사이트 및 복제 구조는 것이 좋습니다, 다시 호스팅할 때 해당 사이트의 다른 Dc 재호스팅 전에 사이트당 한 DC의 rehost를 마감 합니다.  
  
이 옵션은 각 도메인에 대 한 몇 가지 도메인 컨트롤러만 있는 소규모 조직에 유용 합니다. 모든 Gc 금요일 밤에 다시 작성 될 수 하 고 월요일 아침 전까지 모든 읽기 전용 도메인에 대 한 복제를 완료 분할 필요한 경우. 하지만 전 세계에 걸쳐 사이트를 포함 하는 대규모 도메인을 복구 해야 할 경우 모든 Gc에서 읽기 전용 도메인 파티션에 재호스팅 다른 도메인에 대 한 상당히 영향 작업 및 수 잠재적 작동 중단 시간이 필요 합니다.  
  
## <a name="remove-lingering-objects"></a>느린 개체를 제거 합니다.

포리스트 복구 프로세스와 유사 하나 DC 백업에서 복원 복구에서 나머지 Dc의 메타 데이터 정리를 수행 하 고, AD DS 도메인 빌드를 다시 설치 해야 하는 도메인에서. 포리스트의 다른 모든 도메인의 Gc에 복구 된 도메인의 읽기 전용으로 파티션에 대 한 느린 개체를 제거할 수 있습니다.  

느린 개체를 정리에 대 한 원본 복구 된 도메인의 DC 이어야 합니다. 원본 DC 어떤 도메인 파티션에 대 한 모든 느린 개체가 없는 일에 GC 경우 글로벌 카탈로그를 제거할 수 있습니다.  

느린 개체를 제거 하는 것이 다른 옵션과 관련 된 가동 중지 시간을 받지는 대규모 조직의 유리 합니다.  

자세한 내용은 [느린 개체를 제거를 사용 하 여 Repadmin](https://technet.microsoft.com/library/cc785298.aspx)합니다.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구-필수 구성 요소](AD-Forest-Recovery-Prerequisties.md)  
- [사용자 지정 포리스트 복구 계획을 고안 AD 포리스트 복구-](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD 포리스트 복구 문제를 식별 합니다.](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD 포리스트 Recovery-복구 하는 방법 결정](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD 포리스트 복구-초기 복구를 수행 합니다.](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)  
- [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
- [AD 포리스트 복구-Multidomain 포리스트에 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)  
