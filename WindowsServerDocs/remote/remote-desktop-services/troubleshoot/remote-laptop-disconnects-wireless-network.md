---
title: 무선 네트워크에서 원격 노트북 연결 끊김
description: 원격 랩톱과 무선 네트워크의 연결이 끊어지는 문제를 해결합니다.
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 72bf482512ff3bb0a678ae59cd6ac20b947a54d9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857156"
---
# <a name="remote-laptop-disconnects-from-wireless-network"></a>무선 네트워크에서 원격 노트북 연결 끊김

이 문제는 원격 데스크톱 클라이언트에서 802.1x 무선 네트워크를 사용하여 랩톱 컴퓨터에 연결할 때 발생할 수 있습니다. 랩톱에서 무선 네트워크와의 연결이 간헐적으로 끊기고 자동으로 다시 연결되지 않습니다.

이는 무선 네트워크 연결에 대한 네트워크 인증 설정이 **사용자 인증**일 때 발생하는 알려진 이슈입니다.

이 이슈를 해결하려면 네트워크 인증 설정을 **사용자 또는 컴퓨터 인증** 또는 **컴퓨터 인증**으로 설정합니다.

 > [!NOTE]  
> 단일 컴퓨터에서 네트워크 인증 설정을 변경하려면 네트워크 및 공유 센터 제어판을 사용하여 새로운 설정으로 새 무선 연결을 만들어야 합니다.

GPO를 사용하여 무선 네트워크 설정을 구성하는 방법에 대한 전체 설명은 [무선 네트워크(IEEE 802.11) 정책 구성](../../../networking/core-network-guide/cncg/wireless/e-wireless-access-deployment.md#bkmk_policies)을 참조하세요.
