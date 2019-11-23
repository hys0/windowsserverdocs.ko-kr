---
title: vRSS 관리
description: 이 항목에서는 Windows PowerShell 명령을 사용 하 여 Vm (가상 머신) 및 Hyper-v 호스트에서 vRSS를 관리 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9d528f7e658d61f613eedc635fb81d8f18fd59aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405167"
---
# <a name="manage-vrss"></a>vRSS 관리

이 항목에서는 Windows PowerShell 명령을 사용 하 여 가상 컴퓨터 \(Vm\) 및 하이퍼\-V 호스트에서 vRSS를 관리 합니다.

>[!NOTE]
>이 항목에서 설명 하는 명령에 대 한 자세한 내용은 [RSS 및 vRSS에 대 한 Windows PowerShell 명령](vrss-wps.md)을 참조 하세요.

## <a name="vmq-on-hyper-v-hosts"></a>Hyper-v 호스트의 VMQ

Hyper-v 호스트에서는 VMQ 프로세서를 제어 하는 키워드를 사용 해야 합니다.

**현재 설정 보기:** 

```PowerShell
Get-NetAdapterVmq
```

**VMQ 설정 구성:** 

```PowerShell
Set-NetAdapterVmq
```


## <a name="vrss-on-hyper-v-switch-ports"></a>Hyper-v 스위치 포트의 vRSS

Hyper-v 호스트의 경우 하이퍼\-V 가상 스위치 포트에서 vRSS를 사용 하도록 설정 해야 합니다.

**현재 설정 보기:**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
다음 설정 모두 **True**여야 합니다. 

- VrssEnabledRequested: True
- VrssEnabled: True
    
>[!IMPORTANT]
>일부 리소스 제한 조건에서 하이퍼\-V 가상 스위치 포트는이 기능을 사용 하도록 설정 하지 못할 수 있습니다. 이는 일시적인 상태 이며 나중에 기능을 사용할 수 있게 될 것입니다.
>
>**VrssEnabled** 가 **True**이면이\-hyper-v 가상 스위치 포트 (즉,이 VM 또는 vNIC)에 대해이 기능이 활성화 됩니다.

**스위치 포트 vRSS 설정 구성:**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## <a name="vrss-in-vms-and-host-vnics"></a>Vm의 vRSS 및 호스트 vNICs

기본 RSS에 사용 되는 것과 동일한 명령을 사용 하 여 Vm 및 호스트 vNICs에서 vRSS 설정을 구성할 수 있습니다 .이를 통해 호스트 vNICs에서 RSS를 사용 하도록 설정할 수도 있습니다.  

**현재 설정 보기:**

```PowerShell
Get-NetAdapterRSS
```

**VRSS 설정 구성:**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> VM 내에서 프로필을 설정 해도 작업 예약에는 영향을 주지 않습니다. 하이퍼\-V는 모든 일정을 결정 하 고 VM 내에서 프로필을 무시 합니다.

## <a name="disable-vrss"></a>VRSS 사용 안 함

VRSS를 사용 하지 않도록 설정 하 여 앞서 언급 한 설정 중 하나를 사용 하지 않도록 설정할 수 있습니다.

- 실제 NIC 또는 VM에 대해 VMQ를 사용 하지 않도록 설정 합니다.

  >[!CAUTION]
  >실제 NIC에서 VMQ를 사용 하지 않도록 설정 하면 들어오는 패킷을 처리 하는 하이퍼\-V 호스트의 기능에 심각한 영향을 줍니다.

- 하이퍼\-V 호스트의\-Hyper-v 가상 스위치 포트에서 VM에 대해 vRSS를 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- 하이퍼\-V 호스트의\-Hyper-v 가상 스위치 포트에서 호스트 vNIC vRSS를 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- Vm \(에서 RSS를 사용 하지 않도록 설정 하거나 호스트에서 vNIC \(\)를 호스트\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
