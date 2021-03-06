---
title: 장애 조치(Failover) 클러스터에서 쿼럼 구성 및 관리
description: Windows Server 장애 조치 (failover) 클러스터에서 클러스터 쿼럼을 관리 하는 방법에 대 한 자세한 정보입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
manager: lizross
ms.technology: storage-failover-clustering
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 67ef309bc2a09c5e241d52c747ab800cfde86168
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720527"
---
# <a name="configure-and-manage-quorum"></a>쿼럼 구성 및 관리

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

이 항목에서는 Windows Server 장애 조치 (failover) 클러스터에서 쿼럼을 구성 하 고 관리 하는 배경 및 단계를 제공 합니다.

## <a name="understanding-quorum"></a>쿼럼 이해

클러스터의 쿼럼은 해당 클러스터가 올바르게 시작되거나 지속적으로 실행되기 위해 활성 클러스터 구성원의 일부여야 하는 응답 요소 수에 따라 결정됩니다. 자세한 설명은 [클러스터 및 풀 쿼럼 이해 문서](../storage/storage-spaces/understand-quorum.md)를 참조 하세요.

## <a name="quorum-configuration-options"></a>쿼럼 구성 옵션

Windows Server의 쿼럼 모델은 유연 합니다. 클러스터에 대 한 쿼럼 구성을 수정 해야 하는 경우 클러스터 쿼럼 구성 마법사 또는 장애 조치 (Failover) 클러스터 Windows PowerShell cmdlet을 사용할 수 있습니다. 쿼럼 구성 단계 및 고려 사항은 이 항목의 뒷부분에 있는 [클러스터 쿼럼 구성](#configure-the-cluster-quorum)을 참조하세요.

다음 표에는 클러스터 쿼럼 구성 마법사에서 사용할 수 있는 세 가지 쿼럼 구성 옵션이 나와 있습니다.

| 옵션  |설명  |
| --------- | ---------|
| 일반 설정 사용     |  클러스터에서 각 노드에 응답을 자동으로 할당하고 노드 응답을 동적으로 관리합니다. 클러스터에 적합하고 사용 가능한 클러스터 공유 스토리지가 있는 경우 클러스터에서 디스크 감시를 선택합니다. 클러스터에 대해 가장 높은 가용성을 제공하는 쿼럼 및 감시 구성을 클러스터 소프트웨어에서 자동으로 선택하므로 대부분의 경우 이 옵션을 사용하는 것이 좋습니다.       |
| 쿼럼 감시를 추가 또는 변경     |   감시 리소스를 추가, 변경 또는 제거할 수 있습니다. 파일 공유 또는 디스크 감시를 구성할 수 있습니다. 클러스터에서 각 노드에 응답을 자동으로 할당하고 노드 응답을 동적으로 관리합니다.      |
| 고급 쿼럼 구성 및 감시 선택     | 쿼럼 구성을 위한 애플리케이션 관련 또는 사이트 관련 요구 사항이 있는 경우에만 이 옵션을 선택해야 합니다. 쿼럼 감시를 수정하고, 노드 응답을 추가 또는 제거하고, 클러스터에서 노드 응답을 동적으로 관리할지 여부를 선택할 수 있습니다. 기본적으로 응답은 모든 노드에 할당되며, 노드 응답은 동적으로 관리됩니다.        |

선택한 쿼럼 구성 옵션 및 특정 설정에 따라 다음 쿼럼 모드 중 하나로 클러스터가 구성됩니다.

| Mode  | 설명  |
| --------- | ---------|
| 노드 과반수(감시 없음)     |   노드에만 응답이 있으며, 쿼럼 감시는 구성되지 않습니다. 클러스터 쿼럼은 활성 클러스터 구성원의 과반수 응답 노드입니다.      |
| 감시 있는 노드 과반수(디스크 또는 파일 공유)     |   노드에 응답이 있으며, 쿼럼 감시에도 응답이 있습니다. 클러스터 쿼럼은 활성 클러스터 구성원의 과반수 응답 노드와 감시 응답으로 구성됩니다. 쿼럼 감시는 지정된 디스크 감시 또는 지정된 파일 공유 감시일 수 있습니다. 
| 과반수 없음(디스크 감시에만 해당)     | 노드에 응답이 없으며, 디스크 감시에만 응답이 있습니다. <br>클러스터 쿼럼은 디스크 감시 상태에 따라 결정됩니다. 일반적으로 이 모드는 권장되지 않으며, 클러스터에 대한 단일 실패 지점을 만들므로 선택해서는 안 됩니다.       |

다음 하위 섹션에서는 고급 쿼럼 구성 설정에 대 한 자세한 정보를 제공 합니다.

### <a name="witness-configuration"></a>감시 구성

일반적으로 쿼럼을 구성할 때 클러스터의 응답 요소는 홀수여야 합니다. 따라서 클러스터에 짝수 개의 응답 노드가 포함된 경우 디스크 감시 또는 파일 공유 감시를 구성해야 합니다. 클러스터는 아래쪽에 추가 노드 하나를 유지할 수 있습니다. 또한 감시 응답을 추가하면 클러스터 노드 절반이 작동 중지되거나 연결이 끊어진 경우 클러스터가 계속 실행될 수 있습니다.

디스크 감시는 일반적으로 모든 노드에서 디스크를 볼 수 있는 경우에 권장됩니다. 파일 공유 감시는 복제된 스토리지를 사용하여 다중 사이트 재해 복구를 수행해야 하는 경우에 권장됩니다. 복제된 스토리지로 디스크 감시를 구성하는 것은 스토리지 공급업체가 모든 사이트에서 복제된 스토리지에 읽기/쓰기 액세스할 수 있도록 지원하는 경우에만 가능합니다. <strong>*디스크 감시는 스토리지 공간 다이렉트 지원 되지 않습니다*</strong>.

다음 표에는 쿼럼 감시 유형에 대한 추가 정보 및 고려 사항이 나와 있습니다.

| 감시 유형  | 설명  | 요구 사항 및 권장 사항  |
| ---------    |---------        |---------                        |
| 디스크 감시     |  <ul><li> 클러스터 데이터베이스의 복사본을 저장하는 전용 LUN</li><li> 복제되지 않은 공유 스토리지를 사용하는 클러스터에 가장 유용함</li>       |  <ul><li>LUN 크기는 최소 512MB여야 함</li><li> 클러스터에만 사용되고 클러스터된 역할에 할당되지 않아야 함</li><li> 클러스터된 스토리지에 포함되고 스토리지 유효성 검사 테스트를 통과해야 함</li><li> CSV(클러스터 공유 볼륨)인 디스크일 수 없음</li><li> 단일 볼륨이 있는 기본 디스크</li><li> 드라이브 문자가 필요 없음</li><li> NTFS 또는 ReFS로 포맷할 수 있음</li><li> 필요한 경우 내결함성을 위해 하드웨어 RAID로 구성할 수 있음</li><li> 백업 및 바이러스 백신 검사에서 제외해야 함</li><li> 디스크 감시는 스토리지 공간 다이렉트 지원 되지 않습니다.</li>|
| 파일 공유 감시     | <ul><li>Windows Server를 실행하는 파일 서버에 구성되는 SMB 파일 공유</li><li> 클러스터 데이터베이스의 복사본을 저장하지 않음</li><li> witness.log 파일에만 클러스터 정보를 유지 관리함</li><li> 복제된 스토리지를 사용하는 다중 사이트 클러스터에 가장 유용함 </li>       |  <ul><li>최소 5MB의 사용 가능한 공간이 있어야 함</li><li> 단일 클러스터에만 사용해야 하며, 사용자 또는 애플리케이션 데이터를 저장할 수 없음</li><li> 컴퓨터 개체에 클러스터 이름에 대한 쓰기 권한이 있어야 함</li></ul><br>파일 공유 감시를 호스트하는 파일 서버에 대한 추가 고려 사항:<ul><li>여러 클러스터에 대한 파일 공유 감시로 단일 파일 서버를 구성할 수 있습니다.</li><li> 파일 서버는 클러스터 작업과 별도의 사이트에 있어야 합니다. 이렇게 하면 사이트 간 네트워크 통신이 끊어진 경우 모든 클러스터 사이트에 동등한 존속 기회가 제공됩니다. 파일 서버가 동일한 사이트에 있는 경우 해당 사이트가 기본 사이트가 되며 이 사이트에서만 파일 공유에 연결할 수 있습니다.</li><li> 가상 컴퓨터가 파일 공유 감시를 사용하는 동일한 클러스터에서 호스트되지 않는 경우 가상 컴퓨터에서 파일 서버를 실행할 수 있습니다.</li><li> 고가용성을 위해 별도의 장애 조치(failover) 클러스터에서 파일 서버를 구성할 수 있습니다. </li>      |
| 클라우드 감시     |  <ul><li>Azure blob storage에 저장 된 미러링 모니터 파일</li><li> 클러스터의 모든 서버에 안정적인 인터넷 연결이 있는 경우에 권장 됩니다.</li>      |  [클라우드 감시 배포를](https://docs.microsoft.com/windows-server/failover-clustering/deploy-cloud-witness)참조 하세요.       |

### <a name="node-vote-assignment"></a>노드 응답 할당

고급 쿼럼 구성 옵션인 노드 단위로 쿼럼 응답을 할당 하거나 제거 하도록 선택할 수 있습니다. 기본적으로 모든 노드에 응답이 할당됩니다. 응답 할당에 상관없이 모든 노드는 클러스터에서 지속적으로 작동하며, 클러스터 데이터베이스 업데이트를 받고, 애플리케이션을 호스트할 수 있습니다.

특정 재해 복구 구성의 경우 노드에서 응답을 제거할 수도 있습니다. 예를 들어 다중 사이트 클러스터의 경우 백업 사이트의 노드가 쿼럼 계산에 영향을 주지 않도록 이러한 노드에서 응답을 제거할 수 있습니다. 이 구성은 사이트 간의 수동 장애 조치(failover)에만 권장됩니다. 자세한 내용은 이 항목의 뒷부분에 있는 [재해 복구 구성에 대한 쿼럼 고려 사항](#quorum-considerations-for-disaster-recovery-configurations)을 참조하세요.

[Start-clusternode](https://technet.microsoft.com/library/hh847268.aspx)Windows PowerShell cmdlet을 사용 하 여 클러스터 노드의 **nodeweight** 공용 속성을 조회 하 여 노드의 구성 된 투표를 확인할 수 있습니다. 0 값은 노드에 구성된 쿼럼 응답이 없음을 나타내며, 1 값은 노드의 쿼럼 응답이 할당되고 클러스터에서 관리됨을 나타냅니다. 노드 응답 관리에 대한 자세한 내용은 이 항목의 뒷부분에 있는 [동적 쿼럼 관리](#dynamic-quorum-management)를 참조하세요.

**클러스터 쿼럼 유효성 검사** 유효성 테스트를 사용하여 모든 클러스터 노드에 대한 응답 할당을 확인할 수 있습니다.

#### <a name="additional-considerations-for-node-vote-assignment"></a>노드 응답 할당에 대 한 추가 고려 사항

  - 노드 응답 할당은 홀수 개의 응답 노드를 적용하는 데 권장되지 않습니다. 대신 디스크 감시 또는 파일 공유 감시를 구성해야 합니다. 자세한 내용은이 항목의 뒷부분에 있는 [감시 구성](#witness-configuration) 을 참조 하세요.
  - 동적 쿼럼 관리를 사용하는 경우 노드 응답이 할당되도록 구성된 노드에서만 동적으로 응답을 할당하거나 제거할 수 있습니다. 자세한 내용은 이 항목의 뒷부분에 있는 [동적 쿼럼 관리](#dynamic-quorum-management)를 참조하세요.

### <a name="dynamic-quorum-management"></a>동적 쿼럼 관리

Windows Server 2012에서는 고급 쿼럼 구성 옵션으로 클러스터 별로 동적 쿼럼 관리를 사용 하도록 선택할 수 있습니다. 동적 쿼럼의 작동 방식에 대 한 자세한 내용은 [이 설명](../storage/storage-spaces/understand-quorum.md#dynamic-quorum-behavior)을 참조 하세요.

또한 동적 쿼럼 관리를 사용하면 마지막으로 남아 있는 노드에서 클러스터를 실행할 수 있습니다. 쿼럼 과반수 요구 사항을 동적으로 조정함으로써 클러스터는 단일 노드로 순차적인 노드 종료를 유지할 수 있습니다.

클러스터에서 할당 된 노드의 동적 응답은 [Start-clusternode](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusternode?view=win10-ps) Windows PowerShell cmdlet을 사용 하 여 클러스터 노드의 **dynamicweight** 공용 속성을 사용 하 여 확인할 수 있습니다. 0 값은 노드에 쿼럼 응답이 없음을 나타내며, 1 값은 노드에 쿼럼 응답이 있음을 나타냅니다.

**클러스터 쿼럼 유효성 검사** 유효성 테스트를 사용하여 모든 클러스터 노드에 대한 응답 할당을 확인할 수 있습니다.

#### <a name="additional-considerations-for-dynamic-quorum-management"></a>동적 쿼럼 관리를 위한 추가 고려 사항

- 동적 쿼럼 관리를 사용하면 클러스터에서 과반수 응답 구성원의 동시 실패를 유지할 수 없습니다. 실행을 계속하려면 노드 종료 또는 실패 시 클러스터에 항상 쿼럼 과반수가 있어야 합니다.

- 노드의 응답을 명시적으로 제거한 경우 클러스터는 동적으로 응답을 추가하거나 제거할 수 없습니다.
- 스토리지 공간 다이렉트 사용 하도록 설정 된 경우 클러스터는 두 개의 노드 오류만 지원할 수 있습니다. 이에 대해서는 [풀 쿼럼 섹션](../storage/storage-spaces/understand-quorum.md) 에서 자세히 설명 합니다.

## <a name="general-recommendations-for-quorum-configuration"></a>쿼럼 구성에 대한 일반 권장 사항

클러스터 소프트웨어는 구성된 노드 수 및 공유 스토리지의 가용성을 기반으로 새 클러스터에 대한 쿼럼을 자동으로 구성합니다. 일반적으로 이 구성이 해당 클러스터에 가장 적합한 쿼럼 구성입니다. 그러나 클러스터가 만들어진 후 해당 클러스터를 프로덕션 환경에 배치하기 전에 쿼럼 구성을 검토하는 것이 좋습니다. 자세한 클러스터 쿼럼 구성을 보려면 구성 유효성 검사 마법사 또는 [테스트 클러스터](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps) Windows PowerShell cmdlet을 사용 하 여 **쿼럼 구성 유효성 검사** 테스트를 실행할 수 있습니다. 장애 조치(Failover) 클러스터 관리자에서 선택한 클러스터에 대 한 요약 정보에 기본 쿼럼 구성이 표시 됩니다. [또는 Windows PowerShell cmdlet을 실행할](https://docs.microsoft.com/powershell/module/failoverclusters/get-clusterquorum?view=win10-ps) 때 반환 되는 쿼럼 리소스에 대 한 정보를 검토할 수 있습니다.

언제든지 **쿼럼 구성 유효성 검사** 테스트를 실행하여 쿼럼 구성이 클러스터에 가장 적합한 구성인지 확인할 수 있습니다. 테스트 출력에는 쿼럼 구성 변경이 권장되는지 여부와 최적의 설정이 표시됩니다. 변경이 권장되는 경우 클러스터 쿼럼 구성 마법사를 사용하여 권장 설정을 사용할 수 있습니다.

클러스터를 프로덕션 환경에 배치한 후에는 변경 내용이 클러스터에 적절하다고 확인한 경우가 아니면 쿼럼 구성을 변경하지 마세요. 다음과 같은 경우에 쿼럼 구성 변경을 고려할 수 있습니다.

- 노드 추가 또는 제거
- 스토리지 추가 또는 제거
- 장기적인 노드 또는 감시 실패
- 다중 사이트 재해 복구 시나리오에서 클러스터 복구

하드웨어 유효성 검사 테스트에 대한 자세한 내용은 [장애 조치(failover) 클러스터에 대한 하드웨어 유효성 검사](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>)를 참조하세요.

## <a name="configure-the-cluster-quorum"></a>클러스터 쿼럼 구성

장애 조치(Failover) 클러스터 관리자 또는 장애 조치 (Failover) 클러스터 Windows PowerShell cmdlet을 사용 하 여 클러스터 쿼럼 설정을 구성할 수 있습니다.

> [!IMPORTANT]
> 일반적으로 클러스터 쿼럼 구성 마법사에서 권장하는 쿼럼 구성을 사용하는 것이 좋습니다. 변경 내용이 클러스터에 적절하다고 확인한 경우에만 쿼럼 구성을 사용자 지정하는 것이 좋습니다. 자세한 내용은 이 항목에서 [쿼럼 구성에 대한 일반 권장 사항](#general-recommendations-for-quorum-configuration)을 참조하세요.

### <a name="configure-the-cluster-quorum-settings"></a>클러스터 쿼럼 설정 구성

이 절차를 완료하려면 최소한 각 클러스터된 서버에서 로컬 **Administrators** 그룹의 구성원이거나 이와 동등한 권한이 있어야 합니다. 또한 사용하는 계정이 도메인 사용자 계정이어야 합니다.

> [!NOTE]
> 클러스터를 중지하거나 클러스터 리소스를 오프라인으로 상태로 전환하지 않고 클러스터 쿼럼 구성을 변경할 수 있습니다.

### <a name="change-the-quorum-configuration-in-a-failover-cluster-by-using-failover-cluster-manager"></a>장애 조치(Failover) 클러스터 관리자를 사용 하 여 장애 조치 (failover) 클러스터의 쿼럼 구성 변경

1. 장애 조치(failover) 클러스터 관리자에서 변경할 클러스터를 선택하거나 지정합니다.
2. 클러스터를 선택한 상태에서 **작업**아래에서 **기타 작업**을 선택 하 고 **클러스터 쿼럼 설정 구성**을 선택 합니다. 클러스터 쿼럼 구성 마법사가 나타납니다. **다음**을 선택합니다.
3. **쿼럼 구성 옵션 선택** 페이지에서 세 가지 구성 옵션 중 하나를 선택하고 해당 옵션에 대한 단계를 완료합니다. 쿼럼 설정을 구성하기 전에 선택 항목을 검토할 수 있습니다. 옵션에 대 한 자세한 내용은이 항목의 앞부분에 있는 [쿼럼 이해](#understanding-quorum)를 참조 하십시오.

    - 클러스터에서 현재 클러스터 구성에 가장 적합 한 쿼럼 설정을 자동으로 다시 설정할 수 있도록 하려면 **일반 설정 사용** 을 선택한 다음 마법사를 완료 합니다.
    - 쿼럼 감시를 추가 하거나 변경 하려면 **쿼럼 감시 추가 또는 변경**을 선택 하 고 다음 단계를 완료 합니다. 쿼럼 감시 구성에 대한 자세한 내용 및 고려 사항은 이 항목의 앞부분에 있는 [감시 구성](#witness-configuration)을 참조하세요.

      1. **쿼럼 감시 선택** 페이지에서 디스크 감시 또는 파일 공유 감시를 구성하는 옵션을 선택합니다. 클러스터에 권장되는 감시 선택 옵션이 마법사에 표시됩니다.

          > [!NOTE]
          > **쿼럼 감시 구성 안 함**을 선택하고 마법사를 완료할 수도 있습니다. 클러스터에 짝수 개의 응답 노드가 있는 경우 이 구성은 권장되는 구성이 아닐 수 있습니다.

      2. 디스크 감시를 구성하는 옵션을 선택한 경우 **스토리지 감시 구성** 페이지에서 디스크 감시로 할당할 스토리지 볼륨을 선택하고 마법사를 완료합니다.
      3. 파일 공유 감시를 구성하는 옵션을 선택한 경우 **파일 공유 감시 구성** 페이지에서 감시 리소스로 사용할 파일 공유를 입력하거나 찾은 다음 마법사를 완료합니다.

    - 쿼럼 관리 설정을 구성 하 고 쿼럼 감시를 추가 하거나 변경 하려면 **고급 쿼럼 구성 및 감시 선택**을 선택 하 고 다음 단계를 완료 합니다. 고급 쿼럼 구성 설정에 대한 자세한 내용 및 고려 사항은 이 항목의 앞부분에 있는 [노드 응답 할당](#node-vote-assignment) 및 [동적 쿼럼 관리](#dynamic-quorum-management)를 참조하세요.

      1. **응답 구성 선택** 페이지에서 노드에 응답을 할당하는 옵션을 선택합니다. 기본적으로 모든 노드에 응답이 할당됩니다. 그러나 특정 시나리오의 경우 노드 하위 집합에만 응답을 할당할 수 있습니다.

          > [!NOTE]
          > **노드 없음**을 선택할 수도 있습니다. 이 옵션을 선택하면 노드가 쿼럼 응답에 참여할 수 없으며 디스크 감시를 구성해야 하므로 일반적으로 권장되지 않습니다. 이 디스크 감시는 클러스터의 단일 실패 지점이 됩니다.

      2. **쿼럼 관리 구성** 페이지에서 **클러스터에서 노드 응답 할당을 동적으로 관리하도록 허용** 옵션을 선택하거나 선택 취소할 수 있습니다. 이 옵션을 선택하면 일반적으로 클러스터의 가용성이 향상됩니다. 이 옵션은 기본적으로 선택되며, 선택을 취소하지 않는 것이 좋습니다. 이 옵션을 사용하면 이 옵션을 사용하지 않을 경우 가능하지 않은 실패 시나리오에서 클러스터를 계속 실행할 수 있습니다.
      3. **쿼럼 감시 선택** 페이지에서 디스크 감시 또는 파일 공유 감시를 구성하는 옵션을 선택합니다. 클러스터에 권장되는 감시 선택 옵션이 마법사에 표시됩니다.

          > [!NOTE]
          > **쿼럼 감시 구성 안 함**을 선택하고 마법사를 완료할 수도 있습니다. 클러스터에 짝수 개의 응답 노드가 있는 경우 이 구성은 권장되는 구성이 아닐 수 있습니다.

      4. 디스크 감시를 구성하는 옵션을 선택한 경우 **스토리지 감시 구성** 페이지에서 디스크 감시로 할당할 스토리지 볼륨을 선택하고 마법사를 완료합니다.
      5. 파일 공유 감시를 구성하는 옵션을 선택한 경우 **파일 공유 감시 구성** 페이지에서 감시 리소스로 사용할 파일 공유를 입력하거나 찾은 다음 마법사를 완료합니다.

4. **다음**을 선택합니다. 표시 되는 확인 페이지에서 선택 항목을 확인 하 고 **다음**을 선택 합니다.

마법사를 실행 하 고 **요약** 페이지가 표시 된 후 마법사에서 수행한 작업에 대 한 보고서를 보려면 **보고서 보기**를 선택 합니다. 가장 최근 보고서는 이름이 **quorumconfiguration.mht 라는**인 <em>systemroot</em>**\\Cluster\\Reports** 폴더에 유지 됩니다.

> [!NOTE]
> 클러스터 쿼럼을 구성한 후에는 **쿼럼 구성 유효성 검사** 테스트를 실행하여 업데이트된 쿼럼 설정을 확인하는 것이 좋습니다.

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell 해당 명령

다음 예에서는 클러스터 쿼럼을 구성 [하는 데](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum?view=win10-ps) 사용 하는 방법을 보여 줍니다.

다음 예제에서는 *CONTOSO FC1* 클러스터의 쿼럼 구성을 쿼럼 감시가 없는 단순한 노드 과반수 구성으로 변경합니다.

```PowerShell
Set-ClusterQuorum –Cluster CONTOSO-FC1 -NodeMajority
```

다음 예제에서는 로컬 클러스터의 쿼럼 구성을 감시 구성이 있는 노드 과반수로 변경합니다. *Cluster Disk 2*라는 디스크 리소스가 디스크 감시로 구성됩니다.

```PowerShell
Set-ClusterQuorum -NodeAndDiskMajority "Cluster Disk 2"
```

다음 예제에서는 로컬 클러스터의 쿼럼 구성을 감시 구성이 있는 노드 과반수로 변경합니다. * \\ \\CONTOSO-FS\\fsw* 라는 파일 공유 리소스가 파일 공유 감시로 구성 됩니다.

```PowerShell
Set-ClusterQuorum -NodeAndFileShareMajority "\\fileserver\fsw"
```

다음 예제에서는 로컬 클러스터의 *ContosoFCNode1* 노드에서 쿼럼 응답을 제거합니다.

```PowerShell
(Get-ClusterNode ContosoFCNode1).NodeWeight=0
```

다음 예제에서는 로컬 클러스터의 *ContosoFCNode1* 노드에 쿼럼 응답을 추가합니다.

```PowerShell
(Get-ClusterNode ContosoFCNode1).NodeWeight=1
```

다음 예제에서는 **CONTOSO FC1** 클러스터의 *DynamicQuorum* 속성을 사용하도록 설정합니다(이전에 사용하지 않도록 설정된 경우).

```PowerShell
(Get-Cluster CONTOSO-FC1).DynamicQuorum=1
```

## <a name="recover-a-cluster-by-starting-without-quorum"></a>쿼럼 없이 시작하여 클러스터 복구

쿼럼 응답 수가 부족한 클러스터는 시작되지 않습니다. 첫 번째 단계로, 항상 클러스터 쿼럼 구성을 확인하고 클러스터에 더 이상 쿼럼이 없는 이유를 조사해야 합니다. 이는 응답이 중지된 노드가 있는 경우 또는 다중 사이트 클러스터에서 기본 사이트에 연결할 수 없는 경우에 발생할 수 있습니다. 클러스터 실패의 근본 원인을 확인한 후에는 이 섹션에 설명된 복구 단계를 사용할 수 있습니다.

> [!NOTE]
> * 쿼럼 손실로 인해 클러스터 서비스가 중지된 경우 이벤트 ID 1177이 시스템 로그에 나타납니다.
> * 항상 클러스터 쿼럼이 손실된 이유를 조사해야 합니다.
> * 항상 쿼럼 없이 클러스터를 시작하는 것보다 노드 또는 쿼럼 감시를 정상 상태로 전환(클러스터에 연결)하는 것이 좋습니다.

### <a name="force-start-cluster-nodes"></a>클러스터 노드 강제 시작

노드 또는 쿼럼 감시를 정상 상태로 전환하는 것으로 클러스터를 복구할 수 없음을 확인한 후에는 클러스터를 강제로 시작해야 합니다. 클러스터를 강제로 시작하면 클러스터 쿼럼 구성 설정이 재정의되고 클러스터가 **ForceQuorum** 모드로 시작됩니다.

쿼럼이 없는 경우 클러스터를 강제로 시작하는 것은 다중 사이트 클러스터에서 특히 유용할 수 있습니다. 기본 사이트와 백업 사이트가 *SiteA*와 *SiteB*로 별도로 구성된 클러스터에 대한 재해 복구 시나리오를 고려해 보겠습니다. *SiteA*에서 실제 재해가 발생한 경우 해당 사이트를 다시 온라인 상태로 복구하는 데 상당한 시간이 걸릴 수 있습니다. 이 경우 *SiteB*를 강제로 온라인 상태로 전환할 수 있으며, 이는 이 사이트에 쿼럼이 없는 경우에도 마찬가지입니다.

클러스터가 **ForceQuorum** 모드로 시작된 경우에는 충분한 쿼럼 응답을 다시 얻은 후 클러스터가 자동으로 강제 상태를 종료하고 정상적으로 작동합니다. 따라서 클러스터를 정상적으로 다시 시작할 필요가 없습니다. 클러스터에서 노드가 손실되고 이로 인해 쿼럼이 손실되면 더 이상 강제 상태에 있지 않으므로 클러스터가 다시 오프라인 상태로 전환됩니다. 쿼럼이 없는 경우 다시 온라인 상태로 전환 하려면 쿼럼 없이 클러스터를 강제로 시작 해야 합니다.

> [!IMPORTANT]
> * 클러스터가 강제로 시작된 후 관리자는 클러스터에 대한 모든 권한을 가집니다.
> * 클러스터는 강제로 시작된 노드의 클러스터 구성을 사용하며 이를 사용 가능한 다른 모든 노드에 복제합니다.
> * 쿼럼 없이 클러스터를 강제로 시작하면 클러스터가 **ForceQuorum** 모드로 유지되는 동안 모든 쿼럼 구성 설정이 무시됩니다. 여기에는 특정 노드 응답 할당 및 동적 쿼럼 관리 설정이 포함됩니다.

### <a name="prevent-quorum-on-remaining-cluster-nodes"></a>나머지 클러스터 노드에서 쿼럼 방지

노드에서 클러스터를 강제로 시작한 후에는 쿼럼을 방지하는 설정으로 클러스터의 나머지 노드를 시작해야 합니다. 쿼럼을 방지하는 설정으로 시작된 노드는 클러스터 서비스에 새 클러스터 인스턴스를 구성하는 대신 기존의 실행 중인 클러스터에 연결하도록 지시합니다. 이는 나머지 노드에서 두 개의 경쟁 인스턴스가 포함된 분할 클러스터를 구성하는 것을 방지합니다.

이는 백업 사이트 *SiteB*의 클러스터를 강제로 시작한 후 일부 다중 사이트 재해 복구 시나리오에서 클러스터를 복구해야 하는 경우에 필요합니다. *SiteB*에서 강제로 시작된 클러스터에 연결하려면 기본 사이트 *SiteA*의 노드를 쿼럼이 방지된 설정으로 시작해야 합니다.

> [!IMPORTANT]
> 클러스터를 하나의 노드에서 강제로 시작한 후에는 항상 나머지 노드를 쿼럼이 방지된 설정으로 시작하는 것이 좋습니다.

장애 조치(Failover) 클러스터 관리자를 사용 하 여 클러스터를 복구 하는 방법은 다음과 같습니다.

1. 장애 조치(failover) 클러스터 관리자에서 변경할 클러스터를 선택하거나 지정합니다.
2. 클러스터를 선택한 상태에서 **작업**아래에 있는 **클러스터 강제 시작**을 선택 합니다.

    장애 조치(failover) 클러스터 관리자가 연결할 수 있는 모든 노드에서 클러스터를 강제로 시작합니다. 이 클러스터는 시작할 당시의 클러스터 구성을 사용합니다.

> [!NOTE]
> * 사용할 클러스터 구성이 포함 된 특정 노드에서 클러스터를 강제로 시작 하려면이 절차 이후에 제공 되는 것과 같은 명령줄 도구 또는 Windows PowerShell cmdlet을 사용 해야 합니다. 
> * 장애 조치(failover) 클러스터 관리자를 사용하여 강제 시작된 클러스터에 연결한 경우 **클러스터 서비스 시작** 작업을 사용하여 노드를 시작하면 쿼럼을 방지하는 설정으로 노드가 자동으로 시작됩니다.

#### <a name="windows-powershell-equivalent-commands-start-clusternode"></a>Windows PowerShell 해당 명령 (Start-clusternode)

다음 예제에서는 **Start-ClusterNode** cmdlet을 사용하여 *ContosoFCNode1* 노드에서 클러스터를 강제로 시작하는 방법을 보여 줍니다.

```PowerShell
Start-ClusterNode –Node ContosoFCNode1 –FQ
```

또는 노드에서 다음 명령을 로컬로 입력할 수 있습니다.

```PowerShell
Net Start ClusSvc /FQ
```

다음 예제에서는 **Start-ClusterNode** cmdlet을 사용하여 *ContosoFCNode1* 노드에서 쿼럼이 방지된 설정으로 클러스터 서비스를 시작하는 방법을 보여 줍니다.

```PowerShell
Start-ClusterNode –Node ContosoFCNode1 –PQ
```

또는 노드에서 다음 명령을 로컬로 입력할 수 있습니다.

```PowerShell
Net Start ClusSvc /PQ
```

## <a name="quorum-considerations-for-disaster-recovery-configurations"></a>재해 복구 구성에 대한 쿼럼 고려 사항

이 섹션에는 재해 복구 배포의 두 가지 다중 사이트 클러스터 구성에 대한 특성 및 쿼럼 구성이 요약되어 있습니다. 쿼럼 구성 지침은 사이트 간의 작업에 자동 장애 조치(failover)가 필요한지 또는 수동 장애 조치(failover)가 필요한지에 따라 다릅니다. 일반적으로 구성은 사이트의 장애 또는 재해 시 클러스터된 작업을 제공하고 지원하기 위해 조직에 구현되어 있는 SLA(서비스 수준 계약)를 따릅니다.

### <a name="automatic-failover"></a>자동 장애 조치(automatic failover)

이 구성에서는 클러스터가 클러스터된 역할을 호스트할 수 있는 둘 이상의 사이트로 구성됩니다. 임의의 사이트에서 장애가 발생한 경우 클러스터된 역할이 나머지 사이트로 자동으로 장애 조치(failover)되어야 합니다. 따라서 임의의 사이트에서 전체 사이트 장애를 유지할 수 있도록 클러스터 쿼럼을 구성해야 합니다.

다음 표에는 이 구성에 대한 고려 사항 및 권장 사항이 요약되어 있습니다.

| 항목  | 설명  |
| ---------| ---------|
| 사이트당 노드 응답 수     | 동일해야 함       |
| 노드 응답 할당     |  모든 노드가 동일하게 중요하므로 노드 응답을 제거할 수 없음       |
| 동적 쿼럼 관리     |   사용해야 함      |
| 감시 구성     |  파일 공유 감시가 권장되며, 클러스터 사이트와 별도의 사이트에 구성됨       |
| 워크로드     |  모든 사이트에서 작업을 구성할 수 있음       |

#### <a name="additional-considerations-for-automatic-failover"></a>자동 장애 조치에 대 한 추가 고려 사항

- 각 사이트에 동등한 존속 기회를 제공하려면 파일 공유 감시를 별도의 사이트에 구성해야 합니다. 자세한 내용은 이 항목의 앞부분에 있는 [감시 구성](#witness-configuration)을 참조하세요.

### <a name="manual-failover"></a>수동 장애 조치(failover)

이 구성에서는 클러스터가 기본 사이트(*SiteA*)와 백업(복구) 사이트(*SiteB*)로 구성됩니다. 클러스터된 역할은 *SiteA*에서 호스트됩니다. 클러스터 쿼럼 구성으로 인해, *SiteA*의 모든 노드에서 장애가 발생한 경우 클러스터의 작동이 중지됩니다. 이 시나리오에서는 관리자가 클러스터 서비스를 *SiteB*로 수동으로 장애 조치(failover)하고 추가 단계를 수행하여 클러스터를 복구해야 합니다.

다음 표에는 이 구성에 대한 고려 사항 및 권장 사항이 요약되어 있습니다.

| 항목   |설명  |
| ---------| ---------|
| 사이트당 노드 응답 수     |  <ul><li> 노드 응답을 기본 사이트(**SiteA**)의 노드에서 제거할 수 없음</li><li>노드 응답을 백업 사이트(**SiteB**)의 노드에서 제거해야 함</li><li>**SiteA**에서 장기 중단이 발생한 경우 해당 사이트의 쿼럼 과반수를 복구의 일부로 사용하려면 **SiteB**의 노드에 응답을 할당해야 함</li>       |
| 동적 쿼럼 관리     |  사용해야 함       |
| 감시 구성     |  <ul><li>**SiteA**에 짝수 개의 노드가 있는 경우 감시 구성</li><li>감시가 필요한 경우 **SiteA**의 노드에서만 액세스할 수 있는 파일 공유 감시 또는 디스크 감시 구성(비대칭 디스크 감시라고도 함)</li>       |
| 워크로드     |  기본 설정된 소유자를 사용하여 **SiteA**의 노드에서 작업의 실행 상태 유지       |

#### <a name="additional-considerations-for-manual-failover"></a>수동 장애 조치 (failover)에 대 한 추가 고려 사항

- *SiteA*의 노드만 초기에 쿼럼 응답으로 구성됩니다. 이는 *SiteB*의 노드 상태가 클러스터 쿼럼에 영향을 주지 않도록 하는 데 필요합니다.
- *SiteA*의 장애가 일시적인지 또는 장기적인지에 따라 복구 단계가 다를 수 있습니다.

## <a name="more-information"></a>자세한 정보

* [장애 조치(failover) 클러스터링](failover-clustering.md)
* [장애 조치(Failover) 클러스터 Windows PowerShell cmdlet](https://docs.microsoft.com/powershell/module/failoverclusters/?view=win10-ps)
* [클러스터 및 풀 쿼럼 이해](../storage/storage-spaces/understand-quorum.md)