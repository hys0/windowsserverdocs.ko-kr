---
title: 부모 및 자식 가상 하드 디스크는 서로 다른 볼륨에 때 차이점 보관용 가상 하드 디스크를 사용 하는 경우 저장소 서비스 품질을 사용 하지 않습니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2bdc8462c4d9dc50dbb69792f2f294add0ca3a74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856204"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>부모 및 자식 가상 하드 디스크는 서로 다른 볼륨에 때 차이점 보관용 가상 하드 디스크를 사용 하는 경우 저장소 서비스 품질을 사용 하지 않습니다

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|설명|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**Severity**|경고|  
|**범주**|Configuration|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제점**  
*부모 및 자식 가상 하드 디스크와 별도 볼륨에 차이점 보관용 가상 하드 디스크에 저장소 서비스 품질 사용할 수 있습니다.*  
  
## <a name="impact"></a>**Impact**  
*이 구성은 예기치 않은 저장소 부모 및 자식 볼륨에 다른 가상 하드 디스크 뿐만 아니라 차이점 보관용 가상 하드 디스크에 대 한 서비스 품질 동작이 발생할 수 있습니다. 다음에 영향을 주는 가상 하드 디스크:*  
  
\<가상 하드 디스크의 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*참조 된 가상 하드 디스크에서 저장소 서비스 품질을 사용 하지 않도록 설정 하거나 동일한 볼륨에 부모 및 자식 가상 하드 디스크를 이동 하는 저장소 마이그레이션 수행 합니다.*  
  


