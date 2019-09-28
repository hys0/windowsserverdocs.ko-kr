---
ms.assetid: 22c514b2-401e-49e1-a87e-0cbaa2c1dac1
title: 사이트 기능
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 109f576bfdacf68a0eadc7dd84ddb9a4148e6dd9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408670"
---
# <a name="site-functions"></a>사이트 기능

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Windows Server 2008에서는 라우팅 복제, 클라이언트 선호도, 시스템 볼륨 (SYSVOL) 복제, 분산 파일 시스템 네임 스페이스 (DFSN) 및 서비스 위치를 비롯 하 여 다양 한 용도로 사이트 정보를 사용 합니다.  
  
## <a name="routing-replication"></a>라우팅 복제  
Active Directory Domain Services (AD DS)는 복제에 대 한 저장소 및 전달 방법을 사용 합니다. 도메인 컨트롤러는 디렉터리 변경 내용을 두 번째 도메인 컨트롤러와 통신 합니다. 그러면 모든 도메인 컨트롤러가 변경 내용을 받을 때까지 세 번째 도메인 컨트롤러와 통신 합니다. 복제 대기 시간을 줄이고 트래픽을 줄이는 데 가장 적합 한 균형을 이루기 위해 사이트 토폴로지는 사이트 내에서 발생 하는 복제와 사이트 간에 발생 하는 복제를 구분 하 여 복제를 Active Directory 합니다.  
  
사이트 내에서 복제는 속도에 맞게 최적화 되 고, 데이터 업데이트는 복제를 트리거하고 데이터는 데이터 압축에 필요한 오버 헤드 없이 전송 됩니다. 반대로, WAN (광역 네트워크) 링크를 통해 전송 되는 비용을 최소화 하기 위해 사이트 간 복제가 압축 됩니다. 사이트 간에 복제가 발생 하는 경우 각 사이트에서 도메인당 단일 도메인 컨트롤러는 디렉터리 변경 내용을 수집 하 여 저장 하 고 예약 된 시간에 다른 사이트의 도메인 컨트롤러에 전달 합니다.  
  
## <a name="client-affinity"></a>클라이언트 선호도  
도메인 컨트롤러는 사이트 정보를 사용 하 여 클라이언트와 가장 가까운 사이트 내에 있는 도메인 컨트롤러에 대 한 Active Directory 클라이언트에 알립니다. 예를 들어 시애틀 사이트에서 사이트 정보를 알지 못하는 클라이언트를 고려 하 고 애틀랜타 사이트에서 도메인 컨트롤러에 연결 합니다. 클라이언트의 IP 주소에 따라 애틀랜타의 도메인 컨트롤러는 클라이언트가 실제로 속한 사이트를 결정 하 고 사이트 정보를 클라이언트에 게 다시 보냅니다. 도메인 컨트롤러는 또한 선택한 도메인 컨트롤러가 가장 가까운 도메인 컨트롤러 인지 여부를 클라이언트에 알립니다. 클라이언트는 애틀랜타에서 도메인 컨트롤러에서 제공 하는 사이트 정보를 캐시 하 고, 사이트 특정 서비스 (SRV) 리소스 레코드 (AD DS 도메인 컨트롤러를 찾는 데 사용 되는 DNS (Domain Name System) 리소스 레코드)를 쿼리하고, 도메인을 찾습니다. 동일한 사이트 내에 있는 컨트롤러  
  
클라이언트는 동일한 사이트에서 도메인 컨트롤러를 찾아 WAN 링크를 통한 통신을 방지 합니다. 클라이언트 사이트에 도메인 컨트롤러가 없는 경우 다른 연결 된 사이트를 기준으로 순위가 가장 낮은 도메인 컨트롤러가 자동으로 보급 됩니다 (DNS의 사이트 관련 서비스 (SRV) 리소스 레코드를 등록 함). 도메인 컨트롤러. DNS에 게시 된 도메인 컨트롤러는 사이트 토폴로지에서 정의한 대로 가장 가까운 사이트의 컨트롤러입니다. 이 프로세스를 통해 모든 사이트에는 인증을 위한 기본 도메인 컨트롤러가 있습니다.  
  
도메인 컨트롤러를 찾는 프로세스에 대 한 자세한 내용은 Active Directory Collection ([https://go.microsoft.com/fwlink/?LinkID=88626](https://go.microsoft.com/fwlink/?LinkID=88626))을 참조 하세요.  
  
## <a name="sysvol-replication"></a>SYSVOL 복제  
SYSVOL은 도메인의 각 도메인 컨트롤러에 있는 파일 시스템의 폴더 모음입니다. SYSVOL 폴더는 Gpo (그룹 정책 개체), 시작 및 종료 스크립트, 로그온 및 로그 오프 스크립트를 포함 하 여 도메인 전체에 복제 해야 하는 파일에 대 한 기본 Active Directory 위치를 제공 합니다.  Windows Server 2008는 FRS (파일 복제 서비스) 또는 DFSR (분산 파일 시스템 복제)를 사용 하 여 SYSVOL 폴더에 대 한 변경 내용을 한 도메인 컨트롤러에서 다른 도메인 컨트롤러로 복제할 수 있습니다. FRS 및 DFSR은 사이트 토폴로지 디자인 중에 만든 일정에 따라 이러한 변경 내용을 복제 합니다.  
  
## <a name="dfsn"></a>DFSN  
DFSN 사이트 정보를 사용 하 여 사이트 내에서 요청 된 데이터를 호스팅하는 서버로 클라이언트를 보냅니다. DFSN가 클라이언트와 동일한 사이트 내에서 데이터의 복사본을 찾지 못하면 DFSN는 AD DS의 사이트 정보를 사용 하 여 DFSN 공유 데이터가 있는 파일 서버 중 클라이언트에 가장 가까운 파일 서버를 확인 합니다.  
  
## <a name="service-location"></a>서비스 위치  
AD DS에서 파일 및 인쇄 서비스와 같은 서비스를 게시 하면 Active Directory 클라이언트에서 동일 하거나 가장 가까운 사이트 내에서 요청 된 서비스를 찾을 수 있습니다. 인쇄 서비스는 AD DS에 저장 된 location 특성을 사용 하 여 사용자가 정확한 위치를 몰라도 위치 별로 프린터를 찾아볼 수 있도록 합니다. 인쇄 서버를 설계 하 고 배포 하는 방법에 대 한 자세한 내용은 인쇄 서버 디자인 및 배포 ([https://go.microsoft.com/fwlink/?LinkId=107041](https://go.microsoft.com/fwlink/?LinkId=107041))를 참조 하세요.  
  


