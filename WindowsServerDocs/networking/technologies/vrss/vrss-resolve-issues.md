---
title: VRSS 문제 해결
description: VM Lp 트래픽을 분산 로드 vRSS 보이지 vRSS 문제를 해결 합니다.
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
ms.sourcegitcommit: 515b4fd5c40fcbae0e12a2c30090384533972353
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/29/2018
ms.locfileid: "8232522"
---
## VRSS 문제 해결

모두 준비 단계가 완료 하는 경우 여전히 VM Lp 트래픽을 분산 로드 vRSS 표시 되지 않으면 다른 가능한 문제가 있습니다.

1. 준비 단계를 수행 하기 전에 vRSS-비활성화 되 고 이제 사용할 수 있어야 합니다. VM에 대 한 vRSS 수 있도록 **설정 VMNetworkAdapter** 실행할 수 있습니다.

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS는 호스트 vNIC 또는 VM에서 사용할 수 없습니다. Windows Server 2016 기본적으로 RSS 수 있습니다. 사용자가 사용 하지 못할 것. 

   - 활성화 = **True**

   **현재 설정을 보려면** 

   (VRSS에는 VM\)에 대 한 VM\에서 다음 PowerShell cmdlet을 실행 또는 호스트에서 \ (예: 호스트 vNIC vRSS\).

   ```PowerShell
   Get-NetAdapterRss
   ```

   **기능을 활성화 합니다.** 

   True에서 False 값을 변경, 하려면 다음 PowerShell cmdlet을 실행 합니다.

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   RSS를 구성 하는 다른 시스템 수준 방법은 netsh를 사용 합니다. 사용 
   
    ```cmd
   netsh int tcp show global
   ```
   
   되도록 해당 RSS 전체적으로 비활성화 되지 않습니다. 하 고 필요한 경우 사용 합니다. 이 설정은 하 여 터치 되지 *-NetAdapterRSS 합니다.

3. VRSS를 구성한 후 VMMQ 됨을 찾을 경우 가상 스위치에 연결 된 각 어댑터에서 다음 설정을 확인 합니다.

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq 지원](../../media/vmmq-enabled.png)

   **현재 설정을 보려면** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **기능을 활성화 합니다.** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(Windows Server 2019)_ VMMQ를 활성화할 수 없습니다 (VmmqEnabled = False)를 **동적** **VrssQueueSchedulingMode** 를 설정 하는 동안 합니다. VrssQueueSchedulingMode VMMQ 설정 되 면 동적으로 변경 되지 않습니다.<p>**동적** 의 **VrssQueueSchedulingMode** VMMQ 활성화 되 면 드라이버 지원이 필요 합니다.  VMMQ 논리 프로세서에서 패킷 배치는 오프 로드 되며, 동적 알고리즘을 활용 하 여 드라이버 지원이 필요 합니다.  NIC 공급 업체의 드라이버 및 동적 VMMQ를 지 원하는 펌웨어를 설치 하세요.



---
