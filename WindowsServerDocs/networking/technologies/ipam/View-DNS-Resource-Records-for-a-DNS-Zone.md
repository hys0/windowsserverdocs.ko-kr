---
title: DNS 영역에 대한 DNS 리소스 레코드 보기
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 375feefc-949e-47c3-9e61-35b79e021966
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 44db34199257367e98279ccbcbc2d5041ee9884c
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283810"
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>DNS 영역에 대한 DNS 리소스 레코드 보기

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IPAM 클라이언트 콘솔에서 DNS 영역에 대 한 DNS 리소스 레코드를 보려면이 항목을 사용할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-view-dns-resource-records-for-a-zone"></a>영역에 대 한 DNS 리소스 레코드를 보려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서에서 **모니터링 및 관리**, 를 클릭 하 여 **DNS 영역**합니다.  탐색 창 위쪽 탐색 창 및 아래쪽 탐색 창으로 나눕니다.  
  
3.  아래쪽 탐색 창에서 클릭 **정방향 조회**, 를 확장 한 다음 도메인 및 영역 목록을 찾아 보려는 영역을 선택 합니다. 예를 들어 더블린 이름이 있으면 클릭 **더블린**합니다.  
  
    ![보려는 영역 선택](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)  

  
4.  디스플레이 창에서 기본 보기 영역에 대 한 DNS 서버입니다. 보기를 변경 하려면 클릭 **현재 보기**, 를 클릭 하 고 **리소스 레코드**합니다.  
  
    ![리소스 레코드에 보기를 변경 합니다.](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)  
  
5.  영역에 대 한 DNS 리소스 레코드가 표시 됩니다. 레코드를 필터링 하려면에서 찾으려는 텍스트를 입력 **필터**합니다.  
  
    ![레코드를 필터링 할 텍스트 입력](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)  
  
6.  레코드 종류, 액세스 범위 또는 기타 기준에 따라 리소스 레코드를 필터링 하려면 클릭 **조건을 추가**, 조건 목록에서 선택 하 고 클릭 **추가**합니다.  
  
    ![레코드를 필터링 할 조건을 사용 하 여](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)  
  
## <a name="see-also"></a>관련 항목  
[DNS 영역 관리](DNS-Zone-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


