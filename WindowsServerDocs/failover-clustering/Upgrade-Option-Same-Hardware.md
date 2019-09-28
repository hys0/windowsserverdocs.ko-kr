---
title: 동일한 하드웨어를 사용 하 여 장애 조치 (Failover) 클러스터 업그레이드
ms.prod: windows-server
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: 이 문서에서는 동일한 하드웨어를 사용 하는 2 노드 장애 조치 (Failover) 클러스터 업그레이드에 대해 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 5fe93f1d43e0c3a1bc4269b585cb9d021d3461aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361403"
---
# <a name="upgrading-failover-clusters-on-the-same-hardware"></a>동일한 하드웨어에서 장애 조치 (Failover) 클러스터 업그레이드

> 적용 대상: Windows Server 2019, Windows Server 2016

장애 조치(failover) 클러스터는 응용 프로그램 및 서비스의 가용성을 높이기 위해 함께 작동하는 독립적인 컴퓨터 그룹입니다. 클러스터된 서버(노드라고 함)는 실제 케이블과 소프트웨어로 연결됩니다. 클러스터 노드 중 하나가 실패하면 다른 노드에서 서비스(장애 조치로 알려진 프로세스)를 제공하기 시작합니다. 사용자는 최소한의 서비스 중단을 경험 합니다.

이 가이드에서는 동일한 하드웨어를 사용 하 여 이전 버전에서 windows Server 2019 또는 Windows Server 2016로 클러스터 노드를 업그레이드 하는 단계에 대해 설명 합니다.

## <a name="overview"></a>개요

기존 장애 조치 (failover) 클러스터에서 운영 체제를 업그레이드 하는 것은 Windows Server 2016에서 Windows 2019로 이동 하는 경우에만 지원 됩니다.  장애 조치 (failover) 클러스터가 Windows Server 2012 R2이 하 버전 등의 이전 버전을 실행 하는 경우 클러스터 서비스가 실행 되는 동안 업그레이드 하는 것은 노드를 함께 연결 하는 것을 허용 하지 않습니다.  동일한 하드웨어를 사용 하는 경우 단계를 수행 하 여 최신 버전으로 가져올 수 있습니다.  

장애 조치 (failover) 클러스터를 업그레이드 하기 전에 [Windows Server 업그레이드 콘텐츠](../upgrade/upgrade-overview.md)를 참조 하세요.  현재 위치에서 Windows Server를 업그레이드 하는 경우 동일한 하드웨어를 유지 하면서 기존 운영 체제 릴리스를 최신 릴리스로 이동 합니다. Windows Server는 하나 이상의 위치에서 업그레이드할 수 있으며, 경우에 따라 두 가지 버전이 전달 됩니다. 예를 들어 windows server 2012 R2 및 Windows server 2016은 Windows Server 2019로 바로 업그레이드할 수 있습니다.  또한 [클러스터 마이그레이션 마법사](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/) 는 사용할 수 있지만 최대 두 버전 에서만 지원 됩니다. 다음 그림은 Windows Server에 대 한 업그레이드 경로를 보여 줍니다. 아래쪽 화살표는 이전 버전에서 Windows Server 2019로 이동 하는 지원 되는 업그레이드 경로를 나타냅니다.

![내부 업그레이드 다이어그램](media/In-Place-Upgrade/In-Place-Upgrade-1.png)

다음 단계는 동일한 하드웨어를 사용 하 여 Windows Server 2012 장애 조치 (failover) 클러스터 서버에서 Windows Server 2019로 이동 하는 예입니다.  

업그레이드를 시작 하기 전에 시스템 상태를 포함 하 여 현재 백업이 수행 되었는지 확인 하세요.  또한 사용할 운영 체제에 대 한 모든 드라이버 및 펌웨어가 인증 된 수준으로 업데이트 되었는지 확인 합니다.  이러한 두 노트는 여기에서 다루지 않습니다.

아래 예에서는 장애 조치 (failover) 클러스터의 이름이 CLUSTER이 고 노드 이름은 NODE1 및 노드 2입니다.

## <a name="step-1-evict-first-node-and-upgrade-to-windows-server-2016"></a>1단계: 첫 번째 노드를 제거 하 고 Windows Server 2016로 업그레이드

1. 장애 조치(Failover) 클러스터 관리자에서 노드를 마우스 오른쪽 단추로 클릭 하 고 **일시 중지** 및 **드레이닝 역할**을 선택 하 여 NODE1에서 노드 2로 모든 리소스를 드레이닝 합니다.  또는 PowerShell 명령 [start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)를 사용할 수 있습니다.

    ![드레이닝 노드](media/In-Place-Upgrade/In-Place-Upgrade-2.png)

2. 노드를 마우스 오른쪽 단추로 클릭 하 고 **추가 작업** 및 **제거**를 선택 하 여 클러스터에서 NODE1을 제거 합니다.  또는 PowerShell 명령 [start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode)를 사용할 수 있습니다.

    ![드레이닝 노드](media/In-Place-Upgrade/In-Place-Upgrade-3.png)

3. 예방 조치로 사용 하는 저장소에서 NODE1을 분리 합니다.  경우에 따라 컴퓨터에서 저장소 케이블을 분리 해도 충분 합니다.  필요한 경우 저장소 공급 업체에 적절 한 분리 단계가 있는지 확인 합니다.  저장소에 따라이 작업이 필요 하지 않을 수 있습니다.

4. Windows Server 2016를 사용 하 여 NODE1을 다시 빌드합니다.  필요한 모든 역할, 기능, 드라이버 및 보안 업데이트를 추가 했는지 확인 합니다.

