---
title: SDN용 iDNS(내부 DNS 서비스)
description: 이 항목에서는 Windows Server 2016의 소프트웨어 정의 네트워킹와 통합 되는 내부 DNS (Idn)를 사용 하 여 호스 티 드 테 넌 트 워크 로드에 DNS 서비스를 제공할 수는 방법을 설명 합니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: ad848a5b-0811-4c67-afe5-6147489c0384
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4d4ae5ee5f5600d86349ca26b7acbdb284b45bac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824084"
---
# <a name="internal-dns-service-idns-for-sdn"></a>SDN용 iDNS(내부 DNS 서비스)

>적용 대상: Windows Server (반기 채널), Windows Server 2016

클라우드 서비스 공급자에 대해 작업 하는 경우 \(CSP\) 또는 소프트웨어 정의 네트워킹 배포 계획은 Enterprise \(SDN\) Windows Server 2016에서 호스트 된 테 넌 트 워크 로드에 DNS 서비스를 제공할 수 있습니다 내부 DNS를 사용 하 여 \(Idn\), SDN을 사용 하 여 통합 합니다.

호스트 된 가상 머신 \(Vm\) 각자 고유한 네트워크 내부 및 인터넷에서 외부 리소스를 사용 하 여 통신 하도록 DNS를 요구 하는 응용 프로그램 및 합니다. Idn을 사용 하 여 인터넷 리소스 및 해당 격리 된, 로컬 네임 스페이스에 대 한 DNS 이름 확인 서비스를 사용 하 여 테 넌 트 제공할 수 있습니다.

Idn 서비스, 테 넌 트 가상 네트워크에서에서 액세스할 수 없기 때문에 다른 Idn 프록시를 통해 서버는 테 넌 트 네트워크에서 악성 활동에 취약 합니다.

**주요 기능**

Idn에 대 한 주요 기능은 다음과 같습니다.

- 공유 DNS 이름 확인 서비스 테 넌 트에 대 한 워크 로드를 제공 합니다.
- 이름 확인 및 테 넌 트 네임 스페이스 내에서 DNS 등록에 대 한 권한이 있는 DNS 서비스
- 테 넌 트 Vm에서에서 인터넷 이름 확인에 대 한 재귀 DNS 서비스입니다.
- 원하는 경우 동시 호스팅 패브릭 및 테 넌 트 이름을 구성할 수 있습니다.
- 비용 효율적인 DNS 솔루션-테 넌 트 필요가 자체 DNS 인프라를 배포 합니다.
- 고가용성 요구 하는 Active Directory 통합

이러한 기능 외에 AD 통합을 유지 하는 방법에 대 한 우려되는 경우 DNS 서버는 인터넷에 열린, 경계 네트워크의 다른 재귀 확인자 뒤에 Idn 서버를 배포할 수 있습니다.

Idn 모든 DNS 쿼리에 대 한 중앙 집중식된 서버 이기 때문에 CSP 또는 엔터프라이즈 수 또한 테 넌 트 DNS 방화벽을 구현, 필터를 적용, 악의적인 활동을 검색 및 중앙 위치에서 트랜잭션 감사

## <a name="idns-infrastructure"></a>Idn 인프라
Idn 인프라 Idn 서버 및 Idn 프록시를 포함합니다.

### <a name="idns-servers"></a>Idn 서버
Idn VM DNS 리소스 레코드와 같은 테 넌 트 별 데이터를 호스팅하는 DNS 서버 집합이 포함 되어 있습니다.

Idn 서버는 해당 내부 DNS 영역에 대 한 신뢰할 수 있는 서버 및 공용 이름 위한 확인 자가 역할도 경우 외부 리소스에 연결 하려고 하는 Vm을 테 넌 트입니다.

가상 네트워크의 Vm에 대 한 호스트 이름의 모든 동일한 영역에서 DNS 리소스 레코드로 저장 됩니다. 예를 들어 contoso.local 명명 된 영역에 대 한 Idn을 배포 하는 경우 해당 네트워크에서 Vm에 대 한 DNS 리소스 레코드를 contoso.local 영역에 저장 됩니다.

