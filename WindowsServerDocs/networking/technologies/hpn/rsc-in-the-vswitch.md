---
title: vSwitch RSC(수신 세그먼트 통합)
description: 수신 세그먼트 (RSC) vSwitch에는 Windows Server 2019의 기능 및 Windows 10 년 10 월 2018 Update는 절감 호스트 CPU 사용률 및 가상 워크 로드에 대 한 처리량 증가에 적지만 크기가 큰 여러 TCP 세그먼트를 결합 하 여 세그먼트입니다. 더 적은 수의 큰 세그먼트 (병합)을 처리 하는 것은 처리 보다 더 효율적으로 여러 개의 작은 세그먼트입니다.
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.author: dacuo
author: shortpatti
ms.date: 09/07/2018
ms.openlocfilehash: 667e795e398443cadd4c966cc31e65eeee4962f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827784"
---
# <a name="rsc-in-the-vswitch"></a>VSwitch의 RSC
>적용 대상: Windows Server 2019

수신 세그먼트 (RSC) vSwitch에는 Windows Server 2019의 기능 및 Windows 10 년 10 월 2018 Update는 절감 호스트 CPU 사용률 및 가상 워크 로드에 대 한 처리량 증가에 적지만 크기가 큰 여러 TCP 세그먼트를 결합 하 여 세그먼트입니다. 더 적은 수의 큰 세그먼트 (병합)을 처리 하는 것은 처리 보다 더 효율적으로 여러 개의 작은 세그먼트입니다.

Windows Server 2012 이상 수신 세그먼트 통합이 라고도 하는 기술의 (실제 네트워크 어댑터에서 구현 됨)는 하드웨어만 오프 로드 버전이 포함 되었습니다. RSC의 오프 로드 된이 버전은 Windows의 이후 버전에서 계속 사용할 수 있습니다. 그러나 가상 워크 로드와 호환 되지 않습니다 및 vSwitch를 실제 네트워크 어댑터 연결 되 면 사용 하지 않도록 설정 되었습니다. RSC의 하드웨어 전용 버전에 대 한 자세한 내용은 참조 하세요. [수신 세그먼트 병합 (RSC)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh997024(v=ws.11))합니다.

## <a name="scenarios-that-benefit-from-rsc-in-the-vswitch"></a>VSwitch의 RSC를 활용 하는 시나리오

이 기능에서 해당 데이터 경로 가상 스위치를 통과 하는 워크 로드 이점을 제공 합니다.

예를 들어 다음과 같은 가치를 제공해야 합니다.

-   호스트 가상 Nic 포함:

    -   소프트웨어 방식 네트워킹

    -   Hyper-V 호스트

    -   저장소 공간 다이렉트

-   Hyper-v 게스트 가상 Nic

-   소프트웨어 정의 네트워킹 GRE 게이트웨이

-   컨테이너

이 기능을 사용 하 여 호환 되지 않는 워크 로드에는 다음이 포함 됩니다.

-   소프트웨어 정의 네트워킹 IPSEC 게이트웨이

-   SR-IOV 가상 Nic를 사용 하도록 설정

-   SMB 다이렉트

## <a name="configure-rsc-in-the-vswitch"></a>RSC vSwitch에서 구성


RSC는 기본적으로 외부 Vswitch에서 사용 됩니다.

**현재 설정을 보려면:**

```PowerShell
Get-VMSwitch -Name vSwitchName | Select-Object *RSC*
```

**VSwitch의 RSC를 사용 하지 않도록 설정 하거나 사용**


>[!IMPORTANT]
>중요: RSC vSwitch에서 사용 될 수 있고 기존 연결에 영향을 주지 않고 즉시 사용할 수 없습니다.


**VSwitch의 RSC를 사용 하지 않도록 설정**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $false
```

**다시 RSC vSwitch에서 사용 하도록 설정**

```PowerShell
Set-VMSwitch -Name vSwitchName -EnableSoftwareRsc $True
```
자세한 내용은 [Set-vmswitch](https://docs.microsoft.com/powershell/module/hyper-v/set-vmswitch?view=win10-ps)합니다.
