---
title: Windows Server 소프트웨어 정의 네트워킹 스택 문제 해결
description: 이 Windows Server 가이드 소프트웨어 정의 네트워킹 (SDN) 일반적인 오류와 오류 시나리오를 검사 하 고 사용 가능한 진단 도구를 활용 하는 문제 해결 워크플로 간략하게 설명 합니다.
manager: ravirao
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: pashort
author: JMesser81
ms.openlocfilehash: af59ae6746467f9aecf384d1b3cf9af1e8baeb9a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Windows Server 소프트웨어 정의 네트워킹 스택 문제 해결

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 가이드 소프트웨어 정의 네트워킹 (SDN) 일반적인 오류와 오류 시나리오를 검사 하 고 사용 가능한 진단 도구를 활용 하는 문제 해결 워크플로 간략하게 설명 합니다.  

Microsoft의 소프트웨어 네트워킹 정의 대 한 자세한 내용은 참조 [소프트웨어 네트워킹 정의](../../sdn/Software-Defined-Networking--SDN-.md)합니다.  

## <a name="error-types"></a>오류 유형  
다음 목록 문제 Hyper-v 네트워크 가상화 (HNVv1) 흔히 볼 클래스 Windows Server 2012 r 2 마켓 내 프로덕션 배포에서 나타내고 같은 유형의와 새 소프트웨어 정의 네트워크 (SDN) 스택 HNVv2 Windows Server 2016에에서 표시 하는 문제는 여러 가지 방법으로 일치 합니다.  

대부분의 오류 클래스 작은 집합에 나눌 수 있습니다.   
* **잘못 된 또는 지원 되지 않는 구성**  
   사용자가 호출 잘못 또는 잘못 된 정책 NorthBound API 합니다.   

* **정책 응용 프로그램에서 오류**  
     네트워크 컨트롤러에서 정책 크게 지연 및/또는 모든 Hyper-v 호스트 (예를 들어, 후 실시간 마이그레이션)에서 최신 상태가 아닙니다 Hyper-v 호스트 배달 하지 못했습니다.  
* **구성, 바람 또는 소프트웨어 버그**  
 경로 데이터 문제 손실된 패킷을 발생 합니다.  

