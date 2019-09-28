---
title: DNS 리소스 레코드의 보기 필터링
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 541645a274481bb8b044c37df572d7746c5da30e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405668"
---
# <a name="filter-the-view-of-dns-resource-records"></a>DNS 리소스 레코드의 보기 필터링

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔에서 DNS 리소스 레코드의 보기를 필터링 할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>DNS 리소스 레코드 보기를 필터링 하려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서에서 **모니터링 및 관리**, 를 클릭 하 여 **DNS 영역**합니다.  탐색 창 위쪽 탐색 창 및 아래쪽 탐색 창으로 나눕니다.  
  
3.  아래쪽 탐색 창에서 클릭 **정방향 조회**합니다. 모든 IPAM에서 관리 하는 DNS 정방향 조회 영역 검색 결과 표시 창에에서 표시 됩니다.  
  
4.  보고 필터링 할 레코드가 있는 영역을 클릭 합니다.  
  
5.  디스플레이 창에서 **현재 보기**를 클릭 한 다음 **리소스 레코드**를 클릭 합니다. 영역에 대 한 리소스 레코드는 표시 창에 표시 됩니다.  
  
6.  디스플레이 창에서 **조건 추가**를 클릭 합니다.  
  
    ![조건 추가](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  드롭다운 목록에서 조건을 선택 합니다. 예를 들어 특정 레코드 종류를 보려면 **레코드 종류**를 클릭 합니다.  
  
    ![조건 선택](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  **추가**를 클릭합니다.  
  
    ![조건 추가](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. **레코드 형식이** 검색 매개 변수로 추가 됩니다. 찾으려는 레코드 유형에 대 한 텍스트를 입력 합니다. 예를 들어 SRV 레코드만 보려면 **srv**를 입력 합니다.  
  
    ![찾을 레코드 유형을 지정 합니다.](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. Enter 키를 누릅니다. DNS 리소스 레코드는 지정 된 조건 및 검색 구에 따라 필터링 됩니다.  
  
    ![필터 실행](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>관련 항목  
[DNS 리소스 레코드 관리](DNS-Resource-Record-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


