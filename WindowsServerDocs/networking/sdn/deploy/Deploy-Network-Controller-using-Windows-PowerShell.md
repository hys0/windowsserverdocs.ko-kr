---
title: Windows PowerShell을 사용하여 네트워크 컨트롤러 배포
description: 이 항목에서는 하나 이상의 컴퓨터 또는 Windows Server 2016를 실행 하는 가상 컴퓨터 (Vm)에서 네트워크 컨트롤러를 배포 하려면 Windows PowerShell을 사용 하 여 설명 합니다.
manager: dougkim
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
ms.date: 08/23/2018
ms.openlocfilehash: 31c1579dc840f6f4eb805ac4e10f51192a6b4c99
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816194"
---
# <a name="deploy-network-controller-using-windows-powershell"></a>Windows PowerShell을 사용하여 네트워크 컨트롤러 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 하나 이상의 가상 머신에서 (Vm) Windows Server 2016을 실행 하는 네트워크 컨트롤러를 배포 하려면 Windows PowerShell을 사용 하 여 지침을 제공 합니다.

>[!IMPORTANT]
>실제 호스트에서 네트워크 컨트롤러 서버 역할을 배포 하지 않습니다. 네트워크 컨트롤러를 배포 하려면 Hyper-v 가상 컴퓨터에서 네트워크 컨트롤러 서버 역할을 설치 해야 \(VM\) Hyper-v 호스트에 설치 된. 세 가지 다른 하이퍼의 Vm에서 네트워크 컨트롤러를 설치한 후\-V 호스트 Hyper을 사용 하도록 설정 해야\-소프트웨어 정의 네트워킹에 대 한 호스트 \(SDN\) 호스트를 사용 하 여 네트워크 컨트롤러를 추가 하 여 Windows PowerShell 명령 **새로 만들기-NetworkControllerServer**합니다. 이렇게 하면 함수에 SDN 소프트웨어 부하 분산 장치를 사용 하는 합니다. 자세한 내용은 [새로 만들기-NetworkControllerServer](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollerserver)합니다.

이 항목에는 다음 섹션이 수록되어 있습니다.

