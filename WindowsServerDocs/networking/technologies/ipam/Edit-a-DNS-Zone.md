---
title: DNS 영역 편집
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b632203289c3affd16735026e0c553be09c5e9e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847444"
---
# <a name="edit-a-dns-zone"></a>DNS 영역 편집

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IPAM 클라이언트 콘솔에서 DNS 영역을 편집 하려면이 항목에서는 사용할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-edit-a-dns-zone"></a>DNS 영역을 편집 하려면  
  
1.  서버 관리자에서 클릭 **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서에서 **모니터링 및 관리**, 를 클릭 하 여 **DNS 영역**합니다. 탐색 창 위쪽 탐색 창 및 아래쪽 탐색 창으로 나눕니다.  
  
3.  아래쪽 탐색 창에서 다음 선택 항목 중 하나를 수행 합니다.  
  
    -   정방향 조회  
  
    -   IPv4 역방향 조회  
  
    -   IPv6 역방향 조회  
  
4.  예를 들어 IPv4 역방향 조회를 선택 합니다.  
  
    ![영역 형식 선택](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)  
  
5.  디스플레이 창에서 편집 하 고 클릭 하려는 영역을 마우스 오른쪽 단추로 **DNS 영역 편집**합니다.  
  
    ![DNS 영역 편집](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)  
  
6.  **편집 DNS 영역** 대화 상자가 열립니다 합니다 **일반** 선택한 페이지입니다. 필요한 경우 일반 영역 속성을 편집 합니다. **DNS 서버**, **영역 범주**, 및 **형식 영역**를 클릭 하 고 **적용** 또는 편집이 완료 되 면 **확인**합니다.  
  
    ![영역 속성 편집 및 저장](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)  
  
7.  에 **Edit DNS 영역** 대화 상자, 클릭 **고급**합니다. 합니다 **고급** 영역 속성 페이지가 열립니다. 필요한 경우 변경 하 고 클릭 하려는 속성을 편집할 **적용** 또는 편집이 완료 되 면 **확인**합니다.  
  
    ![고급 영역 속성 편집](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)  
  
8.  필요한 경우 추가 영역 속성 페이지 이름 (이름 서버, SOA, 영역 전송)를 선택, 편집을 확인 하 고 클릭 **Apply** 하거나 **확인**합니다. 모든 영역 변경 작업을 검토 하려면 클릭 **요약**를 클릭 하 고 **확인**합니다.  
  
## <a name="see-also"></a>관련 항목  
[DNS 영역 관리](DNS-Zone-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


