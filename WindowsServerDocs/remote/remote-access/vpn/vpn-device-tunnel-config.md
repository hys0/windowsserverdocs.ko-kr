---
title: Windows 10에서 VPN 장치 터널 구성
description: Windows 10에서 VPN 장치 터널을 만드는 방법에 알아봅니다.
ms.prod: windows-server-threshold
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 989216f90e78689b464240cff957bab1d9c1229b
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749566"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>Windows 10에서 VPN 장치 터널 구성

>적용 대상: Windows 10 버전 1709

Always On VPN 장치 또는 컴퓨터에 대 한 전용된 VPN 프로필을 만들 수가 있습니다. Always On VPN 연결에는 터널의 두 가지 유형이 포함 됩니다. 

- _장치 터널_ 장치 사용자가 로그온 하기 전에 지정 된 VPN 서버에 연결 합니다. 사전 로그인 연결 시나리오 및 장치 관리 목적으로 장치 터널을 사용 합니다.

- _사용자 터널_ 사용자 장치에 로그온 한 후에 연결 합니다. 사용자 터널을 사용 하면 VPN 서버를 통해 조직 리소스에 액세스할 수 있습니다.

와 달리 _사용자 터널_만 연결 하는 사용자가 장치 또는 컴퓨터에 로그온 한 후 _장치 터널_ VPN 사용자가 로그온 하기 전에 연결을 허용 합니다. 둘 다 _장치 터널_ 하 고 _사용자 터널_ 해당 VPN 프로필을 사용 하 여 독립적으로 작동할 동시에 연결 될 수 있으며 다른 인증 방법 및 다른 VPN 구성 설정을 사용할 수 있습니다 적절 하 게 합니다. 사용자 터널 SSTP 및 IKEv2를 지원 하 고 장치 터널 SSTP 대체 (fallback) 지원 되지 않습니다 함께만 IKEv2를 지원 합니다.

사용자 터널에는 도메인에 가입 된, 비도메인 가입 (작업 그룹) 또는 enterprise와 BYOD 시나리오에 대 한 허용 하도록 Azure AD-가입 된 장치입니다. 모든 Windows 버전에서 사용할 수 있습니다 및 플랫폼 기능은 UWP VPN 플러그 인 지원을 통해 타사에 사용할 수 있습니다.

장치 터널은 Windows 10 Enterprise 또는 교육용 버전 1709 이상을 실행 하는 도메인에 가입 된 장치에만 구성할 수 있습니다. 장치 터널의 타사 컨트롤에 대 한 지원은 없습니다.


## <a name="device-tunnel-requirements-and-features"></a>장치 터널 요구 사항 및 기능
VPN 연결에 대 한 컴퓨터 인증서 인증을 사용 하도록 설정 하 고 들어오는 VPN 연결을 인증 하는 것에 대 한 루트 인증 기관 정의 해야 합니다. 

```PowerShell
$VPNRootCertAuthority = “Common Name of trusted root certification authority”
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like “*$VPNRootCertAuthority*” })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![장치 터널 기능 및 요구 사항](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>VPN 장치 터널 구성

장치 터널을 통해 시나리오만 클라이언트에서 풀을 시작 하는 위치에 대 한 좋은 지침을 제공 하는 다음 XML 샘플 프로필 필수 이며  트래픽 필터를 활용 하 여 장치 터널 관리 트래픽만 제한 합니다.  이 구성은 Windows 업데이트, 일반적인 그룹 정책 (GP) 및 System Center Configuration Manager (SCCM) 업데이트 시나리오와 캐시 된 자격 증명 없이 첫 번째 로그온에 대 한 VPN 연결에 적합 하거나 암호 재설정 시나리오. 

Windows Remote Management (WinRM), 원격 GPUpdate 및 원격 SCCM 업데이트 시나리오와 같은 푸시 서버에서 시작한 경우에 대 한 트래픽 필터를 사용할 수 있도록 장치 터널 인바운드 트래픽을 허용 해야 합니다.  장치 터널 프로필의 트래픽 필터를 설정한 경우 장치 터널 인바운드 트래픽을 거부 합니다.  이 제한은 향후 릴리스에서 제거 될 예정입니다.


### <a name="sample-vpn-profilexml"></a>샘플 VPN profileXML

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

각 특정 배포 시나리오의 요구에 따라 다른 VPN 장치 터널을 사용 하 여 구성할 수 있는 기능은 [신뢰할 수 있는 네트워크 검색](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection)합니다.

```
 <!-- inside/outside detection -->
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

