---
title: 가상 네트워크 어댑터에서 vRSS를 사용 하도록 설정
description: 이 항목에서는 장치 관리자 또는 Windows PowerShell을 사용 하 여 Windows Server에서 vRSS를 사용 하도록 설정 하는 방법을 알아봅니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: cb48315c-0204-4927-aa24-64f6789c2e20
manager: dougkim
ms.localizationpriority: medium
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 19e8011fb98b84c20e8237792664551d2362d589
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882684"
---
# <a name="enable-vrss-on-a-virtual-network-adapter"></a>가상 네트워크 어댑터에서 vRSS를 사용 하도록 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

가상 RSS \(vRSS\) 가상 머신 큐 필요 \(VMQ\) 실제 어댑터에서 지원 합니다. VMQ는 사용 되지 않거나 지원 되지 않습니다 다음 가상 수신측 배율을 사용 되지 않습니다. 

자세한 내용은 [vRSS 사용 계획](vrss-plan.md)합니다.

## <a name="enable-vrss-on-a-vm"></a>VM에서 vRSS를 사용 하도록 설정
 
Windows PowerShell 또는 장치 관리자를 사용 하 여 vRSS를 사용 하도록 설정 하려면 다음 절차를 사용 합니다.

-   장치 관리자
-   Windows PowerShell
  
### <a name="device-manager"></a>장치 관리자

장치 관리자를 사용 하 여 vRSS를 사용 하도록 설정 하려면이 절차를 사용할 수 있습니다.

>[!NOTE]
>이 절차의 첫 번째 단계는 Windows 10 또는 Windows Server 2016을 실행 중인 Vm에 관련이 있습니다. VM은 다른 운영 체제를 실행 하는 경우 첫 번째 제어판을 열고, 다음 찾기 및 열기 장치 관리자에서 장치 관리자를 열면 됩니다.
  
1.  VM 작업 표시줄에서 **검색할 형식을**, 형식 **장치**. 

2.  검색 결과에서 클릭 **장치 관리자**합니다.

3.  장치 관리자에서 클릭 하 여 확장 **네트워크 어댑터가**합니다. 

4.  구성 하 고 클릭 하려는 네트워크 어댑터를 마우스 오른쪽 단추로 클릭 **속성**합니다.<p>네트워크 어댑터 **속성** 대화 상자가 열립니다.

5.  네트워크 어댑터에서 **속성**를 클릭 합니다 **고급** 탭 합니다. 

6.  **속성**, 아래로 스크롤하여 클릭 **수신측**합니다. 

7.  선택 내용을 **값** 됩니다 **Enabled**합니다. 

8.  **확인**을 클릭합니다.
  
> [!NOTE]
> 에 **고급** 탭 일부 네트워크 어댑터는 어댑터에서 지원 되는 RSS 큐 수도 표시 합니다.

---

### <a name="windows-powershell"></a>Windows PowerShell

Windows PowerShell을 사용 하 여 vRSS를 사용 하도록 설정 하려면 다음 절차를 따르십시오.

1. 가상 컴퓨터에서 엽니다 **Windows PowerShell**합니다.

2. 바꾸는 확인 하 고 다음 명령을 입력 합니다 *AdapterName* 에 대 한 값을 **-이름** 매개 변수를 구성 하 고 enter 키를 눌러 네트워크 어댑터의 이름. 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >또는 vRSS를 사용 하도록 설정 하려면 다음 명령을 사용할 수 있습니다.
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

자세한 내용은 [RSS 및 vRSS Windows PowerShell 명령](vrss-wps.md)입니다.

---