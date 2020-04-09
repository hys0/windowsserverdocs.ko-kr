---
title: AD 포리스트 복구-포리스트 복원 단계
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 537543bedd68bff002054f637d96240a71f75793
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823406"
---
# <a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>AD 포리스트 복구-포리스트 복원 단계

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 섹션에서는 포리스트를 복구 하는 데 권장 되는 경로의 개요를 제공 합니다. 포리스트 복구 단계는 나중에 자세히 설명 합니다.  
  
다음 목록에는 높은 수준의 복구 단계가 요약 되어 있습니다.  
  
1. [문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)  

   IT 및 Microsoft 지원를 사용 하 여 문제 범위와 잠재적 원인을 파악 하 고 모든 비즈니스 관련자와 관련 하 여 가능한 해결책을 평가 하세요. 대부분의 경우 전체 포리스트 복구가 마지막 옵션 이어야 합니다.  
  
2. [포리스트를 복구 하는 방법 결정](AD-Forest-Recovery-Determine-how-to-Recover.md)  

   포리스트 복구가 필요 하다 고 판단 되 면 준비 하는 준비 단계를 완료 합니다. 현재 포리스트 구조를 확인 하 고, 각 DC에서 수행 하는 기능을 식별 하 고, 각 도메인에 대해 복원할 DC를 결정 하 고, 쓰기 가능한 모든 Dc를 오프 라인 상태로 만들 수 있는지 확인 합니다.  

3. [초기 복구 수행](AD-Forest-Recovery-Perform-initial-recovery.md)  

   격리에서 각 도메인에 대해 하나의 DC를 복구한 후 정리 하 고 도메인을 다시 연결 합니다. 권한 있는 계정을 다시 설정 하 고이 단계에서 보안 위반으로 인해 발생 한 문제를 해결 합니다.  
  
4. [남은 Dc 다시 배포](AD-Forest-Recovery-Restore-Additional-DCs.md)  

   포리스트를 다시 배포 하 여 오류 전 상태로 되돌립니다. 이 단계는 특정 디자인 및 요구 사항에 맞게 조정 해야 합니다. 가상화 된 도메인 컨트롤러 복제를 통해이 프로세스를 신속 하 게 수행할 수 있습니다.  

5. [정리](AD-Forest-Recovery-Cleanup.md)  

   기능이 복원 된 후에는 필요에 따라 이름 확인을 다시 구성 하 고 LOB 응용 프로그램을 작동 합니다.  

이 가이드의 단계는 위험한 데이터를 복구 된 포리스트로 재 도입 가능성을 최소화 하도록 설계 되었습니다. 다음과 같은 요인을 고려 하 여 이러한 단계를 수정 해야 할 수 있습니다.  
  
- 확장성  
- 원격 관리 효율성  
- 복구 속도  
