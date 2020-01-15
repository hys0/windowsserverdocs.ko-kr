---
title: VRSS 문제 해결
description: VM LPs에 대 한 vRSS 부하 분산 트래픽이 표시 되지 않는 경우 vRSS 문제를 해결 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: 3bbb70657cb009ce760ccfe273b24c6df17d3ca7
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949908"
---
# <a name="resolve-vrss-issues"></a>VRSS 문제 해결

모든 준비 단계를 완료 했 고 여전히 VM LPs에 대 한 vRSS 부하 분산 트래픽이 표시 되지 않는 경우 가능한 여러 가지 문제가 있습니다.

1. 준비 단계를 수행 하기 전에 vRSS를 사용 하지 않도록 설정 하 고 이제를 사용 하도록 설정 해야 합니다. **VMNetworkAdapter** 를 실행 하 여 VM에 대해 vRSS를 사용 하도록 설정할 수 있습니다.

   ```PowerShell
   Set-VMNetworkAdapter <VMname> -VrssEnabled $TRUE
   Set-VMNetworkAdapter -ManagementOS -VrssEnabled $TRUE
   ```

2. RSS가 VM 또는 호스트 vNIC에서 사용 하지 않도록 설정 되었습니다. Windows Server 2016에서는 기본적으로 RSS를 사용 하도록 설정 합니다. 누군가가 사용 하지 않도록 설정 했을 수 있습니다. 

   - Enabled = **True**

   **현재 설정 보기:** 

   Vm\)의 vRSS에 대 한 VM\(또는 host vNIC vRSS\)에 대 한 호스트 \(에서 다음 PowerShell cmdlet을 실행 합니다.

   ```PowerShell
   Get-NetAdapterRss
   ```

   **기능을 사용 하도록 설정 합니다.** 

   값을 False에서 True로 변경 하려면 다음 PowerShell cmdlet을 실행 합니다.

   ```PowerShell
   Enable-NetAdapterRss *
   ```
   
   RSS를 구성 하는 다른 시스템 차원의 방법은 netsh를 사용 하는 것입니다. 기본 수학에는 
   
    ```cmd
   netsh int tcp show global
   ```
   
   RSS가 전역적으로 사용 하지 않도록 설정 되어 있는지 확인 합니다. 필요한 경우 사용 하도록 설정 합니다. 이 설정은 *-Set-netadapterrss에서 처리 되지 않습니다.

3. VRSS를 구성한 후 VMMQ를 사용할 수 없는 경우 가상 스위치에 연결 된 각 어댑터에서 다음 설정을 확인 합니다.

   - VmmqEnabled = **False**
   - VmmqEnabledRequested = **True**

   ![vmmq-사용](../../media/vmmq-enabled.png)

   **현재 설정 보기:** 

   ```PowerShell
   Get-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS'
   ```

   **기능을 사용 하도록 설정 합니다.** 

   ```PowerShell
   Set-NetAdapterAdvancedProperty -Name NICName -DisplayName 'Virtual Switch RSS' -DisplayValue Enabled”
   ```
 
4. _(Windows Server 2019)_ **VrssQueueSchedulingMode** 를 **동적**으로 설정 하는 동안에는 VMMQ (VmmqEnabled = False)를 사용 하도록 설정할 수 없습니다. VMMQ를 사용 하도록 설정 하면 VrssQueueSchedulingMode는 동적으로 변경 되지 않습니다.<p>VMMQ를 사용 하는 경우 **동적** **VrssQueueSchedulingMode** 드라이버 지원이 필요 합니다.  VMMQ는 논리적 프로세서에서 패킷 배치를 오프 로드 하는 것으로, 동적 알고리즘을 활용 하려면 드라이버를 지원 해야 합니다.  동적 VMMQ을 지 원하는 NIC 공급 업체의 드라이버 및 펌웨어를 설치 하세요.



---
