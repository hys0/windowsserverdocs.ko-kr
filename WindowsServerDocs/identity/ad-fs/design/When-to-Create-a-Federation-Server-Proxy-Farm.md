---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: 페더레이션 서버 프록시 팜을 만들어야 하는 경우
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c33475d7420383448439e2b769562e55127c7b0e
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190633"
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>페더레이션 서버 프록시 팜을 만들어야 하는 경우

대규모 Active Directory Federation Services를 해야 하는 경우 추가 페더레이션 서버 프록시를 설치 하는 것이 좋습니다 \(AD FS\) 내결함성을 제공, 로드를 배포 하려면\-분산 및 확장성 프록시 배포 합니다. 동일한 경계 네트워크에 두 개 이상의 페더레이션 서버 프록시를 만들기 및 구성 하는 각각 동일한 AD FS 페더레이션 서비스를 보호 하는 작업에는 페더레이션 서버 프록시 팜을 만듭니다.  
  
페더레이션 서버 프록시 팜을 만들거나 AD FS 페더레이션 서버 프록시 구성 마법사를 사용 하 여 기존 팜에 추가 페더레이션 서버 프록시를 설치할 수 있습니다. 자세한 내용은 [페더레이션 서버 프록시를 만들어야 하는 경우](When-to-Create-a-Federation-Server-Proxy.md)합니다.  
  
모든 페더레이션 서버 프록시 팜을 함께 작동할 수 있습니다, 전에 클러스터링 해야 해당 아래에 있는 하나의 IP 주소와 하나의 Domain Name System \(DNS\) 정규화 된 도메인 이름 \(FQDN\)합니다. Microsoft 네트워크 부하 분산 배포 하 여 서버를 클러스터링 할 수 있습니다 \(NLB\) 경계 네트워크 내에서. 다음 표의 작업에서는 NLB는 팜에 페더레이션 서버 프록시를 클러스터 하도록 적절 하 게 구성 해야 합니다.  
  
Microsoft NLB 기술을 사용 하 여 클러스터에 대 한 FQDN을 구성 하는 방법에 대 한 자세한 내용은 참조 하세요. [클러스터 매개 변수 지정](https://go.microsoft.com/fwlink/?linkid=74651)합니다.  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>팜에 대한 페더레이션 서버 프록시 구성  
다음 표에서 각 페더레이션 서버 프록시 팜에 참여할 수 있도록 완료 해야 하는 작업을 설명 합니다.  
  
|태스크|설명|  
|--------|---------------|  
|동일한 AD FS 페더레이션 서비스 이름으로 팜의 모든 프록시 지점|페더레이션 서버 프록시를 만들 때 팜에 참여 하는 모든 페더레이션 서버 프록시에 대 한 AD FS 페더레이션 서버 프록시 구성 마법사에서 동일한 페더레이션 서비스 이름을 입력 해야 합니다. 페더레이션 서버 프록시를 구성 하는 AD FS 페더레이션 서비스 인스턴스를 확인 하려면이 DNS 호스트 이름을 해당 연락처 URL을 사용 합니다.<br /><br />자세한 내용은 [컴퓨터 페더레이션 서버 프록시 역할에 대 한 구성](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)합니다.|  
|인증서 가져오기 및 공유|공용 인증 기관에서 서버 인증 인증서를 얻을 수 있습니다 \(CA\)-예를 들어, VeriSign-다음의 동일한 개인 키 부분을 공유 하는 모든 페더레이션 서버 프록시 수 있도록 인증서를 구성 합니다 각 페더레이션 서버 프록시에 대 한 기본 웹 사이트에서 동일한 인증서입니다. 인증서를 공유 하려면 각 페더레이션 서버 프록시에 대 한 기본 웹 사이트에 동일한 서버 인증 인증서를 설치 해야 있습니다. 자세한 내용은 참조 [기본 웹 사이트로 서버 인증 인증서 가져오기](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.<br /><br />자세한 내용은 [페더레이션 서버 프록시에 대 한 인증서 요구 사항](Certificate-Requirements-for-Federation-Server-Proxies.md)합니다.|  
  
페더레이션 서버 프록시 팜을 만들어야 하는 새 페더레이션 서버 프록시를 추가 하는 방법에 대 한 자세한 내용은 참조 하세요. [검사 목록: 페더레이션 서버 프록시 설정](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)합니다.  
  
## <a name="see-also"></a>관련 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
