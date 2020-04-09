---
title: 확장 포트 액세스 제어 목록을 사용하여 보안 정책 만들기
description: 이 항목에서는 Windows Server 2016의 확장 된 포트 Access Control 목록 (Acl)에 대해 설명 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: a92e61c3-f7d4-4e42-8575-79d75d05a218
ms.author: lizross
author: eross-msft
ms.openlocfilehash: e4ea3d118a00a4862ce9eb3f93b079f05cc1cd1b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853316"
---
# <a name="create-security-policies-with-extended-port-access-control-lists"></a>확장 포트 액세스 제어 목록을 사용하여 보안 정책 만들기

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 Windows Server 2016의 확장 된 포트 Access Control 목록 (Acl)에 대해 설명 합니다. Hyper-V 가상 스위치에서 확장 ACL을 구성하여 가상 네트워크 어댑터를 통해 스위치에 연결된 VM(가상 컴퓨터)에서 들어오고 나가는 네트워크 트래픽을 허용하거나 차단할 수 있습니다.  
  
이 항목에는 다음과 같은 섹션이 포함되어 있습니다.  
  
-   [자세한 ACL 규칙](#bkmk_detailed)  
  
-   [상태 저장 ACL 규칙](#bkmk_stateful)  
  
## <a name="detailed-acl-rules"></a><a name="bkmk_detailed"></a>자세한 ACL 규칙  
Hyper-v 가상 스위치 확장 Acl에는 Hyper-v 가상 스위치에 연결 된 개별 VM 네트워크 어댑터에 적용할 수 있는 자세한 규칙을 만들 수 있습니다. 다중 테 넌 트 공유 서버 환경에서 네트워크 기반 보안 위협을 해결 하기 엔터프라이즈 및 클라우드 서비스 공급자 (Csp)를 허용 하는 자세한 규칙을 만들 수 있습니다.  
  
이제 VM에서 들어오고 나가는 모든 프로토콜의 모든 트래픽을 허용하거나 차단하는 광범위한 규칙을 만들 필요 없이 확장 ACL을 사용하여 VM에서 실행되는 개별 프로토콜의 네트워크 트래픽을 차단하거나 허용할 수 있습니다. 매개 변수 다음 5 개 튜플 집합을 포함 하는 Windows Server 2016에 확장된 ACL 규칙을 만들 수 있습니다: 원본 IP 주소, 대상 IP 주소, 프로토콜, 원본 포트 및 대상 포트입니다. 또한 각 규칙에서 들어오거나 나가는 네트워크 트래픽 방향과 규칙에서 지원하는 작업(트래픽 차단 또는 허용)을 지정할 수 있습니다.  
  
예를 들어 VM에서 포트 80을 통해 들어오고 나가는 HTTP 및 HTTPS 트래픽은 허용하고 모든 포트에서 다른 프로토콜의 네트워크 트래픽은 모두 차단하도록 포트 ACL을 구성할 수 있습니다.  
  
테넌트 VM에서 받을 수 있거나 받을 수 없는 프로토콜 트래픽을 지정하는 이 기능을 통해 보안 정책을 유연하게 구성할 수 있습니다.  
  
### <a name="configuring-acl-rules-with-windows-powershell"></a>Windows PowerShell을 사용하여 ACL 규칙 구성  
확장 ACL을 구성하려면 Windows PowerShell 명령 **Add-VMNetworkAdapterExtendedAcl**을 사용해야 합니다. 이 명령에는 고유한 용도의 네 가지 구문이 있습니다.  
  
1.  -VMName, 첫 번째 매개 변수로 지정 된 명명 된 vm-네트워크 어댑터의 모든 확장된 ACL을 추가 합니다. 구문:  
  
    > [!NOTE]  
    > 하나의 네트워크 어댑터에 확장된 ACL을 추가 하려면 매개 변수와 함께 네트워크 어댑터를 지정할 수 있습니다-VMNetworkAdapterName 합니다.  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VMName] <string[]> [-Action] <VMNetworkAdapterExtendedAclAction> {Allow | Deny}  
        [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>]  
        [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight]  
        <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName  
        <string>] [-ComputerName <string[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
2.  특정 VM의 특정 가상 네트워크 어댑터에 확장 ACL을 추가합니다. 구문:  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VMNetworkAdapter] <VMNetworkAdapterBase[]> [-Action]  
        <VMNetworkAdapterExtendedAclAction> {Allow | Deny} [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound |  
        Outbound} [[-LocalIPAddress] <string>] [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort]  
        <string>] [[-Protocol] <string>] [-Weight] <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID  
        <int>] [-Passthru] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
