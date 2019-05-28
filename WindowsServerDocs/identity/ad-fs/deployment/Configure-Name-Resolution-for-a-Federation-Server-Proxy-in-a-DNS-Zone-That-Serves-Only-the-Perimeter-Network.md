---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: 경계 네트워크에서만 작동하는 DNS 영역에 페더레이션 서버 프록시에 대한 이름 확인 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7d046c720c5c6250b6efa03e068aa66e2a6bbe3d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192299"
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>경계 네트워크에서만 작동하는 DNS 영역에 페더레이션 서버 프록시에 대한 이름 확인 구성


페더레이션 서버는 Active Directory Federation Services에 대 한 이름 확인이 성공적으로 작업할 수 있도록 \(AD FS\) 시나리오는 하나 이상의 도메인 이름 시스템 \(DNS\) 영역 경계 에서만 제공 네트워크, 다음 작업을 완료 해야 합니다.  
  
-   페더레이션 서버의 IP 주소를 추가 하려면 호스트 파일에 페더레이션 서버 프록시를 업데이트 해야 합니다.  
  
-   AD FS에 대 한 모든 클라이언트 요청에 호스트 이름을 페더레이션 서버 프록시를 해결 하려면 경계 네트워크에 DNS는 구성 합니다. 호스트를 추가 하면이 위해 \(A\) 페더레이션 서버 프록시에 대 한 경계 DNS에 리소스 레코드입니다.  
  
> [!NOTE]  
> 이러한 절차를 가정 하는 호스트 \(A\) 리소스 레코드는 페더레이션 서버는 회사에서 이미 만들어진 대 한 네트워크 DNS입니다. 이 레코드 아직 존재 하지 않는 경우이 레코드를 만들고이 절차를 수행 합니다. 호스트를 만드는 방법에 대 한 자세한 내용은 \(A\) 페더레이션 서버에 대 한 리소스 레코드 참조 [호스트 & #40;를 추가 합니다. & #41; 페더레이션 서버에 대해 회사 DNS에 리소스 레코드](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)합니다.  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>호스트 파일에 페더레이션 서버의 IP 주소를 추가 합니다.  
호스트 파일을 가리키는 페더레이션 서버의 DNS 호스트 이름에 해당 페더레이션 서버 프록시에는 항목을 추가 해야 작동 하도록 페더레이션 서버 프록시 계정 파트너의 경계 네트워크에서 예상 대로, \(예를 들어 fs.fabrikam.com\) 및 IP 주소 \(예를 들어 192.168.1.4\) 계정 파트너의 회사 네트워크에 있습니다. 페더레이션 서버 프록시 클라이언트를 해결 하려면 자체에서 방지 hosts 파일에이 항목을 추가\-는 페더레이션 서버는 계정 파트너의 호출을 시작 합니다.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>호스트 파일에 페더레이션 서버의 IP 주소를 추가 하려면  
  
1.  % Systemroot %로 이동\\Winnt\\System32\\드라이버 디렉터리 폴더 찾아서는 **호스트** 파일입니다.  
  
2.  메모장을 시작 하 고 엽니다는 **호스트** 파일입니다.  
  
3.  페더레이션 서버의 호스트 이름과 IP 주소에는 계정 파트너의 추가 **호스트** 다음 예와에서 같이 파일:  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  파일을 저장하고 닫습니다.  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>호스트 추가 \(A\) 페더레이션 서버 프록시에 대 한 경계 DNS에 리소스 레코드  
호스트를 먼저 만들어야 인터넷의 클라이언트를 성공적으로 새로 배포 된 페더레이션 서버 프록시를 통해 페더레이션 서버에 액세스할 수, 있도록 \(A\) 경계 DNS에에서 리소스 레코드입니다. 이 리소스 레코드의 계정 페더레이션 서버 호스트 이름을 확인 \(예를 들어 fs.fabrikam.com\) 계정 페더레이션 서버 프록시의 IP 주소를 \(예를 들어 131.107.27.68\) 경계 네트워크에 있습니다.  
  
> [!NOTE]  
> 사용 하는 DNS 서버를 Windows 2000 Server, Windows Server 2003 또는 Windows Server 2008 DNS 서버 서비스와 함께 실행 경계 DNS 영역을 제어 하 간주 됩니다.  
  
멤버 자격이 **관리자**, 또는 이와 동등한 최소한이이 절차를 완료 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>호스트를 추가 하려면 \(A\) 페더레이션 서버 프록시에 대 한 경계 DNS에 리소스 레코드  
  
1.  경계 네트워크에 대 한 DNS 서버에서 DNS 스냅인을 열고\-에 있습니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **DNS**합니다.  
  
2.  콘솔 트리에서 마우스 오른쪽\-적용 가능한 정방향 조회 영역을 클릭 한 다음 클릭 **새 호스트 \(A 또는 AAAA\)** 합니다.  
  
3.  **이름**, 페더레이션 서버 컴퓨터 이름만 입력 합니다. 정규화 된 도메인 이름에 대 한 예를 들어 \(FQDN\) fs.fabrikam.com, 형식 **fs**합니다.  
  
4.  **IP 주소**, 예를 들어 새 페더레이션 서버 프록시에 대 한 IP 주소를 입력 **131.107.27.68**합니다.  
  
5.  **호스트 추가**를 클릭합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[페더레이션 서버 프록시에 대한 이름 확인 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)  
  

