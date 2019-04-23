---
title: 동일한 하드웨어를 사용 하 여 장애 조치 클러스터 업그레이드
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: 이 문서는 동일한 하드웨어를 사용 하 여 2 노드 장애 조치 클러스터 업그레이드에 대해 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 0bfeb05c8cbc205745dc16bc7ef04052481668ea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854834"
---
# <a name="upgrading-failover-clusters-on-the-same-hardware"></a>동일한 하드웨어에서 장애 조치 클러스터 업그레이드

> 적용 대상: Windows Server 2019, Windows Server 2016

장애 조치(failover) 클러스터는 응용 프로그램 및 서비스의 가용성을 높이기 위해 함께 작동하는 독립적인 컴퓨터 그룹입니다. 클러스터된 서버(노드라고 함)는 실제 케이블과 소프트웨어로 연결됩니다. 클러스터 노드 중 하나가 실패하면 다른 노드에서 서비스(장애 조치로 알려진 프로세스)를 제공하기 시작합니다. 서비스 중단을 최소화할 수 있습니다.

이 가이드에는 동일한 하드웨어를 사용 하 여 이전 버전에서 클러스터 노드에서 Windows Server 2019 또는 Windows Server 2016로 업그레이드 하기 위한 단계를 설명 합니다.

## <a name="overview"></a>개요

클러스터는 기존 장애 조치 시 운영 체제를 업그레이드 경우 Windows Server 2016에서 Windows 2019 에서만 있습니다.  장애 조치 클러스터는 이전 버전을 실행 하는 경우 등 Windows Server 2012 R2와 같은 및 이전 버전에서는 클러스터 서비스가 실행 되는 동안 업그레이드에서는 노드를 함께 조인 합니다.  동일한 하드웨어를 사용 하는 경우 최신 버전에 단계를 수행할 수 있습니다.  

