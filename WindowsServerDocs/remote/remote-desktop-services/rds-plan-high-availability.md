---
title: 원격 데스크톱 서비스-고가용성
description: 항상 사용 가능한 RDS 배포를 설정 하는 방법에 대 한 정보를 계획 합니다.
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
ms.openlocfilehash: b5a2bd38c8831063d6fd2ba525b71a10403b8fc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839264"
---
# <a name="remote-desktop-services---high-availability"></a>원격 데스크톱 서비스-고가용성

>적용 대상: Windows Server (반기 채널), Windows Server 2016

오류 및 제한은 대규모 시스템에서 피할 수 없습니다. 간단 하 게 원활 하 게 연결 하도록 고가용성을 지원 하 고 최종 사용자를 허용 하도록 원격 데스크톱 인프라 역할 설정 될 때마다 합니다.

원격 데스크톱 서비스의 다음 항목을 고가용성을 설정 하려면 해당 해당 지침을 사용 하 여 원격 데스크톱 인프라 역할을 나타냅니다.
- [원격 데스크톱 연결 브로커](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)
- [원격 데스크톱 게이트웨이](Deploy-a-RD-Web-Access-and-Gateway-farm.md)
- 원격 데스크톱 라이선싱
- [원격 데스크톱 웹 액세스](Deploy-a-RD-Web-Access-and-Gateway-farm.md)

고가용성은 두 번째 컴퓨터에서 역할 서비스를 각각을 복제 하 여 설정 됩니다. Azure에서 가용성에는 두 개의 가상 머신 (역할을 호스팅하는 동일한) 집합을 배치 하 여 작동 시간을 보장된 받을 수를 설정 합니다.

가용성 집합을 함께 이제 항상 연결 정보를 포함 하는 데스크톱 및 응용 프로그램에 사용자를 리디렉션할 수 있도록 Azure SQL Database 및 해당 되는 Azure 지원 SLA의 기능을 활용할 수 있습니다.

RDS 환경 만들기에 대 한 모범 사례를 참조 하십시오 합니다 [데스크톱 호스팅 아키텍처](desktop-hosting-reference-architecture.md)합니다.