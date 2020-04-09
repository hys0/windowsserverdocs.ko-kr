---
title: DNS 영역 만들기
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0ae9869b95cfa1da04e0103b5a824ff1fc21568f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814756"
---
# <a name="create-a-dns-zone"></a>DNS 영역 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 IPAM 클라이언트 콘솔을 사용 하 여 DNS 영역을 만들 수 있습니다.  
  
이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  
  
### <a name="to-create-a-dns-zone"></a>DNS 영역을 만들려면  
  
1.  서버 관리자에서 클릭  **IPAM**합니다. IPAM 클라이언트 콘솔에 나타납니다.  
  
2.  탐색 창의 **모니터 및 관리**에서 **DNS 및 DHCP 서버**를 클릭 합니다. 디스플레이 창에서 **서버 유형**을 클릭 한 다음 **DNS**를 클릭 합니다. IPAM에서 관리 하는 모든 DNS 서버가 검색 결과에 나열 됩니다.  
  
3.  영역을 추가 하려는 서버를 찾고 서버를 마우스 오른쪽 단추로 클릭 합니다.  **DNS 영역 만들기**를 클릭 합니다.  
  
    ![DNS 영역 만들기](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)  
  
4.  **DNS 영역 만들기** 대화 상자가 열립니다. **일반 속성**에서 영역 범주를 선택 하 고 영역 **이름**에 이름을 입력 합니다. 또한 **고급 속성**에서 배포에 적합 한 값을 선택 하 고 **확인**을 클릭 합니다.  
  
    ![고급 속성](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)  
  
## <a name="see-also"></a>관련 항목  
[DNS 영역 관리](DNS-Zone-Management.md)  
[IPAM 관리](Manage-IPAM.md)  
  


