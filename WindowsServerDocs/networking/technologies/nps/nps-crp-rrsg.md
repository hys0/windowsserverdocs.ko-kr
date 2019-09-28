---
title: 원격 RADIUS 서버 그룹
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버 원격 RADIUS 서버 그룹에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: d81678a7-be21-48f2-9b3f-5a75d6aef013
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 63a6eb5f0f78ed8dbcc0144602f16274fd6ec213
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71396317"
---
# <a name="remote-radius-server-groups"></a>원격 RADIUS 서버 그룹

>적용 대상: Windows Server(반기 채널), Windows Server 2016

NPS (네트워크 정책 서버)를 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 프록시로 구성 하는 경우 NPS를 사용 하 여 연결 요청을 수행할 수 있는 연결 요청을 처리할 수 있는 RADIUS 서버에 전달 합니다. 사용자 또는 컴퓨터 계정이 있는 도메인의 인증 및 권한 부여 예를 들어 트러스트 되지 않은 도메인에 있는 하나 이상의 RADIUS 서버에 연결 요청을 전달 하려는 경우 트러스트 되지 않은 도메인의 원격 RADIUS 서버에 요청을 전달 하도록 NPS를 RADIUS 프록시로 구성할 수 있습니다.

>[!NOTE]
>원격 RADIUS 서버 그룹은 Windows 그룹과 관련이 없습니다.

NPS를 RADIUS 프록시로 구성 하려면 NPS에서 전달할 메시지와 메시지를 보낼 위치를 평가 하는 데 필요한 모든 정보를 포함 하는 연결 요청 정책을 만들어야 합니다.

NPS에서 원격 RADIUS 서버 그룹을 구성 하 고 해당 그룹을 사용 하 여 연결 요청 정책을 구성 하는 경우 NPS가 연결 요청을 전달 하는 위치를 지정 합니다.

## <a name="configuring-radius-servers-for-a-group"></a>그룹에 대 한 RADIUS 서버 구성

원격 RADIUS 서버 그룹은 하나 이상의 RADIUS 서버를 포함 하는 명명 된 그룹입니다. 둘 이상의 서버를 구성 하는 경우 부하 분산 설정을 지정 하 여 프록시가 서버를 사용 하는 순서를 결정 하거나, 하나 이상의 서버를 오버 로드 하지 못하도록 그룹의 모든 서버에서 RADIUS 메시지의 흐름을 분산 시킬 수 있습니다. 연결 요청이 너무 많음

그룹의 각 서버에는 다음과 같은 설정이 있습니다.

- **이름 또는 주소**입니다. 각 그룹 구성원은 그룹 내에서 고유한 이름을 가져야 합니다. 이름은 ip 주소 또는 IP 주소로 확인할 수 있는 이름일 수 있습니다.

- **인증 및 계정**. 각 원격 RADIUS 서버 그룹 구성원에 인증 요청, 계정 요청 또는 둘 다를 전달할 수 있습니다.

- **부하 분산**. 우선 순위 설정은 주 서버 그룹의 구성원을 나타내는 데 사용 됩니다 (우선 순위는 1로 설정 됨). 우선 순위가 같은 그룹 멤버의 경우 가중치 설정은 각 서버에 RADIUS 메시지를 보내는 빈도를 계산 하는 데 사용 됩니다. 추가 설정을 사용 하 여 그룹 멤버를 먼저 사용할 수 없게 되 고 사용할 수 없는 것으로 확인 된 후에 사용할 수 있게 되 면 NPS에서 검색 되는 방법을 구성할 수 있습니다.

원격 RADIUS 서버 그룹을 구성한 후에는 연결 요청 정책의 인증 및 계정 설정에서 그룹을 지정할 수 있습니다. 이로 인해 먼저 원격 RADIUS 서버 그룹을 구성할 수 있습니다. 그런 다음 새로 구성 된 원격 RADIUS 서버 그룹을 사용 하도록 연결 요청 정책을 구성할 수 있습니다. 또는 새 연결 요청 정책 마법사를 사용 하 여 연결 요청 정책을 만드는 동안 새 원격 RADIUS 서버 그룹을 만들 수 있습니다.

NPS에 대 한 자세한 내용은 [nps (네트워크 정책 서버)](nps-top.md)를 참조 하세요.
