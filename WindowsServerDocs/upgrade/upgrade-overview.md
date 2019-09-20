---
title: Windows Server 업그레이드 개요 | Microsoft Docs
description: 실제 업그레이드를 수행 하기 전에 고려해 야 할 사항을 비롯 한 몇 가지 일반적인 Windows Server 업그레이드 정보를 알아봅니다.
ms.prod: windows server
ms.technology: server-general
ms.topic: upgrade
author: RobHindman
ms.author: robhind
ms.date: 09/10/2019
ms.openlocfilehash: 6f57e52657ca3c80c92d56c54ea87e43aabd1e99
ms.sourcegitcommit: 27f0caf74e88781054250455c3c1adf06deb6234
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71124793"
---
# <a name="overview-about-windows-server-upgrades"></a>Windows Server 업그레이드 개요

최신 버전의 Windows Server로 업그레이드 하는 프로세스는 시작 하는 운영 체제와 수행 하는 경로에 따라 크게 다를 수 있습니다. 다음 용어를 사용 하 여 새 Windows Server 배포에 포함 될 수 있는 다른 작업을 구분할 수 있습니다.

- **업그레이드할.** "전체 업그레이드" 라고도 합니다. 이전 버전의 운영 체제에서 최신 버전으로 이동 하면서도 동일한 실제 하드웨어를 유지 합니다. **이는이 섹션에서 다룰 메서드입니다.**

    >[!Important]
    >공용 또는 사설 클라우드 회사에서 전체 업그레이드를 지원할 수도 있습니다. 그러나 자세한 내용은 클라우드 공급자에 게 문의 해야 합니다. 또한 **VHD에서 부팅**하도록 구성 된 모든 Windows 서버에서 전체 업그레이드를 수행할 수 없습니다.

- **설치가.** "새로 설치" 라고도 합니다. 이전 버전의 운영 체제에서 최신 버전으로 이동 하 여 이전 버전의 운영 체제를 삭제 합니다.

- **마이그레이션이나.** 다른 하드웨어 또는 가상 컴퓨터 집합으로 전송 하 여 이전 버전의 운영 체제에서 최신 버전의 운영 체제로 이동 합니다.

- **클러스터 OS 롤링 업그레이드.** Hyper-v 또는 스케일 아웃 파일 서버 작업을 중지 하지 않고 클러스터 노드의 운영 체제를 업그레이드 합니다. 이 기능을 사용하면 서비스 수준 계약에 영향을 줄 수 있는 가동 중지 시간을 방지할 수 있습니다. 자세한 내용은 [클러스터 운영 체제 롤링 업그레이드](../failover-clustering/cluster-operating-system-rolling-upgrade.md) 를 참조 하세요.

- **라이선스 변환.** 간단한 명령과 적절 한 라이선스 키를 사용 하 여 단일 단계에서 특정 버전의 릴리스를 동일한 릴리스의 다른 버전으로 변환 합니다. "라이선스 변환" 이라고 합니다. 예를 들어 서버가 Windows Server 2016 Standard를 실행하는 경우 Windows Server 2016 Datacenter로 변환할 수 있습니다.

## <a name="which-version-of-windows-server-should-i-upgrade-to"></a>어떤 버전의 Windows Server를로 업그레이드 해야 하나요?

최신 버전의 Windows Server로 업그레이드 하는 것이 좋습니다. Windows Server 2019. 최신 버전의 Windows Server를 실행 하면 최신 보안 기능을 포함 하 여 최신 기능을 사용할 수 있으며 최상의 성능을 제공 합니다.

그러나 항상 가능 하지는 않습니다. 다음 다이어그램을 사용 하 여 현재 사용 중인 버전에 따라로 업그레이드할 수 있는 Windows Server 버전을 파악할 수 있습니다.

![사용 가능한 전체 업그레이드 경로](media/upgrade-paths.png)

Windows Server는 일반적으로 하나 이상의 버전을 통해 업그레이드할 수 있습니다. 예를 들어 windows server 2012 R2 및 Windows server 2016은 모두 Windows Server 2019로 바로 업그레이드할 수 있습니다.

운영 체제의 평가 버전에서 일반 정품 버전으로 업그레이드 하거나, 이전 일반 정품 버전에서 최신 버전으로 업그레이드 하거나, 경우에 따라 운영 체제의 볼륨 라이선스 버전을 일반 정품 버전으로 업그레이드할 수도 있습니다. 현재 위치의 업그레이드 이외의 업그레이드 옵션에 대 한 자세한 내용은 [Windows Server의 업그레이드 및 변환 옵션](../get-started/supported-upgrade-paths.md)을 참조 하십시오.
