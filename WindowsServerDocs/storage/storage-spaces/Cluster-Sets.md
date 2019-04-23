---
title: 클러스터 집합
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: johnmarlin-msft
ms.date: 01/30/2019
description: 이 문서에서는 클러스터 집합 시나리오를 설명합니다.
ms.localizationpriority: medium
ms.openlocfilehash: 2deeb6968f910e80bacb2354ad2e575060a7797a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833954"
---
# <a name="cluster-sets"></a>클러스터 집합

> 적용 대상: Windows Server Insider Preview 빌드 17650 이상

클러스터 집합은 단일 소프트웨어 정의 데이터 센터 (SDDC) 클라우드에서 클러스터 노드 수의 크기가 증가 하는이 미리 보기 릴리스에서 새 클라우드 스케일 아웃 기술. 클러스터 집합은 여러 장애 조치 클러스터의 느슨하게 결합 된 그룹: 계산, 저장소 또는 하이퍼 수렴 형입니다. 클러스터 집합 기술을 사용 하도록 설정 가상 컴퓨터 환경에 걸쳐 클러스터 집합 및 통합된 저장소 네임 스페이스 내에서 멤버 클러스터 집합을 지원 하기 위해 가상 컴퓨터 환경에서. 

멤버 클러스터에서 기존 장애 조치 클러스터의 유지 관리 환경을, 하는 동안 클러스터 집합 인스턴스는 또한 집계에서 수명 주기 관리와 관련 한 주요 사용 사례를 제공 합니다. 이 Windows Server 미리 보기 시나리오 평가 가이드는 PowerShell을 사용 하 여 클러스터 집합 기술을 평가 하는 단계별 지침과 함께 필요한 배경 정보를 제공 합니다. 

## <a name="technology-introduction"></a>기술 소개

소프트웨어 정의 데이터 센터 (SDDC) 클라우드 규모에서 작동 하는 특정 고객 요청을 충족 하기 위해 클러스터 집합 기술을 개발 됩니다. 이 미리 보기 릴리스에서 클러스터 집합 가치는 다음과 같이 요약할 수 있습니다.  

