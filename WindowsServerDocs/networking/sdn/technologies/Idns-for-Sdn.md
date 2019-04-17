---
title: SDN 내부 DNS 서비스 (Idn)
description: 이 항목에서는 Windows Server 2016에 네트워킹 정의 된 소프트웨어와 통합 된 내부 DNS (Idn)를 사용 하 여 호스팅된 테 작업을 DNS 서비스를 제공할 수는 방법을 설명 합니다.
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
ms.openlocfilehash: 4bdb495b585cf60315dee60f9365e282877fdc1d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="internal-dns-service-idns-for-sdn"></a>내부 DNS \(iDNS\) SDN에 대 한 서비스

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

클라우드 서비스 공급자 \(CSP\) 또는 Windows Server 2016에 소프트웨어 네트워킹 정의 \(SDN\) 배포를 계획 하는 엔터프라이즈 작업 하는 경우 SDN 통합 되어 내부 DNS \(iDNS\)를 사용 하 여 호스팅된 테 작업을 DNS 서비스를 제공할 수 있습니다.

가상 컴퓨터 호스팅된 \(VMs\) 및 응용 프로그램 내 네트워크 및 인터넷 외부 리소스와 통신 하도록 DNS 필요 합니다. Idn, 인터넷 리소스 및 자신의 격리, 로컬 이름 공간에 대 한 DNS 이름 해상도 서비스 테 넌을 제공할 수 있습니다.

Idn 서비스 테 가상 네트워크에서에서 액세스할 수 없기 때문에 다른 통해 Idn 프록시 서버는 테 네트워크에서 악성 활동에 노출 될 합니다.

**주요 특징이 있는지 확인**

다음은 Idn에 대 한 핵심 기능입니다.

- 공유 DNS 이름 작업에 대 한 테 확인 서비스를 제공 합니다.
- 신뢰할 수 있는 DNS 및 서비스를 이름 확인 테 네임 스페이스 내 DNS 등록
- 반복 DNS 서비스 해상도 테 Vm에서에서 인터넷 이름입니다.
- 원하는 경우 패브릭 및 테 이름의 동시 호스트 구성할 수 있습니다.
- 효과적인 DNS 솔루션을 테 넌 하지 않아도 자체 DNS infrastructure 배포
- 필요한 Active Directory 통합 높은 가용성 합니다.

이 기능 이외에 통합 하 여 광고를 유지 하는 데 문제가 있는 경우 인터넷에 DNS 서버 열고, 주변 네트워크에서 다른 반복 확인자 뒤 Idn 서버 배포할 수 있습니다.

Idn 모든 DNS 쿼리에 대 한 중앙 집중식된 서버 이므로 CSP 또는 엔터프라이즈 테 DNS 방화벽 구현, 필터를 적용, 악성 활동을 감지 하 고 수도 거래를 중앙 위치에 감사

## <a name="idns-infrastructure"></a>인프라 Idn
Idn infrastructure Idn 프록시 서버 Idn 포함합니다.

### <a name="idns-servers"></a>서버 Idn
Idn VM DNS 리소스 양식에 테 관련 데이터를 호스트 하는 DNS 서버 설정에 포함 됩니다.

Idn 서버의 내부 DNS 영역에 대 한 권한 있는 서버 및 공공 이름 확인자 역할도 때 Vm 외부 리소스에 연결 하려고 테 넌 트 합니다.

모든 가상 네트워크에서 Vm 호스트 이름을 동일한 영역에서 리소스 DNS 레코드도 저장 됩니다. 예를 들어, Idn contoso.local 라는 영역에 대 한 배포 하는 경우 해당 네트워크에 Vm에 대 한 리소스 DNS 레코드 contoso.local 영역에 저장 됩니다.

테 VM 완벽 하 게 된 도메인 이름 \(FQDNs\) 가상 네트워크 GUID 형식에 대 한의 컴퓨터 이름 및 DNS 접미사 문자열으로 구성 됩니다. 예를 들어 VM 이라는 가상 네트워크 contoso 로컬에 있는 TENANT1 거주 하는 경우는 VM FQDN TENANT1은 합니다. *vn guid*. contoso.local, 어디 *vn guid* DNS 접미사 문자열 가상 네트워크입니다.

