---
ms.assetid: 22c514b2-401e-49e1-a87e-0cbaa2c1dac1
title: "사이트 기능"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f40122d84185c69fa19f5158c2b1c370ec1bfe82
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="site-functions"></a>사이트 기능

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

 Windows Server 2008 라우팅 복제, 클라이언트 선호도, 시스템 볼륨 (SYSVOL) 복제, 분산 파일 시스템 네임 스페이스 (DFSN), 위치 서비스 등 다양 한 목적 사이트 정보를 사용 합니다.  
  
## <a name="routing-replication"></a>라우팅 복제  
Active Directory Domain Services (AD DS) 복제 마스터, 스토어 앞으로 방법을 사용 합니다. 도메인 컨트롤러 통신 다음와 통신 하는 제 3 등에 모든 도메인 컨트롤러 변경을 수신 될 때까지 두 번째 도메인 컨트롤러에 디렉터리 변경 합니다. 적절 한 간에 복제 지연 절약 및 교통 감소를 위해 사이트 토폴로지 사이트 내에서 발생 하는 복제와 사이트 간의 발생 하는 복제 사이의 구분 하 여 Active Directory 복제를 제어할 수 있습니다.  
  
사이트 내에서 복제 speeddata 업데이트 트리거 복제에 대해 최적화 되어 있고 필요 없이 데이터 압축 하 여는 데 필요한 데이터를 전송 합니다. 반대로 사이트 간의 복제 넓은 지역 (네트워크) 연결을 통해 전송의 비용 최소화 압축 되어 있습니다. 복제가 사이트 간의 발생 하는 경우 각 각 사이트 도메인 단일 도메인 컨트롤러 수집 디렉터리 변경 내용 저장 및 다른 사이트에 도메인 컨트롤러에 예약된 된 시간에 통신 합니다.  
  
## <a name="client-affinity"></a>클라이언트 선호도  
도메인 컨트롤러 도메인 컨트롤러 내는 클라이언트와 가까운 사이트에 대 한 Active Directory 클라이언트를 알리기 위해 사이트 정보를 사용 합니다. 예를 들어 클라이언트 시애틀 사이트에 있는 도메인 컨트롤러 애틀랜타 사이트에서 연락처 하 고 해당 사이트 소속 알 수 없습니다. 클라이언트의 IP 주소를 기초로 애틀랜타에서 도메인 컨트롤러 클라이언트 실제로 이며 클라이언트로 사이트 정보를 보내고 있는 사이트를 결정 합니다. 또한 도메인 컨트롤러 선택한 도메인 컨트롤러에 근접 한 인지 클라이언트 알립니다. 클라이언트는 애틀랜타 사이트 관련 서비스 (SRV) 리소스 기록 (도메인 컨트롤러 AD DS을 찾는 데는 시스템 DNS (도메인 이름) 리소스 레코드)에 대 한 쿼리가 있는 도메인 컨트롤러에서 제공 하는 사이트 정보를 캐시와 되므로 동일한 사이트에 도메인 컨트롤러를 찾습니다.  
  
동일한 사이트에 도메인 컨트롤러를 찾아 클라이언트 WAN 연결 통신을 방지 합니다. 도메인 컨트롤러 클라이언트 사이트에서 발견 된 경우 다른 연결 된 사이트를 기준으로 가장 비용 연결 된 도메인 컨트롤러 사이트 되어 있지는 않은 도메인 컨트롤러의에서 (사이트 관련 서비스 (SRV) 리소스 기록 dns에서 등록) 자체 알립니다. 사이트 토폴로지별 정의 된 대로 DNS에 게시 되어 있는 도메인 컨트롤러에서 가까운 사이트 들입니다. 이 프로세스는 모든 사이트에 인증에 대 한 기본 도메인 컨트롤러 설치할 수 있도록 보장 합니다.  
  
도메인 컨트롤러를 찾는 프로세스에 대 한 자세한 내용은 참조 Active Directory 컬렉션 ([https://go.microsoft.com/fwlink/?LinkID=88626](https://go.microsoft.com/fwlink/?LinkID=88626)).  
  
## <a name="sysvol-replication"></a>SYSVOL 복제  
SYSVOL 각 도메인 컨트롤러에 도메인에 있는 파일 시스템의 폴더의 모음입니다. SYSVOL 폴더 (Gpo) 그룹 정책 개체, 시작 및 종료 스크립트 로그온 한 로그 오프 스크립트 등 도메인 전체 복제 해야 하는 파일에 대 한 Active Directory 기본 위치를 제공 합니다.  Windows Server 2008 복제 다른 도메인 컨트롤러에 도메인 컨트롤러에서 SYSVOL 폴더를 변경 하는 파일 FRS (복제 서비스) 또는 분산 파일 시스템 복제 (DFSR)를 사용할 수 있습니다. FRS 및 DFSR 복제 사이트 토폴로지 디자인 중 만드는 일정에 따라 이러한 변경 합니다.  
  
## <a name="dfsn"></a>DFSN  
DFSN 직접 클라이언트는 서버에 요청된 데이터 사이트 내에서 호스트 하는 사이트 정보를 사용 합니다. DFSN는 클라이언트와 동일한 사이트에 있는 데이터의 복사본을 찾지 못하면 DFSN 사용 하는 사이트 정보 AD DS DFSN는 어떤 파일 서버에 데이터 공유 확인 하려면에 가장 가까운 클라이언트 합니다.  
  
## <a name="service-location"></a>위치 서비스  
파일 같은 서비스 및 인쇄 서비스 AD DS에서를 게시 하 여 Active Directory 클라이언트 동일한 또는 사이트 가까운 요청한 서비스를 찾을 수 있도록 합니다. 인쇄 서비스 AD DS에 저장 된 위치 특성 사용자의 정밀한 위치를 파악 없이 위치에 따라 프린터에 대 한 검색을 사용 합니다. 디자인 하 고 배포 인쇄 서버에 대 한 자세한 내용은 참조 디자인 및 배포 인쇄 서버 ([https://go.microsoft.com/fwlink/?LinkId=107041](https://go.microsoft.com/fwlink/?LinkId=107041)).  
  


