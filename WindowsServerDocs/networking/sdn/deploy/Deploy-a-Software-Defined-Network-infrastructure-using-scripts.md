---
title: 스크립트를 사용 하 여 소프트웨어 정의 네트워크 인프라 배포
description: 이 항목에서는 Windows Server 2016에서 스크립트를 사용 하 여 Microsoft 네트워크 SDN (소프트웨어) 인프라를 배포 하는 방법에 설명 합니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: dabfe3de4cc307723ff7e614fb73e3903e74aeb2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844624"
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>스크립트를 사용하여 소프트웨어 정의 네트워크 인프라 배포

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 스크립트를 사용 하 여 Microsoft 네트워크 SDN (소프트웨어) 인프라를 배포할 수 있습니다. 고가용성 (HA) 네트워크 컨트롤러, HA 소프트웨어 부하 분산 장치 (SLB)를 포함 하는 인프라 / MUX, 가상 네트워크 액세스 제어 목록 (Acl)을 연결 합니다. 또한 다른 스크립트는 SDN 인프라의 유효성을 검사 하는 테 넌 트 워크 로드를 배포 합니다.  
  
가상 네트워크 외부 통신에 테 넌 트 워크 로드를 하려는 경우 SLB NAT 규칙, 사이트 간 게이트웨이 터널 또는 계층 3 전달 가상 및 실제 워크 로드 간에 경로 설정할 수 있습니다.  
  
또한 Virtual Machine Manager (VMM)를 사용 하 여 SDN 인프라를 배포할 수 있습니다. 자세한 내용은 [VMM 패브릭에서 네트워크 SDN (소프트웨어) 인프라 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview)합니다.  

  
## <a name="pre-deployment"></a>배포 전  
  
> [!IMPORTANT]  
> 배포를 시작 하기 전에 계획 하 고 호스트 및 실제 네트워크 인프라를 구성 해야 합니다. 자세한 내용은 [소프트웨어 정의 네트워크 인프라 계획](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)을 참조하세요.  
  
모든 Hyper-v 호스트에는 Windows Server 2016이 설치 되어 있어야 합니다.  
  
## <a name="deployment-steps"></a>배포 단계  
Hyper-v 호스트 (물리적 서버)에서 Hyper-v 가상 스위치 및 IP 주소 할당을 구성 하 여 시작 합니다. Hyper-v, 공유 또는 로컬을 사용 하 여 호환 되는 모든 저장소 형식을 사용할 수 있습니다.  

### <a name="install-host-networking"></a>호스트 네트워킹 설치  

