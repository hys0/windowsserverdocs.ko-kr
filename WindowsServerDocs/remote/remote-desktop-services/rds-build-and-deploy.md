---
title: RDS-빌드 및 배포
description: 원격 데스크톱 배포를 빌드하는 단계
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 9c3962a830d9544e915a96f061e32bb9e037949b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404039"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>빌드 및 원격 데스크톱 서비스 배포를 배포 합니다.

원격 데스크톱 서비스 배포는 사용자와 앱 및 리소스를 공유하는 데 사용되는 인프라입니다. 제공하려는 환경에 따라 필요한 만큼 작거나 복잡하게 만들 수 있습니다. 원격 데스크톱 배포를 쉽게 확장 됩니다. 증가 하 고 원격 데스크톱 웹 액세스를 줄일 수, 게이트웨이, 연결 브로커 및 세션 호스트 서버에 됩니다. 작업 부하를 배포 하려면 원격 데스크톱 연결 브로커를 사용할 수 있습니다. Active Directory 기반 인증에는 강력한 보안 환경을 제공합니다. 

[원격 데스크톱 클라이언트](clients/remote-desktop-clients.md)는 Windows, Apple 또는 Android 컴퓨터, 태블릿 또는 휴대폰에서의 액세스를 활성화합니다.

원격 데스크톱 서비스 배포를 구성하기 위해 함께 작동하는 다른 부분에 대한 자세한 설명은 [원격 데스크톱 서비스 아키텍처](desktop-hosting-logical-architecture.md)를 참조하세요.

이전 버전의 Windows Server를 기반으로 하는 기존 원격 데스크톱 배포가 있나요? WIndows Server 2016으로 이동하기 위한 옵션을 확인해보세요. 여기에서 성능 및 규모와 관련된 새롭고 향상된 기능을 활용할 수 있습니다.

- [Windows Server 2016으로 RDS 배포 마이그레이션](migrate-rds-role-services.md)
- [Windows Server 2016으로 RDS 배포 업그레이드](upgrade-to-rds-2016.md)

새 원격 데스크톱 배포를 만들고 싶으신가요? 다음 정보를 사용하여 Windows Server 2016에서 원격 데스크톱을 배포합니다.

- [원격 데스크톱 서비스 인프라 배포](rds-deploy-infrastructure.md)
- [공유하려는 앱 및 리소스를 저장할 세션 컬렉션 만들기](rds-create-collection.md)
- [RDS 배포 라이선스](rds-client-access-license.md)
- 사용자가 앱 및 리소스에 액세스할 수 있도록 [원격 데스크톱 클라이언트](clients/remote-desktop-clients.md)를 설치하도록 합니다. 
- 추가 연결 브로커 및 세션 호스트를 추가하여 고가용성을 활성화합니다.
   - [RD 세션 호스트 팜을 사용하여 기존 RDS 컬렉션 확장](rds-scale-rdsh-farm.md)
   - [RD 연결 브로커 인프라에 고가용성 추가](rds-connection-broker-cluster.md)
   - [RD 웹 및 RD 게이트웨이 웹 프런트에 고가용성 추가](rds-rdweb-gateway-ha.md)
   - [UPD 스토리지용 2노드 스토리지 공간 다이렉트 파일 시스템 배포](rds-storage-spaces-direct-deployment.md)


사용자가 원격 데스크톱을 이용해 고객에게 앱과 리소스를 제공하려는 호스팅 파트너이거나, 사용자의 앱을 호스트할 사람을 찾는 고객이라면 [원격 데스크톱 서비스 호스팅 파트너](rds-hosting-partners.md)를 확인하세요. Azure에서 호스팅 환경으로 RDS를 사용하는 것과 관련한 평가 정보와 통과한 파트너의 목록을 확인하실 수 있습니다.
