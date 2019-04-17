---
ms.assetid: 9831b421-8fb7-4e15-ac27-c013cbca6d05
title: "Federation 서버의 인증서 요구 사항"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 369c0e9e7ab1ef25baee1c35379cc66b886f20d8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="certificate-requirements-for-federation-servers"></a>Federation 서버의 인증서 요구 사항

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

된 Active Directory Federation Services \(AD FS\) 디자인에 다양 한 인증서를 인터넷 클라이언트 및 서버 federation 간에 사용자 인증 시키고 커뮤니케이션 보호를 사용 해야 합니다. 각 federation 서버 ADFS 통신에 참여할 수 있는 전에 서비스 통신 인증서 및 token\ 서명 인증서 있어야 합니다. 다음 표에서 federation 서버와 관련 된 인증서 종류에 설명 합니다.  
  
|인증서 종류|설명|  
|--------------------|---------------|  
|Token\ 서명 인증서|Token\ 서명 인증서가 X509는 인증서 합니다. Federation 서버 관련된 public\/개인 주요 쌍을 사용 하 여 디지털 생성 하는 모든 보안 토큰 서명. 게시 된 federation 메타 데이터와 아티팩트 해상도 요청 로그인 포함 됩니다.<br /><br />여러 token\ 서명 인증서 한 인증서가 만료 가까운 때 인증서 롤오버 될 수 있도록 snap\에서 광고 FS 관리에서 구성 되어 있을 수 있습니다. 기본적으로 목록에 있는 모든 인증서를 게시 있지만 기본 token\ 서명 인증서만은 ADFS 실제로 토큰 서명 하는 데 사용 됩니다. 선택한 모든 인증서 개인 해당 키가 있어야 합니다.<br /><br />자세한 내용은 참조 [토큰 서명 인증서](Token-Signing-Certificates.md) 및 [토큰 서명 인증서를 추가할](../../ad-fs/deployment/Add-a-Token-Signing-Certificate.md)합니다.|  
|서비스 통신 인증서|Federation 서버 라고도 서비스 통신에 대 한 Windows Communication Foundation \(WCF\) 메시지 보안 서버 인증 인증서를 사용 합니다. 기본적으로 federation 서버 주소 \(SSL\) 인증서 인터넷 정보 서비스 \(IIS\)에으로 사용 하 여 동일한 인증서입니다. **참고:** 서비스 통신 인증서도 federation 서버에 대 한 서버 인증 인증서의 snap\ AD FS 관리 가리킵니다.<br /><br />자세한 내용은 참조 [서비스 통신 인증서](Service-Communications-Certificates.md) 및 [서비스 통신 인증서 설정](../../ad-fs/deployment/Set-a-Service-Communications-Certificate.md)합니다.<br /><br />서비스 통신 인증서 클라이언트 컴퓨터 신뢰할 수 있어야을 하기 때문에 신뢰할 수 있는 인증 기관에 의해 서명 인증서를 사용 하는 것이 좋습니다 \(CA\) 합니다. 선택한 모든 인증서 개인 해당 키가 있어야 합니다.|  
|주소 \(SSL\) 인증서 보안|Federation 서버 SSL 인증서 웹 서비스 교통 웹 클라이언트 및 서버 프록시 federation SSL 통신에 대 한 보호를 위해 사용 합니다.<br /><br />클라이언트 컴퓨터 SSL 인증서 신뢰할 수 있어야를 신뢰할 수 있는 캘리포니아에 의해 서명 인증서를 사용 하는 것이 좋습니다. 선택한 모든 인증서 개인 해당 키가 있어야 합니다.|  
|해독 Token\ 인증서|이 인증서 토큰 해당 federation 서버에서 수신 하는 암호를 해독 하려면 사용 됩니다.<br /><br />여러 해독 인증서 있을 수 있습니다. 이렇게 하면 리소스 federation 서버 토큰 새 인증서가 기본 암호 해독 인증서도 설정 된 후 이전 인증서 사용 하 여 발급 한 암호를 해독할 수 있습니다. 모든 인증서 해독에 사용할 수 있지만 기본 token\ 해독 인증서만 실제로 federation 메타 데이터에 게시 됩니다. 선택한 모든 인증서 개인 해당 키가 있어야 합니다.<br /><br />자세한 내용은 참조 [토큰 암호를 해독 인증서 추가](../../ad-fs/deployment/Add-a-Token-Decrypting-Certificate.md)합니다.|  
  
