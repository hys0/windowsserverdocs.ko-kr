---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: "Federation 서버 프록시 역할 컴퓨터를 구성 합니다."
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2a89bab2fd1af1a1d7234da29f2025b4b12d6774
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>Federation 서버 프록시 역할 컴퓨터를 구성 합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

필요한 인증서도 컴퓨터를 구성 하 고 Federation 서비스 프록시 역할 서비스를 설치한 후 컴퓨터를 federation 프록시 서버를 구성 준비가 됩니다. 다음 절차는 컴퓨터에서 federation 서버 프록시 역할 작동할 수 있도록 사용할 수 있습니다.  
  
> [!IMPORTANT]  
> 이 절차를 사용 하 여 해당 federation 서버 프록시 컴퓨터 구성 전에의 모든 단계를 따른 있는지 확인 [검사: 설정을을 Federation 서버 프록시](Checklist--Setting-Up-a-Federation-Server-Proxy.md) 나열 된 순서 대로 합니다. 해당 federation 하나 이상의 서버 배포 되는 있는지 확인 하 고 승인 federation 서버 프록시 구성을 대 한 모든 필요한 자격 증명 하는 구현 확인 합니다. 기본 웹 사이트의 주소 \(SSL\) 바인딩을 구성 해야 하거나이 마법사가 시작 되지 않습니다. 이 federation 서버 프록시 작동할 수 전에 이러한 모든 작업을 완료 해야 합니다.  
  
컴퓨터를 설정을 마친 후 federation 서버 프록시 예상 대로 작동 하는지 확인 합니다. 자세한 내용은 참조 [되어 있는지 확인 한 Federation 서버 프록시가 작동](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)합니다.  
  
