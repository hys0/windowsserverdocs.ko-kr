---
title: 페이징 파일을 사용 하는 가상 하드 디스크 복제에서 제외 되어야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c0be8a5f-64a1-488a-944e-bb913bb90517
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 94e03cf9de3991d003fad9019b9af33fad2f6bae
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855026"
---
# <a name="virtual-hard-disks-with-paging-files-should-be-excluded-from-replication"></a>페이징 파일을 사용 하는 가상 하드 디스크 복제에서 제외 되어야 합니다.

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|정보|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*페이징 파일은 복제에 참여 하지 않도록 제외 되어야 하지만 제외 된 디스크가 없습니다.*  
  
## <a name="impact"></a>영향  
*페이징 파일은 많은 양의 입/출력 작업을 경험 하므로 복제에 참여 하는 데 불필요 하 게 많은 리소스가 필요 합니다. 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*아직 수행 하지 않은 경우 Windows 페이징 파일에 대 한 별도의 가상 하드 디스크를 만듭니다. 초기 복제가 이미 완료 된 경우 Hyper-v 관리자를 사용 하 여 복제를 제거 합니다. 그런 다음 복제를 다시 구성 하 고, 복제에서 페이징 파일을 사용 하 여 가상 하드 디스크를 제외 합니다.*  
  


