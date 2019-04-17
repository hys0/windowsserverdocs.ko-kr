---
title: 네트워크 컨트롤러 보안
description: 네트워크 컨트롤러 및 기타 소프트웨어 및 디바이스 간에 모든 통신에 대 한 보안을 구성 하는 방법을 알아보려면이 항목을 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: bc625de9-ee31-40a4-9ad2-7448bfbfb6e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ab04d3f528beb037988e6390fe85ad9af219266b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="network-controller-security"></a>네트워크 컨트롤러 보안

네트워크 컨트롤러 및 기타 소프트웨어 및 디바이스 간에 모든 통신에 대 한 보안을 구성 하는 방법을 알아보려면이 항목을 사용할 수 있습니다. 

>[!NOTE]
>네트워크 컨트롤러 개요를 참조 하세요. [네트워크 컨트롤러](../technologies/network-controller/network-controller.md)합니다.

통신 경로 보호할 수 있는 관리 평면 클러스터에서 가상 컴퓨터 \(VMs\) 네트워크 컨트롤러 및 데이터 평면 Southbound 통신 간 통신 클러스터에 Northbound 통신을 포함 합니다.

1. **Northbound 통신**합니다. 네트워크 컨트롤러와 같은 Windows PowerShell 및 System Center 가상 컴퓨터 Manager \(SCVMM\) SDN\ 가능 관리 소프트웨어와 함께 관리 평면 통신합니다. 이러한 관리 도구 네트워크 정책이 정의 하 고 하는 실제 구성을 목표 상태와 패리티도 상태로 실제 네트워크 구성 비교할 수 네트워크에 대 한 목표 상태를 만들려면 기능이 제공 됩니다.

2. **네트워크 컨트롤러 클러스터 통신**합니다. 3 개 이상의 Vm 클러스터 노드가 네트워크 컨트롤러와를 구성할 때 이러한 노드 서로 통신할 합니다. 이 통신 노드 또는 네트워크 컨트롤러 서비스 간의 특정 통신 간에 동기화 하 고 데이터를 복제 하 관련 수 있습니다.

3.  **Southbound 통신**합니다. 네트워크 컨트롤러 SDN 인프라 부하 분산 소프트웨어가, 게이트웨이, 호스트 컴퓨터와 같은 다른 디바이스와 데이터 평면 통신합니다. 네트워크 컨트롤러 구성 하 고 네트워크에 대 한 구성 된 목표 상태를 유지 하 않도록 이러한 southbound 디바이스 관리에 사용할 수 있습니다.

## <a name="northbound-communication"></a>Northbound 커뮤니케이션

네트워크 컨트롤러 Northbound 통신 인증, 권한 및 암호화를 지원합니다. 다음 섹션에서는 이러한 보안 설정을 구성 하는 방법에 대해 설명 합니다.

**인증**

네트워크 컨트롤러 Northbound 통신에 대 한 인증을 구성할 때 클러스터 노드가 네트워크 컨트롤러와 통신 하는 디바이스의 id 확인을 위해 관리 클라이언트 허용 합니다.

네트워크 컨트롤러 관리 클라이언트 노드가 네트워크 컨트롤러와 인증 다음 세 가지 모드를 지원합니다.

>[!Note]
>배포 하는 경우 네트워크 컨트롤러 System Center 가상 컴퓨터 Manager와만 **Kerberos** 모드 지원 됩니다.

1. **Kerberos**합니다. 모두 관리를 같은 클라이언트 SCVMM 및 모든 네트워크 컨트롤러 클러스터 노드가 실행 하는 컴퓨터 도메인 계정 인증에 사용 된 Active Directory 도메인에 가입한 Kerberos 인증을 사용할 수 있습니다.

2. **X509**합니다. X509는 certificate\ 기반 인증입니다. X509 사용할 수 있는 관리 하는 클라이언트 Active Directory 도메인에 가입 하지 않은 경우 인증 합니다. X509를 사용 하려면 인증서 모든 클러스터 노드가 네트워크 컨트롤러 및 관리 클라이언트를 등록 해야 및 노드 및 관리 하는 클라이언트 서로의 인증서 신뢰 해야 합니다.

3. **없음**합니다. 이 모드를 선택 하면 인증이 관리 클라이언트 네트워크 컨트롤러와 수행 되지 않습니다. 이 모드 테스트 목적을 위해서만 제공 됩니다 및 생산 환경에서 사용할 수 있도록 권장 되지 않습니다. 