- 단일 클러스터에 소프트웨어 오류 경계를 유지 하는 동안에 단일 큰 패브릭에 여러 개의 작은 클러스터를 결합 하 여 항상 사용 가능한 virtual machines를 실행 하는 것에 대 한 지원 되는 SDDC 클라우드 규모를 크게 향상
- 전체 마이그레이션 유동적으로 통해 테 넌 트 가상 머신 가용성에 영향을 주지 않고 장애 조치 클러스터 수명 주기를 더 이상 사용 및 온 보 딩을 포함 하 여 클러스터를 관리 합니다.이 큰 패브릭에서 가상 머신
- 에 하이퍼 수렴 형에서 compute-저장소 비율을 변경 하는 쉽게 있나요
- 이점을 [같은 Azure 장애 도메인 및 가용성 집합](htttps://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) 초기 가상 머신 배치 및 이후 가상 컴퓨터 마이그레이션에는 클러스터 간에
- 혼합 및 일치 여러 CPU 하드웨어 세대를 동일한 클러스터에 효율성을 극대화 동종 개별 장애 도메인을 유지 하는 동안에 패브릭에서 설정 합니다.  동일한 하드웨어 권장 사항 전체 클러스터 집합 뿐만 아니라 각 개별 클러스터 내에서 여전히 존재는 note 하십시오.

상위 수준 보기에서이 어떤 클러스터 집합은 다음과 같을 수 있습니다.

![클러스터 설정 솔루션 보기](media\Cluster-sets-Overview\Cluster-sets-solution-View.png)

다음의 각 요소 위 이미지에 대 한 요약을 제공합니다.

**관리 클러스터**

클러스터 집합에 관리 클러스터는 전체 클러스터 집합 및 통합 된 저장소 (클러스터 설정 Namespace) 네임 스페이스 조회 스케일 아웃 파일 서버 (SOFS) 항상 사용 가능한 관리 평면을 호스팅하는 장애 조치 클러스터는입니다. 관리 클러스터는 virtual machine 워크 로드를 실행 하는 멤버 클러스터에서 논리적으로 분리 합니다. 이렇게 하면 모든 지역화 된 클러스터 전체의 오류로 관리 평면을 복원 력 있는 클러스터 멤버 클러스터의 전원 손실 예를 들어 있습니다.   

**클러스터 멤버**

클러스터 집합의 멤버 클러스터는 일반적으로 가상 머신 및 저장소 공간 다이렉트 워크 로드를 실행 하는 기존 하이퍼 수렴 형 클러스터. 여러 멤버 클러스터 단일 클러스터 집합 배포를 더 큰 SDDC 클라우드 패브릭 구성에 참여 합니다. 두 가지 주요 측면인의 관리 클러스터에서 다른 클러스터 멤버: 멤버 클러스터 장애 도메인에 참여 하 고 가용성 집합 구조 멤버 클러스터 호스트 가상 컴퓨터 및 저장소 공간 다이렉트 워크 로드에 맞게 조정도 됩니다. 따라서 클러스터 집합에 있는 클러스터 경계를 넘어 이동 하는 클러스터 집합 가상 머신에 관리 클러스터에서 호스트 되어야 합니다.

**클러스터 네임 스페이스 조회 SOFS 설정**

클러스터 집합 네임 스페이스 조회 (클러스터 설정 Namespace) SOFS는 여기서 각 SMB 공유 클러스터 설정 Namespace SOFS에는이 미리 보기 릴리스에서 새로 도입 된 ' SimpleReferral' 형식의 조회 공유-스케일 아웃 파일 서버.  이 조회 서버 메시지 블록 (SMB) 클라이언트가 멤버 클러스터 SOFS에서 호스트 하는 SMB 공유 대상에 대 한 액세스를 허용 합니다. 클러스터는 I/O 경로에서 SOFS는 간단한 조회 메커니즘이 며 따라서 참여 하지 않는 네임 스페이스 조회를 설정 합니다. SMB 조회 클라이언트 노드 각각에 영구적으로 캐시 됩니다 및 클러스터 집합 네임 스페이스 동적으로 자동으로 이러한 조회 필요에 따라 업데이트 합니다.

**클러스터 마스터 집합**

클러스터 집합에서 멤버 클러스터 간의 통신은 느슨하게 결합 하 여 클러스터 설정 "마스터" (CS 마스터)를 호출 하는 새 클러스터 리소스에서 조정 됩니다. 다른 모든 클러스터 리소스 처럼 CS-마스터는 항상 사용 가능 하 고 관리 클러스터 노드 실패 및/또는 개별 멤버 클러스터 오류에 탄력적으로 대처할입니다. 새 클러스터 설정 WMI 공급자를 통해 CS 마스터 모든 클러스터 설정 관리 상호 작용에 대 한 관리 끝점을 제공합니다.

**클러스터 작업자 설정**

클러스터 설정 배포에서 CS 마스터 멤버 "클러스터 설정 작업자" (CS-작업자)을 호출 하는 클러스터에서 새 클러스터 리소스와 상호 작용 합니다. CS 작업자에서 유일한 담당자로 CS 마스터 요청에 따라 로컬 클러스터 상호 작용을 오케스트레이션 하는 클러스터에서 작동 합니다. 이러한 상호 작용의 예로 가상 머신 배치 및 클러스터 지역 리소스 인벤토리를 들 수 있습니다. 클러스터 집합의 각 멤버에 대 한 CS 작업자 인스턴스 클러스터 하나 뿐입니다. 

**장애 도메인**

장애 도메인은 소프트웨어의 그룹화 하 고 오류가 발생 하는 경우 관리자가 결정 하는 하드웨어 아티팩트 함께 실패할 수 있습니다.  관리자는 장애 도메인으로 하나 이상의 클러스터를 함께 지정할 수, 하는 동안 각 노드의 가용성 집합의 장애 도메인에 참여할 수 없습니다. 클러스터 설정 하는 디자인 유지 하 여 장애 도메인 경계 확인을 결정 하는 관리자에 게는 데이터 센터 토폴로지 고려 사항-예: PDU 사용 하 여 정통한 네트워킹-멤버 클러스터를 공유 합니다. 

**가용성 집합**

가용성 집합에는 가용성 집합에 구성 하 고 해당 가용성 집합에 워크 로드를 배포 하 여 장애 도메인에 걸쳐 클러스터형된 워크 로드의 원하는 중복성을 구성 하는 관리자 수 있습니다. 2 계층 응용 프로그램을 배포 하는 경우는 해당 가용성 집합에 하나의 장애 도메인 떨어지면 응용 프로그램은 이상 있는지 확인 하는 각 계층을 위해 가용성 집합에서 두 개 이상의 가상 컴퓨터를 구성 하는 것이 좋습니다를 가정해 보겠습니다 가상 컴퓨터는 동일한 가용성 집합에 서로 다른 장애 도메인에서 호스트 되는 각 계층에 하나입니다.

## <a name="why-use-cluster-sets"></a>클러스터 집합을 사용 하는 이유

클러스터 설정 복원 력을 유지 하면서 규모의 혜택을 제공 합니다.  

클러스터 집합 있습니다 여러 클러스터에 클러스터링 함께 각 클러스터의 복원 력을 독립적인 상태를 유지 하는 동안은 큰 패브릭 만들기.  몇 가지 4 개 노드 HCI 있는 예를 들어 클러스터 가상 컴퓨터를 실행 합니다.  각 클러스터 자체에 필요한 복원 력을 제공 합니다.  저장소 또는 메모리 채워지기 시작 되 면 다음 단계는 확장 합니다.  확장을 사용 하 여 일부의 옵션 및 고려 사항입니다.

1. 현재 클러스터에 더 많은 저장소를 추가 합니다.  저장소 공간 다이렉트를 사용 하 여 때문일 까다로운 정확히 동일한 모델/펌웨어 드라이브를 사용할 수 있습니다.  다시 빌드 시간이 고려 해야 고려해 야 합니다.
2. 메모리를 추가하십시오.  경우에 어떻게 하는 최대값을 초과 컴퓨터가 처리할 수 있는 메모리에?  어떤 경우에는 모든 사용 가능한 메모리 슬롯 전체 인가요?
3. 현재 클러스터에 드라이브를 사용 하 여 추가 계산 노드를 추가 합니다.  이 다시 옵션 1로 간주 되기 위해 필요 합니다.
4. 전체 새 클러스터를 구매 합니다.

이 클러스터 집합 크기 조정의 혜택을 제공 하는 위치입니다.  클러스터 집합에 내 클러스터에 추가 하는 경우 저장소 또는 추가 구매 없이 다른 클러스터에서 사용할 수 있는 메모리의 이점은 빼낼 수 있습니다.  복원 력 관점에서 노드를 저장소 공간 다이렉트를 더 추가 하지 않습니다 쿼럼에 대 한 추가 응답을 제공 합니다.  설명 했 듯이 [여기](drive-symmetry-considerations.md), 저장소 공간 다이렉트 클러스터 진행 하기 전에 2 노드의 손실을 감당할 수 있습니다.  4 개 노드 HCI 클러스터가 있는 경우 3 개의 노드가 다운 전체 클러스터를 중지 해야 합니다.  8 노드 클러스터를 사용 하는 경우 3 개의 노드가 다운 전체 클러스터를 중지 해야 합니다.  두 4-노드 HCI 클러스터 집합에 있는 클러스터 집합을 하나의 HCI에 2 개 노드 이동 하 고 다른 HCI 1 노드 다운 두 클러스터가 실행 상태로 유지 합니다.  것이 더 하나의 큰 16 개 노드 저장소 공간 다이렉트 클러스터 만들기 또는 4 4 개 노드 클러스터로 세분화 및 클러스터 집합을 사용 하 시겠습니까?  (예기치 않게 또는 유지 관리를 위해) 여러 계산 노드가 중단 될 수 있습니다에 같은 눈금 하지만 더 나은 복원 력을 클러스터 집합 제공을 사용 하 여 네 개의 4 개 노드 클러스터가 필요 하 고 프로덕션 유지 됩니다.

## <a name="considerations-for-deploying-cluster-sets"></a>클러스터 집합을 배포 하기 위한 고려 사항

클러스터 설정 사용 해야 할 항목 인지를 고려할 때 이러한 질문을 고려 합니다.

- 현재 HCI 계산 및 저장소 크기 조정도 넘어 이동 해야 하나요?
- 모든 계산 및 저장소 동일 하 게 다릅니다?
- 클러스터 간의 가상 컴퓨터를 마이그레이션하려면 라이브 있습니다?
- 시겠습니까 컴퓨터로 Azure 가용성 집합 및 장애 도메인 여러 클러스터 간에?
- 모든 새 가상 컴퓨터를 배치 해야 하는 위치를 확인 하려면 모든 클러스터를 살펴보는 시간이 해야 하나요?

답변 예 인 경우 다음 클러스터 집합을 해야 합니다.

더 큰 SDDC 전체 데이터 센터 전략을 변경 될 수 있습니다 위치를 고려해 야 할 다른 몇 가지 항목이 있습니다.  SQL Server에는 좋은 예입니다.  클러스터 간에 SQL Server 가상 컴퓨터를 이동 추가 노드에서 실행 하는 SQL 라이선스 필요 합니까?  

## <a name="scale-out-file-server-and-cluster-sets"></a>스케일 아웃 파일 서버 및 클러스터 집합

Windows Server 2019에 인프라 스케일 아웃 파일 서버 (SOFS) 이라는 새 스케일 아웃 파일 서버 역할을 있습니다. 

인프라 SOFS 역할에 다음과 같은 고려 사항이 적용 됩니다.

1.  장애 조치 클러스터에서 인프라 SOFS 클러스터 역할을 최대 하나만 있을 수 있습니다. 인프라 SOFS 역할을 지정 하 여 만들를 "**-인프라**" 매개 변수를 전환 합니다 **추가 ClusterScaleOutFileServerRole** cmdlet.  예를 들어 다음과 같은 가치를 제공해야 합니다.

        Add-ClusterScaleoutFileServerRole -Name "my_infra_sofs_name" -Infrastructure

2.  장애 조치에 자동으로 생성 된 각 CSV 볼륨 CSV 볼륨 이름을 기반으로 자동으로 생성 된 이름을 사용 하 여 SMB 공유의 생성을 트리거합니다. 직접 관리자로 만들거나 CSV 볼륨 만들기/수정 작업을 통해 다른 작업 보다는 SOFS 역할로 SMB 공유를 수정할 수 없습니다.

3.  하이퍼 수렴 형 구성에서 인프라 SOFS에는 SMB 클라이언트를 (Hyper-v 호스트)을 사용 하 여 보장 된 지속적인 가용성 (CA) 인프라 SOFS SMB 서버에 전달할 수 있습니다. 이 하이퍼 수렴 형 SMB 루프백 CA는 소유 하는 가상 머신 id 클라이언트와 서버 간에 전달 되는 해당 가상 디스크 (VHDx) 파일에 액세스 하는 가상 머신을 통해 수행 됩니다. 이 identity 전달 하기 전에 표준 하이퍼 수렴 형 클러스터 구성으로 마찬가지로 ACL 현재 진행형 VHDx 파일을 수 있습니다.

클러스터 집합을 만든 후 클러스터 집합 네임 스페이스 멤버는 클러스터의 각 인프라 SOFS 및 또한 인프라 SOFS 관리 클러스터에 의존 합니다.

시 멤버 클러스터 관리자가 이미 있는 경우 해당 클러스터에서 인프라 SOFS의 이름을 지정 클러스터 집합에 추가 됩니다. 인프라 SOFS 존재 하지 않는 경우에 새 멤버 클러스터에서 새 인프라 SOFS 역할을이 작업에 의해 만들어집니다. 인프라 SOFS 역할을 멤버 클러스터에 이미 있으면 추가 작업이 암시적으로 바꿉니다 지정된 된 이름으로 필요에 따라 합니다. 모든 기존 단일 SMB 서버 또는 클러스터 집합에 의해 사용 하지 않으면 클러스터는 남아 있는 멤버에 비-인프라 SOFS 역할입니다. 

클러스터 집합을 만든 경우 관리자는 관리 클러스터에서 네임 스페이스 루트로 기존 AD 컴퓨터 개체를 사용 하는 옵션을 갖습니다. 클러스터 집합 생성 작업은 인프라 SOFS 클러스터 역할 관리 클러스터에서 만들거나 바로 앞에서 설명한 대로 클러스터 구성원에 대 한 기존 인프라 SOFS 역할의 이름을 바꿉니다. 관리 클러스터에서 인프라 SOFS 클러스터에는 네임 스페이스 조회 (클러스터 설정 Namespace) SOFS 설정 됩니다. 단순히 각 SMB 공유 클러스터에서 SOFS가이 미리 보기 릴리스에서 새로 도입 된 형식 'SimpleReferral'--의 조회에 대 한 공유 네임 스페이스 설정 있는지를 의미 합니다.  이 조회 멤버 클러스터 SOFS에서 호스트 된 SMB 클라이언트가 SMB 공유 대상에 액세스할 수 있습니다. 클러스터는 I/O 경로에서 SOFS는 간단한 조회 메커니즘이 며 따라서 참여 하지 않는 네임 스페이스 조회를 설정 합니다. SMB 조회 클라이언트 노드의 각 영구적 캐시 되 고 클러스터 집합 네임 스페이스 동적으로 자동으로 이러한 조회 필요에 따라 업데이트

## <a name="creating-a-cluster-set"></a>클러스터 집합 만들기

### <a name="prerequisites"></a>사전 요구 사항

클러스터를 만드는 설정 하는 경우 다음 필수 구성 요소 것이 좋습니다.

1. 최신 Windows Server Insider 릴리스를 실행 하는 관리 클라이언트를 구성 합니다.
2. 이 관리 서버에서 장애 조치 클러스터 도구를 설치 합니다.
3. 클러스터 구성원 (두 개 이상의. 클러스터 각 클러스터에서 두 개 이상의 클러스터 공유 볼륨 사용 됨) 만들기
4. 멤버 클러스터를 포괄 하는 관리 클러스터를 (실제 또는 게스트)를 만듭니다.  이 방법을 사용 하면 관리 평면 계속 가능한 멤버 클러스터 실패 했 어도 사용할 수는 클러스터 집합입니다.

### <a name="steps"></a>단계

1. 필수 구성 요소에 정의 된 3 개의 클러스터에서 설정 하는 새 클러스터를 만듭니다.  차트 아래에 만들려는 클러스터의 예제를 제공 합니다.  이 예제에서 클러스터의 이름은 **CSMASTER**합니다.

   | 클러스터 이름               | 나중에 사용 하도록 인프라 SOFS 이름 | 
   |----------------------------|-------------------------------------------|
   | 집합 클러스터                | SOFS-CLUSTERSET                           |
   | CLUSTER1                   | SOFS-CLUSTER1                             |
   | 클러스터 2                   | SOFS-CLUSTER2                             |

2. 모든 클러스터를 만든 후 클러스터 집합 마스터를 만들려면 다음 명령을 사용 합니다.

        New-ClusterSet -Name CSMASTER -NamespaceRoot SOFS-CLUSTERSET -CimSession SET-CLUSTER

3. 클러스터 서버 클러스터 집합에 추가 하는 아래 사용 됩니다.

        Add-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER1
        Add-ClusterSetMember -ClusterName CLUSTER2 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER2

   > [!NOTE]
   > 정적 IP 주소 체계를 사용 하는 경우를 포함 해야 *-StaticAddress x.x.x.x* 에 **새로 만들기-ClusterSet** 명령입니다.

4. 클러스터 구성원에서 설정 하는 클러스터를 만든 후에 노드 집합 및 해당 속성을 나열할 수 있습니다.  모든 멤버를 열거 클러스터 집합에 클러스터:

        Get-ClusterSetMember -CimSession CSMASTER

5. 모든 멤버를 열거 관리 클러스터 노드를 포함 하 여 설정 하는 클러스터에서 클러스터:

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterNode

6. 멤버 클러스터에서 노드를 모두 나열:

        Get-ClusterSetNode -CimSession CSMASTER

7. 클러스터 집합에 대해 모든 리소스 그룹을 나열:

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterGroup 

8. 클러스터를 확인 하려면 생성 프로세스 (Volume1 또는 인프라 파일 서버 및 경로 모두로 이름이 되죠 ScopeName를 사용 하 여 어떤 CSV 폴더 라고 식별) SMB 공유를 하나 만든 인프라 SOFS에서 각 클러스터 구성원에 대 한 설정 CSV 볼륨:

        Get-SmbShare -CimSession CSMASTER

8. 클러스터 집합에 검토를 위해 수집할 수 있는 디버그 로그가 있습니다.  클러스터 설정 및 관리 클러스터 및 모든 멤버에 대 한 클러스터 디버그 로그를 수집할 수 있습니다.

        Get-ClusterSetLog -ClusterSetCimSession CSMASTER -IncludeClusterLog -IncludeManagementClusterLog -DestinationFolderPath <path>

9. Kerberos를 구성 [제한 된 위임](https://blogs.technet.microsoft.com/virtualization/2017/02/01/live-migration-via-constrained-delegation-with-kerberos-in-windows-server-2016/) 모든 클러스터 간에 멤버를 설정 합니다.

10. 설정 하는 클러스터의 각 노드에서 클러스터 간 가상 컴퓨터 실시간 마이그레이션을 인증 형식을 Kerberos 구성 합니다.

        foreach($h in $hosts){ Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos -ComputerName $h }

11. 클러스터 집합의 각 노드에서 로컬 관리자 그룹에 관리 클러스터를 추가 합니다.

        foreach($h in $hosts){ Invoke-Command -ComputerName $h -ScriptBlock {Net localgroup administrators /add <management_cluster_name>$} }

## <a name="creating-new-virtual-machines-and-adding-to-cluster-sets"></a>새 virtual machines 만들기 및 클러스터 집합에 추가 합니다.

설정한 클러스터를 만든 후 다음 단계는 새 가상 컴퓨터를 만드는 것입니다.  일반적으로 가상 컴퓨터를 만들고 클러스터에 추가 하는 데 시간이 되 면 클러스터에서 실행할 수 있습니다는 참조에 대해 몇 가지 검사를 수행 해야 합니다.  이러한 검사는 다음과 같습니다.

- 메모리의 양을 클러스터 노드에서 사용할 수 있는 기능
- 클러스터 노드에서 사용 가능한 디스크 공간이 얼마나?
- 가상 컴퓨터에는 특정 저장소 요구 사항 (즉, 더 빠른 드라이브가;를 실행 하는 클러스터로 SQL Server virtual machines 내 원하는 또는 인프라 가상 머신 내 중요 하지 않은 및 속도가 느린 드라이브에서 실행할 수 있습니다) 필요.

이 질문에 대 한 대답이 되 면 되도록 해야 하는 클러스터에 가상 머신을 만듭니다.  클러스터 집합의 이점 중 하나는 클러스터 집합 수에 대 한 이러한 검사를 수행 하 고 최적의 노드에서 가상 컴퓨터를 배치 합니다.

아래 명령을 모두 최적의 클러스터를 식별 되며 가상 컴퓨터를 배포 합니다.  에 아래 예제에서는 새 가상 머신을 만들어집니다 지정 최소 4gb의 메모리를 가상 머신에 대해 사용할 수 있는지 및 1 개 가상 프로세서를 활용 해야 합니다.

- 4gb를 가상 머신에 대해 사용할 수 있는지 확인 합니다.
- 1에서 사용 되는 가상 프로세서를 설정 합니다.
- 10% 이상 없는지 확인 가상 머신에 대해 사용할 수 있는 CPU

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

완료 되 면 가상 머신에 대 한에 배치 된 위치 정보를 제공 됩니다.  위의 예에서으로 표시 됩니다.

        State         : Running
        ComputerName  : 1-S2D2

에 없는 다음 충분 한 메모리, cpu 또는 디스크 공간이 가상 머신을 추가 하는 경우 오류가 표시 됩니다.

      Get-ClusterSetOptimalNodeForVM : A cluster node is not available for this operation.  

가상 컴퓨터를 만든 후 지정 된 특정 노드에서 Hyper-v 관리자에서 표시 됩니다.  클러스터를 virtual machine을 설정 및 클러스터에 추가, 명령은 다음과 같습니다.  

        Register-ClusterSetVM -CimSession CSMASTER -MemberName $targetnode.Member -VMName CSVM1

완료 되 면 출력이 됩니다.

         Id  VMName  State  MemberName  PSComputerName
         --  ------  -----  ----------  --------------
          1  CSVM1      On  CLUSTER1    CSMASTER

기존 가상 컴퓨터를 사용 하 여 클러스터를 추가한 경우에 가상 컴퓨터를 설정 하므로 모든 가상 컴퓨터를 한 번에 사용 하도록 명령을 등록 하는 클러스터를 사용 하 여 등록할도 해야 합니다.

        Get-ClusterSetMember -name CLUSTER3 -CimSession CSMASTER | Register-ClusterSetVM -RegisterAll -CimSession CSMASTER

그러나 가상 컴퓨터에 대 한 경로 클러스터 집합 네임 스페이스에 추가 해야 하는 대로 프로세스 완전 하지 않습니다.

예를 들어 기존 클러스터 추가 되 고 있기 미리 구성 된 가상 컴퓨터는 reside에는 로컬 공유 볼륨 (CSV (클러스터), VHDX에 대 한 경로 것 "C:\ClusterStorage\Volume1\MYVM\Virtual 하드 Disks\MYVM.vhdx 비슷한.  저장소 마이그레이션 CSV 경로 기본적으로 단일 멤버 클러스터에 로컬 작업을 수행할 수 해야 합니다. 따라서 됩니다 가상 컴퓨터에 액세스할 수 있는 라이브가 멤버 클러스터 간 마이그레이션. 

이 예제에서는 CLUSTER3 인프라 스케일 아웃 파일 서버를 사용 하 여 추가 ClusterSetMember를 사용 하 여 SOFS CLUSTER3로 설정 하는 클러스터에 추가 되었습니다.  가상 머신 구성 및 저장소를 이동 하려면 명령은 다음과 같습니다.

        Move-VMStorage -DestinationStoragePath \\SOFS-CLUSTER3\Volume1 -Name MYVM

완료 되 면 경고가 표시 됩니다.

        WARNING: There were issues updating the virtual machine configuration that may prevent the virtual machine from running.  For more information view the report file below.
        WARNING: Report file location: C:\Windows\Cluster\Reports\Update-ClusterVirtualMachineConfiguration '' on date at time.htm.

이 경고는 "가상 컴퓨터 역할 저장소 구성에서 변경 없이 발견 되었습니다." 경고는 무시할 수 있습니다.  실제 물리적 위치와 경고에 대 한 이유는 변경 되지 않습니다. 에 구성 경로입니다. 

Move-vmstorage에 대 한 자세한 내용은 살펴보시기 이렇게 [링크](https://docs.microsoft.com/powershell/module/hyper-v/move-vmstorage?view=win10-ps)합니다. 

다른 클러스터 집합 클러스터 간의 가상 컴퓨터를 마이그레이션하면 라이브는 과거와는 동일 합니다. 비 클러스터 집합 시나리오의 단계를 것입니다.

1. 클러스터에서 가상 컴퓨터 역할을 제거 합니다.
2. 멤버 노드를 다른 클러스터의 가상 컴퓨터 실시간 마이그레이션.
3. 새 가상 컴퓨터 역할을 클러스터에 가상 컴퓨터를 추가 합니다.

클러스터 집합을 사용 하 여 이러한 단계는 필요 하 고 명령을 하나만 필요 합니다.  예를 들어 CLUSTER1에서 CLUSTER3 NODE2 CL3에 클러스터 설정 가상 컴퓨터를 이동 하려고 합니다.  단일 명령은 다음과 같습니다.

        Move-ClusterSetVM -CimSession CSMASTER -VMName CSVM1 -Node NODE2-CL3

가상 컴퓨터 저장소 또는 구성 파일을 이동 하지 않습니다이 note 하십시오.  가상 컴퓨터에 대 한 경로 그대로으로 필요 없는 \\SOFS CLUSTER1\VOLUME1 합니다.  가상 컴퓨터 등록 되 면 클러스터 집합을 사용 하 여 인프라 파일 서버 공유 경로 드라이브 및 가상 컴퓨터를 하지 않아도 되는 가상 컴퓨터와 동일한 컴퓨터에 있습니다.

## <a name="creating-availability-sets-fault-domains"></a>장애 도메인 설정 유지

소개에서 설명한 대로, 같은 Azure 장애 도메인 및 가용성 집합 클러스터 집합에 구성할 수 있습니다.  초기 가상 머신 배치 및 클러스터 간의 마이그레이션에 유용합니다.  

아래 예제에서는 클러스터 집합에 참여 하는 네 개의 클러스터가 있습니다.  집합 내에서 논리 장애 도메인은 클러스터 및 다른 두 클러스터를 사용 하 여 만든 장애 도메인이 두 개의 만들어집니다.  이러한 두 장애 도메인에는 가용성 집합을 구성 하는 합니다. 

아래 예제에서 CLUSTER1 및 클러스터 2 됩니다 이라고 하는 장애 도메인 **FD1** CLUSTER3 및 CLUSTER4 호출 하는 장애 도메인 수 있지만 **FD2**합니다.  가용성 집합을 호출할 **CSMASTER-AS** 하며 두 장애 도메인의로 구성 되어야 합니다.

장애 도메인을 만들려면 명령은 다음과 같습니다.

        New-ClusterSetFaultDomain -Name FD1 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER1,CLUSTER2 -Description "This is my first fault domain"

        New-ClusterSetFaultDomain -Name FD2 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER3,CLUSTER4 -Description "This is my second fault domain"

성공적으로 만들어진 경우 위해 Get ClusterSetFaultDomain 표시 된 해당 출력을 사용 하 여 실행할 수 있습니다.

        PS C:\> Get-ClusterSetFaultDomain -CimSession CSMASTER -FdName FD1 | fl *

        PSShowComputerName    : True
        FaultDomainType       : Logical
        ClusterName           : {CLUSTER1, CLUSTER2}
        Description           : This is my first fault domain
        FDName                : FD1
        Id                    : 1
        PSComputerName        : CSMASTER

장애 도메인을 만든 했으므로 가용성 집합을 만들어야 합니다.

        New-ClusterSetAvailabilitySet -Name CSMASTER-AS -FdType Logical -CimSession CSMASTER -ParticipantName FD1,FD2

유효성을 검사할를 만든 다음 사용 하 여:

        Get-ClusterSetAvailabilitySet -AvailabilitySetName CSMASTER-AS -CimSession CSMASTER

새 가상 컴퓨터를 만들 때 최적의 노드 결정의 일환으로-AvailabilitySet 매개 변수를 사용 해야 합니다.  그런 다음 다음과 같이 표시 됩니다 하므로:

        # Identify the optimal node to create a new virtual machine
        $memoryinMB=4096
        $vpcount = 1
        $av = Get-ClusterSetAvailabilitySet -Name CSMASTER-AS -CimSession CSMASTER
        $targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10 -AvailabilitySet $av
        $secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
        $cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)

클러스터에서 클러스터를 제거 하는 작업은 다양 한 수명 주기 인해 설정 합니다. 클러스터를 클러스터 집합에서 제거 해야 하는 경우 경우가 있습니다. 모범 사례로, 모든 클러스터 집합의 가상 컴퓨터를 클러스터 외부로 옮겨야 합니다. 사용 하 여 수행할 수 있습니다 합니다 **이동 ClusterSetVM** 하 고 **Move-vmstorage** 명령입니다.

그러나 가상 컴퓨터도 이동 하지 것입니다, 경우 클러스터 집합 일련의 관리자에 게 직관적인 결과 제공 하는 작업을 실행 합니다.  클러스터 집합에서 제거 되 면 모든 나머지 클러스터 집합 호스트 된 가상 머신을 제거 하 고 클러스터에 단순히 항상 사용 가능한 가상 컴퓨터를 해당 저장소에 액세스할 수 있다는 가정 하는 클러스터에 연결 됩니다.  클러스터 집합으로 해당 인벤토리를 자동으로 업데이트 됩니다.

- 지금 제거 클러스터 및에서 실행 중인 virtual machines의 상태를 더 이상 추적
- 클러스터 집합 네임 스페이스는 이제 제거 클러스터에서 호스트 되는 공유에 대 한 모든 참조를 제거 합니다.

예를 들어 CLUSTER1 클러스터 클러스터 집합에서 제거할 명령은 다음과 같습니다.

        Remove-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER

## <a name="frequently-asked-questions-faq"></a>FAQ(질문과 대답)

**질문:** 내 클러스터 집합에 제한만 하이퍼 수렴 형 클러스터를 사용 하 시겠습니까? <br>
**대답:** 아니요.  기존 클러스터를 사용 하 여 저장소 공간 다이렉트을 혼합할 수 있습니다.

**질문:** 내 클러스터 설정 System Center Virtual Machine Manager 통해 관리할 수 있나요? <br>
**대답:** System Center Virtual Machine Manager 클러스터 집합을 현재 지원 하지 않습니다. <br><br> **질문:** Windows Server 2012 R2 또는 2016 클러스터에서에서 공존할 수 있습니다 동일한 클러스터 집합? <br>
**질문:** Windows Server 2012 R2 워크 로드 마이그레이션 수 또는 해당 클러스터를 간단히 함으로써 2016 클러스터를 동일한 클러스터 집합을 조인? <br>
**대답:** 클러스터 집합은 새로운 기술을 Windows Server Preview에 도입 되 고 빌드를 이와 같이 하므로에 존재 하지 않는 이전 버전입니다. 하위 수준 OS 기반 클러스터는 클러스터 집합에 가입할 수 없습니다. 그러나 클러스터 운영 체제 롤링 업그레이드 기술에는 Windows Server 2019로 이러한 클러스터를 업그레이드 하 여 찾고 있는 마이그레이션 기능을 제공 해야 합니다.

**질문:** 클러스터 집합 저장소의 크기를 조정 하거나 계산 (단독)를 허용 합니까? <br>
**대답:** 예, 저장소 공간 다이렉트 또는 기존 Hyper-v 클러스터를 추가 하기만 하면 됩니다. 클러스터 집합을 사용 하 여 하이퍼 수렴 형 클러스터 집합에도 계산-저장소 비율 간단 하 게 변경 될 합니다.

**질문:** 클러스터 집합에 대 한 관리 도구는 무엇입니까 <br>
**대답:** PowerShell 또는 WMI이 릴리스에서 합니다.

**질문:** 다양 한 세대의 프로세서를 사용 하 여 클러스터 간 실시간 마이그레이션 작업을?  <br>
**대답:** 클러스터 집합 프로세서 차이점 해결 되지 않으며 Hyper-v 현재 지 원하는 것 보다 우선 합니다.  따라서 quick migration을 사용 하 여 프로세서 호환성 모드를 사용 해야 합니다.  발생 하도록 클러스터 간에 실시간 마이그레이션을 위해 전체 클러스터 설정 뿐만 아니라 각 개별 클러스터 내에서 동일한 프로세서 하드웨어를 사용 하는 클러스터 집합에 대 한 것이 좋습니다.

**질문:** 수 내 클러스터 집합 가상 컴퓨터 자동으로 장애 조치 클러스터 실패 시?  <br>
**대답:** 이 릴리스에서 클러스터 집합 가상 머신에 마이그레이션할 수 있습니다 수동으로 live-클러스터;에서 하지만 자동으로 장애 조치 수 없습니다. 

**질문:** 저장소는 클러스터 장애에 복원 력이 확인 하는 방법에서는? <br>
**대답:** 클러스터 오류에 저장소 복원 력을 실현 하는 데 멤버 클러스터 간에 클러스터 간 저장소 복제 (SR) 솔루션을 사용 합니다.

**질문:** 멤버 클러스터 간에 복제 저장소 복제 (SR)를 사용 합니다. 복제 대상 저장소 공간 다이렉트 클러스터에 SR 장애 조치 시 UNC 경로 변경 집합 네임 스페이스 저장소를 클러스터 수행? <br>
**대답:** 이 릴리스에서 이러한 클러스터 집합 네임 스페이스 조회 변경 SR 장애 조치를 사용 하 여 발생 하지 않습니다. 이 시나리오는 하 고 사용 하려는 방법에 중요 한 경우 Microsoft에 알리려고 하세요.

**질문:** 재해 복구 상황에서 오류 도메인 간에 가상 머신을 장애 조치 수는 (예: 전체 장애 도메인을 다운)? <br>
**대답:** 아니요, 해당 클러스터 간 장애 조치 확인 오류 논리적 내에서 도메인은 아직 지원 되지 않습니다. 

**질문:** 클러스터가 여러 사이트 (또는 DNS 도메인)에서 범위 클러스터를 설정할 수 있습니까? <br> 
**대답:** 테스트 시나리오를 이며 프로덕션 지원에 대 한 계획 된 즉시는 아닙니다. 이 시나리오는 하 고 사용 하려는 방법에 중요 한 경우 Microsoft에 알리려고 하세요.

**질문:** 클러스터를 집합 IPv6와 함께 작동 합니까? <br>
**대답:** IPv4 및 IPv6 모두 클러스터 집합을 사용 하 여 장애 조치 클러스터와 마찬가지로 지원 됩니다.

**질문:** 클러스터에 대 한 Active Directory 포리스트 요구 사항은 무엇입니까 설정 <br>
**대답:** 모든 멤버 클러스터는 동일한 AD 포리스트에 있어야 합니다.

**질문:** 얼마나 많은 클러스터 또는 노드 단일 클러스터에 속하지 설정할 수 있습니까? <br>
**대답:** 클러스터 집합 미리 보기에서 테스트를 거쳐 최대 64 개의 총 클러스터 노드를 지원 합니다. 그러나 클러스터 훨씬 더 큰 제한 아키텍처 눈금을 설정 하 고 항목이 아니라 제한에 대 한 하드 코딩 됩니다. 더 큰 규모와 사용 하려는 방법에 중요 한 경우 Microsoft에 알리려고 하세요.

**질문:** 클러스터 집합에 있는 모든 저장소 공간 다이렉트 클러스터를 단일 저장소 풀을 형성 하는? <br>
**대답:** 아니요. 저장소 공간 다이렉트 기술을 단일 클러스터 내 및 클러스터 집합의 멤버 클러스터 전체가 아닌에 여전히 작동합니다.

**질문:** 클러스터에 항상 사용 가능한 네임 스페이스 설정 되어 있습니까? <br>
**대답:** 예, 클러스터 집합 네임 스페이스는 관리 클러스터에서 실행 되는 지속적으로 사용할 수 있는 ca (인증) 조회 SOFS 네임 스페이스 서버를 통해 제공 됩니다. 충분 한 수 있도록 복원 력 있는 지역화 된 클러스터 전체의 오류 멤버 클러스터에서 virtual machines의 것이 좋습니다. 그러나 예측할 수 없는 치명적인 오류 – 예의 모든 virtual machines 관리 클러스터를 동시에 다운 – 위해서 조회 정보를 영구적으로 또한에 캐시 됩니다 각 클러스터 집합 노드를 재부팅 간에.
 
**질문:** 클러스터는 클러스터 집합의 저장소 성능을 저하 시킵니까 네임 스페이스 기반 저장소 액세스 집합 합니까? <br>
**대답:** 아니요. 클러스터 집합 네임 스페이스는 개념적으로 같은 분산 파일 시스템 네임 스페이스 (DFSN () – 클러스터 묶어서 오버레이 조회 네임 스페이스를 제공합니다. DFSN, 달리 모든 클러스터 집합 네임 스페이스 조회 메타 데이터는 자동으로 채워진 및 관리자 개입 없이 모든 노드에서 자동으로 업데이트 하므로 성능 오버 헤드가 거의 없습니다 저장소 액세스 경로 

**질문:** 클러스터 집합 메타 데이터를 백업 하려면 어떻게 해야 하나요? <br>
**대답:** 이 지침은 장애 조치 클러스터와 동일합니다. 시스템 상태 백업 클러스터 상태를 사용할 경우에 백업 됩니다.  Windows Server Backup을 통해 방금 노드의 클러스터 데이터베이스 (다양 한 자동 복구 논리 것 때문에 필요 하지는)의 복원을 수행할 수 있습니다 또는 노드 전반에 걸쳐 클러스터 전체 데이터베이스를 롤백하려면 정식 복원을 수행 합니다. 클러스터 집합의 경우 필요한 경우 멤버 클러스터 관리 클러스터 한 다음 먼저 이러한 정식 복원을 수행 하는 것이 좋습니다. 
