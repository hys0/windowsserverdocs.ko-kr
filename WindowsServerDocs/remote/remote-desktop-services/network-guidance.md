---
title: 네트워크 지침
description: 원격 데스크톱 배포에 대한 대역폭 추천 사항입니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 12/12/2019
ms.tgt_pltfrm: na
ms.topic: article
author: Heidilohr
manager: lizross
ms.openlocfilehash: 4e3a9bb66389c00bbac04db34d5d2a5b1d1933e1
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919915"
---
# <a name="network-guidance"></a>네트워크 지침

원격 Windows 세션을 사용하는 경우 네트워크의 사용 가능한 대역폭이 환경의 품질에 큰 영향을 줍니다. 애플리케이션과 디스플레이 해상도가 다르면 다른 네트워크 구성이 필요하므로 네트워크를 요구 사항에 맞게 구성해야 합니다.

>[!NOTE]
>다음 추천 사항은 손실이 0.1% 미만인 네트워크에 적용됩니다. 이러한 추천 사항은 VM(가상 머신)에서 호스팅하는 세션의 수에 관계없이 적용됩니다.

## <a name="applications"></a>애플리케이션

다음 표에는 원활한 사용자 환경에 추천되는 최소 대역폭이 나와 있습니다. 이러한 추천 사항은 [원격 데스크톱 워크로드](remote-desktop-workloads.md)의 지침을 기반으로 합니다.

| 워크로드 유형   | 추천 대역폭 |
|-----------------|-----------------------|
| Light           | 1.5Mbps              |
| 보통          | 3Mbps                |
| Heavy           | 5Mbps                |
| 고급           | 15Mbps               |

네트워크에 가해지는 스트레스는 앱 워크로드의 출력 프레임 속도와 디스플레이 해상도에 따라 달라집니다. 프레임 속도 또는 디스플레이 해상도가 증가하면 대역폭 요구 사항도 증가합니다. 예를 들어 고해상도 디스플레이가 있는 경량 워크로드에는 사용 가능한 대역폭이 일반 해상도 또는 저해상도인 경량 워크로드보다 더 많이 필요합니다.

다음과 같은 다른 시나리오의 대역폭 요구 사항은 사용하는 방법에 따라 달라질 수 있습니다.

- 음성 또는 화상 회의
- 실시간 통신
- 4K 비디오 스트리밍

Login VSI와 같은 시뮬레이션 도구를 사용하여 배포에서 이러한 시나리오를 부하 테스트해야 합니다. 네트워크 요구 사항을 더 잘 이해하려면 원격 세션에서 부하 크기를 변경하고, 스트레스 테스트를 실행하고, 일반적인 사용자 시나리오를 테스트합니다.

## <a name="display-resolutions"></a>디스플레이 해상도

다른 디스플레이 해상도를 사용하려면 다른 사용 가능한 대역폭이 필요합니다. 다음 표에는 프레임 속도가 30fps(초당 프레임)인 일반적인 디스플레이 해상도에서 원활한 사용자 환경에 추천되는 대역폭이 나와 있습니다. 이러한 추천 사항은 단일 및 다중 사용자 시나리오에 적용됩니다. 정적 텍스트 읽기와 같이 30fps 미만의 프레임 속도와 관련된 시나리오에는 사용 가능한 대역폭이 더 적게 필요합니다.

| 30fps의 일반적인 디스플레이 해상도    | 추천 대역폭 |
|------------------------------------------|-----------------------|
| 약 1024x768px                      | 1.5Mbps              |
| 약 1280x720px                      | 3Mbps                |
| 약 1920×1080px                     | 5Mbps                |
| 약 3840x2160px(4K)                | 15Mbps               |

## <a name="additional-resources"></a>추가 리소스

현재 사용 중인 Azure 지역은 네트워크 조건만큼 사용자 환경에 영향을 줄 수 있습니다. 자세한 내용은 [Windows Virtual Desktop 경험 추정기](https://azure.microsoft.com/services/virtual-desktop/assessment/)를 확인하세요.
