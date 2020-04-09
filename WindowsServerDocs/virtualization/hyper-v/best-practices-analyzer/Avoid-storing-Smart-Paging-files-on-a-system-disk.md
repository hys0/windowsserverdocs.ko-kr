---
title: 시스템 디스크에 있는 스마트 페이징 파일을 저장 하지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9b57c9b8-76c5-43c7-bfa6-2c95b3cb6510
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 111cf3b3b95f50d6d36a6b30b5a0bb46e255ee28
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857736"
---
# <a name="avoid-storing-smart-paging-files-on-a-system-disk"></a>시스템 디스크에 있는 스마트 페이징 파일을 저장 하지

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 나타나는 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*가상 컴퓨터를 다시 부팅 하 고 스마트 페이징 파일의 지정 된 위치가 Hyper-v를 실행 하는 서버의 시스템 디스크인 경우 하나 이상의 가상 컴퓨터에 대 한 메모리 구성에서 스마트 페이징을 사용 해야 할 수 있습니다.*  
  
## <a name="impact"></a>영향  
*스마트 페이징에 시스템 디스크를 사용 하면 Hyper-v를 실행 하는 서버에서 문제가 발생할 수 있습니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*시스템 디스크가 아닌 디스크에 스마트 페이징 파일을 저장할 가상 컴퓨터를 다시 구성 하십시오.*  
  


