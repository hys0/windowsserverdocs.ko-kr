---
title: AD 포리스트 복구 가상화
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: c49b40b2-598d-49aa-85b4-766bce960e0d
ms.technology: identity-adds
ms.openlocfilehash: 9e99b6ab5deadf0f3499e4764cdb87b2ed3d65f9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823376"
---
# <a name="active-directory-forest-recovery-virtualization"></a>Active Directory 포리스트 복구 가상화

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 항목에서는 Windows Server 2016, 2012 R2 및 2012의 가상화 된 도메인 컨트롤러 복제 기능에 대해 설명 합니다.  

## <a name="using-virtualized-domain-controller-cloning-to-expedite-forest-recovery"></a>가상화 된 도메인 컨트롤러 복제를 사용 하 여 포리스트 복구 가속화

가상화 된 DC (도메인 컨트롤러) 복제는 도메인에 추가 가상화 된 Dc를 설치 하는 프로세스를 간소화 하 고 신속 하 게 수행 합니다. 특히 여러 Dc가 하이퍼바이저에서 실행 되는 데이터 센터와 같은 중앙 위치에 있습니다. 각 도메인의 한 가상 DC를 백업에서 복원한 후에는 가상화 된 DC 복제 프로세스를 사용 하 여 각 도메인의 추가 Dc를 빠르게 온라인으로 전환할 수 있습니다. 복구 하는 첫 번째 가상화 된 DC를 준비 하 고 종료 한 다음, 해당 가상 하드 디스크를 복제 된 가상화 된 Dc를 만들어 도메인을 빌드하기 위해 필요한 만큼 복사할 수 있습니다.  
  
가상화 된 DC 복제에 대 한 요구 사항은 다음과 같습니다.  
  
- 하이퍼바이저는 VM-Vm-generationid을 지원 해야 합니다. Windows Server 2016, 2012 및 Windows 8의 hyper-v는 VM Vm-generationid을 지 원하는 하이퍼바이저의 예입니다. Vm-generationid가 지원 되는 경우 하이퍼바이저 공급 업체에 문의 하세요.  
- 복제의 원본으로 사용 되는 가상화 된 DC는 Windows Server 2016 또는 2012를 실행 해야 하며 복제 가능 도메인 컨트롤러 그룹의 구성원 이어야 합니다. 
- PDC 에뮬레이터는 Windows Server 2016 또는 2012를 실행 해야 합니다. PDC 에뮬레이터가 가상화 된 경우 복제할 수 있습니다.  
  
가상화 된 DC 복제를 수행 하는 방법에 대 한 단계별 지침은 [Active Directory Domain Services (AD DS) 가상화 소개 (수준 100)](../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)를 참조 하세요. 가상화 된 DC 복제가 작동 하는 방법에 대 한 자세한 내용은 [가상화 된 도메인 컨트롤러 기술 참조 (수준 300)](../deploy/virtual-dc/virtualized-domain-controller-technical-reference--level-300-.md)를 참조 하세요. 

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
