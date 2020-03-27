---
title: SDN용 iDNS(내부 DNS 서비스)
description: 이 항목에서는 Idn (내부 DNS)를 사용 하 여 호스트 된 테 넌 트 워크 로드에 DNS 서비스를 제공 하는 방법에 대해 설명 합니다 .이는 Windows Server 2016의 소프트웨어 정의 네트워킹에 통합 되어 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ad848a5b-0811-4c67-afe5-6147489c0384
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0b08e5af20b3d089391717479817e0d26329fde2
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317252"
---
# <a name="internal-dns-service-idns-for-sdn"></a>SDN용 iDNS(내부 DNS 서비스)

>적용 대상: Windows Server(반기 채널), Windows Server 2016

Windows Server 2016에서 SDN\) 소프트웨어 정의 네트워킹 \(배포를 계획 하는 클라우드 서비스 공급자 \(CSP\) 또는 엔터프라이즈에 대해 작업 하는 경우 SDN과 통합 된 내부 DNS \(Idn\)를 사용 하 여 호스트 된 테 넌 트 워크 로드에 DNS 서비스를 제공할 수 있습니다.

호스트 되는 가상 컴퓨터 \(Vm\) 및 응용 프로그램은 DNS를 사용 하 여 자체 네트워크와 인터넷의 외부 리소스에서 통신 해야 합니다. Idn를 사용 하면 격리 된 로컬 이름 공간 및 인터넷 리소스에 대해 DNS 이름 확인 서비스를 사용 하 여 테 넌 트를 제공할 수 있습니다.

Idn 서비스는 Idn 프록시를 통해서가 아닌 테 넌 트 가상 네트워크에서 액세스할 수 없기 때문에 테 넌 트 네트워크의 악의적인 작업에 취약 하지 않습니다.

**주요 기능**

다음은 Idn에 대 한 주요 기능입니다.

- 테 넌 트 워크 로드에 대 한 공유 DNS 이름 확인 서비스를 제공 합니다.
- 테 넌 트 이름 공간 내에서 이름 확인 및 DNS 등록에 대 한 권한 있는 DNS 서비스
- 테 넌 트 Vm의 인터넷 이름 확인을 위한 재귀 DNS 서비스입니다.
- 필요한 경우 패브릭 및 테 넌 트 이름의 동시 호스팅을 구성할 수 있습니다.
- 비용 효율적인 DNS 솔루션-테 넌 트는 자체 DNS 인프라를 배포할 필요가 없습니다.
- Active Directory 통합이 필요한 고가용성입니다.

이러한 기능 외에도 AD 통합 DNS 서버를 인터넷에 공개 하는 것이 염려 되는 경우 경계 네트워크의 다른 재귀 해결 프로그램 뒤에 Idn 서버를 배포할 수 있습니다.

Idn는 모든 DNS 쿼리에 대해 중앙화 된 서버 이므로 CSP 또는 엔터프라이즈는 테 넌 트 DNS 방화벽을 구현 하 고, 필터를 적용 하 고, 악성 작업을 검색 하 고, 중앙 위치에서 트랜잭션을 감사할 수도 있습니다.

## <a name="idns-infrastructure"></a>Idn 인프라
Idn 인프라에는 Idn Servers 및 Idn proxy가 포함 됩니다.

### <a name="idns-servers"></a>Idn 서버
Idn에는 VM DNS 리소스 레코드와 같은 테 넌 트 관련 데이터를 호스트 하는 DNS 서버 집합이 포함 되어 있습니다.

Idn 서버는 내부 DNS 영역에 대 한 권한 있는 서버 이며, 테 넌 트 Vm이 외부 리소스에 연결 하려고 할 때 공용 이름에 대 한 확인자 역할도 합니다.

가상 네트워크의 Vm에 대 한 모든 호스트 이름은 동일한 영역에 DNS 리소스 레코드로 저장 됩니다. 예를 들어 Idn 이라는 영역에 대해를 배포 하는 경우 해당 네트워크의 Vm에 대 한 DNS 리소스 레코드는 contoso. 로컬 영역에 저장 됩니다.

Fqdn \(\) Fqdn (정규화 된 도메인 이름)은 Virtual Network에 대 한 컴퓨터 이름 및 DNS 접미사 문자열 (GUID 형식)으로 구성 됩니다. 예를 들어 테 넌 트 이라는 테 넌 트 VM Virtual Network이 있는 경우 (예: contoso, local) VM의 FQDN은 테 넌 트입니다. *vn*. 여기서 *vn* 는 VIRTUAL NETWORK에 대 한 DNS 접미사 문자열입니다.

>[!NOTE]
>패브릭 관리자는 Idn 서버로 사용 하기 위해 특별히 새 DNS 서버를 배포 하는 대신 CSP 또는 엔터프라이즈 DNS 인프라를 Idn 서버로 사용할 수 있습니다. Idn에 대 한 새 서버를 배포 하거나 기존 인프라를 사용 하는 경우에는 Idn가 Active Directory에 의존 하 여 고가용성을 제공 합니다. 따라서 Idn 서버는 Active Directory와 통합 되어야 합니다.

### <a name="idns-proxy"></a>Idn 프록시
Idn proxy는 모든 호스트에서 실행 되 고 테 넌 트 Virtual Network DNS 트래픽을 Idn 서버로 전달 하는 Windows 서비스입니다.

다음 그림에서는 Idn 프록시를 통해 테 넌 트 가상 네트워크에서 Idn 서버 및 인터넷으로의 DNS 트래픽 경로를 보여 줍니다.

![Idn 인프라](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Idn를 배포 하는 방법
스크립트를 사용 하 여 Windows Server 2016에 SDN을 배포 하는 경우 Idn가 배포에 자동으로 포함 됩니다.

자세한 내용은 다음 항목을 참조하세요.

- [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Idn 배포 단계 이해
이 섹션을 사용 하 여 스크립트를 사용 하 여 SDN을 배포할 때 Idn가 설치 되 고 구성 되는 방식을 파악할 수 있습니다.

다음은 Idn를 배포 하는 데 필요한 단계를 요약 한 것입니다.

>[!NOTE]
>스크립트를 사용 하 여 SDN을 배포한 경우에는 이러한 단계를 수행할 필요가 없습니다. 이러한 단계는 정보 및 문제 해결을 위해서만 제공 됩니다.

### <a name="step-1-deploy-dns"></a>1 단계: DNS 배포
다음 예제 Windows PowerShell 명령을 사용 하 여 DNS 서버를 배포할 수 있습니다.
    
    Install-WindowsFeature DNS -IncludeManagementTools
    
### <a name="step-2-configure-idns-information-in-network-controller"></a>2 단계: 네트워크 컨트롤러에서 Idn 정보 구성
이 스크립트 세그먼트는 관리자가 네트워크 컨트롤러에 대해 수행 하는 REST 호출로, Idn 영역 구성 (예: iDNSServer의 IP 주소 및 Idn 이름을 호스트 하는 데 사용 되는 영역)에 대해 알립니다. 

```
    Url: https://<url>/networking/v1/iDnsServer/configuration
Method: PUT
{
      "properties": {
        "connections": [
          {
            "managementAddresses": [
              "10.0.0.9"
            ],
            "credential": {
              "resourceRef": "/credentials/iDnsServer-Credentials"
            },
            "credentialType": "usernamePassword"
          }
        ],
        "zone": "contoso.local"
      }
    }
```

>[!NOTE]
>이는 SDNExpress. p s 1에서 **구성 ConfigureIDns** 섹션에서 발췌 한 것입니다. 자세한 내용은 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)를 참조 하세요.

### <a name="step-3-configure-the-idns-proxy-service"></a>3 단계: Idn 프록시 서비스 구성
Idn 프록시 서비스는 각 Hyper-v 호스트에서 실행 되며, 테 넌 트의 가상 네트워크와 Idn 서버가 있는 실제 네트워크 간의 브리지를 제공 합니다. 모든 Hyper-v 호스트에서 다음 레지스트리 키를 만들어야 합니다.


**DNS 포트:** 고정 포트 53

- 레지스트리 키 = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- ValueName = "Port"
- ValueData = 53
- ValueType = "Dword"
       

**DNS 프록시 포트:** 고정 포트 53

- 레지스트리 키 = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- ValueName = "ProxyPort"
- ValueData = 53
- ValueType = "Dword"
        
**DNS IP:** 테 넌 트가 Idn 서비스를 사용 하도록 선택 하는 경우 네트워크 인터페이스에 구성 된 고정 IP 주소

- 레지스트리 키 = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService "
- ValueName = "IP"
- ValueData = "169.254.169.254"
- ValueType = "String"

        
**Mac 주소:** DNS 서버의 미디어 Access Control 주소

- 레지스트리 키 = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService
- ValueName = "MAC"
- ValueData = "aa-bb-cc-aa-/bb-cc"
- ValueType = "String"

**서버 주소 idn:** 쉼표로 구분 된 Idn 서버 목록입니다.

- 레지스트리 키: HKLM\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- ValueName = "전달자"
- ValueData = "10.0.0.9가"
- ValueType = "String"



>[!NOTE]
>이는 SDNExpress. p s 1에서 **구성 ConfigureIDnsProxy** 섹션에서 발췌 한 것입니다. 자세한 내용은 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)를 참조 하세요.

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>4 단계: 네트워크 컨트롤러 호스트 에이전트 서비스 다시 시작
다음 Windows PowerShell 명령을 사용 하 여 네트워크 컨트롤러 호스트 에이전트 서비스를 다시 시작할 수 있습니다.
    
    Restart-Service nchostagent -Force
    
자세한 내용은 [서비스 다시 시작](https://technet.microsoft.com/library/hh849823.aspx)을 참조 하세요.

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>DNS 프록시 서비스에 대해 방화벽 규칙 사용
다음 Windows PowerShell 명령을 사용 하 여 프록시가 VM 및 Idn 서버와 통신 하는 데 필요한 예외를 허용 하는 방화벽 규칙을 만들 수 있습니다.
    
    Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'

자세한 내용은 [set-netfirewallrule](https://technet.microsoft.com/library/jj554869.aspx)를 참조 하세요.
    
### <a name="validate-the-idns-service"></a>Idn 서비스의 유효성을 검사 합니다.
Idn 서비스의 유효성을 검사 하려면 샘플 테 넌 트 워크 로드를 배포 해야 합니다.

자세한 내용은 [VM 만들기 및 테 넌 트 Virtual Network 또는 VLAN에 연결](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)을 참조 하세요.

테 넌 트 VM이 Idn 서비스를 사용 하도록 하려면 VM 네트워크 인터페이스 DNS 서버 구성을 비워 두고 인터페이스가 DHCP를 사용할 수 있도록 해야 합니다. 

이러한 네트워크 인터페이스를 사용 하는 VM이 시작 되 면 VM이 Idn를 사용할 수 있도록 하는 구성을 자동으로 수신 하 고 VM은 즉시 Idn 서비스를 사용 하 여 이름 확인을 수행 하기 시작 합니다.

네트워크 인터페이스 DNS 서버 및 대체 DNS 서버 정보를 비워 두고 Idn 서비스를 사용 하도록 테 넌 트 VM을 구성 하는 경우 네트워크 컨트롤러는 VM에 IP 주소를 제공 하 고 Idn 서버를 사용 하 여 VM을 대신 하 여 DNS 이름 등록을 수행 합니다. . 

또한 네트워크 컨트롤러는 vm에 대 한 Idn 프록시와 VM에 대 한 이름 확인을 수행 하는 데 필요한 세부 정보를 알려 줍니다. 

VM이 DNS 쿼리를 시작 하면 프록시는 Virtual Network에서 Idn 서비스로 쿼리를 전달 하는 역할을 합니다. 

또한 DNS 프록시는 테 넌 트 VM 쿼리가 격리 되도록 합니다. Idn 서버가 쿼리에 대해 권한이 있는 경우 Idn 서버는 신뢰할 수 있는 응답으로 응답 합니다. Idn 서버가 쿼리에 대해 권한이 없는 경우 DNS 재귀를 수행 하 여 인터넷 이름을 확인 합니다.

>[!NOTE]
>이 정보는 **Configuration AttachToVirtualNetwork** in SDNExpressTenant 섹션에 포함 되어 있습니다. 자세한 내용은 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)를 참조 하세요.

