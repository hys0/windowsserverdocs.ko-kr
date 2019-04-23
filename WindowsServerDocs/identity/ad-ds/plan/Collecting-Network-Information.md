---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: 네트워크 정보 수집
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d88cc2fafd9aa4fc221efc901c48fa41ef007a21
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867044"
---
# <a name="collecting-network-information"></a>네트워크 정보 수집

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)에서 효과적인 사이트 토폴로지를 디자인 하는 첫 번째 단계는 조직의 네트워킹 그룹 정보를 수집 하 고 실제 네트워크 토폴로지에 대 한 정기적으로 상호 통신을 참조 하는 것입니다.  
  
## <a name="creating-a-location-map"></a>위치 맵 만들기

사용자 조직의 실제 네트워크 인프라를 나타내는 위치 지도를 만듭니다. 위치 맵 컴퓨터 그룹에 10 메가 비트 (Mbps) 초당 이상의 내부 연결 (로컬 영역 네트워크 (LAN) 속도 이상)를 포함 하는 지리적 위치를 식별 합니다.  
  
## <a name="listing-communication-links-and-available-bandwidth"></a>사용 가능한 대역폭 및 통신 링크 나열

위치 지도 만든 후 문서 통신 링크, 해당 링크 속도 및 각 위치 간에 사용 가능한 대역폭의 유형입니다. 네트워킹 그룹에서 광역 네트워크 (WAN) 토폴로지를 가져옵니다. 일반적인 WAN 회로 형식 및 해당 대역폭 목록을에서 "비용 확인" 섹션을 참조 하세요. [사이트 링크 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Design.md)합니다. 사이트 토폴로지 디자인 프로세스의 뒷부분에 나오는 사이트 링크를 만들려면이 정보가 필요 합니다.  
  
대역폭을 지정 된 시간 내에 통신 채널을 통해 전송할 수 있는 데이터의 양을 가리킵니다. 사용 가능한 대역폭 AD DS에 실제로 사용할 수 있는 대역폭의 양을 가리킵니다. 네트워킹 그룹에서 사용할 수 있는 대역폭 정보를 얻을 수 있습니다 또는 네트워크 모니터와 같은 프로토콜 분석기를 사용 하 여 각 링크에서 트래픽을 분석할 수 있습니다. 네트워크 모니터를 설치 하는 것에 대 한 자세한 문서를 참조 [네트워크 트래픽 모니터링](https://go.microsoft.com/fwlink/?LinkId=107058)합니다.  
  
각 위치와 연결 된 다른 위치를 문서화 합니다. 또한 유형 통신 링크 및 해당 사용 가능한 대역폭을 기록 합니다. 통신 링크 및 사용 가능한 대역폭을 나열 하는 데 도움이 되는 워크시트를 참조 하세요 [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip를 다운로드 하 고 "지리적 위치 및 통신 링크" (DSSTOPO_1.doc)를 엽니다.  
  
## <a name="listing-ip-subnets-within-each-location"></a>각 위치 내에서 IP 서브넷 나열

통신 링크 및 각 위치 간에 사용 가능한 대역폭을 문서화한 후 각 위치 내에서 IP 서브넷을 기록 합니다. 알 수 없는 이미 서브넷 마스크 및 각 위치 내에서 IP 주소를 하는 경우에 네트워킹 그룹을 참조 하세요.  
  
AD DS 사이트 워크스테이션 각 사이트와 연결 된 서브넷이 있는 워크스테이션의 IP 주소를 비교 하 여 연결 합니다. 도메인에 도메인 컨트롤러를 추가 하면 AD DS도 해당 IP 주소를 검사 하 고이 가장 적합 한 사이트에 배치 합니다.  
  
각 위치 내에서 IP 서브넷을 나열 하는 데 도움이 되는 워크시트를 참조 하세요 [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558)Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip를 다운로드 하 고 엽니다 " 위치 및 서브넷"(DSSTOPO_2.doc).  
  
> [!NOTE]  
> IP 버전 4 외에도 (IPv4) 주소, Windows Server IP 버전 6(ipv6)도 지원 서브넷 접두사입니다. IPv6 서브넷 접두사를 나열 하는 데 도움이 되는 워크시트를 참조 하세요. [부록 a: 위치 및 서브넷 접두사](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md)합니다.  

## <a name="listing-domains-and-number-of-users-for-each-location"></a>도메인 및 각 위치에 대 한 사용자 수가 나열

위치에 표시 되는 각 지역 도메인에 대 한 사용자 수가 경우 글로벌 카탈로그 서버를 확인 하 고 지역 도메인 컨트롤러의 배치를 결정 하는 요소 중 하나는 사이트 토폴로지 디자인 프로세스에서 다음 단계는 예를 들어 지역 도메인 컨트롤러 수 여전히에 로그온 할 도메인 WAN 링크 하지 못하면 있도록 100 개가 넘는 지역 도메인 사용자를 포함 하는 위치에 배치 하려고 합니다.  
  
각 위치 및 각 위치에 표시 되는 각 도메인에 대 한 사용자 수에 나타나는 도메인 위치를 기록 합니다. 도메인 및 각 위치에서 표현 되는 사용자 수가 나열 하는 데 도움이 되는 워크시트를 참조 하세요 [작업 보조 기능에 대 한 Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_ 다운로드 Security_Services.zip, 및 열기 "도메인 및 사용자의 각 위치" (DSSTOPO_3.doc)입니다.  
