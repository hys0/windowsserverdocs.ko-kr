---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: 사이트 디자인 만들기
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f6d896213708f8c3ec5de44a1f85fb4ebd86b8c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819074"
---
# <a name="creating-a-site-design"></a>사이트 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 디자인 만들기 만들고 사이트로 설정할 위치 결정, 사이트 개체, 서브넷 개체를 만드는 사이트와 서브넷에 연결 합니다.  
  
## <a name="deciding-which-locations-will-become-sites"></a>사이트로 설정할 위치 결정

다음과 같이 만들려는 위치에 대 한 사이트를 결정 합니다.  
  
- 도메인 컨트롤러를 배치 하려는 모든 위치에 대 한 사이트를 만듭니다. 도메인 컨트롤러를 포함 하는 위치를 식별 하기 위해 "도메인 컨트롤러 배치" (DSSTOPO_4.doc) 워크시트에서 설명 된 정보를 참조 하십시오.  
- 만들려는 사이트를 필요로 하는 응용 프로그램을 실행 하는 서버를 포함 하는 해당 위치에 대 한 사이트를 만듭니다. 특정 응용 프로그램을 같은 분산 파일 시스템 네임 스페이스 (DFSN (), 클라이언트에 가장 가까운 서버를 찾는 사이트 개체를 사용 합니다.  

   > [!NOTE]  
   > 조직에 여러 네트워크 빠르고 안정적인 연결을 사용 하 여 근접해 있는 경우 해당 네트워크의 서브넷의 모든 단일 Active Directory 사이트에 포함할 수 있습니다. 예를 들어, 반환 되는 왕복 네트워크 대기 시간에 서로 다른 두 서버 간에 서브넷 10ms 인지, 동일한 Active Directory 사이트에 두 서브넷을 포함할 수 있습니다. 두 위치 간에 네트워크 대기 시간이 10ms 보다 클 경우 단일 Active Directory 사이트에 서브넷을 포함 되지 않습니다. 도 때 대기 시간이 10ms 되었거나, Active Directory 기반 응용 프로그램에 대 한 사이트 간에 트래픽을 분할 하려는 경우 별도 사이트를 배포 하도록 선택할 수 있습니다.  

- 사이트 위치에 대 한 필요 하지 않은 경우 최대 광역 네트워크 (WAN) 속도 사용 가능한 대역폭 위치에 있는 사이트에 서브넷의 위치를 추가 합니다.  
  
사이트 및 네트워크 주소와 각 위치 내에서 서브넷 마스크 될 위치를 문서화 합니다. 사이트를 문서화 하는 데 도움이 되는 워크시트를 참조 하세요 [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558)Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip를 다운로드 하 고 "연결 서브넷과 함께 엽니다 사이트 "(DSSTOPO_6.doc)입니다.  
  
## <a name="creating-a-site-object-design"></a>사이트 개체 디자인 만들기

사이트를 만들 하기로 모든 위치에 대 한 Active Directory Domain Services (AD DS)에 사이트 개체를 만들 계획 합니다. "사이트와 서브넷 연결" 워크시트에서 사이트에 문서 위치입니다.  
  
사이트 개체를 만드는 방법에 대 한 자세한 내용은 문서 참조 [사이트를 만들](https://go.microsoft.com/fwlink/?LinkId=107067)합니다.  
  
## <a name="creating-a-subnet-object-design"></a>서브넷 개체 디자인 만들기

모든 IP 서브넷 및 각 위치와 연결 된 서브넷 마스크에 대 한 사이트 내에서 모든 IP 주소를 나타내는 AD DS에 서브넷 개체를 만들 계획 합니다.  
  
Active Directory 서브넷 개체를 만들 때 네트워크 IP 서브넷 및 서브넷 마스크에 대 한 정보를 자동으로 변환 됩니다 네트워크 접두사 길이 표기법 서식 <IP address> / <prefix length>합니다. 예를 들어 네트워크 IP 버전 4 (IPv4) 255.255.252.0 서브넷 마스크를 사용 하 여 주소 172.16.4.0 172.16.4.0/22로 표시 됩니다. IPv4 주소 외에도 Windows Server 2008에서는 IP 버전 6(ipv6) 서브넷 접두사, 예를 들어 3FFE:FFFF:0:C000:: / 64입니다. 각 위치에 IP 서브넷에 대 한 자세한 내용은 참조에서 "위치 및 서브넷" (DSSTOPO_2.doc) 워크시트 [네트워크 정보 수집](../../ad-ds/plan/Collecting-Network-Information.md) 고 [부록 a: 위치 및 서브넷 접두사](Appendix-A--Locations-and-Subnet-Prefixes.md)합니다.  
  
"연결 서브넷 사이트와" (DSSTOPO_6.doc) 워크시트는 서브넷을 확인 하려면 "결정 하는 위치는 될 사이트" 섹션에서 참조 하 여 사이트 개체를 사용 하 여 각 서브넷 개체는 사이트에 연결할 연결 합니다. "연결 서브넷 사이트와" (DSSTOPO_6.doc) 워크시트에서 각 위치와 연결 된 Active Directory 서브넷 개체는 문서입니다.  
  
서브넷 개체를 만드는 방법에 대 한 자세한 내용은 문서 참조 [서브넷을 만드는](https://go.microsoft.com/fwlink/?LinkId=107068)합니다.
