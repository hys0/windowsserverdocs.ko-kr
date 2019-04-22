---
title: NIC 고급 속성
description: Nic 및 Windows PowerShell 또는 네트워크 제어판을 통해 모든 기능을 관리할 수 있습니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/20/2018
ms.openlocfilehash: d1a5fb57bf71fd981e001cfd9ac595ab5bc3cfc5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819904"
---
# <a name="nic-advanced-properties"></a>NIC 고급 속성

Nic 및 사용 하 여 Windows PowerShell을 통해 모든 기능을 관리할 수 있습니다 합니다 [NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps) cmdlet.  또한 Nic 및 네트워크 Control Panel (ncpa.cpl)를 사용 하 여 모든 기능을 관리할 수 있습니다. 

1. **Windows PowerShell**실행을 `Get‑NetAdapterAdvancedProperties` 두 개의 다른 메이커/모델 nic에 대해 cmdlet.

   ![Get-NetAdapterAdvancedProperty m1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![Get-NetAdapterAdvancedProperty c1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   이러한 두 개의 NIC 고급 속성 표시의 공통점과 차이점 있습니다.

2. 에 **네트워크 제어판** (ncpa.cpl) 다음을 수행 합니다.

   a. NIC를 마우스 오른쪽 단추로 클릭 하 고

   ![네트워크 연결 대화 상자](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b. 속성 대화 상자에서 클릭 **구성**합니다.

    ![C1 속성](../../media/network-offload-and-optimization/c1-properties.png)

   다. 클릭 합니다 **고급** 고급 속성을 보려면 탭 합니다.<p>이 목록에 있는 항목의 항목에 연결 된 `Get-NetAdapterAdvancedProperties` 출력 합니다.

   ![Chelsio 네트워크 어댑터 속성](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---