---
title: 지원 되는 최대 사용의 논리적 프로세서 수가 초과할 수 없습니다.
description: 이 모범 사례 분석기 규칙에서 보고 한 문제를 해결 하는 지침을 제공 합니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 66df8b02-91d1-424b-8934-a39c214d530e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b6cd948c47e58dec919cd946ad701f70403d6af3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859296"
---
# <a name="the-number-of-logical-processors-in-use-must-not-exceed-the-supported-maximum"></a>지원 되는 최대 사용의 논리적 프로세서 수가 초과할 수 없습니다.

>적용 대상: Windows Server 2016

모범 사례 및 검사에 대한 자세한 내용은 [모범 사례 분석기](https://go.microsoft.com/fwlink/?LinkId=122786)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|오류|  
|**범주**|정책|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 나타나는 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
  
*서버가 너무 많은 논리적 프로세서로 구성 되었습니다.*  
  
## <a name="impact"></a>영향  
  
*Microsoft는이 컴퓨터에서 Hyper-v 실행을 지원 하지 않습니다.*  
  
## <a name="resolution"></a>해상도  
  
*이 컴퓨터에서 일부 프로세서를 제거 하거나 msconfig를 사용 하 여 사용 가능한 프로세서 수를 제한 하십시오.*  
  
Msconfig를 사용 하려면 다음 지침을 참조 하십시오. 프로세서를 제거 하는 방법에 대 한 자세한 컴퓨터와 함께 제공 된 지침을 참조 하거나 하드웨어 제조업체에 문의 합니다. Hyper-v에 대 한 지원 되는 최대 구성에 대 한 자세한 참조 [Windows Server 2016의 Hyper-v 확장성에 대 한 계획](../plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)합니다.  
  
### <a name="to-limit-the-number-of-available-processors"></a>사용 가능한 프로세서의 수를 제한 하려면  
  
1.  시스템을 열고 구성 응용 프로그램 (Msconfig.exe). 이 작업을 수행 하려면 **시작**, 형식 **msconfig**, 를 마우스 오른쪽 단추로 클릭는 **시스템 구성** 데스크톱 응용 프로그램을 클릭 **관리자 권한으로 실행**합니다.  
  
2.  **부팅** 탭을 클릭 하 여 **고급 옵션**합니다.  
  
3.  선택 **프로세서 수가** 한 다음 목록에 숫자를 선택 합니다. **확인**을 클릭합니다.  
  
4.  새 프로세서 수를 사용 하 여 실행 하도록 컴퓨터를 다시 시작 합니다.  
  