5. NODE1로 CLUSTER1 이라는 새 클러스터를 만듭니다.  장애 조치(Failover) 클러스터 관리자를 열고 **관리** 창에서 **클러스터 만들기** 를 선택 하 고 마법사의 지시를 따릅니다.

    ![드레이닝 노드](media/In-Place-Upgrade/In-Place-Upgrade-4.png)

6. 클러스터가 만들어지면 역할은 원래 클러스터에서이 새 클러스터로 마이그레이션해야 합니다.  새 클러스터에서 클러스터 이름 (CLUSTER1)을 마우스 오른쪽 단추로 클릭 하 고 **추가 작업** 을 선택 하 고 **클러스터 역할을 복사**합니다.  마법사의 지침에 따라 역할을 마이그레이션합니다.

    ![드레이닝 노드](media/In-Place-Upgrade/In-Place-Upgrade-5.png)

7.  모든 리소스를 마이그레이션한 후에는 노드 2 (원래 클러스터)의 전원을 끄고 간섭을 발생 시 키 지 않도록 저장소의 연결을 끊습니다.  저장소를 NODE1에 연결 합니다.  모든 리소스를 연결한 후에는 모든 리소스를 온라인으로 전환 하 고이를 정상적으로 작동 하는지 확인 합니다.

## <a name="step-2-rebuild-second-node-to-windows-server-2019"></a>2단계: Windows Server 2019에 두 번째 노드 다시 빌드

모든 것이 제대로 작동 하는지 확인 한 후에는 노드 2를 Windows Server 2019로 다시 작성 하 고 클러스터에 조인할 수 있습니다.

1. 노드 2에서 Windows Server 2019를 새로 설치 합니다. 필요한 모든 역할, 기능, 드라이버 및 보안 업데이트를 추가 했는지 확인 합니다.

2. 이제 원래 클러스터 (클러스터)가 없어졌으므로 새 클러스터 이름을 CLUSTER1로 두거나 원래 이름으로 돌아갈 수 있습니다.  원래 이름으로 돌아가려면 다음 단계를 수행 합니다.
   
   a. 노드 1에서 장애 조치(Failover) 클러스터 관리자 마우스 오른쪽 단추로 클러스터의 이름 (CLUSTER1)을 클릭 하 고 **속성**을 선택 합니다.
   
   b. **일반** 탭에서 클러스터의 이름을 클러스터로 바꿉니다.

   c. 확인 또는 적용을 선택 하면 아래 대화 상자 팝업이 표시 됩니다.

    ![드레이닝 노드](media/In-Place-Upgrade/In-Place-Upgrade-6.png)

    d. 클러스터 서비스가 중지 되 고 이름 바꾸기를 완료 하기 위해 다시 시작 해야 합니다.

3. 노드 1에서 장애 조치(Failover) 클러스터 관리자를 엽니다.  마우스 오른쪽 단추로 **노드** 를 클릭 하 고 **노드 추가**를 선택 합니다.  클러스터에 노드 2를 추가 하는 마법사를 진행 합니다.

4. 저장소를 노드 2에 연결 합니다. 여기에는 저장소 케이블을 다시 연결 하는 작업이 포함 될 수 있습니다. 

5. 노드를 마우스 오른쪽 단추로 클릭 하 고 **일시 중지** 및 **드레이닝 역할**을 선택 하 여 NODE1에서 노드 2까지 모든 리소스를 드레이닝 합니다.  또는 PowerShell 명령 [start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)를 사용할 수 있습니다.  모든 리소스가 온라인 상태이 고 제대로 작동 하는지 확인 합니다.

## <a name="step-3-rebuild-first-node-to-windows-server-2019"></a>3단계: Windows Server 2019에 대 한 첫 번째 노드 다시 빌드

1. 클러스터에서 NODE1을 제거 하 고 이전에 만든 방식으로 노드에서 저장소의 연결을 끊습니다.

2. 노드 1을 Windows Server 2019로 다시 빌드하거나 업그레이드 합니다.  필요한 모든 역할, 기능, 드라이버 및 보안 업데이트를 추가 했는지 확인 합니다.

3. 저장소를 다시 연결 하 고 클러스터에 NODE1을 다시 추가 합니다.

4. 모든 리소스를 NODE1로 이동 하 여 온라인 상태로 전환 하 고 필요에 따라 작동 하는지 확인 합니다.

5. 현재 클러스터 기능 수준은 Windows 2016에 그대로 남아 있습니다.  PowerShell 명령 [CLUSTERFUNCTIONALLEVEL](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel)을 사용 하 여 기능 수준을 Windows 2019으로 업데이트 합니다.

이제 완벽 하 게 작동 하는 Windows Server 2019 장애 조치 (Failover) 클러스터로 실행 됩니다.

## <a name="additional-notes"></a>추가 참고 사항

- 앞에서 설명한 것 처럼 저장소 연결이 끊어질 수도 있고 필요 하지 않을 수도 있습니다.  이 설명서에서는 주의를 기울여야 합니다.  저장소 공급 업체에 문의 하세요.
- 시작 지점이 Windows Server 2008 또는 2008 R2 클러스터 인 경우 단계를 추가로 실행 해야 할 수 있습니다.
- 클러스터가 가상 컴퓨터를 실행 하 고 있는 경우 PowerShell 명령 [업데이트-VMVERSION](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)을 사용 하 여 클러스터 기능 수준을 완료 한 후 가상 컴퓨터 수준을 업그레이드 해야 합니다.
- SQL Server, Exchange Server 등의 응용 프로그램을 실행 하는 경우 응용 프로그램은 클러스터 역할 복사 마법사를 사용 하 여 마이그레이션되지 않습니다.  응용 프로그램의 적절 한 마이그레이션 단계는 응용 프로그램 공급 업체에 문의 해야 합니다.