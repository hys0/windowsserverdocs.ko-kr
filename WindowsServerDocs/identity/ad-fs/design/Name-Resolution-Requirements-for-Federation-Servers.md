---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: 페더레이션 서버에 대한 이름 확인 요구 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 88ec418bd72a6389856deb1abd85641d8782bc30
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408042"
---
# <a name="name-resolution-requirements-for-federation-servers"></a>페더레이션 서버에 대한 이름 확인 요구 사항

회사 네트워크의 클라이언트 컴퓨터가\)AD FS \(Active Directory Federation Services으로 보호 되는 응용 프로그램 또는 웹 서비스에 액세스 하려고 할 때 먼저 페더레이션 서버에 인증 해야 합니다. Windows 통합 인증을 통해 로컬 페더레이션 서버에 액세스 하는 회사 네트워크 클라이언트를 인증 하는 한 가지 방법은 이며  
  
## <a name="configure-corporate-dns"></a>회사 DNS 구성  
이름 확인이 성공한 Windows 통합 인증을 통해 로컬 페더레이션 서버에서 발생할 수 Domain Name System 있도록 \(DNS\) 계정의 회사 네트워크 파트너는 새 호스트에 구성 해야 합니다 \(A\) 정규화 된 도메인 이름 확인 되는 리소스 레코드 \(FQDN\) 의 페더레이션 서버 클러스터의 IP 주소는 페더레이션 서버 호스트 이름입니다.  
  
다음 그림에서 주어진 시나리오에 대해 이 작업을 수행하는 방법을 확인할 수 있습니다. 이 시나리오에서는 Microsoft 네트워크 부하 분산 \(NLB\) 기존 페더레이션 서버 팜에 대 한 단일 클러스터 FQDN 이름 및 단일 클러스터 IP 주소를 제공 합니다.  
  
![이름 요구 사항](media/adfs2_deploy_single_fs.gif)  
  
NLB를 사용 하 여 FQDN 클러스터 또는 클러스터 IP 주소를 구성 하는 방법에 대 한 정보를 참조 하십시오. [클러스터 매개 변수 지정](https://go.microsoft.com/fwlink/?LinkId=75282)합니다.  
  
페더레이션 서버에 대해 회사 DNS를 구성 하는 방법에 대 한 정보를 참조 하십시오. [호스트 & #40;를 추가 합니다. & #41; 페더레이션 서버에 대해 회사 DNS에 리소스 레코드](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)합니다.  
  
경계 네트워크의 페더레이션 서버 프록시를 구성 하는 방법에 대 한 정보를 참조 하십시오. [페더레이션 서버 프록시에 대 한 이름 확인 요구 사항](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  

## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
