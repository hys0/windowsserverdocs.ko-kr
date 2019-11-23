---
title: RSS 및 vRSS에 대 한 Windows PowerShell 명령
description: 이 항목에서는 RSS (수신측 배율) 및 vRSS (가상 RSS)를 위한 Windows PowerShell 명령에 대 한 기술 참조 정보를 신속 하 게 찾는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 49e93b9f-46d9-4cee-bcda-1c4634893ddd
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/05/2018
ms.openlocfilehash: bb915f72e53d28c73a9c2e405b3b0edd656953db
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405277"
---
# <a name="windows-powershell-commands-for-rss-and-vrss"></a>RSS 및 vRSS에 대 한 Windows PowerShell 명령

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 RSS\) 및 가상 RSS \(vRSS\)에 대 한 Windows PowerShell 명령에 대 한 기술 참조 정보를 신속 하 게 찾는 방법을 알아봅니다 \(.

여러 프로세서나 여러 코어가 있는 물리적 컴퓨터에서 RSS를 구성 하려면 다음 RSS 명령을 사용 합니다. 동일한 명령을 사용 하 여 지원 되는 운영 체제를 실행 하는 VM\) \(가상 머신에서 vRSS를 구성할 수 있습니다. 자세한 내용은 [Windows PowerShell의 네트워크 어댑터 cmdlet](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps)(영문)을 참조 하세요.

## <a name="configure-vmq"></a>VMQ 구성

vRSS를 사용 하려면 VMQ를 사용 하도록 설정 하 고 구성 해야 합니다. 다음 Windows PowerShell 명령을 사용 하 여 VMQ 설정을 관리할 수 있습니다.

- [Disable-Set-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Set-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Set-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [Set-netadaptervmq](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## <a name="enable-and-configure-rss-on-a-native-host"></a>네이티브 호스트에서 RSS 사용 및 구성

다음 PowerShell 명령을 사용 하 여 네이티브 호스트에서 RSS를 구성 하 고 VM 또는 호스트 가상 NIC (vNIC)의 RSS를 관리할 수 있습니다. 이러한 명령의 매개 변수 중 일부는 Hyper-v 호스트의 VMQ\) \(가상 머신 큐에도 영향을 줄 수 있습니다.  

>[!IMPORTANT]
>VM 또는 호스트 vNIC에서 RSS를 사용 하도록 설정 하는 것은 vRSS를 사용 하도록 설정 하 고 사용 하기 위한 필수 구성 요소입니다.

- [Disable-Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [Set-netadapterrss](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## <a name="enable-vrss-on-the-hyper-v-virtual-switch-port"></a>하이퍼\-V 가상 스위치 포트에서 vRSS 사용

VM에서 RSS를 사용 하도록 설정 하는 것 외에도 vRSS를 사용 하려면 하이퍼\-V 가상 스위치 포트에서 vRSS를 사용 하도록 설정 해야 합니다. 

VRSS에 대 한 현재 설정을 확인 하 고 VM에 대 한 기능을 사용 하거나 사용 하지 않도록 설정 합니다.

   **현재 설정 보기:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **기능 사용:**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## <a name="enable-or-disable-vrss-on-a-host-vnic"></a>호스트 vNIC vRSS 사용 또는 사용 안 함

VRSS에 대 한 현재 설정을 확인 하 고 호스트 vNIC 기능을 사용 하거나 사용 하지 않도록 설정 합니다.

   **현재 설정 보기:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **기능을 사용 하거나 사용 하지 않도록 설정 합니다.** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## <a name="configure-the-scheduling-mode-on-the-hyper-v-virtual-switch-port"></a>Hyper-v 가상 스위치 포트에서 일정 모드 구성 
>적용 대상: Windows Server 2019

Windows Server 2019에서 vRSS는 네트워크 트래픽을 동적으로 처리 하는 데 사용 되는 논리적 프로세서를 업데이트할 수 있습니다.  지원 되는 드라이버가 있는 장치는 기본적으로이 일정 모드를 사용 하도록 설정 합니다. 

시스템의 현재 예약 모드를 확인 하거나 VM에 대 한 예약 모드를 수정 합니다.

   **현재 설정 보기:** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **예약 모드를 설정 하거나 수정 합니다.**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## <a name="configure-the-scheduling-mode-on-a-host-vnic"></a>호스트 vNIC 일정 모드 구성
>적용 대상: Windows Server 2019

현재 예약 모드를 확인 하거나 호스트 vNIC 일정 모드를 수정 하려면 다음 Windows PowerShell 명령을 사용 합니다.

   **현재 설정 보기:** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **예약 모드를 설정 하거나 수정 합니다.** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## <a name="related-topics"></a>관련 항목 
자세한 내용은 다음 참조 항목을 참조 하세요.

- [VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

자세한 내용은 [vRSS (가상 수신측 배율)](vrss-top.md)를 참조 하세요.