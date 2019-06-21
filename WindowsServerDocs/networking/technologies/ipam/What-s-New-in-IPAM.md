---
title: IPAM의 새로운 기능
description: 이 항목에서는 Windows Server 2016의 새롭거나 변경 된 IP 주소 관리 (IPAM) 기능을 설명 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f2f2f1a5-ac2f-41b7-a495-98ad0e2a9b20
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 64de9327dedadbe421e4cceb71496de3609be398
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283819"
---
# <a name="whats-new-in-ipam"></a>IPAM의 새로운 기능

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016의 새롭거나 변경 된 IP 주소 관리 (IPAM) 기능을 설명 합니다.  
  
IPAM은 엔터프라이즈 또는 클라우드 서비스 공급자 (CSP) 네트워크에서 IP 주소 및 DNS 인프라에 대 한 고도로 사용자 지정 가능한 관리 및 모니터링 기능을 제공합니다. 모니터링, 감사 하 고 IPAM을 사용 하 여 동적 호스트 구성 프로토콜 (DHCP) 및 도메인 이름 시스템 (DNS)를 실행 하는 서버를 관리할 수 있습니다.  
  
## <a name="BKMK_IPAM2012R2"></a>IPAM 서버에서 업데이트  
Windows Server 2016에서 IPAM에 대 한 새로운 기능과 향상 된 기능은 다음과 같습니다.  
  
