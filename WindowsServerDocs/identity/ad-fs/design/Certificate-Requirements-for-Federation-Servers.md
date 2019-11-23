---
ms.assetid: 9831b421-8fb7-4e15-ac27-c013cbca6d05
title: 페더레이션 서버에 대한 인증서 요구 사항
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7eeff82ef3311f18c8252c44c96310fcf3c18217
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359177"
---
# <a name="certificate-requirements-for-federation-servers"></a>페더레이션 서버에 대한 인증서 요구 사항

Active Directory Federation Services \(AD FS\) 디자인에서 다양 한 인증서를 사용 하 여 통신을 보호 하 고 인터넷 클라이언트와 페더레이션 서버 간의 사용자 인증을 용이 하 게 해야 합니다. 각 페더레이션 서버는 서비스 통신 인증서 및 토큰 있어야\-AD FS 통신에 참여 하려면 먼저 인증서에 서명 합니다. 다음 표에서 페더레이션 서버와 연결 된 인증서 종류를 설명 합니다.  
  
|인증서 종류|설명|  
|--------------------|---------------|  
|토큰\-서명 인증서|토큰\-서명 인증서가는 X509 인증서입니다. 페더레이션 서버에 연결 된 공개 사용 하 여\/를 생성 하는 모든 보안 토큰을 디지털 서명 하는 개인 키 쌍입니다. 여기에는 게시된 페더레이션 메타데이터 및 아티팩트 확인 요청에 대한 서명이 포함됩니다.<br /><br />여러 토큰을 사용할 수 있습니다\-AD FS 관리 스냅인에서 인증서를 구성 서명\-에 하나의 인증서가 만료 될 때 인증서 롤오버에 대 한 허용 하도록 합니다. 기본적으로 목록에 있는 모든 인증서는 게시, 기본 토큰만 있지만\-서명 인증서가 사용 되는 AD FS에서 실제로 토큰을 서명 합니다. 선택한 모든 인증서에 해당 프라이빗 키가 있어야 합니다.<br /><br />자세한 내용은 [Token-Signing Certificates](Token-Signing-Certificates.md) 및 [Add a Token-Signing Certificate](../../ad-fs/deployment/Add-a-Token-Signing-Certificate.md)을 참조하세요.|  
|서비스 통신 인증서|페더레이션 서버에 Windows Communication foundation 서비스 통신이 라고도 서버 인증 인증서를 사용 하 여 \(WCF\) 메시지 보안입니다. 기본적으로이 Secure Sockets Layer로 사용 하는 페더레이션 서버는 동일한 인증서 \(SSL\) 인터넷 정보 서비스에서 인증서 \(IIS\)합니다. **참고:** AD FS 관리 스냅인\-서비스 통신 인증서로 페더레이션 서버에 대 한 서버 인증 인증서를 참조 합니다.<br /><br />자세한 내용은 참조 [서비스 통신 인증서](Service-Communications-Certificates.md) 및 [서비스 통신 인증서 설정](../../ad-fs/deployment/Set-a-Service-Communications-Certificate.md)합니다.<br /><br />클라이언트 컴퓨터에서 서비스 통신 인증서를 신뢰할 해야 하기 때문에 신뢰할 수 있는 인증 기관에서 서명한 인증서를 사용 하는 것이 좋습니다 \(CA\)합니다. 선택한 모든 인증서에 해당 프라이빗 키가 있어야 합니다.|  
|Secure Sockets Layer \(SSL\) 인증서|페더레이션 서버는 SSL 인증서를 사용하여 웹 클라이언트 및 페더레이션 서버 프록시와의 SSL 통신에 대한 웹 서비스 트래픽의 보안을 유지합니다.<br /><br />클라이언트 컴퓨터에서 SSL 인증서를 신뢰할 수 있어야 하므로 신뢰할 수 있는 CA에서 서명한 인증서를 사용하는 것이 좋습니다. 선택한 모든 인증서에 해당 프라이빗 키가 있어야 합니다.|  
|토큰\-암호 해독 인증서|이 인증서는이 페더레이션 서버에서 받은 토큰의 해독에 사용 됩니다.<br /><br />여러 암호 해독 인증서를 유지할 수 있습니다. 이렇게 하면 리소스 페더레이션 서버를 새 인증서를 기본 암호 해독 인증서로 설정 된 후 이전 인증서를 통해 발급 된 토큰을 해독할 수 있습니다. 암호 해독, 하지만 주 토큰에 대 한 모든 인증서를 사용할 수 있습니다\-페더레이션 메타 데이터에 실제로 게시는 인증서의 암호를 해독 합니다. 선택한 모든 인증서에 해당 프라이빗 키가 있어야 합니다.<br /><br />자세한 내용은 참조 [토큰 암호 해독 인증서 추가](../../ad-fs/deployment/Add-a-Token-Decrypting-Certificate.md)합니다.|  
  
