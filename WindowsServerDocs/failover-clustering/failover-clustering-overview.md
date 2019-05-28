---
ms.assetid: c9844427-27cf-4d76-b5bb-e06368b092f7
title: 장애 조치(failover) 클러스터링
ms.prod: windows-server-threshold
layout: LandingPage
ms.topic: landing-page
ms.manager: dongill
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 03/08/2019
ms.localizationpriority: high
ms.openlocfilehash: 9e4184e52ef48e758ebc80e63d3d6f952a09cc2c
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222448"
---
# <a name="failover-clustering-in-windows-server"></a>Windows Server에서의 장애 조치 클러스터링

> 적용 대상: Windows Server 2019, Windows Server 2016

>[!TIP]
> 이전 버전의 Windows Server에 대한 자세한 내용이 궁금하십니까? docs.microsoft.com에서 다른 [Windows Server 라이브러리](/previous-versions/windows/)를 확인하세요. 또한 특정 정보에 대해 [이 사이트를 검색](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)할 수 있습니다.

<hr />

장애 조치(failover) 클러스터는 클러스터된 역할(이전의 클러스터된 응용 프로그램 및 서비스)의 사용 가능성과 확장성을 높이기 위해 함께 작동하는 독립 컴퓨터의 그룹입니다. 클러스터된 서버(노드라고 함)는 실제 케이블과 소프트웨어로 연결됩니다. 클러스터 노드 중 하나 이상에 장애가 발생하면 다른 노드에서 서비스를 제공하기 시작합니다. 이 프로세스를 장애 조치(failover)라고 합니다. 또한 클러스터된 역할을 사전에 모니터링하여 정상적으로 작동하는지 확인합니다. 클러스터된 역할이 작동하지 않는 경우 다시 시작되거나 다른 노드로 이동됩니다.

장애 조치(failover) 클러스터는 일관성 있는 분산 네임 스페이스를 제공하는 CSV(클러스터 공유 볼륨) 기능도 제공합니다. 이 네임스페이스는 클러스터된 역할이 모든 노드에서 공유 저장소에 액세스하는 데 사용할 수 있습니다. 장애 조치(failover) 클러스터링 기능을 사용하면 서비스 중단 기간을 최소화할 수 있습니다.

장애 조치 클러스터링은 다음과 같이 다수의 실용적 응용 프로그램을 포함하고 있습니다.
* Microsoft SQL Server 등의 응용 프로그램과 Hyper-V 가상 컴퓨터에 항상 사용할 수 있거나 지속적으로 사용할 수 있는 파일 공유 저장소
* Hyper-V를 실행하는 서버에 설치된 가상 컴퓨터 또는 실제 서버에서 실행되는 항상 사용할 수 있는 클러스터된 역할


|  |  |
|---------|---------|
|![새로운 기능](../media/i-whats-new.svg)  | [**장애 조치 클러스터링의 새로운 기능**](whats-new-in-failover-clustering.md) |


|  |  |  |
|---------|---------|---------|
|![이해](../media/i-cluster.svg)**이해**  |  ![계획](../media/i-cluster.svg)**계획**  |  ![배포](../media/i-cluster.svg)**배포**       |
| [애플리케이션 데이터용 스케일 아웃 파일 서버](sofs-overview.md)    |   [계획 장애 조치 클러스터링 하드웨어 요구 사항 및 저장소 옵션](clustering-requirements.md)      |  [Active Directory Domain Services에서 배포 사전 준비 된 클러스터 컴퓨터 개체](prestage-cluster-adds.md)  |
|  [클러스터 및 풀 쿼럼](../storage/storage-spaces/understand-quorum.md)   |   [CSV(클러스터 공유 볼륨) 사용](failover-cluster-csvs.md)      | [장애 조치 클러스터 만들기](create-failover-cluster.md)        |
|  [장애 도메인 인식](fault-domains.md)   |  [게스트 가상 컴퓨터 클러스터를 사용 하 여 저장소 공간 다이렉트를 사용 하 여](../storage/storage-spaces/storage-spaces-direct-in-vm.md)       | [2노드 파일 서버 배포](../storage/storage-spaces/storage-spaces-direct-in-vm.md)        |
| [간소화된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크](smb-multichannel.md)    |         |  [쿼럼 및 미러링 모니터 서버를 관리 합니다.](manage-cluster-quorum.md)       |
|   [VM 부하 분산](vm-load-balancing-overview.md)  |         |   [클라우드 감시 배포](deploy-cloud-witness.md)      |
|   [클러스터 세트](../storage/storage-spaces/cluster-sets.md)  |         |     [파일 공유 감시 배포](file-share-witness.md)    |
|   [클러스터 선호도](cluster-affinity.md)  |         |    [클러스터 운영 체제 롤링 업그레이드]()     |
|     |         |     [동일한 하드웨어에서 장애 조치 클러스터 업그레이드](upgrade-option-same-hardware.md)    |
|     |         |     [Active Directory 분리 클러스터 배포](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265970\(v%3dws.11\))    |


|  |  |  |
|---------|---------|---------|
|![관리](../media/i-cluster.svg)**관리**  |  ![도구 및 설정](../media/i-cluster.svg)**도구 및 설정**  |  ![커뮤니티 리소스](../media/i-cluster.svg)**커뮤니티 리소스**       |
| [클러스터 인식 업데이트](cluster-aware-updating.md)    |   [장애 조치 클러스터링 PowerShell Cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)      |  [고가용성(클러스터링) 포럼](https://go.microsoft.com/fwlink/p/?LinkId=230641)       |
|  [상태 관리 서비스](health-service-overview.md)   |   [클러스터 인식 업데이트 PowerShell Cmdlet](https://docs.microsoft.com/powershell/module/clusterawareupdating/?view=win10-ps)      | [장애 조치 클러스터링 및 네트워크 부하 분산 팀 블로그](http://blogs.msdn.com/b/clustering/)        |
|  [클러스터 도메인 마이그레이션](cluster-domain-migration.md)   |         |         |
|  [Windows 오류 보고를 사용하여 문제 해결 중](troubleshooting-using-wer-reports.md)   |         |         |
