---
title: DNS 영역 편집
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2175cf9c740d7b727ba017922a77c94d4379c891
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355281"
---
# <a name="edit-a-dns-zone"></a>DNS 영역 편집

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔에서 DNS 영역을 편집할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-edit-a-dns-zone"></a>DNS 영역을 편집 하려면  
  
1.  서버 관리자에서 **IPAM**을 클릭 합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서에서 **모니터링 및 관리**, 를 클릭 하 여 **DNS 영역**합니다. 탐색 창 위쪽 탐색 창 및 아래쪽 탐색 창으로 나눕니다.  
  
3.  아래쪽 탐색 창에서 다음 중 하나를 선택 합니다.  
  
    -   전방 조회  
  
    -   IPv4 역방향 조회  
  
    -   IPv6 역방향 조회  
  
4.  예를 들어 IPv4 역방향 조회를 선택 합니다.  
  
    ![영역 유형 선택](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)  
  
5.  디스플레이 창에서 편집 하려는 영역을 마우스 오른쪽 단추로 클릭 한 다음 **DNS 영역 편집**을 클릭 합니다.  
  
    ![DNS 영역 편집](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)  
  
6.  **일반** 페이지가 선택 된 상태에서 **DNS 영역 편집** 대화 상자가 열립니다. 필요한 경우 일반 영역 속성을 편집 합니다. **DNS 서버**, **영역 범주**및 **영역 유형을 입력**한 다음 **적용** 을 클릭 하거나, 편집이 완료 되 면 **확인**을 클릭 합니다.  
  
    ![영역 속성 편집 및 저장](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)  
  
7.  **DNS 영역 편집** 대화 상자에서 **고급**을 클릭 합니다. **고급** 영역 속성 페이지가 열립니다. 필요한 경우 변경할 속성을 편집한 다음 **적용** 을 클릭 하거나, 편집이 완료 되 면 **확인**을 클릭 합니다.  
  
    ![고급 영역 속성 편집](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)  
  
8.  필요한 경우 추가 영역 속성 페이지 이름 (이름 서버, SOA, 영역 전송)을 선택 하 고 편집을 수행한 다음 **적용** 또는 **확인**을 클릭 합니다. 모든 영역 편집 내용을 검토 하려면 **요약**을 클릭 한 다음 **확인**을 클릭 합니다.  
  
## <a name="see-also"></a>관련 항목  
[DNS 영역 관리](DNS-Zone-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


