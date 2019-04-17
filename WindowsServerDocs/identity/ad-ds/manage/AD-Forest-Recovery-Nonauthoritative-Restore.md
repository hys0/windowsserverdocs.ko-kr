---
title: "광고 숲 복구 신뢰할 수 없는 상태로 복원"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adfs
ms.openlocfilehash: 684672491a0574b12e9b117a8e3c9c1f0936f357
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>신뢰할 수의 Active Directory Domain Services 복원을 수행 

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.
 
 메시지를 신뢰할 수 없는 상태로 복원 하려면 다음 단계를 수행 합니다.  
  
 다음 절차 Wbadmin.exe Active Directory 또는 Active Directory Domain Services (AD DS) 신뢰할 복원을 수행 하려면 사용 합니다. 다른 백업 솔루션을 사용 하는 경우 또는 숲 복구 과정에서 나중에 sysvol 신뢰할 수 있는 복원 하려는 경우 다음 다른 방법 사용 하 여 sysvol 정식 복원을 수행할 수 있습니다.  
  
-   파일 FRS (복제 서비스)를 SYSVOL 복제할를 사용 하는 경우의 단계를 따릅니다 [290762 문서](https://go.microsoft.com/fwlink/?LinkId=148443) Microsoft 기술 자료, 사용 하는 **BurFlags** FRS 복제 세트 다시 초기화 하거나, 필요한 경우 문서 레지스트리 키 315457 [315457](https://support.microsoft.com/kb/315457)SYSVOL 밤나무 다시 합니다. 확인 하려면 FRS SYSVOL를 복제 하는 경우 참조 하십시오 [결정 여부는 도메인 컨트롤러의 SYSVOL 폴더는 DFSR 또는 FRS 복제](https://msdn.microsoft.com/en-us/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs)합니다.  
  
-   (분산 파일 시스템) 복제 SYSVOL 복제할를 사용 하는 경우 참조 [sysvol DFSR 복제 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)합니다.  
  
 
## <a name="performing-a-nonauthoritative-restore"></a>신뢰할 수 없는 복원을 수행  
 다음 절차를 사용 하 여 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008 실행 dc wbadmin.exe를 사용 하 여 권한 없는 복원 AD DS의 및 동시에 sysvol 신뢰할 수 있는 복원 수행할 수 있습니다. 백업을은 명시적으로 시스템 상태 데이터를 포함 해야 전체 서버에 사용 되는 완전 서버 백업이 작동 하지 않습니다. 시스템 상태 백업을 만드는 데 대 한 자세한 내용은 참조 [시스템 상태 데이터를 백업](AD-Forest-Recovery-Backing-up-System-State.md)합니다.  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>수행 하려면 sysvol wbadmin.exe를 사용 하 여 권한 없는 복원 AD DS 고 신뢰할 수 있는 복원  
  
-   포함는 **-authsysvol** 복구 명령에서 전환 다음과 같이 합니다.  
  
    ```  
    wbadmin start systemstaterecovery <otheroptions> -authsysvol  
    ```  
  
     예를 들어:  
  
    ```  
    wbadmin start systemstaterecovery -version:11/20/2012-13:00 -authsysvol  
    ```  
  
 ![복원](media/AD-Forest-Recovery-Nonauthoritative-Restore/nonauth.png)

## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
