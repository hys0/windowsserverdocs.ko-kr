---
title: 동적 메모리는 사용할 수 있지만 일부 가상 컴퓨터에 응답 하지 않습니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 91b7f50f-a071-4ab6-beb1-1b29f92f52b6
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 98bf61e6e132db8c8a16bf719410aefb433a1d99
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861986"
---
# <a name="dynamic-memory-is-enabled-but-not-responding-on-some-virtual-machines"></a>동적 메모리는 사용할 수 있지만 일부 가상 컴퓨터에 응답 하지 않습니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*게스트 운영 체제에서 동적 메모리 하는 데 필요한 드라이버에서 하나 이상의 가상 컴퓨터에 문제가 발생 했습니다.*  
  
## <a name="impact"></a>영향  
*Hyper-v에서 메모리를 동적으로 조정 하 여 메모리 수요 변화에 대응할 수 없기 때문에 다음 가상 컴퓨터의 게스트 운영 체제가 실행 되지 않거나 불안정을 실행할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*가상 컴퓨터를 부팅 하는 경우 예상 되는 동작입니다. 가상 컴퓨터가 부팅 되지 않는 경우 integration services를 최신 버전으로 업그레이드 하 고 게스트 운영 체제에서 동적 메모리을 지원 하는지 확인 합니다.*  
  
Windows Server 2016 년 통합 서비스는 Windows Update를 통해 전달 됩니다. 가상 컴퓨터 통합 서비스의 최신 버전 가져오기에 대 한 업데이트를 수신 하도록 구성 되었는지 확인 합니다.  
  
동적 메모리 지원 되는 게스트의 특정 버전에서 작동합니다. 참조 [Hyper-v 동적 메모리 개요](https://technet.microsoft.com/library/hh831766.aspx) Windows 10 및 Windows Server 2016 보다 오래 된 버전입니다.  
  


