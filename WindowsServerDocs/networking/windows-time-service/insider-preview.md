---
title: Windows Server 2019의 Windows 시간 서비스 기능에 대한 참가자 미리 보기
description: Windows Server 2019의 새로운 Windows 시간 서비스 기능
author: dcuomo
ms.author: dacuo
ms.date: 06/06/2020
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: b96da79679e7ee56067d49e74adead80804705fe
ms.sourcegitcommit: 8b4876ece80c8ab267eb1fbf2f6fa255bcf77cb7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454296"
---
# <a name="insider-preview"></a>참가자 미리 보기


## <a name="leap-second-support"></a>윤초 지원

> 적용 대상: Windows Server 2019 및 Windows 10, 버전 1809

윤초는 특별한 경우에 가감하는 UTC에 대한 1초 조정입니다. 지구의 자전 속도가 느려지므로 [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time)(원자성 시간 표시줄)는 [평균 양력 시간](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) 또는 천문학적 시간에서 분기됩니다. UTC가 최대 .9초에서 분기되면 UTC가 평균 양력 시간과 동기화되도록 유지하기 위해 [윤초](https://en.wikipedia.org/wiki/Leap_second)가 삽입됩니다.

윤초는 미국 및 유럽 연합 모두에서 정확성 및 추적 가능성 규정 요구 사항을 충족하는 데 중요합니다.

자세한 내용은 다음을 참조하세요.

- [공지 블로그](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [개발자](https://aka.ms/Dev-LeapSecond)를 위한 유효성 검사 가이드

- [IT 전문가](https://aka.ms/ITPro-LeapSecond)를 위한 유효성 검사 가이드


## <a name="precision-time-protocol"></a>정밀도 시간 프로토콜

> 적용 대상: Windows Server 2019 및 Windows 10, 버전 1809

Windows Server 2019 및 Windows 10(버전 1809)에 포함된 새 시간 공급자를 사용하면 PTP(Precision Time Protocol)를 사용하여 시간을 동기화할 수 있습니다. 네트워크를 통해 시간이 분산되면 지연(대기 시간)이 발생하고 이에 대해 고려되지 않거나 대칭이 아닌 경우 시간 서버에서 전송된 타임스탬프를 이해하기가 더 어려워집니다. PTP를 사용하면 네트워크 디바이스에서 각 네트워크 디바이스에 도입된 대기 시간을 시간 측정에 추가하여 windows 클라이언트에 훨씬 더 정확한 시간 샘플을 제공할 수 있습니다.

자세한 내용은 다음을 참조하세요.

- [공지 블로그](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [IT 전문가](https://aka.ms/PTPValidation)를 위한 유효성 검사 가이드


## <a name="software-timestamping"></a>소프트웨어 타임스탬프

> 적용 대상: Windows Server 2019 및 Windows 10, 버전 1809

시간 서버에서 네트워크를 통해 타이밍 패킷을 수신하는 경우에는 시간 서비스에서 사용되기 전에 운영 체제의 네트워킹 스택에서 처리되어야 합니다. 네트워킹 스택의 각 구성 요소에는 시간 측정의 정확도에 영향을 주는 가변 지연 시간이 도입되었습니다.

![소프트웨어 타임스탬프](../media/Windows-Time-Service/software-timestamping.png)

이 문제를 해결하기 위해 소프트웨어 타임스탬프를 사용하면 위에 표시된 "Windows 네트워킹 구성 요소" 전후에 타임스탬프 패킷을 사용하여 운영 체제의 지연 시간을 파악할 수 있습니다.

자세한 내용은 다음을 참조하세요.

- [공지 블로그](https://techcommunity.microsoft.com/t5/networking-blog/top-10-networking-features-in-windows-server-2019-10-accurate/ba-p/339739/)

- [개발자와 IT 전문가를 위한 유효성 검사 가이드](https://github.com/microsoft/W32Time/tree/master/Leap%20Seconds)


---
