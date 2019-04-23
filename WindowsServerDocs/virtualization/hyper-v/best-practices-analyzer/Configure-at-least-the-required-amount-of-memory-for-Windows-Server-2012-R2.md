---
title: 최소한 필요한 가상 컴퓨터의 Windows Server 2012 r 2를 실행 하 고 동적 메모리에 사용할 수 있는 메모리 양을 구성합니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a0e69661-6a1d-4b31-b727-f2429f3977d0
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4af27b8ba626abaadb3ebadf7060ddfb1f145d5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881294"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-server-2012-r2-and-enabled-for-dynamic-memory"></a>최소한 필요한 가상 컴퓨터의 Windows Server 2012 r 2를 실행 하 고 동적 메모리에 사용할 수 있는 메모리 양을 구성합니다

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|Error|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제점**  
*하나 이상의 가상 컴퓨터는 Windows Server 2012 R2에 필요한 메모리 용량 보다 더 적은 노력으로 동적 메모리를 사용 하도록 구성 됩니다.*  
  
## <a name="impact"></a>**Impact**  
*다음 가상 머신에서 게스트 운영 체제 실행 되지 않거나 불안정 실행 될 수 있습니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Hyper-v 관리자를 사용 하 여 시작 메모리 256MB 이상 하는 최소 메모리 및 최소 512 MB 이상이 가상 머신에 대 한 최대 메모리를 늘립니다.*  
  
### <a name="increase-memory-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 메모리 확보  
  
1.  Hyper-V 관리자를 엽니다. (서버 관리자에서 클릭 **도구** > **Hyper-v 관리자**.)  
  
2.  가상 컴퓨터의 목록에서 마우스 오른쪽 단추로 입력 한 후 클릭 **설정을**합니다.  
  
3.  탐색 창에서 **메모리**합니다.  
  
4.  변경 된 **RAM** 최소 512 MB 이상에 있습니다.  
  
5.  **동적 메모리**,  변경 된 **최소 RAM** 256mb 이상 및 **최대 RAM** 512MB로 합니다.  
  
6.  **확인**을 클릭합니다.  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 메모리 확보  
  
1.  Windows PowerShell을 엽니다. (바탕 화면에서 클릭 **시작** 입력을 시작 하 고 **Windows PowerShell**.)  
  
2.  마우스 오른쪽 단추로 클릭 **Windows PowerShell** 클릭 **관리자 권한으로 실행**합니다.  
  
3.  다음과 비슷한 명령을 실행을 MyVM 메모리 및 가상 컴퓨터의 이름으로 바꾸고 값으로 적어도 아래 표시 된 값.  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


