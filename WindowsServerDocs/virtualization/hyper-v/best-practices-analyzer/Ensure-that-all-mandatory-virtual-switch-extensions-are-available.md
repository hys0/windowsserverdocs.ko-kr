---
title: 필수 가상 스위치 확장을 모두 사용할 수 있는지 확인
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 14c9fc31521a7d4f5e0eed821c0cc49dcfe74e69
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861936"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>필수 가상 스위치 확장을 모두 사용할 수 있는지 확인

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
*하나 이상의 가상 네트워크 어댑터가 사용 하지 않도록 설정 되었거나 설치 되지 않은 필수 확장의 가상 스위치에 연결 되어 있습니다.*  
  
## <a name="impact"></a>영향  
*다음 가상 컴퓨터의 가상 네트워크 어댑터 중 하나 이상에서 네트워크 트래픽이 차단 되었습니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*먼저 필수 확장이 호스트에 설치 되어 있는지 확인 하 고 필요한 경우 확장을 설치 합니다. 그런 다음 필수 확장이 사용 하지 않도록 설정 된 경우 가상 스위치 관리자 또는 Windows PowerShell cmdlet VMSwitchExtension를 사용 하 여 확장을 사용 하도록 설정 합니다.*  
  


