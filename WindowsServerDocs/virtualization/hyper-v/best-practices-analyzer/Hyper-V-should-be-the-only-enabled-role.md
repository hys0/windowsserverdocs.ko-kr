---
title: Hyper-v 역할만 사용 하도록 설정된 해야 합니다.
description: 이 모범 사례 분석기 규칙에서 보고 한 문제를 해결 하는 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5a0ed176-048f-40b1-b56c-8391b805fd37
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 40dae4baad782d3be4fc6ca8ba2bc4e506131dbf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861916"
---
# <a name="hyper-v-should-be-the-only-enabled-role"></a>Hyper-v 역할만 사용 하도록 설정된 해야 합니다.

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
  
*Hyper-v 이외의 역할은이 서버에서 사용 하도록 설정 됩니다.*  
  
대부분의 경우에서 그 않습니다 Hyper-v 역할을 실행 하는 서버에 다른 역할을 설치 하는 것이 좋습니다. 원격 데스크톱 가상화 호스트 역할 서비스는, 원격 데스크톱 서비스 역할의 일부 이며 동일한 서버에 설치할 Hyper-v가 필요 합니다.  
  
## <a name="impact"></a>영향  
  
*Hyper-v 역할은 서버에서 사용할 수 있는 유일한 역할 이어야 합니다.*  
  
이 모범 사례는 호스트 운영 체제 역할, 기능 및 Hyper-v를 실행 하는 데 필요한 아닌 애플리케이션의 무료 보호할 수 있습니다. Nano 서버에 Hyper-v를 실행 하 고이 최상의 방법에 Nano 서버 Hyper-v 서비스 구성 요소 및 Windows 하이퍼바이저 들어 있기 때문에 소프트웨어 업데이트를 적용 해야 하는 업데이트의 수를 줄일 수 있습니다.  
  
## <a name="resolution"></a>해상도  
  
*서버 관리자를 사용 하 여 Hyper-v를 제외한 모든 역할을 제거 합니다.*  
  
서버 관리자 역할 제거 마법사를 포함 합니다. 이 마법사를 사용 하면 한 번에 둘 이상의 역할을 제거할 수 있습니다. 역할 제거 마법사 역할을 제거 하기 전에 다른 역할을 사용 하는 소프트웨어를 제거할 경우의 위험을 줄이려면 종속성 확인 합니다. 종속성이 발견 되 면 마법사는 다른 역할, 역할 서비스 또는 설치 된 역할에 필요한 소프트웨어의 제거를 승인 하 라는 메시지가 표시 됩니다.   
  
서버 관리자를 사용 하려면 있습니다 로그온 해야 하는 컴퓨터에 관리자 권한으로 합니다.  
  
#### <a name="to-remove-a-role"></a>역할을 제거 하려면  
  
1.  바로 가기 키를 사용 하 여 서버 관리자를 열고는 **시작** 메뉴, Windows 작업 표시줄에서 또는 관리 도구에서입니다.  
2.   에 **역할 요약** 서버 관리자 주 창의 영역 클릭 **역할 제거**합니다. 역할 제거 마법사의 지침을 따릅니다.   
  
  
  