Windows PowerShell 명령을 사용 하 여 Northbound 통신을 위해 인증 모드 구성할 수 있습니다 **설치 NetworkController** 와 **ClientAuthentication** 매개 합니다. 

자세한 내용은 다음 항목을 참조 합니다. 

- [설치 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)
- [설정 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)

**인증**

네트워크 컨트롤러 Northbound 통신에 대 한 권한을 구성할 때 클러스터 노드가 네트워크 컨트롤러와 통신 하는 디바이스를 신뢰할 수 있는 및 통신에 참여할 수 있는 권한이 확인 하려면 관리 클라이언트 허용 합니다.

네트워크 컨트롤러에서 지원 되는 인증 모드 각 다음 인증 방법은 사용 됩니다.

1.  **Kerberos**합니다. Kerberos 인증 방법을 사용 하는 경우 사용자와 Active Directory에 보안 그룹을 만들고 다음 권한이 있는 사용자와 컴퓨터 그룹에 추가 하 여 네트워크 컨트롤러와 통신 하도록 실시 권 자는 컴퓨터 정의 합니다. 그룹을 사용 하는 보안 인증을 위해 사용 하 여 네트워크 컨트롤러 구성할 수 있습니다는 **ClientSecurityGroup** 매개는 **설치 NetworkController** Windows PowerShell 명령을 합니다. 네트워크 컨트롤러를 설치한 후 보안 그룹을 사용 하 여 변경할 수 있습니다는 [설정 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller) 매개 명령 **-ClientSecurityGroup**합니다. SCVMM를 사용 하는 경우 배포 하는 동안 매개도 보안 그룹을 제공 해야 합니다.

2.  **X509**합니다. X509를 사용 하는 경우 인증 방법인 네트워크 컨트롤러만의 요청을 수락 관리 클라이언트 네트워크 컨트롤러도 인증서 지문을 볼 알려져 있습니다. 사용 하 여 이러한 지문을 구성할 수 있습니다는 **ClientCertificateThumbprint** 매개는 **설치 NetworkController** Windows PowerShell 명령을 합니다. 사용 하 여 언제 든 지 다른 클라이언트 지문을 추가할 수는 **설정 NetworkController** 명령 합니다.

3.  **없음**합니다. 이 모드를 선택할 때 관리 클라이언트 노드가 네트워크 컨트롤러와 통신 시도 대해 수행 인증 합니다. 이 모드 테스트 목적을 위해서만 제공 됩니다 및 생산 환경에서 사용할 수 있도록 권장 되지 않습니다. 

자세한 내용은 다음 항목을 참조 합니다. 

