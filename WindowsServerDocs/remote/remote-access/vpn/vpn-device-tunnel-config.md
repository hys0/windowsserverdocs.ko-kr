---
title: Windows 10에서 VPN 장치 터널 구성
description: Windows 10에서 VPN 장치 터널을 만드는 방법을 알아봅니다.
ms.prod: windows-server-threshold
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 005721873ad3a0df942bc9e23eba13728965ccba
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067313"
---
# Windows 10에서 VPN 장치 터널 구성

>적용 대상: Windows 10 버전 1709

Always On VPN을 디바이스 또는 컴퓨터에 대 한 전용된 VPN 프로필을 만들 수가 있습니다. Always On VPN 연결 두 가지 유형의 터널 다음과 같습니다. 

- _장치 터널_ 장치에서 사용자가 로그온 하기 전에 지정 된 VPN 서버에 연결합니다. 사전 로그인 연결 시나리오 및 장치 관리 목적으로 장치 터널을 사용합니다.

- 사용자가 장치에 로그온 한 후에 _사용자 터널_ 연결합니다. 사용자 터널 VPN 서버를 통해 조직의 리소스에 액세스할 수 있습니다.

_사용자 터널_을 연결 하는 사용자가 디바이스 또는 컴퓨터에 로그온 한 후, 달리 _장치 터널_ 연결을 사용자가 로그온 하기 전에 VPN이 있습니다. _장치 터널_ 및 _사용자 터널_ 모두 자신의 VPN 프로필을 사용 하 여 독립적으로 작동 이와 동시에 연결할 수 및 다른 인증 방법 및 다른 VPN 구성 설정을 적절 하 게 사용할 수 있습니다. 사용자 터널 SSTP 및 IKEv2, 지원 및 장치 터널와 SSTP 대체에 대 한 지원 되지 않는 IKEv2를 지원 합니다.

사용자 터널에서 지원 도메인 가입 미가입 (작업 그룹) 또는 Azure AD 가입 – 디바이스 엔터프라이즈 및 BYOD 시나리오 모두 가능 하도록 합니다. 모든 Windows 버전에서 사용할 수 있는 이며 UWP VPN 플러그 인을 지원 통해 제 3 자에 사용할 수 있는 플랫폼 기능입니다.

장치 터널 1709 이상 Windows 10 Enterprise 또는 Education 버전을 실행 하는 도메인에 가입 된 디바이스에만 구성할 수 있습니다. 장치 터널의 타사 컨트롤에 대 한 지원 되지 않습니다.


## 장치 터널 요구 사항 및 기능
VPN 연결에 대 한 컴퓨터 인증서 인증을 사용 하도록 설정 하 고 들어오는 VPN 연결을 인증 하기 위한 루트 인증 기관 정의 해야 합니다. 

```PowerShell
$VPNRootCertAuthority = “Common Name of trusted root certification authority”
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like “*$VPNRootCertAuthority*” })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![장치 터널 기능 및 요구 사항](../../media/device-tunnel-feature-and-requirements.png)

## VPN 장치 터널 구성

시나리오 클라이언트만 당겨 시작 위치에 대 한 좋은 지침을 제공 하는 아래 XML 샘플 프로필은 장치 터널을 통해 필요 합니다.  트래픽 필터 관리 트래픽만를 장치 터널을 제한 하기 위해 활용 됩니다.  이 구성은 Windows Update, 일반적인 GP (그룹 정책) 및 System Center Configuration Manager (SCCM) 업데이트 시나리오 뿐 아니라 처음 로그온 캐시 된 자격 증명 없이 대 한 VPN 연결에 적합 하거나 암호 시나리오를 초기화 합니다. 

Windows 원격 관리 (WinRM), 원격 GPUpdate 및 원격 SCCM 업데이트 시나리오와 같은 서버 시작 푸시 사례에 대 한 트래픽 필터를 사용할 수 있도록 장치 터널 인바운드 트래픽을 허용 해야 합니다.  장치 터널 프로필 트래픽 필터에 설정, 장치 터널 인바운드 트래픽을 거부 합니다.  이 제한은 이후 릴리스에서 제거 될 것입니다.


### VPN profileXML 샘플

다음은 샘플 VPN profileXML입니다.

``` xml
<VPNProfile>  
  <NativeProfile>  
<Servers>vpn.contoso.com</Servers>  
<NativeProtocolType>IKEv2</NativeProtocolType>  
<Authentication>  
  <MachineMethod>Certificate</MachineMethod>  
</Authentication>  
<RoutingPolicyType>SplitTunnel</RoutingPolicyType>  
 <!-- disable the addition of a class based route for the assigned IP address on the VPN interface -->
<DisableClassBasedDefaultRoute>true</DisableClassBasedDefaultRoute>  
  </NativeProfile> 
  <!-- use host routes(/32) to prevent routing conflicts -->  
  <Route>  
<Address>10.10.0.2</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
  <Route>  
<Address>10.10.0.3</Address>  
<PrefixSize>32</PrefixSize>  
  </Route>  
<!-- traffic filters for the routes specified above so that only this traffic can go over the device tunnel --> 
  <TrafficFilter>  
<RemoteAddressRanges>10.10.0.2, 10.10.0.3</RemoteAddressRanges>  
  </TrafficFilter>
