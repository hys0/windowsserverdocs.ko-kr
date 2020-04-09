---
ms.assetid: ad0bf21d-2ace-4565-b1f5-ce57c8eb2689
title: 페더레이션 서버 프록시 팜을 만들어야 하는 경우
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d4b2b889159dee9f3b93a54a2b1924be286792f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858496"
---
# <a name="when-to-create-a-federation-server-proxy-farm"></a>페더레이션 서버 프록시 팜을 만들어야 하는 경우

Active Directory Federation Services \(AD FS\) 배포가 많은 경우 추가 페더레이션 서버 프록시를 설치 하는 것이 좋습니다. 프록시 배포에 대 한 내결함성,\-부하 분산 및 확장성을 제공 하고자 할 수 있습니다. 동일한 경계 네트워크에 둘 이상의 페더레이션 서버 프록시를 만들고 각 프록시를 구성 하 여 동일한 AD FS 페더레이션 서비스 보호 하는 작업은 페더레이션 서버 프록시 팜을 만듭니다.  
  
AD FS 페더레이션 서버 프록시 구성 마법사를 사용 하 여 페더레이션 서버 프록시 팜을 만들거나 기존 팜에 추가 페더레이션 서버 프록시를 설치할 수 있습니다. 자세한 내용은 [When to Create a Federation Server Proxy](When-to-Create-a-Federation-Server-Proxy.md)를 참조하세요.  
  
모든 페더레이션 서버 프록시가 팜으로 함께 작동 하려면 먼저 하나의 IP 주소와 하나의 도메인 이름 시스템 \(DNS\) 정규화 된 도메인 이름 \(FQDN\)로 클러스터링 해야 합니다. 경계 네트워크 내에서 NLB\) \(Microsoft 네트워크 부하 분산을 배포 하 여 서버를 클러스터링 할 수 있습니다. 다음 표의 작업을 수행 하려면 팜에서 페더레이션 서버 프록시를 클러스터링 하도록 NLB를 적절 하 게 구성 해야 합니다.  
  
Microsoft NLB 기술을 사용 하 여 클러스터에 대 한 FQDN을 구성 하는 방법에 대 한 자세한 내용은 [클러스터 매개 변수 지정](https://go.microsoft.com/fwlink/?linkid=74651)을 참조 하세요.  
  
## <a name="configuring-federation-server-proxies-for-a-farm"></a>팜에 대한 페더레이션 서버 프록시 구성  
다음 표에서는 각 페더레이션 서버 프록시가 팜에 참여할 수 있도록 하기 위해 완료 해야 하는 작업에 대해 설명 합니다.  
  
|작업|설명|  
|--------|---------------|  
|팜의 모든 프록시가 동일한 AD FS 페더레이션 서비스 이름으로 가리키기|페더레이션 서버 프록시를 만들 때 팜에 참여 하는 모든 페더레이션 서버 프록시에 대 한 AD FS 페더레이션 서버 프록시 구성 마법사에 동일한 페더레이션 서비스 이름을 입력 해야 합니다. 페더레이션 서버 프록시는이 DNS 호스트 이름을 구성 하는 URL을 사용 하 여 AD FS 페더레이션 서비스 인스턴스를 확인 합니다.<p>자세한 내용은 [Configure a Computer for the Federation Server Proxy Role](../../ad-fs/deployment/Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)를 참조하세요.|  
|인증서 가져오기 및 공유|공용 인증 기관 \(CA\)에서 서버 인증 인증서를 가져온 다음 (예: VeriSign), 모든 페더레이션 서버 프록시가 각 페더레이션 서버 프록시에 대 한 기본 웹 사이트에 있는 동일한 인증서의 동일한 개인 키 부분을 공유 하도록 인증서를 구성할 수 있습니다. 인증서를 공유 하려면 각 페더레이션 서버 프록시에 대 한 기본 웹 사이트에 동일한 서버 인증 인증서를 설치 해야 합니다. 자세한 내용은 참조 [기본 웹 사이트로 서버 인증 인증서 가져오기](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.<p>자세한 내용은 [Certificate Requirements for Federation Server Proxies](Certificate-Requirements-for-Federation-Server-Proxies.md)를 참조하세요.|  
  
새 페더레이션 서버 프록시를 추가 하 여 페더레이션 서버 프록시 팜을 만드는 방법에 대 한 자세한 내용은 [검사 목록: 페더레이션 서버 프록시 설정](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server-Proxy.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
