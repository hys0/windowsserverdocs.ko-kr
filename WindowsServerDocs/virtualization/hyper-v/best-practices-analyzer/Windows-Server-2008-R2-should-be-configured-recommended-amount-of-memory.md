---
title: 권장된 메모리 양은로 Windows Server 2008 r 2는 구성 해야
description: 이 모범 사례 분석기 규칙에 의해 보고 된 문제를 해결 하려면 지침을 제공 합니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 26872519-ccf0-4757-827f-8df2a7a2b9f9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: a2737ef0001e1859e514f44fccd6d49bd3ae3a48
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865364"
---
# <a name="windows-server-2008-r2-should-be-configured-with-the-recommended-amount-of-memory"></a>권장된 메모리 양은로 Windows Server 2008 r 2는 구성 해야

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
  
*Windows Server 2008 R2를 실행 하는 가상 머신 권장 되는 2GB RAM 용량 보다 더 적은 노력으로 구성 됩니다.*  
  
## <a name="impact"></a>영향  
  
*게스트 운영 체제 및 응용 프로그램 잘 작동 하지 않을 수 있습니다. 메모리가 부족 하 여 한 번에 여러 응용 프로그램을 실행 하려면 아닐 수도 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신 이름 목록 >  
  
## <a name="resolution"></a>해결 방법  
  
*Hyper-v 관리자를 사용 하 여이 가상 머신에 최소 2GB에 할당 된 메모리를 늘리세요.*  
  
### <a name="to-increase-the-memory-using-hyper-v-manager"></a>Hyper-v 관리자를 사용 하 여 메모리를 늘리려면  
  
1.  Hyper-V 관리자를 엽니다. 클릭 **시작**, 가리킨 **관리 도구**, 를 클릭 하 고 **Hyper-v 관리자**합니다.  
  
2.  결과 창에서 아래 **가상 컴퓨터**, 구성 하려는 가상 컴퓨터를 선택 합니다. 으로 가상 컴퓨터의 상태를 표시 해야 **오프**합니다. 그렇지 않은 경우 가상 컴퓨터를 마우스 오른쪽 단추로 클릭 하 고 클릭 한 다음 **종료**합니다.  
  
3.  **작업** 창의 가상 컴퓨터 이름에서 **설정**을 클릭합니다.  
  
4.  탐색 창에서 **메모리**합니다.  
  
5.  에 **메모리** 페이지에서 설정 된 **시작 RAM** 최소 2GB를 클릭 한 다음 **확인**합니다.  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Windows PowerShell을 사용 하 여 메모리 확보  
  
1.  Windows PowerShell을 엽니다. (바탕 화면에서 클릭 **시작** 입력을 시작 하 고 **Windows PowerShell**.)  
  
2.  마우스 오른쪽 단추로 클릭 **Windows PowerShell** 클릭 **관리자 권한으로 실행**합니다.  
  
3.  이 명령을 실행 하는 교체 후 \<MyVM > 가상 컴퓨터의 이름으로:  
  
```  
Set-VMMemory <MyVM> -StartupBytes 2GB  
```  
  
## <a name="see-also"></a>관련 항목  
[Set-VMMemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


