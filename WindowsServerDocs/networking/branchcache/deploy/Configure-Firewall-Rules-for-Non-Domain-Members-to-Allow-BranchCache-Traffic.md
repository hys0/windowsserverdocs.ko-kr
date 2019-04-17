---
title: 방화벽 규칙 BranchCache 교통 수 있도록 구성원 비 도메인에 대 한 구성
description: 이 항목은 Windows Server 2016을 지점에서 WAN 대역폭 사용을 최적화 하 분산 / 호스팅된 캐시 모드로 BranchCache 배포 하는 방법을 보여 주는 BranchCache 배포 가이드
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e5f744141efc35bb493bcd95fad53eafbbc3f78d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>방화벽 규칙 BranchCache 교통 수 있도록 구성원 비 도메인에 대 한 구성

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

방화벽 제 3 자 제품을 구성 하 고 수동으로 방화벽 규칙 BranchCache 분산된 캐시 모드에서 실행 하도록 허용 하는 클라이언트 컴퓨터 구성 하려면이 항목의 정보를 사용할 수 있습니다.  
  
> [!NOTE]  
> -   그룹 정책을 사용 하 여 BranchCache 클라이언트 컴퓨터 구성한 경우 그룹 정책 설정을 재정의 정책이 적용 되는 클라이언트 컴퓨터의 모든 수동으로 구성 합니다.  
> -   DirectAccess와 BranchCache를 배포 하는 경우 IPsec 규칙 BranchCache 교통 수 있도록 구성 하려면이 항목의 설정을 사용할 수 있습니다.  
  
회원 **관리자**, 해당 하는 이러한 구성을 변경 하는 데 필요한 최소 또는 합니다.  
  
## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS PCCRD]: 콘텐츠 캐시와 검색 검색 프로토콜 피어  
분산된 캐시 클라이언트 웹 서비스 동적 (WS 검색) 검색 프로토콜에 수행 된 인바인드 및 아웃 바운드 MS PCCRD 교통량을 허용 해야 합니다.  
  
방화벽 설정을 인바인드 및 아웃 바운드 교통 뿐 아니라 멀티 캐스트 교통량을 허용 해야 합니다. 분산된 캐시 모드에 대 한 예외 방화벽 구성 하려면 다음 설정을 사용할 수 있습니다.  
  
멀티 IPv4 캐스트: 239.255.255.250  
  
멀티 IPv6 캐스트: FF02::C  
  
돌아오는 교통: 로컬 포트: 3702, 원격 포트: 임시  
  
아웃 바운드 교통: 로컬 포트: 임시, 원격 포트: 3702  
  
프로그램: %systemroot%\system32\svchost.exe (BranchCache 서비스 [PeerDistSvc])  
  
## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS PCCRR]: 콘텐츠 캐시와 검색 피어: 검색 프로토콜  
분산된 캐시 클라이언트 의견 2616 (RFC)에 대 한 요청에 명시 된 대로 1.1 HTTP 프로토콜에 수행 된 인바인드 및 아웃 바운드 MS PCCRR 교통량을 허용 해야 합니다.  
  
방화벽 설정을 인바인드 및 아웃 바운드 교통량을 허용 해야 합니다. 분산된 캐시 모드에 대 한 예외 방화벽 구성 하려면 다음 설정을 사용할 수 있습니다.  
  
돌아오는 교통: 로컬 포트: 원격 포트 80,: 임시  
  
아웃 바운드 교통: 로컬 포트: 임시, 원격 포트: 80  
  