VM 정규화 된 도메인 이름이 테 넌 트 \(Fqdn\) GUID 형식으로 가상 네트워크의 컴퓨터 이름과 DNS 접미사 문자열을 구성 합니다. 예를 들어, 테 넌 트 가상 네트워크 contoso, 로컬에 있는 TENANT1 이라는 VM을 사용 하는 경우 VM의 FQDN은 TENANT1입니다. *vn guid*. contoso.local, 여기서 *vn guid* 가상 네트워크에 대 한 DNS 접미사 문자열입니다.

>[!NOTE]
>패브릭 관리자 인 경우에 Idn 서버에 맞게 새 DNS 서버를 배포 하는 대신 사용 하 여 Idn으로 서버 CSP 또는 엔터프라이즈 DNS 인프라를 사용할 수 있습니다. Idn에 대 한 새 서버를 배포 하거나 기존 인프라를 사용 하 여, Idn 고가용성을 제공 하기 위해 Active Directory 의존 합니다. 따라서 Active Directory를 사용 하 여 Idn 서버를 통합 합니다.

### <a name="idns-proxy"></a>Idn 프록시
Idn 프록시는 테 넌 트를 가상 네트워크 DNS 서버 Idn 트래픽을 전달 되는 모든 호스트에서 실행 되는 Windows 서비스입니다.

다음 그림은 테 넌 트 가상 네트워크는 Idn 프록시를 통해 Idn 서버 및 인터넷 DNS 트래픽 경로 보여 줍니다.

![Idn 인프라](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>Idn 배포 하는 방법
스크립트를 사용 하 여 Windows Server 2016에서 SDN을 배포한 Idn 배포에서 자동으로 포함 됩니다.

자세한 내용은 다음 항목을 참조하세요.

- [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://docs.microsoft.com/windows-server/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>Idn 배포 단계를 이해합니다.
Idn은 설치 하 고 스크립트를 사용 하 여 SDN을 배포 하는 경우 구성 하는 방법을 이해를 갖추기 위해이 섹션에서는 사용할 수 있습니다.

다음은 Idn을 배포 하는 데 필요한 단계의 요약입니다.

>[!NOTE]
>SDN 스크립트를 사용 하 여 배포한 경우 다음이 단계 중 하나를 수행할 필요가 없습니다. 단계 정보 및 문제 해결 목적 으로만 제공 됩니다.

### <a name="step-1-deploy-dns"></a>1단계: 배포 DNS
다음 예제에서는 Windows PowerShell 명령을 사용 하 여 DNS 서버를 배포할 수 있습니다.
    
    Install-WindowsFeature DNS -IncludeManagementTools
    
### <a name="step-2-configure-idns-information-in-network-controller"></a>2단계: 네트워크 컨트롤러에서 Idn 정보를 구성 합니다.
이 스크립트 세그먼트 REST 호출 되는 관리자가 네트워크 컨트롤러에 IP 주소는 iDNSServer와 Idn 이름을 호스트 하는 데 사용 되는 영역 등 Idn 영역 구성-알리는 것입니다. 

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
>이 섹션에서 발췌 **구성 ConfigureIDns** SDNExpress.ps1에서. 자세한 내용은 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)합니다.

### <a name="step-3-configure-the-idns-proxy-service"></a>3단계: Idn 프록시 서비스를 구성 합니다.
Idn 프록시 서비스는 각 테 넌 트의 가상 네트워크 및 Idn 서버가 있는 실제 네트워크 간의 브리지를 제공 하는 Hyper-v 호스트에서 실행 됩니다. 모든 Hyper-v 호스트에서 다음 레지스트리 키를 만들어야 합니다.


**DNS 포트:** 고정된 포트 53

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName = "Port"
- ValueData = 53
- ValueType = "Dword"
       

**DNS 프록시 포트:** 고정된 포트 53

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName = "ProxyPort"
- ValueData = 53
- ValueType = "Dword"
        
**DNS IP:** Idn 서비스를 사용 하려면 테 넌 트를 선택 하는 경우 네트워크 인터페이스에 구성 된 고정된 IP 주소

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService"
- ValueName = "IP"
- ValueData = "169.254.169.254"
- ValueType = "String"

        
**Mac 주소:** DNS 서버의 미디어 액세스 제어 주소

- Registry Key = HKLM\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService
- ValueName = "MAC"
- ValueData = “aa-bb-cc-aa-bb-cc”
- ValueType = "String"

**IDN 서버 주소:** 쉼표로 구분한 목록 Idn 서버입니다.

- 레지스트리 키: HKLM\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- ValueName "전달자" =
- ValueData = “10.0.0.9”
- ValueType = "String"



>[!NOTE]
>이 섹션에서 발췌 **구성 ConfigureIDnsProxy** SDNExpress.ps1에서. 자세한 내용은 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)합니다.

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>4단계: 네트워크 컨트롤러 호스트 에이전트 서비스를 다시 시작
네트워크 컨트롤러 호스트 에이전트 서비스를 다시 시작 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.
    
    Restart-Service nchostagent -Force
    
