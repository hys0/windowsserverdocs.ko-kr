---
title: AD 포리스트 복구-포리스트를 복원 하기 위한 단계
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adds
ms.openlocfilehash: 1712d3a636160f82495539afdd42ab2ee85ffae2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861474"
---
# <a name="ad-forest-recovery---steps-for-restoring-the-forest"></a>AD 포리스트 복구-포리스트를 복원 하기 위한 단계

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 섹션에서는 포리스트를 복구 하기 위한 권장 되는 경로 대 한 개요를 제공 합니다. 포리스트 복구 절차는 나중에 자세히 설명 됩니다.  
  
다음 목록에 높은 수준의 복구 단계를 요약 되어 있습니다.  
  
1. [문제를 식별 합니다.](AD-Forest-Recovery-Identify-the-Problem.md)  

   작업할 IT 및 Microsoft 지원에 문제 및 잠재적 원인의 범위를 확인 하 고 모든 비즈니스 이해 관계자와 가능한 해결책을 평가 합니다. 대부분의 경우에서 전체 포리스트 복구는 마지막 옵션은 있어야 합니다.  
  
2. [포리스트를 복구 하는 방법 결정](AD-Forest-Recovery-Determine-how-to-Recover.md)  

   완료 준비 단계에 대 한 준비 단계는 포리스트 복구 필요를 확인 한 후: 현재 포리스트 구조를 확인 하 고, 각 DC에는 DC를 결정 하기 위해 수행 각 도메인에 대 한 복원 기능을 식별, 모든 쓰기 가능한 Dc에 되어 있는지 확인 오프 라인 상태가 됩니다.  

3. [초기 복구를 수행 합니다.](AD-Forest-Recovery-Perform-initial-recovery.md)  

   격리에서 각 도메인에 대 한 하나의 DC, 복구한 정리 하면 도메인을 다시 연결 합니다. 권한 있는 계정이 다시 설정 하 고이 단계에서 보안 위반으로 인 한 문제를 해결 합니다.  
  
4. [Dc 남은 다시 배포](AD-Forest-Recovery-Restore-Additional-DCs.md)  

   실패 하기 전에 해당 상태로 돌아갈 포리스트를 다시 배포 합니다. 이 단계는 특정 디자인 및 요구 사항에 적응 해야 합니다. 가상화 된 도메인 컨트롤러 복제이 프로세스를 촉진 하는 데 도움이 됩니다.  

5. [정리](AD-Forest-Recovery-Cleanup.md)  

   기능을 복원한 후 필요에 따라 이름 확인을 다시 구성 하 고 작동 하는 LOB 응용 프로그램을 가져옵니다.  

이 가이드의 단계를 복구 된 포리스트에 위험한 데이터를 다시 가능성을 최소화 하도록 설계 되었습니다. 등의 요인에 대 한 계정에 이러한 단계를 수정 해야 할 수 있습니다.  
  
- 확장성  
- 원격 관리 효율성  
- 복구 속도  
