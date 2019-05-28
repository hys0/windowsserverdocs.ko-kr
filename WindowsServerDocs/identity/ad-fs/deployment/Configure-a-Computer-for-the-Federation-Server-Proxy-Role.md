---
ms.assetid: a2f23877-30a7-439f-817d-387da9e00e86
title: 페더레이션 서버 프록시 역할에 대해 컴퓨터 구성
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b01e2ae567155cd3d53d6d7972bfd0b9ec0cf51b
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192283"
---
# <a name="configure-a-computer-for-the-federation-server-proxy-role"></a>페더레이션 서버 프록시 역할에 대해 컴퓨터 구성

필요한 인증서를 사용 하 여 컴퓨터를 구성 하 고 페더레이션 서비스 프록시 역할 서비스를 설치한 후 페더레이션 서버 프록시 컴퓨터를 구성할 준비가 되었습니다. 다음 절차를 사용하여 컴퓨터가 페더레이션 서버 프록시 역할을 하도록 설정할 수 있습니다.  
  
> [!IMPORTANT]  
> 페더레이션 서버 프록시 컴퓨터를 구성 하려면이 절차를 사용 하기 전에의 모든 단계를 따랐는지 확인 [검사 목록: 설정을 페더레이션 서버 프록시](Checklist--Setting-Up-a-Federation-Server-Proxy.md) 는 나열 된 순서에서입니다. 적어도 하나의 페더레이션 서버가 배포되고 페더레이션 서버 프록시 구성을 인증하는 데 필요한 모든 자격 증명이 구현되었는지 확인합니다. 또한 Secure Sockets Layer 구성 해야 \(SSL\) 바인딩을 기본 웹 사이트에서이 마법사가 시작 되지 않습니다. 이러한 작업을 모두 완료해야 페더레이션 서버 프록시가 작동합니다.  
  
컴퓨터 설정을 마친 후에는 페더레이션 서버 프록시가 예상대로 작동하는지 확인합니다. 자세한 내용은 [페더레이션 서버 프록시 작동 확인](Verify-That-a-Federation-Server-Proxy-Is-Operational.md)을 참조하세요.  
  
