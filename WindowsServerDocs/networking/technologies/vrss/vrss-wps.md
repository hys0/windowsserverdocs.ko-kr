---
title: RSS 및 vRSS Windows PowerShell 명령
description: 이 항목에서는 Windows PowerShell 명령에 대 한 수신 RSS (수신측 배율) 및 가상 vRSS (RSS)에 대 한 기술 참조 정보를 빠르게 찾는 방법을 알아봅니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/05/2018
ms.openlocfilehash: 10039388009e32c10d71067b835bad65db5607ef
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833264"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>RSS 및 vRSS Windows PowerShell 명령

>적용 대상: Windows Server (반기 채널), Windows Server 2016

이 항목에서는 수신측 배율에 대 한 Windows PowerShell 명령에 대 한 기술 참조 정보를 빠르게 찾는 방법을 배웁니다 \(RSS\) 및 가상 RSS \(vRSS\)합니다.

다음 RSS 명령을 사용 하 여 다중 프로세서 또는 다중 코어를 사용 하 여 물리적 컴퓨터에서 RSS를 구성 합니다. 동일한 명령을 사용 하 여 가상 컴퓨터에서 vRSS를 구성 하려면 \(VM\) 지원 되는 운영 체제를 실행 하는 합니다. 자세한 내용은 [Windows PowerShell의 네트워크 어댑터 Cmdlet](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps)합니다.

## <a name="configure-vmq"></a>VMQ를 구성 합니다.

vRSS는 VMQ가 사용 되 고 구성 해야 합니다. VMQ 설정을 관리 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

- [Disable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Enable-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Set-NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>사용 하도록 설정 하 고 기본 호스트에 RSS 구성

호스트 또는 VM에서 RSS를 관리할 수 있을 뿐만 아니라 기본 호스트에서 RSS를 구성 하려면 다음 PowerShell 명령을 사용 하 여 가상 NIC (vNIC). 이러한 명령의 매개 변수 중 일부 가상 머신 큐에도 영향을 줄 수 있습니다 \(VMQ\) Hyper-v 호스트에서.  

>[!IMPORTANT]
>호스트 vNIC 또는 VM에서 RSS를 사용 하도록 설정 하 고 vRSS를 사용 하기 위한 필수 구성 요소입니다.

- [Disable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Enable-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>Hyper에서 vRSS를 사용 하도록 설정\-V 가상 스위치 포트

VM에서 RSS를 사용 하는 것 외에도 vRSS는 하이퍼에서 vRSS를 사용 해야\-V 가상 스위치 포트. 

VRSS의 현재 설정을 확인 및 사용 하도록 설정 하거나 VM에 대 한 기능을 사용 하지 않도록 설정 합니다.

   **현재 설정을 보려면:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **기능을 사용 하도록 설정 합니다.**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>VRSS는 호스트 vNIC에 사용할지 설정 합니다.

VRSS에 대 한 현재 설정을 확인 하 고 사용 하도록 설정 또는 호스트 vNIC에 대 한 기능을 사용 하지 않도록 설정 합니다.

   **현재 설정을 보려면:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **기능을 사용할지 설정 합니다.** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>Hyper-v 가상 스위치 포트에서 예약 모드를 구성 합니다. 
>적용 대상: Windows Server 2019

Windows Server 2019 vRSS 동적으로 네트워크 트래픽을 처리 하는 데 사용 된 논리적 프로세서를 업데이트할 수 있습니다.  지원 되는 드라이버를 사용 하 여 장치에는 기본적으로 사용이 예약 모드를 있습니다. 

VM에 대 한 예약 모드를 수정 또는 시스템에 있는 예약 모드를 확인 합니다.

   **현재 설정을 보려면:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **설정 또는 예약 모드를 수정 합니다.**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>호스트 vNIC의 예약 모드를 구성 합니다.
>적용 대상: Windows Server 2019

현재 예약 모드를 확인 하려면 또는 호스트 vNIC에 대 한 예약 모드를 수정 하려면 다음 Windows PowerShell 명령을 사용 합니다.

   **현재 설정을 보려면:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **설정 또는 예약 모드를 수정 합니다.** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>관련 항목 
자세한 내용은 다음 참조 항목을 참조 하세요.

- [Get-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [Set-VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

자세한 내용은 [가상 수신측 배율 (vRSS)](vrss-top.md)합니다.