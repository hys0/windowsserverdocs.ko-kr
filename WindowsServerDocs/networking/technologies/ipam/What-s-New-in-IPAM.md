---
title: IPAM의 새로운 기능
description: 새로운 또는 변경 Windows Server 2016에는 IP 주소 관리 (IPAM) 기능에 설명 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f2f2f1a5-ac2f-41b7-a495-98ad0e2a9b20
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b90cd1ab223e38cbf5933b58a594b32d5e3d4858
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-ipam"></a>IPAM의 새로운 기능

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

새로운 또는 변경 Windows Server 2016에는 IP 주소 관리 (IPAM) 기능에 설명 합니다.  
  
IPAM은 엔터프라이즈 또는 클라우드 서비스 공급자 (CSP) 네트워크의 IP 주소와 DNS 인프라에 대해 매우 사용자 지정 가능한 관리 및 모니터링 기능을 제공 합니다. 모니터, 감사 하 고 IPAM를 사용 하 여 DHCP Dynamic Host Configuration Protocol () 및 시스템 DNS (도메인 이름)을 실행 하는 서버 관리할 수 있습니다.  
  
## <a name="BKMK_IPAM2012R2"></a>IPAM 서버에 대 한 업데이트  
다음은 Windows Server 2016에 IPAM에 대 한 새로운 기능과 향상 된 기능입니다.  
  
