---
title: 네트워크 컨트롤러 보안
description: 이 항목을 사용 하 여 네트워크 컨트롤러와 기타 소프트웨어 및 장치 간의 모든 통신에 대 한 보안을 구성 하는 방법을 배울 수 있습니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: cea660eb28645fb814d718ac04d0c9acea7b2e34
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867140"
---
# <a name="secure-the-network-controller"></a>네트워크 컨트롤러 보안

이 항목에서는 [네트워크 컨트롤러](../technologies/network-controller/network-controller.md) 와 기타 소프트웨어 및 장치 간의 모든 통신에 대 한 보안을 구성 하는 방법에 대해 알아봅니다. 

보호할 수 있는 통신 경로에는 관리 평면에 대 한 Northbound 통신, 클러스터의 네트워크 컨트롤러 가상 컴퓨터 \(vm\) 간 클러스터 통신 및 데이터에 대 한 Southbound 통신이 포함 됩니다. 수준.

1. **Northbound 통신**. 네트워크 컨트롤러는 Windows PowerShell 및 System Center Virtual Machine Manager\- \(SCVMM\)과 같은 SDN 지원 관리 소프트웨어를 사용 하 여 관리 평면에서 통신 합니다. 이러한 관리 도구는 네트워크 정책을 정의 하 고 네트워크에 대 한 목표 상태를 만들 수 있는 기능을 제공 합니다 .이를 통해 실제 구성을 목표 상태와 함께 패리티에 가져오는 실제 네트워크 구성을 비교할 수 있습니다.

2. **네트워크 컨트롤러 클러스터 통신**. 네트워크 컨트롤러 클러스터 노드로 세 개 이상의 Vm을 구성 하는 경우 이러한 노드는 서로 통신 합니다. 이러한 통신은 여러 노드 간에 데이터를 동기화 하 고 복제 하거나 네트워크 컨트롤러 서비스 간의 특정 통신에 관련 될 수 있습니다.

3.  **Southbound 통신**. 네트워크 컨트롤러는 SDN 인프라 및 소프트웨어 부하 분산 장치, 게이트웨이 및 호스트 컴퓨터와 같은 기타 장치를 사용 하 여 데이터 평면에서 통신 합니다. 네트워크 컨트롤러를 사용 하 여 이러한 southbound 장치를 구성 하 고 관리 하 여 네트워크에 대해 구성한 목표 상태를 유지할 수 있습니다.


## <a name="northbound-communication"></a>Northbound 통신

네트워크 컨트롤러는 Northbound 통신을 위한 인증, 권한 부여 및 암호화를 지원 합니다. 다음 섹션에서는 이러한 보안 설정을 구성 하는 방법에 대 한 정보를 제공 합니다.

### <a name="authentication"></a>인증

네트워크 컨트롤러 Northbound 통신에 대 한 인증을 구성 하는 경우 네트워크 컨트롤러 클러스터 노드 및 관리 클라이언트가 통신 하는 장치의 id를 확인할 수 있습니다.

네트워크 컨트롤러는 관리 클라이언트와 네트워크 컨트롤러 노드 간에 다음과 같은 세 가지 인증 모드를 지원 합니다.

>[!Note]
>System Center Virtual Machine Manager를 사용 하 여 네트워크 컨트롤러를 배포 하는 경우 **Kerberos** 모드만 지원 됩니다.

1. **Kerberos**. 관리 클라이언트와 모든 네트워크 컨트롤러 클러스터 노드를 Active Directory 도메인에 조인할 때 Kerberos 인증을 사용 합니다. Active Directory 도메인에는 인증에 사용 되는 도메인 계정이 있어야 합니다.

2. **X509**. Active Directory 도메인에 가입\-되지 않은 관리 클라이언트에 대해 인증서 기반 인증에 대해 X509를 사용 합니다. 모든 네트워크 컨트롤러 클러스터 노드 및 관리 클라이언트에 인증서를 등록 해야 합니다. 또한 모든 노드 및 관리 클라이언트는 다른 사람의 인증서를 신뢰 해야 합니다.

3. **없음**. 테스트 환경에서 테스트 목적으로는 None을 사용 하 고 따라서 프로덕션 환경에서는 사용 하지 않는 것이 좋습니다. 이 모드를 선택 하면 노드와 관리 클라이언트 간에 인증이 수행 되지 않습니다.

