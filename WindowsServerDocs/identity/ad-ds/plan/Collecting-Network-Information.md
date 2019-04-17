---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: "네트워크 정보를 수집합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 174f11ca85a659f9d0c52e220d5ce37b1804f39b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="collecting-network-information"></a>네트워크 정보를 수집합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

(AD DS) Active Directory Domain Services에서에서 효과적인 사이트 토폴로지 디자인의 첫 번째 단계 조직의 네트워킹 그룹 정보를 수집 하 고 토폴로지에 실제 네트워크에 대 한 정기적으로와 통신을 참조 하는 것입니다.  
  
## <a name="creating-a-location-map"></a>위치 지도 만들기  
조직의 네트워크 실제 인프라 나타내는 위치 지도를 만듭니다. 위치 지도에서 그룹의 컴퓨터 m b p 당 이상 메가 10의 내부 연결 ((lan) 속도 이상)이 포함 된 지리적 위치를 확인 합니다.  
  
## <a name="listing-communication-links-and-available-bandwidth"></a>통신 연결과 대역폭이 목록  
위치 지도 만든 후 문서의 통신 연결과 연결 속도 각 위치 간에 대역폭이 형식 있습니다. 넓은 지역 (네트워크) 토폴로지를 네트워킹 그룹에서 가져옵니다. 일반적인 WAN 회로 형식 및 해당 대역폭 목록에서 "비용을 파악" 섹션을 참조 [사이트 링크 디자인](../../ad-ds/plan/Creating-a-Site-Link-Design.md)합니다. 링크를 만드는 사이트 사이트 토폴로지 디자인 프로세스에서 나중에이 정보가 필요 합니다.  
  
지정된 된 시간 동안의 통신 채널을 통해 전송할 수 있는 데이터의 양을 대역폭 참조 합니다. 대역폭이 실제로에서 사용할 수 있는 AD DS 대역폭의 양을 참조합니다. 네트워킹 그룹에서 사용 가능한 대역폭 정보를 얻을 수 하거나 교통 각 링크를 사용 하 여 네트워크 모니터 같은 프로토콜 분석기 Windows Server 2008와 함께 제공 되는 구성 요소 분석할 수 있습니다. 설치 네트워크 모니터에 대 한 정보를 참조 네트워크 교통 모니터링 ([https://go.microsoft.com/fwlink/?LinkId=107058](https://go.microsoft.com/fwlink/?LinkId=107058)).  
  
각 위치와 연결 된 다른 위치 기록 합니다. 또한 기록 통신 연결과 그 대역폭이 유형의 합니다. 통신 연결과 대역폭이 나열 하는 데 도움이 되도록 워크시트 참조 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))를 다운로드 Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip 하 고 "지리적 위치와 통신 연결이" (DSSTOPO_1.doc) 엽니다.  
  
## <a name="listing-ip-subnets-within-each-location"></a>각 위치 목록 IP 서브넷  
통신 연결과 각 위치 간에 대역폭이, 문서 후 IP 서브넷 각 위치를 기록 합니다. 알 수 없는 이미 서브넷 마스크 및 각 위치 IP 주소, 네트워킹 그룹에 게 문의 하십시오.  
  
AD DS 사이트 워크스테이션 워크스테이션의 IP 주소 각 사이트와 관련 된 서브넷와 비교 하 여 연결 합니다. 도메인에 도메인 컨트롤러를 추가 하 AD DS도 IP 주소를 검사 하 고이 가장 적합 한 사이트에 배치 합니다.  
  
각 위치 IP 서브넷 나열 하는 데 도움이 되도록 워크시트를 참조 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip와 열기 "위치 및 서브넷" (DSSTOPO_2.doc).  
  
> [!NOTE]  
> IP 버전 4 (IPv4) 주소, Windows Server 2008 뿐만 아니라 지원 IP (IPv6) 버전 6 서브넷 접두사 합니다. 워크시트 IPv6 서브넷 접두사 나열 하는 데 도움이 되도록 참조 [부록 a: 위치와 서브넷 접두사](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md)합니다.  
  
## <a name="listing-domains-and-number-of-users-for-each-location"></a>도메인 및 각 위치에 대 한 사용자 수 목록 표시  
위치에 나와 있는 지역 각 도메인에 대 한 사용자 수 중 하나입니다 지역 도메인 컨트롤러의 위치를 결정 하는 요소 및 드 서버 사이트 토폴로지 디자인 프로세스의 다음 단계입니다. 예를 들어, 지역 도메인 컨트롤러 WAN 연결이 경우 도메인에 로그온 여전히 수 있도록 100 개 이상의 지역 도메인 사용자가 있는 위치에 배치 예정입니다.  
  
각 위치와 위치 마다 표시 되는 각 도메인에 대 한 사용자의 수에 표시 되는 도메인의 위치를 기록 합니다. 각 위치에 표시 되는 사용자의 수와 도메인 나열 하는 데 도움이 되도록 워크시트를 참조 작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558))을 다운로드 < DICT__Job_Aids_Designing_and_Deploying_ Directory_and_Security_Services.zip>Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip</DICT__Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip >, 도메인 및 사용자의 각각 "위치" 엽니다 (DSSTOPO_3.doc) 합니다.  
  


