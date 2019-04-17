---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: "Federation 서버 프록시 농장 만들어야 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8935760cad272d5b82edb675cda85caf0456565f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>Federation 서버 프록시 농장 만들어야 하는 경우

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

추가 federation 서버 프록시 큰 Active Directory Federation Services \(AD FS\) 배포 결함 허용, load\ 분산 및 확장성 프록시 배포를 위해 제공 하려는 경우 설치 하는 것이 좋습니다. 두 개 이상의 federation 프록시 서버 동일한 주변 네트워크 만들고 구성 동일한 ADFS Federation 서비스를 보호 하 고 각 act federation 서버 프록시 농장을 만듭니다.  
  
Federation 서버 프록시 팜 만들거나 AD FS Federation 서버 프록시 구성을 마법사를 사용 하 여 추가 federation 서버 프록시 기존 농장을 설치할 수 있습니다. 자세한 내용은 참조 [Federation 프록시 서버를 만들 때](When-to-Create-a-Federation-Server-Proxy.md)합니다.  
  
모든 federation 서버 프록시 역할을 할 수 함께 농장, 하기 전에 해야 먼저 클러스터링 하 하나의 미만 IP 주소와 한 Domain Name System \(DNS\) 정식된 도메인 \(FQDN\) 이름을 지정 합니다. 주변 네트워크 Microsoft 네트워크 부하 분산 \(NLB\) 배포 하 여 서버 클러스터 수 있습니다. 다음 표에 작업 그룹에 federation 서버 프록시 클러스터로 적절 하 게 구성 NLB 필요 합니다.  
  
Microsoft NLB 기술을 사용 하 여 클러스터 FQDN 구성 하는 방법에 대 한 자세한 내용은 참조 [클러스터 매개 지정](https://go.microsoft.com/fwlink/?linkid=74651)합니다.  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>Federation 서버 프록시 농장에 대 한 구성  
다음 표에서 각 federation 서버 프록시 농장에 참여할 수 있도록 완료 해야 하는 작업에 설명 합니다.  
  
|작업|설명|  
|--------|---------------|  
|가리킨 그룹에 있는 모든 프록시 ADFS Federation 서비스 이름이 같은|연합 프록시 서버를 만들 때는 팜에 참여 하는 모든 federation 서버 프록시에 대 한 AD FS Federation 서버 프록시 구성을 마법사에서 동일한 Federation 서비스 이름을 입력 해야 합니다. Federation 서버 프록시 URL 구성 하는이 DNS 호스트 이름 ADFS Federation 서비스 인스턴스를 확인 하 고 연락처를 사용 합니다.<br /><br />자세한 내용은 참조 [Federation 서버 프록시 역할 컴퓨터 구성](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)합니다.|  
|얻고 인증서를 공유|공용 인증 기관에서 서버 인증 인증서를 얻을 수 있습니다 \ (CA\)-등 VeriSign-후 모든 federation 서버 프록시 각 federation 서버 프록시에 대 한 기본 웹 사이트에 대해 동일한 인증서의 같은 개인 주요 부분을 공유 하는 인증서를 구성 합니다. 인증서를 공유 하려면 설치 해야 동일한 서버 인증 인증서 기본 웹 사이트에서 각 federation 서버 프록시. 자세한 내용은 참조 [서버 인증 인증서를 기본 웹 사이트를 가져오는](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.<br /><br />자세한 내용은 참조 [인증서 요구 사항에 대 한 Federation 서버 프록시](Certificate-Requirements-for-Federation-Server-Proxies.md)합니다.|  
  
새 federation 서버 프록시 서버 프록시 federation 팜 만들기를 추가 대 한 자세한 내용은 참조 [검사: 설정을을 Federation 서버 프록시](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