요청 하 고 SSL 인증서 나 서비스 통신 인증서를 통해 Microsoft Management Console \(MMC\) snap\ 서비스 통신 인증서를 요청 하 여 설치-에서 iis 합니다. SSL 인증서 사용에 대 한 자세한 내용을 참조 [IIS 7.0: 구성 주소 IIS 7.0에서](https://go.microsoft.com/fwlink/?LinkID=108544) 및 [IIS 7.0: 서버 인증서 IIS 7.0 구성](https://go.microsoft.com/fwlink/?LinkID=108545) 합니다.  
  
> [!NOTE]  
> Adfs의 SHA\ 1 또는 SHA\ 256 \(more secure\)에 디지털 서명이에 사용 되는 Secure Hash Algorithm \(SHA\) 수준을 변경할 수 있습니다. 광고 FSdoes m d 5 같은 다른 해시 방법으로 인증서의 사용을 지원 하지 \ (기본 hash 알고리즘 Makecert.exe command\ 줄 tool\ 함께 사용 되는). 최적의 보안을 유지 SHA\ 256 사용 하는 것이 좋습니다 \ (default\로 설정 된)에 대 한 모든 서명이 합니다. 통신 SHA\ 256 non\ Microsoft 제품 또는 ADFS 1 등 사용 하 여 지원 하지 않는 제품 작용 해야 하는 경우에만 사용할 수 있도록 SHA\ 1 것이 좋습니다. *x*.  
  
## <a name="determining-your-ca-strategy"></a>캘리포니아 전략 결정  
Adfs는 인증서를 캘리포니아에서 발급 되어야 필요 하지 않습니다. 그러나 SSL 인증서 \ (도 서비스 통신 certificate\로 기본적으로 사용 되는 인증서) ADFS 클라이언트 신뢰할 수 있어야 합니다. 이러한 인증서 종류 self\ 서명 인증서를 사용 하지 않는 것이 좋습니다.  
  
> [!IMPORTANT]  
> Self\ 서명 사용, 생산 환경에서 SSL 인증서 리소스 파트너 조직에서 federation 서버 제어할 수 있는 계정 파트너 조직에서 악의적인 사용자를 허용할 수 있습니다. 이 보안 위험이 self\ 서명 인증서 루트 인증서가 때문에 문제가 발생 합니다. 다른 federation 서버의 루트 신뢰할 수 있는 저장소를 추가 해야 \ (예를 들어,는 리소스 federation server\), 서버를 공격에 취약 해질 수는 있습니다.  
  
인증서에 캐나다에서를 받은 후 로컬 컴퓨터의 개인 인증서 스토어에 모든 인증서를 가져오는 있는지 확인 합니다. 인증서에 snap\ 인증서 mmc 개인용 저장소를 가져올 수 있습니다.  
  
Snap\의 인증서를 사용 하는 대신 SSL 인증서를 기본 웹 사이트에 지정 된 시간에에서 snap\ IIS 관리자 인 ssl을 가져올 수 있습니다. 자세한 내용은 참조 [서버 인증 인증서를 기본 웹 사이트를 가져오는](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.  
  
> [!NOTE]  
> ADFS 소프트웨어 federation 서버가 컴퓨터에 설치 하기 전에 두 인증서 로컬 컴퓨터 개인 인증서 스토어에 있고 SSL 인증서 기본 웹 사이트에 할당 되어 있는지 있는지 확인 합니다. Federation 서버를 설정 하는 데 필요한 작업 주문에 대 한 자세한 내용은 참조 [검사: Federation 서버 설정을](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
보안 및 budget 요구 사항에 따라 신중 하 게는 인증서를 얻는 공용 하 여 캘리포니아 또는 회사 캘리포니아 고려 합니다. 다음 그림은 주어진된 인증서 종류에 대 한 권장된 캘리포니아 발급자 합니다. 이 권장 관련 된 보안 및 비용 best\ 연습 접근을 반영합니다.  
  
![인증서 요구 사항](media/adfs2_fedserver_certstory_1.png)  
  
## <a name="certificate-revocation-lists"></a>인증서 해지 목록  
사용 하는 인증서가 Crl 구성 된 인증서를 사용 하 여 서버 Crl 배포 하는 서버에 연결할 수 있어야 합니다.  
  
## <a name="see-also"></a>참조 하십시오
[Windows Server 2012의에서 지침에 따라 AD FS 디자인](AD-FS-Design-Guide-in-Windows-Server-2012.md)
