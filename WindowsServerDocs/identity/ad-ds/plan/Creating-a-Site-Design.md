---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: "사이트 디자인 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2bcbf30159721e1fc2e12af103ca6f3e79f3ec97
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-site-design"></a>사이트 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 디자인 하 고 위치 사이트가 결정, 사이트 개체 만들기, 서브넷 개체 만들기 서브넷 사이트와 연결 합니다.  
  
## <a name="deciding-which-locations-will-become-sites"></a>위치 사이트가 결정 합니다.  
다음과 같이 대 한 사이트 만들 수 있는 위치를 결정 합니다.  
  
-   도메인 컨트롤러 저장 하려는 모든 위치에 대 한 사이트를 만듭니다. 도메인 컨트롤러를 포함 하는 위치를 식별 하 고 "도메인 컨트롤러 배치" (DSSTOPO_4.doc) 워크시트에 설명 된 정보를 참조 하세요.  
  
-   사이트를 만들 수 있는 사이트를 필요로 하는 응용 프로그램을 실행 하는 서버를 포함 하는 해당 위치에 대 한 만듭니다. 특정 응용 프로그램 등 분산 파일 시스템 네임 스페이스 (DFSN)을 사이트 개체를 사용 하 여 클라이언트 가까운 서버를 찾습니다.  
  
    > [!NOTE]  
    > 조직 신속 하 고 신뢰할 수 있는 연결 된 근접에서 여러 네트워크에을 한 Active Directory 사이트에 있는 모든 서브넷 해당 네트워크에 대 한를 포함할 수 있습니다. 예를 들어, 왕복 반환 네트워크에서 다른 두 서버 대기 서브넷 10 ms는 또는 이하의 서브넷 모두 동일한 Active Directory 사이트에 포함할 수 있습니다. 두 지점 간에 네트워크 대기 10 ms 이상인 경우 한 Active Directory 사이트에 서브넷을 포함 되지 않습니다. 도 때 대기 10 ms 되었거나, 덜 개별 사이트 배포 하는 사이트 Active Directory 기반 응용 프로그램에 대 한 교통량을 분할 하려는 경우 선택할 수 있습니다.  
  
-   사이트 위치 필요 하지 않은 경우 위치 서브넷 최대 다양 한 영역 (네트워크) 속도 사용 가능한 대역폭 위치 갖고 있는 사이트를 추가 합니다.  
  
네트워크 주소 사이트 및 각 위치 서브넷 마스크가 있는 위치를 기록 합니다. 사이트 문서화에 도움을 주고 워크시트를 참조 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, 및 열고 "연결 서브넷와 사이트" (DSSTOPO_6.doc) 합니다.  
  
## <a name="creating-a-site-object-design"></a>사이트 개체 디자인 만들기  
사이트를 만드는 결정 한 모든 위치에 대 한 Active Directory Domain Services (AD DS)의 개체 사이트 만들 예정입니다. 문서 위치 사이트 "사이트와 연결 서브넷" 워크시트에 의존 합니다.  
  
사이트 개체를 만드는 방법에 대 한 자세한 내용은 참조 사이트 만들기 ([https://go.microsoft.com/fwlink/?LinkId=107067](https://go.microsoft.com/fwlink/?LinkId=107067)).  
  
## <a name="creating-a-subnet-object-design"></a>서브넷 개체 디자인 만들기  
IP 서브넷 및 서브넷 마스크 각 위치와 연결 된 모든 사이트 내에서 모든 IP 주소를 나타내는 AD DS에에서 서브넷 개체를 만들 예정입니다.  
  
네트워크 IP 서브넷와 서브넷 마스크에 대 한 정보는 네트워크 접두사 길이 표기법 형식으로 자동으로 번역 서브넷 Active Directory 개체를 만들 때 <IP address> / <prefix length>합니다. 예를 들어 있는 네트워크 IPv4 IP 버전 4 () 주소 172.16.4.0 서브넷 마스크 255.255.252.0 172.16.4.0/22로 나타납니다. IPv4 주소, Windows Server 2008 뿐만 아니라 지원 IP (IPv6) 버전 6 서브넷 접두사, 예를 들어, 3FFE:FFFF:0:C000: 64 / 합니다. IP 서브넷 각 위치에 대 한 자세한 내용은 참조에서 "위치 및 서브넷" (DSSTOPO_2.doc) 워크시트 [네트워크 정보를 수집](../../ad-ds/plan/Collecting-Network-Information.md) 및 [부록 a: 위치 및 서브넷 접두사](Appendix-A--Locations-and-Subnet-Prefixes.md)합니다.  
  
연결 된 서브넷 확인 하려면 "결정 하는 위치는 될 사이트" 섹션에서 "사이트와 연결 서브넷" (DSSTOPO_6.doc) 워크시트를 참조 하 여 사이트 개체와 함께 각 서브넷 개체 하는 사이트와 관련입니다. 각 위치 "사이트와 연결 서브넷" (DSSTOPO_6.doc) 워크시트에와 관련 된 Active Directory 서브넷 개체를 기록 합니다.  
  
서브넷 개체를 만드는 방법에 대 한 자세한 내용은 참조 만들기 서브넷 ([https://go.microsoft.com/fwlink/?LinkId=107068](https://go.microsoft.com/fwlink/?LinkId=107068)).  
  


