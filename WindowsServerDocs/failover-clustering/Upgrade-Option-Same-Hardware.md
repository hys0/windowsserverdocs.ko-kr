---
title: 장애 조치 클러스터는 동일한 하드웨어를 사용 하 여 업그레이드
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 02/28/2019
description: 이 문서에서 설명 하는 동일한 하드웨어를 사용 하 여 2-노드 장애 조치 클러스터로 업그레이드
ms.localizationpriority: medium
ms.openlocfilehash: 0bfeb05c8cbc205745dc16bc7ef04052481668ea
ms.sourcegitcommit: 2c2027b597e2483eea8967d0710d65c2247b6751
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/01/2019
ms.locfileid: "9121325"
---
# 장애 조치 클러스터는 동일한 하드웨어에서 업그레이드

> 적용 대상: Windows Server 2019, Windows Server 2016

장애 조치 클러스터는 응용 프로그램 및 서비스의 가용성을 높이기 위해 함께 작동 하는 독립 컴퓨터 그룹입니다. 클러스터링된 서버(노드라고 함)는 실제 케이블과 소프트웨어로 연결됩니다. 클러스터 노드 중 하나에 실패 하면 다른 노드가 (즉, 장애 조치) 서비스를 제공 합니다. 사용자가 경험을 최소화할 서비스.

이 가이드에서는 클러스터 노드를 동일한 하드웨어를 사용 하 여 이전 버전에서 Windows Server 2019 또는 Windows Server 2016로 업그레이드 하는 단계를 설명 합니다.

## 개요

기존는 장애 조치에 운영 체제 업그레이드 클러스터만 지원 됩니다 Windows Server 2016에서 Windows 2019 하려는 경우.  장애 조치 클러스터는 이전 버전을 실행 하는 경우 등 같은 Windows Server 2012 R2 및 이전 버전에서는 클러스터 서비스 실행 되는 동안 업그레이드에서는 노드를 결합 합니다.  동일한 하드웨어를 사용 하는 경우 새 버전으로 가져오려면 단계를 가져올 수 있습니다.  

