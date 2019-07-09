---
title: 원격 데스크톱 서비스 - 어디에서나 빌드
description: RDS 배포를 호스팅할 수 있는 위치를 결정할 수 있도록 돕는 계획 정보입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c803a383-0eea-4e11-bca5-d204ab758048
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 4563108d2efa9cd864fbe75fa82349d21659a941
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63712330"
---
# <a name="remote-desktop-services---build-anywhere"></a>원격 데스크톱 서비스 - 어디에서나 빌드

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

온-프레미스, 클라우드에서 또는 두 개의 하이브리드를 배포합니다. 비즈니스 요구 사항 변화에 따라 배포를 수정합니다.

위치에 관계없이 원격 데스크톱 서비스 환경의 기본 [아키텍처](desktop-hosting-logical-architecture.md)는 그대로 유지됩니다.
- 외부 사용자에 대한 RD 웹 액세스 및 RD 게이트웨이를 활용하는 인터넷 연결 서버가 여전히 있어야 합니다.
- Active Directory 및 항상 사용 가능한 환경을 위해 사용자 및 원격 데스크톱 속성을 수용하는 SQL 데이터베이스가 여전히 있어야 합니다.
- 최종 사용자를 해당 데스크톱 또는 애플리케이션에 연결할 수 있도록 RD 인프라 역할(RD 연결 브로커, RD 게이트웨이, RD 라이선싱 및 RD 웹 액세스)과 최종 RDSH 또는 RDVH 호스트 간에 통신 액세스가 여전히 있어야 합니다.

이러한 유연성을 통해 둘의 모든 장점을 얻을 수 있습니다.
- 클라우드 및 온라인 세계와 연결된 단순성 및 종량제 메서드
- 온-프레미스에 이미 존재하는 대규모 리소스를 활용하는 친숙하고 번거롭지 않은 방법

추가 정보는 [원격 데스크톱 서비스 배포를 빌드 및 배포](rds-build-and-deploy.md)하는 방법을 확인하세요.