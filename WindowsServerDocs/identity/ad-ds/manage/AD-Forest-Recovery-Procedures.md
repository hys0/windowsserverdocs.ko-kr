---
title: AD 포리스트 복구 - 절차
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.technology: identity-adds
ms.openlocfilehash: da45e3b20c370a2a37b0eab31a78216434dd60be
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827724"
---
# <a name="ad-forest-recovery---procedures"></a>AD 포리스트 복구 - 절차

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 섹션에서는 프로세스와 관련 된 포리스트 복구 절차를 포함 합니다. 절차에 적용할 수 있습니다 Windows Server 2016, 2012 R2, 2012 및 Windows Server 2008 R2 및 몇 가지 사소한 예외를 사용 하 여 2008에 해당 됩니다.

Windows Server 2003에 대 한 변화 하는 단계를 포함 하는 프로시저에 포함 됩니다 [Windows Server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)합니다.  

다음은 백업 및 복원 하는 도메인 컨트롤러와 Active Directory에서 사용 되는 프로시저의 목록입니다.

- [전체 서버 백업](AD-Forest-Recovery-Backing-up-a-Full-Server.md)  
- [시스템 상태 데이터 백업](AD-Forest-Recovery-Backing-up-System-State.md)  
- [전체 서버 복구를 수행합니다.](AD-Forest-Recovery-Perform-a-Full-Recovery.md)  
- [DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화를 수행합니다.](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
- [Active Directory Domain Services의 권한 없는 복원 수행](AD-Forest-Recovery-Nonauthoritative-Restore.md)  

이러한 단계는 동시에 SYSVOL의 정식 복원을 수행 하는 방법을 설명 합니다.  

- [DNS 서버 서비스 구성](AD-Forest-Recovery-Configure-DNS.md)  
- [글로벌 카탈로그를 제거합니다.](AD-Forest-Recovery-Remove-GC.md)  
- [사용 가능한 RID 풀의 값을 발생 시키기](AD-Forest-Recovery-Raise-RID-Pool.md)  
- [현재 RID 풀 무효화](AD-Forest-Recovery-Invaildate-RID-Pool.md)  
- [작업 마스터 역할 점유](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)  
- [복원 후 정리](AD-Forest-Recovery-Cleanup.md)
- [제거 쓰기 가능한 도메인 컨트롤러의 메타 데이터를 정리합니다.](AD-Forest-Recovery-Cleaning-Metadata.md)  
- [도메인 컨트롤러의 컴퓨터 계정 암호를 다시 설정](AD-Forest-Recovery-Reset-Computer-Account-DC.md)  
- [Krbtgt 암호 재설정](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)  
- [트러스트의 한 쪽에서 트러스트 암호를 재설정](AD-Forest-Recovery-Reset-Trust.md)  
- [글로벌 카탈로그 추가](AD-Forest-Recovery-Add-GC.md)  
- [복제가 작동을 확인 하려면 리소스](AD-Forest-Recovery-Verify-Replication.md)  

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
