---
title: Nano Server의 MPIO
description: Nano에서 MPIO 구성
ms.prod: windows-server
manager: DonGill
ms.date: 09/06/2017
ms.technology: server-nano
ms.topic: article
ms.assetid: fbef4d91-e18c-4f1b-952f-a9a7ad46cd74
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: fb38976ca6b2297562e74d9ea29510308ad23ff6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826836"
---
# <a name="mpio-on-nano-server"></a>Nano Server의 MPIO

>적용 대상: Windows Server 2016

> [!IMPORTANT]
> Windows Server, 버전 1709부터 [컨테이너 기본 OS 이미지](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)로만 Nano 서버를 사용할 수 있습니다. [Nano 서버 변경 사항](nano-in-semi-annual-channel.md)을 확인하여 그 의미를 알아보세요. 

이 항목에서는 Windows Server 2016의 Nano 서버 설치에서 MPIO의 사용에 대해 소개합니다. Windows Server에서 MPIO에 대한 일반 정보는 [다중 경로 I/O 개요](https://technet.microsoft.com/library/cc725907.aspx)를 참조하세요.  

## <a name="using-mpio-on-nano-server"></a>Nano 서버에서 MPIO 사용  
Nano 서버에서 MPIO를 사용할 수 있으나 다음과 같은 차이점이 있습니다.  
  
-   MSDSM만 지원됩니다.  
  
-   부하 분산 정책이 동적으로 선택되며 수정할 수 없습니다. 정책은 다음과 같은 특성을 지닙니다.  
  
    -   기본값 -- 라운드 로빈(활성/활성)  
  
    -   SAS HDD -- LeastBlocks  
  
    -   ALUA -- 하위 집합 포함 라운드 로빈  
  
-   ALUA 배열에 대한 경로 상태(활성/수동)가 대상 배열에서 선택됩니다.  
  
-   스토리지 디바이스는 버스 유형(예: FC, iSCSI, SAS)별로 요청됩니다. Nano 서버에 MPIO가 설치되면 MPIO가 특정 디스크를 요청 및 관리하도록 구성될 때까지 디스크가 중복(경로당 하나 사용 가능)된 것으로 계속 노출됩니다. 이 항목의 예제 스크립트는 MPIO에 대한 디스크를 요청 및 요청 취소합니다.

- iSCSI 부팅은 지원되지 않습니다.
  
이 Windows PowerShell cmdlet으로 MPIO를 사용하도록 설정합니다.  
  
`Enable-WindowsOptionalFeature -Online -FeatureName MultiPathIO`  
  
이 예제 스크립트를 통해 호출자는 특정 레지스트리 키를 변경하여 MPIO에 대한 디스크를 요청 및 요청 취소할 수 있습니다. 이러한 키에 디바이스를 추가하여 다른 스토리지 디바이스를 요청할 수 있지만 키를 직접 조작하지 않는 것이 좋습니다.  
  
```  
#  
#  Copyright (c) 2015 Microsoft Corporation.  All rights reserved.  
#    
#  THIS CODE AND INFORMATION IS PROVIDED AS IS WITHOUT WARRANTY   
#  OF ANY KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED   
#  TO THE IMPLIED WARRANTIES OF MERCHANTABILITY AND/OR FITNESS FOR A    
#  PARTICULAR PURPOSE  
#  
  
<#  
.Synopsis  
    This powershell script allows you to enable Multipath-IO support using Microsoft's  
    in-box DSM (MSDSM) for storage devices attached by certain bus types.  
  
    After running this script you will have to either:  
    1. Disable and then re-enable the relevant Host Bus Adapters (HBAs); or  
    2. Reboot the system.  
  
.Description  
  
.Parameter BusType  
    Specifies the bus type for which the claim/unclaim should be done.  
  
    If omitted, this parameter defaults to All.  
  
    All - Will claim/unclaim storage devices attached through Fibre Channel, iSCSI, or SAS.  
  
    FC - Will claim/unclaim storage devices attached through Fibre Channel.  
  
    iSCSI - Will claim/unclaim storage devices attached through iSCSI.  
  
    SAS - Will claim/unclaim storage devices attached through SAS.  
  
.Parameter Server  
    Allows you to specify a remote system, either via computer name or IP address.  
  
    If omitted, this parameter defaults to the local system.  
  
.Parameter Unclaim  
    If specified, the script will unclaim storage devices of the bus type specified by the  
    BusType parameter.  
  
    If omitted, the script will default to claiming storage devices instead.  
  
.Example  
MultipathIoClaim.ps1  
  
Claims all storage devices attached through Fibre Channel, iSCSI, or SAS.    
  
.Example  
MultipathIoClaim.ps1 FC  
  
Claims all storage devices attached through Fibre Channel.  
  
.Example  
MultipathIoClaim.ps1 SAS -Unclaim  
  
Unclaims all storage devices attached through SAS.  
  
.Example  
MultipathIoClaim.ps1 iSCSI 12.34.56.78  
  
Claims all storage devices attached through iSCSI on the remote system with IP address 12.34.56.78.    
  
#>  
[CmdletBinding()]  
param  
(    
    [ValidateSet('all','fc','iscsi','sas')]  
    [string]$BusType='all',  
  
    [string]$Server=127.0.0.1,  
  
    [switch]$Unclaim   
)  
  
#  
# Constants  
#  
$type = [Microsoft.Win32.RegistryHive]::LocalMachine  
[string]$mpioKeyName = SYSTEM\CurrentControlSet\Control\MPDEV  
[string]$mpioValueName = MpioSupportedDeviceList  
[string]$msdsmKeyName = SYSTEM\CurrentControlSet\Services\msdsm\Parameters  
[string]$msdsmValueName = DsmSupportedDeviceList  
  
[string]$fcHwid = MSFT2015FCBusType_0x6     
[string]$sasHwid = MSFT2011SASBusType_0xA    
[string]$iscsiHwid = MSFT2005iSCSIBusType_0x9  
  
#  
# Functions  
#  
  
function AddHardwareId  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid,  
  
        [string]$Srv=127.0.0.1,  
  
        [string]$KeyName=SYSTEM\CurrentControlSet\Control\MultipathIoClaimTest,  
  
        [string]$ValueName=DeviceList  
    )  
  
    $regKey = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey($type, $Srv)  
    $key = $regKey.OpenSubKey($KeyName, 'true')  
    $val = $key.GetValue($ValueName)  
    $val += $Hwid  
    $key.SetValue($ValueName, [string[]]$val, 'MultiString')  
}  
  
function RemoveHardwareId  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid,  
  
        [string]$Srv=127.0.0.1,  
  
        [string]$KeyName=SYSTEM\CurrentControlSet\Control\MultipathIoClaimTest,  
  
        [string]$ValueName=DeviceList  
    )  
  
    [string[]]$newValues = @()  
    $regKey = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey($type, $Srv)  
    $key = $regKey.OpenSubKey($KeyName, 'true')  
    $values = $key.GetValue($ValueName)  
    foreach($val in $values)  
    {  
        # Only copy values that don't match the given hardware ID.  
        if ($val -ne $Hwid)  
        {  
            $newValues += $val  
            Write-Debug $($val) will remain in the key.  
        }  
        else  
        {  
            Write-Debug $($val) will be removed from the key.  
        }  
    }  
    $key.SetValue($ValueName, [string[]]$newValues, 'MultiString')  
}  
  
function HardwareIdClaimed  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid,  
  
        [string]$Srv=127.0.0.1,  
  
        [string]$KeyName=SYSTEM\CurrentControlSet\Control\MultipathIoClaimTest,  
  
        [string]$ValueName=DeviceList  
    )  
  
    $regKey = [Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey($type, $Srv)  
    $key = $regKey.OpenSubKey($KeyName)  
    $values = $key.GetValue($ValueName)  
    foreach($val in $values)  
    {  
        if ($val -eq $Hwid)  
        {  
            return 'true'  
        }  
    }  
  
    return 'false'  
}  
  
function GetBusTypeName  
{  
    param  
    (  
        [Parameter(Mandatory=$True)]  
        [string]$Hwid  
    )  
  
    if ($Hwid -eq $fcHwid)  
    {  
        return Fibre Channel  
    }  
    elseif ($Hwid -eq $sasHwid)  
    {  
        return SAS  
    }  
    elseif ($Hwid -eq $iscsiHwid)  
    {  
        return iSCSI  
    }  
  
    return Unknown  
}  
  
#  
# Execution starts here.  
#  
  
#  
# Create the list of hardware IDs to claim or unclaim.  
#  
[string[]]$hwids = @()  
  
if ($BusType -eq 'fc')  
{  
    $hwids += $fcHwid  
}  
elseif ($BusType -eq 'iscsi')  
{  
    $hwids += $iscsiHwid  
}  
elseif ($BusType -eq 'sas')  
{  
    $hwids += $sasHwid  
}  
elseif ($BusType -eq 'all')  
{  
    $hwids += $fcHwid  
    $hwids += $sasHwid  
    $hwids += $iscsiHwid  
}  
else  
{  
    Write-Host Please provide a bus type (FC, iSCSI, SAS, or All).  
}  
  
$changed = 'false'  
  
#  
# Attempt to claim or unclaim each of the hardware IDs.  
#  
foreach($hwid in $hwids)  
{      
    $busTypeName = GetBusTypeName $hwid  
  
    #  
    # The device is only considered claimed if it's in both the MPIO and MSDSM lists.  
    #  
    $mpioClaimed = HardwareIdClaimed $hwid $Server $mpioKeyName $mpioValueName  
    $msdsmClaimed = HardwareIdClaimed $hwid $Server $msdsmKeyName $msdsmValueName  
    if ($mpioClaimed -eq 'true' -and $msdsmClaimed -eq 'true')  
    {  
        $claimed = 'true'  
    }  
    else  
    {  
        $claimed = 'false'  
    }  
  
    if ($mpioClaimed -eq 'true')  
    {  
        Write-Debug $($hwid) is in the MPIO list.  
    }  
    else  
    {  
        Write-Debug $($hwid) is NOT in the MPIO list.  
    }  
  
    if ($msdsmClaimed -eq 'true')  
    {  
        Write-Debug $($hwid) is in the MSDSM list.  
    }  
    else  
    {  
        Write-Debug $($hwid) is NOT in the MSDSM list.  
    }  
  
    if ($Unclaim)  
    {  
        #  
        # Unclaim this hardware ID.  
        #   
        if ($claimed -eq 'true')  
        {              
            RemoveHardwareId $hwid $Server $mpioKeyName $mpioValueName  
            RemoveHardwareId $hwid $Server $msdsmKeyName $msdsmValueName  
            $changed = 'true'  
            Write-Host $($busTypeName) devices will not be claimed.  
        }  
        else  
        {  
            Write-Host $($busTypeName) devices are not currently claimed.  
        }  
  
    }  
    else  
    {  
        #  
        # Claim this hardware ID.  
        #       
        if ($claimed -eq 'true')  
        {              
            Write-Host $($busTypeName) devices are already claimed.  
        }  
        else  
        {  
            AddHardwareId $hwid $Server $mpioKeyName $mpioValueName  
            AddHardwareId $hwid $Server $msdsmKeyName $msdsmValueName  
            $changed = 'true'  
            Write-Host $($busTypeName) devices will be claimed.  
        }  
    }  
}  
  
#  
# Finally, if we changed any of the registry keys remind the user to restart.  
#  
if ($changed -eq 'true')  
{  
    Write-Host The system must be restarted for the changes to take effect.  
}  
```  
  


