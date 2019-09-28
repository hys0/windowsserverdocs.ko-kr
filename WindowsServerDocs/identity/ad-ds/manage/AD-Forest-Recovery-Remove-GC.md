---
title: AD 포리스트 복구-글로벌 카탈로그 제거
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adds
ms.openlocfilehash: 3ba1336828ad6031ce7fb47a659d084494466e4a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71409094"
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>AD 포리스트 복구-글로벌 카탈로그 제거  

>적용 대상: Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 R2

 다음 절차를 사용 하 여 DC에서 글로벌 카탈로그를 제거할 수 있습니다. 
  
 백업에서 글로벌 카탈로그 서버를 복원 하면 해당 부분 복제본에 대 한 권한이 있는 해당 도메인 보다는 글로벌 카탈로그가 해당 부분 복제본 중 하나에 대 한 최신 데이터를 보유할 수 있습니다. 이 경우 새 데이터는 글로벌 카탈로그에서 제거 되지 않으며 다른 글로벌 카탈로그 서버에도 복제할 수 있습니다. 따라서 글로벌 카탈로그 서버인 DC를 실수로 또는 신뢰할 수 있는 독립 백업으로 복원한 경우에도 복원 작업을 완료 한 후에는 글로벌 카탈로그를 즉시 제거 해야 합니다. 글로벌 카탈로그가 제거 되 면 컴퓨터는 모든 부분 복제본을 제거 합니다. 
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>Active Directory 사이트 및 서비스를 사용 하 여 글로벌 카탈로그를 제거 하려면  
 
1. 서버 관리자 열고 **도구** 를 클릭 한 다음 **Active Directory 사이트 및 서비스**를 클릭 합니다. 
2. 콘솔 트리에서 **사이트** 컨테이너를 확장 하 고 대상 서버가 포함 된 적절 한 사이트를 선택 합니다. 
3. **서버** 컨테이너를 확장 한 다음 글로벌 카탈로그를 제거할 DC에 대 한 *서버* 개체를 확장 합니다. 
4. **NTDS 설정**을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다. 
5. **글로벌 카탈로그** 확인란의 선택을 취소 합니다. 
   ![Remove GC @ no__t-1
6. **적용**을 클릭합니다.
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>Repadmin을 사용 하 여 글로벌 카탈로그를 제거 하려면  
  
관리자 권한 명령 프롬프트를 열고 다음 명령을 입력 하 고 ENTER 키를 누릅니다.  

   ```
   repadmin.exe /options DC_NAME –IS_GC  
   ```  

## <a name="next-steps"></a>다음 단계

- [AD 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [AD 포리스트 복구 - 절차](AD-Forest-Recovery-Procedures.md)
