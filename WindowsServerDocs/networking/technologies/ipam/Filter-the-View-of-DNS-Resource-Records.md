---
title: DNS 리소스 레코드의 보기 필터링
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
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fed5e1f923d3560b91f514d1e59d79b847557c8b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847804"
---
# <a name="filter-the-view-of-dns-resource-records"></a>DNS 리소스 레코드의 보기 필터링

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 IPAM 클라이언트 콘솔에서 DNS 리소스 레코드의 보기를 필터링에 사용할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>DNS 리소스 레코드의 보기를 필터링 하려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서에서 **모니터링 및 관리**, 를 클릭 하 여 **DNS 영역**합니다.  탐색 창 위쪽 탐색 창 및 아래쪽 탐색 창으로 나눕니다.  
  
3.  아래쪽 탐색 창에서 클릭 **정방향 조회**합니다. 모든 IPAM에서 관리 하는 DNS 정방향 조회 영역 검색 결과 표시 창에에서 표시 됩니다.  
  
4.  영역에 있는 레코드 보기 및 필터를 클릭 합니다.  
  
5.  디스플레이 창에서 클릭 **현재 보기**를 클릭 하 고 **리소스 레코드**합니다. 영역에 대 한 리소스 레코드 디스플레이 창에 표시 됩니다.  
  
6.  디스플레이 창에서 클릭 **조건 추가**합니다.  
  
    ![조건 추가](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  드롭다운 목록에서 조건을 선택 합니다. 예를 들어 특정 레코드 유형을 확인 하려면 클릭 **레코드 종류**합니다.  
  
    ![기준 선택](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  **추가**를 클릭합니다.  
  
    ![조건 추가](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. **레코드 종류** 검색 매개 변수로 추가 됩니다. 찾으려는 레코드의 형식에 대 한 텍스트를 입력 합니다. SRV 레코드에만 보려는 경우 입력 하는 예를 들어 **SRV**합니다.  
  
    ![찾으려는 레코드의 유형을 지정합니다](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. Enter 키를 누릅니다. DNS 리소스 레코드를 조건에 따라 필터링 됩니다 및 지정 된 구를 검색 합니다.  
  
    ![필터를 실행 합니다.](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>관련 항목  
[DNS 리소스 레코드 관리](DNS-Resource-Record-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


