---
title: Hyper-V 가상 스위치 포트에서 VLAN 설정 구성 및 확인
description: Windows Server 2016에서 Hyper-v 가상 스위치 포트에 대해 가상 로컬 영역 네트워크 (VLAN) 설정 보기 및 구성에 대 한 모범 사례를 알아보려면이 항목에서는 사용할 수 있습니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 69e0e28a-98ae-4ade-bd27-ce2ad7eb310f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1e4843b0ffee86d728736ae212b953bb7c8552c0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820554"
---
# <a name="configure-and-view-vlan-settings-on-hyper-v-virtual-switch-ports"></a>Hyper-V 가상 스위치 포트에서 VLAN 설정 구성 및 확인

>적용 대상: Windows Server (반기 채널), Windows Server 2016

구성 및 Hyper-v 가상 스위치 포트에 대해 가상 로컬 영역 네트워크 (VLAN) 설정 보기에 대 한 모범 사례를 알아보려면이 항목에서는 사용할 수 있습니다.

두 Windows Hyper-v 가상 스위치 포트에 VLAN 설정을 구성 하려는 경우 사용할 수 있습니다&reg; Server 2016 Hyper-v Manager 또는 System Center Virtual Machine Manager (VMM).

VMM을 사용 하는 경우 VMM 스위치 포트를 구성 하려면 다음 Windows PowerShell 명령을 사용 합니다.

```
Set-VMNetworkAdapterIsolation <VM-name|-managementOS> -IsolationMode VLAN -DefaultIsolationID <vlan-value> -AllowUntaggedTraffic $True
```
VMM을 사용 하지 않는 하 고 Windows Server의 스위치 포트를 구성 하는 경우 Hyper-v Manager 콘솔 또는 Windows PowerShell 명령을 사용할 수 있습니다.
```
Set-VMNetworkAdapterVlan <VM-name|-managementOS> -Access -VlanID <vlan-value>
```

Hyper-v 가상 스위치 포트에서 VLAN 설정을 구성 하는 데 이러한 두 메서드를 인해 되기 스위치 포트 설정을 확인 하려고 할 때 표시를 하는 VLAN 설정이 구성 되지-구성 된 경우에 있습니다.

## <a name="use-the-same-method-to-configure-and-view-switch-port-vlan-settings"></a>동일한 메서드를 사용 하 여 구성 및 스위치 포트가 VLAN 설정 보기

이러한 문제가 발생 하지 않도록 하기 위해 스위치 포트가 VLAN 설정을 구성 하는 스위치 포트 VLAN 설정을 보려면 동일한 메서드를 사용 해야 합니다.

구성 하 고 VLAN 스위치 포트 설정을 보려면 다음을 수행 해야 합니다.

- 사용 하는 VMM 또는 네트워크 컨트롤러를 설정 하 고 네트워크를 관리 하 고 소프트웨어 정의 네트워킹 (SDN)을 배포한 경우을 사용 해야 합니다는 **VMNetworkAdapterIsolation** cmdlet. 
- Windows Server 2016 Hyper-v 관리자 또는 Windows PowerShell cmdlet을 사용 하는 소프트웨어 정의 네트워킹 (SDN) 배포 하지 않은 경우 사용 해야 합니다 **VMNetworkAdapterVlan** cmdlet.

### <a name="possible-issues"></a>가능한 문제

이러한 지침을 따르지 않는 경우에 다음과 같은 문제가 발생할 수 있습니다.

- SDN 배포 하 고 VMM에서 네트워크 컨트롤러를 사용 하는 경우 또는 **VMNetworkAdapterIsolation** Hyper-v 가상 스위치 포트에 대해 VLAN 설정을 구성 하는 cmdlet: Hyper-v 관리자를 사용 하는 경우 또는 **VMNetworkAdapterVlan 가져오기** 구성 설정을 보려면 명령 출력에 VLAN 설정을 표시 되지 것입니다. 대신 사용 해야 합니다 **Get VMNetworkIsolation** VLAN 설정을 보려면 cmdlet.
- SDN을 배포 하지 않은 하 고 대신 Hyper-v 관리자를 사용 하는 경우 또는 **VMNetworkAdapterVlan** Hyper-v 가상 스위치 포트에 대해 VLAN 설정을 구성 하는 cmdlet: 사용 하는 경우는 **Get VMNetworkIsolation** 구성 설정을 보려면 cmdlet은 명령 출력에 VLAN 설정을 표시 되지 것입니다. 대신 사용 해야 합니다 **VMNetworkAdapterVlan 가져오기** VLAN 설정을 보려면 cmdlet.

이러한 구성 방법 모두를 사용 하 여 동일한 스위치 포트가 VLAN 설정을 구성 하 려 하지 않을 중요 이기도 합니다. 이 작업을 수행 하는 경우 스위치 포트를 잘못 구성 및 네트워크 통신에서 오류가 표시 될 수 있습니다.

### <a name="resources"></a>리소스

이 항목에 나와 있는 Windows PowerShell 명령에 대 한 자세한 내용은 다음을 참조 하세요.

- [Set-VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464283.aspx)
- [Get-VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464277.aspx)
- [Set-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848475.aspx)
- [Get-VMNetworkAdapterVlan](https://technet.microsoft.com/library/hh848516.aspx)