요청 하 고 Microsoft Management Console을 통해 서비스 통신 인증서를 요청 하 여 SSL 인증서 또는 서비스 통신 인증서를 설치할 수 있습니다 \(MMC\) 스냅\-에서 IIS에 대 한 합니다. SSL 인증서를 사용 하는 방법에 대 한 자세한 내용은 iis [7.0: iis 7.0에서 SSL(Secure Sockets Layer) 구성](https://go.microsoft.com/fwlink/?LinkID=108544) [7.0: Iis 7.0에서 서버 인증서 구성](https://go.microsoft.com/fwlink/?LinkID=108545) 을 참조 하십시오.  
  
> [!NOTE]  
> AD FS에서 보안 해시 알고리즘을 변경할 수 있습니다 \(SHA\) 어느 SHA 디지털 서명에 사용 되는 수준\-1 또는 SHA\-256 \(보다 안전한\)합니다. AD FSdoes m d 5와 같은 다른 해시 메서드와 함께 인증서의 사용을 지원 하지 \(Makecert.exe 명령은 함께 사용 되는 기본 해시 알고리즘\-선 도구\)합니다. 최상의 보안을 s h A를 사용 하는 것이 좋습니다\-256 \(기본적으로 설정 된\) 모든 서명 합니다. SHA\-1은\-Microsoft 제품이 아닌 Microsoft 제품이 나 AD FS 1과 같이 SHA\-256를 사용 하는 통신을 지원 하지 않는 제품과 상호 운용 해야 하는 경우에만 사용 하는 것이 좋습니다. *x*.  
  
## <a name="determining-your-ca-strategy"></a>CA 전략 결정  
AD FS에서 발급 한 인증서는 CA가 필요 하지 않습니다. 그러나 SSL 인증서 \(서비스 통신 인증서로도 기본적으로 사용 되는 인증서\) AD FS 클라이언트에서 신뢰할 수 있어야 합니다. 사용 하는 자체는 것이 좋습니다\-이러한 인증서 종류에 대 한 인증서를 서명 합니다.  
  
> [!IMPORTANT]  
> 사용 하 여 자체의\-서명 됨, SSL 인증서를 프로덕션 환경에서 허용할 수 악의적인 사용자는 계정 파트너 조직의 리소스 파트너 조직의 페더레이션 서버를 제어할 수 있습니다. 이 보안 위험이 존재 하기 때문에 자체\-서명 된 인증서는 루트 인증서입니다. 다른 페더레이션 서버의 신뢰할 수 있는 루트 저장소에 추가 해야 \(리소스 페더레이션 서버 예를 들어\), 해당 서버를 공격에 취약 해질 수입니다.  
  
CA에서 인증서를 받은 후에는 모든 인증서를 로컬 컴퓨터의 개인 인증서 저장소로 가져와야 합니다. 인증서 MMC 스냅인을 사용 하 여 개인 저장소에 인증서를 가져올 수\-에 있습니다.  
  
인증서를 사용 하는 대신 스냅\-을 가져올 수도 있습니다 IIS 관리자 스냅인을 사용 하 여 SSL 인증서\-에서 SSL을 할당 하는 시간에 인증서를 기본 웹 사이트입니다. 자세한 내용은 참조 [기본 웹 사이트로 서버 인증 인증서 가져오기](../../ad-fs/deployment/Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)합니다.  
  
> [!NOTE]  
> 페더레이션 서버가 될 컴퓨터에 AD FS 소프트웨어를 설치 하기 전에 두 인증서 모두 로컬 컴퓨터 개인 인증서 저장소에 있으며, SSL 인증서가 기본 웹 사이트에 할당 되었는지 확인 합니다. 페더레이션 서버를 설정 하는 데 필요한 작업 순서에 대 한 자세한 내용은 참조 [검사 목록: 페더레이션 서버 설정을](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)합니다.  
  
보안 및 예산 요구 사항에 따라 공용 CA 또는 회사 CA에서 가져올 인증서를 신중하게 고려해야 합니다. 다음 그림에서는 지정된 인증서 종류에 대한 권장 CA 발급자를 보여 줍니다. 이 권장 사항을 반영 모범\-보안 및 비용에 대 한 방법을 연습 합니다.  
  
![인증서 요구 사항](media/adfs2_fedserver_certstory_1.png)  
  
## <a name="certificate-revocation-lists"></a>인증서 해지 목록  
사용하는 인증서에 CRL이 있는 경우, 구성된 인증서를 사용하는 서버에서 해당 CRL을 배포한 서버에 연결할 수 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목
[Windows Server 2012의 AD FS 디자인 가이드](AD-FS-Design-Guide-in-Windows-Server-2012.md)
