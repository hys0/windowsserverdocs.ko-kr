---
title: 원격 데스크톱 서비스-어디에서 나 액세스
description: RD 게이트웨이에 대한 계획 정보
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c38fab1-3586-4b7a-8bf0-7d85a8d5361d
author: lizap
ms.author: elizapo
ms.date: 11/03/2016
manager: dongill
ms.openlocfilehash: 0d3d8ed036b3befd81da6d5bbe8702ee866c6aa8
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63748827"
---
# <a name="remote-desktop-services---access-from-anywhere"></a>원격 데스크톱 서비스-어디에서 나 액세스

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

최종 사용자가 RD 게이트웨이 통해 회사 방화벽 외부에서 안전 하 게 내부 네트워크 리소스에 연결할 수 있습니다.

를 구성한 방식 데스크톱 최종 사용자에 관계 없이 신속 하 고 보안 연결에 대 한 연결 흐름에 RD 게이트웨이 쉽게 연결할 수 있습니다. 최종 사용자에 게 게시 된 피드를 통해 연결에 대 한 전반적인 배포 속성을 구성 하는 대로 RD 게이트웨이 속성을 구성할 수 있습니다. 최종 사용자에 게 피드 없이 데스크톱을 통해 연결에 대 한 조직의 RD 게이트웨이의 이름을 사용 하는 원격 데스크톱 클라이언트 애플리케이션에 관계 없이 연결 속성으로 쉽게 추가할 수 있습니다.

RD 게이트웨이 연결 시퀀스를 순서 대로 세 가지 주요 목적에는
1. **최종 사용자의 디바이스 및 RD 게이트웨이 서버 간에 암호화된 SSL 터널 설정**: RD 게이트웨이 서버를 통해 연결하려면 RD 게이트웨이 서버에 최종 사용자 디바이스에서 인식하는 인증서를 설치해야 합니다. 테스트 및 개념 증명 자체 서명 된 인증서를 사용할 수 있지만 모든 프로덕션 환경에서 인증 기관에서 공개적으로 신뢰할 수 있는 인증서만 사용 해야 합니다.
2. **환경에 사용자 인증**: RD 게이트웨이는 받은 편지함 IIS 서비스를 사용하여 인증을 수행하고 RADIUS 프로토콜을 활용하여 Azure MFA와 같은 [다중 요소 인증](rds-plan-mfa.md) 솔루션을 사용할 수도 있습니다. 만든 기본 정책 외에도 추가 RD 리소스 권한 부여 정책 RD Rap () 및 RD 연결 권한 부여 정책 (RD Cap) 좀 더 구체적으로 어떤 사용자가 액세스할 수 있어야를 정의 하는 안전한 환경 내에서 리소스를 만들 수 있습니다.
3. **최종 사용자의 디바이스 및 지정된 리소스 간에 앞뒤로 트래픽 전달**: RD 게이트웨이는 연결이 설정되어 있는 동안 계속으로 이 작업을 수행합니다. 사용자가 디바이스에서 멀어질 경우 작업 환경의 보안을 유지하기 위해 RD 게이트웨이 서버에서 서로 다른 시간 제한 속성을 지정할 수 있습니다.

[데스크톱 호스팅 참조 아키텍처](desktop-hosting-reference-architecture.md)에서 원격 데스크톱 서비스 배포의 전반적인 아키텍처에 대한 추가 세부 정보를 찾을 수 있습니다.