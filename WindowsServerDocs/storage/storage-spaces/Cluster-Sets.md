---
title: 클러스터 집합
ms.prod: windows-server
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 01/30/2019
description: 이 문서에서는 클러스터 집합 시나리오에 대해 설명 합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 484b6a1e658cd5c0583747194fa42494e54c3301
ms.sourcegitcommit: 4824f3b307e5b8b9bf5be7bc948f7aba9cf7063f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/29/2020
ms.locfileid: "82579936"
---
# <a name="cluster-sets"></a>클러스터 세트

> 적용 대상: 시작

클러스터 집합은 단일 소프트웨어 정의 데이터 센터 (SDDC) 클라우드에서 크기의 순서로 클러스터 노드 수를 늘리는 Windows Server 2019 릴리스의 새로운 클라우드 스케일 아웃 기술입니다. 클러스터 집합은 여러 장애 조치 (Failover) 클러스터 (계산, 저장소 또는 하이퍼 수렴)의 느슨하게 결합 된 그룹입니다. 클러스터 집합 기술은 클러스터 집합 내의 구성원 클러스터와 가상 컴퓨터 fluidity의 지원에 대 한 통합 저장소 네임 스페이스 간에 가상 컴퓨터를 fluidity 수 있도록 합니다.

구성원 클러스터에서 기존 장애 조치 (Failover) 클러스터 관리 환경을 유지 하는 동안 클러스터 집합 인스턴스는 집계에서 수명 주기 관리와 관련 된 주요 사용 사례를 추가로 제공 합니다. 이 Windows Server 2019 시나리오 평가 가이드에서는 PowerShell을 사용 하 여 클러스터 집합 기술을 평가 하는 단계별 지침과 함께 필요한 배경 정보를 제공 합니다.

## <a name="technology-introduction"></a>기술 소개

클러스터 집합 기술은 대규모 SDDC (소프트웨어 정의 데이터 센터) 클라우드를 운영 하는 특정 고객 요청을 충족 하도록 개발 되었습니다. 클러스터 집합 값 제안을 다음과 같이 요약할 수 있습니다.  

