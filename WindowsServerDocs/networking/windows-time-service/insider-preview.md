---
ms.assetid: ''
title: Windows Server 2019에 Windows 시간 서비스 기능에 대 한 참가자 미리 보기
description: Windows Server 2019에 새 Windows 시간 서비스 기능
author: shortpatti
ms.author: pashort
ms.date: 09/05/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: ef0ff317f5957add5ecbe9f88ef83753b805ec41
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829024"
---
# <a name="insider-preview"></a>Insider Preview 


## <a name="leap-second-support"></a>윤 초 지원


>적용 대상: Windows Server 2019 및 Windows 10 버전 1809

윤 초를 가끔 1 초 UTC로 조정 됩니다. 지구 회전 느려지는 대로 [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) (원자 단위 별로)에서 달라 지므로 [양력 표준시](https://en.wikipedia.org/wiki/Solar_time#Mean_solar_time) 또는 천문학 시간입니다.  UTC.9 초 이하의 달라졌는지를 면을 [윤 초](https://en.wikipedia.org/wiki/Leap_second) UTC와 동기화 양력 평균 시간을 유지 하려면 삽입 됩니다.

윤 초 정확도 및 추적 가능성 규정 요구 사항을 모두 미국 및 유럽 연합에서 충족 해야 되 고 있습니다.

참조 항목:

-  우리의 [공지 블로그](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  유효성 검사에 대 한 가이드는 [개발자](https://aka.ms/Dev-LeapSecond)

-  유효성 검사에 대 한 가이드는 [IT 전문가](https://aka.ms/ITPro-LeapSecond)


## <a name="precision-time-protocol"></a>전체 자릿수 시간 프로토콜

>적용 대상: Windows Server 2019 및 Windows 10 버전 1809

Windows Server 2019 및 Windows 10 (버전 1809)에 포함 된 새 시간 공급자를 사용 하면 전체 자릿수 시간 프로토콜 (PTP)를 사용 하 여 시간을 동기화 수 있습니다. 지연 시간 (대기 시간)에 대 한 경우에는 고려 하지 않습니다, 발생 시간 네트워크를 통해 배포 하는 대로 또는 대칭 인 경우 것이 더욱 어려워집니다 시간 서버에서 보낸 시간 타임 스탬프를 알아야 합니다. PTP는 대기 시간이 각 네트워크 장치에서 windows 클라이언트에 훨씬 더 정확한 시간 샘플을 제공 함으로써 타이밍 측정 값에 추가 하려면 네트워크 장치를 수 있습니다.

참조 항목:

-  우리의 [공지 블로그](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  유효성 검사에 대 한 가이드는 [IT 전문가](https://aka.ms/PTPValidation)


## <a name="software-timestamping"></a>소프트웨어 타임 스탬프

>적용 대상: Windows Server 2019 및 Windows 10 버전 1809

시간 서버에서 네트워크를 통해 타이밍 패킷을 수신 하는 경우 이전 시간 서비스에서 사용 중인 운영 체제의 네트워킹 스택에서 처리 되어야 합니다. 네트워킹 스택의 각 구성 요소는 다양 한 크기의 타이밍 측정의 정확도 영향을 주는 대기 시간을 소개 합니다.

![소프트웨어 타임 스탬프](../media/Windows-Time-Service/software-timestamping.png)

이 문제를 해결 하기 위해 소프트웨어 타임 스탬프를 적용 하면 타임 스탬프 패킷에 "Windows 네트워킹 구성 요소" 운영 체제에서 지연 시간을 고려 하려면 위에 표시 된 전후.

참조 항목:

-  우리의 [공지 블로그](https://blogs.technet.microsoft.com/networking/2018/07/18/top10-ws2019-hatime/)

-  유효성 검사에 대 한 가이드는 [IT 전문가](https://github.com/Microsoft/SDN/blob/master/FeatureGuide/Validation%20Guide%20-%20RS5%20-%20Software%20Timestamping.docx)



---