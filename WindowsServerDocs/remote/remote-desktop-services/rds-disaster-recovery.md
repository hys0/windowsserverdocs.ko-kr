---
title: RDS 배포 보호 - 재해 복구
description: 원격 데스크톱 서비스의 재해 복구 옵션 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9ff6a3b0-ea14-424e-9524-209252e9f1a8
author: lizap
ms.author: elizapo
ms.date: 06/12/2017
ms.openlocfilehash: a6eac3a50999633d15b1b6dc28608f60f6fef6c7
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "63743812"
---
# <a name="configure-disaster-recovery-for-remote-desktop-services"></a>원격 데스크톱 서비스의 재해 복구 구성

작업 환경에 원격 데스크톱 서비스를 배포할 경우 인프라, 특히 사용자와 공유하는 앱 및 리소스의 중요한 부분이 됩니다. 자연 재해로 인한 네트워크 장애 때문에 RDS 배포가 작동 중단될 경우 사용자는 해당 앱 및 리소스에 액세스할 수 없으며 비즈니스는 부정적인 영향을 받게 됩니다. 이 문제를 방지하려면 배포를 장애 조치(failover)하도록 허용하는 재해 복구 솔루션을 구성할 수 있습니다. 어떤 이유로든 RDS 배포를 사용할 수 없어도 자동으로 백업을 인수할 수 있습니다.

단일 구성 요소 또는 컴퓨터가 작동 중단될 경우 RDS 배포를 계속 실행하려면 고가용성을 위해 RDS 배포를 구성하는 것이 좋습니다. 이를 위해 [RDSH 팜](rds-scale-rdsh-farm.md)을 설정하고 [고가용성을 위해 연결 브로커를 클러스터링](rds-connection-broker-cluster.md)할 수 있습니다. 

여기서 권장하는 재해 복구 솔루션은 심각한 재해로부터 배포를 보호하여 전체 RDS 배포를 보호하는 솔루션(고가용성을 위해 구성된 중복 역할 포함)입니다. 이러한 재해가 발생할 경우 배포에 기본 제공된 재해 복구 솔루션을 사용하여 전체 배포를 장애 조치(failover)하고 앱 및 리소스를 빠르게 작동되도록 할 수 있습니다.

RDS에서 재해 복구 솔루션을 배포하려면 다음 정보를 사용합니다.

- [Azure 데이터 센터가 작동 중단되더라도 사용자가 RDS 배포에 액세스할 수 있도록 하기 위해 여러 Azure 데이터 센터를 활용합니다(지역 중복).](rds-multi-datacenter-deployment.md)
- [Azure Site Recovery를 배포하여 사이트 간 또는 사이트에서 Azure로의 장애 조치(failover)에서 RDS 구성 요소에 대한 장애 조치(failover) 제공](rds-disaster-recovery-with-azure.md)


