---
ms.assetid: c28c60ff-693d-49ee-a75b-58f24866217b
title: 페더레이션 서버 프록시에 대한 이름 확인 요구 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a94e4de181cd8794d479bbd6695a94658aba0f86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855024"
---
# <a name="name-resolution-requirements-for-federation-server-proxies"></a>페더레이션 서버 프록시에 대한 이름 확인 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

인터넷 상의 클라이언트 컴퓨터를 Active Directory Federation Services에서 보호 되는 응용 프로그램에 액세스 하려고 하는 경우 \(AD FS\), 먼저 페더레이션 서버에 인증 해야 합니다. 대부분의 경우에서 페더레이션 서버 없는 일반적으로 인터넷에서 직접 액세스할 수 있습니다. 따라서 인터넷 클라이언트 컴퓨터 리디렉션되어야 페더레이션 서버 프록시를 대신 합니다. 적절 한 도메인 이름 시스템을 추가 하 여 성공적인 리디렉션을 수행할 수 있습니다 \(DNS\) 레코드 DNS 영역 또는 인터넷 직면 하는 영역입니다.  
  
페더레이션 서버 프록시에 인터넷 클라이언트가 리디렉션할 사용 하는 메서드 경계 네트워크의 DNS 영역 구성 방법 또는 인터넷에서 사용자가 제어 하는 DNS 영역 구성 방법에 따라 달라 집니다. 페더레이션 서버 프록시는 경계 네트워크에서 사용하기 위한 것입니다. 이러한 속성 리디렉션합니다 인터넷 클라이언트 요청을 페더레이션 서버 성공적으로 DNS 모든 인터넷에 올바르게 구성 된 경우에\-사용자가 제어 하는 영역을 연결 합니다. 인터넷의 구성에 따라서\-영역 연결-있는지 여부는 경계 네트워크에만 서비스를 제공 하는 DNS 영역 또는 경계 네트워크와 인터넷 클라이언트가 서비스를 제공 하는 DNS 영역-이 중요 합니다.  
  
이 항목에서는 페더레이션 서버 프록시가 경계 네트워크에 배치 하면 이름 확인을 구성할 수 있는 단계를 설명 합니다. 수행할 단계를 결정하려면 먼저 다음 DNS 시나리오 중 조직의 경계 네트워크에 있는 DNS 인프라와 가장 일치하는 시나리오를 결정합니다. 그런 다음 해당 시나리오에 대한 단계를 수행합니다.  
  
## <a name="dns-zone-serving-only-the-perimeter-network"></a>경계 네트워크만 제공하는 DNS 영역  
이 시나리오에서 조직은 경계 네트워크에 하나 또는 두 개의 DNS 영역을 갖고 조직은 인터넷의 DNS 영역을 제어하지 않습니다. 경계 네트워크 시나리오에만 사용 되는 DNS 영역에 페더레이션 서버 프록시에 대 한 성공적인 이름 확인은 다음 조건에 따라 달라 집니다.  
  
-   페더레이션 서버 프록시는 정규화 된 도메인 이름 확인을 호스트 파일에 설정이 있어야 \(FQDN\) 페더레이션 서버 또는 페더레이션 서버 클러스터의 IP 주소로 페더레이션 서버 끝점 URL입니다.  
  
-   페더레이션 서버 끝점 URL의 FQDN의 페더레이션 서버 프록시 IP 주소로 확인 되도록 하는 계정 파트너의 경계 네트워크에 DNS는 구성 합니다.  
  
다음 그림과 해당 단계에서는 이러한 각 조건이 지정된 예에서 어떻게 달성되는지를 보여 줍니다. 이 그림에서 Microsoft 네트워크 부하 분산 \(NLB\) 기술을 단일, 클러스터 FQDN 및 단일 기존 페더레이션 서버 팜에 대 한 클러스터 IP 주소를 제공 합니다.  
  
![이름 요구 사항](media/adfs2_deploy_single_fs.gif)  
  
