---
title: DNS 리소스 레코드 관리
description: 이 항목은 Windows Server 2016에서 관리 IPAM (IP 주소) 관리 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7b66c09d-e401-4f70-9a2a-6047dd629bfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2db802fa928a4051fbe409fc0ba60d774bb0428
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284048"
---
# <a name="dns-resource-record-management"></a>DNS 리소스 레코드 관리

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 IPAM을 사용 하 여 DNS 리소스 레코드를 관리 하는 방법에 대 한 정보를 제공 합니다.  
  
> [!NOTE]  
> 이 항목 외에 다음 DNS 리소스 레코드를 관리 항목은이 섹션에 있습니다.  
>   
> -   [DNS 리소스 레코드 추가](../../technologies/ipam/Add-a-DNS-Resource-Record.md)  
> -   [DNS 리소스 레코드를 삭제 합니다.](../../technologies/ipam/Delete-DNS-Resource-Records.md)  
> -   [DNS 리소스 레코드의 보기를 필터링](../../technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)  
> -   [특정 IP 주소에 대 한 DNS 리소스 레코드 보기](../../technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-Address.md)  
  
## <a name="resource-record-management-overview"></a>리소스 레코드를 관리 개요  
Windows Server 2016에서 IPAM을 배포할 때에 DHCP 및 DNS 서버는 IPAM 서버 관리 콘솔에 추가할 서버 검색을 수행할 수 있습니다. IPAM 서버 경우 동적으로 DNS 데이터가 6 시간 마다에서 수집 하도록 구성 된 DNS 서버를 관리 합니다. IPAM이 DNS 데이터를 저장 하는 로컬 데이터베이스를 관리 합니다. IPAM을 날짜 및 시간 다음날 알리는 뿐만 아니라 서버 데이터 수집 된와 DNS 서버에서 데이터 수집이 발생 하는 경우 시간에 대 한 알림을 제공 합니다.  
  
다음 그림에 노란색 상태 표시줄 IPAM 알림 사용자 인터페이스 위치를 보여 줍니다.  
  
![IPAM 알림](../../media/DNS-Resource-Record-Management/ipam_DataCollection_01.jpg)  
  
수집 되는 DNS 데이터를 DNS 영역 및 리소스 레코드 정보를 포함 합니다. 기본 설정된 DNS 서버에서 표준 시간대 정보를 수집 하는 IPAM을 구성할 수 있습니다.  IPAM은 파일 기반 및 Active Directory 영역을 수집합니다.  
  
> [!NOTE]  
> IPAM은 도메인에 가입 된 Microsoft DNS 서버 에서만에서 데이터를 수집합니다. 타사 DNS 서버 및 비-도메인에 가입 된 서버 IPAM에서 지원 되지 않습니다.  
  
다음은 IPAM에서 수집 하는 DNS 리소스 레코드 형식의 목록입니다.  
  
-   AFS 데이터베이스  
  
-   ATM 주소  
  
-   CNAME  
  
-   DHCID  
  
-   DNAME  
  
-   호스트 A 또는 AAAA  
  
-   호스트 정보  
  
-   ISDN  
  
-   MX  
  
-   이름 서버  
  
-   PTR (포인터)  
  
-   책임자  
  
-   통과 연결  
  
-   서비스 위치  
  
-   SOA  
  
-   SRV  
  
-   텍스트 모드  
  
-   잘 알려진 서비스  
  
-   WINS  
  
-   WINS-R  
  
-   X.25  
  
Windows Server 2016의 IPAM은 IP 주소 인벤토리, DNS 영역 및 DNS 리소스 레코드 간의 통합을 제공:  
  
-   자동으로 DNS 리소스 레코드의 IP 주소 인벤토리를 작성 하려면 IPAM을 사용할 수 있습니다.  
  
-   DNS A 및 AAAA 리소스 레코드에서 수동으로 IP 주소 인벤토리를 만들 수 있습니다.  
  
-   특정 DNS 영역에 대 한 DNS 리소스 레코드를 볼 수 있으며, IP 주소, 리소스 레코드 데이터 형식과 다른 필터링 옵션에 따라 레코드를 필터링 수 있습니다.  
  
-   IPAM에는 자동으로 IP 주소 범위 및 DNS 역방향 조회 영역 간의 매핑을 만듭니다.  
  
-   IPAM의 IP 주소 역방향 조회 영역에 있는 및 해당 IP 주소 범위에 포함 되는 PTR 레코드를 만듭니다. 필요한 경우에 수동으로이 매핑을 수정할 수 있습니다.  
  
IPAM을 사용 하면 IPAM 콘솔에서 리소스 레코드에서 다음 작업을 수행할 수 있습니다.  
  
-   DNS 리소스 레코드 만들기  
  
-   DNS 리소스 레코드를 편집 합니다.  
  
-   DNS 리소스 레코드 삭제  
  
-   연결 된 리소스 레코드 만들기  
  
IPAM에는 자동으로 확인 하는 IPAM 콘솔을 사용 하는 모든 DNS 구성 변경 기록 합니다.  
  
## <a name="see-also"></a>관련 항목  
[IPAM 관리](Manage-IPAM.md)  
  


