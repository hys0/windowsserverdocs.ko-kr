---
title: "광고 숲 복구 숲 복원 하기 위한 단계"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: 29988c262897649173e039cc052bb64f38a1a0ca
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
#<a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>광고 숲 복구 숲 복원 하기 위한 단계 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

이 섹션에 숲 복구 하기 위한 권장된 경로 개요를 제공 합니다. 숲 복구 단계 나중에 자세히 설명 되어 있습니다.  
  
 개략적 복구 단계를 다음과 같습니다.  
  
1.  [한 문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)  
  
     작업을 IT 문제와 가능한 원인은 범위를 결정 하 고 모든 비즈니스 관련 자가를 해결할 수도 평가 하 고 있습니다. 대부분의 경우 전체 숲 복구 최후의 수단 있어야 합니다.  
  
2.  [숲 복구 하는 방법을 결정 합니다.](AD-Forest-Recovery-Determine-how-to-Recover.md)  
  
     완료 임시 숲 복구 필요 하다를 확인 한 후에 대 한 준비를 단계: 현재 숲 구조 확인 하 고, 식별에서 수행 하는 기능 각 DC을 결정 하는 DC 각 도메인 복원 하는 모든 쓰기 Dc 오프 라인을 확인 합니다.  
  
3.  [초기 복구](AD-Forest-Recovery-Perform-initial-recovery.md)  
  
     격리에서 각 도메인에 대 한 DC 복구 하 고, 정리 도메인 다시 연결 합니다. 권한 계정, 초기화 하 고이 단계에서 보안 위반 하 여 발생 하는 문제를 해결 하세요.  
  
4.  [Dc 남은 배포](AD-Forest-Recovery-Restore-Additional-DCs.md)  
  
     오류가 발생 하기 전에 상태로 반환 숲을 배포 합니다. 이 단계 특정 디자인 및 요구 사항에 맞게 조정 해야 합니다. 가상화 도메인 컨트롤러 복제이 프로세스를 신속 하는 데 도움이 됩니다.  
  
5.  [정리](AD-Forest-Recovery-Cleanup.md)  
  
     기능이 복원 된 후 이름 확인 필요에 따라 다시 작동 LOB 응용 프로그램.  

  
 이 가이드는 단계는 위험한 데이터 복구 숲에 다시 초래 최소화 하도록 설계 되었습니다. 다음이 단계를 등을 고려 수정 해야 할 수 있습니다.  
  
-   확장성  
-   원격 관리  
-   복구 속도  

