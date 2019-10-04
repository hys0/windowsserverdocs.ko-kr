---
title: 도메인 구성원이 아닌 BranchCache 트래픽을 허용 하도록 방화벽 규칙 구성
description: 이 항목은 일부는 BranchCache 배포 가이드에 대 한 Windows Server 2016, 지사에 WAN 대역폭 사용량을 최적화 하기 위해 분산 및 호스트 캐시 모드로 BranchCache를 배포 하는 방법을 보여 주는
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: da956be0-c92d-46ea-99eb-85e2bd67bf07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a96b67b235b813ad455d5b289b7238f671e4c547
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356712"
---
# <a name="configure-firewall-rules-for-non-domain-members-to-allow-branchcache-traffic"></a>도메인 구성원이 아닌 BranchCache 트래픽을 허용 하도록 방화벽 규칙 구성

>적용 대상: Windows Server(반기 채널), Windows Server 2016

타사 방화벽 제품을 구성 하 고 수동으로 BranchCache 분산된 캐시 모드에서 실행 되도록 허용 하는 방화벽 규칙에는 클라이언트 컴퓨터를 구성 하려면이 항목의 정보를 사용할 수 있습니다.  
  
> [!NOTE]  
> -   그룹 정책을 사용 하 여 BranchCache 클라이언트 컴퓨터를 구성한 경우 그룹 정책 설정은 정책이 적용 되는 클라이언트 컴퓨터를 수동으로 구성 하는 모든 문서를 무시 합니다.  
> -   DirectAccess와 BranchCache를 배포한 경우에 BranchCache 트래픽을 허용 하도록 IPsec 규칙을 구성 하려면이 항목의 설정을 사용할 수 있습니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 이러한 구성을 변경 하는 데 필요한 최소값입니다.  
  
## <a name="ms-pccrd-peer-content-caching-and-retrieval-discovery-protocol"></a>[MS PCCRD]: 피어 콘텐츠 캐싱 및 검색 검색 프로토콜  
분산된 캐시 클라이언트는 웹 서비스 동적 검색 (Ws-discovery) 프로토콜에 전달 되는 인바운드 및 아웃 바운드 MS PCCRD 트래픽을 허용 해야 합니다.  
  
방화벽 설정에는 인바운드 및 아웃 바운드 트래픽 외에 멀티 캐스트 트래픽을 허용 해야 합니다. 분산된 캐시 모드에 대 한 방화벽 예외를 구성 하려면 다음 설정을 사용할 수 있습니다.  
  
IPv4 멀티 캐스트: 239.255.255.250  
  
IPv6 멀티 캐스트: FF02:: C  
  
인바운드 트래픽: 로컬 포트: 3702, 원격 포트: 임시  
  
아웃 바운드 트래픽: 로컬 포트: 임시, 원격 포트: 3702  
  
프로그램의 경우: %systemroot%\system32\svchost.exe (BranchCache 서비스 [PeerDistSvc])  
  
## <a name="ms-pccrr-peer-content-caching-and-retrieval-retrieval-protocol"></a>[MS PCCRR]: 피어 콘텐츠 캐싱 및 검색: 검색 프로토콜  
분산된 캐시 클라이언트는 RFC 2616 주석에 대 한 요청에 설명 된 대로 HTTP 1.1 프로토콜에 전달 되는 인바운드 및 아웃 바운드 MS PCCRR 트래픽을 허용 해야 합니다.  
  
방화벽 설정에는 인바운드 및 아웃 바운드 트래픽을 허용 해야 합니다. 분산된 캐시 모드에 대 한 방화벽 예외를 구성 하려면 다음 설정을 사용할 수 있습니다.  
  
인바운드 트래픽: 로컬 포트: 80, 원격 포트: 임시  
  
아웃 바운드 트래픽: 로컬 포트: 임시, 원격 포트: 80  
  