자세한 내용은 [Restart-service](https://technet.microsoft.com/library/hh849823.aspx)합니다.

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>DNS 프록시 서비스에 대 한 방화벽 규칙을 사용 하도록 설정
VM 및 Idn 서버와 통신 하는 프록시에 대 한 예외를 허용 하는 방화벽 규칙을 만들려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.
    
    Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'

자세한 내용은 [Enable-netfirewallrule](https://technet.microsoft.com/library/jj554869.aspx)합니다.
    
### <a name="validate-the-idns-service"></a>Idn 서비스 유효성 검사
Idn 서비스의 유효성을 검사 하는 샘플 테 넌 트 워크 로드를 배포 해야 합니다.

자세한 내용은 [VM 및 테 넌 트 가상 네트워크 또는 VLAN에 연결 만들기](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)합니다.

테 넌 트 Idn 서비스를 사용 하는 VM을 하려는 경우에 VM 네트워크 인터페이스 DNS 서버 구성은 비워 둡니다 하 고 DHCP를 사용 하는 인터페이스를 허용 해야 합니다. 

이러한 네트워크 인터페이스를 사용 하 여 VM이 시작 되 면 Idn을 사용 하도록 VM을 허용 하는 구성을 자동으로 수신 하 고 VM 즉시 Idn 서비스를 사용 하 여 이름 확인을 수행을 시작 합니다.

테 넌 트 네트워크 인터페이스 DNS 서버 및 보조 DNS 서버 정보를 비워 두면 Idn 서비스를 사용 하는 VM을 구성 하는 경우 네트워크 컨트롤러 IP 주소를 사용 하 여 VM을 제공 하 고 서버 Idn 사용 하 여 VM을 대신 하 여 DNS 이름 등록을 수행 . 

또한 네트워크 컨트롤러 VM과 필요한 세부 정보를 VM에 대 한 이름 확인을 수행 하는 방법에 대 한 Idn 프록시를 알립니다. 

VM에서 DNS 쿼리를 시작 하는 경우 프록시 전달자 역할을 가상 네트워크에서 Idn 서비스에 쿼리 합니다. 

또한 DNS 프록시는 테 넌 트 VM 쿼리 격리 되어 있는지 확인 합니다. Idn 서버가 쿼리에 대 한 신뢰할 수 있는 경우 Idn 서버는 신뢰할 수 있는 응답으로 응답 합니다. Idn server 쿼리에 대 한 권한이 없는 경우 인터넷 이름을 확인 하기 위해 DNS 재귀를 수행 합니다.

>[!NOTE]
>섹션에서이 정보가 포함 됩니다 **구성 AttachToVirtualNetwork** SDNExpressTenant.ps1에서. 자세한 내용은 [스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)합니다.

