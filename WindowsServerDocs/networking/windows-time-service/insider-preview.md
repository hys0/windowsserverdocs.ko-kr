---
ms.assetid: ''
title: Windows Server 2019의 Windows 시간 서비스 기능에 대 한 Insider preview
description: Windows Server 2019의 새로운 Windows 시간 서비스 기능
author: shortpatti
ms.author: pashort
ms.date: 09/05/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 38682afa37a4c6882ee2e63a4abf4cd9fdbd2b27
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405215"
---
# <a name="insider-preview"></a>Insider Preview 


## <a name="leap-second-support"></a>Leap second 지원


>적용 대상: Windows Server 2019 및 Windows 10, 버전 1809

초당 1 초의 UTC로 조정 되는 시간입니다. 지구 회전이 느려지는 대로 [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (원자 단위)는 [달라 지므로, astronomical 시간에서 시작 됩니다](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) .  UTC가 최대 .9 초에 달라져서 되 면 [1](https://en.wikipedia.org/wiki/Leap_second) 초를 삽입 하 여 utc 동기화를 평균 양력 시간으로 유지 합니다.

윤 초는 미국 및 유럽 연합 모두에서 정확성 및 추적 가능성 규정 요구 사항을 충족 하는 데 중요 합니다.

자세한 내용은 다음을 참조하세요.

-  [발표 블로그](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  [개발자](https://aka.ms/Dev-LeapSecond) 를 위한 유효성 검사 가이드

-  [IT 전문가](https://aka.ms/ITPro-LeapSecond) 를 위한 유효성 검사 가이드


## <a name="precision-time-protocol"></a>전체 자릿수 시간 프로토콜

>적용 대상: Windows Server 2019 및 Windows 10, 버전 1809

Windows Server 2019 및 Windows 10 (버전 1809)에 포함 된 새 시간 공급자를 사용 하면 PTP (Precision Time Protocol)를 사용 하 여 시간을 동기화 할 수 있습니다. 네트워크를 통해 시간이 분산 되 면 지연 (대기 시간)이 발생 하 고이에 대해 고려 되지 않거나 대칭이 아닌 경우 시간 서버에서 전송 된 타임 스탬프를 이해 하기가 더 어려워집니다. PTP를 사용 하면 네트워크 장치에서 각 네트워크 장치에 도입 된 대기 시간을 시간 측정에 추가 하 여 windows 클라이언트에 훨씬 더 정확한 시간 샘플을 제공할 수 있습니다.

자세한 내용은 다음을 참조하세요.

-  [발표 블로그](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  [IT 전문가](https://aka.ms/PTPValidation) 를 위한 유효성 검사 가이드


## <a name="software-timestamping"></a>소프트웨어 타임 스탬프

>적용 대상: Windows Server 2019 및 Windows 10, 버전 1809

시간 서버에서 네트워크를 통해 타이밍 패킷을 수신 하는 경우에는 시간 서비스에서 사용 되기 전에 운영 체제의 네트워킹 스택에서 처리 해야 합니다. 네트워킹 스택의 각 구성 요소에는 시간 측정의 정확도에 영향을 주는 가변 지연 시간이 도입 되었습니다.

![소프트웨어 타임 스탬프](../media/Windows-Time-Service/software-timestamping.png)

이 문제를 해결 하기 위해 소프트웨어 타임 스탬프를 사용 하면 위에 표시 된 "Windows 네트워킹 구성 요소" 전후에 타임 스탬프 패킷을 사용 하 여 운영 체제의 지연 시간을 파악할 수 있습니다.

자세한 내용은 다음을 참조하세요.

-  [발표 블로그](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  [IT 전문가](https://github.com/Microsoft/SDN/blob/master/FeatureGuide/Validation%20Guide%20-%20RS5%20-%20Software%20Timestamping.docx) 를 위한 유효성 검사 가이드



---