---
ms.assetid: c28c60ff-693d-49ee-a75b-58f24866217b
title: "Federation 서버 프록시 이름 해상도 요구 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a94e4de181cd8794d479bbd6695a94658aba0f86
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="name-resolution-requirements-for-federation-server-proxies"></a>Federation 서버 프록시 이름 해상도 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

인터넷에 연결 클라이언트 컴퓨터를 Active Directory Federation Services \(AD FS\)로 보호 된 응용 프로그램에 액세스 하려고 먼저 federation 서버 인증 해야 합니다. 대부분의 경우 federation 서버는 일반적으로 하지 직접은 인터넷에서 액세스할 수 있습니다. 따라서 인터넷 클라이언트 컴퓨터 해야 리디렉션됩니다 federation 서버 프록시 대신 합니다. 성공 리디렉션을 적절 한 Domain Name System \(DNS\) 레코드 DNS 영역이 나 인터넷 얼굴 영역에 추가 하 여 수행할 수 있습니다.  
  
Federation 서버 프록시 이동 인터넷 클라이언트를 사용 하는 방법을 주변 네트워크에는 DNS 영역을 구성 하는 방법 또는 인터넷의 제어할 수 있는 DNS 영역을 구성 하는 방법에 따라 달라 집니다. Federation 서버 프록시 주변 네트워크에 사용 하 여 위한 것입니다. 이러한 인터넷 클라이언트 서버 요청을 다시 federation 성공적으로 사용자를 제어 하는 모든 Internet\ 전면 영역에서 DNS 제대로 구성 된 경우에 합니다. 따라서 구성 Internet\ 전면 영역에-주변 네트워크만 제공 DNS 영역이 나 주변 네트워크 및 인터넷 클라이언트 역할 DNS 영역 보유 여부 등이 중요 합니다.  
  
이 항목에서는 주변 네트워크에 federation 서버 프록시 놓으면 이름 확인 구성할 수 있는 단계에 설명 합니다. 있는 단계에 따라를 확인 하려면 먼저 다음 DNS 시나리오 중 주변 네트워크 조직에 DNS 인프라에 가장 잘 맞는 확인 합니다. 그런 다음 해당 시나리오에 대 한 단계를 따르세요.  
  
## <a name="dns-zone-serving-only-the-perimeter-network"></a>주변 네트워크만 제공 DNS 영역  
이 시나리오 조직 또는 두 DNS 영역 주변 네트워크에 있고 조직 인터넷에서 모든 DNS 영역 제어 하지 않습니다. 성공 이름 확인 federation 서버 프록시 역할 주변 네트워크 시나리오 DNS 영역에 대해 다음과 같은 경우에 따라 다릅니다.  
  
-   Federation 서버 프록시 설정 있어야 호스트 정식된 도메인 해결 하기 위해 파일의 이름을 federation 서버 또는 federation 서버 클러스터의 IP 주소를 federation 서버 끝점 url \(FQDN\) 합니다.  
  
-   Federation 서버 끝점 URL FQDN federation 서버 프록시의 IP 주소를 확인 하 DNS 계정 파트너의 주변 네트워크에서를 설정 해야 합니다.  
  
다음 그림와 해당 단계 어떻게 각각의 이러한 조건 이루어집니다 지정 예 표시 됩니다. 이 그림 Microsoft 네트워크 부하 분산 \(NLB\) 기술은으로 기존 federation 서버 그룹에 대 한 단일, FQDN 클러스터 단일, 클러스터 IP 주소를 제공합니다.  
  
![이름 요구 사항](media/adfs2_deploy_single_fs.gif)  
  
