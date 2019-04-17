---
ms.assetid: b7109e46-b66e-4c5c-8b87-a6611d68415a
title: "이름 확인 Federation 서버 프록시 주변 네트워크만 사용 하는 DNS 영역에 대해 구성"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 32b8e3cc133ce95872881115608bb8cfb17b2427
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-name-resolution-for-a-federation-server-proxy-in-a-dns-zone-that-serves-only-the-perimeter-network"></a>이름 확인 Federation 서버 프록시 주변 네트워크만 사용 하는 DNS 영역에 대해 구성

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이름 확인 federation 서버에서 하나 이상의 Domain Name System \(DNS\) 영역 주변 네트워크만 제공 된 Active Directory Federation Services \(AD FS\) 시나리오에서 제대로 작동, 되도록 다음 작업이 완료 해야 합니다.  
  
-   Federation 서버의 IP 주소를 추가 하려면 해당 federation 서버 프록시에 호스트 파일을 업데이트 해야 합니다.  
  
-   Adfs의에 대 한 모든 클라이언트 요청에 호스트 이름을 federation 서버 프록시 해결 하기 위해 DNS 주변 네트워크를 설정 해야 합니다. 이 위해 federation 서버 프록시에 대 한 주변 DNS에 호스트 \(A\) 리소스 레코드를 추가 합니다.  
  
> [!NOTE]  
> 이 절차 가정 DNS 회사 네트워크에서 federation 서버에 대 한 호스트 \(A\) 리소스 레코드를 이미 만든 합니다. 이 녹화 아직 없는 경우이 레코드를 만들고이 절차를 수행 합니다. Federation 서버에 대 한 호스트 \(A\) 리소스 레코드를 만드는 방법에 대 한 자세한 내용은 참조 [호스트 & #40; 추가 & #41; 회사 DNS Federation 서버에 대 한 리소스 기록](Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)합니다.  
  
## <a name="add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>호스트 파일에 federation 서버의 IP 주소 추가  
항목 federation 서버의 DNS 호스트 이름 가리키는 해당 federation 서버 프록시에 호스트 파일에 추가 해야 작동 하도록 federation 서버 프록시 계정 파트너의 주변 네트워크 예상 대로, \ (예를 들어 fs.fabrikam.com\) 및 IP 주소 \ (예를 들어 192.168.1.4\) 계정 파트너 회사 네트워크에서 합니다. 호스트 파일이 항목을 추가 하면 federation 서버 프록시를 federation 서버에 계정 파트너 client\ 시작 전화 해결 하기 위해 자체 문의 수 없습니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-the-ip-address-of-a-federation-server-to-the-hosts-file"></a>호스트 파일에 federation 서버의 IP 주소를 추가 하려면  
  
1.  %Systemroot%\\Winnt\\System32\\Drivers 디렉터리 폴더로 이동 하 고 찾고 있는 **호스트** 파일.  
  
2.  메모장을 시작한 다음 엽니다는 **호스트** 파일.  
  
3.  IP 주소와 federation 서버의 호스트 이름을 계정 파트너에 추가 **호스트** 파일 다음과 같이 합니다.  
  
    **192.168.1.4fs.fabrikam.com**  
  
4.  저장 한 파일을 닫습니다.  
  
## <a name="add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>DNS 주변에 호스트 \(A\) 리소스 레코드 federation 프록시 서버에 대 한 추가  
인터넷에서 클라이언트 federation 서버 새로 배포 된 federation 프록시 서버를 통해 액세스할 수 있는, 되도록 호스트 \(A\) 리소스 레코드 DNS 주변에 만들어야 합니다. 이 리소스 레코드 해결 계정 federation 서버의 호스트 이름 \ (예를 들어 fs.fabrikam.com\) 계정 federation 서버 프록시의 IP 주소를 \ (예를 들어 131.107.27.68\) 주변 네트워크에 있습니다.  
  
> [!NOTE]  
> 가정 사용 하 고 있는지 DNS 서버, Windows 2000 Server, Windows Server 2003, 또는 Windows Server 2008 DNS 서버 서비스와 함께 실행 DNS 주변 영역을 제어할 수 있습니다.  
  
회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
#### <a name="to-add-a-host-a-resource-record-to-perimeter-dns-for-a-federation-server-proxy"></a>Federation 프록시 서버에 대 한 주변 DNS에 호스트 \(A\) 리소스 레코드를 추가 하려면  
  
1.  주변 네트워크에 대 한 DNS 서버를 snap\에서 DNS을 엽니다. 클릭 **시작**를 가리킨 **관리 도구**을 차례로 클릭 하 고 **DNS**합니다.  
  
2.  콘솔에서 나무 right\ 클릭 해당 앞으로 조회 영역이 한 다음 **새 호스트 \(A or AAAA\)**합니다.  
  
3.  **이름**만 해당 federation 서버의 컴퓨터 이름을 입력 합니다. 예를 들어 정식된 도메인 이름 \(FQDN\) fs.fabrikam.com 입력 **fs**합니다.  
  
4.  **IP 주소**, 예를 들어 새 federation 서버 프록시 IP 주소를 입력 **131.107.27.68**합니다.  
  
5.  클릭 **호스트 추가**합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: Federation 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Federation 서버 프록시 이름 해상도 요구 사항](https://technet.microsoft.com/library/dd807055.aspx)  
  

