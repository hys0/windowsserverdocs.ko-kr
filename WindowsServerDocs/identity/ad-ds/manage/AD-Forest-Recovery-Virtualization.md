---
title: AD 포리스트 복구 가상화
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: 23317f55fdce18e78ac3e7e1490f6fc4937fd062
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858454"
---
# <a name="active-directory-forest-recovery-virtualization"></a>Active Directory 포리스트 복구 가상화

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 항목에서는 Windows Server 2016, 2012 R2 및 2012에서 가상화 된 도메인 컨트롤러 복제 기능을 설명 합니다.  

## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>가상화 된 도메인 컨트롤러 복제를 사용 하 여 포리스트 복구를 신속 하 게

가상화 된 도메인 컨트롤러 (DC) 복제 간소화 하 고 여러 Dc 하이퍼바이저에서 실행 되는 경우 데이터 센터와 같은 중앙된 위치에 특히 도메인에 추가 가상화 된 Dc를 설치 하기 위한 프로세스 속도 높여 줍니다. 백업에서 각 도메인에 가상 DC가 하나를 복원한 후 각 도메인에 추가 Dc 수 신속 하 게 온라인 상태로 만들 수는 가상화 된 DC 복제 프로세스를 사용 하 여 합니다. 복구, 종료 및 다음 복사 하는 첫 번째 가상화 된 DC를 준비할 수 있으므로 해당 가상 하드 디스크를 순서 대로 하는 데 필요한 만큼 여러 번 만들 복제 가상화 도메인을 구축 하는 Dc입니다.  
  
가상화 된 DC 복제에 대 한 요구 사항은 다음과 같습니다.  
  
- 하이퍼바이저는 Vm-generationid를 지원 해야 합니다. Windows Server 2016, 2012의에서 Hyper-v 및 Windows 8은 Vm-generationid를 지 원하는 하이퍼바이저의 예입니다. Vm-generationid를 지원 되는 경우 하이퍼바이저 공급 업체를 사용 하 여 확인 합니다.  
- 복제 원본으로 사용 되는 가상화 된 DC는 Windows Server 2016 또는 2012를 실행 하 고 복제 가능 도메인 컨트롤러 그룹의 구성원 이어야 해야 합니다. 
- PDC 에뮬레이터 Windows Server 2016 또는 2012를 실행 해야 합니다. 가상화 된 경우 PDC 에뮬레이터를 복제할 수 있습니다.  
  
수행 하는 방법에 대 한 단계별 지침은 가상화 DC 복제에 대 한 참조 [Introduction to Active Directory Domain Services (AD DS) Virtualization (Level 100)](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)합니다. 가상화 DC 복제 작동 방법에 대 한 세부 정보 참조 [가상화 된 도메인 컨트롤러 기술 참조 (수준 300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md)합니다. 

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
