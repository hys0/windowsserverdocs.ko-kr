---
title: VRSS 문제 해결
description: VRSS 트래픽 부하 분산 VM LPs에 표시 되지 않으면 vRSS 문제를 해결 합니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: a2d6eb43149361b4270565b63fc99f483f364f74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824034"
---
## <a name="resolve-vrss-issues"></a>VRSS 문제 해결

모든 준비 단계를 완료 하는 경우 여전히 vRSS 트래픽 부하 분산 VM LPs에 표시 되지 않으면 다른 가능한 문제가 있습니다.

1. 준비 단계를 수행 하기 전에 vRSS-비활성화 되 고 이제 사용할 수 있어야 합니다. 실행할 수 있습니다 **Set-vmnetworkadapter** VM에 대 한 vRSS를 사용 하도록 설정 합니다.

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS는 VM 또는 호스트 vNIC에 비활성화 되었습니다. Windows Server 2016 RSS 기본적으로 사용 하도록 설정 사용자가 될 수 있습니다 사용 하지 않도록 설정한 것입니다. 

   - 사용 하도록 설정 = **True**

   **현재 설정을 보려면:** 

   VM에서 다음 PowerShell cmdlet을 실행\(vRSS vm에서에 대 한\) 컴퓨터나 호스트 \(호스트 vNIC vRSS를\)입니다.

   ```PowerShell
   Get-NetAdapterRss
   ```

   **기능을 사용 합니다.** 

   값을 False에서 True를으로 변경 하려면 다음 PowerShell cmdlet을 실행 합니다.

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   RSS를 구성 하는 다른 시스템 차원의 방법은 netsh를 사용 합니다. 이후 
   
    ```cmd
   netsh int tcp show global
   ```
   
   되도록 해당 RSS는 전역적으로 비활성화 되지 않습니다. 및 필요한 경우 사용 하도록 설정 합니다. 이 설정 되지 않습니다 접한 *-NetAdapterRSS 합니다.

3. VRSS를 구성한 후 VMMQ 해제 되어 있다면 가상 스위치에 연결 된 각 어댑터에서 다음 설정을 확인 합니다.

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq-enabled](../../media/vmmq-enabled.png)

   **현재 설정을 보려면:** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **기능을 사용 합니다.** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(Windows Server 2019)_  VMMQ을 사용할 수 없습니다 (VmmqEnabled = False) 설정 하는 동안 **VrssQueueSchedulingMode** 하려면 **동적**합니다. VrssQueueSchedulingMode VMMQ 활성화 되 면 동적으로 변경 되지 않습니다.<p>합니다 **VrssQueueSchedulingMode** 의 **동적** VMMQ을 사용 하는 경우 드라이버 지원이 필요 합니다.  VMMQ 논리적 프로세서 패킷 배치를 오프 로드 되며 따라서 동적 알고리즘을 활용 하 여 드라이버 지원에 필요 합니다.  NIC 공급 업체의 드라이버 및 지 원하는 동적 VMMQ 펌웨어를 설치 하세요.



---