장애 조치 클러스터의 모든 업그레이드 하기 전에 [Windows 업그레이드 센터](https://www.microsoft.com/upgradecenter)를 참조 하세요.  장소에서 Windows Server를 업그레이드할 때 기존 운영 체제 버전에서을 옮기면를 보다 최근 릴리스로 동일한 하드웨어에서 합니다. 업그레이드 된 바로 하나 이상이 고 때로는 두 버전 앞으로 Windows Server 수 있습니다. 예를 들어 Windows Server 2012 R2 및 Windows Server 2016 업그레이드할 수 있는 Windows Server 2019로 적절 합니다.  또한 [클러스터 마이그레이션 마법사](https://blogs.msdn.microsoft.com/clustering/2012/06/25/how-to-move-highly-available-clustered-vms-to-windows-server-2012-with-the-cluster-migration-wizard/) 를 사용할 수 있지만 두 버전 다시 까지만 지원 되는 유지 합니다. 다음 그림에서는 Windows Server에 대 한 업그레이드 경로 보여 줍니다. 포인팅 아래쪽 화살표 이동 Windows Server 2019까지 이전 버전에서 지원 되는 업그레이드 경로 나타냅니다.

![바로 업그레이드 다이어그램](media\In-Place-Upgrade\In-Place-Upgrade-1.png)

다음 단계는 Windows Server 2012 장애 조치 클러스터 서버에서 동일한 하드웨어를 사용 하 여 Windows Server 2019 전환할의 예입니다.  

업그레이드를 시작 하기 전에 시스템 상태를 포함 하는 현재 백업이 완료 했는지 확인 하세요.  또한 모든 드라이버와 펌웨어를 사용 하는 운영 체제용 인증 된 수준으로 업데이트 되었습니다 있는지 확인 합니다.  이러한 두 노트 여기서 설명 하지 않습니다.

아래 예제에서 장애 조치 클러스터 이름은 클러스터 및 노드 이름의 노드 1 이며 노드 2.

## 1 단계: 첫 번째 노드를 제거 하 고 Windows Server 2016으로 업그레이드

1. 장애 조치 클러스터 관리자에서 마우스 오른쪽 노드를 클릭 하 고 **일시 중지** 및 **드레이닝 역할**을 선택 하 여 노드 2로 노드 1에서 모든 리소스를 소모 합니다.  또는 [일시 중단 CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)PowerShell 명령을 사용할 수 있습니다.

    ![드레인 노드](media\In-Place-Upgrade\In-Place-Upgrade-2.png)

2. 마우스 오른쪽 노드를 클릭 하 고 **기타 작업** 및 **제거**를 선택 하 여 클러스터에서 노드 1을 제거 합니다.  또는 [REMOVE-CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/remove-clusternode)PowerShell 명령을 사용할 수 있습니다.

    ![드레인 노드](media\In-Place-Upgrade\In-Place-Upgrade-3.png)

3. 조치로 노드 1을 사용 하는 저장소에서 분리 합니다.  경우에 따라 컴퓨터에서 저장소 케이블을 연결 끊기 만으로도 충분 합니다.  필요한 경우 적절 한 분리 단계에 대 한 저장소 공급 업체에 문의 있는지 확인 합니다.  저장소에 따라이 필요한 수 없습니다.

4. Windows Server 2016으로 노드 1을 다시 빌드하십시오.  모든 필요한 역할, 기능, 드라이버 및 보안 업데이트 추가한 확인 합니다.

5. 노드 1 사용 하 여 cluster1과 라는 새 클러스터를 만듭니다.  장애 조치 클러스터 관리자를 열고 **관리** 창에서 **클러스터 만들기** 선택한 마법사의 지침을 따릅니다.

    ![드레인 노드](media\In-Place-Upgrade\In-Place-Upgrade-4.png)

6. 클러스터를 만든 후이 새 클러스터에 원래 클러스터에서 마이그레이션할 수 역할 할 수 있습니다.  새 클러스터에서 클러스터 이름 (cluster1과) 및 선택 **기타 작업** 및 **복사 클러스터 역할**에 마우스 오른쪽 클릭 합니다.  역할 마이그레이션 마법사에서 진행 합니다.

    ![드레인 노드](media\In-Place-Upgrade\In-Place-Upgrade-5.png)

7.  모든 리소스를 마이그레이션한 후 노드 2 전원을 (원래 클러스터) / 방해 일으키지 하기 위해 저장소를 분리 합니다.  저장소 노드 1에 연결 합니다.  모두에 연결 되 면 모든 리소스를 온라인 및 해야 하는 대로 작동 하는지 확인 합니다.

## 2 단계: Windows Server 2019에 두 번째 노드를 다시 빌드하십시오.

모든 것이 예상 대로 작동을 확인 한 후 노드 2는 Windows Server 2019를 다시 작성 하 고 클러스터에 가입 수 있습니다.

1. 노드 2에서 Windows Server 2019의 새로 설치를 수행 합니다. 모든 필요한 역할, 기능, 드라이버 및 보안 업데이트 추가한 확인 합니다.

2. 원래 클러스터 (클러스터)이 사라진, 했으므로 cluster1과으로 새 클러스터 이름 하거나 원래 이름으로 다시 이동할 수 있습니다.  원래 이름으로 다시 이동 하려는 경우 다음이 단계를 따르세요.
   
   a. 노드 1 마우스 오른쪽 장애 조치 클러스터 관리자에서에서 클러스터 (cluster1과)의 이름을 클릭 하 고 **속성**을 선택 합니다.
   
   b. **일반** 탭에서 클러스터에 클러스터를 이름을 바꿉니다.

   c. 나타납니다 확인 또는 적용을 선택할 때의 팝업 대화 상자 아래 합니다.

    ![드레인 노드](media\In-Place-Upgrade\In-Place-Upgrade-6.png)

    d. 클러스터 서비스를 중지 하 고 완료 하는 데 이름 바꾸기 다시 시작 해야 하는 데 필요한 됩니다.

3. 노드 1에서 장애 조치 클러스터 관리자를 엽니다.  마우스 오른쪽 **노드** 를 클릭 하 고 **추가 노드**를 선택 합니다.  클러스터 노드 2에 추가 하 고 마법사를 진행 합니다.

4. 저장소 노드 2를 연결 합니다. 저장소 케이블을 다시 포함 될 수 있습니다. 

5. 마우스 오른쪽 노드를 클릭 하 고 **일시 중지** 및 **드레이닝 역할**을 선택 하 여 노드 2로 노드 1에서 모든 리소스를 소모 합니다.  또는 [일시 중단 CLUSTERNODE](https://docs.microsoft.com/powershell/module/failoverclusters/suspend-clusternode)PowerShell 명령을 사용할 수 있습니다.  모든 리소스는 온라인으로 작동 하는지 확인 합니다.

## 3 단계: Windows Server 2019를 첫 번째 노드를 다시 빌드하십시오.

1. 클러스터에서 노드 1을 제거 하 고 저장소에서 방식으로 노드에서 분리 어떤 하면 이전에 있습니다.

2. 빌드하거나 노드 1 Windows Server 2019로 업그레이드 합니다.  모든 필요한 역할, 기능, 드라이버 및 보안 업데이트 추가한 확인 합니다.

3. 저장소를 다시 연결 하 고 노드 1 클러스터 다시 추가 합니다.

4. 노드 1로 모든 리소스를 이동 하 고 온라인 상태로 전환 하 고 필요에 따라 작동 확인 합니다.

5. 현재 클러스터 기능 수준이 Windows 2016에 그대로 유지 됩니다.  기능 수준을 Windows 2019 [UPDATE-CLUSTERFUNCTIONALLEVEL](https://docs.microsoft.com/powershell/module/failoverclusters/update-clusterfunctionallevel)PowerShell 명령을 사용 하 여 업데이트 합니다.

이제 실행 하는 Windows Server 2019 장애 조치 클러스터 완벽 하 게 작동 합니다.

## 추가 참고 사항

- 앞에서 설명한 것 처럼 저장소 연결 끊기 수도 필요 없을 수도 있습니다.  이 설명서에서 주의 기울여 하려고 합니다.  저장소 공급 업체에 문의 하세요.
- 비용을 Windows Server 2008 또는 2008 R2 클러스터 이면의 단계를 사용 하는 추가 실행을 통해 필요할 수 있습니다.
- 클러스터에서 가상 컴퓨터를 실행 중인 경우 [업데이트 VMVERSION](https://docs.microsoft.com/powershell/module/hyper-v/update-vmversion)PowerShell 명령을 사용 하 여 클러스터 기능 수준이 완료 된 후 가상 컴퓨터 수준 업그레이드를 확인 합니다.
- SQL Server, Exchange 서버 등과 같은 응용 프로그램을 실행 하는 경우는 복사 클러스터 역할 마법사를 사용 하 여 응용 프로그램은 마이그레이션되지 않습니다 note 하세요.  응용 프로그램의 적절 한 마이그레이션 단계에 대 한 응용 프로그램 공급 업체에 문의 해야 합니다.