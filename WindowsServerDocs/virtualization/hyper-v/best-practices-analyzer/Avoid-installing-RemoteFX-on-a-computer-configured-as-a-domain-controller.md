---
title: Active Directory 도메인 컨트롤러로 구성 하는 컴퓨터에서 RemoteFX를 설치 하지 않습니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 597dd26d0a317ca026cd94ab29138ce679d7c3b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857766"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Active Directory 도메인 컨트롤러로 구성 하는 컴퓨터에서 RemoteFX를 설치 하지 않습니다

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|오류|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제**  
*RemoteFX가 도메인 컨트롤러에 설치 되어 있습니다.*  
  
## <a name="impact"></a>**식**  
*RemoteFX에 대해 구성 된 가상 컴퓨터는 이러한 컴퓨터에서 사용할 수 없습니다.*  
  
## <a name="resolution"></a>**해결 방법**  
*Hyper-v에 대해 RemoteFX를 사용 하 여이 서버를 구성할 지, 아니면 Active Directory 도메인 컨트롤러로 구성할 것인지 결정 한 다음 필요에 따라 서버를 다시 구성 합니다.*  
  


