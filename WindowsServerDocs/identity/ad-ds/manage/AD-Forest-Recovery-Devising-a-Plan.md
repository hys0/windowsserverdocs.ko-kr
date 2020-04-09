---
title: Ad 포리스트 복구-AD 포리스트 복구 계획 고안
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 17381f30-55f2-4e00-977a-b701675fa4ff
ms.technology: identity-adds
ms.openlocfilehash: ebdff0616d0e3a99b710e07e3bff149a275ff4ea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824027"
---
# <a name="ad-forest-recovery---devising-an-ad-forest-recovery-plan"></a>Ad 포리스트 복구-AD 포리스트 복구 계획 고안

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

사용자 환경 및 비즈니스 요구 사항에 따라이 가이드에 설명 된 모든 단계를 수행 하 여 성공적인 포리스트 복구를 수행할 필요가 없을 수도 있습니다. 이 가이드는 포리스트 복구를 위한 템플릿으로만 제공 되므로 사용자 환경에 적합 하 고 비즈니스 요구를 충족 하는 사용자 지정 포리스트 복구 계획을 세워야 합니다.  
  
예를 들어 포리스트 복구 계획에서 포리스트의 상세 토폴로지 맵이 있어야 합니다. 지도에는 해당 이름, 해당 역할 및 백업 상태, 두 그룹 간의 트러스트 관계 등 Dc에 대 한 모든 정보가 나열 됩니다. 토폴로지 맵을 만드는 데 사용할 수 있는 도구는 [Microsoft Active Directory 토폴로지 Diagrammer](https://www.microsoft.com/download/details.aspx?id=13380)를 참조 하세요.  
  
1 년에 한 번 이상 포리스트 복구 계획을 연습 해야 합니다. 또한 Enterprise Admins 또는 Domain Admins 그룹의 멤버 자격이 변경 되 면 포리스트 복구 훈련을 수행 하는 것이 좋습니다. 이를 통해 IT (정보 기술) 직원은 포리스트 복구 계획을 완벽 하 게 이해할 수 있습니다.

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
