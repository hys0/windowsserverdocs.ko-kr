---
ms.assetid: 22c514b2-401e-49e1-a87e-0cbaa2c1dac1
title: 사이트 기능
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0a330a9dae8ab8d3b9de5d1fff0e52060908f520
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815814"
---
# <a name="site-functions"></a>사이트 기능

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Windows Server 2008 라우팅 복제, 클라이언트 선호도, 시스템 볼륨 (SYSVOL) 복제, 분산 파일 시스템 네임 스페이스 (DFSN (), 및 서비스 위치를 포함 하 여 다양 한 용도로 사이트 정보를 사용 합니다.  
  
## <a name="routing-replication"></a>라우팅 복제  
Active Directory Domain Services (AD DS)는 다중 마스터, 저장 및 전달 방법의 복제를 사용합니다. 도메인 컨트롤러에는 모든 도메인 컨트롤러 변경 내용을 수신 될 때까지 다음 세 번째, 등을 통신 하는 두 번째 도메인 컨트롤러에 디렉터리 변경 전달 합니다. 복제 대기 시간을 줄이고 트래픽을 줄이고 간에 최상의 균형을 달성 하기 사이트 토폴로지는 사이트 내에서 발생 하는 복제 및 사이트 간에 발생 하는 복제를 구별 하 여 Active Directory 복제를 제어 합니다.  
  
사이트 내에서 복제 데이터 압축에 필요한 오버 헤드 없이 보내집니다 속도, 데이터 업데이트 트리거 복제 및 데이터에 대해 최적화 됩니다. 반대로, 사이트 간 복제는 광역 네트워크 (WAN) 링크를 통해 전송의 비용을 최소화 하기 위해 압축 됩니다. 사이트 간에 복제가 발생 합니다이 각 사이트에서 도메인 별로 단일 도메인 컨트롤러가 수집 디렉터리 변경 내용 저장 및 다른 사이트에서 도메인 컨트롤러에 예약된 된 시간에 이러한 통신 합니다.  
  
## <a name="client-affinity"></a>클라이언트 선호도  
도메인 컨트롤러는 Active Directory 클라이언트는 클라이언트와 가장 가까운 사이트 내에 있는 도메인 컨트롤러에 게 알리기 위해 사이트 정보를 사용 합니다. 예를 들어, 애틀랜타 사이트에서 도메인 컨트롤러를 연결 하 고 해당 사이트 정보를 알지 못합니다 시애틀 사이트에 클라이언트를 것이 좋습니다. 애틀랜타에서 도메인 컨트롤러를 클라이언트의 IP 주소에 따라 클라이언트에서 실제로 다시 클라이언트에 사이트 정보를 보냅니다는 사이트를 결정 합니다. 또한 도메인 컨트롤러 선택한 도메인 컨트롤러를 가장 가까운 것을 인지 여부를 클라이언트에 알립니다. 클라이언트는 사이트 관련 서비스 (SRV) 리소스 레코드 (도메인 이름 시스템 (DNS) 리소스 레코드를 AD DS에 대 한 도메인 컨트롤러를 찾는 데 사용)에 대 한 쿼리 애틀랜타에서 도메인 컨트롤러에서 제공 하는 사이트 정보를 캐시 하 고 있으므로 도메인을 찾습니다. 동일한 사이트 내의 컨트롤러입니다.  
  
동일한 사이트에 도메인 컨트롤러를 검색 하 여 클라이언트가 WAN 연결을 통한 통신을 방지 합니다. 클라이언트 사이트의 도메인 컨트롤러가 없는 있는 하는 경우 다른 연결 된 사이트를 기준으로 가장 낮은 비용 연결 된 도메인 컨트롤러 스스로 알립니다 (사이트 관련 서비스 (SRV) 리소스 레코드를 DNS에 등록) 되지 않은 사이트에는 도메인 컨트롤러입니다. DNS에 게시 되는 도메인 컨트롤러는 가장 가까운 사이트에서 사이트 토폴로지 정의 된 대로입니다. 이렇게 하면 모든 사이트는 인증에 대 한 기본 도메인 컨트롤러.  
  
도메인 컨트롤러를 찾는 프로세스에 대 한 자세한 내용은 Active Directory 컬렉션을 참조 하세요. ([https://go.microsoft.com/fwlink/?LinkID=88626](https://go.microsoft.com/fwlink/?LinkID=88626)).  
  
## <a name="sysvol-replication"></a>SYSVOL 복제  
SYSVOL은 도메인의 각 도메인 컨트롤러에 있는 파일 시스템 폴더의 컬렉션. SYSVOL 폴더를 사용 하는 그룹 정책 개체 (Gpo), 시작 및 종료 스크립트 및 로그온 / 로그 오프 스크립트를 포함 하 여 도메인 전체에 걸쳐 복제 해야 하는 파일의 기본 Active Directory 위치를 제공 합니다.  Windows Server 2008 다른 도메인 컨트롤러에 하나의 도메인 컨트롤러에서 SYSVOL 폴더에 대 한 변경 내용을 복제 하도록 복제 서비스 FRS (파일) 또는 파일 시스템 복제 (DFSR (분산)를 사용할 수 있습니다. FRS 및 DFSR 사이트 토폴로지 디자인 중에 만든 일정에 따라 이러한 변경 내용을 복제 합니다.  
  
## <a name="dfsn"></a>DFSN  
DFSN은 사이트 내에서 요청된 된 데이터를 호스팅하는 서버에 클라이언트에 사이트 정보를 사용 합니다. DFSN 클라이언트와 동일한 사이트 내의 데이터의 복사본을 찾지 못하면, DFSN 사용 DFSN 있는 파일 서버 공유 데이터를 확인 하려면 AD DS에서 사이트 정보를 가장 가까운 클라이언트입니다.  
  
## <a name="service-location"></a>서비스 위치  
AD DS에서 인쇄 서비스 및 파일 등의 서비스를 게시, Active Directory 클라이언트 사이트에 가장 가까운 또는 동일한 요청 된 서비스를 찾을 수 있습니다. 인쇄 서비스의 정확한 위치를 알지 못해도 검색을 위치에 따라 사용할 수 있도록 AD DS에 저장 하는 위치 특성을 사용 합니다. 설계 및 인쇄 서버를 배포 하는 방법에 대 한 자세한 내용은 설계 및 인쇄 서버 배포를 참조 하십시오. ([https://go.microsoft.com/fwlink/?LinkId=107041](https://go.microsoft.com/fwlink/?LinkId=107041)).  
  


