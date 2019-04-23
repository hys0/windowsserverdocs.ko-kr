---
title: 네트워크 컨트롤러 보안
description: 네트워크 컨트롤러 및 기타 소프트웨어와 장치 간의 모든 통신에 대 한 보안을 구성 하는 방법을 알아보려면이 항목에서는 사용할 수 있습니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: fccd6ee1ba734d72629264bd5b3bb7d93ddcdb70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884764"
---
# <a name="secure-the-network-controller"></a>네트워크 컨트롤러 보안

이 항목에서는 보안 간의 모든 통신을 구성 하는 방법을 알아봅니다 [네트워크 컨트롤러](../technologies/network-controller/network-controller.md) 기타 소프트웨어 및 장치입니다. 

보호할 수 있는 통신 경로 포함 관리 평면에서 클러스터 통신 네트워크 컨트롤러 가상 컴퓨터의 Northbound 통신 \(Vm\) 클러스터 및 데이터의 Southbound 통신 평면입니다.

1. **Northbound 통신**합니다. 네트워크 컨트롤러가 SDN 사용 하 여 관리 평면에서 통신\-Windows PowerShell 및 System Center Virtual Machine Manager 같은 가능한 관리 소프트웨어 \(SCVMM\)합니다. 이러한 관리 도구는 네트워크 정책을 정의 하 고는 실제 구성이 패리티 목표 상태와 실제 네트워크 구성을 비교할 수 있습니다 네트워크에 대 한 목표 상태를 만들 수 있는 기능을 사용 하 여 제공 합니다.

2. **네트워크 컨트롤러 클러스터 통신**합니다. 네트워크 컨트롤러 클러스터 노드와 3 개 이상의 Vm을 구성한 경우 이러한 노드가 서로 통신 합니다. 이 통신 관련이 있을 수 동기화 및 데이터 복제는 노드 또는 네트워크 컨트롤러 서비스 간의 특정 통신 합니다.

3.  **Southbound 통신**합니다. 네트워크 컨트롤러가 SDN 인프라 및 소프트웨어 부하 분산 장치, 게이트웨이 및 호스트 컴퓨터와 같은 기타 장치를 사용 하 여 데이터 평면에서 통신합니다. 구성 하 고가 네트워크에 대해 구성한 목표 상태를 유지할 수 있도록 이러한 southbound 장치를 관리할 네트워크 컨트롤러를 사용할 수 있습니다.


## <a name="northbound-communication"></a>Northbound 통신

네트워크 컨트롤러 Northbound 통신에 대 한 인증, 권한 부여 및 암호화를 지원합니다. 다음 섹션에서는 이러한 보안 설정을 구성 하는 방법에 정보를 제공 합니다.

### <a name="authentication"></a>인증

네트워크 컨트롤러 Northbound 통신에 대 한 인증을 구성할 때 네트워크 컨트롤러 클러스터 노드 및 관리 클라이언트는 통신 하는 장치 id를 확인 하는 것이 수 있습니다.

네트워크 컨트롤러 관리 클라이언트 및 네트워크 컨트롤러 노드 간의 인증의 다음 세 가지 모드를 지원합니다.

>[!Note]
>배포 하는 경우 네트워크 컨트롤러와 System Center Virtual Machine Manager만 **Kerberos** 모드가 지원 됩니다.

1. **Kerberos**합니다. 관리 클라이언트와 모든 네트워크 컨트롤러 클러스터 노드는 Active Directory 도메인에 가입 하는 경우 Kerberos 인증을 사용 합니다. Active Directory 도메인에는 인증에 사용 되는 도메인 계정이 있어야 합니다.

2. **X509**. X509 인증서에 대 한 사용\-Active Directory 도메인에 가입 되지 관리 클라이언트에 대 한 인증을 기반으로 합니다. 모든 네트워크 컨트롤러 클러스터 노드 및 관리 클라이언트 인증서를 등록 해야 합니다. 또한 모든 노드 및 관리 클라이언트는 다른 사용자 인증서를 신뢰 해야 합니다.

3. **없음**. 프로덕션 환경에서 사용 하 여 사용 None 테스트용 테스트 환경의 목적 및, 따라서 권장 되지 않습니다. 이 모드를 선택 하면 인증이 관리 클라이언트 및 노드 간 수행 되지 않습니다.

