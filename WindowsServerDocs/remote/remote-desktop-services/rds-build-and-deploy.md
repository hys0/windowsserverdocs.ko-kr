---
title: RDS-빌드 및 배포
description: 원격 데스크톱 배포를 구축 하는 단계
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/18/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 176ae424-96e9-4c78-88f5-da418e76c3d7
author: lizap
manager: dongill
ms.openlocfilehash: 309ea068488d005eabfe22f8ea055f85dd098452
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453075"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>빌드 및 원격 데스크톱 서비스 배포를 배포 합니다.

원격 데스크톱 서비스 배포는 사용자를 사용 하 여 앱 및 리소스를 공유 하는 데 인프라입니다. 제공 하려는 환경에 따라 할 수 있습니다이 작게 또는 복잡 한 필요에 따라 합니다. 원격 데스크톱 배포를 쉽게 확장 됩니다. 증가 하 고 원격 데스크톱 웹 액세스를 줄일 수, 게이트웨이, 연결 브로커 및 세션 호스트 서버에 됩니다. 작업 부하를 배포 하려면 원격 데스크톱 연결 브로커를 사용할 수 있습니다. Active Directory 기반 인증에는 강력한 보안 환경을 제공합니다. 

[원격 데스크톱 클라이언트](clients/remote-desktop-clients.md) phone 또는 Windows, Apple 또는 Android 컴퓨터, 태블릿에서 액세스할 수 있도록 합니다.

참조 [원격 데스크톱 서비스 아키텍처](desktop-hosting-logical-architecture.md) 에 대 한 원격 데스크톱 서비스 배포를 만들기 위해 함께 작동 하는 다른 부분에 대해 자세히 설명 합니다.

이전 버전의 Windows Server를 기반으로 기존 원격 데스크톱 배포 있나요? 성능 및 규모와 관련 된 새로운 기능과 향상 기능 활용을 받을 수 있는 WIndows Server 2016으로 이동 하기 위한 옵션을 확인해 보십시오.

- [RDS 배포 Windows Server 2016으로 마이그레이션](migrate-rds-role-services.md)
- [RDS 배포 Windows Server 2016으로 업그레이드](upgrade-to-rds-2016.md)

새 원격 데스크톱 배포를 만들고 싶으십니까? Windows Server 2016에서 원격 데스크톱을 배포 하려면 다음 정보를 사용 합니다.

- [원격 데스크톱 서비스 인프라를 배포 합니다.](rds-deploy-infrastructure.md)
- [앱과 공유 하려는 리소스를 저장할 세션 컬렉션 만들기](rds-create-collection.md)
- [RDS 배포 라이선스](rds-client-access-license.md)
- 설치 사용자를 [원격 데스크톱 클라이언트](clients/remote-desktop-clients.md) 앱 및 리소스에 액세스할 수 있도록 합니다. 
- 추가 연결 브로커 및 세션 호스트를 추가 하 여 고가용성을 사용 합니다.
   - [RD 세션 호스트 팜을 사용하여 기존 RDS 컬렉션 확장](rds-scale-rdsh-farm.md)
   - [RD 연결 브로커 인프라에 고가용성 추가](rds-connection-broker-cluster.md)
   - [RD 웹 및 RD 게이트웨이 웹 프런트에 고가용성 추가](rds-rdweb-gateway-ha.md)
   - [UPD 스토리지용 2노드 스토리지 공간 다이렉트 파일 시스템 배포](rds-storage-spaces-direct-deployment.md)


원격 데스크톱을 사용 하 여 고객 또는 찾는 다른 사용자에 게 앱을 호스트 하는 고객 앱 및 리소스를 제공 하는 데 관심이 호스팅 파트너 라면 체크 아웃 [원격 데스크톱 서비스를 호스팅 파트너](rds-hosting-partners.md) 에 대 한 자세한는 평가 것을 통과 하는 파트너 목록을 뿐만 아니라 호스팅 환경으로 Azure에서 RDS를 사용 하는 방법에 대 한 수행할 수 있습니다.