* **NIC 하드웨어 외부 오류와 관련 된 드라이버 또는 언더레이 네트워크 패브릭 /**  
 (예: VMQ) 작업 오프 로드 또는 (예: MTU) 잘못 구성 언더레이 네트워크 패브릭 것   

 이 문제 해결 가이드 각 이러한 오류 범주를 검사 하 고 유용한 및 진단 도구를 식별 하 고 오류 해결 사용할 수 있는 것을 권장 합니다.  

## <a name="diagnostic-tools"></a>진단 도구  

이러한 유형의 오류가 각각에 대 한 문제 해결 워크플로에 대해 논의 하기 전에 검토 진단 도구를 사용할 수 있습니다.   
  
네트워크 컨트롤러 (제어 경로) 진단 도구를 사용 하려면 먼저 RSAT NetworkController 기능을 설치를 가져올는 ``NetworkControllerDiagnostics``모듈:  

```  
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools  
Import-Module NetworkControllerDiagnostics  
```  

가져올 해야 HNV 진단 (경로 데이터) 진단 도구를 사용 하는 ``HNVDiagnostics``모듈:
  
```  
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics   
```  

### <a name="network-controller-diagnostics"></a>네트워크 컨트롤러 진단  
이러한 cmdlet에 technet 설명는 [네트워크 컨트롤러 진단 Cmdlet 항목](https://docs.microsoft.com/en-us/powershell/module/networkcontrollerdiagnostics/)합니다. 이러한 문제 네트워크 정책 일관성 및 네트워크 컨트롤러와 Hyper-v 호스트에서 실행 중인 NC 호스트 에이전트 네트워크 컨트롤러 노드 사이의 제어-경로를 알려줄 수 있습니다.

 _디버그 ServiceFabricNodeStatus_ 및 _Get NetworkControllerReplica_ cmdlet 네트워크 컨트롤러 노드 가상 컴퓨터 중 하나를 실행 해야 합니다. 다른 모든 NC 진단 cmdlet 모든 호스트 컨트롤러 네트워크에 연결 하 고 네트워크 컨트롤러 관리 보안 그룹 (Kerberos) 중 하나에 또는 네트워크 컨트롤러 관리 하기 위한 X.509 인증서에 액세스할 수 있는에서 실행할 수 있습니다. 
   
### <a name="hyper-v-host-diagnostics"></a>Hyper-v 호스트 진단  
이러한 cmdlet에 technet 설명는 [Hyper-v 네트워크 가상화 (HNV) 진단 Cmdlet 항목](https://docs.microsoft.com/en-us/powershell/module/hnvdiagnostics/)합니다. 테 가상 컴퓨터 (이스트/서쪽) 간에 경로 데이터의 문제를 파악 하는 데 도움이 및 SLB VIP (북쪽/사우스)를 통해 수신 교통 합니다. 

_디버그 VirtualMachineQueueOperation_, _Get CustomerRoute_, _Get PACAMapping_, _Get ProviderAddress_, _Get VMNetworkAdapterPortId_, _Get VMSwitchExternalPortId_, 및 _테스트 EncapOverheadSettings_ 는 어떤 Hyper-v 호스트에서 실행 될 수 있는 모든 로컬 테스트 합니다. 다른 cmdlet 네트워크 컨트롤러를 통해 데이터 경로 테스트를 실행 하 고 따라서 위의 descried으로 네트워크 컨트롤러에 액세스할 수 있어야 합니다.
 
### <a name="github"></a>GitHub
[Microsoft/SDN GitHub 악의적인](https://github.com/microsoft/sdn) 샘플 스크립트 및 위에 상자에서 cmdlet 이러한 빌드는 워크플로 수 있습니다. 특히, 진단 스크립트 있습니다는 [진단](https://github.com/Microsoft/sdn/diagnostics) 폴더 합니다. 꺼냅니다 요청을 제출 하 여 이러한 스크립트에 기여 하는 데 도움이 하세요.

## <a name="troubleshooting-workflows-and-guides"></a>워크플로 및 가이드 문제 해결  

### <a name="hoster-validate-system-health"></a>[호스팅] 시스템 상태 확인
이름이 포함된 된 리소스는 _구성 상태_ 에서 네트워크 컨트롤러 리소스 중 몇 가지 있습니다. 구성 상태 구성 네트워크 컨트롤러 및 Hyper-v 호스트에 실제 (실행) 상태 간의 일관성을 포함 하 여 시스템 상태에 대 한 정보를 제공 합니다. 

구성 상태를 확인 하려면 다음에서에서 실행 모든 Hyper-v 호스트 연결 네트워크 컨트롤러 합니다.

>[!NOTE] 
>에 대 한 값은 *NetworkController* 매개 해야 하거나 X.509의 제목 이름에 따라 FQDN 또는 IP 주소 > 인증서 네트워크 컨트롤러 용으로 작성 합니다.
>
>*자격 증명* 매개만 네트워크 컨트롤러 (VMM 배포 일반) Kerberos 인증을 사용 하는 경우 지정 해야 합니다. 네트워크 컨트롤러 관리 보안 그룹에 있는 사용자에 대 한 자격 증명 해야 합니다.

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
> 시스템 오류 "가상 스위치를-호스트 되지 연결에 컨트롤러"를 사용 하 여 실패 상태의 SLB Mux 교통 VM NIC에 대 한 네트워크 인터페이스 리소스는 어디에서 버그가 있습니다. VM NIC 리소스에 IP 구성 교통 논리 네트워크 IP 풀의 IP 주소도 설정 된 경우이 오류가 발생 안전 하 게 무시 수 있습니다. 시스템 오류 "가상 스위치를-PortBlocked"를 사용 하 여 실패 상태의 게이트웨이 HNV 공급자 VM Nic에 대 한 네트워크 인터페이스 리소스는 어디에서 두 번째 버그가 있습니다. 이 오류가 발생도 무시 해도 IP 구성 VM NIC 리소스에 설정 된 경우를으로 설계 null 합니다.


다음 표에서 목록이 오류 코드, 메시지 및 작업이 관찰 구성 상태에 따라 추가 작업을 수행 합니다.

  
| **코드**| **메시지**| **알림**|  
|:--------:|:-----------:|----------:|  
| 알 수 없음| 알 수 없는 오류| |  
| HostUnreachable                       | 호스트 컴퓨터에 연결할 수 없기 | 네트워크 컨트롤러 및 호스트 간 관리 네트워크 연결 확인 |  
| PAIpAddressExhausted                  | 소진된 파 Ip 주소 | HNV 공급자 논리 서브넷 IP 풀 크기 늘리기 |  
| PAMacAddressExhausted                 | 소진된 파 Mac 주소 | Mac 풀 범위 늘리기 |  
| PAAddressConfigurationFailure         | 파 주소 호스트를 연결할 하지 못했습니다. | 네트워크 컨트롤러와 호스트 사이의 관리 네트워크 연결을 확인 합니다. |  
| CertificateNotTrusted                 | 인증서가 신뢰할 수 있는  |호스트와 통신을 위해 사용 되는 인증서를 수정 합니다. |  
| CertificateNotAuthorized              | 인증서 권한이 없는 | 호스트와 통신을 위해 사용 되는 인증서를 수정 합니다. |  
| PolicyConfigurationFailureOnVfp       | VFP 정책 구성에서 실패 | 이 런타임 실패 합니다.  없음 명확한 해결 합니다. 로그를 수집 합니다. |  
| PolicyConfigurationFailure            | 정책 통신 실패 하거나 다른 사람으로 인해 호스트에 밀어에 실패는 NetworkController에 오류가 발생 합니다.| 확정 작업이 있습니다.  이 목표 상태 네트워크 컨트롤러 모듈에서 처리 하는 동안 오류가 발생 합니다. 로그를 수집 합니다. |  
| HostNotConnectedToController          | 호스트 연결 되어 있지 아직 네트워크 컨트롤러 | 네트워크 컨트롤러에서 연결할 수 포트 프로필 호스트 또는 호스트 적용 되지 않습니다. HostID 레지스트리 키 서버 리소스의 인스턴스 ID와 일치 하는지 확인 합니다. |  
| MultipleVfpEnabledSwitches            | 여러 VFp 호스트 스위치를 활성화 가지  | 네트워크 컨트롤러 호스트 에이전트만 사용 VFP 확장명이 한 vSwitch를 지원 하므로 스위치를 중 하나를 삭제합니다 |  
| PolicyConfigurationFailure            | VNet 정책으로 인해 인증서 오류 또는 연결 오류 VmNic에 대 한 밀어 하지 못했습니다.  | 적절 한 인증서 배포 된 확인 (인증서 제목 호스트 FQDN 일치 해야 합니다). 네트워크 컨트롤러와 호스트 연결 확인 |  
| PolicyConfigurationFailure            | VSwitch 정책으로 인해 인증서 오류 또는 연결 오류 VmNic에 대 한 밀어 하지 못했습니다.  | 적절 한 인증서 배포 된 확인 (인증서 제목 호스트 FQDN 일치 해야 합니다). 네트워크 컨트롤러와 호스트 연결 확인|
| PolicyConfigurationFailure            | 방화벽 정책으로 인해 인증서 오류 또는 연결 오류 VmNic에 대 한 밀어 하지 못했습니다. | 적절 한 인증서 배포 된 확인 (인증서 제목 호스트 FQDN 일치 해야 합니다). 네트워크 컨트롤러와 호스트 연결 확인|
| DistributedRouterConfigurationFailure | 호스트 vNic에 분산 라우터 설정을 구성 못했습니다.                          | TCPIP 스택 오류입니다. 이 오류 보고 된 서버의 파 및 DR 호스트 vNICs 정리 해야 할 수 있습니다. |
| DhcpAddressAllocationFailure          | DHCP 주소 할당 한 VMNic에 대 한 하지 못했습니다.                                                    | NIC 리소스에 고정 IP 주소 특성을 구성 하는 경우 확인 |  
| CertificateNotTrusted<br>CertificateNotAuthorized | 네트워크나 인증서 오류 때문 Mux에 연결 하지 못했습니다. | 오류 메시지 코드에 제공 되는 숫자 코드 확인: winsock 오류 코드에 해당 합니다. 인증서 오류는 세밀 (예를 들어, 인증서를 확인할 수 없으면 권한이 없는 인증서 등.) |  
| HostUnreachable                       | MUX는 비정상적인 (일반적인 경우 연결이 끊어진 BGPRouter은) | BGP 피어 랙 위에 (에) 스위치 또는 RRAS (BGP 가상 컴퓨터)에 연결할 수 없는 또는 하지 피어 링 성공적으로입니다. 소프트웨어 부하 분산 멀티플렉서 리소스와 BGP 피어 (에 또는 RRAS 가상 컴퓨터)에 BGP 설정 확인 |  
| HostNotConnectedToController          | SLB 호스트 에이전트 연결 되어 있지 않으면  | SLB 호스트 에이전트 서비스 실행 중인지 확인 이유로 SLB 호스트 에이전트 로그 (자동 실행)를 참조 하세요 SLBM (NC)에서 실행 되는 호스트 에이전트 제시 인증서 거부 된 경우에 대비 상태 됩니다 표시 되는 이유 nuanced 정보  |  
| PortBlocked                           | VNET 부족 VFP 포트가 차단 된 / ACL 정책 | 다른 모든 오류를 정책 구성 해야 할 수 있는 되는지 확인 합니다. |  
| 오버                            | Loadbalancer MUX 오버는  | 성능 문제를 MUX |  
| RoutePublicationFailure               | Loadbalancer MUX BGP 라우터에 연결 되지 않은 | MUX BGP 라우터와 연결 되어 있는 경우 및 BGP 피어 링 올바르게 설정 되어 있는지 확인 |  
| VirtualServerUnreachable              | Loadbalancer MUX SLB 관리자에 연결 되지 않은 | SLBM MUX와 연결 확인 |  
| QosConfigurationFailure               | 구성 QOS 정책 하지 못했습니다. | 충분 한 대역폭 QOS 예약을 사용 하는 경우 모든 VM를 사용할 수 있는지 확인 |


#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>네트워크 컨트롤러와 Hyper-v 호스트 (NC 호스트 에이전트 서비스) 네트워크 연결 확인
실행는 *netstat* NC 호스트 에이전트 및 네트워크 컨트롤러 노드와 한 LISTENING socket Hyper-v 호스트 연결 연결 세 가지 유효성을 검사 하기 아래 명령
- 포트 TCP:6640 Hyper-v 호스트 (NC 호스트 에이전트 서비스)에서 수신
- IP (> 32000) 포트에서 NC 노드 ip 6640 포트에서 개최 된 Hyper-v에서 두 개의 기존된 연결
- 하나 설정 6640 포트에서 네트워크 컨트롤러 나머지 IP Hyper-v 호스트 IP 임시 포트에 연결

>[!NOTE]
>해당 호스트에 배포 테 가상 컴퓨터 없는 경우 Hyper-v 호스트 연결 두만 수 합니다.

```none
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```
#### <a name="check-host-agent-services"></a>서비스 호스트 에이전트 확인
네트워크 컨트롤러 Hyper-v 호스트에서 두 개의 호스트 에이전트 서비스와 통신: SLB 호스트 에이전트와 NC 호스트 에이전트 합니다. 이러한 서비스 중 하나 또는 둘 실행 하지 않는 것 같습니다. 상태를 확인 하 고 실행 하지 하는 경우 다시 시작 합니다.

```none
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>네트워크 컨트롤러 상태 확인
세 개의 연결 연결 되지 있거나 네트워크 컨트롤러 표시 응답 하지 않는 경우 되어 있는지 확인 합니다 모든 노드와 서비스 모듈 실행 다음 cmdlet 사용 하 여 확인 합니다. 

```none
# Prints a DIFF state (status is automatically updated if state is changed) of a particular service module replica 
Debug-ServiceFabricNodeStatus [-ServiceTypeName] <Service Module>
```
네트워크 컨트롤러 서비스 모듈은 다음과 같습니다.
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

ReplicaStatus는 확인 **준비** HealthState 이며 **확인**합니다.

여러 노드 네트워크 컨트롤러와 프로덕션 배포는에 기본 된 각 서비스에는 어떤 노드와 개별 복제 상태를 확인할 수도 있습니다.

```none  
Get-NetworkControllerReplica

# Sample Output for the API service module
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready

```
준비 복제 상태 인지 확인 된 각 서비스에 대 한 합니다.
 
#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>해당 HostIDs 및 네트워크 컨트롤러 및 각 Hyper-v 호스트 사이 인증서 확인 
Hyper-v 호스트는 HostID 네트워크 컨트롤러 서버 리소스의 인스턴스 Id 일치 하는지 확인 하려면 다음 명령을 실행합니다

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

*개선* SDNExpress를 사용 하 여 스크립트 또는 수동 배포 업데이트 서버 리소스의 인스턴스 Id와 일치 하는 HostId 키. Hyper-v 서버 VMM에서 삭제 VMM를 사용 하 여 네트워크 컨트롤러 호스트 에이전트 Hyper-v 호스트 (실제 서버)에서 다시 시작 하 고 HostId 레지스트리 키를 제거 합니다. VMM 통해 서버를 다시 추가 합니다.


Hyper-v 호스트 (NC 호스트 에이전트 서비스) 사이의 노드가 네트워크 컨트롤러 (SouthBound) 통신 Hyper-v 호스트 (호스트 됩니다 인증서의 제목 이름이)에서 사용 되는 X.509 인증서 지문을 동일한 지 확인 합니다. 네트워크 컨트롤러의 나머지 인증서의 제목 이름에 있는지 확인할 수도 *CN =<FQDN or IP>*합니다.

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

제목 이름은 란 있는지 각 인증서의 다음 매개 변수를 확인할 수도 있습니다 (호스트 또는 NC 나머지 FQDN 또는 IP) 예상 인증서가 만료 아직 하지 및 인증서 체인의 모든 인증 기관 신뢰할 기관에 포함 되어 있습니다.

- 제목 이름  
- 만료 날짜  
- 최상위 인증 기관에서 신뢰할 수 있는  

*개선* 여러 인증서를 사용 하는 동일한 주체 이름을 Hyper-v 호스트 하는 경우 네트워크 컨트롤러 호스트 에이전트는 임의로 중 하나를 선택 네트워크 컨트롤러에 게 제공 됩니다. 알려진 네트워크 컨트롤러 서버 리소스의 지문와 일치 하지 않을 수 있습니다. 이 경우 인증서 Hyper-v 호스트 이름이 같은 주제 중 하나를 삭제 하 고 네트워크 컨트롤러 호스트 에이전트 서비스가 다시 시작 합니다. 연결을 계속 설정할 수 없습니다., Hyper-v 호스트 주제 이름이 같은 다른 인증서를 삭제 하 고 해당 서버 리소스 VMM에서 삭제 합니다. 를 다시 만들어야 서버 리소스 vmm는 새 X.509 인증서를 생성 하 고 Hyper-v 호스트에 설치 됩니다.
  

#### <a name="check-the-slb-configuration-state"></a>SLB 구성 상태 확인
Debug-NetworkController cmdlet에 대 한 출력의 일부로 구성 SLB 상태를 확인할 수 있습니다. 이 cmdlet 현재 집합이 JSON 파일, 각 Hyper-v 호스트 (서버)에서 모든 IP 구성 호스트 에이전트 데이터베이스 테이블에서 정책이 로컬 네트워크의 네트워크 컨트롤러 리소스 출력도 합니다. 

추가 추적 기본적으로 수집 됩니다. 추적을 수집 하지-IncludeTraces 추가: $false 매개 합니다.

```none
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential 
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>기본 출력 위치 < working_directory > \NCDiagnostics\ 디렉터리 됩니다. 사용 하 여 기본 출력 디렉터리 변경할 수 있습니다는 `-OutputDirectory`매개 합니다. 

SLB 구성 상태 정보를 찾을 수 있는 _진단 slbstateResults.Json_ 이 디렉터리에 파일.

다음 섹션으로이 JSON 파일 구분할 수 있습니다.
 * 패브릭
   * 이 섹션에 SlbmVips-네트워크 컨트롤러 coodinate 구성과 SLB 호스트 에이전트와 SLB Muxes 상태를 사용 하는 SLB 관리자 VIP 주소의 IP 주소를 나열 됩니다.
   * MuxState-이 섹션은 mux 상태 제공 배포 하 각 SLB Mux에 대 한 하나의 값을 목록이 표시
   * 라우터 구성-이 섹션 업스트림 라우터 (BGP 동료) 목록이 표시 자율 시스템 번호 (ASN), 교통 IP 주소 및 id입니다. 또한 SLB Muxes ASN 및 교통 IP 나열 합니다.
   * 연결 호스트 정보-이 섹션은 목록 관리 IP 주소 모든 부하가 작업을 실행할 수 있는 Hyper-v 호스트 합니다.
   * Vip 범위-이 섹션의 공개 하 게 비밀로 VIP IP 풀 범위 나열 됩니다. SLBM VIP 이러한 범위 중 하나에서 할당된 IP으로 포함 됩니다. 
   * Mux 경로-이 섹션의 경로 광고 해당 특정 mux에 대 한 모든 포함 된 배포 하 각 SLB Mux에 대 한 하나의 값을 나열 합니다.
 * 테
   * VipConsolidatedState-이 섹션 높아질된 경로 접두사, Hyper-v 호스트 담그고 끝점 등 각 테 VIP에 대 한 연결 상태를 목록이 표시 됩니다.
    
> [!NOTE]
> 사용 하 여 직접 SLB 상태 조사할 수 있습니다는 [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) 스크립트에서 사용할 수 있는 [Microsoft SDN GitHub 저장소](https://github.com/microsoft/sdn)합니다. 

#### <a name="gateway-validation"></a>게이트웨이 유효성 검사

**네트워크 컨트롤러 다음과 같습니다.**
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

**(에) 랙 스위치 위에서:**

`sh ip bgp summary (for 3rd party BGP Routers)`

**Windows BGP 라우터**
```
Get-BgpRouter
Get-BgpPeer
Get-BgpRouteInformation
```

(특히 기반 SDNExpress 배포)에 지금까지 보았습니다 문제에서이 외에도 테 삽입 GW Vm에서 하지 구성 되는 가장 일반적인 원인 GW FabricConfig.psd1에 용량이 TenantConfig.psd1에서 (S2S 터널) 네트워크 연결에 할당 하려고 하는 사람들에 비해 간단히 한다는 사실이 되도록 것 같습니다. 다음 명령을 출력 비교 하 여 쉽게 확인할 수 있습니다.

```
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>[호스팅] 평면 데이터 유효성 검사
네트워크 컨트롤러 배포한 하 고 테 가상 네트워크와 서브넷 만든, 가상 서브넷 Vm 연결 된, 추가 패브릭 수준 테스트 호스팅 테 연결 상태를 확인 하 여 수행할 수 있습니다.

#### <a name="check-hnv-provider-logical-network-connectivity"></a>HNV 공급자 논리 네트워크 연결 상태를 확인
네트워크 컨트롤러 VM Hyper-v 호스트에서 실행 되는 테 가상 네트워크에 연결 하는 첫 번째 게스트 후 Hyper-v 호스트 두 개의 HNV 공급자 IP 주소 (파 IP 주소)를 할당 합니다. 이러한 IPs HNV 공급자 논리 네트워크 IP 풀에서 제공 되며와 네트워크 컨트롤러에서 관리할 수 있습니다.  이러한 두 가지 HNV IP 주소를 찾도록의

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

이러한 HNV 공급자 IP 주소 (파 IPs) 별도 TCPIP 네트워크에에서 만든 이더넷 어댑터에 할당 되어 있고 어댑터의 이름을 _VLANX_ X HNV 공급자 (transport) 논리 네트워크에 할당 VLAN가 있습니다.

추가 한 삽입와 ping가 할 수 논리 네트워크 HNV 공급자를 사용 하 여 두 Hyper-v 호스트 연결 (-c Y) 매개는 어디에 Y TCPIP 네트워크 삽입은 PAhostVNICs 만들어집니다. 이 삽입을 실행 하 여 확인할 수 있습니다.

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
> 파 호스트 vNIC 어댑터 경로 데이터에 사용 되지 않는 및 하므로 하지 않은 IP "(PAhostVNic) vEthernet 어댑터"에 할당 합니다.

예를 들어 1과 2 Hyper-v 호스트 IP 주소를 HNV 공급자 (파)는 가정 다음과 같습니다.

|Hyper-v 호스트-|1 파 IP 주소|파 IP 주소가 2|
|---             |---            |---             |
|1 호스트 | 10.10.182.64 | 10.10.182.65 |
|호스트 2 | 10.10.182.66 | 10.10.182.67 |

HNV 공급자 논리 네트워크 연결을 확인 하려면 다음 명령을 사용 하 여 둘 사이 했습니다 ping 할 수 있습니다.

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

*개선* 경우 HNV 공급자 ping는 하지 작동, VLAN 구성을 포함 하 여 실제 네트워크 연결을 확인 합니다. 각 Hyper-v 호스트 물리적 Nic 트렁크 모드에 할당 된 없이 특정 VLAN와 있어야 합니다. 관리 호스트 vNIC 관리 논리 네트워크 VLAN에 분리 해야 합니다.

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
 
#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>HNV 논리 네트워크 공급자에 MTU 및 점보 프레임 지원이 확인

또 다른 일반적인 문제 HNV 공급자 논리 네트워크에서 이더넷 카드 및/또는 실제 네트워크 포트 VXLAN (또는 NVGRE) 캡슐화에서 오버 처리 하도록 구성 충분히 MTU 설치 되지 않은입니다. 
>[!NOTE]
> 일부 이더넷 카드 및 드라이버를 새 지원 * EncapOverhead 키워드 네트워크 컨트롤러 호스트 에이전트 160 값을 하 여 자동으로 설정 됩니다. 이 값 값으로 추가 됩니다는 * JumboPacket 키워드를 합계 높아질된 MTU로 사용 됩니다.
> 예를 들어 * EncapOverhead 160 = 및 * JumboPacket 1514 = = > MTU 1674B =

```none
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

사용 하 여 HNV 공급자 논리 네트워크는 더 큰 MTU 크기-끝을 지원 하는지 여부를 테스트 하 고 _테스트 LogicalNetworkSupportsJumboPacket_ cmdlet:
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

*개선*
* 되도록 하려면 적어도 물리적 스위치 포트에서 MTU 크기 조정 1674B (14b가 이더넷 헤더 및 예고편 포함)
* NIC 카드가 EncapOverhead 키워드를 지원 하지 않는 경우 조정 되도록 하려면 적어도 JumboPacket 키워드 1674B


#### <a name="check-tenant-vm-nic-connectivity"></a>테 VM NIC 연결 확인
Guest VM에 할당 각 VM NIC 개인 고객이 주소 (캐나다)와 HNV 공급자 주소 (파) 공간 캘리포니아 파 매핑하를 있습니다. 이러한 매핑 각 Hyper-v 호스트 OVSDB 서버 테이블에 유지 되 및 다음 cmdlet 실행에서 찾을 수 있습니다.

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
> 원하는 캘리포니아 파 매핑으로 지정된 테 VM에 대 한 출력 하지는 경우에 네트워크 컨트롤러를 사용 하 여 VM NIC 및 IP 구성 리소스를 확인 하세요는 _Get NetworkControllerNetworkInterface_ cmdlet 합니다. 네트워크 컨트롤러 및 NC 호스트 에이전트 노드 간의 설정된 연결을 확인 합니다.

이 정보를 될 사용 하 여 네트워크 컨트롤러 호스팅에 의해 테 VM ping를 시작 수 있는 _테스트 VirtualNetworkConnection_ cmdlet 합니다.

## <a name="specific-troubleshooting-scenarios"></a>특정 문제를 해결 시나리오

다음 섹션에서는 특정 시나리오 문제 해결에 대 한 지침을 제공 합니다.

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>두 개의 테 가상 컴퓨터 간에 네트워크 연결

1.  [테] Windows 방화벽 테 가상 컴퓨터에서 교통량을 차단 하 고 있지 있는지 확인 합니다.  
2.  [테] IP 주소를 실행 하 여 테 가상 컴퓨터에 할당 된 있는지 확인 _ipconfig_합니다. 
3.  [호스팅] 실행 **테스트 VirtualNetworkConnection** Hyper-v 호스트 연결 문제가 두 테 가상 컴퓨터 간에 유효성을 검사으로 합니다. 

>[!NOTE]
>VSID id.는 가상 서브넷을 참조 VXLAN의 경우는 VXLAN 네트워크 식별자 (vni) 또는입니다. 실행 하 여이 값을 찾을 수는 **Get PACAMapping** cmdlet 합니다.

#### <a name="example"></a>예제

    $password = ConvertTo-SecureString -String "password" -AsPlainText -Force
    $cred = New-Object pscredential -ArgumentList (".\administrator", $password) 

호스트 ip 관리 "sa18n30-2.sa18.nttest.microsoft.com" 10.127.132.153의 ListenerCA ip 192.168.1.5 모두 연결을 가상 서브넷 (VSID) 4114의에서 192.168.1.4의 SenderCA ip "녹색 웹 VM 1" 간에 캘리포니아 ping 만듭니다.

    Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114

    Test-VirtualNetworkConnection at command pipeline position 1

시작 캘리포니아 공간 핑 테스트 192.168.1.4 Rtt 주소에서 성공 192.168.1.5에 대 한 Ping 추적 세션을 시작 = 0 ms


캘리포니아 경로 정보:

    Local IP: 192.168.1.4
    Local VSID: 4114
    Remote IP: 192.168.1.5
    Remote VSID: 4114
    Distributed Router Local IP: 192.168.1.1
    Distributed Router Local MAC: 40-1D-D8-B7-1C-06
    Local CA MAC: 00-1D-D8-B7-1C-05
    Remote CA MAC: 00-1D-D8-B7-1C-07
    Next Hop CA MAC Address: 00-1D-D8-B7-1C-07

파 경로 정보:

    Local PA IP: 10.10.182.66
    Remote PA IP: 10.10.182.65
 
 <snip> ...

4.  [테] 가상 서브넷 또는 교통 체증을 차단 하는 VM 한 네트워크 인터페이스에 지정 된 분산된 방화벽 정책이 인지 확인 합니다.    

네트워크 컨트롤러 REST API sa18.nttest.microsoft.com 도메인에 있는 sa18n30nc 데모 환경에서 발견 쿼리.

    $uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
    Get-NetworkControllerAccessControlList -ConnectionUri $uri 

# <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>IP 구성 하 고이 ACL 참조 하 고 있는 가상 서브넷 확인

1. [호스팅] 실행 ``Get-ProviderAddress``모두 Hyper-v의 두 가지 호스트 호스트 질문에서 가상 컴퓨터 테 넌 트 한 다음 실행 ``Test-LogicalNetworkConnection``또는 ``ping -c <compartment>``Hyper-v 호스트 HNV 공급자 논리 네트워크에 연결 유효성을 검사 하기
2.  [호스팅] Hyper-v 호스트에 정확 하 고 모든 계층 2 디바이스 Hyper-v 호스트 사이 전환 MTU 설정 되어 있는지 확인 합니다. 실행 ``Test-EncapOverheadValue``모든 Hyper-v 호스트 의심에 있습니다. 또한 사이 있는 모든 2 계층 스위치 최소 1674 바이트 160 바이트 최대 오버에 맞게 설정 MTU 있는지 확인 합니다.  
3.  [호스팅] 파 IP 주소가 없는 경우, 캘리포니아 연결이 끊어진 네트워크 정책 받았는지 확인 하기 확인 합니다. 실행 ``Get-PACAMapping``캡슐화 규칙과 오버레이 가상 네트워크 만드는 데 필요한 캘리포니아 파 매핑 올바르게 설정 하는 경우를 확인 합니다.  
4.  [호스팅] 네트워크 컨트롤러 호스트 에이전트 네트워크 컨트롤러에 연결 되어 있는지 확인 합니다. 실행 ``netstat -anp tcp |findstr 6640``되는지 확인 하 고   
5.  [호스팅] 호스트 HKLM의 ID 확인 / 서버 리소스 호스팅 테 가상 컴퓨터의 인스턴스 ID와 일치 합니다.  
6. [호스팅] 포트 프로필 ID 테 가상 컴퓨터의 VM 네트워크 인터페이스 인스턴스 ID와 일치 하는지 확인 합니다.  

## <a name="logging-tracing-and-advanced-diagnostics"></a>로그인, 추적과 고급 진단

다음 섹션 고급 진단, 로그온 및 추적 정보를 제공 합니다.

### <a name="network-controller-centralized-logging"></a>네트워크 컨트롤러 중앙 집중식 로그인 
 
자동으로 네트워크 컨트롤러 디버거 로그를 수집 하 고 중앙된 위치에 저장할 수 있습니다. 처음으로 또는 나중에 언제 든 지에 대 한 네트워크 컨트롤러를 배포 하는 경우 로그 컬렉션을 사용할 수 있습니다. 로그는 네트워크 컨트롤러에서 수집 하 고 요소 네트워크 컨트롤러에서 관리 하는 네트워크: 컴퓨터, 부하 분산 소프트웨어가 (SLB) 및 게이트웨이 컴퓨터를 호스팅할 합니다. 

이러한 로그 네트워크 컨트롤러 클러스터, 네트워크 컨트롤러 응용 프로그램, 게이트웨이 로그, SLB, 가상 네트워킹 및 분산된 방화벽 디버그 로그 포함 됩니다. 새로운 호스트/SLB/게이트웨이 네트워크 컨트롤러에 추가 되 면 때마다 로깅 해당 컴퓨터에 시작 됩니다. 마찬가지로, 호스트/SLB/게이트웨이 네트워크 컨트롤러에서 제거 되 면 로깅 해당 컴퓨터에 중지 됩니다.

#### <a name="enable-logging"></a>로깅 사용

사용 하 여 네트워크 컨트롤러 클러스터 설치 하는 경우 로그인 자동으로 활성화는 **설치 NetworkControllerCluster** cmdlet 합니다. 기본적으로 로그가 수집 됩니다 로컬로에서 네트워크 컨트롤러 노드에서 *%systemdrive%\SDNDiagnostics*합니다. **좋습니다** (하지 로컬) 원격 파일 공유 하려면이 위치를 변경 합니다. 

네트워크 컨트롤러 클러스터 로그가에 저장 되어 *%programData%\Windows Fabric\log\Traces*합니다. 사용 하 여 로그 컬렉션에 대 한 중앙 집중식된 위치 지정할 수 있습니다의 **DiagnosticLogLocation** 이기도 권장 매개 원격 파일 공유 됩니다. 

이 위치에 대 한 액세스를 제한 하려면 액세스 자격 증명을 제공할 수 있는 **LogLocationCredential** 매개 합니다. 또한 제공 해야 하는 경우 로그 위치에 액세스할 수 자격 증명을 제공는 **CredentialEncryptionCertificate** 매개 네트워크 컨트롤러 노드에 로컬로 저장 된 자격 증명을 암호화 하는 데 사용 됩니다.  

기본 설정을 사용 하 여 했을 때 75 g B 이상 로컬 노드에서 여유 공간이 중앙 위치 및 25 g B (중앙 위치를 사용 하지) 네트워크 컨트롤러 3 노드에서 클러스터에 대 한 것이 좋습니다.

#### <a name="change-logging-settings"></a>로그인 설정 변경

언제 든 지를 사용 하 여 로그인 설정을 변경할 수 있는 ``Set-NetworkControllerDiagnostic``cmdlet 합니다. 다음 설정은 변경할 수 있습니다.

- **로그 위치 중앙 집중식**합니다.  모든 로그도 저장할 위치를 변경할 수 있는 ``DiagnosticLogLocation``매개 합니다.  
- **로그 위치에 액세스할 수 자격 증명**합니다.  로그 위치를 사용 하 여 액세스할 수 있는 자격 증명을 변경할 수 있는 ``LogLocationCredential``매개 합니다.  
- **로컬 로깅 이동**합니다.  중앙 로그 저장소를 제공 하는 경우 다시 이동할 수 있습니다 로컬 네트워크 컨트롤러 노드와에 로그인 하는 ``UseLocalLogLocation``매개 (큰 디스크 공간 요구 사항으로 인해 권장 하지 않음).  
- **로그인 범위**합니다.  기본적으로 모든 로그가 수집 됩니다. 범위를만 네트워크 컨트롤러 클러스터 로그를 수집 변경할 수 있습니다.  
- **로깅 수준을**합니다.  기본 로깅 수준 알림입니다. 오류를 경고 또는 자세한 정보를 변경할 수 있습니다.  
- **시간이 오래 로그**합니다.  로그는 돌려서에 저장 됩니다. 3 일간의 로그인 데이터 로컬 로깅 또는 중앙 집중식된 로깅 사용 하 든 기본적으로 해야 합니다. 이 시간 제한이 설정 된 변경할 수 **LogTimeLimitInDays** 매개 합니다.  
- **크기 오래 로그**합니다.  기본적으로 로컬 로깅 사용 하는 경우 중앙 집중식된 기록 및 25 g B를 사용 하는 경우 로그인 데이터 최대 75 g B 해야 합니다. 이 제한 되어 있으며 변경할 수 있는 **LogSizeLimitInMBs** 매개 합니다.

#### <a name="collecting-logs-and-traces"></a>기록 수집 하 고 추적

네트워크 컨트롤러에 대 한 중앙 집중식된 로깅 기본적으로 사용 하는 VMM 배포 합니다. 네트워크 컨트롤러 서비스 템플릿으로 배포할 때 이러한 로그에 대 한 파일 공유 위치 지정 됩니다.

파일 위치를 지정 로컬 되지 않은 경우 로그인 각 네트워크 컨트롤러 노드에서 로그 C:\Windows\tracing\SDNDiagnostics에서 저장 된 사용 됩니다. 다음과 같은 계층을 사용 하 여 이러한 로그 저장 됩니다.

- 크래시 덤프
- NCApplicationCrashDumps
- NCApplicationLogs
- PerfCounters
- SDNDiagnostics
- 추적

네트워크 컨트롤러 (Azure) 서비스 패브릭 사용합니다. 특정 문제를 해결할 때 서비스 패브릭 로그 필요할 수 있습니다. 이러한 로그 C:\ProgramData\Microsoft\Service 패브릭에서 각 네트워크 컨트롤러 노드에서 확인할 수 있습니다.

사용자가 실행 하는 경우는 _디버그 NetworkController_ cmdlet, 추가 로그에서 네트워크 컨트롤러 서버 리소스와 지정 하는 각 Hyper-v 호스트에서 사용할 수 있습니다. 이러한 로그 (및 추적 사용 하는 경우) C:\NCDiagnostics 이하로 유지은

### <a name="slb-diagnostics"></a>SLB 진단

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>SLBM 패브릭 오류 (호스팅 서비스 공급자 동작)

1.  소프트웨어 부하 분산 장치 관리자 (SLBM) 작동 하 고 오케스트레이션 layers 서로 통신할 수 확인: SLBM SLB Mux-> 및 SLBM SLB 호스트 에이전트-> 합니다. 실행 [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) 네트워크 컨트롤러 나머지 끝점에 액세스할 수 있는 모든 노드에서 합니다.  
2.  유효성 검사는 *SDNSLBMPerfCounters* 성능 네트워크 컨트롤러 노드 Vm (가능 주 네트워크 컨트롤러 노드-Get-NetworkControllerReplica) 중 하나에서:
    1.  부하 분산 (파운드) 엔진 SLBM에 연결 되어 있나요? (*SLBM LBEngine 구성 총* > 0)  
    2.  가 SLBM 적어도 대해 알고 자체 끝점? (*VIP 끝점 총* > 2 =)  
    3.  SLBM에 (담그고) Hyper-v 호스트 연결 되나요? (*연결한 HP 클라이언트* num 서버 = =)   
    4.  SLBM은 Muxes에 연결 되어 있나요? (*Muxes 연결* == *SLBM에 Muxes 건강* == *Muxes 보고 건강* = # SLB Muxes Vm).  
3.  구성 BGP 라우터 SLB MUX와 피어 링 성공적으로 있는지 확인  
    1.  원격 (예: BGP 가상 컴퓨터)에 액세스할 수 있는 RRAS 사용:  
        1.  Get-BgpPeer 연결 나타납니다.  
        2.  Get-BgpRouteInformation는 SLBM에 대 한 최소 경로 표시 되어야 자체 VIP  
    2.  실제 위쪽의-랙 (에)를 사용 하 여 BGP 피어도 전환, 설명서를 참조 하십시오.  
        1.  예를 들어: # bgp 인스턴스를 표시 합니다.  
4.  유효성 검사는 *SlbMuxPerfCounters* 및 *SLBMUX* SLB Mux VM에서 성능 카운터
5.  부하 분산 소프트웨어가 관리자 리소스에 VIP 범위 구성 상태 확인  
    1.  Get-NetworkControllerLoadBalancerConfiguration ConnectionUri < https://<FQDN or IP>| convertto json-8 깊이 (IP 풀에서 VIP 범위를 확인 하 고 SLBM 자체 VIP 확인 (*LoadBalanacerManagerIPAddress*) 및이 범위 내에 있는 모든 테 전면 Vip)  
        1. Get-NetworkControllerIpPool NetworkId "</공개 VIP 논리 네트워크 리소스 ID >"-SubnetId "</공개 VIP 논리 서브넷 리소스 ID >"-ResourceId "<IP Pool Resource Id>"-ConnectionUri $uri | convertto json-깊이 8 
    2.  Debug-NetworkControllerConfigurationState-  

검사가 실패 위의 경우 테 SLB 상태 오류 모드로 수도 있습니다.  

**개선**   
다음 해결에 표시 된 다음 진단 정보 based 다음과 같습니다.  
* SLB Multiplexers 연결 되어 있는지 확인  
  * 인증서 문제 해결  
  * 네트워크 연결 문제 해결  
* BGP 피어 링 정보 성공적으로 구성 되어 있는지 확인  
* 레지스트리에서 호스트 ID Server 인스턴스 ID 서버 리소스에 게 일치 (부록에 대 한 참조 *HostNotConnected* 오류 코드)  
* 로그를 수집 합니다.  

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>SLBM 테 오류 (호스팅 서비스 공급자와 테 작업)

1.  [호스팅] 확인 *디버그 NetworkControllerConfigurationState* LoadBalancer 리소스 오류 상태에서를 확인 하려면. 작업 항목 부록에는 테이블에 따라 완화 하려고 합니다.   
    1.  현재 및 광고 경로 VIP 끝점 인지 확인  
    2.  VIP 끝점 개수 담그고 끝점 만들었을 확인합니다  
2.  [테] 유효성을 검사 잘못 지정 하시 부하 분산 리소스  
    1.  담그고의 유효성을 검사 끝점 SLBM에 등록 하는 해당 LoadBalancer 백 엔드 주소 풀 IP 구성 하는 테 가상 컴퓨터 호스팅하고  
3.  [호스팅] 담그고 끝점 발견 되지 않거나 연결는 다음과 같습니다.   
    1.  확인 *디버그 NetworkControllerConfigurationState*  
        1.  해당 NC의 유효성을 검사 하 고 SLB 호스트 에이전트 성공적으로 사용 하 여 컨트롤러 이벤트 Coordinator 네트워크에 연결 ``netstat -anp tcp |findstr 6640)``  
    2.  확인 *HostId* 에 *nchostagent* 서비스 regkey (참조 *HostNotConnected* 부록에 오류 코드) Id 해당 서버 리소스 인스턴스를 찾습니다 (``Get-NCServer |convertto-json -depth 8``)  
    3.  포트 가상 컴퓨터에 대 한 포트 프로필 id 일치 인스턴스 해당 가상 컴퓨터 NIC 리소스의 Id 확인   
4.  [호스팅 공급자] 로그를 수집 합니다.   

#### <a name="slb-mux-tracing"></a>SLB Mux 추적

소프트웨어 부하 분산 Muxes 정보도 뷰어를 통해 확인할 수 있습니다. 
1. 이벤트 뷰어 보기 메뉴에서 "표시 분석 하 고 디버그 로그" 클릭
2. "응용 프로그램 및 서비스 로그"로 이동 > Microsoft > Windows > SlbMuxDriver > 이벤트 뷰어에서 추적 
3. 마우스 오른쪽 단추로 클릭 하 고 "로그 사용"을 선택 합니다.

>[!NOTE]
>이 로그인 문제를 재현 하는 동안 짧은 시간 동안 사용할 수 있는 기간은 것이 좋습니다.

### <a name="vfp-and-vswitch-tracing"></a>VFP vSwitch 추적 하 고

테 가상 네트워크에 연결 된 VM 게스트 호스트 하는 개최 된 모든 Hyper-v의, VFP 추적 문제가 있을 수 있습니다 결정을 수집할 수 있습니다.

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch 
netsh trace stop
netsh trace convert .\vfp.etl ov=yes 
```