장애 조치 클러스터의 업그레이드를 참조 하십시오 합니다 [Windows 업그레이드 Center](https://www.microsoft.com/upgradecenter)합니다.  위치에서 Windows Server를 업그레이드할 때 이동할 있습니다 기존 운영 체제 버전에서 동일한 하드웨어 사용 하면서 최신 릴리스. Windows Server 업그레이드 원위치에서 하나 이상의 경우에 따라 두 가지 버전 앞으로 수 있습니다. Windows Server 2012 R2 및 Windows Server 2016 업그레이드할 수 있습니다 예를 들어, Windows Server 2019로 해당 위치에서.  또한에 유의 합니다 [클러스터 마이그레이션 마법사](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/) 사용할 수 있지만 두 가지 버전 다시 최대 에서만 지원 됩니다. 다음 그림에는 Windows Server에 대 한 업그레이드 경로 보여 줍니다. 아래쪽 가리키는 화살표는 Windows Server 2019까지 이전 버전에서 이동 하 여 지원 되는 업그레이드 경로 나타냅니다.

![현재 위치 업그레이드 다이어그램](media\In-Place-Upgrade\In-Place-Upgrade-1.png)

다음 단계는 Windows Server 2012 장애 조치 클러스터 서버에서 동일한 하드웨어를 사용 하 여 Windows Server 2019 것인지의 예입니다.  

업그레이드를 시작 하기 전에 시스템 상태를 포함 하 여 현재 백업 완료 되었는지 확인 하세요.  또한 사용 하려는 운영 체제에 대 한 인증 된 수준으로 업데이트 되었습니다 모든 드라이버 및 펌웨어를 확인 합니다.  이 두 정보는 수 여기에서 다루지 않습니다.

아래 예제에서는 장애 조치 클러스터의 이름은 클러스터 및 노드 이름에는 NODE1과 NODE2 합니다.

## <a name="step-1-evict-first-node-and-upgrade-to-windows-server-2016"></a>1단계: 첫 번째 노드를 제거 하 고 Windows Server 2016으로 업그레이드

1. 장애 조치 클러스터 관리자를 마우스 오른쪽 노드를 클릭 하 고 선택 하 여 NODE2로 NODE1에서 모든 리소스를 드레이닝 **일시 중지** 하 고 **역할 드레이닝**합니다.  또는 PowerShell 명령을 사용할 수 있습니다 [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)합니다.

    ![노드 드레이닝](media\In-Place-Upgrade\In-Place-Upgrade-2.png)

2. 오른쪽 마우스 단추로 노드를 클릭 하 고 선택 하 여 클러스터에서 노드 1을 제거 **기타 작업** 하 고 **제거**합니다.  또는 PowerShell 명령을 사용할 수 있습니다 [제거 노드](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode)합니다.

    ![노드 드레이닝](media\In-Place-Upgrade\In-Place-Upgrade-3.png)

3. 예방 조치로 사용 하는 저장소에서 NODE1를 분리 합니다.  경우에 따라 컴퓨터에서 저장소 케이블을 연결 끊기 만으로도 충분 합니다.  필요한 경우 적절 한 분리 단계에 대 한 저장소 공급 업체에 확인 합니다.  저장소에 따라이 필요한 수 없습니다.

4. Windows Server 2016 사용 하 여 노드 1을 다시 작성 합니다.  추가한 모든 필요한 역할, 기능, 드라이버 및 보안 업데이트를 확인 합니다.

5. Node1 CLUSTER1 라는 새 클러스터를 만듭니다.  장애 조치 클러스터 관리자를 열고 및 합니다 **관리** 창 선택 **클러스터 만들기** 마법사의 지침을 따릅니다.

    ![노드 드레이닝](media\In-Place-Upgrade\In-Place-Upgrade-4.png)

6. 클러스터를 만든 후 역할 원본 클러스터에서이 새 클러스터로 마이그레이션할 수 해야 합니다.  새 클러스터에서 마우스 오른쪽 단추로 (CLUSTER1) 클러스터 이름을 클릭 하 고 선택 **기타 작업** 하 고 **클러스터 역할 복사**합니다.  역할 마이그레이션 마법사에서 수행 합니다.

    ![노드 드레이닝](media\In-Place-Upgrade\In-Place-Upgrade-5.png)

7.  모든 리소스를 마이그레이션한 후 NODE2 전원을 (원래 클러스터) 및 간섭을 일으키지 하도록 저장소를 분리 합니다.  NODE1에 저장소를 연결 합니다.  모든 연결 되 면 모든 리소스를 온라인 상태로 전환 후와 마찬가지로 작동 하는지 확인 합니다.

## <a name="step-2-rebuild-second-node-to-windows-server-2019"></a>2단계: Windows Server 2019에 두 번째 노드를 다시 작성

모든 항목이 예상 대로 작동을 확인 한 후 노드 2는 Windows Server 2019를 다시 작성 하 고 클러스터에 조인할 수 있습니다.

1. 노드 2에서 Windows Server 2019 새로 설치를 수행 합니다. 추가한 모든 필요한 역할, 기능, 드라이버 및 보안 업데이트를 확인 합니다.

2. 이제 원래 클러스터 (클러스터)을 삭제 했으므로 CLUSTER1 클러스터 이름을 새 수도 있고 원래 이름을 다시 이동할 수 있습니다.  원래 이름으로 다시 이동 하려는 경우 다음이 단계를 수행 합니다.
   
   a. 노드 1에서 마우스 오른쪽 장애 조치 클러스터 관리자에서에서 (CLUSTER1) 클러스터의 이름을 클릭 하 고 선택 **속성**합니다.
   
   b. 에 **일반** 탭에서 클러스터에 클러스터 이름을 바꿉니다.

   다. 확인 또는 적용을 선택 하면 나타납니다는 아래 팝업 대화 상자.

    ![노드 드레이닝](media\In-Place-Upgrade\In-Place-Upgrade-6.png)

    d. 클러스터 서비스를 중지 하 고 완료 하려면 이름을 바꾸려면 다시 시작 하는 데 필요한 됩니다.

3. 노드 1에서 장애 조치 클러스터 관리자를 엽니다.  마우스 오른쪽 단추로 클릭 **노드가** 선택한 **노드 추가**합니다.  NODE2 클러스터에 추가 마법사를 진행 합니다.

4. NODE2로 저장소를 연결 합니다. 이 저장소 케이블 다시 연결을 포함할 수 있습니다. 

5. 마우스 오른쪽 노드를 클릭 하 고 선택 하 여 NODE2로 NODE1에서 모든 리소스를 드레이닝 **일시 중지** 하 고 **역할 드레이닝**합니다.  또는 PowerShell 명령을 사용할 수 있습니다 [SUSPEND-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)합니다.  모든 리소스가 온라인 상태이 고 해야 하는 대로 작동 하는지 확인 합니다.

## <a name="step-3-rebuild-first-node-to-windows-server-2019"></a>3단계: Windows Server 2019에 첫 번째 노드를 다시 작성

1. 클러스터에서 노드 1을 제거 하 고에서 방식 노드에서 저장소 연결을 끊을 수 있는 이전에 있습니다.

2. 다시 작성 하거나 Windows Server 2019 NODE1 업그레이드 합니다.  추가한 모든 필요한 역할, 기능, 드라이버 및 보안 업데이트를 확인 합니다.

3. 저장소를 다시 연결 하 고 클러스터에 다시 노드 1을 추가 합니다.

4. Node1에서 모든 리소스를 이동 하 고 온라인 상태로 전환 하며 필요에 따라 함수를 확인 합니다.

5. 현재 클러스터 기능 수준을 Windows 2016에 그대로 유지 됩니다.  PowerShell 명령을 사용 하 여 Windows 2019에 기능 수준을 업데이트 [UPDATE-CLUSTERFUNCTIONALLEVEL](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel)합니다.

이제 모든 기능을 갖춘 Windows Server 2019 장애 조치 클러스터를 사용 하 여 실행 중인 있습니다.

## <a name="additional-notes"></a>추가 참고 사항

- 앞에서 설명한 대로 저장소 연결을 끊는 중 수도 필요가 없을 수 있습니다.  설명서에서 매우 주의 기울여 하고자 합니다.  저장소 공급 업체에 문의 하세요.
- 시작 지점부터 Windows Server 2008 또는 2008 R2 클러스터 인 경우 단계를 통해 추가 실행을 필요할 수 있습니다.
- 클러스터는 가상 컴퓨터를 실행 하는 경우 클러스터 기능 수준을 PowerShell 명령을 사용 하 여 완료 된 후 가상 머신 수준 업그레이드 되도록 [업데이트 VMVERSION](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)합니다.
- SQL Server, Exchange Server 등 응용 프로그램을 실행 하는 경우는 클러스터 역할 복사 마법사를 사용 하 여 응용 프로그램은 마이그레이션되지 않습니다 note 하십시오.  응용 프로그램의 적절 한 마이그레이션 단계에 대 한 응용 프로그램 공급 업체를 참조 하십시오.