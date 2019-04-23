---
title: RDS 배포-재해 복구 보호
description: 원격 데스크톱 서비스에 대 한 재해 복구 옵션에 알아봅니다
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834084"
---
# <a name="configure-disaster-recovery-for-remote-desktop-services"></a>원격 데스크톱 서비스에 대 한 재해 복구 구성

환경에 원격 데스크톱 서비스를 배포할 때에 특히 앱 및 리소스를 사용자와 공유 하는 인프라의 중요 한 부분 됩니다. 작동이 중단 되더라도 RDS 배포 항목으로 인해 네트워크 오류를 자연 재해에 사용자가 해당 앱 및 리소스에 액세스할 수 없습니다 및 비즈니스 성능이 저하 됩니다. 이 문제를 방지 하려면 배포-장애 조치를 허용 하는 재해 복구 솔루션을 구성할 수 있습니다 어떤 이유로 든 RDS 배포를 사용할 수 없는 경우 백업을 자동으로 수행 하려면 사용할 수 있습니다.

단일 구성 요소 또는 컴퓨터가 다운의 경우 실행 RDS 배포를 유지 하려면 고가용성을 위해 RDS 배포를 구성 하는 것이 좋습니다. 설정 하 여이 수행할 수 있습니다는 [RDSH 팜을](rds-scale-rdsh-farm.md) 보장 하 [연결 브로커 고가용성을 위해 클러스터는](rds-connection-broker-cluster.md). 

여기서 권장 하는 재해 복구 솔루션 배포-고가용성을 위해 구성 된 중복 역할 등 전체 RDS 배포를 사용 하는 것 심각한 재해 로부터 보호 되도록 합니다. 이러한 재해에 도달 하는 경우 배포에 기본 제공 재해 복구 솔루션을 사용 하면 장애 조치를 전체 배포를 신속 하 게 앱 및 리소스 및 사용자에 게 실행 합니다.

RDS에서 재해 복구 솔루션을 배포 하려면 다음 정보를 사용 합니다.

- [사용자가 액세스할 수 있도록 RDS 배포에 하나의 Azure 데이터 센터 (지역 중복)를 중단 하는 경우에 여러 Azure 데이터 센터를 활용 합니다.](rds-multi-datacenter-deployment.md)
- [사이트 간 또는 사이트에서 Azure로 장애 조치의 RDS 구성 요소에 대 한 장애 조치를 위해 Azure Site Recovery를 배포 합니다.](rds-disaster-recovery-with-azure.md)


