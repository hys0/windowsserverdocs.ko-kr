---
title: DNS 영역에 대한 액세스 범위 설정
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6155cee3f1924486f1358632dcef2fba7046edb3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355131"
---
# <a name="set-access-scope-for-a-dns-zone"></a>DNS 영역에 대한 액세스 범위 설정

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔을 사용 하 여 DNS 영역에 대 한 액세스 범위를 설정할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-set-the-access-scope-for-a-dns-zone"></a>DNS 영역에 대 한 액세스 범위를 설정 하려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서 **DNS 영역**을 클릭 합니다. 디스플레이 창에서 액세스 범위를 변경할 DNS 영역을 마우스 오른쪽 단추로 클릭 한 다음 **액세스 범위 설정**을 클릭 합니다.  
  
    ![액세스 범위 설정](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)  
  
3.  **액세스 범위 설정** 대화 상자가 열립니다. 배포에 필요한 경우 **부모에서 액세스 범위 상속**을 클릭 하 여 선택 취소 합니다. **액세스 범위 선택**에서 항목을 선택 하 고 **확인**을 클릭 합니다.  
  
    ![액세스 범위 선택](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)  
  
4.  IPAM 클라이언트 콘솔 디스플레이 창에서 영역에 대 한 액세스 범위가 변경 되었는지 확인 합니다.  
  
    ![영역에 대 한 액세스 범위가 변경 되었는지 확인 합니다.](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)  
  
## <a name="see-also"></a>관련 항목  
[역할 기반 Access Control](Role-based-Access-Control.md)  
[IPAM 관리](Manage-IPAM.md)  
  


