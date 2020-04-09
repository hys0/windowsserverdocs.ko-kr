---
title: Windows 10에서 VPN 장치 터널 구성
description: Windows 10에서 VPN 장치 터널을 만드는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.date: 11/05/2018
ms.technology: networking-ras
ms.topic: article
ms.assetid: 158b7a62-2c52-448b-9467-c00d5018f65b
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.openlocfilehash: 855eb8d45297f15afceedf6cc11c2175c899ae45
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818796"
---
# <a name="configure-vpn-device-tunnels-in-windows-10"></a>Windows 10에서 VPN 장치 터널 구성

>적용 대상: Windows 10 버전 1709

Always On VPN은 장치 또는 컴퓨터에 대 한 전용 VPN 프로필을 만드는 기능을 제공 합니다. Always On VPN 연결에는 두 가지 유형의 터널이 포함 됩니다. 

- 사용자가 장치에 로그온 하기 전에 _장치 터널이_ 지정 된 VPN 서버에 연결 합니다. 사전 로그인 연결 시나리오 및 장치 관리 용도는 장치 터널을 사용 합니다.

- 사용자가 장치에 로그온 한 후에만 _사용자 터널이_ 연결 됩니다. 사용자 터널을 통해 사용자는 VPN 서버를 통해 조직 리소스에 액세스할 수 있습니다.

사용자가 장치 또는 컴퓨터에 로그온 한 후에 연결 하는 _사용자 터널_과 달리 _장치 터널_ 을 사용 하면 VPN에서 사용자가 로그온 하기 전에 연결을 설정할 수 있습니다. _장치 터널_ 및 _사용자 터널_ 은 모두 VPN 프로필과 독립적으로 작동 하 고 동시에 연결 될 수 있으며, 다른 인증 방법 및 기타 VPN 구성 설정을 적절 하 게 사용할 수 있습니다. 사용자 터널은 SSTP 및 i k e v 2를 지원 하 고, 장치 터널은 SSTP 대체를 지원 하지 않고 IKEv2만 지원 합니다.

도메인에 가입 된 도메인, 비도메인 조인 된 (작업 그룹) 또는 Azure AD 조인 장치에서 사용자 터널이 지원 되므로 엔터프라이즈 및 BYOD 시나리오를 모두 사용할 수 있습니다. 모든 Windows 버전에서 사용할 수 있으며, 타사에서 UWP VPN 플러그 인 지원을 통해 플랫폼 기능을 사용할 수 있습니다.

장치 터널은 Windows 10 Enterprise 또는 교육용 버전 1709 이상을 실행 하는 도메인에 가입 된 장치 에서만 구성할 수 있습니다. 장치 터널의 타사 제어는 지원 되지 않습니다.


## <a name="device-tunnel-requirements-and-features"></a>장치 터널 요구 사항 및 기능
VPN 연결에 대해 컴퓨터 인증서 인증을 사용 하도록 설정 하 고 들어오는 VPN 연결을 인증 하기 위한 루트 인증 기관을 정의 해야 합니다. 

```PowerShell
$VPNRootCertAuthority = "Common Name of trusted root certification authority"
$RootCACert = (Get-ChildItem -Path cert:LocalMachine\root | Where-Object {$_.Subject -Like "*$VPNRootCertAuthority*" })
Set-VpnAuthProtocol -UserAuthProtocolAccepted Certificate, EAP -RootCertificateNameToAccept $RootCACert -PassThru
```

![장치 터널 기능 및 요구 사항](../../media/device-tunnel-feature-and-requirements.png)

## <a name="vpn-device-tunnel-configuration"></a>VPN 장치 터널 구성

아래 샘플 프로필 XML은 장치 터널을 통해 클라이언트에서 시작한 가져오기만 필요한 시나리오에 적합 한 지침을 제공 합니다.  트래픽 필터를 활용 하 여 장치 터널을 관리 트래픽으로만 제한할 수 있습니다.  이 구성은 Windows 업데이트, 일반 그룹 정책 (GP) 및 Microsoft 끝점 Configuration Manager 업데이트 시나리오 뿐만 아니라 캐시 된 자격 증명이 없는 첫 번째 로그온을 위한 VPN 연결 또는 암호 다시 설정 시나리오에 적합 합니다. 

Windows 원격 관리 (WinRM), 원격 GPUpdate 및 원격 Configuration Manager 업데이트 시나리오와 같은 서버에서 시작 된 푸시 사례의 경우에는 장치 터널에서 인바운드 트래픽을 허용 해야 하므로 트래픽 필터를 사용할 수 없습니다.  장치 터널 프로필에서 트래픽 필터를 켜면 장치 터널에서 인바운드 트래픽을 거부 합니다.  이 제한은 이후 릴리스에서 제거 될 예정입니다.


