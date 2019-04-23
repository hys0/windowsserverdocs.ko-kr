---
title: AD 포리스트 복구-광고를 고안 포리스트 복구 계획
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.technology: identity-adds
ms.openlocfilehash: edfc874fe030c6394bc8bda95c49e61951e78f43
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881784"
---
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>AD 포리스트 복구-광고를 고안 포리스트 복구 계획

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

환경 및 비즈니스 요구 사항에 따라 수 또는 성공한 포리스트 복구를 수행 하려면이 가이드에 설명 된 모든 단계를 수행 필요가 없을 수도 있습니다. 이 가이드는 포리스트 복구를 위해 템플릿으로, 사용자 환경에 적합 한 비즈니스 요구를 충족 하는 사용자 지정 포리스트 복구 계획을 고안 하는 중요 한 것입니다.  
  
예를 들어 포리스트 복구 계획에 있어야 포리스트 자세한 토폴로지 맵의 합니다. Map의 이름, 해당 역할 및 백업 상태 및 이들 간의 트러스트 관계와 같은 Dc에 대 한 모든 정보를 나열 해야 합니다. 토폴로지 맵을 만드는 데 사용할 수 있는 도구를 참조 하세요 [Microsoft Active Directory 토폴로지 Diagrammer](https://www.microsoft.com/download/details.aspx?id=13380)합니다.  
  
일년에 적어도 한 번에 포리스트 복구 계획을 연습 해야 합니다. 이기도 Domain Admins 또는 Enterprise Admins 그룹에 멤버 자격 변경 내용이 있는 경우에 포리스트 복구 드릴을 수행 하는 것이 좋습니다. 이렇게 하면 정보 기술 (IT) 담당자 포리스트 복구 계획을 완전히 이해할 수 있습니다.

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
