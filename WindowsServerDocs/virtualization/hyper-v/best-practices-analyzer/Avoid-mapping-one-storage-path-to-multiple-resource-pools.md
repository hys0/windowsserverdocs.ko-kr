---
title: 여러 개의 리소스 풀에 하나의 스토리지 경로 매핑 방지
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 24992453-762b-4892-9a50-55d237b9b7f2
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 53ef04a2dde875b26dd109075a2cfa4484ebd5cd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857756"
---
# <a name="avoid-mapping-one-storage-path-to-multiple-resource-pools"></a>여러 개의 리소스 풀에 하나의 스토리지 경로 매핑 방지

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제**  
*저장소 파일 경로는 여러 리소스 풀에 매핑됩니다.*  
  
## <a name="impact"></a>**식**  
*지정 된 저장소 풀 유형에 대해 다음 부모 및 자식 풀이 동일한 저장소 경로를 공유 합니다.*  
  
풀 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*Windows PowerShell을 사용 하 여 여러 풀에서 동일한 저장소 경로를 사용 하지 않도록 저장소 리소스 풀을 다시 구성 합니다.*  
  