회원 **관리자**, 로컬 컴퓨터에서 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  해당 계정을 사용에 대 한 세부 정보를 검토 및 그룹 구성원에 [로컬와 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>Federation 서버 프록시 역할 컴퓨터 구성 하려면  
  
1.  두 가지 방법으로 AD FS Federation 서버 구성 마법사를 시작 합니다. 마법사를 시작 하려면 다음 중 하나를 수행 합니다.  
  
    -   에 **시작** 화면에서 입력**광고 FS Federation 서버 프록시 구성을 마법사**, ENTER 키를 누릅니다.  
  
    -   언제 든 지 설치 마법사를 완료 한 개방형 Windows 탐색기 되 면 탐색 하는 **C:\\Windows\\ADFS** 폴더 double\ 클릭 한 다음 **FspConfigWizard.exe**합니다.  
  
2.  마법사를 시작 방법 중 하나로 및에 **시작** 페이지, 클릭 **다음**합니다.  
  
3.  에 **Federation 서비스 이름 지정** 페이지의 **Federation 서비스 이름**,이 컴퓨터는 프록시 역할 역할 Federation 서비스를 나타내는 이름을 입력 합니다.  
  
4.  특정 네트워크 요구 사항에 따라, Federation 서비스를 요청을 전송 하도록 HTTP 프록시 서버를 사용 해야 하는지 여부를 확인 합니다. 그렇다면 선택는 **HTTP 프록시 서버가 Federation 서비스를 요청을 보낼 때 사용 하 여** 확인란을 아래에서 **HTTP 프록시 서버 주소** 프록시 서버 주소를 입력 합니다 **플레이어 연결 테스트로** 연결을 확인을 클릭 한 다음 **다음**합니다.  
  
5.  메시지가 표시 되 면이 federation 서버 프록시와 Federation 서비스 간의 신뢰 하는 데 필요한 자격 증명을 지정 합니다.  
  
    기본적으로 로컬 BUILTIN\\Administrators 그룹의 회원 하거나 Federation 서비스에서 사용 되는 서비스 계정만 federation 서버 프록시 권한을 부여할 수 있습니다.  
  
6.  에 **설정 적용 준비가** 페이지에서 세부 정보를 확인 합니다. 설정을 올바르게 표시를 클릭 **다음** 이러한 프록시 설정 사용이 컴퓨터 구성 시작 합니다.  
  
7.  에 **구성 결과** 페이지에서 검색 결과 검토 합니다. 모든 구성 단계가 완료 되 면 클릭 **닫기** 마법사를 종료 합니다.  
  
    Microsoft Management Console \(MMC\) snap\ 없이-에 federation 서버 proxys 관리 하기 위해 사용 합니다. 구성 하려면 각 federation 서버 proxys 설정을 조직에서 Windows PowerShell cmdlet을 사용 합니다.  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>암호 확인용 TCP\/IP 포트 프록시 작업에 대 한 구성  
기본적으로 federation 서버 프록시 서비스 HTTPS 교통 및 HTTP 소통 federation 서버와 통신에 대 한 포트 80 443 TCP 포트를 사용 하도록 구성 됩니다. HTTP에 대 한 포트 81 TCP 포트 https 444 등의 다른 포트를 구성 하는 다음과 같은 작업을 완료 합니다.  
  
> [!NOTE]  
> 암호 확인용 TCP\/IP 포트에서 작동 하도록 ADFS 배포 처음 하려는 경우 federation 서버와 federation 서버 프록시 컴퓨터 HTTP 및 HTTPS IIS 프로토콜 바인딩에서 포트 먼저 수정 해야 합니다. 초기 구성에 대 한 ADFS 구성 마법사 실행 하기 전에 나타나야 합니다. 먼저 인터넷 정보 서비스 \(IIS\) 구성, wizard\ 기반 구성 ADFS, 내에서 발생 하 고 다음 절차에 필요 없는 대체 TCP\/IP 포트 설정은 발견 됩니다. 업데이트 IIS 프로토콜 바인딩 포트 설정을 나중에 변경 하려는 경우 먼저 사용 하 여 다음 절차 포트 설정 업데이트를 적절 하 게 합니다. 편집 IIS 바인딩이 대 한 자세한 내용은 참조 [149605 문서](https://go.microsoft.com/fwlink/?LinkId=190275) Microsoft 기술 자료 합니다.  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>암호 확인용 TCP\/IP 포트를 사용 하 여 federation 서버 프록시 구성 하  
  
1.  기본 포트를 사용 하도록 federation 서버를 구성 합니다.  
  
    이 위해 사용 하 여를 포함 하 여 기본 포트 번호를 지정는 *HttpsPort* 및 *HttpPort* 의 일환으로 옵션은 **Set\ ADFSProperties** cmdlet 합니다. 예를 들어,이 포트를 구성 해당 federation 서버 컴퓨터에서 Windows PowerShell 세션에서 다음 명령을 사용:  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  Federation 서버 프록시 아닌 포트를 사용 하도록 구성 합니다.  
  
    이 위해 사용 하 여를 포함 하 여 기본 포트 번호를 지정는 *HttpsPort* 및 *HttpPort* 의 일환으로 옵션은 **Set\ ADFSProxyProperties** cmdlet 합니다. 예를 들어,이 포트를 구성 해당 federation 서버 컴퓨터에서 Windows PowerShell 세션에서 다음 명령을 사용:  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > Endpoint Url federation 서버 프록시 서비스는 기본적으로 활성화 되지 않습니다. 새 federation 서버 설치를 구성 하는 경우 먼저 federation 서버 프록시 서비스 끝점 설정 해야 합니다. 예를 들어, 것으로 간주이 절차의 예제를 참조 하 여 모든 끝점을 설정 했는지을 프록시 snap\에서 광고 FS 관리를 선택 하 고 다음 선택 하 여 **프록시 설정**합니다.  
  
3.  보안 설정 Markup Language \(SAML\) 및 WS\ 신뢰 끝점 업데이트 포트 번호를 반영 하도록 구성 된 federation 서버 프록시에 IIS 다시 설치를 업데이트 합니다. 이 위해 토큰과 systemdrive%\\inetpub\\adfs\\ls\\ federation 서버 프록시 컴퓨터에 있는에서 다음을 수정 하려면 메모장을 사용할 수 있습니다. 예를 들어, 가정 하 라는 sts1.contoso.com federation 서버 있으며 새 포트 번호는 444 하 고 해당 federation 서버 프록시 컴퓨터에서 메모장에는 토큰과 열고, 다음 섹션을 찾습니다, 아래 강조 표시 된으로 포트 번호를 수정 하 고 다음 저장 하 고 종료 메모장 찾습니다.  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  추가 federation 프록시 서버 서비스 사용자 계정 액세스 제어 \(ACL\) 관련된 endpoint Url에 대 한 나열 합니다. 예를 들어 포트 번호 1234 이며에서 광고 FSfederation 서버 프록시 서비스를 실행 하는 데 사용 된 사용자 계정에서 built\ 네트워크 서비스 계정, 경우 명령 프롬프트에서 다음 명령을 입력 합니다.  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    이전 명령 federation 서버와 federation 서버 프록시 컴퓨터에서 실행 해야 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: Federation 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

