---
title: "광고 숲 복구 Virtualization"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adfs
ms.openlocfilehash: 08b0c4a4c5ed230f91241fcfb67db1749935c5e2
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="active-directory-forest-recovery-virtualization"></a>복구 Virtualization active Directory 숲

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

Windows Server 2016, R2, 2012 및 2012 가상화 도메인 컨트롤러 복제 기능에 설명 합니다.  
 
## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>가상화 도메인 컨트롤러 복제 사용 하 여 신속 하 게 처리 숲 복구  
 가상화 도메인 컨트롤러 (DC) 복제 신속히 추가 가상화 Dc 여러 Dc 하이퍼바이저에서 실행 되는 위치 데이터 센터 등 중앙된 위치에 특히 도메인에 설치 하는 프로세스를 간단 합니다. 백업에서 각 도메인에 있는 한 가상 DC 복원한 후 각 도메인에 추가 Dc 온라인 시킬 수 신속 하 게 가상화 DC 복제 프로세스를 사용 하 여 합니다. 복구를 종료 한 다음 복사 하는 첫 번째 가상화 DC 준비할 수 가상 하드 디스크에 필요한 횟수 복제 만들면서 가상화 Dc 도메인을 개발할 수 있습니다.  
  
 DC 가상화 복제의 요구 사항은 다음과 같습니다.  
  
-   하이퍼바이저는 VM-GenerationID 지원 해야 합니다. Windows Server 2016 년 2012에에서 Hyper-v 및 Windows 8에서 지 원하는 VM-GenerationID 하이퍼바이저의 예입니다. 공급 업체에 문의 하이퍼바이저 VM-GenerationID 지원 되는 경우를 확인 합니다.  
  
-   원본으로 복제에 사용 되는 가상화 DC Windows Server 2016 또는 2012를 실행 하 고 복제 가능한 도메인 컨트롤러 그룹 구성원 해야 합니다.  
  
-   Windows Server 2016 또는 2012 PDC 에뮬레이터 실행 해야 합니다. PDC 에뮬레이터 가상화 되 면 복제할 수 있습니다.  
  
 DC 복제 수행 하는 방법에 대 한 단계별 지침 가상화 참조 [Active Directory Domain Services (AD DS) Virtualization (수준을 100) 소개](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)합니다. DC 작동 복제 가상화 방법에 대 한 세부 정보에 대 한 참고 [가상화 도메인 컨트롤러 기술 참조 (300 수준)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md)합니다.  

-   [광고 숲 복구 필수](AD-Forest-Recovery-Prerequisties.md)  
-   [사용자 지정 숲 복구 계획 고안-광고 숲 복구](AD-Forest-Recovery-Devising-a-Plan.md)  
- [광고 숲 복구-문제 식별](AD-Forest-Recovery-Identify-the-Problem.md)
-   [광고 숲 복구-복구 하는 방법을 확인](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [광고 숲 복구-초기 복구](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)  
-   [광고 숲 복구-질문과 대답](AD-Forest-Recovery-FAQ.md)  
-   [광고 숲 복구-Multidomain 숲 내 단일 도메인 복구](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [광고 숲 복구-Windows Server 2003 도메인 컨트롤러 관련 숲 복구](AD-Forest-Recovery-Windows-Server-2003.md) 

  
