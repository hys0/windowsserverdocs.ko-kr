---
title: DNS 리소스 기록 삭제
description: 이 항목은 Windows Server 2016에는 IP 주소 관리 (IPAM) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 366e6fd5-d563-4de3-9551-5614cbb8f2cb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f9ebfeca1da9e36cd00272113f2e86c33174074b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="delete-dns-resource-records"></a>DNS 리소스 기록 삭제

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

하나 이상의 DNS 리소스 레코드 IPAM 클라이언트 콘솔을 사용 하 여 삭제 하려면이 항목을 사용할 수 있습니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
### <a name="to-delete-dns-resource-records"></a>DNS 리소스 기록을 삭제 하려면  
  
1.  서버 관리자 클릭 **IPAM**합니다. IPAM 클라이언트 콘솔이 나타납니다.  
  
2.  탐색 창에서에 **모니터 관리**, 클릭 **DNS 영역**합니다.  탐색 창 위 탐색 창 하 고 낮은 탐색 창을 나눕니다.  
  
3.  확장을 **앞으로 조회** 하 고 삭제 하려는 영역과 리소스 기록 있는 도메인. 창에 해당 영역을 켜고을 누르고 **현재 보기**합니다. 클릭 **리소스 레코드**합니다.  
  
4.  디스플레이 창에서 찾아 리소스 레코드 삭제할를 선택 합니다.  
  
    ![선택 리소스 기록을 삭제 하려면](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_01.jpg)  
  
5.  선택한 레코드를 마우스 오른쪽 단추로 클릭 한 다음 한 **리소스 삭제 DNS 레코드**합니다.  
  
    ![레코드 삭제](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_02.jpg)  
  
6.  **DNS 리소스 기록 삭제** 대화 상자를 엽니다. 올바른 DNS 서버 선택 되어 있는지 확인 합니다. 없는 경우 클릭 **DNS 서버** 리소스 기록 삭제 하려는 서버를 선택 합니다. 클릭 **확인**합니다. IPAM은 DNS 서버에서 리소스 기록을 삭제합니다.  
  
    ![올바른 DNS 서버 선택 되어 있는지 확인 하 고 기록 삭제](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_03.jpg)  
  
## <a name="see-also"></a>참조 하십시오  
[DNS 리소스 기록 관리](DNS-Resource-Record-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