|기능/기능|새로운 기능이 나 향상 된|설명|  
|--------------------------|-------------------|---------------|  
|[향상 된 IP 주소 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|개선|I p v 4/32 및 IPv6 /128 서브넷 처리, IP 주소 블록에서 무료 IP 주소 서브넷 및 범위를 찾는 등 시나리오에 대해 IPAM 기능이 개선 되었습니다.|  
|[고급 DNS 서비스 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|새로운|IPAM은 리소스 DNS 레코드, 조건부 전달자 및 DNS 영역 관리 모두 도메인에 가입 Active Directory 통합 하 고 파일 백업 DNS 서버를 지원합니다.|  
|[통합 DNS, DHCP 및 IP 주소 (DDI) 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|개선|몇 가지 새로운 환경과 통합된 수명 주기 관리 IP 주소와 관련 된 모든 DNS 리소스 레코드 시각화와 같은 작업을 활성화 인벤토리 DNS 리소스 기록과 IP 주소 수명 주기 관리 DNS 및 DHCP 작업에 대 한에 따라 IP 주소를 자동으로 합니다.|  
|[여러 Active Directory 숲 지원](#bkmk_ad)|새로운|IPAM 양방향 신뢰 IPAM 설치 되어 있는 숲와 각각 원격 숲 관계 있을 때의 여러 Active Directory 숲 DNS 및 DHCP 서버 관리에 사용할 수 있습니다.|  
|[활용 데이터 지우기](#bkmk_purge)|새로운|사용자가 지정 된 날짜 보다 오래 된 IP 주소 활용도 데이터를 제거 하 여 이제 IPAM 데이터베이스 크기를 줄일 수 있습니다.|  
|[Windows PowerShell 지원 역할 기반 액세스 제어](#bkmk_ps)|새로운|Windows PowerShell IPAM 개체에 대 한 액세스 범위를 설정 하려면 사용할 수 있습니다.|  
  
### <a name="EIP"></a>향상 된 IP 주소 관리  
다음과 같은 기능 IPAM 주소 관리 기능을 개선 합니다.  
>[!NOTE]
>Windows PowerShell IPAM 명령 참조 참조 [Windows PowerShell의 IP 주소 관리 (IPAM) 서버 Cmdlet](https://technet.microsoft.com/library/jj553807.aspx)합니다.  
  
#### <a name="support-for-31-32-and-128-subnets"></a>/31, / 32, /128 지원 서브넷  
지금 지원 /31, / 32, 및 /128 서브넷 Windows Server 2016에에서 IPAM 합니다. 예를 들어, 두 주소 서브넷 (/ IPv4 31) 지점 간 링크 스위치 사이 대해 필요할 수 있습니다. 또한 일부 스위치 단일 루프백 주소를 필요할 수 있습니다 (32 / ipv6 /128 i p v 4).  
  
#### **<a name="find-free-subnets-with-find-ipamfreesubnet"></a>찾기 IpamFreeSubnet와 무료 서브넷 찾기**  
  
이 명령을에 할당을 사용할 수 있는 서브넷 반환 IP block, 접두사 길이 및 요청한 서브넷 수 있습니다.   
  
사용 가능한 서브넷 수 요청한 서브넷 수가 보다 작은 경우 사용 가능한 서브넷 사용할 수 있는 요청 번호 보다 작으면 나타내는 경고 반환 됩니다.  
  
>[!NOTE]
>그들만 보고,이 기능이 서브넷 실제로 할당 되지 않습니다. 그러나 cmdlet 출력 수 전달할는 **추가 IpamSubnet** 명령 서브넷 만들 수 있습니다.  
  
자세한 내용은 참조 [찾기 IpamFreeSubnet](https://technet.microsoft.com/library/mt712782.aspx)합니다.  
  
#### **<a name="find-free-address-ranges-with-find-ipamfreerange"></a>찾기 IpamFreeRange 범위 무료 주소 찾기**  
  
이 새로운 명령 반환 사용할 수 있는 IP 주소 범위 IP 서브넷, 주소 고 범위 내에 필요한 수가 및 영역 요청할 수 있습니다.   
  
명령 연속 일련의 수가 요청한 주소와 일치 하는 할당된 IP 주소를 검색 합니다. 프로세스 요청된 수가 범위 발견 되 면 더 이상 사용할 수 있는 될 때까지 주소 범위를 사용할 수 있는 또는 될 때까지 반복 됩니다.  
  
> [!NOTE]
> 그들만 보고,이 기능이 범위 실제로 할당 되지 않습니다. 그러나 cmdlet 출력 수 전달할는 **추가 IpamRange** 범위를 만들기 위해 명령을 합니다.  
  
자세한 내용은 참조 [찾기 IpamFreeRange](https://technet.microsoft.com/library/mt712772.aspx)합니다.  
  
### <a name="EDNS"></a>고급 DNS 서비스 관리  
Windows Server 2016에 IPAM 지원 IPAM 실행 되 고 있는 된 Active Directory 숲 속의 파일 기반 도메인 가입, DNS 서버를 검색 합니다.  
  
또한 다음과 같은 DNS 기능 추가 되었습니다.  
  
-   DNS 영역과 리소스 컬렉션 (이외의 DNSSEC에 관한) Windows Server 2008 이상을 실행 DNS 서버에서 기록 합니다.  
  
-   구성 (, 수정, 만들고 삭제) 속성 및 모든 종류의 (이외의 DNSSEC에 관한) 리소스 레코드에 대 한 작업입니다.  
  
-   구성 (만드는, 수정, 삭제) 속성 및 모든 종류의 기본 보조, 및 스텁 영역 포함 하 여 DNS 영역에 대 한 작업).  
  
-   보조 작업 및 스텁 영역에 관계 없이 경우 발생 하거나 역방향 조회 영역 앞으로 합니다. 예를 들어,와 같은 작업을 **마스터에서 전송** 또는 **마스터에서 새로운 영역 복사본을 전송**합니다.  
  
-   역할 기반 지원된 DNS 구성 (DNS 레코드 및 DNS 영역)에 대 한 액세스를 제어 합니다.  
  
-   수집과 구성 조건부 전달자 (만들고, 삭제, 편집).  
  
### <a name="DDI"></a>통합 DNS, DHCP 및 IP 주소 (DDI) 관리  
IP 주소 목록에는 IP 주소를 볼 때 IP 주소와 연결 된 모든 DNS 리소스 기록을 보려면 자세히 보기의 옵션을가지고 있습니다.  
  
일부 DNS 리소스 기록 컬렉션으로 IPAM DNS 역방향 조회 영역이 대 한 PTR 기록을 수집합니다. 영역에 대 한 모든는 역방향 조회 하는 모든 IP 주소 범위에 매핑됩니다, IPAM 해당 매핑된 IP 주소 범위 내에 해당 영역에 속하는 모든 PTR 레코드에 대 한 IP 주소 레코드를 만듭니다. IP 주소가 이미 있는 경우 PTR 녹화는 해당 IP 주소와 연결 하기만 하면 됩니다. 역방향 조회 영역이 모든 IP 주소 범위 매핑할 수 없는 경우 IP 주소 자동으로 만들어지지 됩니다.  
  
PTR 기록 IPAM 통해 역방향 조회 영역이 만들면 위에서 설명한 대로 IP 주소 인벤토리 동일한 방식으로 업데이트 됩니다. 이후 수집 하는 동안 IP 주소, 시스템에 이미 있으므로 이후 PTR 기록 간단 하 게 매핑됩니다 해당 IP 주소를 사용 합니다.  
  
### <a name="bkmk_ad"></a>여러 Active Directory 숲 지원  
Windows Server 2012 r 2 IPAM은를 검색 하 고 IPAM 서버와 같은 Active Directory 숲에 속하는 DHCP 및 DNS 서버 관리 수 있었습니다. 이제 양방향 보안 관계가 IPAM 서버가 설치 되어 숲이 되 면 다른 광고 숲에 속하는 DNS 및 DHCP 서버 관리할 수 있습니다. 으로 이동할 수는 **서버 검색 구성** 대화 상자에서 다른 도메인 관리할 숲 신뢰할 수 있는 추가 및 합니다. 서버를 검색 한 후 동일한 숲 IPAM 설치 되어 있는에 속하는 서버와 동일 관리 경험이입니다.  
  
자세한 내용은 참조 [리소스 여러 Active Directory 숲에서 관리](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md)  
  
### <a name="bkmk_purge"></a>활용 데이터 지우기  
활용 데이터 지우기 오래 된 IP 주소 활용도 데이터를 삭제 하 여 IPAM 데이터베이스 크기를 줄일 수 있습니다. 날짜를 지정 하면 데이터 삭제를 수행 하려면 및 IPAM 보다 오래 된 모든 데이터베이스 항목을 삭제 하거나 날짜 사용자가 제공 합니다.   
  
자세한 내용은 참조 [활용도 데이터 지우기](../../technologies/ipam/Purge-Utilization-Data.md)합니다.  
  
### <a name="bkmk_ps"></a>Windows PowerShell 지원 역할 기반 액세스 제어  
이제 Windows PowerShell 역할 기반 액세스 제어 구성할 사용할 수 있습니다. Windows PowerShell 명령을 IPAM에서 DNS 및 DHCP 개체를 검색 하 고 자녀가 액세스 범위를 변경할를 사용할 수 있습니다. 이 인해 액세스 범위 다음 개체를 할당 하려면 Windows PowerShell 스크립트를 작성할 수 있습니다.  
  
-   IP 주소 공간  
  
-   IP 주소 차단  
  
-   IP 주소 서브넷  
  
-   IP 주소 범위  
  
-   DNS 서버  
  
-   DNS 영역  
  
-   DNS 조건부 전달자를 포함  
  
-   DNS 레코드 리소스  
  
-   DHCP 서버  
  
-   DHCP 대  
  
-   DHCP 범위  
  
자세한 내용은 참조 [관리 역할 기반 액세스 제어를 Windows PowerShell로](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) 및 [Windows PowerShell의 IP 주소 관리 (IPAM) 서버 Cmdlet](https://technet.microsoft.com/library/jj553807.aspx)합니다.  

