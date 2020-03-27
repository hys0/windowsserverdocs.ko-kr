---
title: 스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포
description: 이 항목에서는 Windows Server 2016의 스크립트를 사용 하 여 Microsoft SDN (소프트웨어 정의 네트워크) 인프라를 배포 하는 방법을 설명 합니다.
manager: dougkim
ms.prod: windows-server
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: lizross
author: eross-msft
ms.date: 08/23/2018
ms.openlocfilehash: 1a17d5f5fec0a05b4258b295eb37b6dc80cdaee1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313049"
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>스크립트를 사용하여 소프트웨어 정의 네트워크 인프라 배포

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 스크립트를 사용 하 여 Microsoft SDN (소프트웨어 정의 네트워크) 인프라를 배포 합니다. 인프라에는 HA (고가용성) 네트워크 컨트롤러, SLB (HA Software Load Balancer)/MUX, 가상 네트워크 및 연결 된 Access Control 목록 (Acl)이 포함 됩니다. 또한 다른 스크립트는 SDN 인프라의 유효성을 검사 하기 위해 테 넌 트 워크 로드를 배포 합니다.  

테 넌 트 워크 로드가 가상 네트워크 외부에서 통신 하도록 하려면 SLB NAT 규칙, 사이트 간 게이트웨이 터널 또는 계층 3 전달을 설정 하 여 가상 및 실제 워크 로드 간에 라우팅할 수 있습니다.  

Virtual Machine Manager (VMM)를 사용 하 여 SDN 인프라를 배포할 수도 있습니다. 자세한 내용은 [VMM 패브릭에서 SDN (소프트웨어 정의 네트워크) 인프라 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview)을 참조 하세요.  


## <a name="pre-deployment"></a>배포 전  

> [!IMPORTANT]  
> 배포를 시작 하기 전에 호스트 및 실제 네트워크 인프라를 계획 하 고 구성 해야 합니다. 자세한 내용은 [소프트웨어 정의 네트워크 인프라 계획](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)을 참조하세요.  

모든 Hyper-v 호스트에 Windows Server 2016가 설치 되어 있어야 합니다.  

## <a name="deployment-steps"></a>배포 단계  
Hyper-v 호스트의 (물리적 서버) Hyper-v 가상 스위치 및 IP 주소 할당을 구성 하 여 시작 합니다. Hyper-v와 호환 되는 모든 저장소 유형 (공유 또는 로컬)을 사용할 수 있습니다.  

### <a name="install-host-networking"></a>호스트 네트워킹 설치  

1. NIC 하드웨어에 사용할 수 있는 최신 네트워크 드라이버를 설치 합니다.  
2. 모든 호스트에 Hyper-v 역할을 설치 합니다. 자세한 내용은 [Windows Server 2016에서 hyper-v 시작](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/Get-started-with-Hyper-V-on-Windows)을 참조 하세요.   

   ```PowerShell
   Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
   ```  

3. Hyper-v 가상 스위치를 만듭니다.<p>모든 호스트에 대해 동일한 스위치 이름 (예: **Sdnswitch**)을 사용 합니다. 하나 이상의 네트워크 어댑터를 구성 하거나, 설정을 사용 하는 경우 두 개 이상의 네트워크 어댑터를 구성 합니다. Nic 2 개를 사용 하는 경우 최대 인바운드 분산이 발생 합니다.  

   ```PowerShell
   New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True
   ```  
   >[!TIP] 
   >별도의 관리 Nic가 있는 경우 4 단계와 5 단계를 건너뛸 수 있습니다.

3. 계획 항목 ([소프트웨어 정의 네트워크 인프라 계획](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md))을 참조 하 고 네트워크 관리자와 협력 하 여 관리 VLAN의 vlan ID를 가져옵니다. 새로 만든 가상 스위치의 관리 vNIC를 관리 VLAN에 연결 합니다. 환경에서 VLAN 태그를 사용 하지 않는 경우이 단계를 생략할 수 있습니다.  

   ```PowerShell
   Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True
   ```  

