---
title: 복제에 대 한 인증서 기반 인증 것이 좋습니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d931cc57-414f-4bdf-9ebd-08fd5e22b19d
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: c5e356792ba93d21d9ce130a46e1d60336c99844
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857676"
---
# <a name="certificate-based-authentication-is-recommended-for-replication"></a>복제에 대 한 인증서 기반 인증 것이 좋습니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>**문제**  
*복제용으로 선택 된 하나 이상의 가상 컴퓨터가 Kerberos 인증에 대해 구성 되어 있습니다.*  
  
## <a name="impact"></a>**식**  
*주 서버에서 복제 서버로의 복제 네트워크 트래픽이 암호화 되지 않았습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*다른 방법을 사용 하 여 암호화를 수행 하는 경우이를 무시할 수 있습니다. 그렇지 않으면 가상 컴퓨터 설정을 수정 하 여 인증서 기반 인증을 선택 합니다.*  
  


