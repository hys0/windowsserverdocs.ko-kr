---
title: "광고 숲 복구 절차"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.technology: identity-adfs
ms.openlocfilehash: 91e3954c05fe3cd12d35b5db91afd29fb3a31e00
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2017
---
# <a name="ad-forest-recovery---procedures"></a>광고 숲 복구 절차


>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

This section contains procedures related to the forest recovery process. The procedures are applicable for Windows Server 2016, 2012 R2, 2012 and are also applicable to Windows Server 2008 R2 and 2008 with some minor exceptions. 

Procedures that include steps that vary for Windows Server 2003 are found in [Forest Recovery with Windows Server 2003 Domain Controllers](AD-Forest-Recovery-Windows-Server-2003.md).  

The following is a list of procedures that are used in backing up and restoring domain controllers and Active Directory.
  
-   [Backing up a full server](AD-Forest-Recovery-Backing-up-a-Full-Server.md)  
-   [시스템 상태 데이터를 백업](AD-Forest-Recovery-Backing-up-System-State.md)  
-   [Performing a full server recovery](AD-Forest-Recovery-Perform-a-Full-Recovery.md)  
-   [Performing an authoritative synch of DFSR-replicated SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
-   [신뢰할 수의 Active Directory Domain Services 복원을 수행](AD-Forest-Recovery-Nonauthoritative-Restore.md)  
  
     These steps explain how to perform an authoritative restore of SYSVOL at the same time.  
-   [Configuring the DNS Server service](AD-Forest-Recovery-Configure-DNS.md)  
-   [Removing the global catalog](AD-Forest-Recovery-Remove-GC.md)  
-   [Raising the value of available RID pools](AD-Forest-Recovery-Raise-RID-Pool.md)  
-   [Invalidating the current RID pool](AD-Forest-Recovery-Invaildate-RID-Pool.md)  
-   [Seizing an operations master role](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)  
-   [Cleaning up after a restore](AD-Forest-Recovery-Cleanup.md)
-   [Cleaning metadata of removed writable domain controllers](AD-Forest-Recovery-Cleaning-Metadata.md)  
-   [Resetting the computer account password of the domain controller](AD-Forest-Recovery-Reset-Computer-Account-DC.md)  
-   [Resetting the krbtgt password](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)  
-   [한쪽의 보안 신뢰 암호 다시 설정](AD-Forest-Recovery-Reset-Trust.md)  
-   [Adding the global catalog](AD-Forest-Recovery-Add-GC.md)  
-   [복제 작동 하는지 확인 하는 데 리소스](AD-Forest-Recovery-Verify-Replication.md)  
  
  
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
