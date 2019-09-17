---
title: 원격 데스크톱 서비스 - 고가용성
description: 고가용성 RDS 배포 설정에 대한 계획 정보입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec630ea0-ab80-4dfe-a25f-f4f601651f72
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: ab9a6118641b49dfa971e66dc9ba75ef88bbd84a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870883"
---
# <a name="remote-desktop-services---high-availability"></a>원격 데스크톱 서비스 - 고가용성

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

대규모 시스템에서는 실패 및 제한을 피할 수 없습니다. 고가용성을 지원하도록 원격 데스크톱 인프라 역할을 간단히 설정하고 최종 사용자가 항상 원활하게 연결하도록 할 수 있습니다.

원격 데스크톱 서비스에서 다음 항목은 고가용성을 설정하기 위한 해당 지침과 원격 데스크톱 인프라 역할을 나타냅니다.
- [원격 데스크톱 연결 브로커](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)
- [원격 데스크톱 게이트웨이](Deploy-a-RD-Web-Access-and-Gateway-farm.md)
- 원격 데스크톱 라이선싱
- [원격 데스크톱 웹 액세스](Deploy-a-RD-Web-Access-and-Gateway-farm.md)

고가용성은 두 번째 컴퓨터에서 각 역할 서비스를 복제하여 설정합니다. Azure에서 사용자는 가용성 집합에 두 개의 가상 머신(동일한 역할 호스트)을 배치하여 보장된 가동 시간을 받을 수 있습니다.

이제, 가용성 집합을 함께 Azure SQL Database 및 해당 Azure 지원 SLA의 기능을 활용하여 항상 연결 정보를 파악하고 해당 데스크톱 및 애플리케이션으로 사용자를 리디렉션할 수 있습니다.

RDS 환경을 만들기 위한 모범 사례에 대해서는 [데스크톱 호스팅 아키텍처](desktop-hosting-reference-architecture.md)를 참조하세요.