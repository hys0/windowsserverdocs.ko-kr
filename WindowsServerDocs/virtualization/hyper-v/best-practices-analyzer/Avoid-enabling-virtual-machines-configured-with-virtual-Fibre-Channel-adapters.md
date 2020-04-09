---
title: 원본에 대해 보다 대상에 파이버 채널 논리 단위 (Lun)에 더 적은 경로가 있으면 실시간 마이그레이션을 허용 하도록 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 사용 하지 않습니다
description: 이 모범 사례 분석기 규칙에 대 한 텍스트의 온라인 버전입니다.
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7989d2e1908f6be32f4661900fc507b5843b55c9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857776"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>원본에 대해 보다 대상에 파이버 채널 논리 단위 (Lun)에 더 적은 경로가 있으면 실시간 마이그레이션을 허용 하도록 가상 파이버 채널 어댑터를 사용 하 여 구성 하는 가상 컴퓨터를 사용 하지 않습니다

>적용 대상: Windows Server 2016

모범 사례 분석기 및 검사에 대한 자세한 내용은 [모범 사례 분석기 검사 실행 및 검사 결과 관리](https://go.microsoft.com/fwlink/p/?LinkID=223177)를 참조하세요.  
  
|속성|세부 정보|  
|-|-|  
|**운영 체제**|Windows Server 2016|  
|**제품/기능**|Hyper-V|  
|**등급**|경고|  
|**범주**|구성|

다음 섹션에서는 기울임꼴이이 문제에 대 한 모범 사례 분석기 도구에 표시 되는 UI 텍스트를 나타냅니다.
  
## <a name="issue"></a>**문제**  
*하나 이상의 가상 컴퓨터에는 가상화 WMI 공급자에 설정 된 AllowReducedFcRedunancy 속성이 있습니다.*  
  
## <a name="impact"></a>**식**  
*다음 가상 컴퓨터의 실시간 마이그레이션으로 인해 데이터가 손실 되거나 저장소에 대 한 i/o가 중단 될 수 있습니다.*  
  
가상 컴퓨터 \<목록 >  
  
## <a name="resolution"></a>**해결 방법**  
*영향을 받는 가상 컴퓨터에서 AllowReducedFcRedundancy WMI 속성을 지우는 것이 좋습니다. 이 속성을 선택 취소 하면 대상의 파이버 채널 경로 수가 원본에 있는 경로 수보다 크거나 같은 경우에만 가상 파이버 채널 어댑터를 사용 하 여 구성 된 가상 컴퓨터에서 실시간 마이그레이션을 수행할 수 있습니다. 이러한 검사는 저장소에 대 한 i/o 중단 또는 데이터 손실을 방지 하는 데 도움이 됩니다.* 