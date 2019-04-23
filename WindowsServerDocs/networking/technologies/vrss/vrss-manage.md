---
title: vRSS 관리
description: 이 항목에서는 Windows PowerShell 명령을 사용 하 여 Hyper-v 호스트 및 virtual machines (Vm)에서 vRSS를 관리.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0fe5bfc3-591f-4a19-b98a-0668d4c9f93a
ms.localizationpriority: medium
manager: dougkim
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8af800608bee7037b48141a7a2edb0c872a7aac0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856194"
---
# <a name="manage-vrss"></a>vRSS 관리

이 항목에서는 virtual machines에서 vRSS를 관리 하는 Windows PowerShell 명령을 사용 \(Vm\) 및 하이퍼\-호스트 합니다.

>[!NOTE]
>이 항목에서 설명 하는 명령에 대 한 자세한 내용은 참조 하세요. [RSS 및 vRSS Windows PowerShell 명령](vrss-wps.md)입니다.

## <a name="vmq-on-hyper-v-hosts"></a>Hyper-v 호스트에서 VMQ

Hyper-v 호스트에서 VMQ 프로세서를 제어 하는 키워드를 사용 해야 합니다.

**현재 설정을 보려면:** 

```PowerShell
Get-NetAdapterVmq
```

**VMQ 설정을 구성 합니다.** 

```PowerShell
Set-NetAdapterVmq
```


## <a name="vrss-on-hyper-v-switch-ports"></a>vRSS hyper-v 스위치 포트

Hyper-v 호스트에서 설정할 수도 있습니다는 하이퍼에서 vRSS\-V 가상 스위치 포트.

**현재 설정을 보려면:**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
다음과 같은 설정을 모두 있어야 합니다 **True**합니다. 

- VrssEnabledRequested: True
- VrssEnabled: True
    
>[!IMPORTANT]
>조건에 따라 리소스 제한, Hyper\-V 가상 스위치 포트가 기능을 사용 하도록 설정 하는 일을 할 수 있습니다. 임시 조건을 이며 이후 시간에 기능을 사용할 수 있게 됩니다.
>
>경우 **VrssEnabled** 됩니다 **True**,이 기능이이 하이퍼에 대 한 다음\-V 가상 스위치 포트-즉,이 VM에 vNIC입니다.

**스위치 포트 vRSS 설정을 구성 합니다.**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## <a name="vrss-in-vms-and-host-vnics"></a>Vm 및 호스트 Vnic에서 vRSS

호스트 Vnic에서 RSS를 사용 하도록 설정 하는 방법 이기도 Vm 및 호스트 Vnic에서 vRSS 설정을 구성 하려면 기본 RSS에 사용 되는 동일한 명령을 사용할 수 있습니다.  

**현재 설정을 보려면:**

```PowerShell
Get-NetAdapterRSS
```

**VRSS 설정을 구성 합니다.**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> VM 내의 프로필 설정은 영향을 주지 않습니다 작업을 예약 합니다. 하이퍼\-V를 사용 하면 모든 일정 결정 및 VM 내의 프로필을 무시 합니다.

## <a name="disable-vrss"></a>VRSS를 사용 하지 않도록 설정

앞에서 언급 한 설정을 사용 하지 않으려면 vRSS를 비활성화할 수 있습니다.

- 실제 NIC 또는 VM에 대 한 VMQ를 사용 하지 않도록 설정 합니다.

  >[!CAUTION]
  >VMQ를 사용 하지 않으면 물리적 NIC 심각한 영향을 미치게 Hyper 기능\-들어오는 패킷을 처리를 호스트 합니다.

- Hyper에서 VM에 대 한 vRSS를 사용 하지 않도록 설정\-Hyper V 가상 스위치 포트\-호스트 합니다.

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- Hyper에서 호스트 vNIC에 대 한 vRSS를 사용 하지 않도록 설정\-Hyper V 가상 스위치 포트\-호스트 합니다.

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- VM에서 RSS를 사용 하지 않도록 설정 \(또는 호스트 vNIC\) VM 내에서 \(또는 호스트\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
