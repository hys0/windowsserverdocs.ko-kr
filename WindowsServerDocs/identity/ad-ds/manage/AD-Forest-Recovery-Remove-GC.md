---
title: AD 포리스트 복구-글로벌 카탈로그 제거
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adds
ms.openlocfilehash: d730ce65fc179aee6a98f7cfc1a5b693bfcd6c93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817074"
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>AD 포리스트 복구-글로벌 카탈로그를 제거 합니다.  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 글로벌 카탈로그 DC를 제거 하려면 다음 절차를 따르십시오. 
  
 부분 해당 복제본에 대 한 권한이 있는 해당 도메인이 아닌 일부 복제본 중 하나에 대 한 최신 데이터를 포함 하는 글로벌 카탈로그에서 글로벌 카탈로그 서버를 백업에서 복원 될 수 있습니다. 이 경우 최신 데이터는 글로벌 카탈로그에서 제거 되지 않습니다 하 고 다른 글로벌 카탈로그 서버가 복제도 않을 수 있습니다. 결과적으로, DC는 글로벌 카탈로그 서버를 하거나 실수로 복원 하지 못했습니다 또는 독립 백업 기 때문에 사용자를 신뢰 하는 경우에 복원 작업이 완료 된 직후에 글로벌 카탈로그를 제거 해야 합니다. 글로벌 카탈로그 제거 되 면 컴퓨터의 모든 부분 복제본을 제거 합니다. 
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>Active Directory 사이트 및 서비스를 사용 하 여 글로벌 카탈로그를 제거 하려면  
 
1. 서버 관리자를 열고 **도구가** 클릭 **Active Directory 사이트 및 서비스**합니다. 
2. 콘솔 트리에서 확장 된 **사이트** 컨테이너 및 대상 서버를 포함 하는 적절 한 사이트를 선택 합니다. 
3. 확장을 **서버** 컨테이너를 펼친 다음는 *서버* 글로벌 카탈로그를 제거 하려는 DC에 대 한 개체입니다. 
4. 마우스 오른쪽 단추로 클릭 **NTDS 설정**를 클릭 하 고 **속성**합니다. 
5. 선택을 취소 합니다 **글로벌 카탈로그** 확인란 합니다. 
   ![GC를 제거 합니다.](media/AD-Forest-Recovery-Remove-GC/removegc1.png)
6. **적용**을 클릭합니다.
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>Repadmin을 사용 하 여 글로벌 카탈로그를 제거 하려면  
  
관리자 권한 명령 프롬프트를 열고, 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

   ```
   repadmin.exe /options DC_NAME –IS_GC  
   ```  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 절차](AD-Forest-Recovery-Procedures.md)
