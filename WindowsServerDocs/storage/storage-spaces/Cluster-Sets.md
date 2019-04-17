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
ms.sourcegitcommit: 07aefbdbb0eedb42aaed3d195c2429310c761da0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2019
ms.locfileid: "9041009"
---
# 클러스터 집합

> 적용 대상: Windows Server Insider Preview 빌드 17650 이상

클러스터 집합의 크기가 단일 소프트웨어 정의 데이터 센터 (SDDC) 클라우드에서 클러스터 노드 수 증가 하는이 미리 보기 릴리스의 새로운 클라우드 스케일 아웃 기술입니다. 클러스터 집합은 여러 장애 조치 클러스터의 느슨하게 결합 된 그룹: 컴퓨팅, 저장소 또는 하이퍼 수렴 형 합니다. 클러스터 설정 기술을 사용 하면 가상 컴퓨터 유연성 클러스터 세트와 통합 된 저장소 네임 스페이스 내에서 멤버 클러스터 간에 가상 컴퓨터 유연성 지원 하기 위해 집합입니다. 

보존 기존 장애 조치 클러스터 관리 구성원 클러스터의 경험을 하는 동안 클러스터 집합 인스턴스를는 또한 집계에 수명 주기 관리 키 사용 사례를 제공 합니다. 이 Windows Server 미리 보기 시나리오 평가 가이드 PowerShell을 사용 하 여 클러스터 집합 기술 평가 하는 단계별 지침과 함께 필요한 배경 정보를 제공 합니다. 

## 기술 소개

클러스터 집합 기술은 소프트웨어 정의 데이터 센터 (SDDC) 클라우드 규모에서 작동 하는 특정 고객 요청에 맞게 개발 됩니다. 이 미리 보기 릴리스의 클러스터 집합 가치는 다음과 같이 요약할 수 있습니다.  

