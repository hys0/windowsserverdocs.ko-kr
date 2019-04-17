---
title: 스크립트를 사용 하는 소프트웨어 정의 된 네트워크 Infrastructure 배포
description: 이 항목에서는 스크립트 Windows Server 2016에 사용 하 여 Microsoft 소프트웨어 정의 네트워크 (SDN) 인프라를 배포 하는 방법에 설명 합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4428ad73ab8933510d5a759ec4fa7377ea222ebd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>스크립트를 사용 하는 소프트웨어 정의 된 네트워크 Infrastructure 배포

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목에서는 스크립트를 사용 하는 Microsoft 소프트웨어 정의 네트워크 (SDN) 인프라를 배포 하는 방법에 설명 합니다. 인프라 포함 된 만들 소프트웨어 부하 분산 (SLB)를 항상 사용 가능한 (HA) 네트워크 컨트롤러 / MUX, 가상 네트워크 액세스를 제어 (Acl 목록)에 연결 하 고 있습니다. 또한 다른 스크립트 SDN 인프라의 유효성을 검사 하 여 테 작업을 배포 합니다.  
  
가상 네트워크에서 벗어나 있는 소통 하 고 테 작업 원하는 가상 및 물리적 작업 간에 경로 SLB NAT 규칙, 인 사이트 게이트웨이 터널 또는 계층 3 전달를 설정할 수 있습니다.  
  
가상 컴퓨터 관리자 VMM ()를 사용 하 여 SDN 인프라를 배포할 수 있습니다. 자세한 내용은 참조 [VMM 패브릭에서 소프트웨어 정의 네트워크 (SDN) 인프라 설정](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview)합니다.  
  
## <a name="pre-deployment"></a>예약 배포  
  
> [!IMPORTANT]  
> 배포를 시작 하기 전에 계획 하 고 호스트와 실제 네트워크 infrastructure 구성 해야 합니다. 자세한 내용은 참조 [소프트웨어 정의 네트워크 Infrastructure 계획](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)합니다.  
  
모든 Hyper-v 호스트 Windows Server 2016 설치 되어 있어야 합니다.  
  
