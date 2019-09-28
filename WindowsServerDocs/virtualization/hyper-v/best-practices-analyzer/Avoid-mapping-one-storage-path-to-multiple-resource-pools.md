---
title: 여러 개의 리소스 풀에 하나의 저장소 경로 매핑 방지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e89c0382d20d586d8c0b50396ddbd56d6fdadf0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365257"
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
*저장소 파일 경로는 여러 리소스 풀에 매핑됩니다.*  
  
## <a name="impact"></a>**식**  
*지정 된 저장소 풀 유형에 대해 다음 부모 및 자식 풀이 동일한 저장소 경로를 공유 합니다.*  
  
\< 개의 풀 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Windows PowerShell을 사용 하 여 여러 풀에서 동일한 저장소 경로를 사용 하지 않도록 저장소 리소스 풀을 다시 구성 합니다.*  
  


