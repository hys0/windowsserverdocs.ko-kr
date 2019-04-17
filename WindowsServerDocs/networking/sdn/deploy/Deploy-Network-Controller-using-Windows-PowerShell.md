---
title: 네트워크 컨트롤러를 사용 하 여 Windows PowerShell 배포
description: 이 항목에서 Windows PowerShell를 사용 하 여 컴퓨터 또는 Vm (가상 컴퓨터) Windows Server 2016을 실행 하는 하나 이상의 네트워크 컨트롤러 배포 하는 지침을 제공 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 2448d381-55aa-4c14-997a-202c537c6727
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cfd06662f317381fb77bf31db5ed60c2489ff871
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-network-controller-using-windows-powershell"></a>네트워크 컨트롤러를 사용 하 여 Windows PowerShell 배포

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서 Windows PowerShell를 사용 하 여 네트워크 컨트롤러에서 하나 이상의 Vm (가상 컴퓨터) Windows Server 2016을 실행 하는 배포 하는 지침을 제공 합니다.

>[!IMPORTANT]
>네트워크 컨트롤러 서버 역할 실제 호스트에서를 배포 하지 않습니다. Hyper-v 가상 컴퓨터가에 네트워크 컨트롤러 서버 역할 설치 해야 하는 배포 하는 네트워크 컨트롤러, Hyper-v 호스트에 설치 되어 있는 \(VM\) 합니다. 네트워크 컨트롤러 Vm에서 세 가지 Hyper\ V 호스트에서를 설치한 후 Windows PowerShell 명령을 사용 하 여 네트워크 컨트롤러 호스트 추가 하 여 소프트웨어 네트워킹 정의 \(SDN\)에 대해 Hyper\ V 호스트를 설정 해야 **새로 NetworkControllerServer**합니다. 이렇게 하면 SDN 소프트웨어 부하 분산 기능을 사용할 수 있게 됩니다. 자세한 내용은 참조 [새로 NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)합니다.

이 항목 다음 섹션에 포함 되어 있습니다.