## <a name="deployment-steps"></a>배포 단계  
구성 Hyper-v 호스트 (실제 서버) Hyper-v의 가상 스위치와 IP 주소를 지정 하 여 시작 합니다. Hyper-v, 공유 또는 로컬와 호환 되는 모든 저장소 입력을 사용할 수 있습니다.  
### <a name="install-host-networking"></a>네트워킹 호스트 설치  
1. NIC 하드웨어에 사용 가능한 최신 네트워크 드라이버를 설치 합니다.  
2. 모든 호스트 Hyper-v 역할을 설치 (자세한 내용은 참조 [Windows Server 2016에 Hyper-v 시작](https://technet.microsoft.com/en-us/library/mt126159.aspx)합니다.   
  
   관리자 Windows PowerShellcommand 프롬프트에서:  
   ``Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart``  
    
    한 합니다. Hyper-v 가상 스위치 (사용에 대 한 모든 호스트 스위치 이름이 같은 만들기. For example: **sdnSwitch**). 하나 이상의 네트워크 어댑터를 구성 하거나, Embedded 팀 스위치를 사용 하는 경우 두 개 이상 네트워크 어댑터를 구성 합니다. 최대 인바인드 확산 두 Nic를 사용 하는 경우 발생 합니다.  
 `` New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True``  
 
 >[!NOTE] 
 >별도 관리 Nic 있는 경우 3-4 단계를 건너뛸 수 있습니다.

3. 계획 항목을 참조 ([소프트웨어 정의 네트워크 Infrastructure 계획](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) 관리 vlan VLAN ID를 받으려면 네트워크 관리자가 작동 하 고 있습니다. 관리 VLAN 새로 만든 가상 스위치 관리 vNIC 연결 합니다. 귀하의 환경 VLAN 태그를 사용 하지 않는 경우이 단계를 생략 수 있습니다.  
 `` Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True``  
 
4. 계획 항목을 참조 ([소프트웨어 정의 네트워크 Infrastructure 계획](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) 작업 중 하나 DHCP를 사용 하 여 네트워크 관리자 또는 새로 만든된 vSwitch의 관리 vNIC에 IP 주소를 지정 하려면 고정 IP 할당 합니다. 고정 IP 주소를 만들고 하 고 vSwitch의 관리 vNIC 지정 하는 방법은 다음과 같습니다.  
 ``New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>``  
      
5. [선택적] 호스트 Active Directory Domain Services 가상 컴퓨터에 배포한 ([설치 Active Directory Domain Services (수준을 100)](https://technet.microsoft.com/library/hh472162.aspx) 와 DNS 서버 합니다.  
   
    한 합니다. Active Directory/DNS 서버 가상 컴퓨터 관리 VLAN에 연결 합니다.
    
            Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
   
   B 합니다. Active Directory Domain Services와 DNS 설치 합니다.  
      >[!NOTE]
      >네트워크 컨트롤러 인증을 위한 인증서 Kerberos 및 X.509을 지원합니다. 이 가이드 (필수 하나만 되어도) 다양 한 목적 모두 인증 메커니즘을 사용 합니다.  
        
6. 도메인에 있는 모든 Hyper-v 호스트 연결 합니다. IP 주소가 도메인 이름 확인할 수 있는 DNS 서버 관리 네트워크 지점에 할당 된 네트워크 어댑터에 대 한 항목이 활성화 된 DNS 서버를 확인 합니다. 예를 들어:

        Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   
   한 합니다. 마우스 오른쪽 단추로 클릭 **시작**, 클릭 **시스템**을 차례로 클릭 하 고 **설정 변경**합니다.  
   B 합니다. 클릭 **변경**합니다.  
   C 합니다. 클릭 **도메인** 도메인 이름 지정 하 고 있습니다.  
   D 합니다. 클릭 **확인**합니다.  
   E 합니다. 메시지가 표시 되 면 사용자 이름 및 암호 자격을 입력 합니다.  
   F 합니다. 서버를 다시 시작 합니다.  
  
### <a name="validation"></a>유효성 검사  
사용 하 여 네트워킹 호스트 확인 하려면 다음 단계를 올바르게 설정 되어 있습니다.  
1. VM 스위치 만들었습니다 있는지 확인 합니다.  
      
    ``Get-VMSwitch "<switch name>"``  
2. VM 스위치 관리 vNIC 관리 VLAN에 연결 되어 있는지 확인 합니다.  
    >[!NOTE]
    >관리 및 테 교통 같은 NIC 공유 하는 경우에 해당    
      
    ``Get-VMNetworkAdapterIsolation -ManagementOS``  
3. 하는지 확인할 모든 Hyper-v 호스트 (및 외부의 관리 리소스: DNS 서버) 자녀가 관리 IP 주소 및/또는 정식된 FQDN (도메인 이름)을 사용 하 여 ping를 통해 액세스할 수 있습니다.   
      
   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  
4. 배포 호스트에서 다음 명령을 실행 하 고 모든 서버에 대 한 액세스를 제공 하는 각 Hyper-v 호스트 사용 Kerberos 자격 증명을 위해 FQDN 지정 합니다.  
      
   ``winrm id -r:<Hyper-V Host FQDN>``  
      
### <a name="nano-installation-requirements-and-notes"></a>메모 하 고 Nano 설치 요구 사항  
배포에 대 한 Hyper-v 호스트 (실제 서버) Nano를 사용 하는 경우 추가 요구 사항은 다음과 같습니다.  
1. 모든 Nano 노드 DSC 패키지 언어 팩과 함께 설치 해야 합니다.  
   
   * Microsoft-NanoServer-DSC-Package.cab  
   * Microsoft-NanoServer-DSC-Package_en-us.cab
   
        ``dism /online /add-package /packagepath:<Path> /loglevel:4``  
2. SDN Express 스크립트 비 Nano 호스트 (Windows Server의 핵심 또는 Windows Server GUI 포함)를에서 실행 해야 합니다. PowerShell 워크플로 Nano에서 지원 되지 않습니다.  
3.  네트워크 컨트롤러 NorthBound API PowerShell 또는 NC 나머지 래퍼 (있음 Invoke-WebRequest와 Invoke-RestMethod 사용) 사용 하 여 해야 호출할 비 Nano 호스트에서 합니다.  
   
         
### <a name="run-sdn-express-scripts"></a>기본 스크립트 SDN 실행  
  
1.  설치 파일은 GitHub에서 있습니다. Zip 파일을 다운로드는 [Microsoft SDN GitHub 저장소](https://github.com/Microsoft/SDN.git)합니다. Microsoft SDN 저장소 페이지, 클릭 **복제 또는 다운로드** 차례로 클릭 하 고 **ZIP 다운로드**합니다.  
  
2.  배포 컴퓨터도 컴퓨터를 지정 합니다.  이 컴퓨터 Windows Server 2016을 실행 해야 합니다. Zip 파일 및 복사 확장는 **SDNExpress** 배포 컴퓨터에 폴더 `C:\`폴더 합니다.  
  
3.  공유는 `C:\SDNExpress`폴더 "**SDNExpress**"에 대 한 권한이 있는 **모든** 에 **읽기/쓰기**합니다.  
  
4.  이동 하 여 `C:\SDNExpress`폴더 합니다.

 다음과 같은 폴더가 나타납니다.  

|폴더 이름|설명|  
|---------------|---------------|  
|AgentConf|새 프로그램 네트워크 정책으로 각 Windows Server 2016 Hyper-v 호스트 SDN 호스트 에이전트가에서 사용 되는 OVSDB 스키마 복사본 보유 합니다.|  
|인증서|임시 NC 인증서 파일에 대 한 위치를 공유 합니다.|  
|이미지|비우기, Windows Server 2016 vhdx 이미지 여기 장소|  
|도구|문제 해결 및 디버깅에 대 한 유틸리티입니다.  호스트 및 가상 컴퓨터에 복사 합니다.  배치 하는 네트워크 모니터 또는 Wireshark 여기서 필요한 경우에 사용할 수 있도록 하는 것이 좋습니다.|  
|스크립트|배포 스크립트 합니다.<br /><br />-   **SDNExpress.ps1**<br />    배포 하 고 네트워크 컨트롤러 가상 컴퓨터, SLB Mux 가상 컴퓨터, 게이트웨이 풀에 해당 하는 풀 HNV 게이트웨이 가상 컴퓨터 등 패브릭을 구성 합니다.<br />-   **FabricConfig.psd1**<br />    SDNExpress 스크립트에 대 한 구성 파일 템플릿을 합니다.  귀하의 환경에 대 한이 사용자 지정 합니다.<br />-   **SDNExpressTenant.ps1**<br />    부하가 VIP 사용 하 여 가상 네트워크에서 샘플 테 작업을 배포합니다.<br />    또한 이전에 만든된 테 작업에 연결 되는 서비스 공급자 edge 게이트웨이에서 하나 이상의 네트워크 연결 (IPSec S2S VPN, GRE, l 3) 구축 합니다. IPSec 및 GRE 게이트웨이 연결에 사용할 수 있는 l 3 전달 게이트웨이 및 해당 VIP IP 주소, 해당 주소 풀을 통해 합니다.<br />    이 스크립트 취소 옵션을 사용 하 여 해당 구성도 삭제를 사용할 수 있습니다.<br />-   **TenantConfig.psd1**<br />    서식 구성 테 작업과 S2S 게이트웨이 구성에 대 한 파일.<br />-   **SDNExpressUndo.ps1**<br />    패브릭 환경 정리 하 고 시작 상태를 다시 설정 합니다.<br />-   **SDNExpressEnterpriseExample.ps1**<br />    한 원격 액세스 게이트웨이 사이트 마다 하나의 (선택 사항) 해당 enterprise 가상 컴퓨터와 하나 또는 여러 개의 엔터프라이즈 사이트 환경을 제공 합니다. IPSec 또는 GRE 엔터프라이즈 게이트웨이 S2S 터널 설정를 서비스 공급자 게이트웨이의 해당 VIP IP 주소에 연결 합니다. L 3 전달 게이트웨이 해당 피어 IP 주소를 통해 연결합니다. <br />            이 스크립트 취소 옵션을 사용 하 여 해당 구성도 삭제를 사용할 수 있습니다.<br />-   **EnterpriseConfig.psd1**<br />    템플릿 구성 엔터프라이즈 사이트 게이트웨이 및 클라이언트 VM 구성에 대 한 파일.|  
|TenantApps|파일이 들어 테 작업을 배포 하는 데 사용 합니다.|  
  
5.  Windows Server 2016 VHDX 파일 인지 확인는 **이미지** 폴더 합니다.  
  
6. SDNExpress\scripts\FabricConfig.psd1 파일을 변경 하 여 사용자 지정 하는 **<< 교체 >>** 계획 네트워크 항목에 태그 호스트 이름, 도메인 이름, 사용자 이름 및 암호를 포함 하 여 랩 인프라 적합 하도록 하는 네트워크에 대 한 정보를 네트워크 특정 값으로 나열 됩니다.  
7. NetworkControllerRestName (FQDN) 및 NetworkControllerRestIP dns에서 호스트 A 기록을 생성 합니다.  
8. 사용자 도메인 관리자 자격 증명으로 스크립트를 실행할.  
      
    ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
9.  모든 작업을 취소 하려면 다음 명령을 실행 합니다.  
      
    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
#### <a name="validation"></a>유효성 검사  
가정 SDN Express 스크립트 원활 하 게 완료 될 때까지 된 오류 보고, 하 고 패브릭 리소스 배포한 올바르게 되며 테 배포를 위해 사용할 수 있는지 확인 하려면 다음 단계를 수행할 수 있습니다.  

- 사용 하 여 [진단 도구](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack) 네트워크 컨트롤러에서 패브릭 리소스에 오류가 없는 수 있도록 합니다.  
      
    ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  
        
   
### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>소프트웨어 부하 분산와 샘플 테 작업을 배포 합니다.  
    
패브릭 리소스를 배포 했으므로 샘플 테 작업을 배포 하 여 사용자 SDN 배포-끝을 확인할 수 있습니다. 이와 같은 테 작업 두 가상 서브넷 (웹 계층와 데이터베이스 계층) 배포 SDN 방화벽을 사용 하 여 목록 ACL (액세스 제어) 규칙을 통해 보호 구성 되어 있습니다. 웹 계층 가상 서브넷은 가상 IP (VIP) 주소를 사용 하 여 SLB/MUX를 통해 액세스할 수 있습니다. 자동으로 스크립트 두 웹 계층 가상 컴퓨터 및 한 데이터베이스 계층 가상 컴퓨터를 배포 하 고 가상 서브넷에 연결 합니다.  
  
1.  SDNExpress\scripts\TenantConfig.psd1 파일을 변경 하 여 사용자 지정 하 고 **<< 교체 >>** 특정 값으로 태그 (예: VHD 이미지, 네트워크 컨트롤러 나머지 이름, vSwitch 이름, FabricConfig.psd1 파일에 이전에 정의 된 등)  
2.  스크립트를 실행 합니다. 예를 들어:  
``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  
3.  구성을 취소 하려면와 동일한 스크립트를 실행할는 **취소** 매개 합니다. 예를 들어:  
``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>유효성 검사  
이 성공적으로 테 배포의 유효성을 검사 하려면 다음을 수행 합니다.
1.  데이터베이스 계층 가상 컴퓨터에 로그인 하 고 웹 계층 가상 컴퓨터 (웹 계층 가상 컴퓨터에서 Windows 방화벽 꺼져 있는지 확인) 중 하나의 IP 주소를 다시 ping 해 보세요.  
2.  오류에 대 한 네트워크 컨트롤러 테 리소스를 확인 합니다. 네트워크 컨트롤러 모든 Hyper-v 호스트 계층 3 연결 다음을 실행 합니다.  
      
    ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``
3. 부하 분산 제대로 실행 되 고 있는지를 확인 하려면 다음 Hyper-v 호스트 모든에서 실행 합니다.
    
        wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing
   
   여기서 `<VIP IP address>`TenantConfig.psd1 파일에서 구성 된 VIP IP 주소 웹 계층입니다. 검색에서 `VIPIP`TenantConfig.psd1에서 가변 합니다.

   사용 가능한 Dip 사이 전환 부하 분산 보려면이 복수 번 실행 됩니다. 또한 웹 브라우저를 사용 하 여이 문제를 확인할 수 있습니다. 찾아보기 `<VIP IP address>/unique.htm`합니다. 새 인스턴스의 브라우저를 닫 및 열고 다시 검색 합니다. 파란색 페이지와 캐시 꺼지기 전 브라우저 페이지를 캐시 하는 경우를 제외 하 고 암호 확인용 녹색 페이지가 표시 됩니다.