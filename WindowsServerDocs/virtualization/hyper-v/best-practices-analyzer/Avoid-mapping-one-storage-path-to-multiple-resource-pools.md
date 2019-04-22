---
title: 여러 개의 리소스 풀에 하나의 저장소 경로 매핑 방지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 7c012836309f722e55c28b2ddbe3d54de641b4af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823964"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>여러 개의 리소스 풀에 하나의 저장소 경로 매핑 방지

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제점**  
*저장소 파일 경로 여러 개의 리소스 풀에 매핑됩니다.*  
  
## <a name="impact"></a>**Impact**  
*지정 된 저장소 풀 유형에 대 한 다음 부모 및 자식 풀 같은 저장소 경로 공유:*  
  
\<풀 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Windows PowerShell을 사용 하 여 여러 풀 동일한 저장소 경로 사용 하지 마십시오는 저장소 리소스 풀을 다시 구성 합니다.*  
  