### <a name="sample-vpn-profilexml"></a>샘플 VPN 프로 파일링 Exml

다음은 샘플 VPN 프로 파일링 Exml입니다.

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

각 특정 배포 시나리오의 요구 사항에 따라 장치 터널을 사용 하 여 구성할 수 있는 다른 VPN 기능을 [신뢰할 수 있는 네트워크 검색](https://social.technet.microsoft.com/wiki/contents/articles/38546.new-features-for-vpn-in-windows-10-and-windows-server-2016.aspx#Trusted_Network_Detection)이라고 합니다.

```
 <!-- inside/outside detection -->
  <TrustedNetworkDetection>corp.contoso.com</TrustedNetworkDetection>
```

## <a name="deployment-and-testing"></a>배포 및 테스트

Windows PowerShell 스크립트를 사용 하 고 WMI(Windows Management Instrumentation) (WMI) 브리지를 사용 하 여 장치 터널을 구성할 수 있습니다. Always On VPN 장치 터널은 **로컬 시스템** 계정의 컨텍스트에서 구성 해야 합니다. 이를 위해 [Sysinternals](https://docs.microsoft.com/sysinternals/) 유틸리티 모음에 포함 된 [PsTools](https://docs.microsoft.com/sysinternals/downloads/pstools) 중 하나인 [PsExec](https://docs.microsoft.com/sysinternals/downloads/psexec)를 사용 해야 합니다.

장치당 사용자별 `(.\User)` 프로필 `(.\Device)`를 배포 하는 방법에 대 한 지침은 [WMI 브리지 공급자와 함께 PowerShell 스크립팅 사용](https://docs.microsoft.com/windows/client-management/mdm/using-powershell-scripting-with-the-wmi-bridge-provider)을 참조 하세요.

다음 Windows PowerShell 명령을 실행 하 여 장치 프로필을 성공적으로 배포 했는지 확인 합니다.

  ```powershell
  Get-VpnConnection -AllUserConnection
  ```

출력에는 장치에 배포 된 장치\-wide VPN 프로필의 목록이 표시 됩니다.

### <a name="example-windows-powershell-script"></a>Windows PowerShell 스크립트 예제

다음 Windows PowerShell 스크립트를 사용 하 여 프로필을 만드는 데 필요한 스크립트를 직접 만들 수 있습니다.

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

- [Configuration Manager에서 VPN 프로필을 만드는 방법](https://docs.microsoft.com/configmgr/protect/deploy-use/create-vpn-profiles)
- [Windows 10 클라이언트 Always On VPN 연결 구성](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [VPN 프로필 옵션](https://docs.microsoft.com/windows/access-protection/vpn/vpn-profile-options)

### <a name="remote-access-server-gateway-resources"></a>원격 액세스 서버 게이트웨이 리소스

RAS (원격 액세스 서버) 게이트웨이 리소스는 다음과 같습니다.

- [컴퓨터 인증 인증서를 사용 하 여 RRAS 구성](https://technet.microsoft.com/library/dd458982.aspx)
- [IKEv2 VPN 연결 문제 해결](https://technet.microsoft.com/library/dd941612.aspx)
- [IKEv2 기반 원격 액세스 구성](https://technet.microsoft.com/library/ff687731.aspx)

>[!IMPORTANT]
>Microsoft RAS 게이트웨이와 함께 장치 터널을 사용 하는 경우 [여기](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee922682%28v=ws.10%29)에 설명 된 대로 **ikev2 인증에 대 한 컴퓨터 인증서 인증 허용** 방법을 사용 하도록 설정 하 여 ikev2 컴퓨터 인증서 인증을 지원 하도록 RRAS 서버를 구성 해야 합니다. 이 설정을 사용 하도록 설정 하 고 나면 **VpnAuthProtocol** PowerShell Cmdlet을 **RootCertificateNameToAccept** 선택적 매개 변수와 함께 사용 하 여 명시적으로 정의 된 내부/개인 루트 인증 기관에 연결 된 VPN 클라이언트 인증서에 대해서만 RRAS IKEv2 연결이 허용 되도록 하는 것이 좋습니다. 또는 [여기](https://blogs.technet.microsoft.com/rrasblog/2009/06/10/what-type-of-certificate-to-install-on-the-vpn-server/)에 설명 된 대로 공용 인증 기관을 포함 하지 않도록 RRAS 서버의 **신뢰할 수 있는 루트 인증 기관** 저장소를 수정 해야 합니다. 다른 VPN 게이트웨이의 경우에도 유사한 방법을 고려해 야 합니다.