>[!NOTE]
>패브릭 관리자 인 경우 Idn로 사용을 위해 특별히 새 DNS 서버를 배포 하는 대신 Idn 서버 서버 CSP 또는 엔터프라이즈 DNS infrastructure를 사용할 수 있습니다. 사용 하는지 여부를 Idn에 대 한 새로운 서버를 배포 하거나 기존의 인프라를 사용 하 여, Idn Active Directory를 항상 사용 가능 합니다. Idn 서버 Active directory 따라서 통합 합니다.

### <a name="idns-proxy"></a>프록시 Idn
Idn 프록시 모든 호스트 실행 되 고 가상 네트워크 DNS 서버 Idn 트래픽을 테 전달 된 Windows 서비스입니다.

다음 그림에서는 Idn 프록시 서버 Idn 통해 테 가상 네트워크 및 인터넷에서 DNS 교통 경로 보여 줍니다.

![인프라 Idn](../../media/Internal-Dns/Internal-Dns.jpg)

## <a name="how-to-deploy-idns"></a>배포 Idn 하는 방법
Windows Server 2016에 SDN 스크립트를 사용 하 여 배포 하는 경우 Idn 배포에 자동으로 포함 됩니다.

자세한 내용은 다음 항목을 참조 합니다.

- [스크립트를 사용 하는 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)


## <a name="understanding-idns-deployment-steps"></a>이해 Idn 배포 단계
이 섹션 Idn 설치 되 고 스크립트를 사용 하 여 SDN 배포할 때 구성 되는 방식을 파악를 사용할 수 있습니다.

다음은 Idn 배포 하는 데 필요한 단계의 요약입니다.

>[!NOTE]
>스크립트를 사용 하 여 SDN 배포한 경우 다음이 단계를 수행 필요가 없습니다. 단계에 대 한 정보와 문제 해결 용도로 제공 됩니다.

### <a name="step-1-deploy-dns"></a>1 단계: DNS 배포
이때 Windows PowerShell 명령을 사용 하 여 DNS 서버를 배포할 수 있습니다.
    
    Install-WindowsFeature DNS -IncludeManagementTools
    
### <a name="step-2-configure-idns-information-in-network-controller"></a>네트워크 컨트롤러의 Idn 정보를 구성 하는 2 단계:
이 스크립트 세그먼트 하려고 관리자가 네트워크 컨트롤러는 iDNSServer 및 호스트 Idn 이름 하는 데 사용 되는 영역의 IP 주소 같은-Idn 영역 구성에 대 한 알리는 나머지 전화입니다. 

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
>이 섹션의 일부는 **구성 ConfigureIDns** SDNExpress.ps1에 있습니다. 자세한 내용은 참조 [스크립트 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)합니다.

### <a name="step-3-configure-the-idns-proxy-service"></a>3 단계: 구성 Idn 프록시 서비스
각 소유 가상 네트워크와 Idn 서버가 있는 실제 네트워크 사이의 다리 제공 Hyper-v 호스트 Idn 프록시 서비스도 실행 합니다. 다음 레지스트리 키 모든 Hyper-v 호스트 만들어야 합니다.


**DNS 포트:** 포트 53 고정

- 레지스트리 키 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService = "
- 값 = "포트"
- ValueData 53 =
- 값 = "Dword"
       

**프록시 포트 DNS:** 포트 53 고정

- 레지스트리 키 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService = "
- 값 = "ProxyPort"
- ValueData 53 =
- 값 = "Dword"
        
**DNS IP:** 는 테 Idn 서비스를 사용 하기로 결정 하는 경우에 네트워크 인터페이스 구성 고정된 IP 주소입니다.

- 레지스트리 키 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService = "
- 값 = "IP"
- ValueData = "169.254.169.254"
- 값 = "문자열"

        
**Mac 주소:** DNS 서버 주소 미디어 액세스 제어

