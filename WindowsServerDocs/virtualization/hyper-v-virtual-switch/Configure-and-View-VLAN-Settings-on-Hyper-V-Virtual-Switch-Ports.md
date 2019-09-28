---
title: Hyper-V 가상 스위치 포트에서 VLAN 설정 구성 및 확인
description: 이 항목을 사용 하 여 Windows Server 2016의 Hyper-v 가상 스위치 포트에서 VLAN (virtual Local Area Network) 설정을 구성 하 고 보는 방법에 대 한 모범 사례를 배울 수 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: article
ms.assetid: 69e0e28a-98ae-4ade-bd27-ce2ad7eb310f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 28abdfe8295ad3f9fac29b8cc80aeebe2992392c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366874"
---
# <a name="configure-and-view-vlan-settings-on-hyper-v-virtual-switch-ports"></a>Hyper-V 가상 스위치 포트에서 VLAN 설정 구성 및 확인

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 Hyper-v 가상 스위치 포트에서 VLAN (virtual Local Area Network) 설정을 구성 하 고 보는 방법에 대 한 모범 사례를 배울 수 있습니다.

Hyper-v 가상 스위치 포트에서 VLAN 설정을 구성 하려는 경우 Windows @ no__t-0 Server 2016 Hyper-v 관리자 또는 System Center Virtual Machine Manager (VMM)를 사용할 수 있습니다.

VMM을 사용 하는 경우 VMM에서 다음 Windows PowerShell 명령을 사용 하 여 스위치 포트를 구성 합니다.

```
Set-VMNetworkAdapterIsolation <VM-name|-managementOS> -IsolationMode VLAN -DefaultIsolationID <vlan-value> -AllowUntaggedTraffic $True
```
VMM을 사용 하지 않고 Windows Server에서 스위치 포트를 구성 하는 경우 Hyper-v 관리자 콘솔 이나 다음 Windows PowerShell 명령을 사용할 수 있습니다.
```
Set-VMNetworkAdapterVlan <VM-name|-managementOS> -Access -VlanID <vlan-value>
```

Hyper-v 가상 스위치 포트에서 VLAN 설정을 구성 하는 두 가지 방법으로 인해, 스위치 포트 설정을 확인 하려고 하면 VLAN 설정이 구성 되지 않은 것 처럼 표시 될 수 있습니다.

## <a name="use-the-same-method-to-configure-and-view-switch-port-vlan-settings"></a>동일한 방법을 사용 하 여 스위치 포트 VLAN 설정을 구성 하 고 확인 합니다.

이러한 문제가 발생 하지 않도록 하려면 동일한 방법을 사용 하 여 스위치 포트 VLAN 설정을 구성 하는 데 사용한 스위치 포트 VLAN 설정을 확인 해야 합니다.

VLAN 스위치 포트 설정을 구성 하 고 확인 하려면 다음을 수행 해야 합니다.

- VMM 또는 네트워크 컨트롤러를 사용 하 여 네트워크를 설정 및 관리 하 고 SDN (소프트웨어 정의 네트워킹)을 배포한 경우 **VMNetworkAdapterIsolation** cmdlet을 사용 해야 합니다. 
- Windows Server 2016 Hyper-v 관리자 또는 Windows PowerShell cmdlet을 사용 하는 경우 SDN (소프트웨어 정의 네트워킹)을 배포 하지 않은 경우 **set-vmnetworkadaptervlan** cmdlet을 사용 해야 합니다.

### <a name="possible-issues"></a>가능한 문제

이러한 지침을 따르지 않으면 다음과 같은 문제가 발생할 수 있습니다.

- SDN을 배포 하 고 VMM, 네트워크 컨트롤러 또는 **VMNetworkAdapterIsolation** cmdlet을 사용 하 여 Hyper-v 가상 스위치 포트에서 VLAN 설정을 구성 하는 경우: Hyper-v 관리자 또는 **Get set-vmnetworkadaptervlan** 를 사용 하 여 구성 설정을 확인 하는 경우 명령 출력에 VLAN 설정이 표시 되지 않습니다. 대신 **VMNetworkIsolation** cmdlet을 사용 하 여 VLAN 설정을 확인 해야 합니다.
- SDN을 배포 하지 않은 환경에서는 대신 Hyper-v 관리자 또는 **set-vmnetworkadaptervlan** cmdlet을 사용 하 여 Hyper-v 가상 스위치 포트에서 VLAN 설정을 구성 합니다. **VMNetworkIsolation** cmdlet을 사용 하 여 구성 설정을 확인 하는 경우 명령 출력에 VLAN 설정이 표시 되지 않습니다. 대신, VLAN 설정을 보려면 **Get set-vmnetworkadaptervlan** cmdlet을 사용 해야 합니다.

또한 두 구성 방법 모두를 사용 하 여 동일한 스위치 포트 VLAN 설정을 구성 하지 않는 것이 중요 합니다. 이 작업을 수행 하는 경우 스위치 포트가 잘못 구성 되 고 결과는 네트워크 통신에 실패할 수 있습니다.

### <a name="resources"></a>리소스

이 항목에서 설명 하는 Windows PowerShell 명령에 대 한 자세한 내용은 다음을 참조 하십시오.

- [VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464283.aspx)
- [VmNetworkAdapterIsolation](https://technet.microsoft.com/library/dn464277.aspx)
- [Set-vmnetworkadaptervlan](https://technet.microsoft.com/library/hh848475.aspx)
- [Set-vmnetworkadaptervlan](https://technet.microsoft.com/library/hh848516.aspx)





