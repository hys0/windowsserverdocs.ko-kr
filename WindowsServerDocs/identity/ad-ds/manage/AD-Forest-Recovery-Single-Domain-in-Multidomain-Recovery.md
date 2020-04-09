---
title: AD 포리스트 복구-다중 도메인 포리스트의 단일 도메인 복구
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 267541be-2ea7-4af6-ab34-8b5a3fedee2d
ms.technology: identity-adds
ms.openlocfilehash: 13153358f50302de722109bfe101911e3bac4708
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823446"
---
# <a name="ad-forest-recovery---recovering-a-single-domain-in-a-multidomain-forest"></a>AD 포리스트 복구-다중 도메인 포리스트의 단일 도메인 복구

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

전체 포리스트 복구가 아닌 여러 도메인이 있는 포리스트 내에서 단일 도메인만 복구 해야 하는 경우가 있을 수 있습니다. 이 항목에서는 단일 도메인 복구 및 가능한 복구 전략에 대 한 고려 사항에 대해 설명 합니다.  
  
단일 도메인 복구는 GC (글로벌 카탈로그) 서버를 다시 작성 하는 고유한 과제를 제공 합니다. 예를 들어 도메인의 첫 번째 DC (도메인 컨트롤러)가 한 주 전에 만들어진 백업에서 복원 되는 경우 포리스트의 다른 모든 Gc는 복원 된 DC 보다 해당 도메인에 대 한 최신 데이터를 갖게 됩니다. GC 데이터 일관성을 다시 설정 하려면 다음 두 가지 옵션을 사용할 수 있습니다.  
  
- 호스트를 제거 하 고 포리스트의 모든 Gc에서 복구 된 도메인 파티션을 동시에 rehost 합니다.  
- 포리스트 복구 프로세스에 따라 도메인을 복구한 다음 다른 도메인의 Gc에서 느린 개체를 제거 합니다.  
  
다음 섹션에서는 각 옵션에 대 한 일반적인 고려 사항을 제공 합니다. 복구를 위해 수행 해야 하는 전체 단계 집합은 Active Directory 환경 마다 다를 수 있습니다.  
  
## <a name="rehost-all-gcs"></a>모든 Gc Rehost  

> [!WARNING]
> 모든 도메인에 대 한 도메인 관리자 계정의 암호는 문제가 발생 하 여 로그온에 GC에 액세스할 수 없는 경우에 사용할 수 있도록 준비 해야 합니다.  

재호스팅 모든 Gc는 repadmin/unhost 및 repadmin/rehost 명령을 사용 하 여 수행할 수 있습니다 (repadmin/experthelp의 일부). 복구 되지 않은 각 도메인의 모든 GC에서 repadmin 명령을 실행 합니다. 모든 Gc에서 복구 된 도메인의 복사본을 더 이상 저장 하지 않도록 해야 합니다. 이를 위해서는 먼저 포리스트의 모든 비 복구 도메인에 있는 모든 도메인 컨트롤러에서 도메인 파티션을 먼저 호스트 하지 않습니다. 모든 Gc에 파티션이 더 이상 포함 되어 있지 않으면 rehost 수 있습니다. 재호스팅 때 포리스트의 사이트 및 복제 구조를 고려 합니다. 예를 들어, 사이트의 다른 Dc를 재호스팅 하기 전에 사이트별로 rehost 한 DC를 완료 합니다.  
  
이 옵션은 각 도메인에 대해 소수의 도메인 컨트롤러만 있는 소규모 조직에 유용할 수 있습니다. 모든 Gc는 금요일 밤에 다시 작성 될 수 있으며, 필요한 경우 월요일 아침 이전의 모든 읽기 전용 도메인 파티션에 대해 복제를 완료 합니다. 하지만 전 세계에 사이트를 포함 하는 큰 도메인을 복구 해야 하는 경우에는 다른 도메인에 대 한 모든 Gc에서 읽기 전용 도메인 파티션을 재호스팅 작업에 상당한 영향을 줄 수 있으며, 잠재적으로 중단 시간이 필요할 수 있습니다.  
  
## <a name="remove-lingering-objects"></a>느린 개체 제거

포리스트 복구 프로세스와 마찬가지로, 복구 해야 하는 도메인의 백업에서 한 DC를 복원 하 고, 나머지 Dc의 메타 데이터 정리를 수행 하 고, AD DS을 다시 설치 하 여 도메인을 빌드합니다. 포리스트에 있는 다른 모든 도메인의 Gc에서 복구 된 도메인의 읽기 전용 파티션에 대 한 느린 개체를 제거 합니다.  

느린 개체 정리의 원본은 복구 된 도메인의 DC 여야 합니다. 원본 DC에 도메인 파티션에 대 한 느린 개체가 없도록 하려면 GC 인 경우 글로벌 카탈로그를 제거할 수 있습니다.  

느린 개체를 제거 하면 다른 옵션과 관련 된 작동 중단 시간을 줄일 수 없는 대규모 조직의 경우 유용 합니다.  

자세한 내용은 [Repadmin을 사용 하 여 느린 개체 제거](https://technet.microsoft.com/library/cc785298.aspx)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 - 필수 조건](AD-Forest-Recovery-Prerequisties.md)  
- [AD 포리스트 복구-사용자 지정 포리스트 복구 계획 고안](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD 포리스트 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
- [AD 포리스트 복구-복구 방법을 결정 합니다.](AD-Forest-Recovery-Determine-how-to-Recover.md)
- [AD 포리스트 복구-초기 복구 수행](AD-Forest-Recovery-Perform-initial-recovery.md)  
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)  
- [AD 포리스트 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
- [AD 포리스트 복구-다중 도메인 포리스트 내에서 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
- [AD 포리스트 복구-Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)  
