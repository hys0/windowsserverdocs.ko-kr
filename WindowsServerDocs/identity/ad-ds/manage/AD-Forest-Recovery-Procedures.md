---
title: AD 포리스트 복구 - 절차
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.technology: identity-adds
ms.openlocfilehash: 0d427448c8d2a6616b87a524bcc941fc8555cbd4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390315"
---
# <a name="ad-forest-recovery---procedures"></a>AD 포리스트 복구 - 절차

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

이 섹션에는 포리스트 복구 프로세스와 관련 된 절차가 포함 되어 있습니다. 이 절차는 Windows Server 2016, 2012 R2, 2012에 적용 되며 몇 가지 사소한 예외가 있는 Windows Server 2008 R2 및 2008에도 적용 됩니다.

Windows Server 2003에 따라 달라 지는 단계를 포함 하는 절차는 [Windows server 2003 도메인 컨트롤러를 사용 하 여 포리스트 복구](AD-Forest-Recovery-Windows-Server-2003.md)에 있습니다.  

다음은 도메인 컨트롤러를 백업 및 복원 하 고 Active Directory 하는 데 사용 되는 절차 목록입니다.

- [전체 서버 백업](AD-Forest-Recovery-Backing-up-a-Full-Server.md)  
- [시스템 상태 데이터 백업](AD-Forest-Recovery-Backing-up-System-State.md)  
- [전체 서버 복구 수행](AD-Forest-Recovery-Perform-a-Full-Recovery.md)  
- [DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
- [Active Directory Domain Services의 비정식 복원 수행](AD-Forest-Recovery-Nonauthoritative-Restore.md)  

이러한 단계에서는 SYSVOL의 신뢰할 수 있는 복원을 동시에 수행 하는 방법을 설명 합니다.  

- [DNS 서버 서비스 구성](AD-Forest-Recovery-Configure-DNS.md)  
- [글로벌 카탈로그 제거](AD-Forest-Recovery-Remove-GC.md)  
- [사용 가능한 RID 풀의 값을 거듭제곱 합니다.](AD-Forest-Recovery-Raise-RID-Pool.md)  
- [현재 RID 풀을 무효화 합니다.](AD-Forest-Recovery-Invaildate-RID-Pool.md)  
- [작업 마스터 역할 점유](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)  
- [복원 후 정리](AD-Forest-Recovery-Cleanup.md)
- [제거 된 쓰기 가능 도메인 컨트롤러의 메타 데이터 정리](AD-Forest-Recovery-Cleaning-Metadata.md)  
- [도메인 컨트롤러의 컴퓨터 계정 암호를 다시 설정 하는 중](AD-Forest-Recovery-Reset-Computer-Account-DC.md)  
- [Krbtgt 암호 다시 설정](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)  
- [트러스트의 한 쪽에서 트러스트 암호 다시 설정](AD-Forest-Recovery-Reset-Trust.md)  
- [글로벌 카탈로그 추가](AD-Forest-Recovery-Add-GC.md)  
- [복제가 작동 하는지 확인 하기 위한 리소스](AD-Forest-Recovery-Verify-Replication.md)  

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