1. NIC 하드웨어에 대 한 사용 가능한 최신 네트워크 드라이버를 설치 합니다.  
2. 모든 호스트에 Hyper-v 역할을 설치 (자세한 내용은 [Windows Server 2016에서 Hyper-v를 사용 하 여 시작](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/Get-started-with-Hyper-V-on-Windows)합니다.   
  
   ```PowerShell
   Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
   ```  
    
3. Hyper-v 가상 스위치를 만드세요.<p>예를 들어, 모든 호스트에 동일한 스위치 이름을 사용 하 여 **sdnSwitch**합니다. 하나 이상의 네트워크 어댑터를 구성 하거나 집합을 사용 하는 경우 두 개 이상의 네트워크 어댑터를 구성 합니다. 두 개의 Nic를 사용 하는 경우 최대 인바운드 확산이 발생 합니다.  

   ```PowerShell
   New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True
   ```  
   >[!TIP] 
   >별도 관리 nic가 있는 경우 4 ~ 5 단계를 건너뛸 수 있습니다.

3. 계획 항목을 참조 하세요 ([소프트웨어 정의 네트워크 인프라 계획](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) 및 관리 VLAN의 VLAN ID를 얻으려면 네트워크 관리자를 사용 하 여 작업 합니다. 새로 만든된 가상 스위치의 관리 vNIC 관리 VLAN에 연결 합니다. 환경의 VLAN 태그를 사용 하지 않는 경우이 단계를 생략할 수 있습니다.  
   
   ```PowerShell
   Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True
   ```  
 
4. 계획 항목을 참조 하세요 ([소프트웨어 정의 네트워크 인프라 계획](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) 하거나 DHCP를 사용 하도록 네트워크 관리자 또는 새로 만든 관리 vNIC IP 주소를 할당할 정적 IP 할당을 사용 하 여 작업과 vSwitch 합니다. 다음 예제에서는 고정 IP 주소를 만들고 vSwitch의 관리 vNIC에 할당 하는 방법을 보여 줍니다.  
 
   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>
   ```  
      
5. [선택 사항] Active Directory 도메인 서비스 호스트에 가상 컴퓨터를 배포 ([Active Directory Domain Services 설치 (수준 100)](https://technet.microsoft.com/library/hh472162.aspx) 및 DNS 서버입니다.  
   
    a. Active Directory/DNS 서버 가상 머신 관리 VLAN에 연결 합니다.
    
       ```PowerShell
       Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
       ```   

   b. Active Directory Domain Services 및 DNS를 설치 합니다.  

   >[!NOTE]
   >네트워크 컨트롤러는 인증에 대 한 Kerberos 및 X.509 인증서를 지원합니다. 이 가이드에서는 다양 한 용도로 모두 인증 메커니즘 사용 (하지만 하나에만 필요).  
        
6. 모든 Hyper-v 호스트를 도메인에 조인 합니다. 도메인 이름을 확인할 수 있는 DNS 서버에 관리 네트워크 지점에 할당 된 IP 주소가 있는 네트워크 어댑터에 대 한 DNS 서버 항목을 확인 합니다. 

   ```PowerShell   
   Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   ```
   
   a. 마우스 오른쪽 단추로 클릭 **시작**, 클릭 **System**를 클릭 하 고 **설정 변경**합니다.  
   b. **변경**을 클릭합니다.  
   다. 클릭 **도메인** 도메인 이름을 지정 합니다.  
   d. **확인**을 클릭합니다.  
   e. 사용자 이름 및 암호 자격 증명 대화 상자가 나타나면을 입력 합니다.  
   f. 서버를 다시 시작합니다.  
  
### <a name="validation"></a>유효성 검사  
사용이 네트워킹 해당 호스트의 유효성을 검사 하려면 다음 단계를 올바르게 설정 됩니다.  

1. VM 스위치가 만들어졌음을 확인 합니다.  
      
   ```PowerShell
   Get-VMSwitch "<switch name>"
   ```  

2. 관리 VM 스위치에서 vNIC 관리 VLAN에 연결 되어 있는지 확인 합니다.  

   >[!NOTE]
   >관리 및 테 넌 트 트래픽이 동일한 NIC를 공유 하는 경우에 관련    
      
   ```PowerShell
   Get-VMNetworkAdapterIsolation -ManagementOS
   ```

3. 모든 Hyper-v 호스트 및 외부 management 리소스를 예를 들어, DNS 서버를 확인 합니다.<p>해당 관리 IP 주소 및/또는 정규화 된 도메인 이름 (FQDN)을 사용 하 여 ping을 통해 액세스할 수 있는지 확인 합니다.   
      
   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  

4. 배포 호스트에서 다음 명령을 실행 하 고 모든 서버에 대 한 액세스를 제공 하는 사용 된 Kerberos 자격 증명을 확인 하려면 각 Hyper-v 호스트의 FQDN을 지정 합니다.  
      
   ``winrm id -r:<Hyper-V Host FQDN>``  
      
### <a name="nano-installation-requirements-and-notes"></a>Nano 설치 요구 사항 및 참고 사항  

Hyper-v 호스트 (물리적 서버)으로 Nano를 사용 하 여 배포 하는 경우 다음 사항이 추가 요구 사항:  

1. 모든 Nano 노드는 DSC 패키지를 언어 팩을 사용 하 여 설치 해야 합니다.  
   
    - Microsoft-NanoServer-DSC-Package.cab  
    - Microsoft-NanoServer-DSC-Package_en-us.cab
   
    ``dism /online /add-package /packagepath:<Path> /loglevel:4``  

2. Nano가 아닌 호스트 (Windows Server Core 또는 GUI 포함 Windows Server)에서 SDN Express 스크립트를 실행 해야 합니다. PowerShell 워크플로 Nano에서 지원 되지 않습니다.  

3.  네트워크 컨트롤러 NorthBound API를 호출 합니다. PowerShell 또는 NC REST 래퍼 (사용 하는 Invoke-webrequest 및 Invoke-restmethod)를 사용 하 여 수행 되어야 합니다 아닌 Nano 호스트에서.  
   
         
### <a name="run-sdn-express-scripts"></a>SDN Express 스크립트를 실행 합니다.  
  
1. 로 이동 합니다 [Microsoft SDN GitHub 리포지토리](https://github.com/Microsoft/SDN.git) 설치 파일에 대 한 합니다.

2. 리포지토리에서 지정 된 배포 컴퓨터에 설치 파일을 다운로드 합니다. 클릭 **복제 또는 다운로드** 을 클릭 한 다음 **ZIP 다운로드**합니다.  
 
   >[!NOTE]
   >지정 된 배포 컴퓨터가 2016 이상 Windows Server를 실행 되어야 합니다.
 
3. 복사 및 zip 파일을 확장 합니다 **SDNExpress** 배포 컴퓨터의 폴더 `C:\` 폴더입니다.  
  
4. 공유 합니다 `C:\SDNExpress` 폴더 "**SDNExpress**"에 대 한 권한을 사용 하 여 **Everyone** 에 **읽기/쓰기**합니다.  
  
5. 이동 된 `C:\SDNExpress` 폴더입니다.<p>다음과 같은 폴더가 표시 됩니다.  

   |폴더 이름|설명|  
   |---------------|---------------|  
   |AgentConf|프로그램 네트워크 정책에 각 Windows Server 2016 Hyper-v 호스트에 SDN 호스트 에이전트를 사용 하는 OVSDB 스키마의 새 복사본을 보유 합니다.|  
   |인증서|NC 인증서 파일에 대 한 임시 공유 위치입니다.|  
   |이미지|빈, 여기에 Windows Server 2016 vhdx 이미지|  
   |Tools|문제 해결 및 디버깅을 위한 유틸리티입니다.  호스트 및 가상 컴퓨터에 복사 합니다.  네트워크 모니터 또는 배치 Wireshark 다음 필요한 경우에 사용할 수 있도록 하는 것이 좋습니다.|  
   |스크립트|배포 스크립트입니다.<br /><br />-   **SDNExpress.ps1**<br />    배포 하 고 네트워크 컨트롤러 가상 컴퓨터, SLB Mux 가상 컴퓨터, 게이트웨이 풀 및 해당 하는 풀 HNV 게이트웨이 가상 컴퓨터를 포함 하는 패브릭을 구성 합니다.<br />-   **FabricConfig.psd1**<br />    SDNExpress 스크립트는 구성 파일 템플릿.  사용자 환경에이 사용자 지정 합니다.<br />-   **SDNExpressTenant.ps1**<br />    부하 분산 된 VIP 사용 하 여 가상 네트워크에는 샘플 테 넌 트 워크 로드를 배포합니다.<br />    또한 이전에 만든된 테 넌 트 워크 로드에 연결 된 서비스 공급자에 지 게이트웨이에서 하나 이상의 네트워크 연결 (IPSec S2S VPN, GRE L3)을 프로 비전 합니다. IPSec 및 GRE 게이트웨이 들이 연결에 사용할 수 있는 해당 VIP IP 주소 및 L3 전달 게이트웨이 통해 해당 주소 풀을 통해.<br />    이 스크립트는 실행 취소 옵션을 함께 사용 하 여 해당 구성을 삭제 하려면 사용할 수 있습니다.<br />-   **TenantConfig.psd1**<br />    테 넌 트 워크 로드 및 S2S 게이트웨이 구성에 대 한 템플릿 구성 파일입니다.<br />-   **SDNExpressUndo.ps1**<br />    Fabric 환경을 정리 하 고 시작 상태 다시 설정 합니다.<br />-   **SDNExpressEnterpriseExample.ps1**<br />    원격 액세스 게이트웨이 하나 (선택 사항) 해당 enterprise 가상 컴퓨터를 당 사이트와 하나 이상의 엔터프라이즈 사이트 환경에 프로 비전합니다. IPSec 나 GRE 엔터프라이즈 게이트웨이 S2S 터널을 설정 하기 위해 서비스 공급자 게이트웨이의 해당 VIP IP 주소에 연결 합니다. L3 전달 게이트웨이 해당 피어 IP 주소를 통해 연결합니다. <br />            이 스크립트는 실행 취소 옵션을 함께 사용 하 여 해당 구성을 삭제 하려면 사용할 수 있습니다.<br />-   **EnterpriseConfig.psd1**<br />    엔터프라이즈 사이트 간 게이트웨이 및 클라이언트 VM 구성에 대 한 템플릿 구성 파일입니다.|  
   |TenantApps|파일을 예제 테 넌 트 워크 로드를 배포 하는 데 사용 합니다.|  
   ---
  
6. Windows Server 2016 VHDX 파일에 있는지 확인 합니다 **이미지** 폴더입니다.  
  
7. SDNExpress\scripts\FabricConfig.psd1 파일을 변경 하 여 사용자 지정 된 **<< 대체 >>** 호스트 이름, 도메인 이름, 사용자 이름 및 암호를 포함 하 여 랩 인프라에 맞게 특정 값을 사용 하 여 태그 및 네트워크 계획 항목에 나열 된 네트워크에 대 한 네트워크 정보입니다.  

8. NetworkControllerRestIP 고 NetworkControllerRestName (FQDN)에 대 한 DNS에서 호스트 A 레코드를 만듭니다.  

9. 도메인 관리자 자격 증명이 있는 사용자로 스크립트를 실행 합니다.  
      
   ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
10. 모든 작업을 실행 취소 하려면 다음 명령을 실행 합니다.  
      
    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
#### <a name="validation"></a>유효성 검사  

SDN Express 스크립트 실행이 완료 된 모든 오류를 보고 하지 않고, 가정 패브릭 리소스 올바르게 배포한 및 테 넌 트 배포에 사용할 수 있도록 다음 단계를 수행할 수 있습니다.  

사용 하 여 [진단 도구](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack) 를 네트워크 컨트롤러에서 패브릭 리소스에 오류가 있는지 확인 하십시오.  
      
   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  
        
   
### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>소프트웨어 부하 분산 장치를 사용 하 여 샘플 테 넌 트 워크 로드 배포  
    
패브릭 리소스를 배포 했으므로 SDN 배포에 종단 간 샘플 테 넌 트 워크 로드를 배포 하 여 확인할 수 있습니다. 이 테 넌 트 워크 로드 구성 두 가상 서브넷 (웹 계층과 데이터베이스 계층) 배포 하는 SDN 방화벽을 사용 하 여 액세스 제어 목록 (ACL) 규칙을 통해 보호 됩니다. 웹 계층의 가상 서브넷은 가상 IP (VIP) 주소를 사용 하 여 SLB/MUX를 통해 액세스할 수 있습니다. 스크립트는 자동으로 두 웹 계층 가상 컴퓨터 및 데이터베이스 계층 가상 컴퓨터를 배포 하 고 가상 서브넷에 연결 합니다.  
  
1.  SDNExpress\scripts\TenantConfig.psd1 파일을 변경 하 여 사용자 지정 된 **<< 대체 >>** 특정 값을 사용 하 여 태그 (예: VHD 이미지 이름, 네트워크 컨트롤러 REST 이름, vSwitch 이름, 앞에서 설명한 대로 FabricConfig.psd1 파일에 정의 하는 등)  

2.  스크립트를 실행 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

3.  구성을 실행 취소를 사용 하 여 동일한 스크립트를 실행 합니다 **실행 취소** 매개 변수입니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>유효성 검사  

테 넌 트 배포가 성공적으로 완료 되었는지 유효성을 검사 하려면 다음을 수행 합니다.

1. 데이터베이스 계층 가상 컴퓨터에 로그인 하 고 (웹 계층 가상 컴퓨터에서 Windows 방화벽이 꺼져 있는지 확인) 웹 계층 가상 컴퓨터 중 하나의 IP 주소를 ping 해 봅니다.  

2. 모든 오류에 대 한 네트워크 컨트롤러 테 넌 트 리소스를 확인 합니다. 네트워크 컨트롤러에 레이어 3 연결을 사용 하 여 모든 Hyper-v 호스트에서 다음을 실행 합니다.  
      
   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``

3. 부하 분산 장치를 올바르게 실행 되 고 있는지를 확인 하려면 모든 Hyper-v 호스트에서 다음을 실행 합니다.
    
   ``wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing``
   
   여기서 `<VIP IP address>` 웹 계층 담당자 TenantConfig.psd1 파일에 구성 된 VIP IP 주소입니다. 

   >[!TIP]
   >검색 된 `VIPIP` 담당자 TenantConfig.psd1 변수입니다.

   부하 분산 장치를 사용할 수 있는 Dip를 전환 하려면이 여러 번 실행 합니다. 또한 웹 브라우저를 사용 하 여이 동작을 확인할 수 있습니다. `<VIP IP address>/unique.htm`으로 이동합니다. 브라우저를 닫고 새 인스턴스를 열고 다시 이동 하 합니다. 파란색 페이지가 및 캐시 시간이 초과 되기 전에 브라우저에서 페이지를 캐시 하는 경우를 제외 하 고 대체 녹색 페이지가 표시 됩니다.

---