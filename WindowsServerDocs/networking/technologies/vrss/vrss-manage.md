---
title: VRSS 관리
description: 이 항목에서는 Windows PowerShell 명령을 사용 하 여 vRSS 하 고 Hyper-v 호스트에서 가상 컴퓨터 (Vm)에서 관리 하 합니다.
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133839"
---
# VRSS 관리

이 항목에서는 Windows PowerShell 명령을 사용 하 여 vRSS Hyper\-v 호스트와 가상 컴퓨터 \(VMs\)에서 관리.

>[!NOTE]
>이 항목에 나오는 명령에 대 한 자세한 내용은 [Windows PowerShell 명령 RSS 및 vRSS를](vrss-wps.md)참조 하세요.

## Hyper-v 호스트에서 VMQ

Hyper-v 호스트에서 VMQ 프로세서를 제어 하는 키워드를 사용 해야 합니다.

**현재 설정을 보려면** 

```PowerShell
Get-NetAdapterVmq
```

**VMQ 설정을 구성 합니다.** 

```PowerShell
Set-NetAdapterVmq
```


## Hyper-v에서 vRSS 포트 전환

Hyper-v 호스트에서 vRSS Hyper\-v 가상 스위치 포트에서 사용 해야 합니다.

**현재 설정을 보려면**

```PowerShell
Get-VMNetworkAdapter <vm-name> | fl

Get-VMNetworkAdapter -ManagementOS | fl
```
    
다음 설정 모두 **True**여야 합니다. 

- VrssEnabledRequested: True
- VrssEnabled: True
    
>[!IMPORTANT]
>일부 리소스 제한 조건에서 Hyper\-v 가상 스위치 포트가이 기능을 사용 하도록 할 수 있습니다. 일시적인 상태 이며 기능 다음 번에 사용할 수 있게 됩니다.
>
>**VrssEnabled** **True**인 경우이 기능이이 Hyper\-v 가상 스위치 포트에 대 한-즉,이 VM 또는 vNIC 합니다.

**스위치 포트 vRSS 설정을 구성 합니다.**

```PowerShell
Set-VMNetworkAdapter <vm-name> -VrssEnabled $TRUE
    
Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
```

## Vm 및 호스트 Vnic vRSS

호스트 Vnic에서 RSS를 사용 하도록 설정 하는 방법 이기도 Vm 및 호스트 Vnic vRSS 설정을 구성 하려면 기본 RSS에 대 한 동일한 명령을 사용할 수 있습니다.  

**현재 설정을 보려면**

```PowerShell
Get-NetAdapterRSS
```

**VRSS 설정을 구성 합니다.**

```PowerShell
Set-NetAdapterRss
```

>[!NOTE]
> VM 내부 프로필 설정 영향을 주지 않습니다 작업을 예약 합니다. Hyper\-v는 모든 일정 결정 하 고 VM 내부 프로필을 무시 합니다.

## VRSS 사용 안 함

앞에서 언급 한 설정을 사용 하지 않으려면 vRSS 비활성화할 수 있습니다.

- VM 또는 물리적 NIC에 대 한 VMQ를 사용 하지 않도록 설정 합니다.

  >[!CAUTION]
  >비활성화할 수 있도록 VMQ에 실제 NIC 심각한 영향을 받습니다 들어오는 패킷을 처리 하는 Hyper\-v 호스트의 기능입니다.

- Hyper\-v 가상 스위치 포트 Hyper\-v 호스트에서 VM에 대 한 vRSS를 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled $FALSE
   ```

- VRSS Hyper\-v 호스트에서 Hyper\-v 가상 스위치 포트에서 호스트 vNIC 사용 하지 않도록 설정 합니다.

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $FALSE
   ```

- VM에서 RSS 비활성화 \(or host vNIC\) VM 내부 \ (또는 host\)

   ```PowerShell
   Disable-NetAdapterRSS *
   ```
