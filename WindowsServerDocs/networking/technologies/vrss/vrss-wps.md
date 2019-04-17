---
title: RSS 및 vRSS Windows PowerShell 명령
description: 이 항목에서는 수신 측 크기 조정 (RSS) 및 가상 RSS (vRSS)에 대 한 Windows PowerShell 명령에 대 한 기술 참조 정보를 찾을 신속 하 게 하는 방법을 알아봅니다.
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
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339271"
---
# RSS 및 vRSS Windows PowerShell 명령

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목에서는 \(RSS\) 수신측 배율 및 가상 RSS \(vRSS\) Windows PowerShell 명령에 대 한 기술 참조 정보를 찾을 신속 하 게 하는 방법을 알아봅니다.

다중 프로세서 또는 여러 코어를 사용 하 여 물리적 컴퓨터에서 RSS를 구성 하려면 다음 RSS 명령을 사용 합니다. 동일한 명령을 사용 하 여 가상 컴퓨터에서 vRSS를 구성 하려면 운영 체제를 실행 하는 \(VM\) 합니다. 자세한 내용은 [Windows PowerShell의 네트워크 어댑터 Cmdlet](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps)을 참조 하세요.

## VMQ 구성

vRSS는 VMQ 사용 되 고 구성 해야 합니다. VMQ 설정을 관리 하는 다음 Windows PowerShell 명령을 사용할 수 있습니다.

- [NetAdapterVmq 사용 안 함](https://docs.microsoft.com/powershell/module/netadapter/disable-netadaptervmq?view=win10-ps)
- [Enable NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/enable-netadaptervmq?view=win10-ps)
- [Get NetAdapterVmq](https://docs.microsoft.com/powershell/module/netadapter/get-netadaptervmq?view=win10-ps)
- [NetAdapterVmq 설정](https://docs.microsoft.com/powershell/module/netadapter/set-netadaptervmq?view=win10-ps)

## 사용 설정 및 기본 호스트에서 RSS 구성

다음 PowerShell 명령을 사용 하 여 기본 호스트에서 RSS를 구성할 수 있을 뿐만 아니라 관리 하는 호스트 또는 VM에서 RSS 가상 NIC (vNIC). Hyper-v 호스트에서 가상 컴퓨터 큐 \(VMQ\)에 영향을 줄 수 이러한 명령의 매개 변수 중 일부입니다.  

>[!IMPORTANT]
>호스트 vNIC 또는 VM에서 RSS을 활성화 하 고 vRSS를 사용 하 여 필수 구성 요소입니다.

- [NetAdapterRss 사용 안 함](https://docs.microsoft.com/powershell/module/netadapter/disable-netadapterrss?view=win10-ps)
- [Enable NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/enable-netadapterrss?view=win10-ps)
- [Get NetAdapterRss](https://docs.microsoft.com/powershell/module/netadapter/get-netadapterrss?view=win10-ps)
- [NetAdapterRss 설정](https://docs.microsoft.com/powershell/module/netadapter/Set-NetAdapterRss?view=win10-ps)

## Hyper\-v 가상 스위치 포트에서 vRSS를 사용 하도록 설정

VM에서 RSS를 사용 하는 것 외에도 vRSS vRSS Hyper\-v 가상 스위치 포트에서 사용 하도록 설정 해야 합니다. 

VRSS에 대 한 현재 설정을 확인 하 고 활성화 또는 VM에 대 한 기능을 사용 하지 않도록 설정 합니다.

   **현재 설정을 보려면** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | fl
   ```

   **기능을 활성화 합니다.**
   
   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssEnabled [$True|$False]
   ```

## 활성화 또는 비활성화 호스트 vNIC에서 vRSS

VRSS에 대 한 현재 설정을 확인 하 고 활성화 또는 호스트 vNIC에 대 한 기능을 사용 하지 않도록 설정 합니다.

   **현재 설정을 보려면** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | fl
   ```

   **활성화 또는 기능을 사용 하지 않도록 설정:** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled [$True|$False]
   ```

## Hyper-v 가상 스위치 포트에서 일정 모드를 구성 합니다. 
>적용 대상: Windows Server 2019

Windows Server 2019의 vRSS 동적으로 네트워크 트래픽을 처리 하는 데 논리 프로세서를 업데이트할 수 있습니다.  지원 되는 드라이버를 사용 하 여 디바이스에는 기본적으로 사용이 스케줄링 모드를 있습니다. 

시스템에서 현재 일정 모드를 확인 하거나 VM에 대 한 일정 모드를 수정 합니다.

   **현재 설정을 보려면** 

   ```PowerShell
   Get-VMNetworkAdapter <vm-name> | Select 'VRSSQueue'
   ```

   **설정 또는 일정 모드를 수정 합니다.**

   ```PowerShell
   Set-VMNetworkAdapter <vm-name> -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```

## 호스트 vNIC에서 일정 모드 구성
>적용 대상: Windows Server 2019

존재 일정 모드를 확인 하거나 일정 모드는 호스트 vNIC 수정 하려면 다음 Windows PowerShell 명령을 사용 하세요.

   **현재 설정을 보려면** 

   ```PowerShell
   Get-VMNetworkAdapter -ManagementOS | Select 'VRSSQueue'
   ```

   **설정 또는 일정 모드를 수정 합니다.** 

   ```PowerShell
   Set-VMNetworkAdapter -ManagementOS -VrssQueueSchedulingMode -VrssQueueSchedulingMode [Dynamic|$StaticVrss|StaticVMQ]
   ```


## 관련 항목 
자세한 내용은 다음 참조 항목을 참조 하세요.

- [Get VMNetworkAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmnetworkadapter)
- [VMNetworkAdapter 설정](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmnetworkadapter)

자세한 내용은 [가상 수신측 배율 (vRSS)를](vrss-top.md)참조 하세요.