<!-- need to specify always on = true --> 
  <AlwaysOn>true</AlwaysOn> 
<!-- new node to specify that this is a device tunnel -->  
 <DeviceTunnel>true</DeviceTunnel>
<!--new node to register client IP address in DNS to enable manage out -->
<RegisterDNS>true</RegisterDNS>
</VPNProfile>
```

각 특정 배포 시나리오의 요구 사항에 따라 장치 터널을 사용 하 여 구성할 수 있는 또 다른 VPN 기능에는 [신뢰할 수 있는 네트워크 검색](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection).

```
 <!-- inside/outside detection --> 
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection> 
```

## 배포 및 테스트

Windows PowerShell 스크립트를 사용 하 여 Windows Management Instrumentation \(WMI\) 브리지를 사용 하 여 장치 터널을 구성할 수 있습니다. Always On VPN 장치 터널의 **로컬 시스템** 계정 컨텍스트에서 구성 되어야 합니다. 이를 위해서는 [PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec), 유틸리티 [Sysinternals](https://docs.microsoft.com/sysinternals/) 제품군에 포함 된 [PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools) 중 하나를 사용 하 여 해야 합니다.

배포 하는 방법에 대 한 지침을 장치당 `(.\Device)` 비교는 사용자 당 `(.\User)` 프로필을 [사용 하 여 PowerShell scripting with WMI Bridge Provider를](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider)참조 하세요. 

장치 프로 파일 배포한 성공적으로 확인 하는 다음 Windows PowerShell 명령을 실행 합니다.

    `Get-VpnConnection -AllUserConnection`

출력 장치에 배포 되는 전체 device\ VPN 프로필의 목록을 표시 합니다.


### Windows PowerShell 스크립트 예

프로필 만들기에 대 한 사용자 고유의 스크립트 만들기에 도움이 되도록 다음 Windows PowerShell 스크립트를 사용할 수 있습니다.

```PowerShell
Param(
[string]$xmlFilePath,
[string]$ProfileName
)

$a = Test-Path $xmlFilePath
echo $a

$ProfileXML = Get-Content $xmlFilePath

echo $XML

$ProfileNameEscaped = $ProfileName -replace ' ', '%20'

$Version = 201606090004

$ProfileXML = $ProfileXML -replace '<', '&lt;'
$ProfileXML = $ProfileXML -replace '>', '&gt;'
$ProfileXML = $ProfileXML -replace '"', '&quot;'

$nodeCSPURI = './Vendor/MSFT/VPNv2'
$namespaceName = "root\cimv2\mdm\dmmap"
$className = "MDM_VPNv2_01"

$session = New-CimSession

try
{
$newInstance = New-Object Microsoft.Management.Infrastructure.CimInstance $className, $namespaceName
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ParentID", "$nodeCSPURI", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("InstanceID", "$ProfileNameEscaped", 'String', 'Key')
$newInstance.CimInstanceProperties.Add($property)
$property = [Microsoft.Management.Infrastructure.CimProperty]::Create("ProfileXML", "$ProfileXML", 'String', 'Property')
$newInstance.CimInstanceProperties.Add($property)

$session.CreateInstance($namespaceName, $newInstance)
$Message = "Created $ProfileName profile."
Write-Host "$Message"
}
catch [Exception]
{
$Message = "Unable to create $ProfileName profile: $_"
Write-Host "$Message"
exit
}
$Message = "Complete."
Write-Host "$Message"
```

## 추가 리소스

다음은 VPN 배포를 지원 하기 위해 추가 리소스입니다.

### VPN 클라이언트 구성 리소스

다음은 VPN 클라이언트 구성 리소스입니다.

- [System Center Configuration Manager에서 만드는 VPN 프로필 하는 방법](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles)
- [Windows 10 클라이언트 Always On VPN 연결 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### 원격 액세스 서버 \(RAS\) 게이트웨이 리소스

다음은 RAS 게이트웨이 리소스입니다.

- [컴퓨터 인증 인증서를 사용 하 여 RRAS 구성](https://technet.microsoft.com/library/dd458982.aspx)
- [IKEv2 VPN 연결 문제 해결](https://technet.microsoft.com/library/dd941612.aspx)
- [IKEv2 기반 원격 액세스 구성](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>설명 된 대로 **IKEv2에 대 한 허용 컴퓨터 인증서** 인증 방법을 사용 하 여 IKEv2 컴퓨터 인증서 인증을 지원 하도록 RRAS 서버를 구성 해야 장치 터널 Microsoft RAS 게이트웨이 사용 하는 경우 [다음과 같습니다](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29). 이 설정을 사용 하도록 설정 것이 좋습니다 **집합 VpnAuthProtocol** PowerShell cmdlet **RootCertificateNameToAccept** 선택적 매개 변수를 함께 RRAS IKEv2 연결에 대 한만 허용 되는지 확인 하는 VPN 클라이언트는 해당 체인을 명시적으로 정의 된 내부/개인 루트 인증 기관에 인증서입니다. 또는 설명한 [여기](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)와 공공 인증 기관 포함 되지 않는 RRAS 서버에서 **신뢰할 수 있는 루트 인증 기관** 저장소를 수정 해야 합니다. 유사한 메서드 다른 VPN 게이트웨이 대 한 것으로 간주 해야 합니다.

---
