---
title: Windows Server 소프트웨어 정의 네트워킹 스택 문제 해결
description: 이 Windows Server 가이드는 일반적인 소프트웨어 정의 네트워킹 (SDN) 오류 및 실패 시나리오를 검사 하 고 사용 가능한 진단 도구를 활용 하는 문제 해결 워크플로 간략하게 설명 합니다.
manager: ravirao
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: pashort
author: JMesser81
ms.date: 08/14/2018
ms.openlocfilehash: eeb0c335e4afd3c6835a04421a15073aeab6cdc6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446246"
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Windows Server 소프트웨어 정의 네트워킹 스택 문제 해결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 가이드는 네트워킹 SDN (소프트웨어)는 일반적인 오류 및 오류 시나리오를 검사 하 고 사용할 수 있는 진단 도구를 활용 하는 문제 해결 워크플로 간략하게 설명 합니다.  

Microsoft의 소프트웨어 정의 네트워킹에 대 한 자세한 내용은 참조 [소프트웨어 정의 네트워킹](../../sdn/Software-Defined-Networking--SDN-.md)합니다.  

## <a name="error-types"></a>오류 유형  
다음 목록에는 시장에서 프로덕션 배포에서 Windows Server 2012 r 2에서의 Hyper-v 네트워크 가상화 (HNVv1) 흔히 볼 문제 클래스를 나타냅니다와 일치 하는 여러 가지 방법으로는 동일한 유형의 새 네트워크 SDN (소프트웨어) 스택과 Windows Server 2016 HNVv2에서 동안 문제가 발생 합니다.  

대부분의 오류는 다음과 같은 클래스의 작은 집합으로 분류할 수 있습니다.   
* **잘못 되었거나 지원 되지 않는 구성**  
   잘못 되거나 잘못 된 정책 NorthBound API를 호출 하는 사용자.   

* **정책 응용 프로그램에 오류가 있습니다.**  
     네트워크 컨트롤러에서 정책 상당히 지연 및/또는 최신 버전이 아닙니다 (예: 실시간 마이그레이션) 후 모든 Hyper-v 호스트에서 Hyper-v 호스트를 배달 하지 못했습니다.  
* **구성 드리프트 또는 소프트웨어 버그**  
  삭제 된 패킷의 결과 데이터 경로 문제가 있습니다.  

