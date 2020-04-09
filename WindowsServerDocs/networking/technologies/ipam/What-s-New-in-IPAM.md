---
title: IPAM의 새로운 기능
description: 이 항목에서는 Windows Server 2016에서 새로 또는 변경 된 IPAM (IP 주소 관리) 기능에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: get-started-article
ms.assetid: f2f2f1a5-ac2f-41b7-a495-98ad0e2a9b20
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 5bf0dc2e55b1ff7d04045a860aa9816d47ee8417
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854796"
---
# <a name="whats-new-in-ipam"></a>IPAM의 새로운 기능

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016에서 새로 또는 변경 된 IPAM (IP 주소 관리) 기능에 대해 설명 합니다.  
  
IPAM은 엔터프라이즈 또는 CSP (클라우드 서비스 공급자) 네트워크의 IP 주소 및 DNS 인프라에 대해 사용자 지정이 뛰어난 관리 및 모니터링 기능을 제공 합니다. IPAM을 사용 하 여 DHCP (Dynamic Host Configuration Protocol) 및 DNS (도메인 이름 시스템)를 실행 하는 서버를 모니터링, 감사 및 관리할 수 있습니다.  
  
## <a name="updates-in-ipam-server"></a><a name="BKMK_IPAM2012R2"></a>IPAM 서버의 업데이트  
다음은 Windows Server 2016에서 제공 되는 IPAM의 새로운 기능 및 향상 된 기능입니다.  
  
