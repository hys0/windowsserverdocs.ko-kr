---
title: 원격 RADIUS 서버 그룹
description: 이 항목에서는 네트워크 정책 서버 원격 RADIUS 서버 그룹의 Windows Server 2016의 개요를 제공합니다.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: d81678a7-be21-48f2-9b3f-5a75d6aef013
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9912927a7b75e4c9f04aa3d24eb7ed46c73a7dd2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855264"
---
# <a name="remote-radius-server-groups"></a>원격 RADIUS 서버 그룹

>적용 대상: Windows Server (반기 채널), Windows Server 2016

NPS를 사용 하 여 수행할 수 있으므로 연결 요청을 처리할 수는 RADIUS 서버에 연결 요청을 전달 하도록 전화 접속 사용자 서비스 RADIUS (Remote Authentication) 프록시 서버 NPS (네트워크 정책)를 구성한 경우 인증 및 권한 부여는 사용자 또는 컴퓨터 계정이 있는 도메인입니다. 예를 들어, 트러스트 되지 않은 도메인에 하나 이상의 RADIUS 서버로 연결 요청을 전달 하려는 경우 신뢰할 수 없는 도메인의 원격 RADIUS 서버에 요청을 전달 하는 RADIUS 프록시로 NPS를 구성할 수 있습니다.

>[!NOTE]
>원격 RADIUS 서버 그룹은 관련이 및 별도의 Windows 그룹입니다.

NPS를 RADIUS 프록시로 구성 하려면 모든 전달할 메시지를 평가 하는 NPS 및 메시지를 보낼 위치에 필요한 정보를 포함 하는 연결 요청 정책을 만들어야 합니다.

NPS에서 원격 RADIUS 서버 그룹을 구성 하는 경우 그룹을 사용 하 여 연결 요청 정책을 구성할 NPS 연결 요청을 전달할 위치를 지정 하는 합니다.

## <a name="configuring-radius-servers-for-a-group"></a>그룹에 대 한 RADIUS 서버 구성

원격 RADIUS 서버 그룹은 하나 이상의 RADIUS 서버를 포함 하는 명명 된 그룹입니다. 둘 이상의 서버를 구성 하는 경우 로드 균형 조정 서버 프록시에서 사용 되는 순서를 결정 하거나 또는 하나 이상의 서버를 오버 로드를 방지 하는 그룹의 모든 서버에서 RADIUS 메시지 흐름을 배포 하는 설정을 지정할 수 있습니다. 연결 요청이 너무 많음를 사용 하 여.

그룹의 각 서버에 다음 설정이 있습니다.

- **이름 또는 주소**합니다. 각 그룹 구성원에는 그룹 내에서 고유한 이름이 있어야 합니다. IP 주소 또는 이름을 해당 IP 주소로 확인 될 수 있는 이름일 수 있습니다.

- **인증 및 계정**합니다. 인증 요청, 계정 요청 중 하나 또는 둘 다가 각 원격 RADIUS 서버 그룹 멤버에 전달할 수 있습니다.

- **부하 분산**합니다. 우선 순위 설정 그룹의 멤버는 주 서버 (우선 순위를 1로 설정 됨)을 나타내기 위해 사용 됩니다. 동일한 우선 순위는 그룹 멤버에 대 한 가중치 설정은 빈도 계산 하는 각 서버에 RADIUS 메시지 전송 됩니다. NPS이 그룹 멤버는 먼저 사용할 수 없게 되 고 사용할 수 있을 때 사용할 수 없게 결정 한 후 검색 방법을 구성 하려면 추가 설정을 사용할 수 있습니다.

원격 RADIUS 서버 그룹을 구성한 후의 인증 및 계정 설정은 연결 요청 정책 그룹을 지정할 수 있습니다. 이 인해 원격 RADIUS 서버 그룹을 먼저 구성할 수 있습니다. 그런 다음 새로 구성된 된 원격 RADIUS 서버 그룹을 사용 하는 연결 요청 정책을 구성할 수 있습니다. 또는 연결 요청 정책을 만드는 동안 새 원격 RADIUS 서버 그룹을 만들려면 새 연결 요청 정책 마법사를 사용할 수 있습니다.

NPS에 대 한 자세한 내용은 참조 하세요. [네트워크 정책 (NPS 서버)](nps-top.md)합니다.