Windows PowerShell 명령을 사용 하 여 Northbound 통신에 대 한 인증 모드를 구성할 수 있습니다 **[설치 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** 사용 하 여는 _ClientAuthentication_ 매개 변수입니다. 


### <a name="authorization"></a>Authorization

네트워크 컨트롤러 클러스터 노드와 통신 하는 장치는 신뢰할 수 있는 되었고 참여할 수 있는 권한이 있는지 확인 하려면 관리 클라이언트를 허용 하는 네트워크 컨트롤러 Northbound 통신에 대 한 권한 부여를 구성 합니다 통신 합니다.

각 네트워크 컨트롤러에서 지원 되는 인증 모드에 대 한 다음 권한 부여 메서드를 사용 합니다.

1.  **Kerberos**합니다. Kerberos 인증 메서드를 사용 하는 사용자 및 Active Directory에서 보안 그룹을 만들면 다음 그룹에 권한 있는 사용자 및 컴퓨터를 추가 하 여 네트워크 컨트롤러와 통신할 수 있도록 허가 하는 컴퓨터를 정의 합니다. 네트워크 컨트롤러를 사용 하 여 권한 부여에 대 한 보안 그룹을 사용 하도록 구성할 수 있습니다 합니다 _ClientSecurityGroup_ 의 매개 변수를 **[설치 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** Windows PowerShell 명령입니다. 네트워크 컨트롤러를 설치한 후 사용 하 여 보안 그룹을 변경할 수 있습니다 합니다 **[집합 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** 매개 변수와 함께 명령을 _-ClientSecurityGroup_ . SCVMM을 사용 하는 경우 배포 중 보안 그룹을 매개 변수로 제공 해야 합니다.

2.  **X509**. X509를 사용 하는 경우 인증 방법으로 네트워크 컨트롤러를 네트워크 컨트롤러 인증서 지문 인 알려져 관리 클라이언트의 요청만 허용 합니다. 이 지문을 사용 하 여 구성할 수 있습니다 합니다 _ClientCertificateThumbprint_ 의 매개 변수를 **[설치 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)** Windows PowerShell 명령입니다. 사용 하 여 다른 클라이언트 지문 언제 든 지 추가할 수 있습니다 합니다 **[집합 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)** 명령입니다.

3.  **없음**. 이 모드를 선택 하면 인증이 관리 클라이언트 및 노드 간 수행 되지 않습니다. 프로덕션 환경에서 사용 하 여 사용 None 테스트용 테스트 환경의 목적 및, 따라서 권장 되지 않습니다. 


### <a name="encryption"></a>암호화

Northbound 통신에서는 Secure Sockets Layer \(SSL\) 관리 클라이언트 및 네트워크 컨트롤러 노드 간에 암호화 된 채널을 만들려고 합니다. Northbound 통신에 대 한 SSL 암호화에는 다음 요구 사항을 포함 됩니다.

- 모든 네트워크 컨트롤러 노드 서버 인증과 클라이언트 인증 용도로 확장 된 키 사용에 포함 된 동일한 인증서가 있어야 \(EKU\) 확장 합니다. 

- 네트워크 컨트롤러와 통신할 관리 클라이언트에서 사용 된 URI에는 인증서 주체 이름 이어야 합니다. 인증서 주체 이름은 네트워크 컨트롤러 REST 끝점의 IP 주소 또는 정규화 된 도메인 이름 (FQDN)을 포함 해야 합니다.

- 네트워크 컨트롤러 노드는 서로 다른 서브넷에 있는 경우 해당 인증서의 주체 이름이 같아야에 사용 된 값으로는 _RestName_ 에 매개 변수를 **설치 NetworkController** Windows PowerShell 명령입니다. 

- 모든 관리 클라이언트 SSL 인증서를 신뢰 해야 합니다.


### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL 인증서 등록 및 구성

네트워크 컨트롤러 노드에 SSL 인증서를 수동으로 등록 해야 합니다.

인증서를 등록 한 후 사용 하 여 인증서를 사용 하 여 네트워크 컨트롤러를 구성할 수 있습니다 합니다 **-ServerCertificate** 의 매개 변수를 **설치 NetworkController** Windows PowerShell 명령 . 네트워크 컨트롤러를 이미 설치한 경우에 사용 하 여 언제 든 지 구성을 업데이트할 수 있습니다 합니다 **집합 NetworkController** 명령입니다.

>[!NOTE]
>SCVMM을 사용 하는 경우에 라이브러리 리소스와 인증서를 추가 해야 합니다. 자세한 내용은 [VMM 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)합니다.

## <a name="network-controller-cluster-communication"></a>네트워크 컨트롤러 클러스터 통신

네트워크 컨트롤러 네트워크 컨트롤러 노드 간의 통신에 대 한 인증, 권한 부여 및 암호화를 지원합니다. 통신 스타일러스가 [Windows Communication Foundation](https://msdn.microsoft.com/library/ms731082.aspx) \(WCF\) 및 TCP입니다.

이 모드를 구성할 수 있습니다 합니다 **ClusterAuthentication** 의 매개 변수를 **설치 NetworkControllerCluster** Windows PowerShell 명령입니다. 

자세한 내용은 [설치 NetworkControllerCluster](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontrollercluster)합니다.

### <a name="authentication"></a>인증

네트워크 컨트롤러 클러스터 통신에 대 한 인증을 구성할 때 네트워크 컨트롤러 클러스터 노드 통신 하 고 있는 다른 노드의 id를 확인할 수 있습니다.

네트워크 컨트롤러 네트워크 컨트롤러 노드 간의 인증의 다음 세 가지 모드를 지원합니다.

>[!NOTE]
>SCVMM에만 사용 하 여 네트워크 컨트롤러를 배포 하는 경우 **Kerberos** 모드가 지원 됩니다.

1. **Kerberos**합니다. 인증에 사용 되는 도메인 계정을 사용 하 여 모든 네트워크 컨트롤러 클러스터 노드를 Active Directory 도메인에 가입 된 경우 Kerberos 인증을 사용할 수 있습니다.

2. **X509**. X509 인증서가\-기반 인증 합니다. 네트워크 컨트롤러 클러스터 노드 때 인증을 Active Directory 도메인에 가입 하지 않은 X509를 사용할 수 있습니다. X509를 사용 하려면 모든 네트워크 컨트롤러 클러스터 노드에 인증서를 등록 해야 하 고 모든 노드에 인증서를 신뢰 해야 합니다. 또한 각 노드에서 등록 된 인증서의 주체 이름 노드의 DNS 이름으로 동일한 이어야 합니다.

3. **없음**. 이 모드를 선택 하면 인증이 네트워크 컨트롤러 노드 사이 수행 되지 않습니다. 이 모드는 테스트 목적을 위해서만 제공 됩니다 및 프로덕션 환경에서 용도로 권장 되지 않습니다.

### <a name="authorization"></a>Authorization

네트워크 컨트롤러 클러스터 통신에 대 한 권한 부여를 구성할 때 네트워크 컨트롤러 클러스터 노드 통신 하는 노드는 신뢰할 수 있도록 확인 하 고 통신에 참여할 수 있는 권한이를 수 있습니다.

각 네트워크 컨트롤러에서 지원 되는 인증 모드에 대해 다음 권한 부여 방법 사용 됩니다.

1. **Kerberos**합니다. 네트워크 컨트롤러 노드는 다른 네트워크 컨트롤러 컴퓨터 계정 에서만에서 통신 요청을 수락합니다. 사용 하 여 네트워크 컨트롤러를 배포할 때 이러한 계정을 구성할 수 있습니다는 **이름을** 의 매개 변수를 [새로 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell 명령입니다.

2. **X509**. 네트워크 컨트롤러 노드는 다른 네트워크 컨트롤러 컴퓨터 계정 에서만에서 통신 요청을 수락합니다. 사용 하 여 네트워크 컨트롤러를 배포할 때 이러한 계정을 구성할 수 있습니다는 **이름을** 의 매개 변수를 [새로 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell 명령입니다.

3. **없음**. 이 모드를 선택한 경우 네트워크 컨트롤러 노드 사이 수행 하는 권한이 부여 되지 않습니다. 이 모드는 테스트 목적을 위해서만 제공 됩니다 및 프로덕션 환경에서 용도로 권장 되지 않습니다.

### <a name="encryption"></a>암호화

네트워크 컨트롤러 노드 간의 통신은 WCF 전송 수준 암호화를 사용 하 여 암호화 됩니다. 인증 및 권한 부여 방법이 Kerberos 또는 X509 때 이러한 형태의 암호화는 인증서입니다. 자세한 내용은 다음 항목을 참조하세요.

- [방법: Windows 자격 증명을 사용 하 여 서비스에 보안 설정](https://msdn.microsoft.com/library/ms734673.aspx)
- [방법: X.509 인증서를 사용 하 여 서비스를 보호](https://msdn.microsoft.com/library/ms788968.aspx)합니다.

## <a name="southbound-communication"></a>Southbound 통신

네트워크 컨트롤러 Southbound 통신에 대 한 장치 유형 마다 상호 작용합니다. 다른 프로토콜을 사용 하는 이러한 상호 작용 합니다. 이 인해 인증, 권한 부여 및 암호화 장치 및 네트워크 컨트롤러에서 장치와 통신에 사용 되는 프로토콜의 유형에 따라 다른 요구 사항이 있습니다.

다음 표에서 다양 한 southbound 장치를 사용 하 여 네트워크 컨트롤러의 상호 작용에 대 한 정보를 제공합니다.

| Southbound 장치/서비스 | 프로토콜              | 사용 되는 인증    |
|---------------------------|-----------------------|------------------------|
| 소프트웨어 부하 분산 장치    | WCF (MUX) TCP (호스트) | 인증서           |
| 방화벽                  | OVSDB                 | 인증서           |
| 게이트웨이                   | WinRM                 | Kerberos, 인증서 |
| 가상 네트워킹        | OVSDB, WCF            | 인증서           |
| 사용자 정의 라우팅      | OVSDB                 | 인증서           |

이러한 각 프로토콜에 대 한 통신 메커니즘은 다음 섹션에 설명 되어 있습니다.

### <a name="authentication"></a>인증

Southbound 통신에 대 한 프로토콜 및 인증 메서드를 사용 합니다.

1. **WCF/TCP/OVSDB**. 이러한 프로토콜에 대 한 인증 X509를 사용 하 여 수행 됩니다 인증서입니다. 네트워크 컨트롤러 및 소프트웨어 부하 분산 피어 \(SLB\) 멀티플렉서 \(MUX \) /호스트 컴퓨터 간의 상호 인증에 대 한 해당 인증서를 제공 합니다. 원격 피어가 각 인증서를 신뢰 해야 합니다.

    Southbound 인증용 클라이언트와의 Northbound 통신을 암호화 하는 것에 대 한 구성 된 동일한 SSL 인증서를 사용할 수 있습니다. 또한 SLB MUX 및 호스트 장치에 인증서를 구성 해야 합니다. 인증서 주체 이름의 장치의 DNS 이름과 동일 해야 합니다.

2. **WinRM**. 이 프로토콜에 대 한 Kerberos를 사용 하 여 인증을 수행 \(도메인에 가입 된 컴퓨터\) 인증서를 사용 하 여 \(비-도메인 조인 컴퓨터\)합니다.

### <a name="authorization"></a>Authorization

Southbound 통신에 대 한 프로토콜 및 권한 부여 메서드를 사용 합니다.

1. **WCF/TCP**. 이러한 프로토콜에 대 한 권한 부여는 주체 이름을 피어 엔터티를 기반으로 합니다. 네트워크 컨트롤러 피어 장치 DNS 이름, 저장 및 권한 부여를 위해 사용 합니다. 이 DNS 이름에는 장치에 인증서의 주체 이름을 일치 해야 합니다. 마찬가지로, 네트워크 컨트롤러 인증서 피어 장치에 저장 된 네트워크 컨트롤러의 DNS 이름과 일치 해야 합니다.

2. **WinRM**. Kerberos를 사용 하는 경우 WinRM 클라이언트 계정 서버의 로컬 관리자 그룹 또는 Active Directory에 미리 정의 된 그룹에 있어야 합니다. 인증서를 사용 하는 경우 클라이언트 인증서 주체 이름/발급자를 사용 하 여 서버에 권한을 부여 하는 서버 인증을 수행 하도록 매핑된 사용자 계정을 사용 하는 서버를 표시 합니다.

3.  **OVSDB**. 이 프로토콜에 대해 제공 하는 권한이 부여 되지 않습니다.

### <a name="encryption"></a>암호화

Southbound 통신 프로토콜에 대 한 다음 암호화 방법 사용 됩니다.

1. **WCF/TCP/OVSDB**. 이러한 프로토콜에 대 한 암호화는 클라이언트 또는 서버에 등록 된 인증서를 사용 하 여 수행 됩니다.

2. **WinRM**. Kerberos 보안 지원 공급자를 사용 하 여 기본적으로 WinRM 트래픽이 암호화 됩니다 \(SSP\)합니다. WinRM 서버의 SSL의 형태로 추가 암호화를 구성할 수 있습니다.