로컬 컴퓨터에서 이 절차를 완료하기 위해서는 최소한 **관리자** 또는 이와 동등한 자격이 있어야 합니다.  적절 한 계정을 사용 하는 방법에 대 한 세부 정보를 검토 하 고 그룹 구성원 자격 [로컬 및 도메인 기본 그룹](https://go.microsoft.com/fwlink/?LinkId=83477)합니다.   
  
### <a name="to-configure-a-computer-for-the-federation-server-proxy-role"></a>페더레이션 서버 프록시 역할에 대해 컴퓨터를 구성하려면  
  
1.  AD FS 페더레이션 서버 구성 마법사를 시작 하는 방법은 두 가지가 있습니다. 마법사를 시작하려면 다음 중 하나를 수행합니다.  
  
    -   에 **시작** 화면에서 입력**AD FS 페더레이션 서버 프록시 구성 마법사**, 한 다음 ENTER를 누릅니다.  
  
    -   언제 든 지 설치 마법사를 완료 Windows 탐색기 열기 되 면 이동 합니다 **c:\\Windows\\ADFS** 폴더를 연 다음 double\-클릭 **FspConfigWizard.exe**.  
  
2.  두 방법 중 하나를 사용하여 마법사를 시작하고 **시작** 페이지에서 **다음**을 클릭합니다.  
  
3.  **페더레이션 서비스 이름 지정** 페이지의 **페더레이션 서비스 이름**에 이 컴퓨터가 프록시 역할을 할 페더레이션 서비스를 나타내는 이름을 입력합니다.  
  
4.  특정 네트워크 요구 사항에 따라, HTTP 프록시 서버를 사용하여 페더레이션 서비스로 요청을 전달해야 하는지 여부를 결정합니다. HTTP 프록시 서버를 사용해야 하는 경우 **이 페더레이션 서비스로 요청을 보낼 때 HTTP 프록시 서버 사용** 확인란을 선택하고 **HTTP 프록시 서버 주소** 에 프록시 서버의 주소를 입력한 다음 **연결 테스트** 를 클릭하여 연결을 확인하고 **다음**을 클릭합니다.  
  
5.  메시지가 나타나면 이 페더레이션 서버 프록시와 페더레이션 서비스 간에 트러스트를 설정하는 데 필요한 자격 증명을 지정합니다.  
  
    기본적으로 로컬 기본의 멤버 또는 페더레이션 서비스에서 사용 하는 서비스 계정만\\Administrators 그룹에는 페더레이션 서버 프록시 권한을 부여할 수 있습니다.  
  
6.  **설정 적용 준비 완료** 페이지에서 세부 정보를 검토합니다. 설정이 올바르게 표시되면 **다음**을 클릭하여 이러한 프록시 설정으로 이 컴퓨터 구성을 시작합니다.  
  
7.  **구성 결과** 페이지에서 결과를 검토합니다. 모든 구성 단계가 완료되면 **닫기**  를 클릭하여 마법사를 종료합니다.  
  
    Microsoft 관리 콘솔이 \(MMC\) 맞춤\-하려면 페더레이션 서버 proxys를 관리 하는 데 사용 합니다. 조직의 각 페더레이션 서버 proxys에 대 한 설정을 구성 하려면 Windows PowerShell cmdlet을 사용 합니다.  
  
## <a name="configuring-an-alternate-tcpip-port-for-proxy-operations"></a>구성 된 대체 TCP\/프록시 작업에 대 한 IP 포트  
기본적으로 HTTPS 트래픽 및 페더레이션 서버와의 통신에 HTTP 트래픽에 대해 포트 80에 TCP 포트 443을 사용 하는 페더레이션 서버 프록시 서비스가 구성 됩니다. HTTPS용 TCP 포트 444과 HTTP용 포트 81과 같이 서로 다른 포트를 구성하려면 다음 작업을 완료해야 합니다.  
  
> [!NOTE]  
> 처음에 대체 TCP에서 작동 하도록 AD FS를 배포 하려는 경우\/IP 포트를 페더레이션 서버와 페더레이션 서버 프록시 컴퓨터 모두에서 HTTP 및 HTTPS에 대 한 IIS 프로토콜 바인딩의 포트를 먼저 수정 해야 합니다. 초기 구성과 AD FS 구성 마법사를 실행 하기 전에 발생 해야 합니다. 인터넷 정보 서비스를 구성 하는 경우 \(IIS\) 대체 TCP에 첫 번째\/마법사 때 IP 포트 설정이 검색 되므로\-기반된 구성 내 AD FS에서 발생 하 고 다음 프로시저가 아닙니다 필요 합니다. 나중에 포트 설정을 변경하려면 먼저 IIS 프로토콜 바인딩을 업데이트한 후 다음 절차를 사용하여 포트 설정을 적절하게 업데이트합니다. IIS 바인딩 편집에 대 한 자세한 내용은 참조 하세요. [문서 149605](https://go.microsoft.com/fwlink/?LinkId=190275) Microsoft 기술 자료에서 합니다.  
  
#### <a name="to-configure-alternate-tcpip-ports-for-the-federation-server-proxy-to-use"></a>대체 TCP를 구성 하려면\/IP 포트를 사용 하 여 페더레이션 서버 프록시에 대 한  
  
1.  기본이 아닌 포트를 사용하도록 페더레이션 서버를 구성합니다.  
  
    이 작업을 수행 하려면 포함 하 여 기본이 아닌 포트 번호를 지정 합니다 *HttpsPort* 및 *HttpPort* 옵션의 일부로 합니다 **설정\-에서** cmdlet. 예를 들어 이러한 포트를 구성 하려면 페더레이션 서버 컴퓨터의 Windows PowerShell 세션에서 다음 명령을 사용 합니다.  
  
    ```  
    Set-ADFSProperties -HttpsPort 444  
    Set-ADFSProperties -HttpPort 81  
    ```  
  
2.  기본이 아닌 포트를 사용 하도록 페더레이션 서버 프록시를 구성 합니다.  
  
    이 작업을 수행 하려면 포함 하 여 기본이 아닌 포트 번호를 지정 합니다 *HttpsPort* 하 고 *HttpPort* 옵션의 일부로 **설정\-ADFSProxyProperties** cmdlet입니다. 예를 들어 이러한 포트를 구성 하려면 페더레이션 서버 컴퓨터의 Windows PowerShell 세션에서 다음 명령을 사용 합니다.  
  
    ```  
    Set-ADFSProxyProperties -HttpsPort 444  
    Set-ADFSProxyProperties -HttpPort 81  
    ```  
  
    > [!NOTE]  
    > 끝점 Url은 페더레이션 서버 프록시 서비스는 기본적으로 사용할 수 없습니다. 새 페더레이션 서버 설치를 구성 하는 경우 페더레이션 서버 프록시 서비스 끝점을 먼저 설정 해야 합니다. 이 절차의 예제에서에서 참조 하는 모든 끝점에 대해 설정한 해당 프록시에 대 한 AD FS 관리 스냅인에서 선택 하 여 가정 예를 들어\-에서 다음을 선택 하 고 **프록시에서 사용**합니다.  
  
3.  따라서 페더레이션 서버 프록시에 IIS 설치를 업데이트 해당 Security Assertion Markup Language \(SAML\) ws\-끝점 업데이트 된 포트 번호를 반영 하도록 구성 된 신뢰 합니다. 이렇게 하려면 systemdrive %에 있는 Web.config 파일에서 다음을 수정 하려면 메모장을 사용할 수 있습니다\\inetpub\\adfs\\ls\\ 페더레이션 서버 프록시 컴퓨터. 예를 들어, 이름이 sts1.contoso.com 페더레이션 서버가 있고 새 포트 번호가 444 인, 가정 이동할 및 페더레이션 서버 프록시 컴퓨터에서 메모장에서 Web.config 파일을 엽니다, 그리고 다음 섹션을 찾습니다, 그리고 대로 포트 번호를 수정 아래 강조 표시 한 다음 저장 하 고 메모장을 종료 합니다.  
  
    ```  
    <securityTokenService samlProtocolEndpoint="https://sts1.contoso.com:444/adfs/services/trust/samlprotocol/proxycertificatetransport"  
          wsTrustEndpoint="https://sts1.contoso.com:444/adfs/services/trust/proxycertificatetransport" />  
    ```  
  
4.  페더레이션 서버 프록시 서비스가 사용자 계정 액세스 제어 목록에 추가 \(ACL\) 관련된 끝점 Url에 대 한 합니다. 예를 들어 포트 번호가 1234 경우와 AD FSfederation 서버 프록시 실행에 사용 되는 사용자 계정에서 서비스는 기본 제공\-네트워크 서비스 계정으로 명령 프롬프트에서 다음 명령을 입력 합니다.  
  
    ```  
    netsh http add urlacl https://+:444/adfs/fs/federationserverservice.asmx/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/FederationMetadata/2007-06/ user="NT Authority\Network Service"  
    netsh http add urlacl https://+:444/adfs/services/ user="NT Authority\Network Service"  
  
    netsh http add urlacl http://+:81/adfs/services/ user="NT Authority\Network Service"  
    ```  
  
    이전 명령은 페더레이션 서버와 페더레이션 서버 프록시 컴퓨터에서 실행 되어야 합니다.  
  
## <a name="additional-references"></a>추가 참조  
[검사 목록: 페더레이션 서버 프록시 설정](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