_Clientauthentication_ 매개 변수와 함께 Windows PowerShell 명령 **[NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** 를 사용 하 여 Northbound 통신에 대 한 인증 모드를 구성할 수 있습니다. 


### <a name="authorization"></a>Authorization

네트워크 컨트롤러 Northbound 통신에 대 한 권한 부여를 구성 하는 경우 네트워크 컨트롤러 클러스터 노드 및 관리 클라이언트에서 통신 하는 데 사용 되는 장치가 신뢰할 수 있고에 참여할 권한이 있는지 확인할 수 있습니다. 통신이.

네트워크 컨트롤러에서 지원 되는 각 인증 모드에 대해 다음과 같은 권한 부여 방법을 사용 합니다.

1.  **Kerberos**. Kerberos 인증 방법을 사용 하는 경우 Active Directory에 보안 그룹을 만든 다음 권한 있는 사용자 및 컴퓨터를 그룹에 추가 하 여 네트워크 컨트롤러와 통신할 수 있는 사용자 및 컴퓨터를 정의 합니다. **[NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** Windows PowerShell 명령의 _clientsecuritygroup_ 매개 변수를 사용 하 여 보안 그룹을 권한 부여에 사용 하도록 네트워크 컨트롤러를 구성할 수 있습니다. 네트워크 컨트롤러를 설치한 후에는 **[NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** 명령을 매개 변수 _-clientsecuritygroup_과 함께 사용 하 여 보안 그룹을 변경할 수 있습니다. SCVMM을 사용 하는 경우 배포 하는 동안 보안 그룹을 매개 변수로 제공 해야 합니다.

2.  **X509**. X509 인증 방법을 사용 하는 경우 네트워크 컨트롤러는 인증서 지문을 네트워크 컨트롤러에 알고 있는 관리 클라이언트의 요청만 수락 합니다. **[NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** Windows PowerShell 명령의 _clientcertificatethumbprint_ 매개 변수를 사용 하 여 이러한 지문을 구성할 수 있습니다. **[NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** 명령을 사용 하 여 언제 든 지 다른 클라이언트 지문을 추가할 수 있습니다.

3.  **없음**. 이 모드를 선택 하면 노드와 관리 클라이언트 간에 인증이 수행 되지 않습니다. 테스트 환경에서 테스트 목적으로는 None을 사용 하 고 따라서 프로덕션 환경에서는 사용 하지 않는 것이 좋습니다. 


### <a name="encryption"></a>암호화

Northbound 통신은 SSL(Secure Sockets Layer) \(SSL\) 을 사용 하 여 관리 클라이언트와 네트워크 컨트롤러 노드 간에 암호화 된 채널을 만듭니다. Northbound 통신을 위한 SSL 암호화에는 다음 요구 사항이 포함 됩니다.

- 모든 네트워크 컨트롤러 노드에는 향상 된 키 사용 \(EKU\) 확장의 서버 인증 및 클라이언트 인증 목적을 포함 하는 동일한 인증서가 있어야 합니다. 

- 관리 클라이언트에서 네트워크 컨트롤러와 통신 하는 데 사용 하는 URI는 인증서 주체 이름 이어야 합니다. 인증서 주체 이름에는 네트워크 컨트롤러 REST 끝점의 FQDN (정규화 된 도메인 이름) 또는 IP 주소를 포함 해야 합니다.

- 네트워크 컨트롤러 노드가 서로 다른 서브넷에 있는 경우 해당 인증서의 주체 이름은 **NetworkController** Windows PowerShell 명령에서 _RestName_ 매개 변수에 사용 되는 값과 동일 해야 합니다. 

- 모든 관리 클라이언트는 SSL 인증서를 신뢰 해야 합니다.


### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL 인증서 등록 및 구성

SSL 인증서는 네트워크 컨트롤러 노드에 수동으로 등록 해야 합니다.

인증서를 등록 한 후에는 **NetworkController** Windows PowerShell 명령의 **-servercertificate** 매개 변수와 함께 인증서를 사용 하도록 네트워크 컨트롤러를 구성할 수 있습니다. 네트워크 컨트롤러를 이미 설치한 경우 **NetworkController** 명령을 사용 하 여 언제 든 지 구성을 업데이트할 수 있습니다.

>[!NOTE]
>SCVMM을 사용 하는 경우 인증서를 라이브러리 리소스로 추가 해야 합니다. 자세한 내용은 [VMM 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)을 참조 하세요.

## <a name="network-controller-cluster-communication"></a>네트워크 컨트롤러 클러스터 통신

네트워크 컨트롤러는 네트워크 컨트롤러 노드 간 통신에 대 한 인증, 권한 부여 및 암호화를 지원 합니다. 통신은 [Windows Communication Foundation](https://msdn.microsoft.com/library/ms731082.aspx) \(WCF\) 및 TCP를 통해 전달 됩니다.

**NetworkControllerCluster** Windows PowerShell 명령의 **clusterauthentication** 매개 변수를 사용 하 여이 모드를 구성할 수 있습니다. 

자세한 내용은 [NetworkControllerCluster](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontrollercluster)를 참조 하세요.

### <a name="authentication"></a>인증

네트워크 컨트롤러 클러스터 통신에 대 한 인증을 구성 하는 경우 네트워크 컨트롤러 클러스터 노드에서 통신할 다른 노드의 id를 확인할 수 있습니다.

네트워크 컨트롤러는 네트워크 컨트롤러 노드 간에 다음과 같은 세 가지 인증 모드를 지원 합니다.

>[!NOTE]
>SCVMM을 사용 하 여 네트워크 컨트롤러를 배포 하는 경우에는 **Kerberos** 모드만 지원 됩니다.

1. **Kerberos**. 모든 네트워크 컨트롤러 클러스터 노드가 인증에 사용 되는 도메인 계정을 사용 하 여 Active Directory 도메인에 가입 되어 있는 경우 Kerberos 인증을 사용할 수 있습니다.

2. **X509**. X509는 인증서\-기반 인증입니다. 네트워크 컨트롤러 클러스터 노드가 Active Directory 도메인에 가입 되지 않은 경우 X509 인증을 사용할 수 있습니다. X509를 사용 하려면 모든 네트워크 컨트롤러 클러스터 노드에 인증서를 등록 해야 하며 모든 노드는 인증서를 신뢰 해야 합니다. 또한 각 노드에 등록 된 인증서의 주체 이름은 노드의 DNS 이름과 동일 해야 합니다.

3. **없음**. 이 모드를 선택 하면 네트워크 컨트롤러 노드 간에 인증이 수행 되지 않습니다. 이 모드는 테스트 목적 으로만 제공 되며 프로덕션 환경에서 사용 하지 않는 것이 좋습니다.

### <a name="authorization"></a>Authorization

네트워크 컨트롤러 클러스터 통신에 대 한 권한 부여를 구성 하는 경우 네트워크 컨트롤러 클러스터 노드에서 통신 중인 노드가 신뢰 되 고 통신에 참여할 수 있는 권한이 있는지 확인할 수 있습니다.

네트워크 컨트롤러에서 지원 되는 각 인증 모드에 대해 다음과 같은 권한 부여 방법이 사용 됩니다.

1. **Kerberos**. 네트워크 컨트롤러 노드는 다른 네트워크 컨트롤러 컴퓨터 계정의 통신 요청만 수락 합니다. [NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell 명령의 **Name** 매개 변수를 사용 하 여 네트워크 컨트롤러를 배포할 때 이러한 계정을 구성할 수 있습니다.

2. **X509**. 네트워크 컨트롤러 노드는 다른 네트워크 컨트롤러 컴퓨터 계정의 통신 요청만 수락 합니다. [NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell 명령의 **Name** 매개 변수를 사용 하 여 네트워크 컨트롤러를 배포할 때 이러한 계정을 구성할 수 있습니다.

3. **없음**. 이 모드를 선택 하면 네트워크 컨트롤러 노드 간에 권한 부여가 수행 되지 않습니다. 이 모드는 테스트 목적 으로만 제공 되며 프로덕션 환경에서 사용 하지 않는 것이 좋습니다.

### <a name="encryption"></a>암호화

네트워크 컨트롤러 노드 간 통신은 WCF 전송 수준 암호화를 사용 하 여 암호화 됩니다. 이러한 형태의 암호화는 인증 및 권한 부여 방법이 Kerberos 또는 X509 인증서 일 때 사용 됩니다. 자세한 내용은 다음 항목을 참조하세요.

- [방법: Windows 자격 증명을 사용 하 여 서비스 보호](https://msdn.microsoft.com/library/ms734673.aspx)
- [방법: X.509 인증서](https://msdn.microsoft.com/library/ms788968.aspx)를 사용 하 여 서비스를 보호 합니다.

## <a name="southbound-communication"></a>Southbound 통신

네트워크 컨트롤러는 Southbound 통신을 위해 다양 한 유형의 장치와 상호 작용 합니다. 이러한 상호 작용에는 서로 다른 프로토콜이 사용 됩니다. 이로 인해 네트워크 컨트롤러에서 장치와 통신 하는 데 사용 하는 장치 및 프로토콜 유형에 따라 인증, 권한 부여 및 암호화에 대 한 요구 사항이 다릅니다.

다음 표에서는 다양 한 southbound 장치와의 네트워크 컨트롤러 상호 작용에 대 한 정보를 제공 합니다.

| Southbound 장치/서비스 | 프로토콜              | 사용 되는 인증    |
|---------------------------|-----------------------|------------------------|
| 소프트웨어 부하 분산 장치    | WCF (MUX), TCP (호스트) | 인증서           |
| 방화벽                  | OVSDB                 | 인증서           |
| 게이트웨이                   | WinRM                 | Kerberos, 인증서 |
| 가상 네트워킹        | OVSDB, WCF            | 인증서           |
| 사용자 정의 라우팅      | OVSDB                 | 인증서           |

이러한 각 프로토콜에 대 한 통신 메커니즘은 다음 섹션에 설명 되어 있습니다.

### <a name="authentication"></a>인증

Southbound 통신의 경우 다음 프로토콜과 인증 방법이 사용 됩니다.

1. **WCF/TCP/OVSDB**. 이러한 프로토콜의 경우 인증은 X509 인증서를 사용 하 여 수행 됩니다. 네트워크 컨트롤러와 피어 소프트웨어 부하 \(분산 SLB\) 멀티플렉서 \(MUX\)/host 컴퓨터는 상호 인증을 위해 인증서를 서로 표시 합니다. 각 인증서는 원격 피어에서 신뢰 해야 합니다.

    Southbound 인증의 경우 Northbound 클라이언트와의 통신을 암호화 하도록 구성 된 동일한 SSL 인증서를 사용할 수 있습니다. 또한 SLB MUX 및 호스트 장치에서 인증서를 구성 해야 합니다. 인증서 주체 이름은 장치의 DNS 이름과 동일 해야 합니다.

2. **WinRM**. 이 프로토콜의 경우 도메인 \(에 가입 된 컴퓨터\) 의 경우 Kerberos를 사용 하 고 도메인에 \(가입 되지 않은 컴퓨터\)에는 인증서를 사용 하 여 인증을 수행 합니다.

### <a name="authorization"></a>Authorization

Southbound 통신의 경우 다음 프로토콜과 권한 부여 방법이 사용 됩니다.

1. **WCF/TCP**. 이러한 프로토콜의 경우 권한 부여는 피어 엔터티의 주체 이름을 기반으로 합니다. 네트워크 컨트롤러는 피어 장치 DNS 이름을 저장 하 고 권한을 부여 하는 데 사용 합니다. 이 DNS 이름은 인증서에 있는 장치의 주체 이름과 일치 해야 합니다. 마찬가지로, 네트워크 컨트롤러 인증서는 피어 장치에 저장 된 네트워크 컨트롤러 DNS 이름과 일치 해야 합니다.

2. **WinRM**. Kerberos를 사용 하는 경우 WinRM 클라이언트 계정은 Active Directory의 미리 정의 된 그룹 또는 서버의 로컬 관리자 그룹에 있어야 합니다. 인증서를 사용 하는 경우 클라이언트는 서버에 주체 이름/발급자를 사용 하 여 권한을 부여 하는 인증서를 서버에 제공 하 고, 서버는 매핑된 사용자 계정을 사용 하 여 인증을 수행 합니다.

3.  **OVSDB**. 이 프로토콜에 대해 제공 된 권한 부여가 없습니다.

### <a name="encryption"></a>암호화

Southbound 통신의 경우 프로토콜에 대해 다음과 같은 암호화 방법이 사용 됩니다.

1. **WCF/TCP/OVSDB**. 이러한 프로토콜의 경우 클라이언트 또는 서버에 등록 된 인증서를 사용 하 여 암호화를 수행 합니다.

2. **WinRM**. WinRM 트래픽은 Kerberos security support provider \(SSP\)를 사용 하 여 기본적으로 암호화 됩니다. WinRM 서버에서 SSL 형식의 추가 암호화를 구성할 수 있습니다.
