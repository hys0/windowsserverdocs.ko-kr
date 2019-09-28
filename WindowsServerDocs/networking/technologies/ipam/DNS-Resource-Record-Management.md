---
title: DNS 리소스 레코드 관리
description: 이 항목은 Windows Server 2016의 IPAM (IP 주소 관리) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8fe318a8ac17c650d8dbf2339e72b561de529c4a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405680"
---
# <a name="dns-resource-record-management"></a>DNS 리소스 레코드 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 IPAM을 사용 하 여 DNS 리소스 레코드를 관리 하는 방법에 대해 설명 합니다.  
  
> [!NOTE]  
> 이 항목 외에 다음 DNS 리소스 레코드 관리 항목을이 섹션에서 사용할 수 있습니다.  
>   
> -   [DNS 리소스 레코드 추가](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [DNS 리소스 레코드 삭제](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [DNS 리소스 레코드 보기 필터링](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [특정 IP 주소에 대 한 DNS 리소스 레코드 보기](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>리소스 레코드 관리 개요  
Windows Server 2016에서 IPAM을 배포할 때 서버 검색을 수행 하 여 DHCP 및 DNS 서버를 IPAM 서버 관리 콘솔에 추가할 수 있습니다. 그러면 IPAM 서버는 관리 하도록 구성 된 DNS 서버에서 6 시간 마다 DNS 데이터를 동적으로 수집 합니다. IPAM은이 DNS 데이터를 저장 하는 로컬 데이터베이스를 유지 관리 합니다. IPAM은 서버 데이터가 수집 된 날짜와 시간에 대 한 알림을 제공 하 고, DNS 서버에서 데이터를 수집 하는 다음 날짜와 시간을 알려줍니다.  
  
다음 그림의 노란색 상태 표시줄에는 IPAM 알림의 사용자 인터페이스 위치가 나와 있습니다.  
  
![IPAM 알림](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
수집 되는 DNS 데이터에는 DNS 영역 및 리소스 레코드 정보가 포함 됩니다. 기본 설정 DNS 서버에서 영역 정보를 수집 하도록 IPAM을 구성할 수 있습니다.  IPAM은 파일 기반 및 Active Directory 영역을 모두 수집 합니다.  
  
> [!NOTE]  
> IPAM은 도메인에 가입 된 Microsoft DNS 서버 에서만 데이터를 수집 합니다. 타사 DNS 서버와 도메인에 가입 되지 않은 서버는 IPAM에서 지원 되지 않습니다.  
  
다음은 IPAM에 의해 수집 되는 DNS 리소스 레코드 유형 목록입니다.  
  
-   AFS 데이터베이스  
  
-   ATM 주소  
  
-   CNAME  
  
-   DHCID  
  
-   이름의  
  
-   호스트 A 또는 AAAA  
  
-   호스트 정보  
  
-   상태의  
  
-   MX  
  
-   이름 서버  
  
-   포인터 (PTR)  
  
-   담당자  
  
-   경로 통과  
  
-   서비스 위치  
  
-   SOA  
  
-   SRV  
  
-   텍스트  
  
-   잘 알려진 서비스  
  
-   WINS  
  
-   WINS-R  
  
-   X. 25  
  
Windows Server 2016에서는 IPAM이 IP 주소 인벤토리, DNS 영역 및 DNS 리소스 레코드 간의 통합을 제공 합니다.  
  
-   IPAM을 사용 하 여 DNS 리소스 레코드에서 IP 주소 인벤토리를 자동으로 만들 수 있습니다.  
  
-   DNS A 및 AAAA 리소스 레코드에서 IP 주소 인벤토리를 수동으로 만들 수 있습니다.  
  
-   특정 DNS 영역에 대 한 DNS 리소스 레코드를 보고 유형, IP 주소, 리소스 레코드 데이터 및 기타 필터링 옵션에 따라 레코드를 필터링 할 수 있습니다.  
  
-   IPAM에서 IP 주소 범위와 DNS 역방향 조회 영역 간의 매핑을 자동으로 만듭니다.  
  
-   IPAM은 역방향 조회 영역에 있고 해당 IP 주소 범위에 포함 된 PTR 레코드에 대 한 IP 주소를 만듭니다. 필요한 경우이 매핑을 수동으로 수정할 수도 있습니다.  
  
IPAM을 사용 하면 IPAM 콘솔에서 리소스 레코드에 대해 다음 작업을 수행할 수 있습니다.  
  
-   DNS 리소스 레코드 만들기  
  
-   DNS 리소스 레코드 편집  
  
-   DNS 리소스 레코드 삭제  
  
-   연결 된 리소스 레코드 만들기  
  
Ipam은 IPAM 콘솔을 사용 하 여 수행 하는 모든 DNS 구성 변경 내용을 자동으로 기록 합니다.  
  
## <a name="see-also"></a>관련 항목  
[IPAM 관리](Manage-IPAM.md)  
  


