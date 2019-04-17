---
title: VRSS 가상 네트워크 어댑터에서 사용 하도록 설정
description: 이 항목에서는 장치 관리자 또는 Windows PowerShell을 사용 하 여 Windows Server의 vRSS를 사용 하는 방법을 알아봅니다.
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133419"
---
# VRSS 가상 네트워크 어댑터에서 사용 하도록 설정

>적용 대상: Windows Server(반기 채널), Windows Server 2016

가상 RSS \(vRSS\) 실제 어댑터에서 가상 컴퓨터 큐 \(VMQ\) 지원 해야 합니다. VMQ 사용 되지 않거나 지원 되지 않습니다 다음 가상 수신측 배율 비활성화 됩니다. 

자세한 내용은 [vRSS 사용 계획](vrss-plan.md)을 참조 하세요.

## VM에서 vRSS를 사용 하도록 설정
 
Windows PowerShell 또는 장치 관리자를 사용 하 여 vRSS를 사용 하도록 설정 하려면 다음 절차를 사용 합니다.

-   장치 관리자
-   Windows PowerShell
  
### 장치 관리자

장치 관리자를 사용 하 여 vRSS 수 있도록이 절차를 사용할 수 있습니다.

>[!NOTE]
>이 절차의 첫 번째 단계는 Windows 10 또는 Windows Server 2016을 실행 중인 Vm에 특정 합니다. VM에서 다른 운영 체제를 실행 중인 경우 먼저 제어판을 열고, 다음 찾아서 장치 관리자 장치 관리자를 열 수 있습니다.
  
1.  VM 작업 표시줄에서 **검색 유형 여기** **장치**를 입력 합니다. 

2.  검색 결과에서 **장치 관리자**를 클릭 합니다.

3.  장치 관리자에서 클릭 하 여 **네트워크 어댑터**를 확장 합니다. 

4.  구성 하려는 네트워크 어댑터를 마우스 오른쪽 단추로 클릭 하 고 **속성**을 클릭 합니다.<p>네트워크 어댑터 **속성** 대화 상자가 열립니다.

5.  네트워크 어댑터 **속성**에서 **고급** 탭을 클릭 합니다. 

6.  **속성**아래로 스크롤한 **수신측 배율**을 클릭 합니다. 

7.  **값** 에서 선택을 **사용할 수**있는지 확인 합니다. 

8.  **확인**을 클릭합니다.
  
> [!NOTE]
> **고급** 탭의 일부 네트워크 어댑터도 어댑터에서 지 원하는 RSS 큐 수를 표시 합니다.

---

### Windows PowerShell

Windows PowerShell을 사용 하 여 vRSS를 사용 하려면 다음 절차를 사용 합니다.

1. 가상 컴퓨터에서 **Windows PowerShell**을 엽니다.

2. 바꾸면 *AdapterName* 값을 확인 하 고 다음 명령을 입력 합니다 **-이름** 매개 변수를 구성 하 고 enter 하려는 네트워크 어댑터의 이름입니다. 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >또는 vRSS를 사용 하도록 설정 하려면 다음 명령을 사용할 수 있습니다.
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

자세한 내용은 [Windows PowerShell 명령 RSS 및 vRSS를](vrss-wps.md)참조 하세요.

---