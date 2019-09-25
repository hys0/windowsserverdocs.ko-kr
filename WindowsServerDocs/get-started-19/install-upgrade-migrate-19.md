---
title: Windows Server 2019 설치, 업그레이드 또는 마이그레이션
description: Windows Server를 새로 설치하거나, 현재 위치에서 업그레이드하거나 이 버전으로 마이그레이션하는 방법
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4e99cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 1c0c6ca10e7ebac16d81fe1393e471a7878fd0ca
ms.sourcegitcommit: ccec91c1d32a978159f9b8bb5e39ead5805c26c4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/19/2019
ms.locfileid: "71143754"
---
# <a name="install-upgrade-or-migrate-to-windows-server"></a>Windows Server 설치, 업그레이드 또는 마이그레이션

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008

> [!IMPORTANT]
> Windows Server 2008 R2 및 Windows Server 2008에 대한 연장 지원이 2020년 1월에 종료됩니다. [업그레이드 옵션에 대한 자세한 정보](http://aka.ms/upgradecenter) Windows Server 2019를 다운로드하려면 [Windows Server 평가판](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)을 참조하세요.

Windows Server 새 버전으로 전환할 시점입니까? 현재 실행하는 버전에 따라 다양한 옵션을 사용할 수 있습니다.

## <a name="clean-install"></a>새로 설치

Windows Server를 설치하는 가장 간단한 방법은 빈 서버에 설치하거나 기존 운영 체제를 덮어쓰는 새로 설치를 수행하는 것입니다. 가장 간단한 방법이지만 먼저 데이터를 백업하고 나중에 애플리케이션을 재설치할 계획을 세워야 합니다. 시스템 요구 사항 등과 같이 미리 알아야 할 사항들이 몇 가지 있으니 [Windows Server 2019](https://go.microsoft.com/fwlink/?linkid=2006124), [Windows Server 2016](https://go.microsoft.com/fwlink/?LinkID=825558), [Windows Server 2012 R2](https://technet.microsoft.com/library/dn303418) 및 [Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx) 등의 세부 사항을 반드시 확인하시기 바랍니다.

## <a name="in-place-upgrade"></a>현재 위치 업그레이드

서버를 평면화하지 않으면서 설정한 동일한 하드웨어 및 모든 서버 역할을 유지하려면 **현재 위치 업그레이드**를 수행하여 설정, 서버 역할 및 데이터는 그대로 두면서 이전 운영 체제에서 새 버전으로 전환합니다. 예를 들어, 서버에서 Windows Server 2012 R2를 실행하는 경우 Windows Server 2016 또는 Windows Server 2019로 업그레이드할 수 있습니다. 그러나 모든 기존 운영 체제가 모든 새 운영 체제로 업그레이드될 수 있는 것은 아닙니다. 

업그레이드에 대한 단계별 지침은 [Windows Server 업그레이드 콘텐츠](../upgrade/upgrade-overview.md)를 검토하세요.

## <a name="cluster-os-rolling-upgrade"></a>클러스터 OS 롤링 업그레이드

클러스터 운영 체제 롤링 업그레이드로 관리자는 Hyper-V 또는 스케일 아웃 파일 서버 워크로드를 중지하지 않고 클러스터 노드의 운영 체제를 Windows Server 2012 R2 및 Windows Server 2016에서 업그레이드할 수 있습니다. 이 기능을 사용하면 서비스 수준 계약에 영향을 줄 수 있는 가동 중지 시간을 방지할 수 있습니다. 이 새로운 기능은 [클러스터 운영 체제 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)에 자세히 설명되어 있습니다.

## <a name="migration"></a>마이그레이션

Windows Server 마이그레이션은 Windows Server를 실행하는 원본 컴퓨터로부터 동일 버전 또는 새 버전의 Windows Server를 실행하는 다른 대상 컴퓨터로 역할 또는 기능을 한 번에 하나씩 이동하는 경우를 나타냅니다. 이와 같은 목적일 때 마이그레이션은 동일한 컴퓨터에서 기능을 업그레이드하는 작업이 아니라 하나의 역할 또는 기능과 그 데이터를 다른 컴퓨터로 옮기는 작업으로 정의됩니다. 

## <a name="license-conversion"></a>라이선스 변환

일부 운영 체제 릴리스에서는 해당 릴리스의 특정 버전을 간단한 명령과 적절한 라이선스 키만으로 동일한 릴리스의 다른 버전으로 한 번에 변환할 수 있습니다. 이를 **라이선스 변환**이라고 합니다. 예를 들어 서버가 Windows Server 2016 Standard를 실행하는 경우 Windows Server 2016 Datacenter로 변환할 수 있습니다. Server 2016 Standard에서 Server 2016 Datacenter로 전환할 수 있지만 이 프로세스를 되돌려 Datacenter에서 Standard로 전환할 수 없습니다. 또한 일부 Windows Server 릴리스에서는 동일한 명령과 적절한 키를 이용하여 OEM, 볼륨 라이선스 및 일반 정품 버전 사이에서 자유롭게 변환할 수도 있습니다.