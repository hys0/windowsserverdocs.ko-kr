---
title: 원격 데스크톱 세션 호스트를 Windows Server 2016으로 업그레이드
description: 이 문서에서는 기존 원격 데스크톱 서비스 배포를 Windows Server 2016으로 업그레이드하는 방법을 설명합니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.topic: article
ms.assetid: 5c9b98b8-4eca-4a39-b10b-2bac729f7f44
author: spatnaik
manager: scottman
ms.openlocfilehash: e685c51a003a7121dab19c74d82796311ef0889a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857126"
---
# <a name="upgrading-your-remote-desktop-session-host-to-windows-server-2016"></a>원격 데스크톱 세션 호스트를 Windows Server 2016으로 업그레이드

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

> [!IMPORTANT]
> 업그레이드로 인해 발생할 수 있는 애플리케이션 호환성 이슈를 피하려면 업그레이드 전에 모든 애플리케이션을 제거했다가 업그레이드 후에 다시 설치해야 합니다.

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 역할이 설치된 지원되는 OS 업그레이드
Windows Server 2016으로의 업그레이드는 Windows Server 2012 R2 및 Windows Server 2016 TP5에서만 지원됩니다.

## <a name="upgrading-a-rds-session-based-collection"></a>RDS 세션 기반 컬렉션 업그레이드
가동 중지 시간을 최소한으로 유지하려면 RDS 세션 기반 컬렉션을 업그레이드하는 동안 아래 단계를 수행하는 것이 좋습니다.

1. 업그레이드할 서버(컬렉션에 있는 서버의 절반 정도)를 식별합니다.
2. **새 연결 허용**을 false로 설정하여 이러한 서버에 대한 새 연결을 방지합니다.
3. 이러한 서버의 모든 세션에서 로그오프합니다. 
4. 컬렉션에서 이러한 서버를 제거합니다.
5. 서버를 Windows Server 2016으로 업그레이드합니다.
6. 컬렉션의 나머지 서버에서 **새 연결 허용**을 "false"로 설정합니다.
7. 업그레이드한 서버를 해당 컬렉션에 다시 추가합니다.
8. 컬렉션에서 업그레이드할 나머지 서버 세트를 제거합니다.
9. 컬렉션의 업그레이드한 서버에서 **새 연결 허용**을 "true"로 설정합니다.
10. 이제 위의 3~9단계에 따라 배포의 나머지 서버를 업그레이드합니다.

## <a name="upgrading-a-standalone-rd-session-host-server"></a>독립 실행형 RD 세션 호스트 서버 업그레이드
독립 실행형 RD 세션 호스트 서버는 언제든지 업그레이드할 수 있습니다.