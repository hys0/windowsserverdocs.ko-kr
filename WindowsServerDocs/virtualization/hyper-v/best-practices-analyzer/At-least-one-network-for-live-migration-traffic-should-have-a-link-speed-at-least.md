---
title: 실시간 마이그레이션 트래픽에 대 한 하나 이상의 네트워크 이상 1gbps의 링크 속도 있어야 합니다.
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 04ce4ea86e39e8bd98216ae4e6b12899c9366421
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857826"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>실시간 마이그레이션 트래픽에 대 한 하나 이상의 네트워크 이상 1gbps의 링크 속도 있어야 합니다.

>적용 대상: Windows Server 2016


  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|오류|  
|**범주**|구성|  
  
다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.  
  
## <a name="issue"></a>문제  
*실시간 마이그레이션 트래픽에 대 한 네트워크 중 최소 1Gbps의 링크 속도를 갖지 않습니다.*  
  
## <a name="impact"></a>영향  
*실시간 마이그레이션은 느리게 발생할 수 있으며 TCP 연결 시간 제한으로 인해 네트워크 연결이 끊어질 수 있습니다.*  
  
## <a name="resolution"></a>해상도  
*속도가 1Gbps 이상인 실시간 마이그레이션 네트워크를 하나 이상 구성 합니다.*  
  
알아보려면 경우 적어도 1gbps의 연결 속도 지원할 수 기존 네트워크 어댑터 네트워크 하드웨어 공급 업체의 설명서를 참조 합니다.  
  


