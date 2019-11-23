---
title: Windows Vista를 실행 하 고 동적 메모리를 사용 하 여 구성 하는 가상 컴퓨터 메모리 설정에 대 한 권장된 값을 사용 해야
description: 이 모범 사례 분석기 규칙에서 보고 한 문제를 해결 하는 지침을 제공 합니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c35f08b2-e624-4811-a159-c1e5bb6d5281
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0a9ce14c31d2ea6e26b03d5c430a428474255b84
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366581"
---
# <a name="a-virtual-machine-running-windows-vista-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Windows Vista를 실행 하 고 동적 메모리를 사용 하 여 구성 하는 가상 컴퓨터 메모리 설정에 대 한 권장된 값을 사용 해야

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*하나 이상의 가상 컴퓨터는 Windows Vista에 권장 되는 메모리 용량 보다 더 작은 동적 메모리를 사용 하도록 구성 되어 있습니다.*  
  
### <a name="impact"></a>영향  
*다음 가상 컴퓨터의 게스트 운영 체제가 실행 되지 않거나 불안정을 실행할 수 있습니다.*  
  
가상 컴퓨터 \<목록 >  
      
## <a name="resolution"></a>해결 방법  
*Hyper-v 관리자 또는 Windows PowerShell을 사용 하 여 최소 메모리를 256 MB 이상, 시작 메모리를 최소 512 MB 이상, 최대 메모리를 1gb 이상으로 늘립니다.*  
  
#### <a name="increase-memory-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 메모리 확보  
  
1.  Hyper-V 관리자를 엽니다. (서버 관리자에서 클릭 **도구** > **Hyper-v 관리자**.)  
  
2.  가상 컴퓨터의 목록에서 마우스 오른쪽 단추로 입력 한 후 클릭 **설정을**합니다.  
  
3.  탐색 창에서 **메모리**합니다.  
  
4.  변경 된 **RAM** 최소 512 MB 이상에 있습니다.  
  
5.  아래에서 **동적 메모리**,  변경의 **최소 RAM** 256mb 이상 및 **최대 RAM** 1gb로 줄어듭니다.  
  
6.  **확인**을 클릭합니다.  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 메모리 확보  
  
1.  Windows PowerShell을 엽니다. (바탕 화면에서 클릭 **시작** 입력을 시작 하 고 **Windows PowerShell**.)  
  
2.  마우스 오른쪽 단추로 클릭 **Windows PowerShell** 클릭 **관리자 권한으로 실행**합니다.  
  
3.  다음과 비슷한 명령을 실행을 MyVM 메모리 및 가상 컴퓨터의 이름으로 바꾸고 값으로 적어도 아래 표시 된 값.  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 1GB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


