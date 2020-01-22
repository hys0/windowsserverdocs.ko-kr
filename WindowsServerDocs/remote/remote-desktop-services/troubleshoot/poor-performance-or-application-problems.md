---
title: 원격 데스크톱 연결 중 성능 저하 또는 애플리케이션 문제 발생
description: 원격 데스크톱 연결 중에 발생하는 성능 저하 또는 애플리케이션 문제를 해결합니다.
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: bcf2c8163123cbb71162f8ee44d283c532bd01a8
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265925"
---
# <a name="poor-performance-or-application-problems-during-remote-desktop-connection"></a>원격 데스크톱 연결 중 성능 저하 또는 애플리케이션 문제 발생

이 문서에서는 사용자가 원격 데스크톱 기능을 사용할 때 발생할 수 있는 몇 가지 일반적인 문제를 해결합니다.

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>새 Microsoft Azure 가상 머신의 일시적인 문제

이 이슈는 최근에 프로비저닝된 가상 머신에 영향을 줍니다. 사용자가 가상 머신에 연결되면 원격 데스크톱 세션에서 사용자의 설정 일부를 올바르게 로드하지 않습니다.

이 이슈를 해결하려면 가상 머신에서 연결을 끊고, 20분 이상 기다렸다가 다시 연결합니다.

이 이슈를 해결하려면 다음 업데이트를 가상 머신에 적절하게 적용합니다.

  - Windows 10 및 Windows Server 2016: KB 4343884, [2018년 8월 30일 - KB4343884(OS 빌드 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2: KB 4343891, [2018년 8월 30일 - KB4343891(월별 롤업 미리 보기)](https://support.microsoft.com/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Windows 10 버전 1709의 비디오 재생 이슈

이 이슈는 사용자가 Windows 10 버전 1709를 실행하는 원격 컴퓨터에 연결할 때 발생합니다. 이러한 사용자가 VMR9(Video Mixing Renderer 9) 코덱을 사용하여 비디오를 재생하면 플레이어에서 검은색 창만 표시합니다.

이는 Windows 10 버전 1709에서 알려진 이슈입니다. Windows 10 버전 1703에서는 이 문제가 발생하지 않습니다.

### <a name="desktop-sharing-issues-on-windows-10"></a>Windows 10의 데스크톱 공유 이슈

이 이슈는 키오스크 시나리오처럼 사용자가 읽기 전용 사용자 프로필(및 관련된 레지스트리 하이브)을 갖고 있는 경우에 발생합니다. 이러한 사용자가 Windows 10 버전 1803을 실행하는 원격 컴퓨터에 연결되면 자신의 데스크톱을 공유할 수 없습니다.

이 이슈를 해결하려면 Windows 10 업데이트 4340917, [2018년 7월 24일 - KB4340917(OS 빌드 17134.191)](https://support.microsoft.com/help/4340917/windows-10-update-kb4340917)을 적용합니다.

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>NLA를 사용하지 않도록 설정하면 Windows 10 버전을 혼합할 때 성능 이슈 발생

이 문제는 Windows 10을 실행하는 원격 데스크톱 클라이언트 컴퓨터에서 원격 데스크톱(NLA를 사용하지 않도록 설정되어 있는 동안 다른 버전의 Windows 10 실행)에 연결하는 경우에 발생합니다. Windows 10 버전 1709 이하를 실행하는 컴퓨터의 원격 데스크톱 클라이언트 사용자가 Windows 10 버전 1803 이상을 실행하는 원격 데스크톱에 연결하면 성능이 저하됩니다.

NLA를 사용하지 않도록 설정하면 이전 클라이언트 컴퓨터가 Windows 10 버전 1803 이상에 연결할 때 속도가 느린 프로토콜을 사용하므로 이 문제가 발생합니다.

이 이슈를 해결하려면 KB 4340917, [2018년 7월 24일 - KB4340917(OS 빌드 17134.191)](https://support.microsoft.com/help/4340917/windows-10-update-kb4340917)을 적용합니다.

### <a name="black-screen-issue"></a>검은색 화면 이슈

이 이슈는 Windows 8.0, Windows 8.1, Windows 10 RTM 및 Windows Server 2012 R2에서 발생합니다. 사용자는 원격 데스크톱에서 여러 애플리케이션을 시작한 다음, 세션 연결을 종료합니다. 사용자는 정기적으로 원격 데스크톱에 다시 연결하여 애플리케이션과 상호 작용한 다음, 연결을 다시 끊습니다. 어떤 시점에서 사용자가 다시 연결하면 원격 데스크톱 세션에서 검은색 화면만 표시합니다. 세션이 올바르게 다시 표시되도록 하려면 사용자가 원격 컴퓨터의 콘솔 또는 RDSH 서버 콘솔에서 해당 세션을 종료하고 이 세션의 애플리케이션을 중지해야 합니다.

이 이슈를 해결하려면 다음 업데이트를 적절하게 적용합니다.

  - Windows 8 및 Windows Server 2012: KB4103719, [2018년 5월 17일 - KB4103719(월별 롤업 미리 보기)](https://support.microsoft.com/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 및 Windows Server 2012 R2: KB4103724, [2018년 5월 17일 - KB4103724(월별 롤업 미리 보기)](https://support.microsoft.com/help/4103724/windows-81-update-kb4103724) 및 KB 4284863, [2018년 6월 21일 - KB4284863(월별 롤업 미리 보기)](https://support.microsoft.com/help/4284863/windows-81-update-kb4284863)
  - Windows 10: KB4284860, [2018년 6월 12일 - KB4284860(OS 빌드 10240.17889)](https://support.microsoft.com/help/4284860/windows-10-update-kb4284860)에서 수정됨