- 레지스트리 키 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NcHostAgent\Parameters\Plugins\Vnet\InfraServices\DnsProxyService =
- 값 = "MAC"
- ValueData = "aa-bb-cc-aa-bb-cc"
- 값 = "문자열"

**서버 주소 IDN:** 쉼표로 구분 서버 Idn 목록입니다.

- 레지스트리 키: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\DNSProxy\Parameters
- 값 = "전달자"
- ValueData = "10.0.0.9"
- 값 = "문자열"



>[!NOTE]
>이 섹션의 일부는 **구성 ConfigureIDnsProxy** SDNExpress.ps1에 있습니다. 자세한 내용은 참조 [스크립트 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)합니다.

### <a name="step-4-restart-the-network-controller-host-agent-service"></a>4 단계: 네트워크 컨트롤러 호스트 에이전트 서비스 다시 시작
다음 Windows PowerShell 명령을 네트워크 컨트롤러 호스트 에이전트 서비스 다시 시작을 사용할 수 있습니다.
    
    Restart-Service nchostagent -Force
    
자세한 내용은 참조 [서비스 다시 시작](https://technet.microsoft.com/library/hh849823.aspx)합니다.

### <a name="enable-firewall-rules-for-the-dns-proxy-service"></a>DNS 프록시 서비스에 대 한 규칙 방화벽을 사용 하도록 설정
다음 Windows PowerShell 명령을 VM Idn 서버와 통신 하는 프록시에 대 한 예외 수 있도록 해 주는 방화벽 규칙을 만드는 사용할 수 있습니다.
    
    Enable-NetFirewallRule -DisplayGroup 'DNS Proxy Firewall'

자세한 내용은 참조 [활성화 NetFirewallRule](https://technet.microsoft.com/library/jj554869.aspx)합니다.
    
### <a name="validate-the-idns-service"></a>서비스 Idn의 유효성을 검사합니다
서비스 Idn 유효성을 검사 하기 샘플 테 작업을 배포 해야 합니다.

자세한 내용은 참조 [VM 만들고 VLAN 또는 테 가상 네트워크에 연결](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create-a-tenant-vm)합니다.

테 VM Idn 서비스를 사용 하 여 비워 VM 네트워크 인터페이스 DNS 서버 구성 고 인터페이스 DHCP를 사용 하도록 허용 합니다. 

한 네트워크 인터페이스 VM 시작 되 면 자동으로 받을 Idn를 사용 하 여 VM 수 있도록 해 주는 구성 하 고 VM 즉시 이름 확인 Idn 서비스를 사용 하 여 수행 하을 시작 합니다.

테 Idn 서비스를 사용 하 여 네트워크 인터페이스 DNS 서버 및 보조 DNS 서버의 정보를 비워 두고 VM 구성 하는 경우 네트워크 컨트롤러 VM IP 주소를 제공 하 고 VM Idn 서버를 대표 하 여 DNS 이름 등록을 수행 합니다. 

네트워크 컨트롤러에도 vm 이름을 확인을 수행 하는 VM 및 다음 필요한 세부 정보에 대 한 Idn 프록시를 알립니다. 

VM DNS 쿼리에 시작 프록시 역할을 Idn 서비스 가상 네트워크에서 쿼리 전달자 합니다. 

또한 DNS 프록시 테 VM 쿼리 격리 되어 있는지 확인 합니다. Idn 서버가 쿼리 신뢰할 수 있는 경우 신뢰할 수 있는 응답 Idn 서버가 응답 합니다. Idn 서버 쿼리를 신뢰할 수 없는 경우 인터넷 이름을 확인 하기 위해 DNS 반복적으로 실행 것입니다.

>[!NOTE]
>이 정보는 섹션에 포함 되어 **구성 AttachToVirtualNetwork** SDNExpressTenant.ps1에 있습니다. 자세한 내용은 참조 [스크립트 사용 하 여 소프트웨어 정의 네트워크 인프라 배포](https://technet.microsoft.com/windows-server-docs/networking/sdn/deploy/deploy-a-software-defined-network-infrastructure-using-scripts)합니다.

