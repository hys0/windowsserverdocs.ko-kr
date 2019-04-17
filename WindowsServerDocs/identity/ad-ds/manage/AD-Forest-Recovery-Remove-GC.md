---
title: "광고 숲 복구 드 제거"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adfs
ms.openlocfilehash: b7da7c03cbae4691e8f902f1be0cb33c0c912248
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>광고 숲 복구-드 제거  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 다음 절차를 사용 하 여 드 DC에서 제거 합니다.  
  
 드 서버 백업에서 복원 드 부분 복제 그에 대 한 권한이 해당 도메인 보다 부분 복제 그 중 하나에 대 한 최신 데이터만 될 수 있습니다. 이러한 경우 최신 데이터 드에서 제거 되지 않습니다 및 다른 드 서버에도 복제 수 있습니다. 결과적으로, 된 드 서버 하거나 실수로 DC 복원 무엇 또는 신뢰할 수 있는 벡 백업 때문에, 하는 경우에 복원 작업이 완료 된 후에 곧 드를 제거 해야 합니다. 드 제거 되 면 컴퓨터의 모든 부분 복제 제거 합니다.  
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>드 Active Directory 사이트 및 서비스를 사용 하 여 제거 하려면  
 
1.  서버 관리자를 열을 클릭 **도구** 클릭 **Active Directory 사이트 및 서비스**합니다.  
2.  콘솔 트리에서 확장는 **사이트** 컨테이너 및 대상 서버를 포함 하는 해당 사이트를 선택 합니다.  
3.  확장은 **서버** 컨테이너, 다음를 확장 하 고 있는 *서버* 드 제거 하려는 DC 대 한 합니다.  
4.  마우스 오른쪽 단추로 클릭 **NTDS 설정**을 차례로 클릭 하 고 **속성**합니다.  
5.  지우기는 **드** 확인란을 선택 합니다.  
![GC 제거](media/AD-Forest-Recovery-Remove-GC/removegc1.png)
6.  클릭 **적용**합니다.
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>드 Repadmin를 사용 하 여 제거 하려면  
  
1.  관리자 명령 프롬프트를 열고 다음 명령을 입력 하 ENTER 키를 누릅니다.  
  
    ```  
    repadmin.exe /options DC_NAME –IS_GC  
    ```  
  
 ## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