## <a name="deployment-and-testing"></a>배포 및 테스트

Windows PowerShell 스크립트를 사용 하 고 Windows Management Instrumentation (WMI) 브리지를 사용 하 여 장치의 터널을 구성할 수 있습니다. Always On VPN 장치 터널의 컨텍스트에서 구성 해야 합니다 **로컬 시스템** 계정. 이를 위해 사용 하는 데 필요한 됩니다 [PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec)하나씩의 합니다 [PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools) 에 포함는 [Sysinternals](https://docs.microsoft.com/sysinternals/) 유틸리티입니다.

배포 하는 방법에 대 한 지침을 장치당 `(.\Device)` 비교는 사용자별 `(.\User)` 프로필을 참조 하세요 [WMI 연결 공급자를 사용 하 여 PowerShell 스크립팅을](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider).

장치 프로필을 성공적으로 배포 되었는지 확인 하려면 다음 Windows PowerShell 명령을 실행 합니다.

  ```powershell
  Get-VpnConnection -AllUserConnection
  ```

출력 장치 목록이 표시 됩니다.\-장치에 배포 된 VPN 프로필 다양 합니다.

### <a name="example-windows-powershell-script"></a>Windows PowerShell 스크립트 예제

프로필 만들기에 대 한 사용자 지정 스크립트를 만드는 데 유용한 다음 Windows PowerShell 스크립트를 사용할 수 있습니다.

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

## <a name="additional-resources"></a>추가 리소스

VPN 배포에 도움이 되는 추가 리소스는 다음과 같습니다.

### <a name="vpn-client-configuration-resources"></a>VPN 클라이언트 구성 리소스

VPN 클라이언트 구성 리소스는 다음과 같습니다.

- [System Center Configuration Manager에서 VPN 프로필을 만드는 방법](https://docs.microsoft.com/sccm/protect/deploy-use/create-vpn-profiles)
- [Windows 10 클라이언트를 VPN 연결에 always On 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-gateway-resources"></a>원격 액세스 서버 게이트웨이 리소스

원격 액세스 서버 (RAS) 게이트웨이 리소스는 다음과 같습니다.

- [컴퓨터 인증 인증서를 사용 하 여 RRAS 구성](https://technet.microsoft.com/library/dd458982.aspx)
- [IKEv2 VPN 연결 문제 해결](https://technet.microsoft.com/library/dd941612.aspx)
- [IKEv2 기반의 원격 액세스 구성](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>장치 터널을 사용 하 여 Microsoft RAS 게이트웨이 사용 하 여 IKEv2 컴퓨터 인증서 인증을 지원 하도록 RRAS 서버를 구성 해야 합니다는 **IKEv2 용 컴퓨터 인증서 인증을 허용** 인증 방법 설명 된 대로 [여기](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29)합니다. 면이 설정을 사용 하는 것이 좋습니다는 합니다 **집합 VpnAuthProtocol** PowerShell cmdlet을 함께 합니다 **RootCertificateNameToAccept** 하도록 선택적 매개 변수는 RRAS의 IKEv2 연결 에서만 허용 됩니다 VPN 클라이언트 인증서를 명시적으로 정의 된 내부/개인 루트 인증 기관에 연결 합니다. 또는 합니다 **신뢰할 수 있는 루트 인증 기관** RRAS 서버의 저장소는 포함 하지 공용 인증 기관 설명 했 듯이 되도록 이메일과 [여기](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)합니다. 비슷한 메서드가 다른 VPN gateway에 대 한 것으로 간주 해야 할 수도 있습니다.