4. 계획 항목 ([소프트웨어 정의 네트워크 인프라 계획](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md))을 참조 하 고 네트워크 관리자와 협력 하 여 DHCP 또는 고정 ip 할당을 사용 하 여 새로 만든 VSwitch의 관리 VNIC에 IP 주소를 할당 합니다. 다음 예에서는 고정 IP 주소를 만들어 vSwitch의 관리 vNIC에 할당 하는 방법을 보여 줍니다.  

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>
   ```  

5. 필드 Active Directory Domain Services ([Active Directory Domain Services (수준 100)](https://technet.microsoft.com/library/hh472162.aspx) 및 DNS 서버를 호스트 하는 가상 컴퓨터를 배포 합니다.  

    a. 관리 VLAN에 Active Directory/DNS 서버 가상 컴퓨터를 연결 합니다.

       ```PowerShell
       Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
       ```   

   b. Active Directory Domain Services 및 DNS를 설치 합니다.  

   >[!NOTE]
   >네트워크 컨트롤러는 인증을 위해 Kerberos 및 x.509 인증서를 모두 지원 합니다. 이 가이드에서는 다른 용도로 두 인증 메커니즘을 모두 사용 합니다 (하나만 필요 함).  

6. 모든 Hyper-v 호스트를 도메인에 가입 시킵니다. 관리 네트워크에 할당 된 IP 주소가 있는 네트워크 어댑터에 대 한 DNS 서버 항목이 도메인 이름을 확인할 수 있는 DNS 서버를 가리키는지 확인 합니다. 

   ```PowerShell   
   Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   ```

   a. **시작**을 마우스 오른쪽 단추로 클릭 하 고 **시스템**을 클릭 한 다음 **설정 변경**을 클릭 합니다.  
   b. **변경**을 클릭합니다.  
   c. **도메인** 을 클릭 하 고 도메인 이름을 지정 합니다.  
   . **확인**을 클릭합니다.  
   e. 메시지가 표시 되 면 사용자 이름 및 암호 자격 증명을 입력 합니다.  
   f. 서버를 다시 시작합니다.  

### <a name="validation"></a>유효성 검사  
호스트 네트워킹이 올바르게 설정 되었는지 확인 하려면 다음 단계를 사용 합니다.  

1. VM 스위치가 성공적으로 만들어졌는지 확인 합니다.  

   ```PowerShell
   Get-VMSwitch "<switch name>"
   ```  

2. VM 스위치의 관리 vNIC 관리 VLAN에 연결 되어 있는지 확인 합니다.  

   >[!NOTE]
   >관리 및 테 넌 트 트래픽이 동일한 NIC를 공유 하는 경우에만 해당 됩니다.    

   ```PowerShell
   Get-VMNetworkAdapterIsolation -ManagementOS
   ```

3. 모든 Hyper-v 호스트 및 외부 관리 리소스 (예: DNS 서버)의 유효성을 검사 합니다.<p>관리 IP 주소 및/또는 FQDN (정규화 된 도메인 이름)을 사용 하 여 ping을 통해 액세스할 수 있는지 확인 합니다.   

   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  

4. 배포 호스트에서 다음 명령을 실행 하 고, 사용 되는 Kerberos 자격 증명이 모든 서버에 대 한 액세스를 제공 하도록 각 Hyper-v 호스트의 FQDN을 지정 합니다.  

   ``winrm id -r:<Hyper-V Host FQDN>``  

### <a name="nano-installation-requirements-and-notes"></a>Nano 설치 요구 사항 및 참고 사항  

배포를 위한 Hyper-v 호스트 (물리적 서버)로 Nano를 사용 하는 경우 추가 요구 사항은 다음과 같습니다.  

1. 모든 Nano 노드에는 언어 팩과 함께 설치 된 DSC 패키지가 있어야 합니다.  

   - Microsoft-NanoServer-DSC-Package  
   - NanoServer-Package_en-us

     ``dism /online /add-package /packagepath:<Path> /loglevel:4``  

2. SDN Express 스크립트는 비 Nano 호스트 (Windows Server Core 또는 Windows Server w/GUI)에서 실행 해야 합니다. PowerShell 워크플로는 Nano에서 지원 되지 않습니다.  

3. PowerShell 또는 NC REST 래퍼 (Invoke WebRequest 및 Invoke-restmethod를 사용 하는)를 사용 하 여 네트워크 컨트롤러 NorthBound API를 호출 하려면 비 Nano 호스트에서 작업을 수행 해야 합니다.  


### <a name="run-sdn-express-scripts"></a>SDN Express 스크립트 실행  

1. 설치 파일에 대 한 [MICROSOFT SDN GitHub 리포지토리](https://github.com/Microsoft/SDN.git) 로 이동 합니다.

2. 저장소에서 지정 된 배포 컴퓨터로 설치 파일을 다운로드 합니다. **복제 또는 다운로드** 를 클릭 한 다음 **ZIP 다운로드**를 클릭 합니다.  

   >[!NOTE]
   >지정 된 배포 컴퓨터는 Windows Server 2016 이상을 실행 해야 합니다.

3. Zip 파일을 확장 하 고 **Sdnexpress** 폴더를 배포 컴퓨터의 `C:\` 폴더에 복사 합니다.  

4. **모든 사용자** 가 **읽기/쓰기**권한을 가진 "**sdnexpress**"로 `C:\SDNExpress` 폴더를 공유 합니다.  

5. `C:\SDNExpress` 폴더로 이동 합니다.<p>다음 폴더가 표시 됩니다.  


   | Folder Name |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              설명                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |  AgentConf  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   각 Windows Server 2016 Hyper-v 호스트에서 SDN 호스트 에이전트가 사용 하는 OVSDB 스키마의 새 복사본을 프로그램 네트워크 정책에 보관 합니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |    인증서    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         NC 인증서 파일에 대 한 임시 공유 위치입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |   이미지    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         비어 있습니다. 여기에 Windows Server 2016 vhdx 이미지를 넣습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |    도구    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            문제 해결 및 디버깅을 위한 유틸리티입니다.  호스트 및 가상 컴퓨터에 복사 됩니다.  필요한 경우 사용할 수 있도록 여기에 네트워크 모니터 또는 Wireshark를 추가 하는 것이 좋습니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |   스크립트   | 배포 스크립트.<br /><br />-   **Sdnexpress.** p s 1<br />    네트워크 컨트롤러 가상 컴퓨터, SLB Mux 가상 컴퓨터, 게이트웨이 풀 및 해당 풀에 해당 하는 HNV 게이트웨이 가상 컴퓨터를 포함 하 여 패브릭을 배포 하 고 구성 합니다.<br />-   **FabricConfig psd1**<br />    SDNExpress 스크립트에 대 한 구성 파일 템플릿입니다.  사용자 환경에 맞게 사용자 지정 합니다.<br />-   **SDNExpressTenant**<br />    부하 분산 VIP를 사용 하 여 가상 네트워크에 샘플 테 넌 트 워크 로드를 배포 합니다.<br />    또한 이전에 만든 테 넌 트 워크 로드에 연결 된 서비스 공급자에 지 게이트웨이에서 하나 이상의 네트워크 연결 (IPSec S2S VPN, GRE, L3)을 프로 비전 합니다. IPSec 및 GRE 게이트웨이는 해당 하는 VIP IP 주소와 해당 주소 풀을 통해 L3 전달 게이트웨이를 통해 연결할 수 있습니다.<br />    이 스크립트는 실행 취소 옵션을 사용 하 여 해당 구성을 삭제 하는 데에도 사용할 수 있습니다.<br />-   **tenantconfig**<br />    테 넌 트 워크 로드 및 S2S 게이트웨이 구성에 대 한 템플릿 구성 파일입니다.<br />-   **SDNExpressUndo**<br />    패브릭 환경을 정리 하 고 시작 상태로 다시 설정 합니다.<br />-   **SDNExpressEnterpriseExample**<br />    하나 이상의 엔터프라이즈 사이트 환경을 프로 비전 하 고, 하나 이상의 엔터프라이즈 가상 컴퓨터를 사이트별로 제공 합니다. IPSec 또는 GRE 엔터프라이즈 게이트웨이는 S2S 터널을 설정 하기 위해 서비스 공급자 게이트웨이의 해당 VIP IP 주소에 연결 합니다. L3 전달 게이트웨이는 해당 피어 IP 주소를 통해 연결 합니다. <br />            이 스크립트는 실행 취소 옵션을 사용 하 여 해당 구성을 삭제 하는 데에도 사용할 수 있습니다.<br />-   **EnterpriseConfig psd1**<br />    엔터프라이즈 사이트 간 게이트웨이 및 클라이언트 VM 구성의 템플릿 구성 파일입니다. |
   | TenantApps  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             예제 테 넌 트 작업을 배포 하는 데 사용 되는 파일입니다.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

   ---

6. Windows Server 2016 VHDX 파일이 **Images** 폴더에 있는지 확인 합니다.  

7. 호스트 이름, 도메인 이름, 사용자 이름 및 암호, 네트워크 계획 항목에 나열 된 네트워크에 대 한 네트워크 정보를 비롯 하 여 랩 인프라에 맞게 > > 태그를 특정 값으로 **대체 < <** 변경 하 여 SDNExpress\scripts\FabricConfig.psd1 파일을 사용자 지정 합니다.  

8. NetworkControllerRestName (FQDN) 및 NetworkControllerRestIP에 대 한 호스트 A 레코드를 DNS에 만듭니다.  

9. 도메인 관리자 자격 증명이 있는 사용자로 스크립트를 실행 합니다.  

   ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

10. 모든 작업을 실행 취소 하려면 다음 명령을 실행 합니다.  

    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

#### <a name="validation"></a>유효성 검사  

오류를 보고 하지 않고 SDN Express 스크립트를 완료로 실행 했다고 가정 하면 다음 단계를 수행 하 여 패브릭 리소스를 올바르게 배포 하 고 테 넌 트 배포에 사용할 수 있는지 확인할 수 있습니다.  

[진단 도구](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack) 를 사용 하 여 네트워크 컨트롤러의 패브릭 리소스에 오류가 없는지 확인 합니다.  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  


### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>소프트웨어 부하 분산 장치를 사용 하 여 샘플 테 넌 트 워크 로드 배포  

이제 패브릭 리소스가 배포 되었으므로 샘플 테 넌 트 워크 로드를 배포 하 여 SDN 배포의 유효성을 검사할 수 있습니다. 이 테 넌 트 작업은 SDN 분산 방화벽을 사용 하 여 ACL (Access Control 목록) 규칙을 통해 보호 되는 두 개의 가상 서브넷 (웹 계층 및 데이터베이스 계층)으로 구성 됩니다. 웹 계층의 가상 서브넷은 VIP (가상 IP) 주소를 사용 하 여 SLB/MUX를 통해 액세스할 수 있습니다. 이 스크립트는 두 개의 웹 계층 가상 머신과 하나의 데이터베이스 계층 가상 머신을 자동으로 배포 하 고이를 가상 서브넷에 연결 합니다.  

1.  <를 변경 하 **< > >** 태그를 특정 값 (예: VHD 이미지 이름, 네트워크 컨트롤러 REST 이름, vSwitch 이름 등)으로 변경 하 여 SDNExpress\scripts\TenantConfig.psd1 파일을 사용자 지정 하 여 이전에 FabricConfig psd1 파일에 정의 된 대로  

2.  스크립트를 실행 합니다. 예를 들면 다음과 같습니다.  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

3.  구성을 실행 취소 하려면 실행 **취소** 매개 변수를 사용 하 여 동일한 스크립트를 실행 합니다. 예를 들면 다음과 같습니다.  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>유효성 검사  

테 넌 트 배포가 성공적으로 수행 되었는지 확인 하려면 다음을 수행 합니다.

1. 데이터베이스 계층 가상 컴퓨터에 로그인 하 고 웹 계층 가상 컴퓨터 중 하나의 IP 주소를 ping 해 봅니다. 웹 계층 가상 컴퓨터에서 Windows 방화벽이 꺼져 있는지 확인 합니다.  

2. 네트워크 컨트롤러 테 넌 트 리소스에서 오류를 확인 합니다. 네트워크 컨트롤러에 대 한 계층 3 연결을 사용 하 여 Hyper-v 호스트에서 다음을 실행 합니다.  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``

3. 부하 분산 장치가 올바르게 실행 되 고 있는지 확인 하려면 Hyper-v 호스트에서 다음을 실행 합니다.

   ``wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing``

   여기서 `<VIP IP address>`는 psd1 파일에서 구성한 웹 계층 VIP IP 주소입니다. 

   >[!TIP]
   >Psd1에서 `VIPIP` 변수를 검색 합니다.

   이 복수를 실행 하 여 사용 가능한 Dip 사이에서 부하 분산 장치 스위치를 확인 합니다. 웹 브라우저를 사용 하 여이 동작을 관찰할 수도 있습니다. `<VIP IP address>/unique.htm`로 이동 합니다. 브라우저를 닫고 새 인스턴스를 연 후 다시 검색 합니다. 브라우저에서 캐시 시간이 초과 되기 전에 페이지를 캐시 하는 경우를 제외 하 고 파란색 페이지와 녹색 페이지가 교대로 표시 됩니다.

---