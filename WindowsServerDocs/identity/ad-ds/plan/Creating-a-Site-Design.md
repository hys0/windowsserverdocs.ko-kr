---
ms.assetid: 83f746e5-81db-4610-9977-1d5c57699f50
title: 사이트 디자인 만들기
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5b017582dad68938377fde4055d9a37b0c0af29b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402737"
---
# <a name="creating-a-site-design"></a>사이트 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 디자인을 만들려면 사이트가 되는 위치, 사이트 개체 만들기, 서브넷 개체 만들기 및 서브넷을 사이트에 연결을 결정 해야 합니다.  
  
## <a name="deciding-which-locations-will-become-sites"></a>사이트가 될 위치 결정

다음과 같이 사이트를 만들 위치를 결정 합니다.  
  
- 도메인 컨트롤러를 추가 하려는 모든 위치에 대 한 사이트를 만듭니다. 도메인 컨트롤러를 포함 하는 위치를 식별 하려면 "도메인 컨트롤러 배치" (DSSTOPO_4) 워크시트에 설명 된 정보를 참조 하십시오.  
- 사이트를 만들어야 하는 응용 프로그램을 실행 하는 서버를 포함 하는 위치에 대 한 사이트를 만듭니다. DFSN (분산 파일 시스템 네임 스페이스)와 같은 특정 응용 프로그램에서는 사이트 개체를 사용 하 여 클라이언트에 가장 가까운 서버를 찾습니다.  

   > [!NOTE]  
   > 조직에서 빠르고 신뢰할 수 있는 연결을 사용 하 여 여러 네트워크를 긴밀 하 게 연결 하는 경우 해당 네트워크의 모든 서브넷을 단일 Active Directory 사이트에 포함할 수 있습니다. 예를 들어 서로 다른 서브넷에 있는 두 서버 간의 왕복에서 네트워크 대기 시간이 10 밀리초 이하인 경우 두 서브넷을 동일한 Active Directory 사이트에 포함할 수 있습니다. 두 위치 간의 네트워크 대기 시간이 10 밀리초를 초과 하는 경우 단일 Active Directory 사이트에 서브넷을 포함 하지 않아야 합니다. 대기 시간이 10 밀리초 이하인 경우에도 Active Directory 기반 응용 프로그램에 대 한 사이트 간 트래픽을 분할 하려면 개별 사이트를 배포 하도록 선택할 수 있습니다.  

- 특정 위치에 대 한 사이트가 필요 하지 않은 경우 해당 위치에 최대 WAN (광역 네트워크) 속도와 사용 가능한 대역폭을 사용 하는 사이트에 위치의 서브넷을 추가 합니다.  
  
각 위치 내에서 사이트와 네트워크 주소 및 서브넷 마스크로 사용할 문서 위치 사이트를 문서화 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://go.microsoft.com/fwlink/?LinkID=102558)을 참조 하 고, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고, "서브넷을 사이트와 연결" (DSSTOPO_6)을 엽니다.  
  
## <a name="creating-a-site-object-design"></a>사이트 개체 디자인 만들기

사이트를 만들도록 결정 한 모든 위치에 대해 Active Directory Domain Services (AD DS)에서 사이트 개체를 만들도록 계획 합니다. "사이트와 서브넷 연결" 워크시트에서 사이트가 될 문서 위치입니다.  
  
사이트 개체를 만드는 방법에 대 한 자세한 내용은 [사이트 만들기](https://go.microsoft.com/fwlink/?LinkId=107067)문서를 참조 하세요.  
  
## <a name="creating-a-subnet-object-design"></a>서브넷 개체 디자인 만들기

각 위치와 연결 된 모든 IP 서브넷 및 서브넷 마스크에 대해 사이트 내의 모든 IP 주소를 나타내는 AD DS 서브넷 개체를 만들도록 계획 합니다.  
  
Active Directory subnet 개체를 만들 때 네트워크 IP 서브넷 및 서브넷 마스크에 대 한 정보는 자동으로 /<prefix length><IP address>네트워크 접두사 길이 표기법 형식으로 변환 됩니다. 예를 들어 서브넷 마스크가 255.255.252.0 인 네트워크 IP 버전 4 (IPv4) 주소 172.16.4.0은 172.16.4.0/22로 표시 됩니다. IPv4 주소 외에도 Windows Server 2008는 IPv6 (IP 버전 6) 서브넷 접두사 (예: 3FFE: FFFF: 0: C000::/64)도 지원 합니다. 각 위치의 IP 서브넷에 대 한 자세한 내용은 [네트워크 정보 수집](../../ad-ds/plan/Collecting-Network-Information.md) 및 [부록 a: 위치 및 서브넷 접두사](Appendix-A--Locations-and-Subnet-Prefixes.md)에서 "위치 및 서브넷" (DSSTOPO_2) 워크시트를 참조 하세요.  
  
"사이트의 위치 결정" 섹션의 "사이트에 서브넷 연결" (DSSTOPO_6 .doc) 워크시트를 참조 하 여 각 서브넷 개체를 사이트 개체와 연결 합니다. "사이트에 서브넷 연결" (DSSTOPO_6 .doc) 워크시트에서 각 위치와 연결 된 Active Directory 서브넷 개체를 문서화 합니다.  
  
서브넷 개체를 만드는 방법에 대 한 자세한 내용은 [서브넷 만들기](https://go.microsoft.com/fwlink/?LinkId=107068)문서를 참조 하세요.
