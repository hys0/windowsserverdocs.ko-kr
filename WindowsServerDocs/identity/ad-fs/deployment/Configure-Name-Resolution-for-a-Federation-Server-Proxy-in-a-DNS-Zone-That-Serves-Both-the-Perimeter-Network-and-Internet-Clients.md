---
ms.assetid: 1a6740e6-5b6d-41f8-9ec4-32cdbee3e1bb
title: "이름 확인에는 DNS 서버 Federation 프록시 Zone 해당 역할 모두 주변 네트워크 및 인터넷 클라이언트에 대 한 구성"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3b154459163b2142ff1d3aba424a86305d093de4
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-both-the-perimeter-network-and-internet-clients"></a>이름 확인에는 DNS 서버 Federation 프록시 Zone 해당 역할 모두 주변 네트워크 및 인터넷 클라이언트에 대 한 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이름 확인 federation 서버 프록시 하나 이상의 Domain Name System \(DNS\) 영역 제공 주변 네트워크 및 인터넷 클라이언트 된 Active Directory Federation Services \(AD FS\) 시나리오에 대해 성공적으로 작동 수 있도록 다음과 같은 작업을 완료할 수 해야 합니다.  
  
-   Adfs의에 대 한 모든 인터넷 클라이언트 요청에 호스트 이름을 federation 서버 프록시 해결 하기 위해 사용자를 제어 하는 인터넷 영역에서 DNS 설정 해야 합니다. 이렇게 하기 위해 federation 서버 프록시 인터넷 DNS 영역에 호스트 \(A\) 리소스 레코드를 추가 합니다.  
  
-   Adfs의에 대 한 모든 들어오는 클라이언트 요청 호스트 federation 서버에 이름을 해결 하기 위해 DNS 주변 네트워크를 설정 해야 합니다. 이를 위해 federation 서버 프록시에 대 한 주변 DNS 영역 호스트 \(A\) 리소스 레코드를 추가 합니다.  
  
> [!NOTE]  
> DNS 회사 네트워크에서 federation 서버에 대 한 호스트 \(A\) 리소스 레코드를 이미 만든 것으로 간주 합니다. 이 녹화 아직 없는 경우이 레코드를 만들고이 절차를 수행 합니다. Federation 서버에 대 한 호스트 \(A\) 리소스 기록을 생성 하는 방법에 대 한 자세한 내용은 참조 [호스트 & #40; 추가 & #41; 회사 DNS Federation 서버에 대 한 리소스 기록](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)합니다.  
  
## <a name="add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>인터넷 DNS 영역 호스트 \(A\) 리소스 레코드 federation 프록시 서버에 대 한 추가  
인터넷에 연결 클라이언트 컴퓨터 federation 서버 새로 배포 된 federation 프록시 서버를 통해 액세스할 수 있는, 되도록 호스트 \(A\) 리소스 레코드를 제어 하는 인터넷 DNS 영역에서 만들어야 합니다. 이 리소스 레코드 해결 계정 federation 서버의 호스트 이름 \ (예를 들어 fs.fabrikam.com\) 계정 federation 서버 프록시의 IP 주소를 \ (예를 들어 131.107.27.68\) 주변 네트워크에 있습니다.  
  
> [!NOTE]  
> Windows 2000 Server, Windows Server 2003, 또는 Windows Server 2008 DNS 서버 서비스와 함께 실행 DNS 서버를 사용 하는 인터넷 DNS 영역을 제어할 수 있는 것으로 간주 합니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](http://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-resource-record-to-the-internet-dns-zone-for-a-federation-server-proxy"></a>Federation 프록시 서버에 대 한 호스트 \(A\) 리소스 레코드 인터넷 DNS 영역에 추가 하려면  
  
1.  인터넷 DNS 영역에 대 한 DNS 서버를 snap\에서 DNS을 엽니다.  
  
2.  콘솔에서 나무 right\ 클릭 해당 앞으로 조회 영역이 한 다음 **새 호스트 \(A or AAAA\)**합니다.  
  
3.  **이름**만 해당 federation 서버의 컴퓨터 이름을 입력 합니다. 예를 들어 정식된 도메인 이름 \(FQDN\) fs.fabrikam.com 입력 **fs**합니다.  
  
4.  **IP 주소**, 새 federation 서버 프록시 131.107.27.68 예를 들어, IP 주소를 입력 합니다.  
  
5.  클릭 **호스트 추가**합니다.  
  
## <a name="add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>주변 DNS 영역 호스트 \(A\) 리소스 레코드 federation 프록시 서버에 대 한 추가  
인터넷 클라이언트 요청 federation 서버 프록시 성공적으로 처리 되 고 인터넷 DNS 영역 내에서 확인 된 후 federation 서버에 연결할 수 있도록 주변 DNS 영역에서 호스트 \(A\) 리소스 레코드를 만들어야 합니다. 이 리소스 레코드 해결 계정 federation 서버의 호스트 이름 \ (예: fs 합니다. fabrikam.com\) 계정 federation 서버의 IP 주소를 \ (예를 들어 192.168.1.4\) 회사의 네트워크 안에 있습니다.  
  
> [!NOTE]  
> DNS 주변 영역을 제어할 수 DNS 서버 서비스와 Windows 2000 Server, Windows Server 2003, Windows Server 2008 또는 Windows Server® 2012를 실행 하는 DNS 서버를 사용 중인 것으로 간주 합니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](http://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-resource-record-to-the-perimeter-dns-zone-for-a-federation-server-proxy"></a>Federation 프록시 서버에 대 한 주변 DNS 영역에 호스트 \(A\) 리소스 레코드를 추가 하려면  
  
1.  주변 네트워크에 대 한 DNS 서버를에서 엽니다는 **snap\에서 DNS**합니다.  
  
2.  콘솔에서 나무 right\ 클릭 해당 앞으로 조회 영역이 한 다음 **새 호스트 \(A or AAAA\)**합니다.  
  
3.  **이름**만 해당 federation 서버의 컴퓨터 이름을 입력 합니다. 예를 들어, FQDN fs.fabrikam.com 입력 **fs**합니다.  
  
4.  에 **IP 주소** IP 입력 텍스트 상자 등 192.168.1.4 회사의 네트워크 안에 federation 서버에 대 한 해결 합니다.  
  
5.  클릭 **호스트 추가**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: Federation 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Federation 서버 프록시 이름 해상도 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)  
  