- 소프트웨어 장애 경계를 단일 클러스터로 유지 하면서 여러 개의 작은 클러스터를 하나의 큰 패브릭에 결합 하 여 항상 사용 가능한 가상 컴퓨터를 실행 하는 데 지원 되는 SDDC 클라우드 규모를 크게 증가 시킵니다.
- 이 큰 패브릭에 대 한 가상 컴퓨터 유동적으로을 통해 테 넌 트 가상 컴퓨터의 가용성에 영향을 주지 않고 클러스터 온 보 딩 및 사용 중지를 포함 하 여 전체 장애 조치 클러스터 수명 주기
- 하이퍼 수렴 형 I에서 계산-저장소 비율을 쉽게 변경
- 초기 가상 머신 배치 및 후속 가상 머신 마이그레이션 시 클러스터에서 [Azure와 같은 장애 도메인 및 가용성 집합](htttps://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) 혜택
- 개별 장애 도메인을 최대 효율성을 위해 동일 하 게 유지 하는 동시에 다양 한 CPU 하드웨어 세대를 동일한 클러스터 세트 패브릭에 대조 하 고 일치 시킵니다.  동일한 하드웨어의 권장 사항은 전체 클러스터 집합 뿐만 아니라 각 개별 클러스터 내에도 표시 됩니다.

상위 수준 보기에서 볼 수 있는 클러스터 집합은 다음과 같습니다.

![클러스터 집합 솔루션 뷰](media/Cluster-sets-Overview/Cluster-sets-solution-View.png)

다음에서는 위의 이미지에 있는 각 요소에 대 한 간략 한 요약을 제공 합니다.

**관리 클러스터**

클러스터 집합의 관리 클러스터는 전체 클러스터 집합 및 통합 저장소 네임 스페이스 (클러스터 집합 네임 스페이스) 조회 스케일 아웃 파일 서버 (SOFS)의 항상 사용 가능한 관리 평면을 호스트 하는 장애 조치 (Failover) 클러스터입니다. 관리 클러스터는 가상 머신 워크 로드를 실행 하는 구성원 클러스터와 논리적으로 분리 됩니다. 이렇게 하면 클러스터 집합 관리 평면이 클러스터 전체 오류 (예: 구성원 클러스터의 기능 손실)에 탄력적으로 복원 됩니다.   

**구성원 클러스터**

클러스터 집합의 구성원 클러스터는 일반적으로 가상 컴퓨터를 실행 하는 기존 하이퍼 수렴 형 클러스터 이며 작업 스토리지 공간 다이렉트 합니다. 여러 구성원 클러스터는 단일 클러스터 집합 배포에 참여 하 여 더 큰 SDDC 클라우드 패브릭을 형성 합니다. 구성원 클러스터는 두 가지 주요 측면에서 관리 클러스터와 다릅니다. 구성원 클러스터는 장애 도메인 및 가용성 집합 구문에 참여 하 고, 가상 컴퓨터를 호스트 하 고 작업을 스토리지 공간 다이렉트 하는 데에도 구성원 클러스터의 크기가 조정 됩니다. 이러한 이유로 클러스터 집합에서 클러스터 경계를 넘어 이동 하는 클러스터 집합 가상 머신은 관리 클러스터에서 호스트 되지 않아야 합니다.

**클러스터 집합 네임 스페이스 조회 SOFS**

클러스터 집합 네임 스페이스 조회 (클러스터 집합 네임 스페이스) SOFS는 클러스터 집합 네임 스페이스 SOFS의 각 SMB 공유가 Windows Server 2019에 새로 도입 된 ' SimpleReferral ' 형식의 조회 공유 인 스케일 아웃 파일 서버입니다. 이 조회를 통해 SMB (서버 메시지 블록) 클라이언트가 구성원 클러스터 SOFS 호스트 되는 대상 SMB 공유에 액세스할 수 있습니다. 클러스터 집합 네임 스페이스 조회 SOFS는 경량 조회 메커니즘 이므로 i/o 경로에 참여 하지 않습니다. SMB 조회는 각 클라이언트 노드에서 캐시 된 영구적으로 클러스터는 필요에 따라 동적으로 이러한 조회를 업데이트 합니다.

**클러스터 세트 마스터**

클러스터 집합에서 구성원 클러스터 간의 통신은 느슨하게 결합 되며 "Cluster Set Master" (CS-Master) 라는 새 클러스터 리소스에 의해 조정 됩니다. 다른 클러스터 리소스와 마찬가지로, CS-마스터는 항상 사용 가능 하며 개별 구성원 클러스터 오류 및/또는 관리 클러스터 노드 오류에 대 한 복원 력이 높습니다. 새 클러스터 집합 WMI 공급자를 통해 CS-마스터는 모든 클러스터 집합 관리 효율성 상호 작용에 대 한 관리 끝점을 제공 합니다.

**클러스터 집합 작업자**

클러스터 집합 배포에서 CS-마스터는 "Cluster Set Worker" (CS-Worker) 라는 구성원 클러스터의 새 클러스터 리소스와 상호 작용 합니다. CS-작업자는 CS-마스터에서 요청 하는 대로 로컬 클러스터 상호 작용을 오케스트레이션 하는 클러스터의 유일한 소유 역할을 합니다. 이러한 상호 작용의 예로는 가상 머신 배치 및 클러스터 로컬 리소스 인벤토리를 들 수가 있습니다. 클러스터 집합의 각 구성원 클러스터에 대 한 CS 작업자 인스턴스는 하나 뿐입니다. 

**장애 도메인**

장애 도메인은 오류가 발생 했을 때 관리자가 함께 장애 조치할 수 있는 소프트웨어 및 하드웨어 아티팩트의 그룹입니다.  관리자가 하나 이상의 클러스터를 장애 도메인으로 지정할 수 있지만 각 노드는 가용성 집합의 장애 도메인에 참여할 수 있습니다. 설계상의 클러스터 집합은 데이터 센터 토폴로지 고려 사항 (예: PDU, 네트워킹 – 구성원 클러스터가 공유 됨)을 잘 익숙한 관리자에 게 장애 도메인 경계 결정을 내려야 합니다. 

**가용성 집합**

가용성 집합을 사용 하면 관리자가 장애 도메인 전체에서 클러스터 된 작업의 원하는 중복성을 구성할 수 있습니다 .이를 가용성 집합으로 구성 하 고 해당 가용성 집합에 워크 로드를 배포 합니다. 2 계층 응용 프로그램을 배포 하는 경우 각 계층에 대 한 가용성 집합에 두 개 이상의 가상 컴퓨터를 구성 하는 것이 좋습니다. 그러면 해당 가용성 집합의 장애 도메인 하나가 다운 될 때 응용 프로그램에는 동일한 가용성 집합의 다른 장애 도메인에 호스트 된 각 계층에 가상 컴퓨터가 하나 이상 포함 됩니다.

## <a name="why-use-cluster-sets"></a>클러스터 세트를 사용 하는 이유

클러스터 집합은 복원 력을 저하 시 키 지 않고 규모의 이점을 제공 합니다.  

클러스터 집합을 사용 하면 여러 클러스터를 함께 클러스터링 하 여 대량 패브릭을 만들 수 있으며 각 클러스터는 복원 력에 독립적으로 유지 됩니다.  예를 들어 가상 컴퓨터를 실행 하는 4 개 노드 HCI 클러스터가 여러 개 있을 수 있습니다.  각 클러스터는 자신에 게 필요한 복원 력을 제공 합니다.  저장소 또는 메모리 채우기가 시작 되 면 다음 단계를 확장 합니다.  확장을 사용 하는 경우 몇 가지 옵션과 고려 사항이 있습니다.

1. 현재 클러스터에 저장소를 더 추가 합니다.  스토리지 공간 다이렉트 사용 하는 것은 정확한 동일한 모델/펌웨어 드라이브를 사용 하지 못할 수 있기 때문에 어려울 수 있습니다.  다시 빌드 시간 고려도 고려해 야 합니다.
2. 메모리를 추가하십시오.  컴퓨터에서 처리할 수 있는 메모리를 최대값 면 어떻게 하나요?  사용 가능한 모든 메모리 슬롯이 꽉 차면 어떻게 되나요?
3. 드라이브가 포함 된 추가 계산 노드를 현재 클러스터에 추가 합니다.  이는 고려해 야 할 옵션 1로 돌아갑니다.
4. 전체 새 클러스터 구매

여기서 클러스터 집합은 크기 조정의 이점을 제공 합니다.  클러스터 집합에 클러스터를 추가 하는 경우 추가 구매 없이 다른 클러스터에서 사용할 수 있는 저장소 또는 메모리를 활용할 수 있습니다.  복원 력 측면에서 스토리지 공간 다이렉트에 노드를 더 추가 하는 것은 쿼럼에 대 한 추가 투표를 제공 하지 않습니다.  [여기](drive-symmetry-considerations.md)에 설명 된 것 처럼 작동이 중단 되기 전에 스토리지 공간 다이렉트 클러스터는 2 개 노드의 손실을 감당할 수 있습니다.  4 노드 HCI 클러스터를 사용 하는 경우 3 개의 노드가 다운 되 면 전체 클러스터가 작동 중지 됩니다.  8 개 노드 클러스터가 있는 경우 3 개의 노드가 다운 되 면 전체 클러스터가 작동 중지 됩니다.  집합에 두 개의 4 노드 HCI 클러스터가 있는 클러스터 집합을 사용 하는 경우 한 HCI의 노드 2 개는 중단 되 고 다른 HCI에는 1 개의 노드가 작동 중단 됩니다. 두 클러스터는 모두 유지 됩니다.  하나의 대량 16 노드 스토리지 공간 다이렉트 클러스터를 만들거나 4 개 노드 클러스터로 분리 하 고 클러스터 집합을 사용 하는 것이 더 나은 가요?  클러스터 집합을 포함 하는 4 개 노드 클러스터가 4 개 있으면 동일한 규모를 제공 하지만 여러 계산 노드가 다운 (예기치 않게 또는 유지 관리의 경우) 될 수 있고 프로덕션이 남아 있는 경우의 복원 력이 향상 됩니다.

## <a name="considerations-for-deploying-cluster-sets"></a>클러스터 집합 배포에 대 한 고려 사항

클러스터 집합이 사용 해야 하는 것이 무엇 인지 고려 하는 경우 다음 사항을 고려 하세요.

- 현재 HCI 계산 및 저장소 크기 제한을 초과 해야 하나요?
- 모든 계산과 저장소는 동일 하지는 않습니다.
- 클러스터 간에 가상 컴퓨터를 실시간으로 마이그레이션 하나요?
- 여러 클러스터에서 Azure와 같은 컴퓨터 가용성 집합과 장애 도메인을 사용 하 시겠습니까?
- 모든 클러스터를 확인 하 여 새 가상 컴퓨터를 배치 해야 하는 위치를 확인 해야 하나요?

대답이 예 인 경우에는 클러스터 집합이 필요 합니다.

더 큰 SDDC에서 전체 데이터 센터 전략을 변경 하는 경우 고려해 야 할 몇 가지 다른 항목이 있습니다.  SQL Server은 좋은 예입니다.  클러스터 간에 SQL Server 가상 컴퓨터를 이동 하려면 추가 노드에서 라이선스 SQL을 실행 해야 하나요?  

## <a name="scale-out-file-server-and-cluster-sets"></a>스케일 아웃 파일 서버 및 클러스터 집합

Windows Server 2019에는 인프라 스케일 아웃 파일 서버 (SOFS) 이라는 새로운 스케일 아웃 파일 서버 역할이 있습니다. 

인프라 SOFS 역할에 적용 되는 고려 사항은 다음과 같습니다.

1. 장애 조치 (Failover) 클러스터에는 하나의 인프라 SOFS 클러스터 역할만 있을 수 있습니다. 인프라 SOFS 역할은 **ClusterScaleOutFileServerRole** cmdlet에 "**-Infrastructure**" 스위치 매개 변수를 지정 하 여 만듭니다.  다음은 그 예입니다. 

    ```PowerShell
    Add-ClusterScaleoutFileServerRole -Name "my_infra_sofs_name" -Infrastructure
    ```

2. 장애 조치 (failover) 시 생성 된 각 CSV 볼륨은 CSV 볼륨 이름을 기반으로 자동 생성 된 이름으로 SMB 공유 생성을 자동으로 트리거합니다. 관리자는 CSV 볼륨 만들기/수정 작업 외에 SOFS 역할을 통해 직접 SMB 공유를 만들거나 수정할 수 없습니다.

3. 하이퍼 수렴 형 구성에서 인프라 SOFS를 사용 하면 SMB 클라이언트 (Hyper-v 호스트)가 보장 된 CA (지속적인 가용성)와 SMB 서버 인프라 SOFS 통신할 수 있습니다. 클라이언트와 서버 간에 소유 하는 가상 컴퓨터 id가 전달 되는 가상 디스크 (VHDx) 파일에 액세스 하는 가상 컴퓨터를 통해이 하이퍼 수렴 형 SMB 루프백 CA를 구현할 수 있습니다. 이 id 전달을 사용 하면 이전 처럼 표준 하이퍼 수렴 형 클러스터 구성에서와 마찬가지로 ACL을 사용 하는 VHDx 파일을 사용할 수 있습니다.

클러스터 세트를 만든 후 클러스터 집합 네임 스페이스는 각 구성원 클러스터의 인프라 SOFS를 사용 하 고 관리 클러스터의 인프라 SOFS을 추가로 사용 합니다.

클러스터 집합에 구성원 클러스터가 추가 될 때 관리자는 해당 클러스터에 대 한 인프라 SOFS (이미 있는 경우)의 이름을 지정 합니다. 인프라 SOFS 없는 경우 새 구성원 클러스터에 대 한 새 인프라 SOFS 역할이이 작업에 의해 생성 됩니다. 인프라 SOFS 역할이 이미 구성원 클러스터에 있으면 추가 작업은 필요에 따라 지정 된 이름으로 이름을 암시적으로 바꿉니다. 클러스터 집합에서 구성원 클러스터의 모든 기존 단일 SMB 서버 또는 비 인프라 SOFS 역할을 사용 하지 않습니다. 

클러스터 세트를 만들 때 관리자는 기존 AD 컴퓨터 개체를 관리 클러스터의 네임 스페이스 루트로 사용 하는 옵션을 사용할 수 있습니다. 클러스터 집합 만들기 작업은 관리 클러스터에서 인프라 SOFS 클러스터 역할을 만들거나 구성원 클러스터에 대해 앞에서 설명한 대로 기존 Infrastructure SOFS 역할의 이름을 바꿉니다. 관리 클러스터의 인프라 SOFS는 클러스터 집합 네임 스페이스 조회 (클러스터 집합 네임 스페이스) SOFS 사용 됩니다. 단순히 클러스터 집합 네임 스페이스 SOFS의 각 SMB 공유가 ' SimpleReferral ' 유형 (Windows Server 2019에 새로 도입 됨)의 조회 공유 임을 의미 합니다.  이 조회를 통해 SMB 클라이언트는 구성원 클러스터 SOFS에서 호스트 되는 대상 SMB 공유에 액세스할 수 있습니다. 클러스터 집합 네임 스페이스 조회 SOFS는 경량 조회 메커니즘 이므로 i/o 경로에 참여 하지 않습니다. SMB 조회는 각 클라이언트 노드에 캐시 된 영구적으로 클러스터에서 네임 스페이스를 동적으로 업데이트 하 여 필요에 따라 자동으로 업데이트 합니다.

## <a name="creating-a-cluster-set"></a>클러스터 집합 만들기

### <a name="prerequisites"></a>전제 조건

클러스터 집합을 만들 때 다음 필수 구성 요소를 권장 합니다.

1. Windows Server 2019를 실행 하는 관리 클라이언트를 구성 합니다.
2. 이 관리 서버에 장애 조치 (Failover) 클러스터 도구를 설치 합니다.
3. 클러스터 구성원 만들기 (각 클러스터에 두 개 이상의 클러스터 공유 볼륨을 포함 하는 두 개 이상의 클러스터)
4. 구성원 클러스터를 cmio 관리 클러스터 (물리적 또는 게스트)를 만듭니다.  이 방법을 사용 하면 가능한 구성원 클러스터 오류에도 불구 하 고 클러스터에서 관리 평면을 계속 사용할 수 있습니다.

### <a name="steps"></a>단계

1. 필수 구성 요소에 정의 된 대로 세 개의 클러스터에서 새 클러스터 집합을 만듭니다.  아래 차트는 만들 클러스터의 예제를 제공 합니다.  이 예제에서 클러스터 집합의 이름은 **Csmaster**가 됩니다.

   | 클러스터 이름               | 나중에 사용할 인프라 SOFS 이름 | 
   |----------------------------|-------------------------------------------|
   | 설정-클러스터                | SOFS-CLUSTERSET                           |
   | CLUSTER1                   | SOFS-CLUSTER1                             |
   | 클러스터 2                   | SOFS-클러스터 2                             |

2. 모든 클러스터를 만들었으면 다음 명령을 사용 하 여 클러스터 집합 마스터를 만듭니다.

    ```PowerShell
    New-ClusterSet -Name CSMASTER -NamespaceRoot SOFS-CLUSTERSET -CimSession SET-CLUSTER
    ```

3. 클러스터 집합에 클러스터 서버를 추가 하려면 아래를 사용 합니다.

    ```PowerShell
    Add-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER1
    Add-ClusterSetMember -ClusterName CLUSTER2 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER2
    ```

   > [!NOTE]
   > 고정 IP 주소 체계를 사용 하는 경우에는 **새-ClusterSet** 명령에 *-staticaddress x* . x. x를 포함 해야 합니다.

4. 클러스터 구성원으로 설정 된 클러스터를 만들었으면 노드 집합 및 해당 속성을 나열할 수 있습니다.  클러스터 집합의 모든 구성원 클러스터를 열거 하려면:

    ```PowerShell
    Get-ClusterSetMember -CimSession CSMASTER
    ```

5. 관리 클러스터 노드를 포함 하 여 클러스터 집합의 모든 구성원 클러스터를 열거 하려면:

    ```PowerShell
    Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterNode
    ```

6. 멤버 클러스터의 모든 노드를 나열 하려면 다음을 수행 합니다.

    ```PowerShell
    Get-ClusterSetNode -CimSession CSMASTER
    ```

7. 클러스터 집합 전체에서 모든 리소스 그룹을 나열 하려면 다음을 수행 합니다.

    ```PowerShell
    Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterGroup 
    ```

8. 클러스터 집합 생성 프로세스에서 각 클러스터 구성원의 CSV 볼륨에 대 한 인프라 SOFS에 하나의 SMB 공유 (Volume1로 식별 되거나 ScopeName로 레이블이 지정 된 CSV 폴더의 이름 및 두 파일의 경로)가 생성 되었는지 확인 하려면 다음을 수행 합니다.

    ```PowerShell
    Get-SmbShare -CimSession CSMASTER
    ```

8. 클러스터 집합에는 검토를 위해 수집할 수 있는 디버그 로그가 있습니다.  모든 구성원 및 관리 클러스터에 대해 클러스터 집합과 클러스터 디버그 로그를 모두 수집할 수 있습니다.

    ```PowerShell
    Get-ClusterSetLog -ClusterSetCimSession CSMASTER -IncludeClusterLog -IncludeManagementClusterLog -DestinationFolderPath <path>
    ```

9. 모든 클러스터 집합 구성원 사이에서 Kerberos [제한 위임을](https://techcommunity.microsoft.com/t5/virtualization/live-migration-via-constrained-delegation-with-kerberos-in/ba-p/382334) 구성 합니다.

10. 클러스터 집합의 각 노드에서 클러스터 간 가상 머신 실시간 마이그레이션 인증 유형을 Kerberos로 구성 합니다.

    ```PowerShell
    foreach($h in $hosts){ Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos -ComputerName $h }
    ```

11. 클러스터 집합의 각 노드에 있는 로컬 관리자 그룹에 관리 클러스터를 추가 합니다.

    ```PowerShell
    foreach($h in $hosts){ Invoke-Command -ComputerName $h -ScriptBlock {Net localgroup administrators /add <management_cluster_name>$} }
    ```

## <a name="creating-new-virtual-machines-and-adding-to-cluster-sets"></a>새 가상 컴퓨터 만들기 및 클러스터 집합에 추가

클러스터 집합을 만든 후 다음 단계는 새 가상 컴퓨터를 만드는 것입니다.  일반적으로 가상 컴퓨터를 만들고 클러스터에 추가할 때 클러스터에 대 한 몇 가지 검사를 수행 하 여에서 실행 하는 것이 가장 좋을 수 있습니다.  이러한 검사에는 다음이 포함 될 수 있습니다.

- 클러스터 노드에서 사용할 수 있는 메모리는 어느 정도 인가요?
- 클러스터 노드에서 사용할 수 있는 디스크 공간은 어느 정도 인가요?
- 가상 컴퓨터에는 특정 저장소 요구 사항이 필요 합니다 (즉, 내 SQL Server 가상 컴퓨터에서 더 빠른 드라이브를 실행 하는 클러스터로 이동 하 고, 또는 인프라 가상 컴퓨터는 중요 하지 않고 속도가 느린 드라이브에서 실행 될 수 있음).

이 질문에 대 한 답변을 받으면 필요한 클러스터에서 가상 머신을 만듭니다.  클러스터 집합의 이점 중 하나는 클러스터에서 해당 검사를 수행 하 고 가장 최적 노드에 가상 컴퓨터를 저장 한다는 것입니다.

아래 명령은 모두 최적의 클러스터를 식별 하 고 여기에 가상 컴퓨터를 배포 합니다.  아래 예제에서는 가상 머신에 최소 4gb의 메모리를 사용할 수 있고 1 개의 가상 프로세서를 사용 해야 함을 지정 하는 새 가상 머신을 만듭니다.

- 가상 컴퓨터에 대해 4gb를 사용할 수 있는지 확인 합니다.
- 1에서 사용 되는 가상 프로세서를 설정 합니다.
- 가상 컴퓨터에 사용할 수 있는 CPU가 10% 이상 인지 확인 합니다.

```PowerShell
# Identify the optimal node to create a new virtual machine
$memoryinMB=4096
$vpcount = 1
$targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10
$secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
$cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)

# Deploy the virtual machine on the optimal node
Invoke-Command -ComputerName $targetnode.name -scriptblock { param([String]$storagepath); New-VM CSVM1 -MemoryStartupBytes 3072MB -path $storagepath -NewVHDPath CSVM.vhdx -NewVHDSizeBytes 4194304 } -ArgumentList @("\\SOFS-CLUSTER1\VOLUME1") -Credential $cred | Out-Null

Start-VM CSVM1 -ComputerName $targetnode.name | Out-Null
Get-VM CSVM1 -ComputerName $targetnode.name | fl State, ComputerName
```

완료 되 면 가상 머신에 대 한 정보와 해당 위치가 배치 된 위치에 대 한 정보가 제공 됩니다.  위의 예제에서는 다음과 같이 표시 됩니다.

```
State         : Running
ComputerName  : 1-S2D2
```

가상 컴퓨터를 추가 하는 데 충분 한 메모리, cpu 또는 디스크 공간이 없는 경우 다음과 같은 오류가 표시 됩니다.

```
Get-ClusterSetOptimalNodeForVM : A cluster node is not available for this operation.  
```

가상 머신이 만들어지면 지정 된 특정 노드에 Hyper-v 관리자에 표시 됩니다.  클러스터 집합 가상 머신으로 클러스터에 추가 하려면 다음 명령을 추가 합니다.  

```PowerShell
Register-ClusterSetVM -CimSession CSMASTER -MemberName $targetnode.Member -VMName CSVM1
```

완료 되 면 출력은 다음과 같습니다.

```
Id  VMName  State  MemberName  PSComputerName
--  ------  -----  ----------  --------------
1  CSVM1      On  CLUSTER1    CSMASTER
```

기존 가상 컴퓨터를 사용 하 여 클러스터를 추가한 경우에는 가상 컴퓨터를 클러스터 집합에 등록 해야 합니다. 그러면 모든 가상 컴퓨터를 한 번에 등록 해야 사용할 수 있습니다.

```PowerShell
Get-ClusterSetMember -Name CLUSTER3 -CimSession CSMASTER | Register-ClusterSetVM -RegisterAll -CimSession CSMASTER
```

그러나 가상 머신의 경로를 클러스터 집합 네임 스페이스에 추가 해야 하므로 프로세스가 완료 되지 않습니다.

예를 들어 기존 클러스터가 추가 되 고 미리 구성 된 가상 컴퓨터가 CSV (local 클러스터 공유 볼륨)에 있는 경우 VHDX의 경로는 "C:\ClusterStorage\Volume1\MYVM\Virtual Hard Disks\MYVM.vhdx."와 비슷합니다.  CSV 경로는 단일 구성원 클러스터에 대해 로컬로 설계 되므로 저장소 마이그레이션을 수행 해야 합니다. 따라서는 구성원 클러스터 간에 실시간으로 마이그레이션되는 가상 컴퓨터에 액세스할 수 없습니다. 

이 예제에서 CLUSTER3는 SOFS로 스케일 아웃 파일 서버 인프라를 사용 하 여 CLUSTER3로 추가 ClusterSetMember를 사용 하 여 클러스터 집합에 추가 되었습니다.  가상 컴퓨터 구성 및 저장소를 이동 하는 명령은 다음과 같습니다.

```PowerShell
Move-VMStorage -DestinationStoragePath \\SOFS-CLUSTER3\Volume1 -Name MYVM
```

완료 되 면 경고를 받게 됩니다.

```
WARNING: There were issues updating the virtual machine configuration that may prevent the virtual machine from running.  For more information view the report file below.
WARNING: Report file location: C:\Windows\Cluster\Reports\Update-ClusterVirtualMachineConfiguration '' on date at time.htm.
```

이 경고는 "가상 컴퓨터 역할 저장소 구성에서 변경 내용이 검색 되지 않았습니다." 라는 경고가 발생 한 경우 무시 해도 됩니다.  실제 실제 위치에 대 한 경고의 원인은 변경 되지 않습니다. 구성 경로만. 

VMStorage 이동에 대 한 자세한 내용은이 [링크](https://docs.microsoft.com/powershell/module/hyper-v/move-vmstorage?view=win10-ps)를 검토 하세요. 

서로 다른 클러스터 집합 클러스터 간에 가상 컴퓨터를 실시간으로 마이그레이션하는 것은 과거와 동일 하지 않습니다. 비 클러스터 집합 시나리오에서 단계는 다음과 같습니다.

1. 클러스터에서 가상 컴퓨터 역할을 제거 합니다.
2. 가상 컴퓨터를 다른 클러스터의 구성원 노드로 실시간 마이그레이션합니다.
3. 새 가상 컴퓨터 역할로 클러스터에 가상 컴퓨터를 추가 합니다.

클러스터 집합을 사용 하면 이러한 단계가 필요 하지 않으며 명령만 있으면 됩니다.  먼저 명령을 사용 하 여 마이그레이션에 사용할 수 있는 모든 네트워크를 설정 해야 합니다.

```PowerShell
Set-VMHost -UseAnyNetworkForMigration $true
```

예를 들어 클러스터 집합 가상 머신을 CLUSTER1에서 CL3의 CLUSTER3로 이동 하려고 합니다.  단일 명령은 다음과 같습니다.

```PowerShell
Move-ClusterSetVM -CimSession CSMASTER -VMName CSVM1 -Node NODE2-CL3
```

가상 컴퓨터 저장소 또는 구성 파일은 이동 하지 않습니다.  가상 컴퓨터에 대 한 경로가 SOFS-CLUSTER1\VOLUME1.으로 \\ \\유지 되므로이 작업이 필요 하지 않습니다.  가상 컴퓨터에 등록 된 가상 컴퓨터의 인프라 파일 서버 공유 경로가 있는 경우 드라이브와 가상 컴퓨터는 가상 컴퓨터와 동일한 컴퓨터에 있지 않아도 됩니다.

## <a name="creating-availability-sets-fault-domains"></a>가용성 집합 장애 도메인 만들기

소개에 설명 된 대로 Azure와 같은 장애 도메인 및 가용성 집합은 클러스터 집합에서 구성할 수 있습니다.  이는 클러스터 간의 초기 가상 머신 배치 및 마이그레이션에 유용 합니다.  

아래 예제에서는 클러스터 집합에 참여 하는 네 개의 클러스터가 있습니다.  집합 내에서 논리적 장애 도메인은 두 개의 클러스터와 다른 두 클러스터를 사용 하 여 만든 장애 도메인을 사용 하 여 생성 됩니다.  이러한 두 장애 도메인은 가용성 집합으로 구성 됩니다. 

아래 예제에서 CLUSTER1 및 클러스터 2는 **f** 라는 장애 도메인에 있으며, CLUSTER3 및 CLUSTER4는 **FD2**라는 장애 도메인에 있습니다.  가용성 집합은 **Csmaster-로** 호출 되며 두 개의 장애 도메인으로 구성 됩니다.

장애 도메인을 만드는 명령은 다음과 같습니다.

```PowerShell
New-ClusterSetFaultDomain -Name FD1 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER1,CLUSTER2 -Description "This is my first fault domain"

New-ClusterSetFaultDomain -Name FD2 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER3,CLUSTER4 -Description "This is my second fault domain"
```

성공적으로 만들어졌는지 확인 하려면 출력을 표시 한 상태로 Get ClusterSetFaultDomain을 실행할 수 있습니다.

```PowerShell
PS C:\> Get-ClusterSetFaultDomain -CimSession CSMASTER -FdName FD1 | fl *

PSShowComputerName    : True
FaultDomainType       : Logical
ClusterName           : {CLUSTER1, CLUSTER2}
Description           : This is my first fault domain
FDName                : FD1
Id                    : 1
PSComputerName        : CSMASTER
```

이제 장애 도메인을 만들었으므로 가용성 집합을 만들어야 합니다.

```PowerShell
New-ClusterSetAvailabilitySet -Name CSMASTER-AS -FdType Logical -CimSession CSMASTER -ParticipantName FD1,FD2
```

유효성을 검사 하려면 다음을 사용 합니다.

```PowerShell
Get-ClusterSetAvailabilitySet -AvailabilitySetName CSMASTER-AS -CimSession CSMASTER
```

새 가상 컴퓨터를 만들 때 최적 노드를 결정 하는 과정에서-가용성 집합 매개 변수를 사용 해야 합니다.  그러면 다음과 같이 표시 됩니다.

```PowerShell
# Identify the optimal node to create a new virtual machine
$memoryinMB=4096
$vpcount = 1
$av = Get-ClusterSetAvailabilitySet -Name CSMASTER-AS -CimSession CSMASTER
$targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10 -AvailabilitySet $av
$secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
$cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)
```

다양 한 수명 주기 때문에 클러스터 집합에서 클러스터를 제거 합니다. 클러스터 집합에서 클러스터를 제거 해야 하는 경우가 있습니다. 모든 클러스터 집합 가상 머신은 클러스터에서 이동 해야 하는 것이 가장 좋습니다. 이는 **이동 ClusterSetVM** 및 **vmstorage** 명령을 사용 하 여 수행할 수 있습니다.

그러나 가상 컴퓨터도 이동 하지 않을 경우 클러스터 세트는 일련의 작업을 실행 하 여 관리자에 게 직관적인 결과를 제공 합니다.  클러스터가 집합에서 제거 되 면 제거 되는 클러스터에서 호스트 되는 나머지 클러스터 집합 가상 컴퓨터는 모두 해당 클러스터에 바인딩된 항상 사용 가능한 가상 컴퓨터로 사용 되며, 해당 저장소에 대 한 액세스 권한이 있다고 가정 합니다.  또한 클러스터 집합은 다음을 기준으로 인벤토리를 자동으로 업데이트 합니다.

- 이제 제거 된 클러스터와이 클러스터에서 실행 중인 가상 컴퓨터의 상태를 더 이상 추적 하지 않습니다.
- 클러스터 집합 네임 스페이스 및 현재 제거 된 클러스터에 호스트 된 공유에 대 한 모든 참조를 제거 합니다.

예를 들어 클러스터 집합에서 CLUSTER1 클러스터를 제거 하는 명령은 다음과 같습니다.

```PowerShell
Remove-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER
```

## <a name="frequently-asked-questions-faq"></a>질문과 대답(FAQ)

**질문:** 내 클러스터 집합에서 하이퍼 수렴 형 클러스터만 사용 하도록 제한 됩니까? <br>
**답변:** 아니요.  기존 클러스터와 스토리지 공간 다이렉트 혼합할 수 있습니다.

**질문:** System Center Virtual Machine Manager를 통해 내 클러스터 집합을 관리할 수 있나요? <br>
**답변:** System Center Virtual Machine Manager는 현재 클러스터 집합을 지원 하지 않습니다. <br><br> **질문:** Windows Server 2012 R2 또는 2016 클러스터가 동일한 클러스터 집합에 공존할 수 있나요? <br>
**질문:** 이러한 클러스터를 동일한 클러스터 집합에 조인 하기만 하면 Windows Server 2012 R2 또는 2016 클러스터에서 워크 로드를 마이그레이션할 수 있나요? <br>
**답변:** 클러스터 집합은 Windows Server 2019에 도입 되는 새로운 기술 이므로 이전 릴리스에는 존재 하지 않습니다. 하위 수준 OS 기반 클러스터는 클러스터 집합에 가입할 수 없습니다. 그러나 클러스터 운영 체제 롤링 업그레이드 기술은 이러한 클러스터를 Windows Server 2019로 업그레이드 하 여 원하는 마이그레이션 기능을 제공 해야 합니다.

**질문:** 클러스터 집합에서 저장소 크기를 조정 하거나 계산 (단독) 할 수 있나요? <br>
**답변:** 예, 저장소 공간 다이렉트 또는 기존 Hyper-v 클러스터를 추가 하기만 하면 됩니다. 클러스터 세트를 사용 하 여 하이퍼 수렴 형 클러스터 집합 에서도 계산-저장소 비율을 간단 하 게 변경할 수 있습니다.

**질문:** 클러스터 집합에 대 한 관리 도구 <br>
**답변:** PowerShell 또는이 릴리스의 WMI.

**질문:** 클러스터 간 실시간 마이그레이션은 다른 세대의 프로세서와 어떻게 작동 하나요?  <br>
**답변:** 클러스터 집합은 프로세서의 차이점을 해결 하지 않으며 현재 Hyper-v에서 지 원하는 기능을 대체 합니다.  따라서 빠른 마이그레이션과 함께 프로세서 호환성 모드를 사용 해야 합니다.  클러스터 집합에 대 한 권장 사항은 각 개별 클러스터 내에서 동일한 프로세서 하드웨어를 사용 하는 것이 고, 클러스터 간 실시간 마이그레이션에 대 한 전체 클러스터 집합을 사용 하는 것입니다.

**질문:** 클러스터를 설정 하는 동안 클러스터에서 가상 컴퓨터를 자동으로 장애 조치 (failover) 할 수 있나요?  <br>
**답변:** 이 릴리스에서는 클러스터 집합 가상 컴퓨터를 클러스터 간에 수동으로 실시간 마이그레이션할 수 있습니다. 하지만 자동으로 장애 조치 (failover) 할 수 없습니다. 

**질문:** 클러스터 오류에 대해 저장소를 복원 하려면 어떻게 해야 하나요? <br>
**답변:** 클러스터 오류에 대 한 저장소 복원 력을 실현 하려면 구성원 클러스터에서 클러스터 간 저장소 복제 (SR)를 사용 합니다.

**질문:** SR-IOV (저장소 복제본)를 사용 하 여 멤버 클러스터 간에 복제 합니다. 클러스터 집합 네임 스페이스 저장소 UNC 경로 SR 장애 조치 (failover)에서 복제본 대상 스토리지 공간 다이렉트 클러스터로 변경 하 시겠습니까? <br>
**답변:** 이 릴리스에서 이러한 클러스터 집합 네임 스페이스 조회 변경은 SR-IOV 장애 조치 (failover)에서 발생 하지 않습니다. 이 시나리오가 중요 한 것과 사용 방법에 대해 Microsoft에 알려 주십시오.

**질문:** 재해 복구 상황에서 장애 도메인을 통해 가상 컴퓨터를 장애 조치 (failover) 할 수 있나요? (전체 장애 도메인이 중단 되었다고 가정)? <br>
**답변:** 아니요, 논리적 장애 도메인 내에서 클러스터 간 장애 조치 (failover)는 아직 지원 되지 않습니다. 

**질문:** 내 클러스터 집합에서 여러 사이트 (또는 DNS 도메인)에 클러스터를 확장할 수 있나요? <br> 
**답변:** 이는 테스트 되지 않은 시나리오 이며 프로덕션 지원에 대해 즉시 계획 되지 않습니다. 이 시나리오가 중요 한 것과 사용 방법에 대해 Microsoft에 알려 주십시오.

**질문:** 클러스터가 i p v 6에서 작동 하나요? <br>
**답변:** IPv4 및 IPv6 모두 장애 조치 (Failover) 클러스터와 함께 클러스터 집합에서 지원 됩니다.

**질문:** 클러스터 집합에 대 한 Active Directory 포리스트 요구 사항은 무엇 인가요? <br>
**답변:** 모든 구성원 클러스터는 동일한 AD 포리스트에 있어야 합니다.

**질문:** 단일 클러스터 집합에 포함할 수 있는 클러스터 또는 노드는 몇 개입니까? <br>
**답변:** Windows Server 2019에서는 클러스터 집합이 테스트 되었으며 총 64 개의 클러스터 노드가 지원 됩니다. 그러나 클러스터 집합 아키텍처는 훨씬 더 큰 제한으로 확장 되며 한도에 대해 하드 코드 된 것은 아닙니다. 더 큰 규모의 경우 사용자에 게 중요 한 것이 고이를 사용 하는 방법은 Microsoft에 알려 주십시오.

**질문:** 클러스터 집합의 모든 스토리지 공간 다이렉트 클러스터는 단일 저장소 풀을 구성 하나요? <br>
**답변:** 아니요. 스토리지 공간 다이렉트 기술은 클러스터 집합의 구성원 클러스터가 아닌 단일 클러스터 내에서 계속 작동 합니다.

**질문:** 클러스터 집합 네임 스페이스를 항상 사용할 수 있나요? <br>
**답변:** 예, 클러스터 집합 네임 스페이스는 관리 클러스터에서 실행 되는 지속적으로 사용 가능한 (CA) 조회 SOFS 네임 스페이스 서버를 통해 제공 됩니다. Microsoft는 구성원 클러스터에서 충분 한 수의 가상 컴퓨터를 사용 하 여 지역화 된 클러스터 전체 오류에 탄력적으로 대처할 수 있도록 하는 것이 좋습니다. 그러나 예기치 않은 치명적인 오류가 발생 하는 경우 (예: 관리 클러스터의 모든 가상 컴퓨터가 동시에 중단 됨) 다시 부팅 하더라도 각 클러스터 집합 노드에서 조회 정보가 영구적으로 영구적으로 캐시 됩니다.
 
**질문:** 클러스터에서 네임 스페이스 기반 저장소 액세스를 설정 하면 클러스터 집합의 저장소 성능이 저하 됩니까? <br>
**답변:** 아니요. 클러스터 집합 네임 스페이스는 DFSN (분산 파일 시스템 네임 스페이스)와 같이 개념적으로 클러스터 집합 내에 오버레이 조회 네임 스페이스를 제공 합니다. DFSN와 달리 모든 클러스터 집합 네임 스페이스 조회 메타 데이터는 관리자 개입 없이 모든 노드에서 자동으로 채워지고 자동으로 업데이트 되므로 저장소 액세스 경로에 성능 오버 헤드가 거의 없습니다. 

**질문:** 클러스터 집합 메타 데이터를 백업 하려면 어떻게 해야 하나요? <br>
**답변:** 이 지침은 장애 조치 (Failover) 클러스터와 동일 합니다. 시스템 상태 백업도 클러스터 상태를 백업 합니다.  Windows Server 백업를 통해 노드 클러스터 데이터베이스 (보유 한 자체 복구 논리로 인해 필요 하지 않음)를 복원 하거나 모든 노드에서 전체 클러스터 데이터베이스를 롤백하는 신뢰할 수 있는 복원을 수행할 수 있습니다. 클러스터 집합의 경우 먼저 구성원 클러스터에서 신뢰할 수 있는 복원을 수행 하 고 필요한 경우 관리 클러스터를 수행 하는 것이 좋습니다.
