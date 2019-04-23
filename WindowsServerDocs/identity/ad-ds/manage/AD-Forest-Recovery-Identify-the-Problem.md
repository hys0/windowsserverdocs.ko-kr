---
title: AD 포리스트 복구 - 문제 식별
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: cb3cf45f778ff305c8fe5aad5e23f0257650d6f5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865524"
---
# <a name="identify-the-problem"></a>문제를 식별 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2
  
포리스트 오류의 증상 표시 되 면 이벤트 로그 또는 기타 모니터링 솔루션에서 작업 실패의 원인을 확인 하려면 Microsoft 지원 하 고 모든 가능한 구제 평가 같은 합니다.  

## <a name="examples-of-forest-wide-failures"></a>포리스트 오류의 예

- 모든 Dc 논리적으로 손상 되었거나 비즈니스 연속성은 불가능 한 지점에 물리적으로 손상 예를 들어 AD DS에 종속 된 모든 비즈니스 응용 프로그램 작동 하지 않습니다.  
- 악의적인 관리자가 Active Directory 환경을 손상 됩니다.  
- 공격자가 의도적으로-또는 관리자가 실수로-포리스트 전체에서 데이터 손상을 확산 되는 스크립트를 실행 합니다.  
- 공격자가 의도적으로-또는 관리자가 실수로-악의적 이거나 충돌 하는 변경 내용과 Active Directory 스키마를 확장 합니다.  
- 공격자가 Dc에서 악성 소프트웨어를 설치 하려면 관리 되는 수 있는 Microsoft 기술 지원 서비스에서 백업에서 포리스트를 복구 하려면.  
  
   > [!IMPORTANT]
   >  이 문서는 해킹 되었거나 손상 된 포리스트를 복구 하는 방법에 대 한 보안 권장 사항 적용 되지 않습니다. 일반적으로 것이 좋습니다 따라-Pass-the-hash 완화 기술 환경을 강화 합니다. 자세한 내용은 [완화-Pass-the-hash (PtH) 공격 및 기타 자격 증명 도용 기술](https://www.microsoft.com/download/details.aspx?id=36036)합니다.
  
- Dc에 하나도 해당 복제 파트너와 복제할 수 있습니다.  
- 모든 도메인 컨트롤러에서 AD DS에 변경할 수 없습니다.  
- 모든 도메인에 새 Dc는 설치할 수 없습니다.  
  
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
