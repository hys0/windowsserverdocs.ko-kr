---
title: AD 포리스트 복구-신뢰할 수 없는 복원
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adds
ms.openlocfilehash: 65e33e6507d2affc4d07cc0780a7baf91a170a09
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280584"
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Active Directory Domain Services의 권한 없는 복원 수행 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

신뢰할 수 없는 복원을 수행 하려면 다음 절차를 완료 합니다.  
  
다음 절차는 Active Directory 또는 Active Directory Domain Services (AD DS)의 신뢰할 수 없는 복원을 수행 하는 Wbadmin.exe를 사용 합니다. 다른 백업 솔루션을 사용 하는 경우, 전체 포리스트 복구 프로세스의 뒷부분에 나오는 SYSVOL의 신뢰할 수 있는 복원 하려는 경우에 이러한 대체 방법을 사용 하 여 SYSVOL의 신뢰할 수 있는 복원 하는 경우를 수행할 수 있습니다.  
  
- 를 사용 하 SYSVOL을 복제 하려면 복제 서비스 FRS (파일)를 사용 하는 경우의 단계에 따라 [290762 문서](https://go.microsoft.com/fwlink/?LinkId=148443) Microsoft 기술 자료에서 사용 하는 **BurFlags** FRS 복제를 다시 초기화 하려면 레지스트리 키 설정 하거나 필요한 경우 문서 315457 [315457](https://support.microsoft.com/kb/315457)SYSVOL 트리를 다시 작성 해야 합니다. FRS가 SYSVOL은 복제 하는 경우를 확인 하려면 참조 [DFSR 또는 FRS 확인 여부는 도메인 컨트롤러의 SYSVOL 폴더를 복제](https://msdn.microsoft.com/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs)합니다.  
- 분산 파일 시스템 (DFS) 복제 SYSVOL을 복제 하려면를 사용 하는 경우 참조 [DFSR 복제 SYSVOL의 신뢰할 수 있는 동기화가 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.  

## <a name="performing-a-nonauthoritative-restore"></a>신뢰할 수 없는 복원을 수행합니다.

Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008을 실행 하는 DC에서 wbadmin.exe를 사용 하 여 AD DS의 신뢰할 수 없는 복원 및 동시 SYSVOL의 정식 복원을 수행 하려면 다음 절차를 따르십시오. 백업에서 시스템 상태 데이터를 명시적으로 포함 해야 전체 서버 복구에 사용 되는 전체 서버 백업 작동 하지 않습니다. 시스템 상태 백업을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [시스템 상태 데이터를 백업](AD-Forest-Recovery-Backing-up-System-State.md)합니다.  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>AD ds 및 신뢰할 수 있는 신뢰할 수 없는 복원을 수행 하려면 wbadmin.exe를 사용 하 여 SYSVOL의 복원  
  
- 포함 된 **-authsysvol** 다음 예와에서 같이 복구 명령에 전환:  

   ```  
   wbadmin start systemstaterecovery <otheroptions> -authsysvol  
   ```  

   예를 들어 다음과 같은 가치를 제공해야 합니다.  

   ```  
   wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol  
   ```  
  
![복원](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
