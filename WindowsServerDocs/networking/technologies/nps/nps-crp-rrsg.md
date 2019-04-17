---
title: 원격 RADIUS 서버 그룹
description: 이 항목에서는 네트워크 정책 서버 원격 RADIUS 서버 그룹 Windows Server 2016에 대 한 개요입니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d81678a7-be21-48f2-9b3f-5a75d6aef013
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1f27b5e501f110a038264cd54d75c8b8f9566a64
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="remote-radius-server-groups"></a>원격 RADIUS 서버 그룹

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 프록시 서버 NPS (네트워크 정책)를 구성할 때은 사용자 또는 컴퓨터 계정이 있는 도메인에 인증과 수행할 수 있으므로 연결 요청을 처리할 수 RADIUS 서버에 연결 요청을 전송 하도록 NPS 사용 합니다. 예를 들어 신뢰할 수 없는 하는 도메인의 하나 이상 RADIUS 서버에 연결 요청을 전송 하도록 하려는 경우 NPS RADIUS 프록시 신뢰할 수 없는 도메인의 원격 RADIUS 서버에 요청을 전송 하도록으로 구성할 수 있습니다.

>[!NOTE]
>원격 RADIUS 서버 그룹은 관련이 및 Windows 그룹 별개입니다.

NPS RADIUS 프록시를 구성 하려면 모든 NPS 전달 하는 메시지를 확인 및 메시지를 보낼 수 있는 위치에 필요한 정보를 포함 하는 연결 요청 정책을 만들어야 합니다.

원격 RADIUS 서버 그룹 NPS에서 구성 그룹과 연결 요청 정책을 구성할 때 NPS 연결 요청을 전송 하도록 위치를 지정 하는 것입니다.

## <a name="configuring-radius-servers-for-a-group"></a>그룹에 대 한 RADIUS 서버 구성

원격 RADIUS 서버 그룹 하나 또는 여러 개의 RADIUS 서버 포함 된 명명된 그룹이입니다. 둘 이상의 서버 구성한 경우 부하 분산 프록시 서버 사용 되는 순서를 결정 하거나 하거나 하나 또는 여러 개의 서버에 연결 요청을 너무 많이 채우지 방지 그룹의 모든 서버 RADIUS 메시지 흐름 분산 설정을 지정할 수 있습니다.

그룹의 각 서버에는 다음과 같은 설정이 있습니다.

- **이름 또는 주소**합니다. 각 그룹 구성원 고유한 이름을 그룹 내 있어야 합니다. IP 주소 또는 IP 주소를 확인할 수 있는 이름을 이름일 수 있습니다.

- **인증과 계정**합니다. 인증 요청, 계정 요청 또는 둘 다 원격 각 RADIUS 서버 그룹 구성원에 게 전달할 수 있습니다.

- **부하 분산**합니다. 우선 순위 설정 (우선 순위 1로 설정 되어) 주 서버 그룹 구성원 나타내는 데 사용 됩니다. 그룹 구성원 순위가 동일한의 두께 설정 얼마나 자주를 계산 하는 데 사용 RADIUS 메시지 각 서버로 전송 됩니다. 사용할 수 있을 때 사용할 수를 확인 한 후 및 그룹 구성원을 처음 사용할 수 있을 때 하지 NPS 서버에서 검색 하는 방법을 구성할 수의 추가 설정을 사용할 수 있습니다.

원격 RADIUS 서버 그룹 구성한 경우에 인증 및 연결 요청 정책의 계정 설정에 그룹을 지정할 수 있습니다. 이 인해 원격 RADIUS 서버 그룹 먼저 구성할 수 있습니다. 다음으로 구성된 새로 원격 RADIUS 서버 그룹을 사용 하 여 연결 요청 정책을 구성할 수 있습니다. 또는 그룹을 만들려면 새 원격 RADIUS 서버 연결 요청 정책 만드는 동안 새 연결 요청 정책 마법사를 사용할 수 있습니다.

NPS에 대 한 자세한 내용은 참조 [네트워크 NPS 정책 서버 ()](nps-top.md)합니다.
