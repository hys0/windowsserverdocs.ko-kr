---
title: Virtual Network 어댑터에서 vRSS 사용
description: 이 항목에서는 Device Manager 또는 Windows PowerShell을 사용 하 여 Windows Server에서 vRSS를 사용 하도록 설정 하는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: cb48315c-0204-4927-aa24-64f6789c2e20
manager: dougkim
ms.localizationpriority: medium
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8f2886f01e4835cf2edb86fcae0a1fe77bc03d25
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405252"
---
# <a name="enable-vrss-on-a-virtual-network-adapter"></a>Virtual Network 어댑터에서 vRSS 사용

>적용 대상: Windows Server(반기 채널), Windows Server 2016

가상 RSS \(vRSS @ no__t-1을 사용 하려면 실제 어댑터에서 가상 머신 큐 \(VMQ @ no__t-3 지원이 필요 합니다. VMQ를 사용 하지 않도록 설정 하거나 지원 하지 않는 경우에는 가상 수신측 배율을 사용할 수 없습니다. 

자세한 내용은 [VRSS 사용 계획](vrss-plan.md)을 참조 하세요.

## <a name="enable-vrss-on-a-vm"></a>VM에서 vRSS 사용
 
Windows PowerShell 또는 Device Manager를 사용 하 여 vRSS를 사용 하도록 설정 하려면 다음 절차를 따르십시오.

-   장치 관리자
-   Windows PowerShell
  
### <a name="device-manager"></a>장치 관리자

Device Manager를 사용 하 여 vRSS를 사용 하도록 설정 하려면이 절차를 사용할 수 있습니다.

>[!NOTE]
>이 절차의 첫 번째 단계는 Windows 10 또는 Windows Server 2016를 실행 하는 Vm에 해당 합니다. VM이 다른 운영 체제를 실행 하는 경우 먼저 제어판을 열고 Device Manager를 찾아서 여는 방법으로 Device Manager를 열 수 있습니다.
  
1.  VM 작업 표시줄에서 **검색할 형식**에 **device**를 입력 합니다. 

2.  검색 결과에서 **Device Manager**를 클릭 합니다.

3.  Device Manager에서 **네트워크 어댑터**를 클릭 하 여 확장 합니다. 

4.  구성할 네트워크 어댑터를 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.<p>네트워크 어댑터 **속성** 대화 상자가 열립니다.

5.  네트워크 어댑터 **속성**에서 **고급** 탭을 클릭 합니다. 

6.  **속성**에서 아래로 스크롤하고 **수신측 배율**을 클릭 합니다. 

7.  **값** 선택이 **사용 하도록 설정**되어 있는지 확인 합니다. 

8.  **확인**을 클릭합니다.
  
> [!NOTE]
> **고급** 탭에서 일부 네트워크 어댑터는 어댑터에서 지 원하는 RSS 큐의 수도 표시 합니다.

---

### <a name="windows-powershell"></a>Windows PowerShell

Windows PowerShell을 사용 하 여 vRSS를 사용 하도록 설정 하려면 다음 절차를 따르십시오.

1. 가상 머신에서 **Windows PowerShell**을 엽니다.

2. 다음 명령을 입력 하 여 **-Name** 매개 변수의 *adaptername* 값을 구성할 네트워크 어댑터의 이름으로 바꾼 다음 enter 키를 누릅니다. 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >또는 다음 명령을 사용 하 여 vRSS를 사용 하도록 설정할 수 있습니다.
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

자세한 내용은 [RSS 및 vRSS에 대 한 Windows PowerShell 명령](vrss-wps.md)을 참조 하세요.

---