|기능|새로운 기능 또는 향상된 기능|설명|  
|--------------------------|-------------------|---------------|  
|[향상 된 IP 주소 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|향상된 기능|IPAM 기능/32 IPv4 및 IPv6 /128 서브넷을 처리 하 고 IP 주소 블록에서 사용 가능한 IP 주소 서브넷 및 범위를 찾는 등의 시나리오에 대 한 개선 되었습니다.|  
|[향상 된 DNS 서비스 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|새로 만들기|IPAM 두 도메인에 가입 된 Active Directory 통합 및 파일 지원 DNS 서버의 DNS 리소스 레코드, 조건부 전달자 및 DNS 영역 관리를 지원합니다.|  
|[통합 DNS, DHCP 및 IP 주소 (DDI) 관리](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|향상된 기능|IP 주소와 관련 된 모든 DNS 리소스 레코드를 시각화와 같은 작업을 사용 하는 몇 가지 새로운 경험 형식 및 통합 된 수명 주기 관리의 DNS 리소스 레코드와 DNS 및 DHCP 작업을 모두에 대 한 IP 주소 수명 주기 관리에 따라 IP 주소 인벤토리를 자동화 합니다.|  
|[다중 Active Directory 포리스트 지원](#bkmk_ad)|새로 만들기|IPAM 설치 되어 있는 포리스트와 사이의 각 원격 포리스트에 양방향 트러스트 관계가 경우 여러 Active Directory 포리스트 DNS 및 DHCP 서버를 관리 하려면 IPAM을 사용할 수 있습니다.|  
|[사용률 데이터 제거](#bkmk_purge)|새로 만들기|이제 지정한 날짜 보다 오래 된 IP 주소 사용률 데이터를 제거 하 여 IPAM 데이터베이스 크기를 줄일 수 있습니다.|  
|[역할 기반 Access Control에 대 한 Windows PowerShell 지원](#bkmk_ps)|새로 만들기|IPAM 개체에 대 한 액세스 범위를 설정 하려면 Windows PowerShell을 사용할 수 있습니다.|  
  
### <a name="enhanced-ip-address-management"></a><a name="EIP"></a>향상 된 IP 주소 관리  
다음 기능은 IPAM 주소 관리 기능을 개선 합니다.  
>[!NOTE]
>IPAM Windows PowerShell 명령 참조는 [Windows powershell의 ipam (IP 주소 관리) 서버 cmdlet](https://docs.microsoft.com/powershell/module/ipamserver/)을 참조 하세요.  
  
#### <a name="support-for-31-32-and-128-subnets"></a>/31,/32 및/128 서브넷 지원  
Windows Server 2016의 IPAM은 이제/31,/32 및/128 서브넷을 지원 합니다. 예를 들어 스위치 간의 지점 간 연결에는 두 개의 주소 서브넷 (/31 IPv4)이 필요할 수 있습니다. 또한 일부 스위치에는 단일 루프백 주소가 필요할 수 있습니다 (/32, i p v 6의 경우/128의 경우).  
  
#### <a name="find-free-subnets-with-find-ipamfreesubnet"></a>**IpamFreeSubnet를 사용 하 여 사용 가능한 서브넷 찾기**  
  
이 명령은 IP 블록, 접두사 길이 및 요청 된 서브넷 수가 지정 된 경우 할당에 사용할 수 있는 서브넷을 반환 합니다.   
  
사용 가능한 서브넷 수가 요청 된 서브넷 수보다 적으면 사용할 수 있는 서브넷이 요청 된 수보다 적을 수 있음을 나타내는 경고와 함께 반환 됩니다.  
  
>[!NOTE]
>이 함수는 실제로 서브넷을 할당 하지 않으며 가용성만 보고 합니다. 그러나 cmdlet 출력을 **IpamSubnet** 명령으로 파이프 하 여 서브넷을 만들 수 있습니다.  
  
자세한 내용은 [IpamFreeSubnet](https://docs.microsoft.com/powershell/module/ipamserver/Find-IpamFreeSubnet)를 참조 하세요.  
  
#### <a name="find-free-address-ranges-with-find-ipamfreerange"></a>**IpamFreeRange를 사용 하 여 사용 가능한 주소 범위 찾기**  
  
이 새 명령은 IP 서브넷이 지정 된 사용 가능한 IP 주소 범위, 범위에 필요한 주소 수 및 요청 된 범위 수를 반환 합니다.   
  
이 명령은 요청 된 주소 수와 일치 하는 연속 된 일련의 할당 되지 않은 IP 주소를 검색 합니다. 요청 된 범위 수를 찾을 때까지 또는 사용 가능한 주소 범위가 더 이상 없을 때까지 프로세스가 반복 됩니다.  
  
> [!NOTE]
> 이 함수는 실제로 범위를 할당 하지 않으며 가용성만 보고 합니다. 그러나 cmdlet 출력을 **IpamRange** 명령으로 파이프 하 여 범위를 만들 수 있습니다.  
  
자세한 내용은 [IpamFreeRange](https://docs.microsoft.com/powershell/module/ipamserver/Find-IpamFreeRange)를 참조 하세요.  
  
### <a name="enhanced-dns-service-management"></a><a name="EDNS"></a>향상 된 DNS 서비스 관리  
이제 Windows Server 2016의 IPAM은 IPAM을 실행 하는 Active Directory 포리스트에서 파일 기반 도메인에 가입 된 DNS 서버를 검색할 수 있도록 지원 합니다.  
  
또한 다음과 같은 DNS 기능이 추가 되었습니다.  
  
-   Windows Server 2008 이상을 실행 하는 DNS 서버에서 DNS 영역 및 리소스 레코드 컬렉션 (DNSSEC에 관련 된 컬렉션 제외)  
  
-   모든 유형의 리소스 레코드에 대 한 속성 및 작업을 구성 (생성, 수정 및 삭제) 합니다 (DNSSEC와 관련 된 레코드 제외).  
  
-   기본 보조 및 스텁 영역을 포함 하 여 모든 유형의 DNS 영역에 대 한 속성 및 작업을 구성 (만들기, 수정, 삭제) 합니다.  
  
-   전방 또는 역방향 조회 영역에 관계 없이 보조 및 스텁 영역에서 작업을 트리거 했습니다. 예를 들어 **master에서 전송** 또는 **master에서 새 영역 복사본 전송과**같은 작업이 있습니다.  
  
-   지원 되는 DNS 구성 (DNS 레코드 및 DNS 영역)에 대 한 역할 기반 액세스 제어  
  
-   조건부 전달자 컬렉션 및 구성 (만들기, 삭제, 편집).  
  
### <a name="integrated-dns-dhcp-and-ip-address-ddi-management"></a><a name="DDI"></a>통합 DNS, DHCP 및 IP 주소 (DDI) 관리  
Ip 주소 인벤토리에서 ip 주소를 볼 때 세부 정보 보기에 IP 주소와 연결 된 모든 DNS 리소스 레코드를 표시 하는 옵션이 있습니다.  
  
DNS 리소스 레코드 컬렉션의 일부로 IPAM은 DNS 역방향 조회 영역에 대 한 PTR 레코드를 수집 합니다. 모든 IP 주소 범위에 매핑된 모든 역방향 조회 영역에 대해 IPAM은 해당 하는 매핑된 IP 주소 범위에서 해당 영역에 속하는 모든 PTR 레코드에 대 한 IP 주소 레코드를 만듭니다. IP 주소가 이미 있는 경우 PTR 레코드는 해당 IP 주소에만 연결 됩니다. 역방향 조회 영역을 IP 주소 범위에 매핑하지 않은 경우 IP 주소가 자동으로 생성 되지 않습니다.  
  
IPAM을 통해 역방향 조회 영역에서 PTR 레코드를 만드는 경우 IP 주소 인벤토리가 위에서 설명한 것과 동일한 방식으로 업데이트 됩니다. 이후에 수집 하는 동안 IP 주소가 시스템에 이미 존재 하기 때문에 PTR 레코드는 해당 IP 주소를 사용 하 여 간단히 매핑됩니다.  
  
### <a name="multiple-active-directory-forest-support"></a><a name="bkmk_ad"></a>다중 Active Directory 포리스트 지원  
Windows Server 2012 r 2에서 IPAM은 IPAM 서버와 동일한 Active Directory 포리스트에 속하는 DNS 및 DHCP 서버를 검색 하 고 관리할 수 있었습니다. 이제 IPAM 서버가 설치 된 포리스트와 양방향 트러스트 관계가 있는 경우 다른 AD 포리스트에 속한 DNS 및 DHCP 서버를 관리할 수 있습니다. **서버 검색 구성** 대화 상자로 이동 하 여 관리 하려는 다른 트러스트 된 포리스트의 도메인을 추가할 수 있습니다. 서버를 검색 한 후에는 IPAM이 설치 된 동일한 포리스트에 속하는 서버에 대 한 관리 환경이 동일 합니다.  
  
자세한 내용은 [여러 Active Directory 포리스트에서 리소스 관리](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md) 를 참조 하세요.  
  
### <a name="purge-utilization-data"></a><a name="bkmk_purge"></a>사용률 데이터 제거  
사용률 데이터 제거를 사용 하면 오래 된 IP 주소 사용률 데이터를 삭제 하 여 IPAM 데이터베이스 크기를 줄일 수 있습니다. 데이터 삭제를 수행 하려면 날짜를 지정 하 고 IPAM은 사용자가 제공한 날짜 보다 오래 되었거나 같은 모든 데이터베이스 항목을 삭제 합니다.   
  
자세한 내용은 [사용률 데이터 제거](../../technologies/ipam/Purge-Utilization-Data.md)를 참조 하세요.  
  
### <a name="windows-powershell-support-for-role-based-access-control"></a><a name="bkmk_ps"></a>역할 기반 Access Control에 대 한 Windows PowerShell 지원  
이제 Windows PowerShell을 사용 하 여 Access Control 따라 역할을 구성할 수 있습니다. Windows PowerShell 명령을 사용 하 여 IPAM의 DNS 및 DHCP 개체를 검색 하 고 해당 액세스 범위를 변경할 수 있습니다. 이로 인해 다음 개체에 액세스 범위를 할당 하는 Windows PowerShell 스크립트를 작성할 수 있습니다.  
  
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
  
자세한 내용은 windows powershell을 [사용 하 여 역할 기반 Access Control 관리](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) 및 [WINDOWS powershell의 IPAM (IP 주소 관리) 서버 cmdlet](https://docs.microsoft.com/powershell/module/ipamserver/)을 참조 하세요.  