- [설치 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontroller)
- [설정 NetworkController](https://technet.microsoft.com/itpro/powershell/windows/network-controller/set-networkcontroller)

**암호화**

Northbound 통신 \(SSL\) 주소를 사용 하 여 관리 클라이언트 노드가 네트워크 컨트롤러와 암호화 된 채널을 만듭니다. Northbound 통신에 대 한 암호화 SSL 다음 요구 사항을 포함합니다.

- 모든 네트워크 컨트롤러 노드 키 사용 향상 \(EKU\) 확장에서 서버 인증와 클라이언트 인증 목적을 포함 하는 동일한 인증서가 있어야 합니다. 

- 네트워크 컨트롤러와 통신 하도록 관리 하는 클라이언트에서 사용 하는 URI 인증서 제목 있어야 합니다. 인증서 제목 적격은 도메인 이름 (FQDN) 또는 네트워크 컨트롤러 나머지 Endpoint의 IP 주소를 포함 해야 합니다.

- 해당 인증서의 제목 이름은 가치에 대 한 사용 하는 것과 동일한 해야 노드가 네트워크 컨트롤러, 다른에 있는 경우는 **RestName** 매개는 **설치 NetworkController** Windows PowerShell 명령을 합니다. 

- 모두 관리 클라이언트 ssl 신뢰할 수 있어야 합니다.

### <a name="ssl-certificate-enrollment-and-configuration"></a>SSL 인증서 등록이 및 구성

네트워크 컨트롤러 노드에서 SSL 인증서 수동으로 등록 해야 합니다.

인증서가 등록 한 후 네트워크 컨트롤러와 인증서를 사용 하도록 구성할 수 있습니다의 **-못했기** 매개는 **설치 NetworkController** Windows PowerShell 명령을 합니다. 네트워크 컨트롤러, 이미 설치한 경우 언제 든 지 구성을 사용 하 여 업데이트할 수 있습니다는 **설정 NetworkController** 명령을 합니다.

>[!NOTE]
>SCVMM를 사용 하는 경우 라이브러리 리소스 인증서를 추가 해야 합니다. 자세한 내용은 참조 [VMM 패브릭에서 SDN 네트워크 컨트롤러 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-network-controller)합니다.

## <a name="network-controller-cluster-communication"></a>네트워크 컨트롤러 클러스터 통신

네트워크 컨트롤러 네트워크 컨트롤러 노드 간 통신에 대 한 인증, 권한 및 암호화를 지원합니다. 통신 끝났습니다 [사항](https://msdn.microsoft.com/library/ms731082.aspx) \(WCF\) 및 TCP 합니다.

이 모드를 구성할 수 있습니다의 **ClusterAuthentication** 매개는 **설치 NetworkControllerCluster** Windows PowerShell 명령을 합니다. 

자세한 내용은 참조 [설치-NetworkControllerCluster](https://technet.microsoft.com/itpro/powershell/windows/network-controller/install-networkcontrollercluster)합니다.

**인증**

네트워크 컨트롤러 클러스터 통신에 대 한 인증을 구성할 때 통신 하는 다른 노드의 id 확인을 위해 클러스터 노드가 네트워크 컨트롤러 허용 합니다.

네트워크 컨트롤러 네트워크 컨트롤러 노드 사이의 인증 다음 세 가지 모드를 지원합니다.

>[!NOTE]
>SCVMM만 사용 하 여 네트워크 컨트롤러 배포한 **Kerberos** 모드 지원 됩니다.

1. **Kerberos**합니다. 도메인 계정 인증에 사용 되는 모든 네트워크 컨트롤러 클러스터 노드에서 된 Active Directory 도메인에 가입한 경우 Kerberos 인증을 사용할 수 있습니다.

2. **X509**합니다. X509는 certificate\ 기반 인증입니다. 네트워크 컨트롤러 클러스터 노드에서 경우 인증 된 Active Directory 도메인에 가입 하지 않은 X509 사용할 수 있습니다. X509를 사용 하 여 모든 네트워크 컨트롤러 클러스터 노드가에 인증서를 등록 해야 하 고 모든 노드 인증서를 신뢰 해야 합니다. 또한 각 노드에서 등록 인증서의 제목 이름을 노드의 DNS 이름과 같은 이어야 합니다.

3. **없음**합니다. 이 모드를 선택 하면 인증이 사이 네트워크 컨트롤러 노드 수행 되지 않습니다. 이 모드 테스트 목적을 위해서만 제공 됩니다 및 생산 환경에서 사용할 수 있도록 권장 되지 않습니다.

**인증**

네트워크 컨트롤러 클러스터 통신에 대 한 권한을 구성할 때 통신 있는 노드 신뢰할 수 있는지 확인 하 고 통신에 참여할 수 있는 권한이를 클러스터 노드가 네트워크 컨트롤러 허용 합니다.

네트워크 컨트롤러에서 지원 되는 인증 모드 각 다음 인증 방법은 사용 됩니다.

1. **Kerberos**합니다. 네트워크 컨트롤러 노드 다른 네트워크 컨트롤러 기계 계정 에서만에서 통신 요청을 접수. 네트워크 컨트롤러를 사용 하 여 배포 하는 경우 이러한 계정의 구성할 수 있습니다는 **이름** 매개는 [새로 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell 명령을 합니다.

2. **X509**합니다. 네트워크 컨트롤러 노드 다른 네트워크 컨트롤러 기계 계정 에서만에서 통신 요청을 접수. 네트워크 컨트롤러를 사용 하 여 배포 하는 경우 이러한 계정의 구성할 수 있습니다는 **이름** 매개는 [새로 NetworkControllerNodeObject](https://technet.microsoft.com/itpro/powershell/windows/network-controller/new-networkcontrollernodeobject) Windows PowerShell 명령을 합니다.

3. **없음**합니다. 이 모드를 선택할 때 사이 네트워크 컨트롤러 노드 수행 인증 합니다. 이 모드 테스트 목적을 위해서만 제공 됩니다 및 생산 환경에서 사용할 수 있도록 권장 되지 않습니다.

**암호화**

네트워크 컨트롤러 노드 간 통신 WCF 전송 수준 암호화를 사용 하 여 암호화 됩니다. 인증과 방법 Kerberos 또는 X509 때이 형태의 암호화 사용 되는 인증서 합니다. 자세한 내용은 다음 항목을 참조 합니다.

- [하는 방법: 보안 Windows 자격 증명 서비스](https://msdn.microsoft.com/library/ms734673.aspx)
- [하는 방법: 보안 인증서 X.509 서비스](https://msdn.microsoft.com/library/ms788968.aspx)합니다.

## <a name="southbound-communication"></a>Southbound 커뮤니케이션

네트워크 컨트롤러 다른 종류의 Southbound 통신에 대 한 장치 상호 작용합니다. 이러한 상호 작용 여러 프로토콜을 사용 합니다. 이 때문 인증, 권한 및 암호화 디바이스 및 네트워크 컨트롤러 디바이스와 통신할 수 사용 하는 프로토콜 유형에 따라에 대 한 여러 요구 사항이 있습니다.

다음 표에서 네트워크 컨트롤러 southbound 다른 디바이스와의 상호 작용에 대 한 정보를 제공합니다.

| Southbound 장치/서비스 | 프로토콜              | 사용 되는 인증    |
|---------------------------|-----------------------|------------------------|
| 부하 분산 소프트웨어가    | WCF (MUX) TCP (호스트) | 인증서           |
| 방화벽                  | OVSDB                 | 인증서           |
| 게이트웨이                   | WinRM                 | 인증서 Kerberos |
| 가상 네트워킹        | OVSDB WCF            | 인증서           |
| 사용자 정의 경로      | OVSDB                 | 인증서           |

이러한 프로토콜 각 통신 메커니즘 다음 섹션에 설명 되어 있습니다.

**인증**

Southbound 통신을 위해 다음과 같은 프로토콜 및 인증 방법을 사용 됩니다.

1. **WCF/TCP/OVSDB**합니다. 이러한 프로토콜에 대 한 인증할 X509를 사용 하 여 인증서 합니다. 네트워크 컨트롤러 및 피어 부하 분산 소프트웨어가 \(SLB\) Multiplexer \ (MUX\) 호스트 시스템 상호 인증을 위한 인증서 서로 있는 / 합니다. 각 인증서 원격 피어 신뢰할 수 있어야 합니다.

    Southbound 인증에 대 한 구성 된 것과 동일한 SSL 인증서 암호화 Northbound 하는 클라이언트와 통신 하는 데 사용할 수 있습니다. 또한 SLB MUX 및 호스트 장치에 인증서를 구성 해야 합니다. 인증서 제목 장치의 DNS 이름을와 동일 해야 합니다.

2. **WinRM**합니다. 이 프로토콜에 대 한 인증할 Kerberos을 사용 하 여 \ (도메인에 가입 machines\)에 대 한 인증서를 사용 하 여 \ (비 도메인 결합된 machines\)에 대 한 합니다.

**인증**

Southbound 통신을 위해 다음과 같은 프로토콜 및 인증 메서드를 사용 합니다.

1. **WCF/TCP**합니다. 이러한 프로토콜에 대 한 권한은 피어 엔터티의 제목 이름을 기반으로 합니다. 네트워크 컨트롤러 피어 장치 DNS 이름 저장 되 고 인증을 위해 사용 합니다. 이 DNS 이름 인증서에는 디바이스의 제목 이름과 일치 해야 합니다. 마찬가지로, 네트워크 컨트롤러 인증서 피어 디바이스에 저장 된 네트워크 컨트롤러 DNS 이름과 일치 해야 합니다.

2. **WinRM**합니다. Kerberos 사용 중인 경우 WinRM 클라이언트 계정 미리 정의 된 Active Directory 또는 서버에서 로컬 관리자가 그룹 그룹에 있어야 합니다. 인증서를 사용 하는 경우 클라이언트는 서버 서버 제목 이름/발행인이 사용 하 여 권한을 부여 하 고 서버 인증을 수행 매핑된 사용자 계정을 사용 하는 인증서를 제공 합니다.

3.  **OVSDB**합니다. 이 프로토콜에 대 한 제공 인증입니다.

**암호화**

Southbound 통신에 대 한 프로토콜에 대 한 다음 암호화 방법은 사용 합니다.

1. **WCF/TCP/OVSDB**합니다. 이러한 프로토콜에 대 한 암호화 클라이언트 또는 서버에 등록 된 인증서를 사용 하 여 수행 됩니다.

2. **WinRM**합니다. Kerberos 보안 지원 공급자를 사용 하 여 기본적으로 WinRM 교통 위치가 암호화 된 \(SSP\) 합니다. 추가 암호화 WinRM 서버의 SSL 형태의 구성할 수 있습니다.
