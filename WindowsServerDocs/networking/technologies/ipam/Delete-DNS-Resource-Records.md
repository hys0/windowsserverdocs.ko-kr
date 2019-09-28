---
title: DNS 리소스 레코드 삭제
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 366e6fd5-d563-4de3-9551-5614cbb8f2cb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fcaaf89989a44cc7a0e84e296ce16083fe021577
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405661"
---
# <a name="delete-dns-resource-records"></a>DNS 리소스 레코드 삭제

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔을 사용 하 여 하나 이상의 DNS 리소스 레코드를 삭제할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-delete-dns-resource-records"></a>DNS 리소스 레코드를 삭제 하려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서에서 **모니터링 및 관리**, 를 클릭 하 여 **DNS 영역**합니다.  탐색 창 위쪽 탐색 창 및 아래쪽 탐색 창으로 나눕니다.  
  
3.  앞으로 조회를 클릭 하 여 삭제 하려는 영역 및 리소스 레코드가 있는 도메인 및 **앞으로 조회** 를 확장 합니다. 영역을 클릭 하 고 디스플레이 창에서 **현재 보기**를 클릭 합니다. **리소스 레코드**를 클릭 합니다.  
  
4.  디스플레이 창에서 삭제 하려는 리소스 레코드를 찾아 선택 합니다.  
  
    ![삭제할 리소스 레코드 선택](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_01.jpg)  
  
5.  선택한 레코드를 마우스 오른쪽 단추로 클릭 한 다음 **DNS 리소스 레코드 삭제**를 클릭 합니다.  
  
    ![레코드 삭제](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_02.jpg)  
  
6.  **DNS 리소스 레코드 삭제** 대화 상자가 열립니다. 올바른 DNS 서버가 선택 되었는지 확인 합니다. 그렇지 않으면 **DNS 서버** 를 클릭 하 고 리소스 레코드를 삭제 하려는 서버를 선택 합니다. **확인**을 클릭합니다. IPAM이 DNS 서버에서 리소스 레코드를 삭제 합니다.  
  
    ![올바른 DNS 서버가 선택 되어 있는지 확인 하 고 레코드를 삭제 합니다.](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_03.jpg)  
  
## <a name="see-also"></a>관련 항목  
[DNS 리소스 레코드 관리](DNS-Resource-Record-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