|기능|새로운 기능 또는 향상된 기능|설명|  
|--------------------------|-------------------|---------------|  
|[향상 된 IP 주소 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|향상된 기능|IPAM 기능/32 IPv4 및 IPv6 /128 서브넷을 처리 하 고 IP 주소 블록에서 사용 가능한 IP 주소 서브넷 및 범위를 찾는 등의 시나리오에 대 한 개선 되었습니다.|  
|[향상 된 DNS 서비스 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|단추를 사용하여 새|IPAM 두 도메인에 가입 된 Active Directory 통합 및 파일 지원 DNS 서버의 DNS 리소스 레코드, 조건부 전달자 및 DNS 영역 관리를 지원합니다.|  
|[통합 된 DNS, DHCP 및 IP 주소 (DDI) 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|향상된 기능|IP 주소와 관련 된 모든 DNS 리소스 레코드를 시각화와 같은 작업을 사용 하는 몇 가지 새로운 경험 형식 및 통합 된 수명 주기 관리의 DNS 리소스 레코드와 DNS 및 DHCP 작업을 모두에 대 한 IP 주소 수명 주기 관리에 따라 IP 주소 인벤토리를 자동화 합니다.|  
|[여러 Active Directory 포리스트 지원](#bkmk_ad)|단추를 사용하여 새|IPAM 설치 되어 있는 포리스트와 사이의 각 원격 포리스트에 양방향 트러스트 관계가 경우 여러 Active Directory 포리스트 DNS 및 DHCP 서버를 관리 하려면 IPAM을 사용할 수 있습니다.|  
|[사용률 데이터 제거](#bkmk_purge)|단추를 사용하여 새|이제 사용자가 지정한 날짜 보다 오래 된 IP 주소 사용률 데이터를 제거 하 여 IPAM 데이터베이스 크기를 줄일 수 있습니다.|  
|[역할 기반 Access Control에 대 한 Windows PowerShell 지원](#bkmk_ps)|단추를 사용하여 새|IPAM 개체에 대 한 액세스 범위를 설정 하려면 Windows PowerShell을 사용할 수 있습니다.|  
  
### <a name="EIP"></a>향상 된 IP 주소 관리  
다음과 같은 기능 IPAM 주소 관리 기능을 개선 합니다.  
>[!NOTE]
>IPAM Windows PowerShell 명령 참조를 참조 하십시오 [Windows PowerShell의 IPAM IP 주소 관리 () 서버 Cmdlet](https://docs.microsoft.com/powershell/module/ipamserver/)합니다.  
  
#### <a name="support-for-31-32-and-128-subnets"></a>/31 지원, / 32, /128 서브넷  
Windows Server 2016 이제 /31, / 32, 및 /128 지원 서브넷에 IPAM. 예를 들어, 두 주소 서브넷 (/ 31 IPv4) 스위치 간에 지점 간 연결에 필요할 수 있습니다. 또한 일부 스위치 단일 루프백 주소를 필요할 수 있습니다 (/ 32 ipv4, ipv6 /128).  
  
#### <a name="find-free-subnets-with-find-ipamfreesubnet"></a>**찾기 IpamFreeSubnet를 사용 하 여 사용 가능한 서브넷 찾기**  
  
이 명령은 반환 할당에 사용할 수 있는 서브넷 IP 블록, 접두사 길이 및 요청 된 서브넷의 수를 지정 합니다.   
  
사용 가능한 서브넷 수가 요청 된 서브넷의 수보다 적은 경우 사용 가능한 서브넷을 사용할 수 있는 요청 된 수보다 작습니다 나타내는 경고와 함께 반환 됩니다.  
  
>[!NOTE]
>이 함수는 실제로 서브넷을 할당 하지 않고 해당 가용성만 보고 합니다. 하지만 Cmdlet 출력을 파이프 될 수 있습니다 합니다 **추가 IpamSubnet** 서브넷을 만드는 명령입니다.  
  
자세한 내용은 [찾기 IpamFreeSubnet](https://docs.microsoft.com/powershell/module/ipamserver/Find-IpamFreeSubnet)합니다.  
  
#### <a name="find-free-address-ranges-with-find-ipamfreerange"></a>**찾기 IpamFreeRange를 사용 하 여 사용 가능한 주소 범위를 찾기**  
  
이 새 명령 반환 사용 가능한 IP 주소 범위 지정 된 IP 서브넷, 주소 범위에서 필요한 수 및 요청 범위의 수.   
  
이 명령은 연속 된 일련의 요청 된 주소의 수와 일치 하는 할당 되지 않은 IP 주소를 검색 합니다. 프로세스, 요청된 된 범위 수 없거나 또는 주소 범위를 사용할 수 없을 때까지 더 이상 사용할 수 있는 때까지 반복 됩니다.  
  
> [!NOTE]
> 이 함수는 실제로 범위를 할당 하지 않고 해당 가용성만 보고 합니다. 하지만 Cmdlet 출력을 파이프 될 수 있습니다 합니다 **추가 IpamRange** 범위를 만드는 명령입니다.  
  
자세한 내용은 [찾기 IpamFreeRange](https://docs.microsoft.com/powershell/module/ipamserver/Find-IpamFreeRange)합니다.  
  
### <a name="EDNS"></a>향상 된 DNS 서비스 관리  
이제 Windows Server 2016에서 IPAM IPAM 실행 되는 Active Directory 포리스트에 파일 기반, 도메인에 가입 된 DNS 서버 검색을 지원 합니다.  
  
또한 다음 DNS 함수가 추가 되었습니다.  
  
-   Windows Server 2008 이상을 실행 하는 DNS 서버에서 DNS 영역 및 리소스 컬렉션 (이외의 DNSSEC 관련)를 기록 합니다.  
  
-   구성 (만들기, 수정 및 삭제) 속성과 (이외의 DNSSEC 관련) 리소스 레코드의 모든 형식에 대 한 작업입니다.  
  
-   구성 (만들기, 수정, 삭제) 속성 및 모든 형식의 기본 보조 및 스텁 영역을 포함 하 여 DNS 영역에 대 한 작업).  
  
-   경우에 트리거됩니다 보조 복제본에서 작업 및 스텁 영역에 관계 없이 정방향 또는 역방향 조회 영역. 예를 들어,와 같은 작업 **마스터에서 전송** 하거나 **마스터에서 영역의 새 복사본을 전송**합니다.  
  
-   지원 되는 DNS 구성 DNS 레코드와 DNS 영역에 대 한 역할 기반 액세스 제어 합니다.  
  
-   조건부 전달자 컬렉션 및 구성 (만들기, 삭제, 편집).  
  
### <a name="DDI"></a>통합 된 DNS, DHCP 및 IP 주소 (DDI) 관리  
IP 주소에 IP 주소 인벤토리를 볼 때에 옵션을 다음 세부 정보 보기 IP 주소에 연결 된 모든 DNS 리소스 레코드에 있습니다.  
  
DNS 리소스 레코드 컬렉션의 일환으로, IPAM은 DNS 역방향 조회 영역에 대 한 PTR 레코드를 수집합니다. IPAM 모든는 역방향 조회 영역에 대 한 모든 IP 주소 범위에 매핑되는 매핑된 해당 IP 주소 범위에서 해당 영역에 속하는 모든 PTR 레코드에 대 한 IP 주소 레코드를 만듭니다. IP 주소를 이미 있는 경우 PTR 레코드는 IP 주소를 사용 하 여 단순히 관련이 있습니다. 역방향 조회 영역을 모든 IP 주소 범위에 매핑되지 않은 경우 IP 주소를 자동으로 만들어지지 않습니다.  
  
IPAM 통해 역방향 조회 영역에 PTR 레코드가 만들어지면, 위에서 설명한 것 처럼 동일한 방식으로 IP 주소 인벤토리 업데이트 됩니다. 후속 수집 하는 동안 시스템에서 IP 주소를 이미 존재 하므로 PTR 레코드를 단순히 매핑될 해당 IP 주소를 사용 하 여 합니다.  
  
### <a name="bkmk_ad"></a>여러 Active Directory 포리스트 지원  
Windows Server 2012 R2의 IPAM에서 검색 하 고 IPAM 서버와 동일한 Active Directory 포리스트에 속하는 DNS 및 DHCP 서버를 관리할 수 있습니다. 이제 IPAM 서버 설치 되어 있는 포리스트와 양방향 트러스트 관계가 있는 경우 다른 AD 포리스트에 속하는 DNS 및 DHCP 서버를 관리할 수 있습니다. 이동할 수 있습니다 합니다 **서버 검색 구성** 대화 상자 및 도메인을 다른 관리 하려는 포리스트를 신뢰할 수 있는 추가 합니다. 서버 검색 되 면 관리 환경은 IPAM 설치 되어 있는 동일한 포리스트에 속해 있는 서버에서와 동일 합니다.  
  
자세한 내용은 참조 하세요. [여러 Active Directory 포리스트에 대 한 리소스 관리](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md)  
  
### <a name="bkmk_purge"></a>사용률 데이터 제거  
사용률 데이터 제거를 사용 하면 이전 IP 주소 사용률 데이터를 삭제 하 여 IPAM 데이터베이스 크기를 줄일 수 있습니다. 날짜를 지정 하면 데이터 삭제를 수행 하려면 및 IPAM 보다 오래 된 모든 데이터베이스 항목을 삭제 또는 제공한 날짜와 같게 됩니다.   
  
자세한 내용은 [사용률 데이터 지우기](../../technologies/ipam/Purge-Utilization-Data.md)합니다.  
  
### <a name="bkmk_ps"></a>역할 기반 Access Control에 대 한 Windows PowerShell 지원  
이제 역할 기반 Access Control을 구성 하려면 Windows PowerShell을 사용할 수 있습니다. IPAM에서 DNS 및 DHCP 개체를 검색 하 고 해당 액세스 범위를 변경 하려면 Windows PowerShell 명령을 사용할 수 있습니다. 이 인해 개체에 대 한 액세스 범위를 할당 하는 Windows PowerShell 스크립트를 작성할 수 있습니다.  
  
-   IP 주소 공간  
  
-   IP 주소 블록  
  
-   IP 주소 서브넷  
  
-   IP 주소 범위  
  
-   DNS 서버  
  
-   DNS 영역  
  
-   DNS 조건부 전달자  
  
-   DNS 리소스 레코드  
  
-   DHCP 서버  
  
-   DHCP 대범위  
  
-   DHCP 범위  
  
자세한 내용은 [역할 기반 Access Control 관리 Windows PowerShell을 사용 하 여](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) 하 고 [Windows PowerShell의 IPAM IP 주소 관리 () 서버 Cmdlet](https://docs.microsoft.com/powershell/module/ipamserver/)합니다.  