- 단일 클러스터에 소프트웨어 오류 경계를 유지 하면서도 단일 큰 패브릭에 여러 개의 더 작은 클러스터를 결합 하 여 항상 사용 가능한 가상 컴퓨터를 실행 하기 위한 지원 되는 SDDC 클라우드 규모를 크게 증가
- 전체 좋아야 마이그레이션 통해 테 넌 트 가상 컴퓨터 가용성에 영향을 주지 않고 장애 조치 클러스터 수명 주기 온 보 딩을 포함 하 고 일부 터 사용 중지 클러스터 관리이 큰 패브릭에서 가상 컴퓨터
- 쉽게에 하이퍼 컨 버 지 드에 저장소로 계산 비율을 변경 하려면
- 초기 가상 컴퓨터 배치 및 후속 가상 컴퓨터 마이그레이션에 클러스터 간에 [Azure와 유사한 오류 도메인 및 가용성 설정](htttps://docs.microsoft.com/azure/virtual-machines/windows/manage-availability) 에서 혜택
- 혼합 일치 세대에 따라 다른 CPU 하드웨어의 동일한 클러스터에 최대 효율성을 위해 동종 개별 장애 도메인을 유지 하는 동안에 패브릭을 설정 합니다.  동일한 하드웨어의 권장 각 개별 클러스터 뿐 아니라 전체 클러스터 세트 내에서 여전히 존재는 note 하세요.

상위 수준 보기에서 어떤 클러스터 집합 유사할 수입니다.

![클러스터 솔루션 보기 설정](media\Cluster-sets-Overview\Cluster-sets-solution-View.png)

다음은 위 이미지에 있는 요소의 각각의 빠른 요약입니다.

**관리 클러스터**

클러스터 집합에서 관리 클러스터 전체 클러스터 세트와 통합 된 저장소 네임 스페이스 (클러스터 설정 Namespace) 조회 스케일 아웃 파일 서버 (SOFS)의 가용성이 관리 평면을 호스팅하는 장애 조치 클러스터는입니다. 관리 클러스터는 논리적으로 가상 컴퓨터 워크 로드를 실행 하는 멤버 클러스터에서 분리 합니다. 따라서 모든 지역화 된 클러스터 전체의 풍부한 오류 복원 관리 평면 설정 클러스터 구성원 클러스터의 예: 손실 됩니다.   

**구성원 클러스터**

클러스터 집합의 멤버 클러스터는 일반적으로 가상 컴퓨터와 저장소 공간 다이렉트 워크 로드를 실행 하는 기존의 하이퍼 수렴 형 클러스터. 여러 구성원 클러스터 더 큰 SDDC 클라우드 패브릭 형성 하는 단일 클러스터 집합 배포에 참여 합니다. 두 가지 주요 측면의 관리 클러스터에서 다른 멤버 클러스터: 장애 도메인에 참여 하는 멤버 클러스터 가용성 구조를 설정 하 고 멤버 클러스터도 호스트 가상 컴퓨터 및 저장소 공간 다이렉트 작업에 맞게 크기가 조정 됩니다. 이러한 이유로 관리 클러스터에서 클러스터 집합에서 클러스터 경계에서 이동 하는 클러스터 집합 가상 컴퓨터를 호스팅할 수 있어야 합니다.

**클러스터 네임 스페이스 조회 SOFS 설정**

클러스터 집합 네임 스페이스 조회 (클러스터 설정 Namespace) SOFS는 하는데 각 SMB 공유 클러스터 설정 Namespace SOFS에는 'SimpleReferral'이 미리 보기 버전에 새로 도입 된 유형의 조회 공유 – 스케일 아웃 파일 서버.  이 참조 서버 메시지 블록 (SMB) 클라이언트 SOFS 구성원 클러스터에 호스트 된 SMB 공유 대상에 대 한 액세스를 허용 합니다. 클러스터는 I/O 경로에 SOFS는 경량 조회 메커니즘 및 이와 같이 참여 하지 않는 네임 스페이스 참조를 설정 합니다. SMB 조회에서 각 클라이언트 노드의 그리며 캐시 된 및 클러스터 집합 네임 스페이스 동적으로 자동으로 이러한 추천 필요에 따라 업데이트 합니다.

**클러스터 마스터를 설정합니다.**

클러스터 집합의 멤버 클러스터 간 통신 느슨하게 결합 하 고 "클러스터 설정 마스터" (CS 마스터) 라는 새 클러스터 리소스 조정 됩니다. 다른 클러스터 리소스와 같이 CS 마스터 가용성과 개별 멤버 클러스터 오류 및/또는 관리 클러스터 노드 장애 복원 됩니다. 새 클러스터 설정 WMI 공급자를 통해 CS 마스터 모든 클러스터 설정 관리 효율성 조작에 대 한 관리 끝점을 제공합니다.

**클러스터 작업자 설정**

클러스터 집합 배포에서는 CS 마스터 구성원 "클러스터 설정 작업자" (CS 작업자) 라는 클러스터에서 새 클러스터 리소스와 상호 작용 합니다. CS 작업자 CS 마스터 요청 로컬 클러스터 상호 작용을 조정 하려면 클러스터에서 유일한 연락 담당자 역할을 합니다. 이러한 상호 작용의 예로 가상 컴퓨터 배치 및 클러스터 로컬 리소스 인벤토리를 들 수 있습니다. 클러스터 집합의 각 구성원에 대 한 CS 작업자 인스턴스 클러스터 하나 뿐입니다. 

**장애 도메인**

장애 도메인은 소프트웨어의 그룹 및 관리자가 결정 하는 하드웨어 아티팩트는 오류가 발생 하는 경우 함께 실패할 수 있습니다.  관리자 수 하나 이상의 클러스터 함께으로 장애 도메인을 지정 하는 동안 각 노드에 가용성 집합에서 장애 도메인에 참여할 수 있습니다. 예: PDU – 데이터 센터 토폴로지 고려 사항의 경우 잘 알고 있는 관리자에 게 오류 도메인 경계 결정을 결정 하는 디자인 그대로 유지 하 여 설정 클러스터 네트워킹 – 구성원 클러스터를 공유 합니다. 

**가용성 설정**

가용성 설정 된 가용성 집합으로 구성 하 고 해당 가용성 세트로 워크 로드를 배포 하 여 오류 도메인에서 클러스터 된 워크 로드의 원하는 중복성 구성 관리자는 데 도움이 됩니다. 2 계층 응용 프로그램을 배포 하는 경우 해당 가용성 집합에서 한 장애 도메인 다운 되 면 응용 프로그램은 둘 이상 보장 하는 각 계층에 대 한 설정 가용성에 두 개 이상의 가상 컴퓨터를 구성 하는 것이 좋습니다 경우를 가정해합니다 해당 동일한 사용 가능한 다른 오류 도메인에서 호스트 되는 각 계층에서 하나의 가상 컴퓨터를 설정 합니다.

## 클러스터 집합을 사용 하는 이유

클러스터 집합 복원 력 저하 없이 규모의 혜택을 제공 합니다.  

클러스터 집합 수 여러 개의 클러스터를 클러스터에 대 한 함께 각 클러스터 복원 력을 위해 독립 동안 큰 패브릭이 만듭니다.  예를 들어 여러 4-노드 HCI 있는 클러스터 가상 컴퓨터를 실행 합니다.  각 클러스터 자체에 필요한 복원 력을 제공 합니다.  저장소 또는 메모리 찰 시작 되 면 다음 단계는 크기 조정 합니다.  크기 조정, 사용 하 여 일부의 옵션 및 고려 사항입니다.

1. 현재 클러스터에 저장소를 추가 합니다.  저장소 공간 다이렉트 사용이 수 있습니다 까다로운 정확히 동일한 모델/펌웨어 드라이브를 사용할 수 없습니다.  다시 횟수 고려 고려해 해야 합니다.
2. 더 많은 메모리를 추가 합니다.  경우에 어떻게 하면는 최대값을 초과 컴퓨터 처리할 수 있는 메모리에?  모든 사용 가능한 메모리 슬롯의 서로 다른 경우 전체
3. 현재 클러스터에 드라이브를 사용 하 여 추가 계산 노드를 추가 합니다.  이 다시 옵션 1 것으로 간주 해야 합니다.
4. 완전히 새로운 클러스터 구입

크기 조정의 혜택을 제공 하는 클러스터 집합입니다.  클러스터 집합으로 클러스터에 추가 하는 경우 I 저장소 또는 모든 추가 구매 하지 않고 다른 클러스터에서 사용할 수 있는 메모리의 이용할 수 있습니다.  복원 력 관점에서 저장소 공간 다이렉트에 다른 노드를 추가로 이동 하지 않는 쿼럼에 대 한 추가 응답을 제공 합니다.  언급 한 [여기](drive-symmetry-considerations.md)로 저장소 공간 다이렉트 클러스터 이동 하기 전에 2 노드 손실을 존속 수 있습니다.  4-노드 HCI 클러스터에 있는 경우 3 노드 다운 전체 클러스터를 중단 됩니다.  8-노드 클러스터에 있는 경우 3 노드 다운 전체 클러스터를 중단 됩니다.  두 개의 4-노드 HCI 클러스터 집합에 포함 된 클러스터 집합을 사용 하 여 하나의 HCI의 2 개 노드 이동 하 고 다른 HCI에서 1 개의 노드만 다운, 두 클러스터를 유지 합니다.  것 더 큰 하나의 16-노드 저장소 공간 다이렉트 클러스터 또는 4 개의 4 노드 클러스터 나누는 만들고 클러스터 집합을 사용 하 여?  여러 계산 노드에서 (예기치 않게 또는 유지 관리를 위해) 이동할 수 있다는 점에서 동일한 배율 있지만 더 나은 복원 력 클러스터 설정 된 4 개의 4 노드 클러스터를 가진 및 프로덕션 유지 됩니다.

## 클러스터 집합을 배포 하기 위한 고려 사항

클러스터 집합을 사용 하 여 필요한 것은 경우을 고려할 때 다음이 사항을 고려 합니다.

- 현재 HCI 계산과 저장소가 배율 제한을 초과 이동 해야 합니까?
- 모든 계산과 저장소가 동일 하 게 같지는 않습니다.
- 클러스터 간에 가상 컴퓨터를 마이그레이션할 라이브 수 있나요?
- 시겠습니까 Azure와 유사한 컴퓨터 가용성 집합 및 오류 도메인이 여러 클러스터 간에?
- 새 가상 컴퓨터를 배치 해야 하는 위치를 확인 하려면 모든 클러스터에 대해에 시간을 투자 해야 합니까?

답변이 예 이면 클러스터 집합 필요한로 합니다.

더 큰 SDDC에 전체 데이터 센터 전략 변경 될 수 있는 고려해 야 할 몇 가지 다른 항목이 있습니다.  SQL Server 좋은 예입니다.  클러스터 간에 이동 SQL Server 가상 컴퓨터에서 추가 노드를 실행 하는 SQL 라이선스 필요 합니까?  

## 스케일 아웃 파일 서버 및 클러스터 집합

Windows Server 2019의 인프라 스케일 아웃 파일 서버 (SOFS) 라는 새로운 스케일 아웃 파일 서버 역할 수 있습니다. 

다음 고려 사항이 인프라 SOFS 역할에 적용 됩니다.

1.  장애 조치 클러스터에 최대 하나의 인프라 SOFS 클러스터 역할 있을 수 있습니다. 인프라 SOFS 역할 지정 하 여 만들어집니다는 "**-인프라**" 매개 변수를 **추가 ClusterScaleOutFileServerRole** cmdlet 전환 합니다.  예를 들면 다음과 같습니다.

        Add-ClusterScaleoutFileServerRole -Name "my_infra_sofs_name" -Infrastructure

2.  장애 조치에서 자동으로 만든 각 CSV 볼륨 CSV 볼륨 이름을 기반으로 자동으로 생성 된 이름으로 SMB 공유 만들기를 트리거합니다. 직접 관리자 만들거나 CSV 볼륨 만들기/수정 작업을 통해 아닌 다른 SOFS 역할에서 SMB 공유를 수정할 수 없습니다.

3.  하이퍼 수렴 형 구성에서 인프라 SOFS SMB 클라이언트를 (Hyper-v 호스트)와 보장 된 지속적인 가용성 (CA) 인프라 SOFS SMB 서버에 통신할 수 있습니다. 이 하이퍼 수렴 형 SMB 루프백 CA는 가상 디스크 (VHDx) 파일과 소유 가상 컴퓨터 id 클라이언트와 서버 간에 전달 되는 위치에 액세스 하는 가상 컴퓨터를 통해 수행 됩니다. 이 identity 전달 하기 전에 표준 하이퍼 수렴 형 클러스터 구성으로 에서처럼 ACL 연산 VHDx 파일을 허용합니다.

클러스터 집합을 만든 후 클러스터 집합 네임 스페이스 멤버 클러스터의 각 부분에 인프라 SOFS 및 또한는 인프라 SOFS 관리 클러스터에 의존 합니다.

시간에 구성원 클러스터 관리자의 이름을 지정 합니다 인프라 SOFS 해당 클러스터에 이미 있는 경우 클러스터 집합에 추가 됩니다. 인프라 SOFS 존재 하지 않는 경우 새 인프라 SOFS 역할 멤버를 새 클러스터에서이 작업에 의해 만들어집니다. 인프라 SOFS 역할 멤버 클러스터에 이미 있는 경우 추가 작업 암시적으로 바꿉니다 지정된 된 이름에 필요에 따라 합니다. 모든 기존 의도 하지 않은 단일 SMB 서버 또는 클러스터 집합에 의해 unutilized 클러스터 남아 멤버에 비 인프라 SOFS 역할입니다. 

클러스터 세트를 만들 때에서 관리자 관리 클러스터에서 네임 스페이스 루트도 기존 광고 컴퓨터 개체를 사용 하는 옵션을 가집니다. 클러스터 집합 만들기 작업 관리 클러스터에서 SOFS 인프라 클러스터 역할 만들기 또는 바로 앞에서 설명한 대로 멤버 클러스터에 대 한 기존 인프라 SOFS 역할 이름을 바꿉니다. 인프라 SOFS 관리 클러스터에서 클러스터 네임 스페이스 조회 (클러스터 설정 Namespace) SOFS 설정에 사용 됩니다. 단순히 각 SMB 공유 클러스터에서 SOFS는이 미리 보기 버전에 새로 도입 된 형식 'SimpleReferral'--의 추천 공유 네임 스페이스 설정 하는 것입니다.  이 참조 SOFS 구성원 클러스터에 호스트 된 SMB 공유 대상에 대 한 SMB 클라이언트 액세스를 허용 합니다. 클러스터는 I/O 경로에 SOFS는 경량 조회 메커니즘 및 이와 같이 참여 하지 않는 네임 스페이스 참조를 설정 합니다. SMB 조회에서 각 클라이언트 노드의 그리며 캐시 된 및 클러스터 집합 네임 스페이스 동적으로 자동으로 이러한 추천 필요에 따라 업데이트

## 클러스터 집합 만들기

### 필수 조건

클러스터 생성 설정 된 경우 필수 구성 요소를 수행한 것이 좋습니다.

1. 최신 Windows Server 참가자 릴리스를 실행 하는 관리 클라이언트를 구성 합니다.
2. 이 관리 서버에 장애 조치 클러스터 도구를 설치 합니다.
3. 클러스터 구성원 (2 개 이상 있는 클러스터 두 개 이상의 클러스터 공유 볼륨 각 클러스터에서) 만들기
4. 구성원 클러스터를 배치 하는 관리 클러스터를 (실제 또는 게스트)를 만듭니다.  이 접근 방식은 클러스터 집합으로 관리 평면 계속 가능한 구성원 클러스터 오류 불구 하 고 사용할 수 있는지 확인 합니다.

### 단계

1. 필수 구성 요소에 정의 된 세 개의 클러스터에서 설정 하는 새 클러스터를 만듭니다.  아래 차트를 만드는 클러스터의 예를 제공 합니다.  이 예제에서 설정 하는 클러스터의 이름 **CSMASTER**됩니다.

   | 클러스터 이름               | 나중에 사용할 인프라 SOFS 이름 | 
   |----------------------------|-------------------------------------------|
   | 클러스터 집합                | SOFS CLUSTERSET                           |
   | CLUSTER1과                   | SOFS CLUSTER1과                             |
   | CLUSTER2                   | SOFS CLUSTER2                             |

2. 모든 클러스터를 만든 다음 명령을 사용 하 여 클러스터 집합 마스터를 만듭니다.

        New-ClusterSet -Name CSMASTER -NamespaceRoot SOFS-CLUSTERSET -CimSession SET-CLUSTER

3. 클러스터 서버 클러스터 세트를 추가 하는 다음 사용 됩니다.

        Add-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER1
        Add-ClusterSetMember -ClusterName CLUSTER2 -CimSession CSMASTER -InfraSOFSName SOFS-CLUSTER2

   > [!NOTE]
   > 정적 IP 주소 스키마를 사용 하는 경우 **새 ClusterSet** 명령에서 *-StaticAddress x.x.x.x* 포함 해야 합니다.

4. 클러스터 구성원에서 설정 클러스터를 만든 후 노드 집합 및 해당 속성을 나열할 수 있습니다.  클러스터 집합의 모든 구성원 클러스터를 열거 합니다.

        Get-ClusterSetMember -CimSession CSMASTER

5. 설정 관리 클러스터 노드를 포함 하 여 클러스터의 모든 구성원 클러스터 열거 합니다.

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterNode

6. 멤버 클러스터의 모든 노드 목록을 만듭니다.

        Get-ClusterSetNode -CimSession CSMASTER

7. 모든 목록을 표시 하려면 클러스터 전체 리소스 그룹 설정 합니다.

        Get-ClusterSet -CimSession CSMASTER | Get-Cluster | Get-ClusterGroup 

8. 클러스터를 확인 하려면 생성 프로세스 (Volume1 또는 어떤 CSV 폴더는 두 가지로 경로 및 파일 서버 인프라의 이름이 되 고 ScopeName로 레이블이 지정로 식별 됨) 하나 SMB 공유를 만든 인프라 SOFS에 각 클러스터 구성원에 대 한 설정 CSV 볼륨:

        Get-SmbShare -CimSession CSMASTER

8. 클러스터 집합에 디버그 로그를 검토 하기 위해 수집할 수 있습니다.  클러스터 설정 및 모두 모든 구성원 및 관리 클러스터에 대 한 클러스터 디버그 로그를 수집할 수 있습니다.

        Get-ClusterSetLog -ClusterSetCimSession CSMASTER -IncludeClusterLog -IncludeManagementClusterLog -DestinationFolderPath <path>

9. Kerberos [제한 위임](https://blogs.technet.microsoft.com/virtualization/2017/02/01/live-migration-via-constrained-delegation-with-kerberos-in-windows-server-2016/) 간의 모든 클러스터 세트 구성원을 구성 합니다.

10. 클러스터 집합의 각 노드에서 클러스터 간 가상 컴퓨터 실시간 마이그레이션은 인증 형식을 Kerberos 구성 합니다.

        foreach($h in $hosts){ Set-VMHost -VirtualMachineMigrationAuthenticationType Kerberos -ComputerName $h }

11. 클러스터 집합의 각 노드에서 로컬 관리자 그룹 관리 클러스터를 추가 합니다.

        foreach($h in $hosts){ Invoke-Command -ComputerName $h -ScriptBlock {Net localgroup administrators /add <management_cluster_name>$} }

## 새 가상 컴퓨터 만들기 및 클러스터 집합에 추가

집합 클러스터를 만든 후에 새 가상 컴퓨터를 만듭니다.  일반적으로 가상 컴퓨터를 만들고 클러스터에 추가 하는 데 시간이 이면 것에서 실행할 수 있는을 클러스터의 일부 검사를 수행 해야 합니다.  이러한 검사는 다음과 같습니다.

- 클러스터 노드에서 제공 되는 메모리 양을?
- 디스크 공간을 클러스터 노드에서 사용할 수 있나요?
- 가상 컴퓨터 (즉, SQL Server 가상 컴퓨터 빠른 드라이브; 실행 하는 클러스터로 이동 하 고 있고, 인프라 가상 컴퓨터 내 중요 하지 않은 느린 드라이브에서 실행할 수 있습니다) 특정 저장소 요구 사항 않아도 됩니다.

이 질문에 대답 후 필요한 되도록 클러스터에서 가상 컴퓨터를 만듭니다.  클러스터 집합의 장점 중 하나는 클러스터 집합을 해당 검사를 수행 하 고 최적의 노드에서 가상 컴퓨터를 배치 합니다.

아래 명령 둘 다 식별 최적의 클러스터 및 가상 컴퓨터에 배포 합니다.  에 아래 예에서는 새 가상 컴퓨터가 만들어집니다 지정 최소 4gb의 메모리 가상 컴퓨터에 제공 되며 1 가상 프로세서를 활용 해야 합니다.

- 4gb 가상 컴퓨터에 사용할 수 있는지 확인
- 1에서 사용 되는 가상 프로세서를 설정 합니다.
- 10% 이상 유지 하기 위해 검사 가상 컴퓨터에 사용할 수 있는 CPU

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

완료 되 면 가상 컴퓨터에 대 한 고 배치 된 정보를 제공 됩니다.  위의 예제에서는으로 표시 됩니다.

        State         : Running
        ComputerName  : 1-S2D2

충분 한 메모리, cpu, 또는 디스크 공간 가상 컴퓨터를 추가 하는 것을 오류를 받게 됩니다.

      Get-ClusterSetOptimalNodeForVM : A cluster node is not available for this operation.  

가상 컴퓨터를 만든 후 지정 된 특정 노드에서 Hyper-v 관리자에 표시 됩니다.  클러스터 가상 컴퓨터를 설정 하 고 명령 미만인 클러스터에 추가 합니다.  

        Register-ClusterSetVM -CimSession CSMASTER -MemberName $targetnode.Member -VMName CSVM1

완료 되 면 출력이 됩니다.

         Id  VMName  State  MemberName  PSComputerName
         --  ------  -----  ----------  --------------
          1  CSVM1      On  CLUSTER1    CSMASTER

기존 가상 컴퓨터를 사용 하 여 클러스터를 추가한 경우 가상 컴퓨터 집합 없으므로 모든 가상 컴퓨터의 한 번에 명령을 사용 하 여 등록 클러스터를 사용 하 여 등록할도 필요 합니다.

        Get-ClusterSetMember -name CLUSTER3 -CimSession CSMASTER | Register-ClusterSetVM -RegisterAll -CimSession CSMASTER

그러나 가상 컴퓨터에 대 한 경로 클러스터 집합 네임 스페이스에 추가 해야 하는 프로세스 완전 하지 않습니다.

예를 들어 기존 클러스터가 추가 되 고는 미리 구성 된 가상 컴퓨터는 reside에는 로컬 CSV 클러스터 공유 볼륨 ()는 VHDX에 대 한 경로 것과 비슷한 "C:\ClusterStorage\Volume1\MYVM\Virtual 하드 Disks\MYVM.vhdx 합니다.  저장소 마이그레이션 CSV 경로 단일 멤버 클러스터에 로컬 기본적으로 이러한 작업은 해야 합니다. 따라서 됩니다 가상 컴퓨터에 액세스할 수 있는 라이브 된 멤버 클러스터 간에 마이그레이션. 

이 예제에서는 CLUSTER3 인프라 스케일 아웃 파일 서버와 추가 ClusterSetMember를 사용 하 여 SOFS CLUSTER3로 설정 하 여 클러스터에 추가 되었습니다.  가상 컴퓨터 구성 및 저장소를 이동 하려면 올바른 명령은 다음과 같습니다.

        Move-VMStorage -DestinationStoragePath \\SOFS-CLUSTER3\Volume1 -Name MYVM

작업이 완료 되 면 경고를 받게 됩니다.

        WARNING: There were issues updating the virtual machine configuration that may prevent the virtual machine from running.  For more information view the report file below.
        WARNING: Report file location: C:\Windows\Cluster\Reports\Update-ClusterVirtualMachineConfiguration '' on date at time.htm.

경고는 "가상 컴퓨터 역할 저장소 구성에서 변경 검색 된" 대로이 경고를 무시할 수 있습니다.  실제 위치도 경고에 대 한 이유를 변경 하지 않습니다. 만 구성 경로입니다. 

이동 VMStorage에 대 한 자세한 내용은이 [링크](https://docs.microsoft.com/powershell/module/hyper-v/move-vmstorage?view=win10-ps)를 검토 하세요. 

라이브 다른 클러스터 집합 클러스터 간에 가상 컴퓨터를 마이그레이션하는 이전 버전과 마찬가지로 동일 합니다. 비 클러스터 집합 시나리오에서 단계는 다음과 같습니다.

1. 클러스터에서 가상 컴퓨터 역할을 제거 합니다.
2. 다른 클러스터의 구성원 노드로 가상 컴퓨터를 실시간 마이그레이션.
3. 새 가상 컴퓨터 역할을 클러스터에 가상 컴퓨터를 추가 합니다.

클러스터 집합을 사용 하 여 이러한 단계는 필요 하 고 하나의 명령 필요 합니다.  예를 들어 cluster1과에서 CLUSTER3 CL3 노드 2로 클러스터 집합 가상 컴퓨터를 이동 하려고 합니다.  단일 명령은 다음과 같습니다.

        Move-ClusterSetVM -CimSession CSMASTER -VMName CSVM1 -Node NODE2-CL3

가상 컴퓨터 저장소 또는 구성 파일 움직이지 않는이 note 하세요.  이 가상 컴퓨터에 대 한 경로 \\SOFS-CLUSTER1\VOLUME1으로 유지 되므로 필요 하지 않습니다.  가상 컴퓨터에 등록 된 후 클러스터 집합으로 인프라 파일 서버 공유 경로, 드라이브 및 가상 컴퓨터 필요 하지 않은 가상 컴퓨터와 동일한 컴퓨터에 연결 됩니다.

## 오류 도메인 설정 가용성 만들기

도입, 설명 된 대로 Azure와 유사한 오류 도메인 및 가용성 집합 클러스터 집합에서 구성할 수 있습니다.  초기 가상 컴퓨터 배치 및 클러스터 간에 마이그레이션을 유용합니다.  

아래 예제에서는 4 개의 클러스터를 클러스터 집합에 참여 하 고 있습니다.  세트 내 논리적 장애 도메인 장애 도메인과 다른 두 개의 클러스터를 사용 하 여 만든 클러스터의 2 개를 사용 하 여 생성 됩니다.  이러한 두 개의 오류 도메인 Availabiilty 집합을 구성 합니다. 

아래 예제에서는 cluster1과 및 CLUSTER2 CLUSTER3 및 CLUSTER4 **FD2**라는 장애 도메인에 있어야 하는 동안 **FD1** 이라고 하는 오류 도메인에서 됩니다.  가용성 설정 호출 될 **CSMASTER-AS** 및 두 개의 오류 도메인 구성 됩니다.

장애 도메인을 만들려면 명령은 다음과 같습니다.

        New-ClusterSetFaultDomain -Name FD1 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER1,CLUSTER2 -Description "This is my first fault domain"

        New-ClusterSetFaultDomain -Name FD2 -FdType Logical -CimSession CSMASTER -MemberCluster CLUSTER3,CLUSTER4 -Description "This is my second fault domain"

성공적으로 생성 된 위해, Get ClusterSetFaultDomain 표시 된 출력으로 실행할 수 있습니다.

        PS C:\> Get-ClusterSetFaultDomain -CimSession CSMASTER -FdName FD1 | fl *

        PSShowComputerName    : True
        FaultDomainType       : Logical
        ClusterName           : {CLUSTER1, CLUSTER2}
        Description           : This is my first fault domain
        FDName                : FD1
        Id                    : 1
        PSComputerName        : CSMASTER

오류 도메인 만들었으니, 이제는 가용성 요구를 만들 수를 설정 합니다.

        New-ClusterSetAvailabilitySet -Name CSMASTER-AS -FdType Logical -CimSession CSMASTER -ParticipantName FD1,FD2

확인할 수를 만든 다음 사용:

        Get-ClusterSetAvailabilitySet -AvailabilitySetName CSMASTER-AS -CimSession CSMASTER

새 가상 컴퓨터를 만들 때 최적의 노드 확인의 일환으로-AvailabilitySet 매개 변수를 사용 해야 합니다.  따라서 다음과 같이 표시 다음 합니다.

        # Identify the optimal node to create a new virtual machine
        $memoryinMB=4096
        $vpcount = 1
        $av = Get-ClusterSetAvailabilitySet -Name CSMASTER-AS -CimSession CSMASTER
        $targetnode = Get-ClusterSetOptimalNodeForVM -CimSession CSMASTER -VMMemory $memoryinMB -VMVirtualCoreCount $vpcount -VMCpuReservation 10 -AvailabilitySet $av
        $secure_string_pwd = convertto-securestring "<password>" -asplaintext -force
        $cred = new-object -typename System.Management.Automation.PSCredential ("<domain\account>",$secure_string_pwd)

다양 한 주기 때문에 설정 클러스터에서 클러스터를 제거 합니다. 클러스터를 클러스터 집합에서 제거 해야 하는 경우 경우가 있습니다. 모범 사례로 클러스터에서 모든 클러스터 집합 가상 컴퓨터를 이동 해야 합니다. **이동 ClusterSetVM** 및 **이동 VMStorage** 명령을 사용 하 여 수행할 수 있습니다.

하지만 가상 컴퓨터도 이동 하지 것입니다, 클러스터 집합은 일련의 관리자에 게 직관적이 결과 제공 하는 작업을 실행 합니다.  클러스터 집합에서 제거 되 면 모든 나머지 클러스터 집합 호스팅되는 가상 컴퓨터 제거 되는 클러스터에서 해당 저장소에 액세스할 수 있으며 가정 하 고 해당 클러스터에 바인딩된 항상 사용 가능한 가상 컴퓨터를 간단 하 게 될 것입니다.  클러스터 집합 하 여 인벤토리에 자동으로 업데이트 합니다.

- 더 이상 지금 제거 클러스터 및 여기에서 실행 중인 가상 컴퓨터의 상태를 추적
- 클러스터 집합 네임 스페이스 및 공유 지금 제거 클러스터에 호스트에 대 한 모든 참조에서 제거

예를 들어 클러스터 집합에서 cluster1과 클러스터를 제거 하는 명령은 다음과 같습니다.

        Remove-ClusterSetMember -ClusterName CLUSTER1 -CimSession CSMASTER

## 질문과 대답(FAQ)

**질문:** 클러스터 세트 내에서 ' m I 사용 하도록 제한만 하이퍼 수렴 형 클러스터? <br>
**응답:** 아니요.  저장소 공간 다이렉트 기존의 클러스터와 함께 사용할 수 있습니다.

**질문:** 내 클러스터 집합 System Center 가상 컴퓨터 관리자를 통해 관리할 수 있습니까? <br>
**응답:** System Center 가상 컴퓨터 Manager 현재 클러스터 집합을 지원 하지 않으므로 <br><br> **질문:** 공존할 수 있는 Windows Server 2012 R2 또는 2016 클러스터 동일한 클러스터 집합에? <br>
**질문:** Windows Server 2012 R2 off 워크 로드로 마이그레이션 또는 클러스터를 간단 하 게 함으로써 2016 클러스터 가입 동일한 클러스터 집합? <br>
**응답:** 클러스터 집합은 새로운 기술 Windows Server 미리 보기에 도입 되 빌드, 따라서 이와 같이 존재 하지 않는 이전 릴리스에서 합니다. 하위 수준 OS 기반 클러스터는 클러스터 집합에 가입할 수 없습니다. 그러나 클러스터 운영 체제 롤링 업그레이드 기술을 이러한 클러스터 Windows Server 2019로 업그레이드 하 여 원하는 마이그레이션 기능을 제공 해야 합니다.

**질문:** 클러스터 집합 저장소의 크기를 조정 하거나 (단독) 계산을 허용할 수 있나요? <br>
**응답:** 예, 저장소 공간 다이렉트 또는 기존의 Hyper-v 클러스터를 추가 하기만 하면 됩니다. 클러스터 집합, 즉 하이퍼 수렴 형 클러스터 집합에도 저장소로 계산 비율의 간단한 변경 됩니다.

**질문:** 클러스터 집합에 대 한 관리 도구를 사용한 란 무엇 인가요 <br>
**응답:** PowerShell 또는 WMI이 릴리스에서 합니다.

**질문:** 다른 세대 프로세서를 사용 하 여 클러스터 간 실시간 마이그레이션을 작동 하는 방법을  <br>
**응답:** 클러스터 집합 프로세서 차이 해결 및 대체 Hyper-v 현재 지원 되지 않습니다.  따라서 빠른 마이그레이션 함께 프로세서 호환 모드를 사용 해야 합니다.  클러스터 집합에 대 한 권장 되려면 클러스터 간에 실시간 마이그레이션에 대 한 전체 클러스터 설정 뿐만 아니라 각 개별 클러스터 내에서 동일한 프로세서 하드웨어를 사용 하는 것입니다.

**질문:** 수 내 클러스터 세트 가상 컴퓨터 자동으로 장애 조치 클러스터 실패 시?  <br>
**응답:** 이 릴리스에서 클러스터 집합 가상 컴퓨터 될 수 있습니다 수동으로 실시간 마이그레이션; 클러스터 간에 하지만 자동 장애 조치 수 없습니다. 

**질문:** 저장소 클러스터 오류에 복원 됩니다 보장 하는 방법을 우리? <br>
**응답:** 클러스터 오류로 저장소 복원 력 실현 하는 데 구성원 클러스터에서 클러스터 간 저장소 복제본 (SR) 솔루션을 사용 합니다.

**질문:** 저장소 복제본 (SR) 멤버 클러스터 간에 복제를 사용 합니다. 작업을 수행 클러스터 집합 네임 스페이스 저장소 UNC 경로 변경에 SR 장애 조치를 복제본 대상 저장소 공간 다이렉트 클러스터? <br>
**응답:** 이 릴리스에서 이러한 클러스터 집합 네임 스페이스 조회 변경 SR 장애 발생 하지 않습니다. 이 시나리오는 및 사용할 계획에 중요 한 경우 Microsoft 알려 주시기 바랍니다.

**질문:** 장애 도메인 재해 복구 상황에서 장애 조치 가상 컴퓨터 수는 (예: 전체 장애 도메인 다운)? <br>
**응답:** 아니요, 클러스터 간 장애 유의 논리적 오류 내에서 도메인 아직 지원 되지 않습니다. 

**질문:** 내 클러스터에 여러 사이트 (또는 DNS 도메인) 범위 클러스터를 설정할 수 있나요? <br> 
**응답:** 이 방법은 및 즉시 프로덕션 지원에 대 한 계획 합니다. 이 시나리오는 및 사용할 계획에 중요 한 경우 Microsoft 알려 주시기 바랍니다.

**질문:** 클러스터는 i p v 6 사용 하 여 작업을 설정? <br>
**응답:** IPv4 및 IPv6 장애 조치 클러스터와 마찬가지로 클러스터 집합으로 지원 됩니다.

**질문:** 클러스터에 대 한 Active Directory 포리스트 요구 사항은 무엇입니까 설정 <br>
**응답:** 모든 구성원 클러스터 동일한 AD 포리스트에 있어야 합니다.

**질문:** 얼마나 많은 클러스터 또는 노드는 단일 클러스터의 일부가 설정할 수 있나요? <br>
**응답:** 클러스터 집합 미리 보기에서 테스트를 거쳐 최대 64 개의 전체 클러스터 노드를 지원 합니다. 그러나 클러스터 아키텍처 크기가 조정 됨을 훨씬 더 큰 제한 설정 하며 제한에 대 한 하드 코드 된 것 아닙니다. 큰 규모 중요 하 고 사용할 계획 어떻게 되는지 알 Microsoft 알려 주시기 바랍니다.

**질문:** 클러스터 집합의 모든 저장소 공간 다이렉트 클러스터 형성 단일 저장소 풀? <br>
**응답:** 아니요. 저장소 공간 다이렉트 기술 단일 클러스터 내에서 그리고 클러스터 집합의 멤버 클러스터 전체에서 아니라 작동 합니다.

**질문:** 클러스터에 네임 스페이스 항상 사용 가능한 설정 되어 있습니까? <br>
**응답:** 예, 클러스터 집합 네임 스페이스 관리 클러스터에서 실행 되는 지속적으로 사용할 수 있는 ca (인증) 조회 SOFS 네임 스페이스 서버를 통해 제공 됩니다. 지역화 된 클러스터 전체의 풍부한 오류를 복원 해야 구성원 클러스터에서 가상 컴퓨터의 충분 한 수 있는 것이 좋습니다. 하지만 예기치 않은 오류가 발생-예: 모든 가상 컴퓨터 관리 클러스터 동시에 다운 될 – 담당 하 참조 정보는 또한 영구적으로 캐시 각 클러스터 집합 노드에 재부팅 에서도 합니다.
 
**질문:** 클러스터는 클러스터 집합의 저장소 성능을 느리게 네임 스페이스 기반 저장소 액세스 설정? <br>
**응답:** 아니요. 클러스터 집합 네임 스페이스 내 클러스터 집합 – 개념적 같은 분산 파일 시스템 네임 스페이스 (DFSN)는 오버레이 조회 네임 스페이스를 제공합니다. 및 DFSN와 달리 모든 클러스터 집합 네임 스페이스 추천 메타 데이터는 모든 노드에서 관리자 개입 없이 자동으로 업데이트 하 고 자동으로 채워집니다 저장소 액세스 경로에서 거의 없으며 성능 오버 헤드가 않도록 합니다. 

**질문:** 클러스터 집합 메타 데이터를 백업 하는 방법 <br>
**응답:** 이 가이드는 장애 조치 클러스터와 같습니다. 시스템 상태 백업도 클러스터 상태를 백업 됩니다.  Windows Server 백업 통해 복원 방금 노드의 클러스터 데이터베이스의 (해야 이상 필요 하지는 자동 복구 논리의 여러 때문) 할 수 있는 또는 전체 클러스터 데이터베이스에 대 한 모든 노드에서 롤백 정식 복원을 수행 합니다. 클러스터 집합의 경우 필요한 경우 멤버 클러스터 및 클러스터 관리에 먼저 이러한 정식 복원을 수행 하는 것이 좋습니다. 
