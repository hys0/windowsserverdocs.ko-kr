---
title: 시스템 디스크에 있는 스마트 페이징 파일을 저장 하지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9b57c9b8-76c5-43c7-bfa6-2c95b3cb6510
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6abc84b406de7e7c33628ccee4e3af706efe5c70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886174"
---
# <a name="avoid-storing-smart-paging-files-on-a-system-disk"></a>시스템 디스크에 있는 스마트 페이징 파일을 저장 하지

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 나타나는 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제점  
*하나 이상의 가상 컴퓨터에 대 한 메모리 구성을 가상 컴퓨터를 다시 부팅 하 고 지정 된 위치에 스마트 페이징 파일에 대 한 Hyper-v를 실행 하는 서버 시스템 디스크 스마트 페이징 사용을 해야 합니다.*  
  
## <a name="impact"></a>영향  
*시스템 디스크 스마트 페이징 사용 문제를 경험 하기 위해 Hyper-v를 실행 하는 서버에 발생할 수 있습니다. 이 가상 컴퓨터에 영향을 줍니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>해결 방법  
*비-시스템 디스크에 스마트 페이징 파일을 저장 하려면 가상 컴퓨터를 다시 구성 합니다.*  
  