- [네트워크 컨트롤러 서버 역할을 설치](#bkmk_role)

- [네트워크 컨트롤러 클러스터 구성](#bkmk_configure)

- [네트워크 컨트롤러 응용 프로그램을 구성](#bkmk_app)

- [네트워크 컨트롤러 배포 유효성 검사](#bkmk_validation)

- [네트워크 컨트롤러에 대 한 추가 Windows PowerShell 명령](#bkmk_ps)

- [네트워크 컨트롤러 구성 스크립트 샘플](#bkmk_script)

- [이후 Post-Deployment 비 Kerberos 배포용 단계](#bkmk_nonkerb)

## <a name="bkmk_role"></a>네트워크 컨트롤러 서버 역할을 설치

이 절차를 사용 하 여 네트워크 컨트롤러 서버 역할 가상 컴퓨터에 설치 하려면 \(VM\) 합니다.

>[!IMPORTANT]
>네트워크 컨트롤러 서버 역할 실제 호스트에서를 배포 하지 않습니다. Hyper-v 가상 컴퓨터가에 네트워크 컨트롤러 서버 역할 설치 해야 하는 배포 하는 네트워크 컨트롤러, Hyper-v 호스트에 설치 되어 있는 \(VM\) 합니다. 네트워크 컨트롤러 Vm에서 세 가지 Hyper\ V 호스트에서를 설치한 후 호스트 컨트롤러 네트워크에 추가 하 여 Hyper\ V 호스트 \(SDN\) 소프트웨어 네트워킹 정의를 설정 해야 합니다. 이렇게 하면 SDN 소프트웨어 부하 분산 기능을 사용할 수 있게 됩니다.

회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다.  

>[!NOTE]
>네트워크 컨트롤러 설치 즉, 서버 관리자 Windows PowerShell 대신 사용 하려는 경우 [네트워크 컨트롤러 서버 역할 서버 관리자를 사용 하 여 설치](https://technet.microsoft.com/library/mt403348.aspx)

네트워크 컨트롤러를 Windows PowerShell를 사용 하 여 설치 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

네트워크 컨트롤러 설치 컴퓨터를 다시 시작 해야 합니다. 이렇게 하기 위해 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

`Restart-Computer`

## <a name="bkmk_configure"></a>네트워크 컨트롤러 클러스터 구성

네트워크 컨트롤러 클러스터 높은 가용성와 확장성 네트워크 컨트롤러와 응용 프로그램을를 클러스터 만든 후 구성할 수 있는 클러스터 위에 호스트 되는을 제공 합니다.

>[!NOTE]
>수행할 수 있는 절차 다음 섹션에 있는 네트워크 컨트롤러, 설치 또는 Windows Server 2016 용 원격 서버 관리 도구를 사용 하 여 Windows Server 2016 또는 Windows 10을 실행 하는 원격 컴퓨터에서 절차를 수행 하 고 VM에서 직접 합니다. 또한의 회원 **관리자**, 해당 하는이 절차를 수행 하는 데 필요한 최소 또는 합니다. 컴퓨터 또는 네트워크 컨트롤러 있는 설치 VM 도메인에 가입, 사용자 계정에 속해야 **도메인 사용자**합니다.

네트워크 컨트롤러 클러스터 노드에서 개체를 만들고 클러스터를 구성 하 여 만들 수 있습니다.

### <a name="create-a-node-object"></a>노드 개체 만들기

각 구성원 네트워크 컨트롤러 클러스터의 VM 노드 개체 만들려면 필요 합니다.

노드 개체를 만들려면 Windows PowerShell 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다. 배포에 적합 한 각 매개에 대 한 값을 추가 하면 있는지 확인 합니다.  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

다음 표에서의 각 매개에 대 한 설명은 **새로 NetworkControllerNodeObject** 명령을 합니다.

|매개|설명|
|-------------|---------------|
|이름|**이름** 매개 변수 클러스터에 추가 하려면 서버의 이름을 지정|
|서버|**서버** 매개 호스트 이름, 정식 도메인 이름 (FQDN), 또는 클러스터에 추가 하려면 서버의 IP 주소를 지정 합니다. 컴퓨터가 도메인에 가입 FQDN 필요 합니다.|
|FaultDomain|**FaultDomain** 매개 클러스터에 추가 하는 서버에 대 한 오류 도메인을 지정 합니다. 이 매개 클러스터에 추가 하는 서버도 동시에 오류가 발생할 수 있는 서버의 정의 합니다. 이 오류는 전원 네트워킹 소스 등 공유 물리적 종속성 때문일 수 있습니다. 일반적으로 오류 도메인와 관련 된 더 많은 서버에서 오류 도메인 밤나무 높은 지점에서 함께 실패할 수와 공유 이러한 종속성 계층을 나타냅니다. 네트워크 컨트롤러 런타임 중 클러스터의 오류 도메인을 고려 하 고 네트워크 컨트롤러 서비스 별도 오류는 도메인의 되도록 별로 하려고 합니다. 이 프로세스를 사용 하도록 있는 한 오류 도메인의 오류가 발생할 경우 해당 서비스 가용성 상태로 손상 되지 않도록 수 있습니다. 오류 도메인 계층 형식으로 지정 되어 있습니다. 예: "Fd: d c 1 월 Rack1/Host1 /", 여기서 d c 1 datacenter 이름, Rack1 랙 이름인 이며 Host1 노드 위치 호스트의 이름을 합니다.|
|RestInterface|**RestInterface** 매개 표시 상태가 전송 (REST) 통신 종료 된 노드에서 인터페이스의 이름을 지정 합니다. 네트워크 컨트롤러 인터페이스가 네트워크의 관리 계층에서 Northbound API 요청을 받습니다.|
|NodeCertificate|**NodeCertificate** 매개 컴퓨터 인증을 위한 네트워크 컨트롤러를 사용 하는 인증서를 지정 합니다. 인증서가 필요한 클러스터; 내 커뮤니케이션에 대 한 가지 옵션이 인증을 사용 하는 경우 네트워크 컨트롤러 서비스 간의 교통의 암호화 인증서도 사용 됩니다. 인증서 제목 노드의 DNS 이름을와 동일 해야 합니다.|

### <a name="configure-the-cluster"></a>클러스터 구성

클러스터를 구성 하려면 Windows PowerShell 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다. 배포에 적합 한 각 매개에 대 한 값을 추가 하면 있는지 확인 합니다.

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

다음 표에서의 각 매개에 대 한 설명은 **설치 NetworkControllerCluster** 명령을 합니다.
  
|매개|설명|
|-------------|---------------|
|ClusterAuthentication|**ClusterAuthentication** 매개 변수 보안 노드 간 통신에 사용 되는 네트워크 컨트롤러 서비스 간의 교통의 암호화는 또한 인증 유형 지정 합니다. 지원 되는 값은 **Kerberos**, **X509** 및 **없음**합니다. Kerberos 인증 도메인 계정을 사용 하 고 네트워크 컨트롤러 노드는 도메인에 가입 하는 경우에 사용할 수 있습니다. X509 기반 인증을 지정 NetworkControllerNode 개체의 인증서를 제공 해야 합니다. 또한, 사용자를 직접 제공 해야 인증서가이 명령을 실행 하기 전에 합니다.|
|ManagementSecurityGroup|**ManagementSecurityGroup** 매개 변수 관리 cmdlet 원격 컴퓨터에서 실행 하도록 허용 하는 사용자가 포함 된 보안 그룹의 이름을 지정 합니다. 이만 ClusterAuthentication Kerberos 경우 해당 합니다. 로컬 컴퓨터에서 도메인 보안 그룹 하 고 보안 그룹 하지 지정 해야 합니다.|
|노드|**노드** 매개 변수를 사용 하 여 네트워크 컨트롤러 노드 목록을 지정는 **새로 NetworkControllerNodeObject** 명령을 합니다.|
|DiagnosticLogLocation|**DiagnosticLogLocation** 매개 진단 로그가 주기적으로 업로드 됩니다 공유 위치를 지정 합니다. 이 매개에 대 한 값을 지정 하지 않으면 로그 각 노드에서 로컬로 저장 됩니다. 로그 폴더 %systemdrive%\Windows\tracing\SDNDiagnostics 로컬로 저장 됩니다. 클러스터 로그 폴더 %systemdrive%\ProgramData\Microsoft\Service Fabric\log\Traces에에서 로컬로 저장 됩니다.|
|LogLocationCredential|**LogLocationCredential** 매개 로그 저장 된 위치 공유 위치에 액세스 하기 위해 필요한 자격 증명을 지정 합니다.|
|CredentialEncryptionCertificate|**CredentialEncryptionCertificate** 매개 네트워크 컨트롤러를 사용 하 여 네트워크 컨트롤러 이진 파일에 액세스 하는 데 사용 하는 자격 증명을 암호화 인증서를 지정 및 **LogLocationCredential**지정 하는 경우, 합니다. 인증서에이 명령을 실행 하기 전에 네트워크 컨트롤러 노드의 모든 제공 해야 하 고 여 동일한 인증서 모든 클러스터 노드에서에 등록 해야 합니다. 업무 환경에서이 매개 변수를 사용 하 여 바이너리 네트워크 컨트롤러 및 로그를 보호 하는 것이 좋습니다. 이 매개 변수를 않고도 자격 증명 암호화 되지 않은 텍스트에 저장 되 고 잘못 권한 없는 사용자가 사용 될 수 있습니다.|
|자격 증명|이 매개 변수는이 명령을 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **자격 증명** 매개 변수가이 명령을 대상 컴퓨터에서 실행할 수 있는 권한이 있는 사용자 계정에 지정 합니다.|
|CertificateThumbprint|이 매개 변수는이 명령을 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **CertificateThumbprint** 매개 변수 공개 키의 디지털 인증서 (X509)가이 명령을 대상 컴퓨터에서 실행할 수 있는 권한이 있는 사용자 계정에 지정 합니다.|
|UseSSL|이 매개 변수는이 명령을 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **UseSSL** 원격 컴퓨터에 연결 하는 데 사용 되는 소켓 SSL (Secure Layer) 프로토콜을 지정 합니다. 기본적으로 SSL 사용 되지 않습니다.|
|컴퓨터 이름|**ComputerName** 매개이 명령을 실행 되는 네트워크 컨트롤러 노드를 지정 합니다. 이 매개에 대 한 값을 지정 하지 않으면 로컬 컴퓨터 기본적으로 사용 됩니다.|
|LogSizeLimitInMBs|이 매개 로그 최대 크기를 mb 네트워크 컨트롤러를 저장할 수 있는 지정 합니다. 로그는 돌려서에 저장 됩니다. 이 매개 기본값 DiagnosticLogLocation이 제공 된 경우 40 g B 수 있습니다. DiagnosticLogLocation 제공 되지 않은 경우 로그 네트워크 컨트롤러 노드에 저장 되 고이 매개 기본값은 15GB 합니다.|
|LogTimeLimitInDays|이 매개 시간 제한 로그 저장 된 일 내에 지정 합니다. 로그는 돌려서에 저장 됩니다. 이 매개 기본값 3 일입니다.|

## <a name="bkmk_app"></a>네트워크 컨트롤러 응용 프로그램을 구성
네트워크 컨트롤러 응용 프로그램을 구성 하려면 Windows PowerShell 명령 프롬프트에서 다음 명령을 입력 하 고 ENTER 키를 누릅니다. 배포에 적합 한 각 매개에 대 한 값을 추가 하면 있는지 확인 합니다.

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

다음 표에서의 각 매개에 대 한 설명은 **설치 NetworkController** 명령을 합니다.

|매개|설명|
|-------------|---------------|
|ClientAuthentication|**ClientAuthentication** 매개 변수 나머지 네트워크 컨트롤러와 커뮤니케이션 보호 하기 위한 사용 되는 인증 유형 지정 합니다. 지원 되는 값은 **Kerberos**, **X509** 및 **없음**합니다. Kerberos 인증 도메인 계정을 사용 하 고 네트워크 컨트롤러 노드는 도메인에 가입 하는 경우에 사용할 수 있습니다. X509 기반 인증을 지정 NetworkControllerNode 개체의 인증서를 제공 해야 합니다. 또한, 사용자를 직접 제공 해야 인증서가이 명령을 실행 하기 전에 합니다.|
|노드|**노드** 매개 변수를 사용 하 여 네트워크 컨트롤러 노드 목록을 지정는 **새로 NetworkControllerNodeObject** 명령을 합니다.|
|ClientCertificateThumbprint|이 매개 변수는 네트워크 컨트롤러 클라이언트에 대 한 가지 옵션이 인증을 사용 하는 경우에 필요 합니다. **ClientCertificateThumbprint** 매개 지문을 클라이언트 Northbound layer에 등록 인증서를 지정 합니다.|
|못했기|**못했기** 매개 네트워크 컨트롤러를 사용 하 여 해당 id를 클라이언트 증명 인증서를 지정 합니다. 서버 인증서 키 사용 향상 확장에서 서버 인증 목적을 포함 해야 하며 클라이언트에서 신뢰할 수 있는 캘리포니아에서 네트워크 컨트롤러를 발행 해야 합니다.|
|RESTIPAddress|값을 지정 필요가 없습니다 **RESTIPAddress** 네트워크 컨트롤러의 단일 노드 배포 됩니다. 여러 노드 배포는 **RESTIPAddress** 매개 변수 CIDR 표기법에서 나머지 endpoint의 IP 주소를 지정 합니다. 예를 들어, 192.168.1.10 월 24 합니다. 주체 이름 값 **못했기** 값을 해결 해야는 **RESTIPAddress** 매개 합니다. 모든 노드 같은 서브넷에 있는 경우 모든 여러 노드 네트워크 컨트롤러 배포에 대 한이 매개 지정 해야 합니다. 사용 해야 노드 인 서로 다른 서브넷에는 **RestName** 매개 변수를 사용 하는 대신 **RESTIPAddress**합니다.|
|RestName|값을 지정 필요가 없습니다 **RestName** 네트워크 컨트롤러의 단일 노드 배포 됩니다. 경우에에 대 한 값 지정 해야 **RestName** 다른 서브넷에 노드 경우 여러 노드 배포 됩니다. 여러 노드 배포는 **RestName** 매개 변수 네트워크 컨트롤러 클러스터에 대 한 FQDN 지정 합니다.|
|ClientSecurityGroup|**ClientSecurityGroup** 매개 변수 구성원 네트워크 컨트롤러 클라이언트 인 Active Directory 보안 그룹의 이름을 지정 합니다. 이 매개는 Kerberos 인증을 사용 하는 경우에 **ClientAuthentication**합니다. 보안 그룹, REST Api 액세스 되어 있는 계정이 있어야 하 고 보안 그룹을 만들고이 명령을 실행 하기 전에 구성원 추가 해야 합니다.|
|자격 증명|이 매개 변수는이 명령을 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **자격 증명** 매개 변수가이 명령을 대상 컴퓨터에서 실행할 수 있는 권한이 있는 사용자 계정에 지정 합니다.|
|CertificateThumbprint|이 매개 변수는이 명령을 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **CertificateThumbprint** 매개 변수 공개 키의 디지털 인증서 (X509)가이 명령을 대상 컴퓨터에서 실행할 수 있는 권한이 있는 사용자 계정에 지정 합니다.|
|UseSSL|이 매개 변수는이 명령을 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **UseSSL** 원격 컴퓨터에 연결 하는 데 사용 되는 소켓 SSL (Secure Layer) 프로토콜을 지정 합니다. 기본적으로 SSL 사용 되지 않습니다.|

네트워크 컨트롤러 응용 프로그램의 구성을 완료 한 후 네트워크 컨트롤러 배포 완료 되었습니다.

## <a name="bkmk_validation"></a>네트워크 컨트롤러 배포 유효성 검사

네트워크 컨트롤러 배포의 유효성을 검사 하기 네트워크 컨트롤러 자격 증명을 추가 하 고 후의 자격 증명을 검색할 수 있습니다.

Kerberos ClientAuthentication 메커니즘 멤버 자격으로 사용 중인 경우는 **ClientSecurityGroup** 이 절차를 수행 하는 데 필요한 최소한은 사용자가 만든 합니다.

#### <a name="to-validate-deployment-of-network-controller"></a>네트워크 컨트롤러의 배포의 유효성을 검사 하려면

1.  클라이언트 컴퓨터에서 Kerberos ClientAuthentication 메커니즘을 사용 하는 경우 계정에 로그인 한 사용자의 구성원에 **ClientSecurityGroup**합니다.

2. Windows PowerShell 열고 네트워크 컨트롤러 자격 증명을 추가 하려면 다음 명령을 입력 ENTER 키를 누릅니다. 배포에 적합 한 각 매개에 대 한 값을 추가 하면 있는지 확인 합니다.

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. 네트워크 컨트롤러에 추가 하는 자격 증명을 검색 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다. 배포에 적합 한 각 매개에 대 한 값을 추가 하면 있는지 확인 합니다.

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. 출력 다음 예제 출력 비슷한 있어야 검토 합니다.

    ```
    Tags                   :
    ResourceRef     : /credentials/cred1
    CreatedTime    : 1/1/0001 12:00:00 AM
    InstanceId        : e16ffe62-a701-4d31-915e-7234d4bc5a18
    Etag                  : W/"1ec59631-607f-4d3e-ac78-94b0822f3a9d"
    ResourceMetadata :
    ResourceId       : cred1
    Properties       : Microsoft.Windows.NetworkController.CredentialProperties
    ```

    > [!NOTE]
    > 실행 하는 경우는 **Get NetworkControllerCredential** 명령 점을 통신사 목록 속성 자격 증명을 사용 하 여 명령 출력 변수를 지정할 수 있습니다. 예를 들어, $cred 합니다. 속성 합니다.

## <a name="bkmk_ps"></a>네트워크 컨트롤러에 대 한 추가 Windows PowerShell 명령

네트워크 컨트롤러를 배포한 후 관리 하 고 배포 수정 Windows PowerShell 명령을 사용할 수 있습니다. 다음은 일부의 배포 하기 시도할 수 있는 변경 합니다.

- 네트워크 컨트롤러 노드와 클러스터, 응용 프로그램 설정을 수정합니다

- 네트워크 컨트롤러 클러스터 및 응용 프로그램 제거

- 네트워크 컨트롤러 클러스터 노드가 포함 하 여 추가, 제거, 설정 및 노드 비활성화 관리 합니다.

다음 표에서 이러한 작업을 수행 하는 데 사용할 수 있는 Windows PowerShell 명령에 대해 구문을 제공 합니다.

|작업|명령|구문|
|--------|-------|----------|
|네트워크 컨트롤러 클러스터 설정을 수정합니다|Set-NetworkControllerCluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 응용 프로그램 설정을 수정합니다|설정 NetworkController|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 노드 설정을 수정합니다|Set-NetworkControllerNode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 진단 설정을 수정합니다|Set-NetworkControllerDiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 응용 프로그램을 제거|Uninstall-NetworkController|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 클러스터 제거|Uninstall-NetworkControllerCluster|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 클러스터 노드가 추가|Add-NetworkControllerNode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|네트워크 컨트롤러 클러스터 노드에서 사용 안 함|Disable-NetworkControllerNode|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|클러스터 노드가 네트워크 컨트롤러를 사용 하도록 설정|Enable-NetworkControllerNode|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|네트워크 컨트롤러 노드에서 클러스터에서 제거|Remove-NetworkControllerNode|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>네트워크 컨트롤러에 대 한 Windows PowerShell 명령에 TechNet 라이브러리에 있는 [네트워크 컨트롤러 Cmdlet](https://technet.microsoft.com/library/mt576401.aspx)합니다.

## <a name="bkmk_script"></a>네트워크 컨트롤러 구성 스크립트 샘플

다음 샘플 구성 스크립트 여러 노드 네트워크 컨트롤러 클러스터 만들고 네트워크 컨트롤러 응용 프로그램을 설치 하는 방법을 보여 줍니다. 또한 $cert 변수 제목 이름 문자열 "networkController.contoso.com" 일치 하는 로컬 컴퓨터 인증서 스토어에서는 인증서를 선택 합니다.

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="bkmk_nonkerb"></a>배포 후에 대 한 단계 비-Kerberos 배포

네트워크 컨트롤러 배포 Kerberos을 사용 하지 않는 경우 인증서 배포 해야 합니다.

자세한 내용은 참조 [네트워크 컨트롤러용 배포 후 단계](../technologies/network-controller/post-deploy-steps-nc.md)합니다.


