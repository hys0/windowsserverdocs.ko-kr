---
title: DNS 리소스 레코드 추가
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 67238c1546e8833298ec061cf6e05a038b9d474c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814846"
---
# <a name="add-a-dns-resource-record"></a>DNS 리소스 레코드 추가

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IPAM 클라이언트 콘솔을 사용 하 여 하나 이상의 새 DNS 리소스 레코드를 추가 하려면이 항목을 사용할 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-add-a-dns-resource-record"></a>DNS 리소스 레코드를 추가 하려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창에서에서 **모니터링 및 관리**, 를 클릭 하 여 **DNS 영역**합니다.  탐색 창 위쪽 탐색 창 및 아래쪽 탐색 창으로 나눕니다.  
  
3.  아래쪽 탐색 창에서 클릭 **정방향 조회**합니다. 모든 IPAM에서 관리 하는 DNS 정방향 조회 영역 검색 결과 표시 창에에서 표시 됩니다. 리소스 레코드를를 추가 하 고 클릭 한 다음 영역을 마우스 오른쪽 단추로 클릭 **추가 DNS 리소스 레코드**합니다.  
  
    ![DNS 리소스 레코드 추가](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  **DNS 리소스 레코드 추가** 대화 상자가 열립니다. **리소스 레코드 속성**, 클릭 **DNS 서버** 하나 이상의 새 리소스 레코드를 추가 하려면 DNS 서버를 선택 합니다. **DNS 리소스 레코드 구성**, 클릭 **새로**합니다.  
  
    ![DNS 리소스 레코드를 구성 합니다.](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  대화 상자에 표시할 확장 **새 리소스 레코드**합니다. 클릭 **리소스 레코드 종류**합니다.  
  
    ![리소스 레코드 종류](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  리소스 레코드 종류의 목록이 표시 됩니다. 추가 하려는 리소스 레코드 종류를 클릭 합니다.  
  
    ![추가할 레코드 종류를 선택 합니다.](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  **새 리소스 레코드** 에서 **이름**, 리소스 레코드 이름을 입력 합니다. **IP 주소**, IP 주소를 입력 하 고 배포에 대 한 적절 한 리소스 레코드 속성을 선택 합니다. 클릭 **리소스 레코드 추가**합니다.  
  
    ![리소스 레코드 추가](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  새 리소스 레코드를 추가로 만들 하려면 클릭 **확인**합니다. 새 리소스 레코드를 추가로 만들려는 경우 클릭 **새로**합니다.  
  
    ![새로운 또는 ok (확인)를 클릭 합니다.](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. 대화 상자에 표시할 확장 **새 리소스 레코드**합니다. 클릭 **리소스 레코드 종류**합니다. 리소스 레코드 종류의 목록이 표시 됩니다. 추가 하려는 리소스 레코드 종류를 클릭 합니다.  
  
10. **새 리소스 레코드** 에서 **이름**, 리소스 레코드 이름을 입력 합니다. **IP 주소**, IP 주소를 입력 하 고 배포에 대 한 적절 한 리소스 레코드 속성을 선택 합니다. 클릭 **리소스 레코드 추가**합니다.  
  
    ![리소스 레코드 추가](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. 리소스 레코드를 더 추가 하려는 경우 레코드를 만들기 위한 프로세스를 반복 합니다. 새 리소스 레코드 만들기를 완료 하면 클릭 **적용**합니다.  
  
    ![완벽 한 리소스 레코드 만들기](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. **리소스 레코드 추가** IPAM가 지정 된 DNS 서버에서 리소스 레코드를 만드는 동안 대화 상자 리소스 레코드 요약을 표시 합니다. 레코드는 성공적으로 만들어지면는 **상태** 는 레코드의 **성공**합니다.  
  
    ![레코드 추가 상태](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
[DNS 리소스 레코드 관리](DNS-Resource-Record-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


