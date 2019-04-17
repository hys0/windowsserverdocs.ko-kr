---
title: VM 만들고 네트워크 또는 VLAN 가상 테에 연결
description: 이 항목은 관리 테 작업 및 Windows Server 2016에 가상 네트워크 방법에 대해 소프트웨어 네트워킹 정의 가이드 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c62f533-1815-4f08-96b1-dc271f5a2b36
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 001eb3efa073e4ffbdfad41f88949303159a7274
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="create-a-vm-and-connect-to-a-tenant-virtual-network-or-vlan"></a>VM 만들고 네트워크 또는 VLAN 가상 테에 연결

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

이 항목을 사용 하 여 가상 거주 만들 \(VM\) 기계 하 고 VM 가상 로컬 네트워크 \(VLAN\) 또는 네트워크 가상화 Hyper-v를 사용 하 여 만든 같은 가상 네트워크에 연결 합니다. 

이 항목 다음 섹션에 포함 되어 있습니다.

- [네트워크 컨트롤러 Windows PowerShell cmdlet 사용 하 여 가상 네트워크에 연결 하 고 VM 만들기](#bkmk_vn)
- [VM 만들고 VLAN NetworkControllerRESTWrappers 사용 하 여 연결](#bkmk_vlan)

## <a name="requirements"></a>요구 사항
다음 섹션에는 절차를 수행 하기 전에 다음과 같은 요구 사항을 note 합니다.

1. 만들어야 VM 네트워크 어댑터 정적 미디어 액세스 제어 \(MAC\) 주소를 VM 수명 동안 VM의 MAC 주소를 변경 하지 않습니다. 
>[!NOTE]
>VM 수명 동안 VM MAC 주소를 변경 하는 경우 네트워크 컨트롤러 네트워크 어댑터에 대 한 필요한 정책을 구성할 수 없습니다. 네트워크 어댑터에 대 한 정책을 구성 되지 않은 경우 네트워크 어댑터에서 네트워크 트래픽을 처리할 수 없거나 하 고 네트워크의 모든 통신 실패 합니다. 

2. VM 시작할 때 네트워크 액세스를 필요한 경우에 네트워크 어댑터 포트 VM에서 인터페이스 ID를 설정 하는 최종 구성 단계-지나기 VM 시작 하지 않는 것이 중요 합니다. 이 단계를 완료 하기 전에 VM를 시작 하면 VM 통신할 수 없는 네트워크에서 네트워크 인터페이스 네트워크 컨트롤러에서 만든 컨트롤러에 모두 적용 가능한 정책을-가상 네트워크 정책을 적용 될 때까지 액세스 제어 \(ACLs\), 및 서비스 \(QoS\) 품질 목록.

또한 가상 기기 배포를 위해이 항목에 설명 된 프로세스를 사용할 수 있습니다. 몇 가지 추가 단계를 기기 처리 또는 가상 네트워크의 다른 Vm에서 진행 되는 데이터 패킷이 검사를 구성할 수 있습니다.

>[!IMPORTANT]
>다음 섹션에 대 한 많은 매개 예 값 포함 된 예제 Windows PowerShell 명령 포함 됩니다. 다음이 명령을 실행 하기 전에 배포에 대 한 적절 한 값으로 들어 값이 명령에서를 교체 해야 합니다.  

## <a name="bkmk_vn"></a>네트워크 컨트롤러 Windows PowerShell cmdlet 사용 하 여 가상 네트워크에 연결 하 고 VM 만들기

이 섹션 다음과 같은 항목이 포함 되어 있습니다.

1.  [VM 정적 MAC 주소를 가진 VM 네트워크 어댑터를 사용 하 여 만들기](#bkmk_create)
2.  [네트워크 어댑터에 연결 하려면 서브넷 포함 된 가상 네트워크 다운로드](#bkmk_getvn)
3.  [네트워크 컨트롤러에서 네트워크 인터페이스 개체 만들기](#bkmk_object)
4.  [네트워크 컨트롤러에서 네트워크 인터페이스 InstanceId 받기](#bkmk_getinstance)
5.  [네트워크 어댑터 포트 인터페이스 ID Hyper-v VM에서 설정](#bkmk_setinstance)
6.  [VM 시작](#bkmk_start)

### <a name="bkmk_create"></a>VM 정적 MAC 주소를 가진 VM 네트워크 어댑터를 사용 하 여 만들기

VM 고정 MAC 주소를가 하는 네트워크 어댑터를 만들려면 명령은 사용 합니다.

    
    New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 
    
    Set-VM -Name "MyVM" -ProcessorCount 4
    
    Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 
    

### <a name="bkmk_getvn"></a>네트워크 어댑터에 연결 하려면 서브넷 포함 된 가상 네트워크 다운로드
이 들어 명령을 사용 하려면 먼저 가상 네트워크를 이미 만든 있는지 확인 합니다. 자세한 내용은 참조 [만들기, 삭제 또는 업데이트 테 가상 네트워크](https://technet.microsoft.com/windows-server-docs/networking/sdn/manage/create%2c-delete%2c-or-update-tenant-virtual-networks)합니다.

가상 네트워크 명령은 사용 합니다.

    
    $vnet = get-networkcontrollervirtualnetwork -connectionuri $uri -ResourceId “Contoso_WebTier”
    

>[!NOTE]
>사용자 지정 Acl 네트워크 인터페이스이 필요 하면 만듭니다 ACL 이제 항목의 지침을 사용 하 여 [사용 액세스 제어 (Acl 목록) Datacenter 네트워크 교통 플로 관리를](../../sdn/manage/Use-Access-Control-Lists--ACLs--to-Manage-Datacenter-Network-Traffic-Flow.md)

### <a name="bkmk_object"></a>네트워크 컨트롤러에서 네트워크 인터페이스 개체 만들기

네트워크 컨트롤러에서 네트워크 인터페이스 개체 만들려면 다음 예 명령을 사용 합니다.

>[!NOTE]
>이전 단계를 수행한 후를 사용자 지정 ACL를 만든 경우 이제 사용할 수 있습니다.

    
    $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
    $vmnicproperties.PrivateMacAddress = "001122334455" 
    $vmnicproperties.PrivateMacAllocationMethod = "Static" 
    $vmnicproperties.IsPrimary = $true 

    $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
    $vmnicproperties.DnsSettings.DnsServers = @("24.30.1.11", "24.30.1.12")
    
    $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $ipconfiguration.resourceid = "MyVM_IP1"
    $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
    $ipconfiguration.properties.PrivateIPAddress = “24.30.1.101”
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"
    
    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $vnet.Properties.Subnets[0].ResourceRef
    
    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    New-NetworkControllerNetworkInterface –ResourceID “MyVM_Ethernet1” –Properties $vmnicproperties –ConnectionUri $uri
    

### <a name="bkmk_getinstance"></a>네트워크 컨트롤러에서 네트워크 인터페이스 InstanceId 받기
InstanceId 네트워크 인터페이스에서 네트워크 컨트롤러를 사용 명령은 합니다.

    
    $nic = Get-NetworkControllerNetworkInterface -ConnectionUri $uri -ResourceId "MyVM-Ethernet1"
    

### <a name="bkmk_setinstance"></a>네트워크 어댑터 포트 인터페이스 ID Hyper-v VM에서 설정
인터페이스 ID Hyper-v VM에 네트워크 어댑터 포트를 설정 하려면 다음 예제 명령을 사용.

>[!NOTE]
>실행 해야이 명령을 Hyper-v 호스트 VM 설치 되어 있습니다.

    
    #Do not change the hardcoded IDs in this section, because they are fixed values and must not change.
    
    $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"
    
    $vmNics = Get-VMNetworkAdapter -VMName “MyVM”
    
    $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNics
    
    if ($CurrentFeature -eq $null)
    {
    $Feature = Get-VMSystemSwitchExtensionPortFeature -FeatureId $FeatureId
    
    $Feature.SettingData.ProfileId = "{$($nic.InstanceId)}"
    $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
    $Feature.SettingData.CdnLabelString = "TestCdn"
    $Feature.SettingData.CdnLabelId = 1111
    $Feature.SettingData.ProfileName = "Testprofile"
    $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
    $Feature.SettingData.VendorName = "NetworkController"
    $Feature.SettingData.ProfileData = 1
    
    Add-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNics
    }
    else
    {
    $CurrentFeature.SettingData.ProfileId = "{$($nic.InstanceId)}"
    $CurrentFeature.SettingData.ProfileData = 1
    
    Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
    }
    

### <a name="bkmk_start"></a>VM 시작
VM를 시작 하려면 다음 예 명령을 사용 합니다.

    
    Get-VM -Name “MyVM” | Start-VM 
    
이제 VM 만든, VM 테 가상 네트워크에 연결 하 고 했습니다 테 작업을 처리할 수 있도록 VM 시작 합니다.

## <a name="bkmk_vlan"></a>VM 만들고 VLAN NetworkControllerRESTWrappers 사용 하 여 연결

이 섹션 다음과 같은 항목이 포함 되어 있습니다.

1. [고정 MAC 주소를 지정 하 고 VM 만들기](#bkmk_mac)
2. [VLAN ID VM 네트워크 어댑터에 대 한 설정](#bkmk_vid)
3. [논리 네트워크 서브넷 및 네트워크 인터페이스 만들기](#bkmk_subnet)
4. [Hyper-v 포트에서 InstanceId 설정](#bkmk_instance)
5. [VM 시작](#bkmk_startvlan)


###<a name="bkmk_mac"></a>고정 MAC 주소를 지정 하 고 VM 만들기
VM를 만들고 VM에 정적 미디어 액세스 제어 \(MAC\) 주소를 지정 하려면 다음 예제 명령을 사용할 수 있습니다.

    New-VM -Generation 2 -Name "MyVM" -Path "C:\VMs\MyVM" -MemoryStartupBytes 4GB -VHDPath "c:\VMs\MyVM\Virtual Hard Disks\WindowsServer2016.vhdx" -SwitchName "SDNvSwitch" 

    Set-VM -Name "MyVM" -ProcessorCount 4

    Set-VMNetworkAdapter -VMName "MyVM" -StaticMacAddress "00-11-22-33-44-55" 

###<a name="bkmk_vid"></a>VLAN ID VM 네트워크 어댑터에 대 한 설정
네트워크 어댑터에 VLAN ID를 설정 하려면 다음 예 명령을 사용할 수 있습니다.


    Set-VMNetworkAdapterIsolation –VMName “MyVM” -AllowUntaggedTraffic $true -IsolationMode VLAN -DefaultIsolationId 123


###<a name="bkmk_subnet"></a>논리 네트워크 서브넷 및 네트워크 인터페이스 만들기

논리 네트워크 서브넷 얻고 논리 네트워크 서브넷을 사용 하 여 네트워크 인터페이스 만들기를에 다음 예제 명령을 사용할 수 있습니다.


    $logicalnet = get-networkcontrollerLogicalNetwork -connectionuri $uri -ResourceId "00000000-2222-1111-9999-000000000002"

    $vmnicproperties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceProperties
    $vmnicproperties.PrivateMacAddress = "00-1D-C8-B7-01-02"
    $vmnicproperties.PrivateMacAllocationMethod = "Static"
    $vmnicproperties.IsPrimary = $true 
    
    $vmnicproperties.DnsSettings = new-object Microsoft.Windows.NetworkController.NetworkInterfaceDnsSettings
    $vmnicproperties.DnsSettings.DnsServers = $logicalnet.Properties.Subnets[0].DNSServers

    $ipconfiguration = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfiguration
    $ipconfiguration.resourceid = "MyVM_Ip1"
    $ipconfiguration.properties = new-object Microsoft.Windows.NetworkController.NetworkInterfaceIpConfigurationProperties
    $ipconfiguration.properties.PrivateIPAddress = “10.127.132.177”
    $ipconfiguration.properties.PrivateIPAllocationMethod = "Static"

    $ipconfiguration.properties.Subnet = new-object Microsoft.Windows.NetworkController.Subnet
    $ipconfiguration.properties.subnet.ResourceRef = $logicalnet.Properties.Subnets[0].ResourceRef

    $vmnicproperties.IpConfigurations = @($ipconfiguration)
    $vnic = New-NetworkControllerNetworkInterface –ResourceID “MyVM_Ethernet1” –Properties $vmnicproperties –ConnectionUri $uri

    $vnic.InstanceId
    

###<a name="bkmk_instance"></a>Hyper-v 포트에서 InstanceId 설정
InstanceId Hyper-v 포트에서를 설정 하려면 사용할 수 있습니다 다음 예제 명령을 Hyper-v 호스트에서 VM입니다.

  
    #The hardcoded Ids in this section are fixed values and must not change.
    $FeatureId = "9940cd46-8b06-43bb-b9d5-93d50381fd56"

    $vmNics = Get-VMNetworkAdapter -VMName “MyVM”

    $CurrentFeature = Get-VMSwitchExtensionPortFeature -FeatureId $FeatureId -VMNetworkAdapter $vmNic
        
    if ($CurrentFeature -eq $null)
    {
        $Feature = Get-VMSystemSwitchExtensionFeature -FeatureId $FeatureId
        
        $Feature.SettingData.ProfileId = "{$InstanceId}"
        $Feature.SettingData.NetCfgInstanceId = "{56785678-a0e5-4a26-bc9b-c0cba27311a3}"
        $Feature.SettingData.CdnLabelString = "TestCdn"
        $Feature.SettingData.CdnLabelId = 1111
        $Feature.SettingData.ProfileName = "Testprofile"
        $Feature.SettingData.VendorId = "{1FA41B39-B444-4E43-B35A-E1F7985FD548}"
        $Feature.SettingData.VendorName = "NetworkController"
        $Feature.SettingData.ProfileData = 1
                
        Add-VMSwitchExtensionFeature -VMSwitchExtensionFeature  $Feature -VMNetworkAdapter $vmNic
    }        
    else
    {
        $CurrentFeature.SettingData.ProfileId = "{$InstanceId}"
        $CurrentFeature.SettingData.ProfileData = 1

        Set-VMSwitchExtensionPortFeature -VMSwitchExtensionFeature $CurrentFeature  -VMNetworkAdapter $vmNic
    }


###<a name="bkmk_startvlan"></a>VM 시작
VM를 시작 하려면 다음 예 명령을 사용할 수 있습니다.


    Get-VM -Name “MyVM” | Start-VM 

이제 VM 만든, VM VLAN에 연결 하 고 했습니다 테 작업을 처리할 수 있도록 VM 시작 합니다.

  

