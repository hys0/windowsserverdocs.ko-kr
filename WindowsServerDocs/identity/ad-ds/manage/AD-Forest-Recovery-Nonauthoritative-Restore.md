---
title: AD 포리스트 복구-비정식 복원
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: e4ce1d18-d346-492a-8bca-f85513aa3ac1
ms.technology: identity-adds
ms.openlocfilehash: d7792cd739931d758125c8946606beb043ce19dd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369094"
---
# <a name="performing-a-nonauthoritative-restore-of-active-directory-domain-services"></a>Active Directory Domain Services의 비정식 복원 수행 

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

비정식 복원 작업을 수행 하려면 다음 절차를 완료 합니다.  
  
다음 절차에서는 stsadm.exe를 사용 하 여 Active Directory 또는 Active Directory Domain Services (AD DS)의 비정식 복원을 수행 합니다. 다른 백업 솔루션을 사용 하 고 있거나 나중에 포리스트 복구 프로세스에서 SYSVOL의 정식 복원을 완료 하려는 경우 다음과 같은 대체 방법을 사용 하 여 SYSVOL의 신뢰할 수 있는 복원을 수행할 수 있습니다.  
  
- FRS (파일 복제 서비스)를 사용 하 여 SYSVOL을 복제 하는 경우 Microsoft 기술 자료 [문서 290762](https://go.microsoft.com/fwlink/?LinkId=148443) 의 단계에 따라 **BurFlags** 레지스트리 키를 사용 하 여 frs 복제 세트를 다시 초기화 하거나 필요한 경우 문서 315457 [ 315457](https://support.microsoft.com/kb/315457)-SYSVOL 트리를 다시 작성 합니다. SYSVOL이 FRS에 의해 복제 되는지 확인 하려면 [도메인 컨트롤러의 SYSVOL 폴더가 DFSR 또는 FRS에 의해 복제 되었는지](https://msdn.microsoft.com/library/windows/desktop/cc507518.aspx#determining_whether_a_domain_controller_s_sysvol_folder_is_replicated_by_dfsr_or_frs)확인을 참조 하세요.  
- DFS (분산 파일 시스템) 복제를 사용 하 여 SYSVOL을 복제 하는 경우 [DFSR 복제 sysvol의 신뢰할 수 있는 동기화 수행](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)을 참조 하세요.  

## <a name="performing-a-nonauthoritative-restore"></a>비정식 복원 수행

다음 절차를 사용 하 여 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008를 실행 하는 DC에서 tcm.exe를 사용 하 여 동시에 AD DS 및 SYSVOL의 신뢰할 수 있는 복원을 수행할 수 있습니다. 백업은 시스템 상태 데이터를 명시적으로 포함 해야 합니다. 전체 서버 복구에 사용 되는 전체 서버 백업이 작동 하지 않습니다. 시스템 상태 백업을 만드는 방법에 대 한 자세한 내용은 [시스템 상태 데이터](AD-Forest-Recovery-Backing-up-System-State.md)백업을 참조 하세요.  
  
### <a name="to-perform-a-nonauthoritative-restore-of-ad-ds-and-authoritative-restore-of-sysvol-using-wbadminexe"></a>Stsadm.exe를 사용 하 여 AD DS 및 SYSVOL의 정식 복원에 대 한 신뢰할 수 없는 복원을 수행 하려면  
  
- 다음 예제와 같이 recovery 명령에 **-authsysvol** 스위치를 포함 합니다.  

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
