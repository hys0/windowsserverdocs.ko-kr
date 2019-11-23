---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: 경계 네트워크 및 인터넷 클라이언트 모두에서 작동하는 DNS 영역에 페더레이션 서버 프록시에 대한 이름 확인 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 118c03ada32d3cd5b198ecd238078984a38df0db
ms.sourcegitcommit: 8fbd2d877612a9feb02d7d91ed0372d7cd441d5c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71359828"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>경계 네트워크 및 인터넷 클라이언트 모두에서 작동하는 DNS 영역에 페더레이션 서버 프록시에 대한 이름 확인 구성


Active Directory Federation Services \(AD FS 페더레이션 서버 프록시에 대 한 이름 확인이 성공적으로 수행 될 수 있도록 하나 이상의 도메인 이름 시스템 \(DNS\) 영역이 경계 네트워크와 인터넷 클라이언트를 모두 제공 하는\) 시나리오는 다음 작업을 완료 해야 합니다.  
  
-   AD FS에 대 한 모든 인터넷 클라이언트 요청에 호스트 이름을 페더레이션 서버 프록시를 해결 하려면 사용자가 제어 하는 인터넷 영역에서 DNS는 구성 합니다. 호스트를 추가 하면이를 위해 \(A\) 페더레이션 서버 프록시에 대 한 인터넷 DNS 영역에 리소스 레코드입니다.  
  
-   경계 네트워크의 DNS 이름을 페더레이션 서버를 호스트 하는 AD FS에 대 한 모든 들어오는 클라이언트 요청을 해결 하려면 구성 되어야 합니다. 호스트를 추가 하면이를 위해 \(A\) 페더레이션 서버 프록시에 대 한 경계 DNS 영역에 리소스 레코드입니다.  
  
> [!NOTE]  
> 가정 하는 호스트 \(A\) 리소스 레코드는 페더레이션 서버는 회사에서 이미 만들어진 대 한 네트워크 DNS입니다. 이 레코드 아직 존재 하지 않는 경우이 레코드를 만들고이 절차를 수행 합니다. 호스트를 만드는 방법에 대 한 자세한 내용은 \(A\) 페더레이션 서버에 대 한 리소스 레코드 참조 [호스트 & #40;를 추가 합니다. & #41; 페더레이션 서버에 대해 회사 DNS에 리소스 레코드](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)합니다.  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>호스트 추가 \(A\) 페더레이션 서버 프록시에 대 한 인터넷 DNS 영역에 리소스 레코드  
호스트를 먼저 만들어야 성공적으로 클라이언트 컴퓨터에서 인터넷 새로 배포 된 페더레이션 서버 프록시를 통해 페더레이션 서버를 액세스할 수 있습니다, \(A\) 사용자가 제어 하는 인터넷 DNS 영역의 리소스 레코드입니다. 이 리소스 레코드의 계정 페더레이션 서버 호스트 이름을 확인 \(예를 들어 fs.fabrikam.com\) 계정 페더레이션 서버 프록시의 IP 주소를 \(예를 들어 131.107.27.68\) 경계 네트워크에 있습니다.  
  
> [!NOTE]  
> DNS 서버 서비스와 함께 Windows 2000 서버, Windows Server 2003 또는 Windows Server 2008를 실행 하는 DNS 서버를 사용 하 여 인터넷 DNS 영역을 제어 하는 것으로 가정 합니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>호스트를 추가 하려면 \(A\) 페더레이션 서버 프록시에 대 한 인터넷 DNS 영역에 리소스 레코드  
  
1.  인터넷 DNS 영역에 대 한 DNS 서버에서 DNS 스냅인을 열고\-에 있습니다.  
  
2.  콘솔 트리에서 마우스 오른쪽\-적용 가능한 정방향 조회 영역을 클릭 한 다음 클릭 **새 호스트 \(A 또는 AAAA\)** 합니다.  
  
3.  **이름**, 페더레이션 서버 컴퓨터 이름만 입력 합니다. 정규화 된 도메인 이름에 대 한 예를 들어 \(FQDN\) fs.fabrikam.com, 형식 **fs**합니다.  
  
4.  **IP 주소**, 예를 들어 131.107.27.68는 새 페더레이션 서버 프록시에 대 한 IP 주소를 입력 합니다.  
  
5.  **호스트 추가**를 클릭합니다.  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>호스트 추가 \(A\) 페더레이션 서버 프록시에 대 한 경계 DNS 영역에 리소스 레코드  
인터넷 클라이언트 요청 페더레이션 서버 프록시에 의해 성공적으로 처리 하 고 인터넷 DNS 영역 내에서 해결 한 후 페더레이션 서버에 연결할를 만들어야 합니다를 호스트 \(A\) 경계 DNS 영역에 리소스 레코드입니다. 이 리소스 레코드의 계정 페더레이션 서버 호스트 이름을 확인 \(fs 예를 들어 있습니다. fabrikam.com\) 계정 페더레이션 서버는의 IP 주소로 \(예를 들어 192.168.1.4\) 회사 네트워크에 있습니다.  
  
> [!NOTE]  
> DNS 서버 서비스와 함께 Windows 2000 서버, Windows Server 2003, Windows Server 2008 또는 Windows Server® 2012을 실행 하는 DNS 서버를 사용 하 여 경계 DNS 영역을 제어 하는 것으로 가정 합니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>호스트를 추가 하려면 \(A\) 페더레이션 서버 프록시에 대 한 경계 DNS 영역에 리소스 레코드  
  
1.  경계 네트워크에 대 한 DNS 서버를 열고는 **DNS 스냅\-에서**합니다.  
  
2.  콘솔 트리에서 마우스 오른쪽\-적용 가능한 정방향 조회 영역을 클릭 한 다음 클릭 **새 호스트 \(A 또는 AAAA\)** 합니다.  
  
3.  **이름**, 페더레이션 서버 컴퓨터 이름만 입력 합니다. 예를 들어 FQDN 인 fs.fabrikam.com 인 입력 **fs**합니다.  
  
4.  에 **IP 주소** 텍스트 상자를 IP를 입력 합니다. 예를 들어 192.168.1.4 회사 네트워크의 페더레이션 서버에 대 한 주소입니다.  
  
5.  **호스트 추가**를 클릭합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[페더레이션 서버 프록시에 대한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)  
  

