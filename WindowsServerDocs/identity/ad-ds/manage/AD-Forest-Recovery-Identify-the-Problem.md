---
title: "광고 복구 포리스트-문제 식별"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 1e9ede12dade0b5f1149eae784620520a8866e30
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="identify-the-problem"></a>한 문제 식별

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
  
 숲 수준의 실패 증상이 표시 되 면 이벤트 로그 또는 모니터링 다른 해결 방법에는 오류 원인을 파악 하려면 Microsoft 지원 서비스와 작동 하 고 모든 가능한 보상 평가 같은 합니다.  
 
## <a name="examples-of-forest-wide-failures"></a>숲 전체 오류의 예 
  
-   모든 Dc 논리적 손상 되었거나 비즈니스 연속성 가능한;는 지점에 물리적 손상 예를 들어, 모든 비즈니스 응용 프로그램 AD DS에 의존 하는 작동 하지 않습니다.  
  
-   악의적인 관리자가 Active Directory 환경을 손상 합니다.  
  
-   시스템에 침투 의도적으로-또는 관리자가 실수로-스크립트 숲 데이터가 손상 분산를 실행 합니다.  
  
-   시스템에 침투 의도적으로-또는 관리자가 실수로-악의적 이거나 충돌 하는 변경 된 Active Directory 스키마를 확장 합니다.  
  
-   Dc, 악성 소프트웨어를 설치 하려면 공격자 관리 하 고 사용자가 있었던 경우 Microsoft 지원 센터에서 숲 백업에서 복구 합니다.  
  
    > [!IMPORTANT]
    >  이 문서 해킹 되었거나 손상 된 숲 복구 하는 방법에 대 한 보안 권장 적용 되지 않습니다. 일반적으로 환경을 강화 하기 위해이에 따라 Pass-the-해시 mitigation 기술을 좋습니다. 자세한 내용은 참조 [완화 Pass-the-해시 (PtH) 공격 및 기타 자격 증명 도용의 기술](https://www.microsoft.com/download/details.aspx?id=36036)합니다.  
  
-   Dc 중 해당 복제 파트너와 함께 복제할 수 있습니다.  
  
-   모든 도메인 컨트롤러에서 AD DS에도 변경할 수 없습니다.  
  
-   새로운 Dc 도메인에 설치할 수 없습니다.  
  
## <a name="next-steps"></a>다음 단계
-   [광고 숲 복구 필수](AD-Forest-Recovery-Prerequisties.md)  
-   [사용자 지정 숲 복구 계획 고안-광고 숲 복구](AD-Forest-Recovery-Devising-a-Plan.md)  
- [광고 숲 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
-   [광고 숲 복구-복구 하는 방법을 확인](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [광고 숲 복구-초기 복구](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  
-   [광고 숲 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
-   [광고 숲 복구-Multidomain 숲 내 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [광고 숲 복구-Windows Server 2003 도메인 컨트롤러 관련 숲 복구](AD-Forest-Recovery-Windows-Server-2003.md) 
