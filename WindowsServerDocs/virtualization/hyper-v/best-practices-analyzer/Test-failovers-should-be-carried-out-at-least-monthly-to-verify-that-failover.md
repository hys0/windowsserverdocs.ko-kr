---
title: 테스트 장애 조치를 수행 해야 최소한 매월 장애 조치는 성공 하 고 장애 조치 후 예상 되는 가상 컴퓨터 작업으로 작동을 확인 하려면
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 57a8aa50-e59e-4a4b-8571-1099d5a8eee4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f99ccfe065015d1731978ba5e7f31c766c343efc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858936"
---
# <a name="test-failovers-should-be-carried-out-at-least-monthly-to-verify-that-failover-will-succeed-and-that-virtual-machine-workloads-will-operate-as-expected-after-failover"></a>테스트 장애 조치를 수행 해야 최소한 매월 장애 조치는 성공 하 고 장애 조치 후 예상 되는 가상 컴퓨터 작업으로 작동을 확인 하려면

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016| 
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|작업|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*하나 이상의 월에 테스트 장애 조치 (failover)가 없습니다.*  
  
## <a name="impact"></a>영향  
*계획 된 장애 조치 (failover) 또는 계획 되지 않은 장애 조치 (failover)가 성공 하거나 장애 조치 (failover) 후에 워크 로드 작업이 정상적으로 계속 이는 다음과 같은 가상 컴퓨터에 영향을 줍니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>해상도  
*Hyper-v 관리자를 사용 하 여 테스트 장애 조치 (failover)를 수행 합니다.*  
  