클러스터 IP 주소 또는 클러스터 FQDN 구성에 대 한 자세한 내용은 참조 NLB을 사용 하 여 [클러스터 매개 지정](https://go.microsoft.com/fwlink/?LinkId=75282)합니다.  
  
### <a name="1-configure-the-hosts-file-on-the-federation-server-proxy"></a>1. 해당 federation 서버 프록시에 호스트 파일을 구성 합니다.  
계정 파트너 federation 서버 프록시 fs.fabrikam.com 실제 계정 federation 서버의 IP 주소를 확인 하는 로컬 호스트 파일에 항목을 갖고 주변 네트워크에는 DNS fs.fabrikam.com에 대 한 모든 요청 계정 federation 서버 프록시도 확인 하도록 구성 되어, \ (또는 federation 서버 farm\ 클러스터 DNS 이름을) 하는 회사 네트워크에 연결 되어 있습니다. 그러면 계정 federation 서버에 아니라 자신에 게 호스트 이름 fs.fabrikam.com 해결 하기 위해 계정 federation 서버 프록시 수-처럼 사용 하 여 주변 DNS fs.fabrikam.com 찾으려면 시도 하면 발생 하는 등 federation 서버 프록시 서버 federation와 통신할 수 있도록 합니다.  
  
### <a name="2-configure-perimeter-dns"></a>2. 주변 DNS을 구성 합니다.  
때문만 있는 단일 ADFS 호스트 이름을 클라이언트 컴퓨터 리디렉션되는-은 인터넷에서 인트라넷 켜거나-주변 DNS 서버를 사용 하는 인터넷에서 클라이언트 컴퓨터 FQDN 계정 federation 서버 \(fs.fabrikam.com\)에 대 한 주변 네트워크에서 계정 federation 서버 프록시의 IP 주소를 확인 해야 합니다. 계정 federation 서버 프록시 설정 된 클라이언트 fs.fabrikam.com 해결 하려고 할 때 발전 수, 되도록 주변 DNS 단일 호스트 \(A\) 리소스 기록 fs \(fs.fabrikam.com\) 및 계정 federation 서버 프록시 주변 네트워크에서의 IP 주소와 제한 된 corp.fabrikam.com DNS 영역 포함 되어 있습니다.  
  
Federation 서버 프록시 호스트 파일을 수정 하 고 경계 네트워크에서 DNS 구성 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 프록시 주변 네트워크만 사용 하는 DNS 영역에 대해 구성 이름 확인](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md)합니다.  
  
## <a name="dns-zone-serving-both-the-perimeter-network-and-internet-clients"></a>주변 네트워크 및 인터넷 클라이언트 역할 DNS 영역  
이 시나리오 조직 DNS 영역 주변 네트워크에서 및 인터넷에서 하나 이상의 DNS 영역을 제어합니다. 성공 이름 확인 federation 서버 프록시가이 시나리오에 대해 다음과 같은 경우에 따라 다릅니다.  
  
-   Federation 서버 호스트 이름 FQDN 주변 네트워크에 federation 서버 프록시의 IP 주소를 확인 하는 계정 파트너의 인터넷 영역에서 DNS는 설정 해야 합니다.  
  
-   Federation 서버 호스트 이름 FQDN federation 서버 회사 네트워크에서의 IP 주소를 확인 하 DNS 계정 파트너의 주변 네트워크에서를 설정 해야 합니다.  
  
다음 그림와 해당 단계 어떻게 각각의 이러한 조건 이루어집니다 지정 예 표시 됩니다.  
  
![이름 요구 사항](media/adfs2_deploy_fsp_3DNS.gif)  
  
### <a name="1-configure-perimeter-dns"></a>1. DNS 주변을 구성 합니다.  
이 시나리오에 대 한 인터넷 DNS 영역 구성한 가정 때문에 해당 사용자 컨트롤 해결 하기 위해 요청 특정 끝점 URL에 대 한 사항이 \ (즉, fs.fabrikam.com\) federation 서버 프록시 주변 네트워크에를 구성 해야 영역 이러한 회사 네트워크에서 federation 서버에이 요청을 전송 하도록 DNS 주변에 있습니다.  
  
Fs.fabrikam.com 해결 하기 위해 시도할 클라이언트를 계정 federation 서버를 전달할 수 있도록 주변 DNS fs \(fs.fabrikam.com\) 및 IP 주소 회사 네트워크에서 계정 federation 서버에 대 한 단일 호스트 \(A\) 리소스 기록으로 구성 됩니다. 그러면 계정 federation 서버에 아니라 자신에 게 호스트 이름 fs.fabrikam.com 해결 하기 위해 계정 federation 서버 프록시 수-처럼 사용 하 여 인터넷 DNS fs.fabrikam.com 찾으려면 시도 하면 발생 하는 등 federation 서버 프록시 서버 federation와 통신할 수 있도록 합니다.  
  
### <a name="2-configure-internet-dns"></a>2. 인터넷 DNS을 구성 합니다.  
이 시나리오 성공적으로 이름 확인을 위해 fs.fabrikam.com 인터넷에 연결 하는 클라이언트 컴퓨터에서 모든 요청 해결 해야 인터넷 DNS 영역 내에서 제어할 수 있습니다. 따라서 인터넷 DNS 영역이 fs.fabrikam.com 주변 네트워크에 계정이 federation 서버 프록시의 IP 주소를에 대 한 클라이언트 요청을 전송 하도록 구성 해야 합니다.  
  
주변 네트워크 및 인터넷 DNS 영역 수정 하는 방법에 대 한 자세한 내용은 참조 [Federation 서버 프록시 DNS 영역은 대용 모두 주변 네트워크 및 인터넷 클라이언트에 대해 구성 이름 확인](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
