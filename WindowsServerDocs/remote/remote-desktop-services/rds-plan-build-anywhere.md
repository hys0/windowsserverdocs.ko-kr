---
title: 원격 데스크톱 서비스-어디에서 빌드
description: RDS 배포를 호스팅할 수 있는 위치를 결정할 수 있도록 계획 정보입니다.
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
ms.openlocfilehash: cbb8e73d753b1fe4f0293cf4427c634020a23a42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869514"
---
# <a name="remote-desktop-services---build-anywhere"></a>원격 데스크톱 서비스-어디에서 빌드

>적용 대상: Windows Server (반기 채널), Windows Server 2016

온-프레미스, 클라우드 또는 둘의 하이브리드 배포 합니다. 비즈니스 요구 변화에 따라 배포를 수정 합니다.

여기서 인 내부에 관계 없이 [아키텍처](desktop-hosting-logical-architecture.md) 원격 데스크톱 서비스의 환경을 그대로 유지 됩니다.
- 여전히 외부 사용자에 대 한 RD 웹 액세스 및 RD 게이트웨이 활용 하는 인터넷 연결 서버 있어야
- 여전히 해야 Active Directory 및--항상 사용 가능한 환경에 대 한 기본 사용자 및 원격 데스크톱 속성에 SQL database
- 여전히 RD 인프라 역할 (RD 연결 브로커, RD 게이트웨이, RD 라이선싱 및 RD 웹 액세스) 및 RDSH 끝 사이 통신 액세스 또는 RDVH 호스트를 최종 사용자가 데스크톱 또는 응용 프로그램에 연결할 수 있어야 합니다.

이러한 유연성을 사용 하면의 장점 모두 얻을 수 있습니다.
- 클라우드 및 온라인 세계와 관련 된 간단 하 고 종 량 제 메서드.
- 친숙 하 고 요구가 많은 리소스를 이미 활용의 간편한 방식으로 온-프레미스 존재 합니다.

자세한 내용은 하는 방법을 살펴보세요 [빌드 및 배포에 원격 데스크톱 서비스 배포](rds-build-and-deploy.md)합니다.