- [네트워크 컨트롤러 서버 역할 설치](#bkmk_role)

- [네트워크 컨트롤러 클러스터 구성](#bkmk_configure)

- [네트워크 컨트롤러 응용 프로그램 구성](#bkmk_app)

- [네트워크 컨트롤러 배포 유효성 검사](#bkmk_validation)

- [네트워크 컨트롤러에 대 한 추가 Windows PowerShell 명령](#bkmk_ps)

- [샘플 네트워크 컨트롤러 구성 스크립트](#bkmk_script)

- [비-Kerberos 배포에 대 한 배포 후 단계](#bkmk_nonkerb)

## <a name="install-the-network-controller-server-role"></a>네트워크 컨트롤러 서버 역할 설치

이 절차를 사용 하 여 가상 컴퓨터에서 네트워크 컨트롤러 서버 역할을 설치 하려면 \(VM\)합니다.

>[!IMPORTANT]
>실제 호스트에서 네트워크 컨트롤러 서버 역할을 배포 하지 않습니다. 네트워크 컨트롤러를 배포 하려면 Hyper-v 가상 컴퓨터에서 네트워크 컨트롤러 서버 역할을 설치 해야 \(VM\) Hyper-v 호스트에 설치 된. 세 가지 다른 하이퍼의 Vm에서 네트워크 컨트롤러를 설치한 후\-V 호스트 Hyper을 사용 하도록 설정 해야\-소프트웨어 정의 네트워킹에 대 한 호스트 \(SDN\) 네트워크 컨트롤러 호스트를 추가 하 여 합니다. 이렇게 하면 함수에 SDN 소프트웨어 부하 분산 장치를 사용 하는 합니다.

이 절차를 수행하려면 최소한 **Administrators** 그룹의 구성원이거나 이와 동등한 자격이 있어야 합니다.  

>[!NOTE]
>Windows PowerShell 대신 서버 관리자를 사용 하 여 네트워크 컨트롤러 설치를 참조 하려는 경우 [서버 관리자를 사용 하 여 네트워크 컨트롤러 서버 역할 설치](https://technet.microsoft.com/library/mt403348.aspx)

Windows PowerShell을 사용 하 여 네트워크 컨트롤러를 설치 하려면 Windows PowerShell 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다.

`Install-WindowsFeature -Name NetworkController -IncludeManagementTools`

네트워크 컨트롤러 설치 컴퓨터를 다시 시작 해야 합니다. 이렇게 하려면 다음 명령을 입력 하 고 ENTER 키를 누릅니다.

`Restart-Computer`

## <a name="configure-the-network-controller-cluster"></a>네트워크 컨트롤러 클러스터 구성

네트워크 컨트롤러 클러스터 높은 가용성과 네트워크 컨트롤러 응용 프로그램에 클러스터를 만든 후 구성할 수 있으며, 이렇게 클러스터 위에 호스팅되는 확장성을 제공 합니다.

>[!NOTE]
>수 절차를 수행한 다음 섹션에서 네트워크 컨트롤러를 설치 하거나 실행 하는 원격 컴퓨터에서 절차를 수행 하려면 원격 서버 관리 도구에 대 한 Windows Server 2016을 사용할 수 있는 VM에서 직접 Windows Server 2016 또는 Windows 10입니다. 또한의 멤버 자격이 **관리자**, 또는 이와 동등한이 절차를 수행 하는 데 필요한 최소입니다. 네트워크 컨트롤러를 설치한 VM 또는 컴퓨터 도메인에 가입 된, 사용자 계정에 속해야 **도메인 사용자**합니다.

네트워크 컨트롤러 클러스터 노드 개체를 만들고 다음 클러스터를 구성 하 여 만들 수 있습니다.

### <a name="create-a-node-object"></a>노드 개체 만들기

네트워크 컨트롤러 클러스터의 구성원 인 각 VM에 대 한 노드 개체를 만들려고 합니다.

노드 개체를 만들려면 Windows PowerShell 명령 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다. 추가한 각 매개 변수에 대 한 배포에 대 한 적절 한 값을 확인 합니다.  

```
New-NetworkControllerNodeObject -Name <string> -Server <String> -FaultDomain <string>-RestInterface <string> [-NodeCertificate <X509Certificate2>]
```

다음 표에서 각 매개 변수에 **새로 NetworkControllerNodeObject** 명령입니다.

|매개 변수|설명|
|-------------|---------------|
|이름|**이름** 매개 변수는 클러스터에 추가 하려는 서버의 이름을 지정 합니다.|
|서버|**서버** 매개 변수는 호스트 이름, 완벽 하 게 정규화 된 도메인 이름 (FQDN), 또는 클러스터에 추가 하려는 서버의 IP 주소를 지정 합니다. 도메인에 가입 된 컴퓨터에 대 한 FQDN이 필요 합니다.|
|FaultDomain|**FaultDomain** 매개 변수는 클러스터에 추가 하는 서버에 대 한 오류 도메인을 지정 합니다. 이 매개 변수는 클러스터에 추가 하는 서버와 동시에 오류를 경험할 수 있는 서버를 정의 합니다. 이 오류는 전력 및 네트워킹 소스와 같은 공유 물리적 종속성 때문일 수 있습니다. 일반적으로 오류 도메인 공유 종속성 오류 도메인 트리에 있는 높은 지점에서 함께 실패할 가능성이 더 많은 서버와 관련 된 계층 구조를 나타냅니다. 런타임 중에, 네트워크 컨트롤러는 클러스터의 장애 도메인을 고려 하 고 분산 된 네트워크 컨트롤러 서비스 별도 오류 도메인에 있도록 하려고 합니다. 이 프로세스 사용 하면, 어떤 하나씩 오류 도메인 오류가 발생 한 경우 상태 및 해당 서비스의 가용성을 손상 되지 않습니다. 오류 도메인 계층 구조 형식에 지정 됩니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. "Fd: / DC1/Rack1/Host1" 여기서 d c 1는 데이터 센터 이름, rack1 랙 이름 고 Host1 노드를 배치할 호스트의 이름입니다.|
|RestInterface|**RestInterface** 매개 변수 REPRESENTATIONAL State Transfer () 통신을 종료 하는 노드에서 인터페이스의 이름을 지정 합니다. 이 네트워크 컨트롤러 인터페이스에서 네트워크의 관리 계층 Northbound API 요청을 수신합니다.|
|NodeCertificate|**NodeCertificate** 매개 변수는 네트워크 컨트롤러 컴퓨터 인증을 위해 사용 하는 인증서를 지정 합니다. 인증서가 필요한; 클러스터 내에서 통신에 대 한 인증서 기반 인증을 사용 하는 경우 인증서는 또한 네트워크 컨트롤러 서비스 간의 트래픽을 암호화에 사용 됩니다. 인증서 주체 이름은 노드의 DNS 이름으로 동일 해야 합니다.|

### <a name="configure-the-cluster"></a>클러스터 구성

클러스터를 구성 하려면 Windows PowerShell 명령 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다. 추가한 각 매개 변수에 대 한 배포에 대 한 적절 한 값을 확인 합니다.

```
Install-NetworkControllerCluster -Node <NetworkControllerNode[]> -ClusterAuthentication <ClusterAuthentication> [-ManagementSecurityGroup <string>][-DiagnosticLogLocation <string>][-LogLocationCredential <PSCredential>] [-CredentialEncryptionCertificate <X509Certificate2>][-Credential <PSCredential>][-CertificateThumbprint <String>] [-UseSSL][-ComputerName <string>][-LogSizeLimitInMBs<UInt32>] [-LogTimeLimitInDays<UInt32>]
```

다음 표에서 각 매개 변수에 **설치 NetworkControllerCluster**  명령입니다.
  
|매개 변수|설명|
|-------------|---------------|
|ClusterAuthentication|**ClusterAuthentication** 매개 변수는 노드 간의 통신 보안에 사용 되 고는 네트워크 컨트롤러 서비스 간의 트래픽이 암호화에도 사용 하는 인증 형식을 지정 합니다. 지원 되는 값은 **Kerberos**, **X509** 및 **None**합니다. Kerberos 인증 도메인 계정을 사용 하 고 네트워크 컨트롤러 노드는 도메인에 가입 된 경우에 사용할 수 있습니다. X509 기반 인증을 지정 하면 NetworkControllerNode 개체에 있는 인증서를 제공 해야 합니다. 또한이 명령을 실행 하기 전에 인증서에 제공 해야 수동으로.|
|ManagementSecurityGroup|**ManagementSecurityGroup** 매개 변수는 원격 컴퓨터에서 관리 cmdlet을 실행 하도록 허용 된 사용자를 포함 하는 보안 그룹의 이름을 지정 합니다. 이 작업은 ClusterAuthentication Kerberos이 경우에 있습니다. 도메인 보안 그룹 및 보안 그룹이 아닌 로컬 컴퓨터에 지정 해야 합니다.|
|노드|**노드** 매개 변수를 사용 하 여 만든 네트워크 컨트롤러 노드 목록이 지정는 **새로 NetworkControllerNodeObject** 명령입니다.|
|DiagnosticLogLocation|**DiagnosticLogLocation** 매개 변수 진단 로그는 주기적으로 업로드 있는 공유 위치를 지정 합니다. 이 매개 변수 값을 지정 하지 않으면 로그는 각 노드에 로컬로 저장 됩니다. 로그 폴더 %systemdrive%\Windows\tracing\SDNDiagnostics 로컬로 저장 됩니다. 클러스터 로그 폴더 %systemdrive%\ProgramData\Microsoft\Service Fabric\log\Traces에에서 로컬로 저장 됩니다.|
|LogLocationCredential|**LogLocationCredential** 매개 변수는 로그를 저장할 공유 위치에 액세스 하는 데 필요한 자격 증명을 지정 합니다.|
|CredentialEncryptionCertificate|**CredentialEncryptionCertificate** 네트워크 컨트롤러를 사용 하 여 네트워크 컨트롤러 이진 파일에 액세스 하는 데 사용 되는 자격 증명을 암호화 인증서를 지정 하는 매개 변수 및 **LogLocationCredential**, 지정 된 경우. 이 명령을 실행 하기 전에 네트워크 컨트롤러 노드를 모두에 인증서를 프로 비전 해야 하 고 모든 클러스터 노드 중에서 동일한 인증서를 등록 해야 합니다. 이 매개 변수를 사용 하 여 네트워크 컨트롤러 이진 파일 및 로그를 보호 하기 위해 프로덕션 환경에서는 좋습니다. 이 매개 변수가 없으면 자격 증명은 일반 텍스트로 저장 되 고 권한이 없는 사용자가 악용할 수 있습니다.|
|자격 증명|이 매개 변수는이 명령은 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **자격 증명** 매개 변수는 대상 컴퓨터에이 명령을 실행할 수 있는 권한을 가진 사용자 계정을 지정 합니다.|
|CertificateThumbprint|이 매개 변수는이 명령은 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **CertificateThumbprint** 디지털 공개 키 인증서 (X509) 대상 컴퓨터에서이 명령을 실행할 수 있는 권한이 있는 사용자 계정의 매개 변수를 지정 합니다.|
|UseSSL|이 매개 변수는이 명령은 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **UseSSL** 매개 변수는 원격 컴퓨터에 대 한 연결을 설정 하는 데 사용 되는 Secure Sockets Layer (SSL) 프로토콜을 지정 합니다. 기본적으로 SSL은 사용되지 않습니다.|
|ComputerName|**ComputerName** 매개 변수는이 명령을 실행 되는 네트워크 컨트롤러 노드를 지정 합니다. 이 매개 변수 값을 지정 하지 않으면 경우 로컬 컴퓨터는 기본적으로 사용 됩니다.|
|LogSizeLimitInMBs|이 매개 변수 (mb) 네트워크 컨트롤러를 저장할 수 있는 최대 로그 크기를 지정 합니다. 로그는 순환 방식으로 저장 됩니다. DiagnosticLogLocation를 제공 하는 경우이 매개 변수의 기본값은 40GB입니다. DiagnosticLogLocation 제공 되지 않은 경우 로그는 네트워크 컨트롤러 노드에 저장 됩니다 하 고이 매개 변수의 기본값은 15 GB입니다.|
|LogTimeLimitInDays|이 매개 변수 로그 저장 됩니다 일 기간 제한을 지정 합니다. 로그는 순환 방식으로 저장 됩니다. 이 매개 변수의 기본값은 3 일입니다.|

## <a name="configure-the-network-controller-application"></a>네트워크 컨트롤러 응용 프로그램 구성
네트워크 컨트롤러 응용 프로그램을 구성 하려면 Windows PowerShell 명령 프롬프트에서 다음 명령을 입력 한 다음 ENTER 키를 누릅니다. 추가한 각 매개 변수에 대 한 배포에 대 한 적절 한 값을 확인 합니다.

```
Install-NetworkController -Node <NetworkControllerNode[]> -ClientAuthentication <ClientAuthentication>  [-ClientCertificateThumbprint <string[]>]  [-ClientSecurityGroup <string>] -ServerCertificate <X509Certificate2> [-RESTIPAddress <String>] [-RESTName <String>] [-Credential <PSCredential>][-CertificateThumbprint <String> ] [-UseSSL]
```

다음 표에서 각 매개 변수에 **설치 NetworkController** 명령입니다.

|매개 변수|설명|
|-------------|---------------|
|ClientAuthentication|**ClientAuthentication** 매개 변수는 REST 및 네트워크 컨트롤러 간의 통신 보안 유지에 사용 되는 인증 유형을 지정 합니다. 지원 되는 값은 **Kerberos**, **X509** 및 **None**합니다. Kerberos 인증 도메인 계정을 사용 하 고 네트워크 컨트롤러 노드는 도메인에 가입 된 경우에 사용할 수 있습니다. X509 기반 인증을 지정 하면 NetworkControllerNode 개체에 있는 인증서를 제공 해야 합니다. 또한이 명령을 실행 하기 전에 인증서에 제공 해야 수동으로.|
|노드|**노드** 매개 변수를 사용 하 여 만든 네트워크 컨트롤러 노드 목록이 지정는 **새로 NetworkControllerNodeObject** 명령입니다.|
|ClientCertificateThumbprint|이 매개 변수는 네트워크 컨트롤러 클라이언트에 대 한 인증서 기반 인증을 사용 하는 경우에 필요 합니다. **ClientCertificateThumbprint** 매개 변수는 Northbound 계층에서 클라이언트에 등록 된 인증서의 지문을 지정 합니다.|
|못했기|**못했기** 매개 변수를 클라이언트의 id를 증명 하기 위해 사용 하 여 네트워크 컨트롤러는 인증서를 지정 합니다. 서버 인증서는 서버 인증 용도로 확장 된 키 사용 확장에 포함 해야 하 고 클라이언트에서 신뢰할 수 있는 CA가 네트워크 컨트롤러에 발급 되어야 합니다.|
|RESTIPAddress|에 대 한 값을 지정할 필요가 없습니다 **RESTIPAddress** 네트워크 컨트롤러의 단일 노드 배포 합니다. 다중 노드 배포는 **RESTIPAddress** 매개 변수는 CIDR 표기법에서 REST 끝점의 IP 주소를 지정 합니다. 예를 들어 192.168.1.10/24 합니다. 주체 이름 값 **못했기** 의 값을 확인 해야 합니다는 **RESTIPAddress** 매개 변수입니다. 이 매개 변수는 동일한 서브넷에 있는 모든 노드의 경우 모든 다중 노드 네트워크 컨트롤러 배포에 대해 지정 되어야 합니다. 사용 해야 노드는 서로 다른 서브넷에 있는 경우는 **RestName** 매개 변수를 사용 하 여 대신 **RESTIPAddress**합니다.|
|RestName|에 대 한 값을 지정할 필요가 없습니다 **RestName** 네트워크 컨트롤러의 단일 노드 배포 합니다. 에 값을 지정 해야 **RestName** 다중 노드 배포는 서로 다른 서브넷에 있는 노드가 포함 된 경우. 다중 노드 배포는 **RestName** 매개 변수는 네트워크 컨트롤러 클러스터에 대 한 FQDN을 지정 합니다.|
|ClientSecurityGroup|**ClientSecurityGroup** 매개 변수 멤버는 네트워크 컨트롤러 클라이언트는 Active Directory 보안 그룹의 이름을 지정 합니다. 에 대 한 Kerberos 인증을 사용 하는 경우에이 매개 변수는 필수 **ClientAuthentication**합니다. 보안 그룹에는 REST Api 액세스 되는 계정 이어야 하며 보안 그룹을 만들고이 명령을 실행 하기 전에 구성원을 추가 해야 합니다.|
|자격 증명|이 매개 변수는이 명령은 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **자격 증명** 매개 변수는 대상 컴퓨터에이 명령을 실행할 수 있는 권한을 가진 사용자 계정을 지정 합니다.|
|CertificateThumbprint|이 매개 변수는이 명령은 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **CertificateThumbprint** 디지털 공개 키 인증서 (X509) 대상 컴퓨터에서이 명령을 실행할 수 있는 권한이 있는 사용자 계정의 매개 변수를 지정 합니다.|
|UseSSL|이 매개 변수는이 명령은 원격 컴퓨터에서 실행 하는 경우에 필요 합니다. **UseSSL** 매개 변수는 원격 컴퓨터에 대 한 연결을 설정 하는 데 사용 되는 Secure Sockets Layer (SSL) 프로토콜을 지정 합니다. 기본적으로 SSL은 사용되지 않습니다.|

네트워크 컨트롤러 응용 프로그램의 구성을 완료 한 후 네트워크 컨트롤러의 배포가 완료 되었습니다.

## <a name="network-controller-deployment-validation"></a>네트워크 컨트롤러 배포 유효성 검사

네트워크 컨트롤러 배포의 유효성을 검사 하려면 자격 증명을 네트워크 컨트롤러에 추가 하 고 자격 증명을 검색 한 다음 키를 누릅니다.

멤버 자격이 ClientAuthentication 메커니즘으로 Kerberos를 사용 한다면는 **ClientSecurityGroup** 을 만들어야 하는 것은이 절차를 수행 하는 데 필요한 최소입니다.

**절차:**

1.  클라이언트 컴퓨터에서 Kerberos를 ClientAuthentication 메커니즘으로 사용 하는 경우 로그온의 구성원 인 사용자 계정과 사용자 **ClientSecurityGroup**합니다.

2. Windows PowerShell을 열고 자격 증명을 네트워크 컨트롤러를 추가 하려면 다음 명령을 입력 한 다음 ENTER 키를 누릅니다. 추가한 각 매개 변수에 대 한 배포에 대 한 적절 한 값을 확인 합니다.

    ```
    $cred=New-Object Microsoft.Windows.Networkcontroller.credentialproperties
    $cred.type="usernamepassword"
    $cred.username="admin"
    $cred.value="abcd"

    New-NetworkControllerCredential -ConnectionUri https://networkcontroller -Properties $cred -ResourceId cred1
    ```

3. 네트워크 컨트롤러에 추가 하는 자격 증명을 검색 하려면 다음 명령을 입력 한 다음 ENTER 키를 누릅니다. 추가한 각 매개 변수에 대 한 배포에 대 한 적절 한 값을 확인 합니다.

    ```
    Get-NetworkControllerCredential -ConnectionUri https://networkcontroller -ResourceId cred1  
    ```

4. 명령을 검토 하 고 출력에 다음 예제 출력과 유사 해야 합니다.

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
    > 실행 하는 경우는 **Get NetworkControllerCredential** 명령, 자격 증명의 속성을 나열 하는 점 연산자를 사용 하 여 명령의 출력을 변수에 할당할 수 있습니다. 예를 들어 $cred 합니다. 속성입니다.

## <a name="additional-windows-powershell-commands-for-network-controller"></a>네트워크 컨트롤러에 대 한 추가 Windows PowerShell 명령

네트워크 컨트롤러를 배포한 후 관리 및 배포를 수정 하려면 Windows PowerShell 명령을 사용할 수 있습니다. 다음은 배포에 적용할 수 있는 변경 내용 중 일부입니다.

- 네트워크 컨트롤러 노드, 클러스터 및 응용 프로그램 설정 수정

- 네트워크 컨트롤러 클러스터 및 응용 프로그램을 제거 합니다.

- 네트워크 컨트롤러 클러스터 노드를 추가, 제거, 활성화 및 노드를 사용 하지 않도록 설정 등을 관리 합니다.

다음 표에서 이러한 작업 수행을 위해 사용할 수 있는 Windows PowerShell에 대 한 구문의 명령을 제공 합니다.

|태스크|Command|구문|
|--------|-------|----------|
|네트워크 컨트롤러 클러스터 설정 수정|집합 NetworkControllerCluster|`Set-NetworkControllerCluster [-ManagementSecurityGroup <string>][-Credential <PSCredential>] [-computerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 응용 프로그램 설정 수정|집합 NetworkController|`Set-NetworkController [-ClientAuthentication <ClientAuthentication>] [-Credential <PSCredential>] [-ClientCertificateThumbprint <string[]>] [-ClientSecurityGroup <string>] [-ServerCertificate <X509Certificate2>] [-RestIPAddress <String>] [-ComputerName <String>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 노드 설정 수정|집합 NetworkControllerNode|`Set-NetworkControllerNode -Name <string> > [-RestInterface <string>] [-NodeCertificate <X509Certificate2>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 진단 설정 수정|집합 NetworkControllerDiagnostic|`Set-NetworkControllerDiagnostic [-LogScope <string>] [-DiagnosticLogLocation <string>] [-LogLocationCredential <PSCredential>] [-UseLocalLogLocation] >] [-LogLevel <loglevel>][-LogSizeLimitInMBs <uint32>] [-LogTimeLimitInDays <uint32>] [-Credential <PSCredential>] [-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 응용 프로그램 제거|NetworkController 제거|`Uninstall-NetworkController [-Credential <PSCredential>][-ComputerName <string>] [-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 클러스터 제거|NetworkControllerCluster 제거|`Uninstall-NetworkControllerCluster [-Credential <PSCredential>][-ComputerName <string>][-CertificateThumbprint <String> ] [-UseSSL]`
|네트워크 컨트롤러 클러스터에 노드 추가|추가 NetworkControllerNode|`Add-NetworkControllerNode -FaultDomain <String> -Name <String> -RestInterface <String> -Server <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-NodeCertificate <X509Certificate2> ] [-PassThru] [-UseSsl]`
|네트워크 컨트롤러 클러스터 노드를 사용 하지 않도록 설정|NetworkControllerNode 사용 안 함|`Disable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|네트워크 컨트롤러 클러스터 노드를 사용 하도록 설정|NetworkControllerNode 사용|`Enable-NetworkControllerNode -Name <String> [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-PassThru] [-UseSsl]`
|클러스터에서 네트워크 컨트롤러 노드를 제거 합니다.|NetworkControllerNode 제거|`Remove-NetworkControllerNode [-CertificateThumbprint <String> ] [-ComputerName <String> ] [-Credential <PSCredential> ] [-Force] [-Name <String> ] [-PassThru] [-UseSsl]`

>[!NOTE]
>네트워크 컨트롤러에 대 한 Windows PowerShell 명령에서 TechNet 라이브러리에 있는 [네트워크 컨트롤러 Cmdlet](https://technet.microsoft.com/library/mt576401.aspx)합니다.

## <a name="sample-network-controller-configuration-script"></a>네트워크 컨트롤러 구성 스크립트 예제

다음 샘플 구성 스크립트에는 네트워크 컨트롤러 다중 노드 클러스터를 만들고 네트워크 컨트롤러 응용 프로그램을 설치 하는 방법을 보여 줍니다. 또한 $cert 변수 주체 이름 문자열 "networkController.contoso.com"와 일치 하는 로컬 컴퓨터 인증서 저장소에서 인증서를 선택 합니다.

```
$a = New-NetworkControllerNodeObject -Name Node1 -Server NCNode1.contoso.com -FaultDomain fd:/rack1/host1 -RestInterface Internal
$b = New-NetworkControllerNodeObject -Name Node2 -Server NCNode2.contoso.com -FaultDomain fd:/rack1/host2 -RestInterface Internal
$c = New-NetworkControllerNodeObject -Name Node3 -Server NCNode3.contoso.com -FaultDomain fd:/rack1/host3 -RestInterface Internal

$cert= get-item Cert:\LocalMachine\My | get-ChildItem | where {$_.Subject -imatch "networkController.contoso.com" }

Install-NetworkControllerCluster -Node @($a,$b,$c)  -ClusterAuthentication Kerberos -DiagnosticLogLocation \\share\Diagnostics - ManagementSecurityGroup Contoso\NCManagementAdmins -CredentialEncryptionCertificate $cert  
Install-NetworkController -Node @($a,$b,$c) -ClientAuthentication Kerberos -ClientSecurityGroup Contoso\NCRESTClients -ServerCertificate $cert -RestIpAddress 10.0.0.1/24
```

## <a name="post-deployment-steps-for-non-kerberos-deployments"></a>비-Kerberos 배포에 대 한 배포 후 단계

네트워크 컨트롤러 배포와 Kerberos를 사용 하지 않는 경우에 인증서를 배포 해야 합니다.

자세한 내용은 참조 [네트워크 컨트롤러에 대 한 배포 후 단계](../technologies/network-controller/post-deploy-steps-nc.md)합니다.


