---
title: vSwitch RSC(수신 세그먼트 통합)
description: VSwitch의 RSC (수신 세그먼트 통합)는 Windows Server 2019 및 Windows 10 10 월 2018 업데이트의 기능입니다 .이 기능을 사용 하면 호스트 CPU 사용률을 줄이고 여러 TCP 세그먼트를 더 작은 수로 결합 하 여 가상 워크 로드에 대 한 처리량을 높일 수 있습니다. 분류. 적은 수의 작은 세그먼트를 처리 하는 것 보다 적은 수의 대량 세그먼트 (병합)를 처리 하는 것이 더 효율적
manager: dougkim
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.author: dacuo
author: dcuomo
ms.date: 09/07/2018
ms.openlocfilehash: 0ffb417728bbdb73d8fb462ff7783b17b511bcd3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814776"
---
# <a name="rsc-in-the-vswitch"></a>VSwitch의 RSC
>적용 대상: Windows Server 2019

VSwitch의 RSC (수신 세그먼트 통합)는 Windows Server 2019 및 Windows 10 10 월 2018 업데이트의 기능입니다 .이 기능을 사용 하면 호스트 CPU 사용률을 줄이고 여러 TCP 세그먼트를 더 작은 수로 결합 하 여 가상 워크 로드에 대 한 처리량을 높일 수 있습니다. 분류. 적은 수의 작은 세그먼트를 처리 하는 것 보다 적은 수의 대량 세그먼트 (병합)를 처리 하는 것이 더 효율적

Windows Server 2012 이상에는 수신 세그먼트 병합이 라고도 하는 하드웨어 전용 오프 로드 버전 (실제 네트워크 어댑터에서 구현 됨)이 포함 되어 있습니다. 이 오프 로드 된 RSC 버전은 Windows의 이후 버전에서 계속 사용할 수 있습니다. 그러나 실제 네트워크 어댑터가 vSwitch에 연결 된 후에는 가상 워크 로드와 호환 되지 않으며 사용 하지 않도록 설정 되었습니다. RSC의 하드웨어 전용 버전에 대 한 자세한 내용은 [rsc (수신 세그먼트 통합)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997024(v=ws.11))를 참조 하세요.

## <a name="scenarios-that-benefit-from-rsc-in-the-vswitch"></a>VSwitch에서 RSC를 활용 하는 시나리오

데이터 경로이이 기능을 통해 가상 스위치를 통과 하는 워크 로드입니다.

예를 들면 다음과 같습니다.

-   다음을 포함 하는 호스트 가상 Nic:

    -   소프트웨어 방식 네트워킹

    -   Hyper-V 호스트

    -   저장소 공간 다이렉트

-   Hyper-v 게스트 가상 Nic

-   소프트웨어 정의 네트워킹 GRE 게이트웨이

-   컨테이너

이 기능과 호환 되지 않는 작업은 다음과 같습니다.

-   소프트웨어 정의 네트워킹 IPSEC 게이트웨이

-   SR-IOV 사용 가상 Nic

-   SMB 다이렉트

## <a name="configure-rsc-in-the-vswitch"></a>VSwitch에서 RSC 구성


기본적으로 외부 vSwitches에서 RSC를 사용 하도록 설정 합니다.

**현재 설정 보기:**

```PowerShell
Get-VMSwitch -Name vSwitchName | Select-Object *RSC*
```

**VSwitch에서 RSC 사용 또는 사용 안 함**


>[!IMPORTANT]
>중요: vSwitch의 RSC를 사용 하도록 설정 하 고 기존 연결에 영향을 주지 않고 즉석에서 사용 하지 않도록 설정할 수 있습니다.


**VSwitch에서 RSC를 사용 하지 않도록 설정**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $false
```

**VSwitch에서 RSC를 다시 사용 하도록 설정**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $True
```
자세한 내용은 [설정-VMSwitch](https://docs.microsoft.com/powershell/module/hyper-v/set-vmswitch?view=win10-ps)를 참조 하세요.