* **외부 오류 NIC 하드웨어와 관련 된 / 드라이버 또는 언더레이 네트워크 패브릭**  
  오동작 작업 오프 로드 (예: VMQ) 또는 언더레이 네트워크 패브릭 MTU) (예: 잘못 구성 되었습니다.   

  이 문제 해결 가이드는 이러한 각 오류 범주를 검사 하 고 모범 사례 및 확인 하 고 오류를 해결 하려면 사용할 수 있는 진단 도구를 권장 합니다.  

## <a name="diagnostic-tools"></a>진단 도구  

각 이러한 유형의 오류에 대 한 문제 해결 워크플로 다루기 전에 사용할 수 있는 진단 도구를 검토해 보겠습니다.   

네트워크 컨트롤러 (제어 경로) 진단 도구를 사용 하려면 먼저 RSAT NetworkController 기능을 설치 하 고 가져오기는 ``NetworkControllerDiagnostics`` 모듈:  

```  
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools  
Import-Module NetworkControllerDiagnostics  
```  

HNV 진단 (데이터 경로) 진단 도구를 사용 하려면 가져와야는 ``HNVDiagnostics`` 모듈:

```  
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics   
```  

### <a name="network-controller-diagnostics"></a>네트워크 컨트롤러 진단  
이러한 cmdlet에는 TechNet에 설명 되어는 [네트워크 컨트롤러 진단 Cmdlet 항목](https://docs.microsoft.com/powershell/module/networkcontrollerdiagnostics/)합니다. 네트워크 정책 일관성은 제어 경로 및 네트워크 컨트롤러와 Hyper-v 호스트에서 실행 되는 NC 호스트 에이전트 네트워크 컨트롤러 노드 사이 문제를 식별 도움이 있습니다.

 _디버그 ServiceFabricNodeStatus_ 및 _Get NetworkControllerReplica_ 네트워크 컨트롤러 노드 가상 컴퓨터 중 하나에서 cmdlet을 실행 해야 합니다. 네트워크 컨트롤러에 연결 되어 및 네트워크 컨트롤러 관리 보안 그룹 (Kerberos)에서 되었거나 네트워크 컨트롤러를 관리 하기 위한 X.509 인증서에 대 한 액세스 하는 모든 호스트에서 다른 모든 NC 진단 cmdlet은 실행할 수 있습니다. 

### <a name="hyper-v-host-diagnostics"></a>Hyper-v 호스트에 대 한 진단 유틸리티  
이러한 cmdlet에는 TechNet에 설명 되어는 [Hyper-v 네트워크 가상화 (HNV) 진단 Cmdlet 항목](https://docs.microsoft.com/powershell/module/hnvdiagnostics/)합니다. 테 넌 트 가상 컴퓨터 (동/서) 간의 데이터 경로에 문제를 식별 하는 데 도움이 및는 SLB VIP (남/북)를 통해 수신 트래픽을 합니다. 

_디버그 VirtualMachineQueueOperation_, _Get CustomerRoute_, _Get PACAMapping_, _Get ProviderAddress_, _Get VMNetworkAdapterPortId_, _Get VMSwitchExternalPortId_, 및 _테스트 EncapOverheadSettings_ 는 모든 Hyper-v 호스트에서 실행 될 수 있는 모든 로컬 테스트 합니다. 네트워크 컨트롤러를 통해 데이터 경로 테스트를 호출 하 고 따라서 위에서 descried와 네트워크 컨트롤러에 대 한 액세스를 해야 하는 다른 cmdlet.

### <a name="github"></a>GitHub
[Microsoft/SDN GitHub 리포지토리](https://github.com/microsoft/sdn) 다양 한 샘플 스크립트와 이러한 기본 cmdlet을 기반으로 구축 하는 워크플로 했습니다. 특히, 진단 스크립트에 있습니다는 [진단](https://github.com/Microsoft/sdn/diagnostics) 폴더입니다. 주시면 끌어오기 요청을 제출 하 여 이러한 스크립트에 기여 합니다.

## <a name="troubleshooting-workflows-and-guides"></a>문제 해결 가이드 및 워크플로  

### <a name="hoster-validate-system-health"></a>[호스터] 시스템 상태 유효성 검사
라는 포함된 된 리소스는 _구성 상태_ 네트워크 컨트롤러 리소스 중 몇 개에 있습니다. 구성 상태는 네트워크 컨트롤러의 구성 및 Hyper-v 호스트에 실제 (실행) 상태 간에 일관성을 포함 하 여 시스템 상태에 대 한 정보를 제공 합니다. 

구성 상태를 확인 하려면에서 다음을 실행 모든 Hyper-v 호스트에 연결 된 네트워크 컨트롤러에 있습니다.

>[!NOTE] 
>에 대 한 값은 *NetworkController* 매개 변수 이름 이어야의 X.509 주체 이름을 기반으로 하는 FQDN 또는 IP 주소 > 네트워크 컨트롤러에 대해 만들어진 인증서입니다.
>
>*자격 증명* 매개 변수에 네트워크 컨트롤러 (VMM 배포에서 일반) Kerberos 인증을 사용 하는 경우 지정 해야 합니다. 네트워크 컨트롤러 관리 보안 그룹에 있는 사용자에 대 한 자격 증명 이어야 합니다.

```none
Debug-NetworkControllerConfigurationState -NetworkController <FQDN or NC IP> [-Credential <PS Credential>]

# Healthy State Example - no status reported
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController 10.127.132.211 -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

샘플 구성 상태 메시지는 다음과 같습니다.

```none
Fetching ResourceType:     servers
---------------------------------------------------------------------------------------------------------
ResourcePath:     https://10.127.132.211/Networking/v1/servers/4c4c4544-0056-4b10-8058-b8c04f395931
Status:           Warning

Source:           SoftwareLoadBalancerManager
Code:             HostNotConnectedToController
Message:          Host is not Connected.
----------------------------------------------------------------------------------------------------------
```

>[!NOTE]
> SLB Mux 전송 중 VM NIC에 대 한 네트워크 인터페이스 리소스가 "가상 스위치-호스트 연결에 컨트롤러가 아닌" 오류와 함께 실패 상태에 있는 시스템에 버그가 있습니다. VM NIC 리소스의 IP 구성이 전송 논리 네트워크의 IP 풀에서 IP 주소로 설정 된 경우이 오류 수 안전 하 게 무시 됩니다. 게이트웨이 HNV 공급자 VM Nic에 대 한 네트워크 인터페이스 리소스가 "가상 스위치-PortBlocked" 오류와 함께 실패 상태에 있는 시스템에서 두 번째 버그가 있습니다. 이 오류도 안전 하 게 무시할 수 VM NIC 리소스의 IP 구성이 설정 된 경우 null로 (디자인).


아래 표에서 오류 코드, 메시지 및 관찰 된 구성 상태에 따라 수행할 작업이의 목록입니다.


| **코드**| **메시지**| **동작**|  
|--------|-----------|----------|  
| 알 수 없음| 알 수 없는 오류| |  
| HostUnreachable                       | 호스트 컴퓨터에 연결할 수 없다는 | 네트워크 컨트롤러와 호스트 간의 네트워크 연결을 관리 확인 |  
| PAIpAddressExhausted                  | PA Ip 주소가 모두 사용된 했습니다. | HNV 공급자 논리 서브넷의 IP 풀 크기 늘리기 |  
| PAMacAddressExhausted                 | PA Mac 주소를 모두 사용된 했습니다. | Mac 풀 범위를 넓힐 |  
| PAAddressConfigurationFailure         | 호스트에 대 한 PA 주소 전문가가 연결 하지 못했습니다. | 네트워크 컨트롤러와 호스트 간의 관리 네트워크 연결을 확인 합니다. |  
| CertificateNotTrusted                 | 인증서를 신뢰할 수 없는 경우  |호스트와의 통신에 사용 되는 인증서를 수정 합니다. |  
| CertificateNotAuthorized              | 권한이 없는 인증서 | 호스트와의 통신에 사용 되는 인증서를 수정 합니다. |  
| PolicyConfigurationFailureOnVfp       | VFP 정책 구성에 실패 | 런타임 오류입니다.  없음 정해진 해결 합니다. 로그를 수집 합니다. |  
| PolicyConfigurationFailure            | 통신 오류 또는 다른 사용자로 인해 호스트에 정책을 푸시하여의 오류는 NetworkController에 오류가 있습니다.| 전체 작업이 없습니다.  이 목표 상태 네트워크 컨트롤러 모듈에서 처리 하는 동안 오류가 발생 합니다. 로그를 수집 합니다. |  
| HostNotConnectedToController          | 호스트는 네트워크 컨트롤러에 아직 연결 되지 않은 | 포트 프로필의 호스트 또는 호스트에 적용 되지 않았습니다 네트워크 컨트롤러에서 연결 되지 않습니다. HostID 레지스트리 키에는 서버 리소스의 인스턴스 ID와 일치 하는지 확인 합니다. |  
| MultipleVfpEnabledSwitches            | 여러 VFp 호스트에서 스위치를 사용 하도록 설정  | 네트워크 컨트롤러 호스트 에이전트만는 지원 하므로 하나의 vSwitch VFP 확장을 사용 하는 사용 되는 스위치 중 하나를 삭제합니다 |  
| PolicyConfigurationFailure            | 인증서 오류 또는 연결 오류로 인해 VmNic VNet 정책을 푸시 하지 못했습니다.  | 적절 한 인증서가 배포 되었는지 확인 하십시오 (호스트의 FQDN 인증서 주체 이름은 일치 해야 합니다). 또한 네트워크 컨트롤러를 호스트 연결 확인 |  
| PolicyConfigurationFailure            | 인증서 오류 또는 연결 오류로 인해 VmNic vSwitch 정책을 푸시 하지 못했습니다.  | 적절 한 인증서가 배포 되었는지 확인 하십시오 (호스트의 FQDN 인증서 주체 이름은 일치 해야 합니다). 또한 네트워크 컨트롤러를 호스트 연결 확인|
| PolicyConfigurationFailure            | 인증서 오류 또는 연결 오류로 인해 VmNic에 대 한 방화벽 정책을 푸시 하지 못했습니다. | 적절 한 인증서가 배포 되었는지 확인 하십시오 (호스트의 FQDN 인증서 주체 이름은 일치 해야 합니다). 또한 네트워크 컨트롤러를 호스트 연결 확인|
| DistributedRouterConfigurationFailure | 호스트 vNic에 분산 라우터 설정을 구성 하지 못했습니다.                          | TCPIP 스택 오류가 발생 했습니다. 이 오류를 보고 서버에서 PA 및 DR 호스트 vNICs를 정리 해야 할 수 있습니다. |
| DhcpAddressAllocationFailure          | VMNic에 대 한 DHCP 주소를 할당 하지 못했습니다.                                                    | NIC 리소스에 대해 정적 IP 주소 특성은 구성 확인 |  
| CertificateNotTrusted<br>CertificateNotAuthorized | 네트워크 또는 인증 오류로 인해 Mux에 연결 하지 못했습니다. | 오류 메시지 코드에 제공 된 숫자 코드를 확인 하십시오: winsock 오류 코드에 해당 합니다. 인증서 오류 세분화 됩니다 (예를 들어 인증서를 확인할 수 없으면 cert 권한이 없는 등이 있습니다.) |  
| HostUnreachable                       | MUX은 비정상 (일반적인 경우 BGPRouter 연결 끊김) | RRAS (BGP 가상 컴퓨터) 또는 위쪽-Tor () 스위치에 대 한 BGP 피어를 성공적으로 액세스할 수 없거나 하지 피어 링입니다. 소프트웨어 부하 분산 장치 멀티플렉서 리소스와 BGP 피어 (ToR 또는 RRAS 가상 컴퓨터)에서 BGP 설정을 확인합니다 |  
| HostNotConnectedToController          | SLB 호스트 에이전트에 연결 되어 있지 않습니다.  | SLB 호스트 에이전트 서비스가 실행 중인지 확인 같은 이유로 SLB 호스트 에이전트 로그 (자동 실행)를 참조 이유, SLBM (NC) 실행 되는 호스트 에이전트를 제공한 인증서를 거부 하는 경우 상태 정보가 표시 됩니다 미묘한  |  
| PortBlocked                           | VNET의 부족으로 인해 VFP 포트는 차단 됩니다 / ACL 정책 | 다른 오류를 정책을 구성 하지 않을 수를 확인 합니다. |  
| 오버로드됨                            | Loadbalancer MUX 오버 로드  | MUX 성능 문제 |  
| RoutePublicationFailure               | Loadbalancer MUX BGP 라우터에 연결 되지 않은 | 가 MUX에 BGP 라우터 연결, 그리고 해당 BGP 피어 링가 제대로 설치 확인 |  
| VirtualServerUnreachable              | Loadbalancer MUX SLB 관리자에 연결 되지 않은 | SLBM 및 MUX 간 연결 확인 |  
| QosConfigurationFailure               | QOS 정책을 구성 하지 못했습니다. | QOS 예약을 사용 하는 경우 모든 VM에 대해 사용 가능한 충분 한 대역폭이 있는지 |


#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>네트워크 컨트롤러와 Hyper-v 호스트 (NC 호스트 에이전트 서비스) 간의 네트워크 연결 확인
실행 된 *netstat* NC 호스트 에이전트 및 네트워크 컨트롤러 노드 Hyper-v 호스트에 하나의 수신 대기 소켓 사이 세 개의 설정 되었음 연결을 확인 하려면 아래 명령을
- Hyper-v 호스트 (NC 호스트 에이전트 서비스)에서 포트 TCP:6640에서 수신 대기
- Hyper-v에서 설정 된 연결은 두 개의 임시 포트 (> 32000)에서 NC 노드 IP 포트 6640 IP를 호스트합니다.
- 네트워크 컨트롤러 REST ip 포트 6640에서 임시 포트에 Hyper-v 호스트 IP에서 설정 된 하나의 연결

>[!NOTE]
>있을 수 있습니다만 Hyper-v 호스트에 설정 된 두 개의 연결이 해당 호스트에 배포 된 테 넌 트 가상 컴퓨터가 없는 경우.

```none
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```
#### <a name="check-host-agent-services"></a>호스트 에이전트 서비스를 확인 합니다.
네트워크 컨트롤러는 Hyper-v 호스트에 두 개의 호스트 에이전트 서비스와 통신합니다. SLB 호스트 에이전트 및 NC 호스트 에이전트입니다. 이러한 서비스 중 하나 또는 모두가 실행 하지는 것 같습니다. 상태를 확인 하 고 실행 되지 않는 경우 다시 시작 하십시오.

```none
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>네트워크 컨트롤러의 상태를 확인 합니다.
세 개의 설정 되었음 연결 하지 않거나 네트워크 컨트롤러 나타나는 응답 하지 않는 경우 하 모든 노드와 서비스 모듈은 작동 하 고 다음 cmdlet을 사용 하 여 확인 합니다. 

```none
# Prints a DIFF state (status is automatically updated if state is changed) of a particular service module replica 
Debug-ServiceFabricNodeStatus [-ServiceTypeName] <Service Module>
```
네트워크 컨트롤러 서비스 모듈에는
- ControllerService
- ApiService
- SlbManagerService
- ServiceInsertion
- FirewallService
- VSwitchService
- GatewayManager
- FnmService
- HelperService
- UpdateService

ReplicaStatus 인지 확인 **준비** HealthState 이며 **확인**합니다.

다중 노드 네트워크 컨트롤러와 프로덕션 배포는 각 서비스에 기본는 노드 및 개별 복제 상태를 확인할 수도 있습니다.

```none  
Get-NetworkControllerReplica

# Sample Output for the API service module 
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready

```
복제본 상태가 준비 인지 확인 하십시오. 각 서비스에 대 한 합니다.

#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>해당 HostIDs 및 네트워크 컨트롤러 및 각 Hyper-v 호스트 간에 인증서 확인 
HostID 네트워크 컨트롤러에서 서버 리소스의 인스턴스 Id에 해당 하는지 확인 하려면 다음 명령을 실행 하는 Hyper-v 호스트에서

```none
Get-ItemProperty "hklm:\system\currentcontrolset\services\nchostagent\parameters" -Name HostId |fl HostId

HostId : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**

Get-NetworkControllerServer -ConnectionUri $uri |where { $_.InstanceId -eq "162cd2c8-08d4-4298-8cb4-10c2977e3cfe"}

Tags             :
ResourceRef      : /servers/4c4c4544-0056-4a10-8059-b8c04f395931
InstanceId       : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**
Etag             : W/"50f89b08-215c-495d-8505-0776baab9cb3"
ResourceMetadata : Microsoft.Windows.NetworkController.ResourceMetadata
ResourceId       : 4c4c4544-0056-4a10-8059-b8c04f395931
Properties       : Microsoft.Windows.NetworkController.ServerProperties
```

*업데이트 관리* 경우 SDNExpress를 사용 하 여 스크립트 또는 수동 배포 업데이트 서버 리소스의 인스턴스 Id와 일치 하도록 레지스트리에서 HostId 키입니다. VMM을 사용 하 여 VMM에서 Hyper-v 서버를 삭제 하는 경우에 Hyper-v 호스트 (실제 서버)의 네트워크 컨트롤러 호스트 에이전트를 다시 시작 하 고 HostId 레지스트리 키를 제거 합니다. 그런 다음 VMM 통해 서버를 다시 추가 합니다.


(호스트 이름이 인증서의 주체 이름 수는) Hyper-v 호스트에서 Hyper-v 호스트 (NC 호스트 에이전트 서비스)와 네트워크 컨트롤러 노드 간의 (SouthBound) 통신에 사용 되는 X.509 인증서의 지문이 동일한 지 확인 합니다. 또한 네트워크 컨트롤러의 REST 인증서의 주체 이름에 있는지를 확인 *CN =<FQDN or IP>* 합니다.

```  
# On Hyper-V Host
dir cert:\\localmachine\my  

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
...

dir cert:\\localmachine\root

Thumbprint                                Subject
----------                                -------
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**

# On Network Controller Node VM
dir cert:\\localmachine\root  

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**
...
```  

각 인증서 주체 이름 이란 인지 확인 하려면 다음 매개 변수를 확인할 수도 있습니다 (호스트 이름 또는 NC REST FQDN 또는 IP)를 예상 및 신뢰할 수 있는 루트 인증 기관에 모든 인증 기관 인증서 체인에 포함 된 인증서가 아직 만료 되지 않습니다.

- 주체 이름  
- 만료 날짜  
- 루트 기관에서 신뢰할 수 있는  

*업데이트 관리* 여러 인증서가 동일한 주체 이름을 Hyper-v 호스트에서 네트워크 컨트롤러 호스트 에이전트는 임의로 선택 네트워크 컨트롤러에 게 제공 하는 하나입니다. 네트워크 컨트롤러에 알려진 서버 리소스의 지 문으로 일치 하지 않을 수 있습니다. 이 경우 Hyper-v 호스트에 동일한 주체 이름 가진 인증서 중 하나를 삭제 하 고 네트워크 컨트롤러 호스트 에이전트 서비스를 다시 시작 합니다. 연결을 계속 설정할 수 없습니다, Hyper-v 호스트에 동일한 주체 이름 가진 다른 인증서를 삭제 하 고 VMM에서 해당 하는 서버 리소스를 삭제 합니다. 그런 다음 새 X.509 인증서를 생성 되며 Hyper-v 호스트에 설치 된 VMM에서 서버 리소스를 다시 만듭니다.


#### <a name="check-the-slb-configuration-state"></a>SLB 구성 상태를 확인 합니다.
디버그 NetworkController cmdlet으로 출력의 일부로 SLB 구성 상태를 확인할 수 있습니다. 이 cmdlet은 JSON 파일, 각 Hyper-v 호스트 (서버)에서 모든 IP 구성을 호스트 에이전트 데이터베이스 테이블에서 로컬 네트워크 정책에서 네트워크 컨트롤러 리소스의 현재 집합을 출력도. 

추가 추적 기본적으로 수집 됩니다. 추적을 수집 하지 않으려면, 추가-IncludeTraces: $false 매개 변수입니다.

```none
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential 
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>기본 출력 위치는 < working_directory > \NCDiagnostics\ 디렉터리 됩니다. 사용 하 여 기본 출력 디렉터리를 변경할 수는 `-OutputDirectory` 매개 변수입니다. 

SLB 구성 상태 정보를 찾을 수는 _진단 slbstateResults.Json_ 이 디렉터리의 파일입니다.

다음 섹션으로이 JSON 파일을 구분할 수 있습니다.
 * 패브릭
   * SlbmVips-이 섹션의 SLB 관리자 VIP 주소 coodinate 구성 및 상태 SLB Muxes와 SLB 호스트 에이전트 간의 네트워크 컨트롤러에서 사용 되는 IP 주소를 나열 합니다.
   * MuxState-이 섹션은 하나의 값에 나열 각 SLB 먹 싱 배포는 mux의 상태를 제공 합니다.
   * 라우터 구성-이 섹션에는 업스트림 라우터 (BGP 피어) 나열 됩니다 번호 ASN (Autonomous System), 전송 중인 IP 주소 및 id입니다. 또한 SLB Muxes ASN 및 전송 IP 나열 됩니다.
   * 호스트 정보-이 섹션에 연결 된 목록 관리 IP 다룰 모든 Hyper-v 호스트 부하 분산 된 작업을 실행할 수 있습니다.
   * Vip 범위-이 섹션은 공용 및 프라이빗 VIP IP 풀 범위를 나열합니다. SLBM VIP는 이러한 범위 중 하나에서 할당 된 IP로 포함 됩니다. 
   * Mux 경로-이 섹션에 대 한 각 SLB 먹 싱 배포 된 모든 해당 특정 mux에 대 한 경로 알림에 포함 된 하나의 값을 나열 됩니다.
 * 테넌트
   * VipConsolidatedState-이 섹션 보급 된 경로 접두사, Hyper-v 호스트 및 DIP 끝점을 포함 하 여 각 테 넌 트 VIP에 대 한 연결 상태를 나열 됩니다.

> [!NOTE]
> SLB 상태를 사용 하 여 직접 조사할 수 있습니다는 [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) 스크립트에서 사용할 수는 [Microsoft SDN GitHub 리포지토리](https://github.com/microsoft/sdn)합니다. 

#### <a name="gateway-validation"></a>게이트웨이 유효성 검사

**네트워크 컨트롤러:**
```
Get-NetworkControllerLogicalNetwork
Get-NetworkControllerPublicIPAddress
Get-NetworkControllerGatewayPool
Get-NetworkControllerGateway
Get-NetworkControllerVirtualGateway
Get-NetworkControllerNetworkInterface
```

**게이트웨이 VM:**
```
Ipconfig /allcompartments /all
Get-NetRoute -IncludeAllCompartments -AddressFamily
Get-NetBgpRouter
Get-NetBgpRouter | Get-BgpPeer
Get-NetBgpRouter | Get-BgpRouteInformation
```

**Tor () 스위치의 위에서:**

`sh ip bgp summary (for 3rd party BGP Routers)`

**Windows BGP 라우터**
```
Get-BgpRouter
Get-BgpPeer
Get-BgpRouteInformation
```

이외에도, (특히 SDNExpress 기반 배포의 경우)에서 지금까지 살펴본 문제에서 테 넌 트 구획 가져오기에 구성 되어 있지 GW Vm에 대 한 가장 일반적인 이유를 찾을 수 있다는 사실을 FabricConfig.psd1의 GW 용량 작은에서 비해 네트워크 연결 (S2S 터널)에 할당 하려고 하는 담당자 TenantConfig.psd1 합니다. 다음 명령 중 출력을 비교 하 여 쉽게 확인할 수 있습니다.

```
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>[호스터] 평면 데이터의 유효성을 검사합니다
네트워크 컨트롤러 배포한 하 고 테 넌 트 가상 네트워크 및 서브넷을 만든 가상 서브넷에 연결 된 Vm, 후 호스터 테 넌 트 연결을 확인 하 여 추가 패브릭 수준 테스트를 수행할 수 있습니다.

#### <a name="check-hnv-provider-logical-network-connectivity"></a>HNV 공급자 논리 네트워크 연결 확인
네트워크 컨트롤러 VM을 Hyper-v 호스트에서 실행 되는 테 넌 트 가상 네트워크에 연결 하는 첫 번째 게스트 후 Hyper-v 호스트에 두 개의 HNV 공급자 IP 주소 (PA IP 주소)를 할당 합니다. 이러한 Ip는 HNV 공급자 논리 네트워크의 IP 풀에서 옵니다 네트워크 컨트롤러에서 관리 합니다.  이 두 HNV IP 주소를 찾도록 하의

```none
PS > Get-ProviderAddress

# Sample Output
ProviderAddress : 10.10.182.66
MAC Address     : 40-1D-D8-B7-1C-04
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11

ProviderAddress : 10.10.182.67
MAC Address     : 40-1D-D8-B7-1C-05
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11
```

이러한 HNV 공급자 IP 주소 (PA Ip)는 별도 TCPIP 네트워크 구획에서 만든 이더넷 어댑터에 할당 되어 있고의 어댑터 이름을 _VLANX_ 여기서 X는 HNV 공급자 (전송) 논리 네트워크에 할당 된 VLAN입니다.

논리 네트워크는 추가 구획이 있는 ping 하 여 수행할 수 있습니다 HNV 공급자를 사용 하는 두 Hyper-v 호스트 간 연결 (-c Y) 매개 변수 Y는 PAhostVNICs 만들어집니다 TCPIP 네트워크 구획입니다. 실행 하 여이 구획을 확인할 수 있습니다.

```none
C:\> ipconfig /allcompartments /all

<snip> ...
==============================================================================
Network Information for *Compartment 3*
==============================================================================
   Host Name . . . . . . . . . . . . : SA18n30-2
<snip> ...

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-04
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::5937:a365:d135:2899%39(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.66(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-05
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::28b3:1ab1:d9d9:19ec%44(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.67(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

*Ethernet adapter vEthernet (PAhostVNic):*
<snip> ...
```

>[!NOTE]
> PA 호스트 vNIC 어댑터의 데이터 경로에 사용 되지 않으며 따라서 "vEthernet (PAhostVNic)"어댑터에 할당 된 IP를 갖지 않습니다.

예를 들어, 가정 Hyper-v 호스트 1과 2의 HNV PA (공급자) IP 주소:

|Hyper-v 호스트-|-1 PA IP 주소|-2 PA IP 주소|
|---             |---            |---             |
|호스트 1 | 10.10.182.64 | 10.10.182.65 |
|호스트 2 | 10.10.182.66 | 10.10.182.67 |

다음 명령을 사용 하 여 HNV 공급자 논리 네트워크 연결을 확인 하 고 둘 사이의 ping 할 수 있습니다.

```none
# Ping the first PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.64

# Ping the second PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.64

# Ping the first PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.65

# Ping the second PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.65
```

*업데이트 관리* 경우 HNV 공급자 ping 작업을 VLAN 구성을 포함 하 여 실제 네트워크 연결을 확인 하지 않습니다. 각 Hyper-v 호스트의 실제 Nic 할당 없는 특정 vlan 트렁크 모드에 있어야 합니다. 관리 호스트 vNIC 관리 논리 네트워크의 VLAN에 격리 되어야 합니다.

```none
PS C:\> Get-NetAdapter "Ethernet 4" |fl

Name                       : Ethernet 4
InterfaceDescription       : <NIC> Ethernet Adapter
InterfaceIndex             : 2
MacAddress                 : F4-52-14-55-BC-21
MediaType                  : 802.3
PhysicalMediaType          : 802.3
InterfaceOperationalStatus : Up
AdminStatus                : Up
LinkSpeed(Gbps)            : 10
MediaConnectionState       : Connected
ConnectorPresent           : True
*VlanID                     : 0*
DriverInformation          : Driver Date 2016-08-28 Version 5.25.12665.0 NDIS 6.60

# VMM uses the older PowerShell cmdlet <Verb>-VMNetworkAdapterVlan to set VLAN isolation
PS C:\> Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName <Mgmt>

VMName VMNetworkAdapterName Mode     VlanList
------ -------------------- ----     --------
<snip> ...        
       Mgmt                 Access   7
<snip> ...

# SDNExpress deployments use the newer PowerShell cmdlet <Verb>-VMNetworkAdapterIsolation to set VLAN isolation
PS C:\> Get-VMNetworkAdapterIsolation -ManagementOS

<snip> ...

IsolationMode        : Vlan
AllowUntaggedTraffic : False
DefaultIsolationID   : 7
MultiTenantStack     : Off
ParentAdapter        : VMInternalNetworkAdapter, Name = 'Mgmt'
IsTemplate           : True
CimSession           : CimSession: .
ComputerName         : SA18N30-2
IsDeleted            : False

<snip> ...
```

#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>HNV 공급자 논리 네트워크에서 MTU 및 점보 프레임 지원 확인

또 다른 일반적인 문제는 HNV 공급자 논리 네트워크에서 실제 네트워크 포트 및/또는 이더넷 카드에의 VXLAN (또는 NVGRE) 캡슐화 하는 오버 헤드를 처리 하도록 구성 하는 충분히 큰 MTU 없는 경우 
>[!NOTE]
> 일부 이더넷 카드 및 드라이버 지원 새 * EncapOverhead 키워드 160 값으로 네트워크 컨트롤러 호스트 에이전트에 의해 자동으로 설정 됩니다. 이 값 다음의 값에 추가할 합니다 * JumboPacket 키워드 해당 합계 보급된 된 MTU로 사용 됩니다.
> 예: * EncapOverhead = 160 및 * JumboPacket 1514 = = > MTU 1674B =

```none
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

HNV 공급자 논리 네트워크가 더 큰 MTU 크기를 엔드투엔드 지원하는지 테스트하려면 _Test-LogicalNetworkSupportsJumboPacket_ cmdlet을 사용합니다.
```none
# Get credentials for both source host and destination host (or use the same credential if in the same domain)
$sourcehostcred = Get-Credential
$desthostcred = Get-Credential

# Use the Management IP Address or FQDN of the Source and Destination Hyper-V hosts
Test-LogicalNetworkSupportsJumboPacket -SourceHost sa18n30-2 -DestinationHost sa18n30-3 -SourceHostCreds $sourcehostcred -DestinationHostCreds $desthostcred

# Failure Results
SourceCompartment : 3
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1632
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1472
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.

# TODO: Success Results aftering updating MTU on physical switch ports
```

*업데이트 관리*
* 적어도 물리적 스위치 포트에서 MTU 크기 조정 1674B (14B 이더넷 헤더 및 트레일러 포함)
* NIC 카드 EncapOverhead 키워드를 지원 하지 않는 경우 조정 적어도 JumboPacket 키워드 1674B


#### <a name="check-tenant-vm-nic-connectivity"></a>테 넌 트 VM NIC 연결 확인
게스트 VM에 할당 된 각 VM NIC에 프라이빗 고객 주소(CA)와 HNV PA (공급자 주소) 공간 간의 CA-PA 매핑이 있습니다. 이러한 매핑은 각 Hyper-v 호스트에서 OVSDB 서버 테이블에 유지 되 고 다음 cmdlet을 실행 하 여 찾을 수 있습니다.

```none
# Get all known PA-CA Mappings from this particular Hyper-V Host
PS > Get-PACAMapping

CA IP Address CA MAC Address    Virtual Subnet ID PA IP Address
------------- --------------    ----------------- -------------
10.254.254.2  00-1D-D8-B7-1C-43              4115 10.10.182.67
10.254.254.3  00-1D-D8-B7-1C-43              4115 10.10.182.67
192.168.1.5   00-1D-D8-B7-1C-07              4114 10.10.182.65
10.254.254.1  40-1D-D8-B7-1C-06              4115 10.10.182.66
192.168.1.1   40-1D-D8-B7-1C-06              4114 10.10.182.66
192.168.1.4   00-1D-D8-B7-1C-05              4114 10.10.182.66
```
>[!NOTE]
> 예상 CA-PA 매핑은 지정된 테 넌 트 VM에 대 한 출력 되지는 않습니다, 경우에 사용 하 여 네트워크 컨트롤러 VM NIC 및 IP 구성 리소스를 확인 하십시오는 _Get NetworkControllerNetworkInterface_ cmdlet입니다. 또한 NC 호스트 에이전트 및 네트워크 컨트롤러 노드 간에 설정 된 연결을 확인 합니다.

이 정보를 사용 하는 테 넌 트 VM ping 이제에서 시작할 수 사용 하 여 네트워크 컨트롤러에서 호스터는 _테스트 VirtualNetworkConnection_ cmdlet입니다.

## <a name="specific-troubleshooting-scenarios"></a>특정 문제 해결 시나리오

다음 섹션에서는 특정 시나리오를 해결 하기 위한 지침을 제공 합니다.

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>두 개의 테 넌 트 가상 컴퓨터 간 네트워크 연결 없음

1.  [Tenant] 테 넌 트 가상 컴퓨터에서 Windows 방화벽이 트래픽을 차단 하지 확인 합니다.  
2.  [Tenant] IP 주소를 실행 하 여 테 넌 트 가상 컴퓨터에 할당 된 있는지 확인 하십시오. _ipconfig_합니다. 
3.  [호스터] 실행할 **테스트 VirtualNetworkConnection** 문제의 두 테 넌 트 가상 컴퓨터 간의 연결의 유효성을 검사 하는 Hyper-v 호스트에서. 

>[!NOTE]
>Vsid가 참조 된 가상 서브넷 id. VXLAN의 경우는 VXLAN 네트워크 식별자 (vni) 또는입니다. 실행 하 여이 값을 찾을 수 있습니다 합니다 **Get PACAMapping** cmdlet.

#### <a name="example"></a>예제

    $password = ConvertTo-SecureString -String "password" -AsPlainText -Force
    $cred = New-Object pscredential -ArgumentList (".\administrator", $password) 

CA-ping 녹색 봚 VM 1"의 호스트에서 192.168.1.4 SenderCA IP를 사용 하 여 간에" sa18n30-2.sa18.nttest.microsoft.com "ListenerCA ip 10.127.132.153 Mgmt IP를 사용 하 여 둘 다 연결에 가상 서브넷 (VSID) 4114 192.168.1.5의 만듭니다.

    Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114

    Test-VirtualNetworkConnection at command pipeline position 1

시작 CA 공간 ping 테스트 192.168.1.4 주소의 성공 192.168.1.5 Ping 추적 세션을 시작 Rtt = 0ms


CA 라우팅 정보:

    Local IP: 192.168.1.4
    Local VSID: 4114
    Remote IP: 192.168.1.5
    Remote VSID: 4114
    Distributed Router Local IP: 192.168.1.1
    Distributed Router Local MAC: 40-1D-D8-B7-1C-06
    Local CA MAC: 00-1D-D8-B7-1C-05
    Remote CA MAC: 00-1D-D8-B7-1C-07
    Next Hop CA MAC Address: 00-1D-D8-B7-1C-07

PA 라우팅 정보:

    Local PA IP: 10.10.182.66
    Remote PA IP: 10.10.182.65

 <snip> ...

4. [Tenant] 가상 서브넷 이나 트래픽을 차단 하는 VM 네트워크 인터페이스에 지정 된 분산된 방화벽 정책이 없습니다 인지 확인 합니다.    

Sa18.nttest.microsoft.com 도메인 있는 sa18n30nc 데모 환경에서 네트워크 컨트롤러 REST API를 쿼리 합니다.

    $uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
    Get-NetworkControllerAccessControlList -ConnectionUri $uri 

# <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>IP 구성 및 가상 서브넷이이 ACL을 참조 하는 확인

1. [호스터] 실행 ``Get-ProviderAddress`` 두 hyper-v 호스트 두 호스팅 질문의 가상 컴퓨터를 테 넌 트 한 다음 실행 ``Test-LogicalNetworkConnection`` 또는 ``ping -c <compartment>`` HNV 공급자 논리 네트워크에 대 한 연결 유효성을 검사 하는 Hyper-v 호스트에서
2.  [호스터] Hyper-v 호스트에 올바른 및 모든 계층 2 장치 사이 Hyper-v 호스트를 전환 MTU 설정 되어 있는지 확인 합니다. 실행 ``Test-EncapOverheadValue`` 에 모든 Hyper-v 호스트에 있습니다. 또한 확인 사이 있는 모든 계층 2 스위치 MTU 160 바이트의 최대 오버 헤드를 고려 하 1674 바이트 이상으로 설정 합니다.  
3.  [호스터] PA IP 주소가 없는 경우, CA 연결이 끊어진 네트워크 정책을 받은 있는지 확인 합니다. 실행 ``Get-PACAMapping`` 캡슐화 규칙 및 오버레이 가상 네트워크를 만드는 데 필요한 CA-PA 매핑은 올바르게 설정 하는 경우를 확인 합니다.  
4.  [호스터] 네트워크 컨트롤러 호스트 에이전트가 네트워크 컨트롤러에 연결 되어 있는지 확인 합니다. 실행 ``netstat -anp tcp |findstr 6640`` 있는지는   
5.  [호스터] HKLM에 호스트 ID 확인 / 테 넌 트 가상 컴퓨터를 호스팅하는 서버 리소스의 인스턴스 ID와 일치 합니다.  
6. [호스터] 포트 프로필 ID 테 넌 트 가상 컴퓨터의 VM 네트워크 인터페이스의 인스턴스 ID와 일치 하는지 확인 합니다.  

## <a name="logging-tracing-and-advanced-diagnostics"></a>로깅, 추적 및 고급 진단

다음 섹션에서는 고급 진단에서 로깅 및 추적 정보를 제공 합니다.

### <a name="network-controller-centralized-logging"></a>네트워크 컨트롤러 중앙 집중식으로 로깅 

자동으로 네트워크 컨트롤러 디버거 로그를 수집 하 고 중앙 집중화 된 위치에 저장할 수 있습니다. 처음으로 또는 나중에 모든 시간에 대 한 네트워크 컨트롤러를 배포 하는 경우 로그 수집을 사용할 수 있습니다. 로그의 네트워크 컨트롤러에서 수집 되 고 네트워크 네트워크 컨트롤러가 관리 하는 요소: 컴퓨터, 소프트웨어 부하 분산 장치 (SLB) 및 게이트웨이 컴퓨터를 호스트 합니다. 

이러한 로그 네트워크 컨트롤러 클러스터, 네트워크 컨트롤러 응용 프로그램, 게이트웨이 로그, SLB, 가상 네트워킹 및 분산된 방화벽에 대 한 디버그 로그를 포함 합니다. 새 호스트/SLB/게이트웨이 네트워크 컨트롤러에 추가 되 면 때마다 로깅 해당 컴퓨터에서 시작 됩니다. 마찬가지로, 호스트/SLB/게이트웨이 네트워크 컨트롤러에서 제거 되 면 해당 컴퓨터에서 로깅이 중지 됩니다.

#### <a name="enable-logging"></a>로깅 사용

자동으로 로깅을 사용 하 여 네트워크 컨트롤러 클러스터를 설치 합니다 **설치 NetworkControllerCluster** cmdlet. 기본적으로 로그는 로컬로 수집의 네트워크 컨트롤러 노드에서 *%systemdrive%\SDNDiagnostics*합니다. **좋습니다** 이 위치를 원격 파일 공유 (로컬) 수를 변경 하는 합니다. 

네트워크 컨트롤러 클러스터 로그에 저장 된 *%programData%\Windows Fabric\log\Traces*합니다. 사용 하 여 로그 수집을 위해 중앙된 위치를 지정할 수 있습니다 합니다 **DiagnosticLogLocation** 매개 변수 이기도 된 권장 구성이 사용할 원격 파일 공유 합니다. 

이 위치에 대 한 액세스를 제한 하려는 경우에 액세스 자격 증명을 제공할 수 있습니다 합니다 **LogLocationCredential** 매개 변수입니다. 또한 제공 해야 로그 위치에 액세스 하려면 자격 증명을 제공 하는 경우는 **CredentialEncryptionCertificate** 네트워크 컨트롤러 노드에 로컬로 저장 된 자격 증명을 암호화 하는 데 사용 되는 매개 변수입니다.  

기본 설정으로 했을 때 최소 75 g B의 여유 공간이 25GB 고 중앙 위치에서 로컬 노드 (중앙 위치를 사용 하지) 네트워크 컨트롤러 3 노드 클러스터에 대 한 것이 좋습니다.

#### <a name="change-logging-settings"></a>로깅 설정 변경

로깅 설정을 사용 하는 모든 시간에 변경할 수는 ``Set-NetworkControllerDiagnostic`` cmdlet입니다. 다음 설정은 변경할 수 있습니다.

- **로그 위치를 중앙 집중식**합니다.  적용 된 모든 로그를 저장 하는 위치를 변경할 수는 ``DiagnosticLogLocation`` 매개 변수입니다.  
- **로그 위치에 액세스 하려면 자격 증명**합니다.  로그 위치와 액세스 하는 데 사용할 자격 증명을 변경할 수는 ``LogLocationCredential`` 매개 변수입니다.  
- **로컬 로깅으로 이동**합니다.  로그를 저장 하는 중앙된 위치를 입력 한 경우 다시 이동할 수 있습니다 사용 하 여 네트워크 컨트롤러 노드를 로컬로 로그온 하는 ``UseLocalLogLocation`` 매개 변수 (많은 디스크 공간 요구 사항으로 인해 권장 하지 않음).  
- **로깅 범위**합니다.  기본적으로 모든 로그가 수집 됩니다. 유일한 네트워크 컨트롤러 클러스터 로그를 수집 하도록 범위를 변경할 수 있습니다.  
- **로깅 수준**합니다.  기본 로깅 수준을 정보입니다. 오류, 경고 또는 자세한 정보 표시를 변경할 수 있습니다.  
- **로그 시간을 에이징**합니다.  로그는 순환 방식으로 저장 됩니다. 로컬 로깅 또는 중앙된 로깅이 기본적으로 로깅 데이터의 3 일을 해야 합니다. 이 시간 제한을 사용 하 여 변경할 수 있습니다 **LogTimeLimitInDays** 매개 변수입니다.  
- **로그 크기 일 유예 기간**합니다.  기본적으로 로컬 로깅을 사용 하는 경우 중앙 집중식된 로깅 및 25GB를 사용 하는 경우 로깅 데이터의 최대 75GB를 해야 합니다. 사용 하 여이 제한을 변경할 수 있습니다 합니다 **LogSizeLimitInMBs** 매개 변수입니다.

#### <a name="collecting-logs-and-traces"></a>로그 수집 및 추적

VMM 배포는 기본적으로 네트워크 컨트롤러에 대 한 중앙 집중식된 로깅을 사용합니다. 이러한 로그에 대 한 파일 공유 위치는 네트워크 컨트롤러 서비스 템플릿을 배포할 때 지정 됩니다.

파일 위치를 로컬 지정 되지 않은 경우 로깅은 C:\Windows\tracing\SDNDiagnostics로 저장 된 로그와 각 네트워크 컨트롤러 노드에 사용 됩니다. 이러한 로그는 다음과 같은 계층을 사용 하 여 저장 됩니다.

- 크래시 덤프
- NCApplicationCrashDumps
- NCApplicationLogs
- PerfCounters
- SDNDiagnostics
- 추적

네트워크 컨트롤러는 서비스 패브릭 (Azure)를 사용합니다. 서비스 패브릭 로그는 특정 문제를 해결할 때 필요할 수 있습니다. 네트워크 컨트롤러 노드마다 C:\ProgramData\Microsoft\Service 패브릭에서 이러한 로그를 볼 수 있습니다.

사용자가 실행 되는 경우는 _디버그 NetworkController_ cmdlet에 추가 로그의 네트워크 컨트롤러에서 서버 리소스와 함께 지정 하는 각 Hyper-v 호스트에서 사용할 수 있습니다. 이러한 로그 (및 추적이 사용 하도록 설정한 경우) C:\NCDiagnostics 이하로 유지 됩니다.

### <a name="slb-diagnostics"></a>SLB 진단

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>SLBM 패브릭 오류 (호스팅 서비스 공급자 동작)

1.  소프트웨어 부하 분산 장치 관리자 (SLBM) 작동 하 고 오케스트레이션 레이어가 서로 통신할 수를 확인 합니다. SLBM SLB Mux-> 하 고 SLBM SLB 호스트 에이전트. 실행 [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) 네트워크 컨트롤러 REST 끝점에 액세스할 수 있는 모든 노드에서 합니다.  
2.  유효성 검사는 *SDNSLBMPerfCounters* 네트워크 컨트롤러 노드 Vm (가급적 주 네트워크 컨트롤러 노드-Get NetworkControllerReplica) 중 하나에서 성능 모니터에서:
    1.  부하 분산 장치 (LB) 엔진 SLBM에 연결 되어 있습니까? (*SLBM LBEngine 구성 총* > 0)  
    2.  SLBM 적어도 알 자체 끝점에 대 한? (*VIP 끝점 총* > = 2)  
    3.  Hyper-v (DIP) 호스트 SLBM에 연결 되어 있습니까? (*연결 된 HP 클라이언트*  num 서버 = =)   
    4.  SLBM은 Muxes에 연결 되어 있습니까? (*Muxes 연결* == *Muxes Healthy on SLBM* == *Muxes 보고 정상* = # SLB Muxes Vm).  
3.  구성 된 BGP 라우터는 SLB MUX와 피어 링 성공적으로 확인 합니다.  
    1.  RRAS를 사용 하 여 원격 액세스 (예: BGP 가상 컴퓨터)와 하는 경우:  
        1.  Get bgppeer가 연결 된 나타나야 합니다.  
        2.  Get BgpRouteInformation는 SLBM에 대 한 최소한의 경로 표시 해야 자체 VIP  
    2.  BGP 피어로 전환 물리적-Top-of-rack ToR ()를 사용 하 여, 설명서를 참조 하십시오.  
        1.  예: # bgp 인스턴스를 보여 줍니다.  
4.  유효성 검사는 *SlbMuxPerfCounters* 및 *SLBMUX* SLB Mux VM에는 PerfMon 카운터
5.  구성 상태 및 소프트웨어 부하 분산 장치 관리자 리소스에 대 한 VIP 범위를 확인 합니다.  
    1.  Get NetworkControllerLoadBalancerConfiguration ConnectionUri < https://<FQDN or IP>| convertto json-8 깊이 (IP 풀의 VIP 범위 SLBM 자체 VIP를 확인 하십시오 (*LoadBalanacerManagerIPAddress*) 및 모든 테 넌 트 쪽 Vip는이 범위 내)  
        1. "< 공개/개인 VIP 논리 네트워크 리소스 ID >" get NetworkControllerIpPool-NetworkId-SubnetId "< 공개/개인 VIP 논리 서브넷 리소스 ID >"-ResourceId "<IP Pool Resource Id>"-ConnectionUri $uri | convertto json-8 깊이 
    2.  디버그-NetworkControllerConfigurationState-  

검사 실패 위의 경우에 실패 모드에 테 넌 트 SLB 상태 수도 있습니다.  

**업데이트 관리**   
제공 된 다음 진단 정보에 따릅니다, 다음 수정 합니다.  
* SLB 멀티플렉서 연결 되도록  
  * 인증서 문제 해결  
  * 네트워크 연결 문제 해결  
* BGP 피어 링 정보 성공적으로 구성 되어 있는지 확인  
* 서버 리소스에 있는 서버 인스턴스 ID를 일치 하는 레지스트리에서 호스트 ID 확인 (부록 d 참조 *HostNotConnected* 오류 코드)  
* 로그 수집  

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>테 넌 트 SLBM 오류 (호스팅 서비스 공급자 및 테 넌 트 작업)

1.  [호스터] 확인 *디버그 NetworkControllerConfigurationState* LoadBalancer 리소스 오류 상태에 있는지 확인 하기 위해. 부록에는 테이블 작업 항목에 따라 완화 하려고 합니다.   
    1.  VIP 끝점은 현재 및 광고 경로 인지 확인  
    2.  VIP 끝점에 대 한 검색 된 DIP 끝점 수 확인  
2.  [Tenant] 유효성을 검사 부하 분산 장치 리소스를 올바르게 지정  
    1.  DIP의 유효성을 검사 SLBM에 등록 되어 있는 끝점 LoadBalancer 백 엔드 주소 풀의 IP 구성에 해당 하는 테 넌 트 가상 컴퓨터를 호스트  
3.  [호스터] DIP 끝점 발견 하지 않거나 연결 합니다.   
    1.  확인 *NetworkControllerConfigurationState 디버그*  
        1.  해당 NC 유효성 검사 및 SLB 호스트 에이전트를 성공적으로 사용 하 여 네트워크 컨트롤러 행사 코디네이터에 연결 ``netstat -anp tcp |findstr 6640)``  
    2.  확인 *HostId* 에서 *nchostagent* 서비스 레지스트리 키 (참조 *HostNotConnected* 부록에 오류 코드) 해당 하는 서버 리소스의 인스턴스 Id와 일치 (``Get-NCServer |convertto-json -depth 8``)  
    3.  가상 컴퓨터 포트에 대 한 포트 프로필 id에 해당 가상 컴퓨터 NIC 리소스의 인스턴스 Id와 일치 확인   
4.  [호스팅 공급자] 로그 수집   

#### <a name="slb-mux-tracing"></a>SLB Mux 추적

소프트웨어 부하 분산 장치 Muxes의 정보는 또한 이벤트 뷰어를 통해 확인할 수 있습니다. 
1. 이벤트 뷰어 보기 메뉴에서 "표시 분석 및 디버그 로그"를 클릭 합니다.
2. "응용 프로그램 및 서비스 로그"로 이동 > Microsoft > Windows > SlbMuxDriver > 이벤트 뷰어에서 추적 
3. 마우스 오른쪽 단추로 클릭 하 고 "로그 사용"을 선택 합니다.

>[!NOTE]
>이 로깅 문제를 재현 하는 동안 잠시 사용 있다고 것이 좋습니다.

### <a name="vfp-and-vswitch-tracing"></a>VFP 및 vSwitch 추적

모든 Hyper-v에서 게스트 테 넌 트 가상 네트워크에 연결 하는 VM을 호스팅하는 호스트, 문제가 있을 수 있습니다 위치를 결정 하는 VFP 추적 수집 수 있습니다.

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch 
netsh trace stop
netsh trace convert .\vfp.etl ov=yes 
```
