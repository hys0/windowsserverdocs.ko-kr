---
title: "광고 숲 복구 sysvol 신뢰할 수 있는 동기화"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.technology: identity-adfs
ms.openlocfilehash: 5bdc619ddf9f28fb074e90dfbf22a7be076a05d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>광고 숲 복구-DFSR 복제 sysvol 신뢰할 수 있는 동기화  

>Windows Server 2016, Windows Server 2012 및 2012 R2, Windows Server 2008 및 2008 r 2에 적용 됩니다.

 여러 가지 방법으로 sysvol 정식 복원을 수행할 수 있습니다. 어느 편집 수는 **msDFSR 옵션** 특성 또는 wbadmin – authsysvol를 사용 하 여 상태 시스템 복원을 수행 합니다. 시스템 상태 백업을 복원 하는 옵션 있는 경우 (즉, 복원 하는 AD DS 같은 하드웨어 및 운영 체제 인스턴스를) wbadmin-authsysvol 사용이 더 간단 합니다. 앙상한 금속 복원을 수행 해야 다음 편집 해야 하지만 **msDFSR 옵션** 특성 합니다.  
  
 동기화를 수행 하는 신뢰할 수 있는 sysvol (DFSR를 사용 하 여 복제) 하는 경우 다음 단계를 사용 하 여 편집 하 여는 **msDFSR 옵션** 특성 합니다. SYSVOL FRS 사용 하 여 복제, 경우 [290762 문서](https://go.microsoft.com/fwlink/?LinkId=148443)합니다.  
  
## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>신뢰할 수 있는 동기화 DFSR 복제 sysvol 수행을  
  
1.  Active Directory 사용자와 컴퓨터를 엽니다.  
2.  클릭 **보기**를 선택한 다음 **사용자가, 연락처, 그룹 및 컨테이너 컴퓨터** 및 **고급 기능**합니다. 
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png) 
3.  나무 보기를 클릭 **도메인 컨트롤러**, DC 복원 사용자의 이름 **DFSR LocalSettings**를 선택한 다음 **도메인 시스템 볼륨**합니다. 
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)  
4.  세부 정보 창에서 마우스 오른쪽 단추로 클릭 **SYSVOL 구독**, 클릭 **속성**를 클릭 하 고 **특성 편집기**합니다.  
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png) 
5.  클릭 **msDFSR 옵션**, 클릭 **편집**, 입력 **1**를 클릭 하 고 **확인**  
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png) 
6.  클릭 **확인** 특성 편집기를 닫습니다.  
  
## <a name="next-steps"></a>다음 단계

- [광고 포리스트 복구 가이드](AD-Forest-Recovery-Guide.md)
- [광고 숲 복구 절차](AD-Forest-Recovery-Procedures.md)
