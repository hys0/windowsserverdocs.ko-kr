---
title: 리소스 DNS 레코드 추가
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
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e14a59e9f172b20e85a34d2299e3733a796adafc
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="add-a-dns-resource-record"></a>리소스 DNS 레코드 추가

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

하나 또는 여러 개의 새 DNS 리소스 레코드 IPAM 클라이언트 콘솔을 사용 하 여 추가 하려면이 항목을 사용할 수 있습니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  
  
### <a name="to-add-a-dns-resource-record"></a>리소스 DNS 레코드를 추가 하려면  
  
1.  서버 관리자 클릭 **IPAM**합니다. IPAM 클라이언트 콘솔이 나타납니다.  
  
2.  탐색 창에서에 **모니터 관리**, 클릭 **DNS 영역**합니다.  탐색 창 위 탐색 창 하 고 낮은 탐색 창을 나눕니다.  
  
3.  낮은 탐색 창에서 클릭 **앞으로 조회**합니다. 모든 IPAM 관리 DNS 앞으로 조회 영역이 디스플레이 창 검색 결과에 표시 됩니다. 리소스 레코드 추가를 클릭 한 다음 영역을 마우스 오른쪽 단추로 클릭 **리소스 추가 DNS 레코드**합니다.  
  
    ![리소스 DNS 레코드 추가](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  **DNS 리소스 레코드 추가** 대화 상자를 엽니다. **리소스 녹화 속성**, 클릭 **DNS 서버** 하나 이상의 새로운 리소스 레코드 추가할 DNS 서버를 선택 합니다. **리소스 구성 DNS 레코드**, 클릭 **새로**합니다.  
  
    ![DNS 레코드 리소스를 구성](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  대화 상자가 표시 하려면 확장 **새 리소스 레코드**합니다. 클릭 **리소스 녹화 종류**합니다.  
  
    ![리소스 녹화 종류](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  리소스 기록 종류의 목록이 표시 됩니다. 추가 하려는 리소스 기록 종류를 클릭 합니다.  
  
    ![추가 녹화 유형 선택](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  **새 리소스 레코드** 에 **이름**, 리소스 기록 이름을 입력 합니다. **IP 주소**, IP 주소를 입력 하 고 여 배포를 위해 적합 한 리소스 녹화 속성을 선택 합니다. 클릭 **리소스 레코드 추가**합니다.  
  
    ![리소스 레코드 추가](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  추가 새로운 리소스 레코드를 만든 하려면 클릭 **확인**합니다. 새로운 리소스 레코드 추가 만들려는 경우 클릭 **새로**합니다.  
  
    ![새로운 또는 확인을 클릭 합니다.](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. 대화 상자가 표시 하려면 확장 **새 리소스 레코드**합니다. 클릭 **리소스 녹화 종류**합니다. 리소스 기록 종류의 목록이 표시 됩니다. 추가 하려는 리소스 기록 종류를 클릭 합니다.  
  
10. **새 리소스 레코드** 에 **이름**, 리소스 기록 이름을 입력 합니다. **IP 주소**, IP 주소를 입력 하 고 여 배포를 위해 적합 한 리소스 녹화 속성을 선택 합니다. 클릭 **리소스 레코드 추가**합니다.  
  
    ![리소스 레코드 추가](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. 더 많은 리소스 레코드를 추가 하려는 경우 레코드를 만들기 위한 프로세스를 반복 합니다. 새로운 리소스 레코드 만드는 작업을 완료 하면 클릭 **적용**합니다.  
  
    ![전체 리소스 녹화 만들기](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. **리소스 기록 추가** 대화 상자가 IPAM 지정한 DNS 서버의 리소스 레코드 만드는 동안 리소스 레코드 요약이 표시 됩니다. 성공적으로 레코드를 만들 때는 **상태** 기록의는 **성공**합니다.  
  
    ![또한 상황 녹화](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. 클릭 **확인**합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[DNS 리소스 기록 관리](DNS-Resource-Record-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


