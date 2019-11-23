---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: 페더레이션 서버 프록시 역할에 대해 컴퓨터 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d47f7d3985aa779276f0712347eb9030857cefdb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359793"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>페더레이션 서버 프록시 역할에 대해 컴퓨터 구성

필요한 인증서를 사용 하 여 컴퓨터를 구성 하 고 페더레이션 서비스 프록시 역할 서비스를 설치한 후에는 컴퓨터가 페더레이션 서버 프록시로 구성 될 준비가 된 것입니다. 다음 절차를 사용하여 컴퓨터가 페더레이션 서버 프록시 역할을 하도록 설정할 수 있습니다.  
  
> [!IMPORTANT]  
> 이 절차를 사용 하 여 페더레이션 서버 프록시 컴퓨터를 구성 하기 전에 검사 목록: 나열 된 순서 대로 [페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md) 의 모든 단계를 수행 했는지 확인 합니다. 적어도 하나의 페더레이션 서버가 배포되고 페더레이션 서버 프록시 구성을 인증하는 데 필요한 모든 자격 증명이 구현되었는지 확인합니다. 또한 기본 웹 사이트에서 SSL\) 바인딩을 \(SSL(Secure Sockets Layer) 구성 해야 합니다. 그렇지 않으면이 마법사가 시작 되지 않습니다. 이러한 작업을 모두 완료해야 페더레이션 서버 프록시가 작동합니다.  
  
컴퓨터 설정을 마친 후에는 페더레이션 서버 프록시가 예상대로 작동하는지 확인합니다. 자세한 내용은 [페더레이션 서버 프록시 작동 확인](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)을 참조하세요.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>페더레이션 서버 프록시 역할에 대해 컴퓨터를 구성하려면  
  
1.  AD FS 페더레이션 서버 구성 마법사를 시작 하는 방법에는 두 가지가 있습니다. 마법사를 시작하려면 다음 중 하나를 수행합니다.  
  
    -   **시작** 화면에서**AD FS 페더레이션 서버 프록시 구성 마법사**를 입력 하 고 enter 키를 누릅니다.  
  
    -   설치 마법사가 완료 되 면 언제 든 지 Windows 탐색기를 열고 **C:\\windows\\ADFS** 폴더로 이동한 다음 **Fspconfigwizard**를 두 번 클릭\-합니다.  
  
2.  두 방법 중 하나를 사용하여 마법사를 시작하고 **시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **페더레이션 서비스 이름 지정** 페이지의 **페더레이션 서비스 이름**에 이 컴퓨터가 프록시 역할을 할 페더레이션 서비스를 나타내는 이름을 입력합니다.  
  
4.  특정 네트워크 요구 사항에 따라, HTTP 프록시 서버를 사용하여 페더레이션 서비스로 요청을 전달해야 하는지 여부를 결정합니다. HTTP 프록시 서버를 사용해야 하는 경우 **이 페더레이션 서비스로 요청을 보낼 때 HTTP 프록시 서버 사용** 확인란을 선택하고 **HTTP 프록시 서버 주소** 에 프록시 서버의 주소를 입력한 다음 **연결 테스트** 를 클릭하여 연결을 확인하고 **다음**을 클릭합니다.  
  
5.  메시지가 나타나면 이 페더레이션 서버 프록시와 페더레이션 서비스 간에 트러스트를 설정하는 데 필요한 자격 증명을 지정합니다.  
  
    기본적으로 페더레이션 서비스에서 사용 하는 서비스 계정 또는 로컬 BUILTIN\\Administrators 그룹의 구성원만 페더레이션 서버 프록시를 인증할 수 있습니다.  
  
6.  **설정 적용 준비 완료** 페이지에서 세부 정보를 검토합니다. 설정이 올바르게 표시되면 **다음**을 클릭하여 이러한 프록시 설정으로 이 컴퓨터 구성을 시작합니다.  
  
7.  **구성 결과** 페이지에서 결과를 검토합니다. 모든 구성 단계가 완료되면 **닫기**  를 클릭하여 마법사를 종료합니다.  
  
    에서 페더레이션 서버 proxys를 관리 하는 데 사용 하기 위해 \(MMC\) 스냅인\-스냅인이 없습니다. 조직의 각 페더레이션 서버 proxys에 대 한 설정을 구성 하려면 Windows PowerShell cmdlet을 사용 합니다.  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>프록시 작업을 위한 대체 TCP\/IP 포트 구성  
기본적으로 페더레이션 서버 프록시 서비스는 HTTPS 트래픽에 대해 TCP 포트 443을 사용 하 고 페더레이션 서버와 통신 하기 위해 HTTP 트래픽에 대해 포트 80을 사용 하도록 구성 됩니다. HTTPS용 TCP 포트 444과 HTTP용 포트 81과 같이 서로 다른 포트를 구성하려면 다음 작업을 완료해야 합니다.  
  
> [!NOTE]  
> 초기에 AD FS를 배포 하 여 대체 TCP\/IP 포트에서 작동 하려면 먼저 페더레이션 서버와 페더레이션 서버 프록시 컴퓨터 모두에서 HTTP 및 HTTPS에 대 한 IIS 프로토콜 바인딩의 포트를 수정 해야 합니다. 초기 구성을 위해 AD FS 구성 마법사를 실행 하기 전에 발생 해야 합니다. IIS\) \(인터넷 정보 서비스를 먼저 구성 하는 경우\-내에서 마법사 AD FS 기반 구성이 발생할 때 대체 TCP\/IP 포트 설정이 검색 되며 다음 절차가 필요 하지 않습니다. 나중에 포트 설정을 변경하려면 먼저 IIS 프로토콜 바인딩을 업데이트한 후 다음 절차를 사용하여 포트 설정을 적절하게 업데이트합니다. IIS 바인딩 편집에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 149605](https://go.microsoft.com/fwlink/?LinkId=190275) 를 참조 하십시오.  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>사용할 페더레이션 서버 프록시에 대 한 대체 TCP\/IP 포트를 구성 하려면  
  
1.  기본이 아닌 포트를 사용하도록 페더레이션 서버를 구성합니다.  
  
    이렇게 하려면 *Httpsport* 및 *Httpsport* 옵션을 **Set\-set-adfsproperties** cmdlet의 일부로 포함 하 여 기본이 아닌 포트 번호를 지정 합니다. 예를 들어 이러한 포트를 구성 하려면 페더레이션 서버 컴퓨터의 Windows PowerShell 세션에서 다음 명령을 사용 합니다.  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  기본이 아닌 포트를 사용 하도록 페더레이션 서버 프록시를 구성 합니다.  
  
    이렇게 하려면 *Httpsport* 및 *Httpsport* 옵션을 **Set\-ADFSProxyProperties** cmdlet의 일부로 포함 하 여 기본이 아닌 포트 번호를 지정 합니다. 예를 들어 이러한 포트를 구성 하려면 페더레이션 서버 컴퓨터의 Windows PowerShell 세션에서 다음 명령을 사용 합니다.  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > 끝점 Url은 페더레이션 서버 프록시 서비스에 대해 기본적으로 사용 하도록 설정 되어 있지 않습니다. 새 페더레이션 서버 설치를 구성 하는 경우 먼저 페더레이션 서버 프록시 서비스 끝점을 사용 하도록 설정 해야 합니다. 예를 들어이 절차의 예제에서 참조 하는 모든 끝점에 대해의 AD FS 관리\-스냅인에서 선택한 다음 **프록시에서 사용**을 선택 하 여 프록시에 사용 하도록 설정한 것으로 가정 합니다.  
  
3.  페더레이션 서버 프록시에서 IIS 설치를 업데이트 하면 Security Assertion Markup Language \(SAML\) 및 WS\-신뢰 끝점이 업데이트 된 포트 번호를 반영 하도록 구성 됩니다. 이렇게 하려면 메모장을 사용 하 여 web.config 파일에서 다음을 수정할 수 있습니다 .이 파일은 inetpub%\\\\adfs\\ls\\ 페더레이션 서버 프록시 컴퓨터에 있습니다. 예를 들어 sts1.contoso.com 라는 페더레이션 서버가 있고 새 포트 번호가 444 인 경우, 페더레이션 서버 프록시 컴퓨터의 메모장에서 web.config 파일을 찾아서 열고 다음 섹션을 찾아 다음 섹션에서 포트 번호를 수정 합니다. 아래에 강조 표시 된 다음 저장 하 고 메모장을 종료 합니다.  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  페더레이션 서버 프록시 서비스 사용자 계정을 관련 끝점 Url에 대 한 ACL\) \(액세스 제어 목록에 추가 합니다. 예를 들어 포트 번호가 1234이 고 AD FSfederation 서버 프록시 서비스를 실행 하는 데 사용 되는 사용자 계정이 네트워크 서비스 계정에서 빌드된\-경우 명령 프롬프트에 다음 명령을 입력 합니다.  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    이전 명령은 페더레이션 서버와 페더레이션 서버 프록시 컴퓨터 모두에서 실행 해야 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

