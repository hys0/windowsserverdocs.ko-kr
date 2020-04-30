---
ms.assetid: 8be8c48d-790c-4199-b9d3-9f4a07d5ced2
title: 네트워크 정보 수집
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6792d565e08a188e1957c67ce419676d4a044d82
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624391"
---
# <a name="collecting-network-information"></a>네트워크 정보 수집

> 적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS)에서 효과적인 사이트 토폴로지를 디자인 하는 첫 번째 단계는 조직의 네트워킹 그룹을 참조 하 여 정보를 수집 하 고 실제 네트워크 토폴로지에 대 한 정보를 정기적으로 통신 하는 것입니다.

## <a name="creating-a-location-map"></a>위치 맵 만들기

조직의 실제 네트워크 인프라를 나타내는 위치 맵을 만듭니다. 위치 맵에서 초당 10mbps 이상의 내부 연결을 사용 하는 컴퓨터 그룹을 포함 하는 지리적 위치를 식별 합니다 (LAN (local area network) 속도 이상).

## <a name="listing-communication-links-and-available-bandwidth"></a>통신 링크 및 사용 가능한 대역폭 나열

위치 맵을 만든 후 통신 링크 유형, 링크 속도 및 각 위치 간의 사용 가능한 대역폭을 문서화 합니다. 네트워킹 그룹에서 WAN (광역 네트워크) 토폴로지를 가져옵니다. 일반적인 WAN 회로 유형 및 해당 대역폭의 목록은 [사이트 링크 디자인 만들기](../../ad-ds/plan/Creating-a-Site-Link-Design.md)의 "비용 확인" 섹션을 참조 하세요. 이 정보는 나중에 사이트 토폴로지 디자인 프로세스에서 사이트 링크를 만드는 데 필요 합니다.

대역폭은 지정 된 시간 동안 통신 채널을 통해 전송할 수 있는 데이터의 양을 나타냅니다. 사용 가능한 대역폭은 AD DS에서 실제로 사용할 수 있는 대역폭의 양을 나타냅니다. 네트워킹 그룹에서 사용 가능한 대역폭 정보를 얻거나 네트워크 모니터와 같은 프로토콜 분석기를 사용 하 여 각 링크의 트래픽을 분석할 수 있습니다. 네트워크 모니터를 설치 하는 방법에 대 한 자세한 내용은 [네트워크 트래픽 모니터링](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc783075(v=ws.10))문서를 참조 하세요.

각 위치 및 여기에 연결 된 다른 위치를 문서화 합니다. 또한 통신 링크 유형 및 사용 가능한 대역폭을 기록 합니다. 통신 링크 및 사용 가능한 대역폭을 나열 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://microsoft.com/download/details.aspx?id=9608)을 참조 하 고, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고, "지리적 위치 및 통신 링크" (DSSTOPO_1)를 엽니다.

## <a name="listing-ip-subnets-within-each-location"></a>각 위치 내의 IP 서브넷 나열

통신 링크와 각 위치 간의 사용 가능한 대역폭을 문서화 한 후 각 위치에 IP 서브넷을 기록 합니다. 각 위치 내에서 서브넷 마스크와 IP 주소를 아직 모르는 경우 네트워킹 그룹을 참조 하세요.

AD DS 워크스테이션의 IP 주소를 각 사이트와 연결 된 서브넷과 비교 하 여 워크스테이션과 사이트를 연결 합니다. 도메인 컨트롤러를 도메인에 추가 하는 경우에도 IP 주소를 검사 하 고 가장 적합 한 사이트에 배치 AD DS 합니다.

각 위치 내의 IP 서브넷을 나열 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://microsoft.com/download/details.aspx?id=9608)을 참조 하 고, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고, "위치 및 서브넷" (DSSTOPO_2)을 엽니다.

> [!NOTE]
> IPv4 (IP 버전 4) 주소 외에도 Windows Server는 IPv6 (IP 버전 6) 서브넷 접두사를 지원 합니다. IPv6 서브넷 접두사를 나열 하는 데 도움이 되는 워크시트는 [부록 a: 위치 및 서브넷 접두사](../../ad-ds/plan/Appendix-A--Locations-and-Subnet-Prefixes.md)를 참조 하세요.

## <a name="listing-domains-and-number-of-users-for-each-location"></a>각 위치에 대 한 도메인 및 사용자 수 나열

특정 위치에 표시 되는 각 지역 도메인의 사용자 수는 지역 도메인 컨트롤러 및 글로벌 카탈로그 서버 (사이트 토폴로지 디자인 프로세스의 다음 단계)의 배치를 결정 하는 요소 중 하나입니다. 예를 들어 100 이상의 지역 도메인 사용자가 포함 된 위치에 지역 도메인 컨트롤러를 배치 하도록 계획 하 여 WAN 링크가 실패할 경우 도메인에 계속 로그온 할 수 있습니다.

위치, 각 위치에 표시 되는 도메인 및 각 위치에 표시 되는 각 도메인에 대 한 사용자 수를 기록 합니다. 각 위치에 표시 되는 도메인 및 사용자 수를 나열 하는 데 도움이 되는 워크시트의 경우 [Windows Server 2003 배포 키트의 작업 지원](https://microsoft.com/download/details.aspx?id=9608)을 참조 하 고, Job_Aids_Designing_and_Deploying_Directory_and_Security_Services .zip을 다운로드 하 고, "각 위치의 도메인 및 사용자" (DSSTOPO_3)를 엽니다.
