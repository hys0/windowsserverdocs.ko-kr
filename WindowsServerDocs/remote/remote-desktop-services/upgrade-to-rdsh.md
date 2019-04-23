---
title: 원격 데스크톱 세션 호스트 Windows Server 2016으로 업그레이드
description: 이 문서에서는 기존 원격 데스크톱 서비스 배포 Windows Server 2016으로 업그레이드 하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c9b98b8-4eca-4a39-b10b-2bac729f7f44
author: spatnaik
manager: scottman
ms.openlocfilehash: 0cf5af29d610ba64d045e10241fd39b01d3f7024
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856064"
---
# <a name="upgrading-your-remote-desktop-session-host-to-windows-server-2016"></a>원격 데스크톱 세션 호스트 Windows Server 2016으로 업그레이드

>적용 대상: Windows Server (반기 채널), Windows Server 2016

> [!IMPORTANT]
> 모든 응용 프로그램 업그레이드 하기 전에 제거 하 고 업그레이드로 인해 증가 수는 응용 프로그램 호환성 문제를 방지 하려면 업그레이드 후 다시 설치 해야 합니다.

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 역할이 설치 된 OS 업그레이드를 지원
Windows Server 2016으로 업그레이드는 Windows Server 2012 R2 및 Windows Server 2016 TP5 에서만 지원 됩니다.

## <a name="upgrading-a-rds-session-based-collection"></a>RDS 세션 기반 컬렉션을 업그레이드합니다.
다운 타임을 최소한으로 유지를 위해 RDS 세션 기반 컬렉션을 업그레이드 하는 동안 아래 단계를 수행 하는 것이 좋습니다.

1. 업그레이드할 서버를 식별 합니다. 예를 들어 절반의 서버 컬렉션입니다.
2. 이러한 서버에 대 한 새 연결을 설정 하 여 방지할 **새 연결을 허용** 를 false로 합니다.
3. 이러한 서버의 모든 세션을 기록 합니다. 
4. 컬렉션에서 이러한 서버를 제거 합니다.
5. Windows Server 2016으로 서버를 업그레이드 합니다.
6. 설정할 **새 연결을 허용** 컬렉션에 있는 나머지 서버를 "false"입니다.
7. 해당 컬렉션으로 업그레이드 된 서버를 추가 합니다.
8. 컬렉션에서 업그레이드할 서버의 나머지 집합을 제거 합니다.
9. 설정할 **새 연결을 허용** 업그레이드 된 서버 컬렉션에서 "true"로 합니다.
10. 이제 위의 9 통해 다음 단계 3에서 배포의 나머지 서버를 업그레이드 합니다.

## <a name="upgrading-a-standalone-rd-session-host-server"></a>독립 실행형 RD 세션 호스트 서버 업그레이드
독립 실행형 RD 세션 호스트 서버는 언제 든 지 업그레이드할 수 있습니다.