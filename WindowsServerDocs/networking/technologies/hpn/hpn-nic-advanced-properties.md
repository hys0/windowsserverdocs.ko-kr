---
title: NIC 고급 속성
description: Windows PowerShell 또는 네트워크 제어판을 통해 Nic 및 모든 기능을 관리할 수 있습니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0cafb1cc-5798-42f5-89b6-3ffe7ac024ba
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/20/2018
ms.openlocfilehash: 78d320f4309d60fa0396cbd723feafa07a65aea1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317008"
---
# <a name="nic-advanced-properties"></a>NIC 고급 속성

[Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps&viewFallbackFrom=winserverr2-ps) cmdlet을 사용 하 여 Windows PowerShell을 통해 nic 및 모든 기능을 관리할 수 있습니다.  네트워크 제어판 (ncpa.cpl)을 사용 하 여 Nic 및 모든 기능을 관리할 수도 있습니다. 

1. **Windows PowerShell**에서 두 개의 서로 다른 nic/모델에 대해 `Get‑NetAdapterAdvancedProperties` cmdlet을 실행 합니다.

   ![NetAdapterAdvancedProperty m1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-m1.png)

   ![NetAdapterAdvancedProperty c1](../../media/network-offload-and-optimization/Get-NetAdapterAdvancedProperty-c1.png)

   이러한 두 NIC 고급 속성 목록에는 유사점과 차이점이 있습니다.

2. **네트워크 제어판** (ncpa.cpl)에서 다음을 수행 합니다.

   a. NIC를 마우스 오른쪽 단추로 클릭 합니다.

   ![네트워크 연결 대화 상자](../../media/network-offload-and-optimization/network-connections-dialog.png)

   b. 속성 대화 상자에서 **구성**을 클릭 합니다.

    ![C1 속성](../../media/network-offload-and-optimization/c1-properties.png)

   c. **고급 탭을** 클릭 하 여 고급 속성을 봅니다.<p>이 목록의 항목은 `Get-NetAdapterAdvancedProperties` 출력의 항목과 관련이 있습니다.

   ![Chelsio 네트워크 어댑터 속성](../../media/network-offload-and-optimization/chelsio-network-adapter-properties.png)

---
