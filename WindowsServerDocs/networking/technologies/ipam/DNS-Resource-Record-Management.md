---
title: DNS 리소스 기록 관리
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
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 5ed781ef37243b80ea9da8aad27a29046b8dc8c9
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="dns-resource-record-management"></a>DNS 리소스 기록 관리

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서는 리소스 DNS 레코드 IPAM를 사용 하 여 관리에 대 한 정보를 제공 합니다.  
  
> [!NOTE]  
> 이 항목 외에도 다음 DNS 리소스 기록 관리 항목은이 섹션에서 사용할 수 있습니다.  
>   
> -   [리소스 DNS 레코드 추가](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [DNS 리소스 기록 삭제](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [필터 DNS 리소스 기록 보기](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [특정 IP 주소가 DNS 리소스 기록 보기](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>리소스 기록 관리 개요  
Windows Server 2016에 IPAM 배포할 때 IPAM 서버 관리 콘솔에 DHCP 및 DNS 서버를 추가 하려면 서버 검색을 수행할 수 있습니다. IPAM 서버 다음 동적 DNS에서에서 데이터를 수집 6 시간 마다 하도록 구성 된 DNS 서버 관리 합니다. IPAM은 DNS 데이터를 저장 하는 로컬 데이터베이스를 유지 합니다. IPAM 하루와 그 다음 날 알리는 뿐만 아니라 서버 데이터가 수집 된 시간 및 DNS 서버에서 데이터 수집 발생할 때의 알림을 제공 합니다.  
  
다음 그림에서 노란색 상태 표시줄 IPAM 알림 사용자 인터페이스 위치를 보여 줍니다.  
  
![IPAM 알림](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
수집 되는 DNS 데이터에는 DNS 영역 및 리소스 기록 정보를 포함 합니다. 기본 설정된 DNS 서버에서 영역 정보를 수집 IPAM 구성할 수 있습니다.  IPAM 파일 기반 및 Active Directory 영역을 수집합니다.  
  
> [!NOTE]  
> IPAM은 도메인에 가입 DNS 서버에서 단독으로 데이터를 수집합니다. 제 3 자 DNS 서버 및 비 도메인 결합된 서버 IPAM에서 지원 되지 않습니다.  
  
다음은 IPAM 하 여 수집 된 DNS 리소스 기록 종류의 목록입니다.  
  
-   AFS 데이터베이스  
  
-   ATM 주소  
  
-   CNAME  
  
-   DHCID  
  
-   DNAME  
  
-   호스트 A 또는 AAAA  
  
-   호스트 정보  
  
-   ISDN  
  
-   MX  
  
-   서버 이름  
  
-   (Ptr)  
  
-   책임자  
  
-   통과 하 여  
  
-   위치 서비스  
  
-   SOA  
  
-   SRV  
  
-   텍스트  
  
-   유명한 서비스  
  
-   WINS  
  
-   WINS R  
  
-   X. 25  
  
Windows Server 2016 IPAM IP 주소 재고, DNS 영역 및 리소스 DNS 레코드 간 통합을 제공합니다.  
  
-   IPAM 자동으로 DNS 레코드 리소스의에서 IP 주소 인벤토리 빌드를 사용할 수 있습니다.  
  
-   DNS A와 AAAA 리소스 기록의 IP 주소 인벤토리 수동으로 만들 수 있습니다.  
  
-   특정 DNS 영역을를 볼 수 있고 유형, IP 주소, 리소스 기록 데이터를 및 기타 필터링 옵션에 따라 레코드 필터링.  
  
-   IPAM IP 주소 범위와 DNS 역방향 조회 영역이 매핑하를 자동으로 만들어집니다.  
  
-   IPAM 역방향 조회 영역이 되며 해당 IP 주소 범위 내에 포함 된 PTR 레코드에 대 한 IP 주소를 만듭니다. 필요한 경우이 지도 제작을 직접 수정할 수 있습니다.  
  
IPAM은 IPAM 콘솔에서 리소스 레코드에 다음과 같은 작업을 수행할 수 있습니다.  
  
-   DNS 레코드 리소스 만들기  
  
-   편집 DNS 리소스  
  
-   DNS 리소스 기록 삭제  
  
-   연결 된 리소스 기록 만들기  
  
IPAM은 IPAM 콘솔을 사용 하는 모든 DNS 구성 변경을 자동으로 로그인 합니다.  
  
## <a name="see-also"></a>참조 하십시오  
[IPAM 관리](Manage-IPAM.md)  
  


