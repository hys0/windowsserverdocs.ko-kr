---
ms.assetid: 74ef34c8-e13f-499b-b2bb-952ad7036622
title: "이름 Federation 서버에 대 한 확인 요구 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 74701cbaa403611b081942f016b21db1c0b3ff70
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="name-resolution-requirements-for-federation-servers"></a>이름 Federation 서버에 대 한 확인 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

회사 네트워크에서 컴퓨터를 응용 프로그램이 나 Active Directory Federation Services \(AD FS\)에 의해 보호 되는 웹 서비스에 액세스 하려고 하는 경우 먼저 federation 서버 인증 해야 합니다. 인증 하는 방법은 회사 네트워크 클라이언트 Windows 통합 인증 통해 로컬 federation 서버에 액세스 하도록 합니다.  
  
## <a name="configure-corporate-dns"></a>회사 DNS 구성  
Windows 통합 인증 통해 로컬 federation 서버에 성공 이름 확인 발생할 수 있도록 계정 파트너 회사 네트워크에서 Domain Name System \(DNS\) federation 서버 정식된 도메인 이름 \(FQDN\) 호스트 이름 해당 federation 서버 클러스터의 IP 주소를 해결 하는 새로운 호스트 \(A\) 리소스 기록에 대 한 구성 합니다.  
  
다음 그림에서는 특정된 시나리오에 대해이 작업은 수행 하는 방법을 확인할 수 있습니다. 이 경우 Microsoft 네트워크 부하 분산 \(NLB\)로 기존 federation 서버 그룹에 대 한 단일 클러스터 FQDN 이름과 단일 클러스터 IP 주소를 제공합니다.  
  
![이름 요구 사항](media/adfs2_deploy_single_fs.gif)  
  
클러스터 IP 주소를 구성 하거나 클러스터 FQDN NLB 사용 하는 방법에 대 한 정보를 참조 하세요. [클러스터 매개 지정](https://go.microsoft.com/fwlink/?LinkId=75282)합니다.  
  
회사 DNS federation 서버에 대 한 구성 하는 방법에 대 한 정보를 참조 하세요. [호스트 & #40; 추가 & #41; 회사 DNS Federation 서버에 대 한 리소스 기록](../../ad-fs/deployment/Add-a-Host--A--Resource-Record-to-Corporate-DNS-for-a-Federation-Server.md)합니다.  
  
주변 네트워크에 federation 서버 프록시 구성 하는 방법에 대 한 정보를 참조 하세요. [이름 해상도 요구 사항을 Federation 서버 프록시](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)합니다.  
  

## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