3.  Hyper-V 호스트 관리 운영 체제에서 사용하도록 예약된 모든 가상 네트워크 어댑터에 확장 ACL을 추가합니다.  
  
    > [!NOTE]  
    > 하나의 네트워크 어댑터에 확장된 ACL을 추가 하려면 매개 변수와 함께 네트워크 어댑터를 지정할 수 있습니다-VMNetworkAdapterName 합니다.  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-Action] <VMNetworkAdapterExtendedAclAction> {Allow | Deny} [-Direction]  
        <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>] [[-RemoteIPAddress]  
        <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight] <int> -ManagementOS  
        [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName <string>]  
        [-ComputerName <string[]>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
4.  와 같은 Windows PowerShell에서 만든 VM 개체에 확장된 ACL을 추가 **$vm = "my_vm" get-vm**합니다. 다음 코드 줄에서 다음과 같은 구문으로 이 명령을 실행하여 확장 ACL을 만들 수 있습니다.  
  
    ```  
    Add-VMNetworkAdapterExtendedAcl [-VM] <VirtualMachine[]> [-Action] <VMNetworkAdapterExtendedAclAction> {Allow |  
        Deny} [-Direction] <VMNetworkAdapterExtendedAclDirection> {Inbound | Outbound} [[-LocalIPAddress] <string>]  
        [[-RemoteIPAddress] <string>] [[-LocalPort] <string>] [[-RemotePort] <string>] [[-Protocol] <string>] [-Weight]  
        <int> [-Stateful <bool>] [-IdleSessionTimeout <int>] [-IsolationID <int>] [-Passthru] [-VMNetworkAdapterName  
        <string>] [-WhatIf] [-Confirm]  [<CommonParameters>]  
    ```  
  
### <a name="detailed-acl-rule-examples"></a>자세한 ACL 규칙 예  
다음은 **Add-VMNetworkAdapterExtendedAcl** 명령을 사용하여 확장 포트 ACL을 구성하고 VM에 대한 보안 정책을 만들 수 있는 방법에 대한 몇 가지 예입니다.  
  
-   [응용 프로그램 수준 보안 적용](#bkmk_enforce)  
  
-   [사용자 수준 및 응용 프로그램 수준 보안 모두 적용](#bkmk_both)  
  
-   [비-TCP/UDP 응용 프로그램에 보안 지원 제공](#bkmk_tcp)  
  
> [!NOTE]  
> 아래 표의 규칙 매개 변수 **Direction**의 값은 규칙을 만들려는 VM에서 들어오고 나가는 트래픽 흐름을 기반으로 합니다. VM에서 트래픽을 받는 경우에는 이 트래픽은 인바운드이고, VM에서 트래픽을 보내는 경우 이 트래픽은 아웃바운드입니다. 예를 들어 인바운드 트래픽을 차단하는 규칙을 VM에 적용하는 경우 인바운드 트래픽의 방향은 외부 리소스에서 VM으로 이동하는 방향입니다. 아웃바운드 트래픽을 차단하는 규칙을 적용하는 경우 아웃바운드 트래픽의 방향은 로컬 VM에서 외부 리소스로 이동하는 방향입니다.  
  
### <a name="enforce-application-level-security"></a><a name="bkmk_enforce"></a>응용 프로그램 수준 보안 적용  
많은 애플리케이션 서버에서 표준화된 TCP/UDP 포트를 사용하여 클라이언트 컴퓨터와 통신하기 때문에 애플리케이션에 지정된 포트에서 들어오고 나가는 트래픽을 필터링하여 애플리케이션 서버에 대한 액세스를 차단하거나 허용하는 규칙을 쉽게 만들 수 있습니다.  
  
예를 들어 RDP(원격 데스크톱 연결)를 사용하여 사용자가 데이터 센터의 애플리케이션 서버에 로그인하도록 할 수 있습니다. RDP에서는 TCP 포트 3389를 사용하므로 다음 규칙을 신속하게 설정할 수 있습니다.  
  
|원본 IP|대상 IP|프로토콜|원본 포트|대상 포트|Direction|작업|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|*|TCP|*|3389|안쪽|허용|  
  
다음은 Windows PowerShell 명령을 사용하여 규칙을 만들 수 있는 방법에 대한 두 가지 예입니다. 첫 번째 예제에서는 규칙은 "ApplicationServer." 라는 VM에 모든 트래픽을 차단합니다 "ApplicationServer" 라는 VM의 네트워크 어댑터에 적용 되는 두 번째 예제에서는 규칙을 VM에 인바운드 RDP 트래픽만을 허용 합니다.  
  
> [!NOTE]  
> 규칙을 만들 때 사용할 수 있습니다는 **-가중치** 매개 변수는 Hyper-v 가상 스위치에서 규칙을 처리 하는 순서를 결정 합니다. 에 대 한 값 **-가중치** ; 정수로 표현 됩니다 더 높은 정수를 사용 하 여 규칙 더 낮은 정수를 사용 하 여 규칙 보다 먼저 처리 됩니다. 예를 들어 VM 네트워크 어댑터에 각각 weight가 1과 10인 두 개의 규칙을 적용한 weight가 10인 규칙이 먼저 적용됩니다.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Inbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Allow" -Direction "Inbound" -LocalPort 3389 -Protocol "TCP" -Weight 10  
```  
  
### <a name="enforce-both-user-level-and-application-level-security"></a><a name="bkmk_both"></a>사용자 수준 및 응용 프로그램 수준 보안 모두 적용  
하나의 규칙에서 5개 튜플 IP 패킷(원본 IP, 대상 IP, 프로토콜, 원본 포트 및 대상 포트)을 일치시킬 수 있으므로 규칙은 포트 ACL보다 더 세부적인 보안 정책을 적용할 수 있습니다.  
  
예를 들어 제한 된 수의 클라이언트에 DHCP 서비스가 DHCP 서버의 특정 집합을 사용 하 여 컴퓨터를 제공 하려는 경우 Hyper-v, 사용자 Vm 호스팅되는 위치를 실행 하는 Windows Server 2016 컴퓨터에서 다음 규칙을 구성할 수 있습니다.  
  
|원본 IP|대상 IP|프로토콜|원본 포트|대상 포트|Direction|작업|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|주소인|UDP|*|67|바깥쪽|허용|  
|*|10.175.124.0/25|UDP|*|67|바깥쪽|허용|  
|10.175.124.0/25|*|UDP|*|68|안쪽|허용|  
  
다음은 Windows PowerShell 명령을 사용하여 이러한 규칙을 만들 수 있는 방법에 대한 예입니다.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Deny" -Direction "Outbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -RemoteIPAddress 255.255.255.255 -RemotePort 67 -Protocol "UDP"-Weight 10  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -RemoteIPAddress 10.175.124.0/25 -RemotePort 67 -Protocol "UDP"-Weight 20  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Inbound" -RemoteIPAddress 10.175.124.0/25 -RemotePort 68 -Protocol "UDP"-Weight 20  
```  
  
### <a name="provide-security-support-to-a-non-tcpudp-application"></a><a name="bkmk_tcp"></a>비-TCP/UDP 응용 프로그램에 보안 지원 제공  
데이터 센터의 네트워크 트래픽은 대부분 TCP 및 UDP이지만 다른 프로토콜을 사용하는 트래픽도 있습니다. 예를 들어 서버 그룹에서 IGMP(Internet Group Management Protocol)를 기반으로 하는 IP 멀티캐스트 애플리케이션을 실행하도록 허용하려는 경우 다음 규칙을 만들 수 있습니다.  
  
> [!NOTE]  
> IGMP에는 지정된 IP 프로토콜 번호(0x02)가 있습니다.  
  
|원본 IP|대상 IP|프로토콜|원본 포트|대상 포트|Direction|작업|  
|-------------|------------------|------------|---------------|--------------------|-------------|----------|  
|*|*|0x02|*|*|안쪽|허용|  
|*|*|0x02|*|*|바깥쪽|허용|  
  
다음은 Windows PowerShell 명령을 사용하여 이러한 규칙을 만들 수 있는 방법에 대한 예입니다.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Inbound" -Protocol 2 -Weight 20  
Add-VMNetworkAdapterExtendedAcl -VMName "ServerName" -Action "Allow" -Direction "Outbound" -Protocol 2 -Weight 20  
```  
  
## <a name="stateful-acl-rules"></a><a name="bkmk_stateful"></a>상태 저장 ACL 규칙  
확장 ACL의 또 다른 새 기능을 사용하여 상태 저장 규칙을 구성할 수 있습니다. 상태 저장 규칙에는 원본 IP, 대상 IP, 프로토콜, 원본 포트 및 대상 포트-패킷의 5 가지 특성에 따라 패킷을 필터링 합니다.  
  
상태 저장 규칙에는 다음과 같은 기능이 있습니다.  
  
-   항상 트래픽을 허용하며, 트래픽을 차단하는 데에는 사용되지 않습니다.  
  
-   매개 변수 **Direction**의 값을 인바운드로 지정한 경우 트래픽이 규칙과 일치하면 Hyper-V 가상 스위치는 VM에서 외부 리소스에 응답하여 아웃바운드 트래픽을 보낼 수 있도록 일치하는 규칙을 동적으로 만듭니다.  
  
-   매개 변수 **Direction**의 값을 아웃바운드로 지정한 경우 트래픽이 규칙과 일치하면 Hyper-V 가상 스위치는 VM에서 외부 리소스 인바운드 트래픽을 받을 수 있도록 일치하는 규칙을 동적으로 만듭니다.  
  
-   여기에는 초 단위로 측정되는 시간 제한 특성이 포함됩니다. 네트워크 패킷이 스위치에 도착하고 패킷이 상태 저장 규칙과 일치하는 경우 Hyper-V 가상 스위치는 같은 흐름의 양방향 모두에서 모든 후속 패킷이 허용되도록 상태를 만듭니다. 시간 제한 값에 지정된 기간 동안 어느 한 방향으로 트래픽이 없는 경우 상태가 만료됩니다.  
  
다음은 상태 저장 규칙을 사용할 수 있는 방법의 예입니다.  
  
### <a name="allow-inbound-remote-server-traffic-only-after-it-is-contacted-by-the-local-server"></a>로컬 서버에서 연결한 후에만 인바운드 원격 서버 트래픽을 허용  
알려지고 설정된 연결을 추적하고 다른 연결과 구분할 수 있는 규칙은 상태 저장 규칙뿐이기 때문에 상태 저장 규칙을 적용해야 하는 경우가 있습니다.  
  
예를 들어 VM 애플리케이션 서버가 포트 80에서 인터넷상의 웹 서비스에 대한 연결을 시작하도록 허용하고, 원격 웹 서버에서 VM 트래픽에 응답할 수 있도록 하려는 경우 웹 서버에 대한 VM의 초기 아웃바운드 트래픽을 허용하는 상태 저장 규칙을 구성할 수 있습니다. 이 규칙은 상태를 저장하기 때문에 웹 서버의 VM으로의 반환 트래픽도 허용됩니다. 보안상의 이유로 VM에 대한 다른 모든 인바운드 네트워크 트래픽을 차단할 수 있습니다.  
  
이 규칙 구성을 실현하려면 아래 표의 설정을 사용하면 됩니다.  
  
> [!NOTE]  
> 서식 제한 및 정보의 양 때문에 정보가 이 문서의 이전 표와 다르게 표시되어 있습니다.  
  
|매개 변수|규칙 1|규칙 2|규칙 3|  
|-------------|----------|----------|----------|  
|원본 IP|*|*|*|  
|대상 IP|*|*|*|  
|프로토콜|*|*|TCP|  
|원본 포트|*|*|*|  
|대상 포트|*|*|80|  
|Direction|안쪽|바깥쪽|바깥쪽|  
|작업|Deny|Deny|허용|  
|상태 저장|아니요|아니요|예|  
|시간 제한(초)|N/A|N/A|3600|  
  
상태 저장 규칙은 VM 애플리케이션 서버에서 원격 웹 서버에 연결하도록 허용합니다. 첫 번째 패킷이 전송되면 원격 웹 서버로 전송되는 모든 패킷과 원격 웹 서버에서 반환되는 모든 패킷을 허용하도록 Hyper-V 가상 스위치에서 두 가지 흐름 상태를 동적으로 만듭니다. 서버 간의 패킷 흐름이 중지되면 지정된 시간 제한 값(3600초 또는 1시간)에서 흐름 상태가 시간 초과됩니다.  
  
다음은 Windows PowerShell 명령을 사용하여 이러한 규칙을 만들 수 있는 방법에 대한 예입니다.  
  
```  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Inbound" -Weight 1   
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Deny" -Direction "Outbound" -Weight 1  
Add-VMNetworkAdapterExtendedAcl -VMName "ApplicationServer" -Action "Allow" -Direction "Outbound" 80 "TCP" -Weight 100 -Stateful -Timeout 3600  
```  
  