클러스터 IP 주소 또는 클러스터 FQDN 구성 하는 방법에 대 한 자세한 내용은 참조 NLB를 사용 하 여 [클러스터 매개 변수 지정](https://go.microsoft.com/fwlink/?LinkId=75282)합니다.  
  
### <a name="1-configure-the-hosts-file-on-the-federation-server-proxy"></a>1. 페더레이션 서버 프록시에 호스트 파일 구성  
계정 파트너 페더레이션 서버 프록시에는 실제 계정 페더레이션 서버의 IP 주소를 fs.fabrikam.com을 확인 하기 위해 로컬 hosts 파일에 항목이 경계 네트워크에 DNS로 계정 페더레이션 서버 프록시에 fs.fabrikam.com에 대 한 모든 요청을 해결 하려면 구성 \(또는 페더레이션 서버 팜에 대 한 클러스터 DNS 이름을\) 회사 네트워크에 연결 된. 그러면 계정 페더레이션 서버는 아닌 자체 호스트 이름 fs.fabrikam.com를 해결 하려면 계정 페더레이션 서버 프록시에 대 한 수-fs.fabrikam.com 경계 DNS를 사용 하 여 조회 하려고 할 경우 발생 하는 대로-페더레이션 서버 프록시가 페더레이션 서버와 통신할 수 있도록 합니다.  
  
### <a name="2-configure-perimeter-dns"></a>2. 경계 DNS 구성  
단일 AD FS 호스트 이름만 클라이언트 컴퓨터에 전송 되 있기 때문에-은 인트라넷 이나 인터넷에-경계 DNS 서버를 사용 하는 인터넷에서 클라이언트 컴퓨터 계정 페더레이션 서버에 대 한 FQDN을 해결 해야 \(fs.fabrikam.com\) 계정 페더레이션 서버 프록시가 경계 네트워크의 IP 주소를 합니다. 경계 DNS 포함 된 단일 호스트 제한 corp.fabrikam.com 이라는 DNS 영역 fs.fabrikam.com 해결 하려고 할 때 클라이언트 계정 페더레이션 서버 프록시에 전달할 수 있습니다, 있도록 \(A\) fs에 대 한 리소스 레코드 \(fs.fabrikam.com\) 및 계정 페더레이션 서버 프록시가 경계 네트워크의 IP 주소입니다.  
  
페더레이션 서버 프록시의 호스트 파일을 수정 하 고 경계 네트워크에 DNS를 구성 하는 방법에 대 한 자세한 내용은 참조 [경계 네트워크 에서만 작동 하는 DNS 영역에 페더레이션 서버 프록시에 대 한 이름 확인 구성](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)합니다.  
  
## <a name="dns-zone-serving-both-the-perimeter-network-and-internet-clients"></a>경계 네트워크와 인터넷 클라이언트를 모두 제공하는 DNS 영역  
이 시나리오에서 조직은 경계 네트워크의 DNS 영역과 인터넷에 있는 하나 이상의 DNS 영역을 제어합니다. 이 시나리오에서 페더레이션 서버 프록시에 대 한 성공적인 이름 확인은 다음 조건에 따라 달라 집니다.  
  
-   페더레이션 서버 호스트 이름의 FQDN의 페더레이션 서버 프록시가 경계 네트워크의 IP 주소로 확인 되도록 하는 계정 파트너의 인터넷 영역에서 DNS는 구성 합니다.  
  
-   페더레이션 서버 호스트 이름의 FQDN을 회사 네트워크의 페더레이션 서버의 IP 주소로 확인 되도록 하는 계정 파트너의 경계 네트워크에 DNS는 구성 합니다.  
  
다음 그림과 해당 단계에서는 이러한 각 조건이 지정된 예에서 어떻게 달성되는지를 보여 줍니다.  
  
![이름 요구 사항](media/adfs2_deploy_fsp_3DNS.gif)  
  
### <a name="1-configure-perimeter-dns"></a>1. 경계 DNS 구성  
이 시나리오에 대 한 인터넷 DNS 영역 구성한 가정 하기 때문에 해결 하려면 제어 하는 만든 요청 특정 끝점 URL에 대 한 \(fs.fabrikam.com 즉,\) 경계 네트워크의 페더레이션 서버 프록시를 구성 해야 영역에서 경계 DNS에 회사 네트워크의 페더레이션 서버에 이러한 요청을 전달 합니다.  
  
경계 DNS 단일 호스트로 구성 된 fs.fabrikam.com 해결 하려는 클라이언트를 계정 페더레이션 서버에 전달할 수 있도록 \(A\) fs에 대 한 리소스 레코드 \(fs.fabrikam.com\) 및 계정 페더레이션 서버는 회사 네트워크의 IP 주소입니다. 그러면 계정 페더레이션 서버는 아닌 자체 호스트 이름 fs.fabrikam.com를 해결 하려면 계정 페더레이션 서버 프록시에 대 한 수-인터넷 DNS를 사용 하 여 fs.fabrikam.com을 조회 하려는 경우 발생 하는 대로-페더레이션 서버 프록시가 페더레이션 서버와 통신할 수 있도록 합니다.  
  
### <a name="2-configure-internet-dns"></a>2. 인터넷 DNS 구성  
이 시나리오에서 이름 확인에 성공하려면 인터넷에서 fs.fabrikam.com에 대한 클라이언트 컴퓨터의 모든 요청을 제어하는 인터넷 DNS 영역으로 확인해야 합니다. 따라서 fs.fabrikam.com의 계정 페더레이션 서버 프록시가 경계 네트워크의 IP 주소에 대 한 클라이언트 요청을 전달 하 여 인터넷 DNS 영역을 구성 해야 합니다.  
  
경계 네트워크와 인터넷 DNS 영역을 수정 하는 방법에 대 한 자세한 내용은 참조 [DNS 영역을 역할 모두 경계 네트워크 및 인터넷 클라이언트에서 페더레이션 서버 프록시에 대 한 이름 확인 구성](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의에서 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
