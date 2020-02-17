---
title: Windows Server 업그레이드 개요 | Microsoft Docs
description: 실제 업그레이드를 수행하기 전에 고려해야 할 사항을 비롯한 몇 가지 일반적인 Windows Server 업그레이드 정보를 알아봅니다.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/10/2019
ms.openlocfilehash: 6f57e52657ca3c80c92d56c54ea87e43aabd1e99
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124793"
---
# <a name="overview-about-windows-server-upgrades"></a>Windows Server 업그레이드 개요

최신 버전의 Windows Server로 업그레이드하는 프로세스는 작업을 시작하는 운영 체제와 진행 경로에 따라 크게 다를 수 있습니다. 다음 용어를 사용하여 새로운 Windows Server 배포에 포함될 수 있는 다양한 작업 간을 구분할 수 있습니다.

- **업그레이드** "현재 위치 업그레이드"라고도 합니다. 이전 버전의 운영 체제에서 최신 버전으로 이동하면서도 동일한 실제 하드웨어를 유지합니다. **이는 이 섹션에서 다룰 메서드입니다.**

    >[!Important]
    >퍼블릭 또는 프라이빗 클라우드 회사에서 현재 위치 업그레이드를 지원할 수도 있습니다. 그러나 자세한 내용은 클라우드 공급자에게 문의해야 합니다. 또한 **VHD에서 부팅**하도록 구성된 모든 Windows 서버에서 현재 위치 업그레이드를 수행할 수 없습니다.

- **설치** "새로 설치"라고도 합니다. 이전 버전의 운영 체제에서 최신 버전으로 이동하여 이전 버전의 운영 체제를 삭제합니다.

- **마이그레이션** 다른 하드웨어 또는 가상 머신 세트로 전송하여 이전 버전의 운영 체제에서 최신 버전의 운영 체제로 이동합니다.

- **클러스터 OS 롤링 업그레이드** Hyper-V나 스케일 아웃 파일 서버 워크로드를 중단하지 않고도 클러스터 노드의 운영 체제를 업그레이드합니다. 이 기능을 사용하면 서비스 수준 계약에 영향을 줄 수 있는 가동 중지 시간을 방지할 수 있습니다. 자세한 내용은 [클러스터 운영 체제 롤링 업그레이드](../failover-clustering/cluster-operating-system-rolling-upgrade.md)를 참조하세요.

- **라이선스 변환** 해당 릴리스의 특정 버전을 간단한 명령과 적절한 라이선스 키만으로 동일한 릴리스의 다른 버전으로 한 번에 변환합니다. 이를 "라이선스 변환"이라고 합니다. 예를 들어 서버가 Windows Server 2016 Standard를 실행하는 경우 Windows Server 2016 Datacenter로 변환할 수 있습니다.

## <a name="which-version-of-windows-server-should-i-upgrade-to"></a>어떤 버전의 Windows Server로 업그레이드해야 하나요?

최신 버전의 Windows Server로 업그레이드하는 것이 좋습니다. Windows Server 2019 최신 버전의 Windows Server를 실행하면 최신 보안 기능을 포함하여 최신 기능을 사용할 수 있으며 최상의 성능을 제공합니다.

그러나 항상 가능하지는 않습니다. 다음 다이어그램을 사용하여 현재 사용 중인 버전에 따라 업그레이드할 수 있는 Windows Server 버전을 파악할 수 있습니다.

![사용 가능한 현재 위치 업그레이드 경로](media/upgrade-paths.png)

Windows Server는 일반적으로 하나 이상의 버전 때로는 두 개의 버전을 통해 업그레이드할 수 있습니다. 예를 들어 Windows Server 2012 R2 및 Windows Server 2016은 모두 Windows Server 2019로 바로 업그레이드할 수 있습니다.

평가판 운영 체제를 일반 정품 버전으로 업그레이드하거나, 이전 일반 정품 버전을 새 버전으로 업그레이드하거나, 경우에 따라 운영 체제의 볼륨 라이선스 버전을 일반 정품 버전으로 업그레이드할 수도 있습니다. 현재 위치 업그레이드 이외의 업그레이드 옵션에 대한 자세한 내용은 [Windows Server에 대한 업그레이드 및 변환 옵션](../get-started/supported-upgrade-paths.md)을 참조하세요.
