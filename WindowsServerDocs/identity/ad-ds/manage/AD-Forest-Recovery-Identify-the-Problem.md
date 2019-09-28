---
title: AD 포리스트 복구 - 문제 식별
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: dddbd187fb100b94b505a74595e040cec580a797
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369123"
---
# <a name="identify-the-problem"></a>문제 식별

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2
  
이벤트 로그 또는 다른 모니터링 솔루션과 같이 포리스트 전체 오류의 증상이 나타나는 경우 Microsoft 지원를 사용 하 여 오류 원인을 확인 하 고 가능한 해결 방법을 평가 합니다.  

## <a name="examples-of-forest-wide-failures"></a>포리스트 전체 오류의 예

- 모든 Dc가 논리적으로 손상 되었거나 비즈니스 연속성을 불가능 하 게 하는 지점으로 물리적으로 손상 되었습니다. 예를 들어 AD DS에 의존 하는 모든 비즈니스 응용 프로그램은 작동 하지 않습니다.  
- 악의적인 관리자가 Active Directory 환경을 손상 시킨 경우  
- 공격자가 의도적으로, 또는 관리자가 실수로 데이터 손상을 분산 하는 스크립트를 실행 합니다.  
- 공격자가 의도적으로 또는 관리자가 실수로 Active Directory 스키마를 확장 하 여 악의적 이거나 충돌 하는 변경 내용을 적용 합니다.  
- 공격자가 Dc에 악성 소프트웨어를 설치 하도록 관리 했으며, 백업에서 포리스트를 복구 하는 Microsoft 지원 하는 것이 좋습니다.  
  
   > [!IMPORTANT]
   >  이 문서에서는 해킹 또는 손상 된 포리스트를 복구 하는 방법에 대 한 보안 권장 사항을 다루지 않습니다. 일반적으로 환경을 강화 하기 위해 해시 전달 완화 기법을 따르는 것이 좋습니다. 자세한 내용은 [통과-해시 (PtH) 공격 및 기타 자격 증명 도난 기술 완화](https://www.microsoft.com/download/details.aspx?id=36036)를 참조 하세요.
  
- 모든 Dc는 해당 복제 파트너와 복제할 수 없습니다.  
- 모든 도메인 컨트롤러에서 AD DS를 변경할 수 없습니다.  
- 모든 도메인에 새 Dc를 설치할 수 없습니다.  
  
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
