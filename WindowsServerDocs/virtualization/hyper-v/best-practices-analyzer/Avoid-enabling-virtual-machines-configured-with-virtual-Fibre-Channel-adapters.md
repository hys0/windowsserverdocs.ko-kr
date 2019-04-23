---
title: 원본에 대해 보다 대상에 파이버 채널 논리 단위 (Lun)에 더 적은 경로가 있으면 실시간 마이그레이션을 허용 하도록 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 사용 하지 않습니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6ff69d5cb09133a806c2a2df3446713264a4e892
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849554"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>원본에 대해 보다 대상에 파이버 채널 논리 단위 (Lun)에 더 적은 경로가 있으면 실시간 마이그레이션을 허용 하도록 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 사용 하지 않습니다

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
*하나 이상의 가상 컴퓨터는 가상화 WMI 공급자에서 설정 AllowReducedFcRedunancy 속성이 있습니다.*  
  
## <a name="impact"></a>**Impact**  
*다음 가상 머신의 실시간 마이그레이션 데이터가 손실 될 수도 저장소 I/O를 중단 합니다.*  
  
\<가상 머신의 목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*영향을 받는 가상 컴퓨터에 AllowReducedFcRedundancy WMI 속성의 선택을 취소 하는 것이 좋습니다. 이 속성의 선택을 취소 하면 대상에 파이버 채널에 대 한 경로 수는 동일 하거나 보다 많은 수의 원본 경로 하는 경우에 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터에서 실시간 마이그레이션을 수행할 수 있습니다. 이러한 검사 도움말 저장소에 데이터 손실 또는 I/O의 중단을 방지 합니다.* 