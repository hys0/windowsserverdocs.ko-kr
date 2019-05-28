---
title: 장애 조치 클러스터링 하드웨어 요구 사항 및 저장소 옵션
description: 하드웨어 요구 사항 및 장애 조치 클러스터를 만들기 위한 저장소 옵션입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: e6eb6f2acd420ae657a5c1b698e9733751378552
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476076"
---
# <a name="failover-clustering-hardware-requirements-and-storage-options"></a>장애 조치 클러스터링 하드웨어 요구 사항 및 저장소 옵션

적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

장애 조치 클러스터를 만들려면 다음 하드웨어가 필요합니다. Microsoft의 지원을 받으려면 모든 하드웨어가 현재 실행 중인 Windows Server 버전에 대해 인증되어야 하며 완전한 장애 조치(failover) 클러스터 솔루션이 구성 유효성 검사 마법사의 모든 테스트를 통과해야 합니다. 장애 조치(Failover) 클러스터 유효성 검사에 대한 자세한 내용은 [Validate Hardware for a Failover Cluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>)를 참조하세요.

- **서버**: 동일하거나 유사한 구성 요소가 포함된 하나의 일치하는 컴퓨터 집합을 사용하는 것이 좋습니다.
- **네트워크 어댑터 및 케이블(네트워크 통신용)** : iSCSI를 사용하는 경우 각 네트워크 어댑터는 네트워크 통신 전용이나 iSCSI 전용 중 하나여야 합니다.

    클러스터 노드를 연결하는 네트워크 인프라에는 단일 실패 지점이 없도록 해야 합니다. 예를 들면 여러 개별 네트워크를 사용하여 클러스터 노드를 연결할 수 있습니다. 또는 팀으로 구성 된 네트워크 어댑터, 중복 스위치, 중복 라우터 또는 단일 실패 지점을 제거 하는 유사한 하드웨어를 사용 하 여 생성 된 하나의 네트워크를 사용 하 여 클러스터 노드를 연결할 수 있습니다.

    >[!NOTE]
    >클러스터 노드를 단일 네트워크에 연결하면 해당 네트워크는 구성 유효성 검사 마법사에서 중복성 요구 사항을 통과합니다. 그러나 마법사에서 생성하는 보고서에는 네트워크에 단일 실패 지점이 없어야 한다는 경고가 포함됩니다.

- **저장소에 대한 장치 컨트롤러 또는 적절한 어댑터**:

  - **SAS(Serial Attached SCSI) 또는 파이버 채널**: SAS(Serial Attached SCSI) 또는 파이버 채널을 사용하는 경우 모든 클러스터형 서버에서 저장소 스택의 모든 요소가 동일해야 합니다. 다중 경로 I/O (MPIO) 소프트웨어가 동일 해야 하며, 장치 DSM (장치별 모듈) 소프트웨어와 동일할 수는 필수 항목입니다. 것이 좋습니다는 대용량 저장 장치 컨트롤러가-호스트 버스 어댑터 (HBA), HBA 드라이버 및 HBA 펌웨어-에 연결 된 클러스터 저장소와 동일할 수 있습니다. 유사하지 않은 HBA를 사용하는 경우 해당 저장소 공급업체에서 지원 또는 권장하는 구성을 따르고 있는지 확인해야 합니다.
  - **iSCSI**: iSCSI를 사용하는 경우 각 클러스터형 서버에는 클러스터 저장소 전용인 하나 이상의 네트워크 어댑터 또는 HBA가 있어야 합니다. iSCSI용으로 사용하는 네트워크는 네트워크 통신용으로 사용하면 안 됩니다. 클러스터형 모든 서버에서 iSCSI 저장소 대상에 연결하는 데 사용하는 네트워크 어댑터가 동일해야 하며 Gigabit Ethernet 이상을 사용하는 것이 좋습니다.
- **저장소**: 사용 해야 합니다 [저장소 공간 다이렉트](../storage/storage-spaces/storage-spaces-direct-overview.md) 또는 Windows Server 2012 R2 또는 Windows Server 2012와 호환 되는 저장소를 공유 합니다. 연결 된 공유 저장소를 사용할 수 있습니다 하 고 장애 조치 클러스터에 구성 된 Hyper-v를 실행 하는 서버에 대 한 공유 저장소로 SMB 3.0 파일 공유를 사용할 수도 있습니다. 자세한 내용은 [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)를 참조하세요.

    대부분의 경우 연결된 저장소에는 하드웨어 수준에서 구성된 여러 개별 디스크(논리 단위 번호, 즉 LUN)가 포함되어야 합니다. 일부 클러스터의 경우 하나의 디스크가 디스크 감시 기능(이 하위 섹션 끝에 설명)을 수행합니다. 다른 디스크에는 클러스터된 역할(전에는 클러스터된 서비스 또는 응용 프로그램이라고 함)에 필요한 파일이 있습니다. 다음과 같은 저장소 요구 사항이 있습니다.

  - 장애 조치(failover) 클러스터링에 포함된 기본 디스크 지원을 사용하려면 동적 디스크가 아닌 기본 디스크를 사용합니다.
  - 파티션을 NTFS 형식으로 만드는 것이 좋습니다. CSV(클러스터 공유 볼륨)를 사용하는 경우 이들의 각 파티션은 NTFS 형식이어야 합니다.

    >[!NOTE]
    >쿼럼 구성에 대한 디스크 감시가 있는 경우 NTFS 또는 ReFS(복원 파일 시스템)로 디스크를 포맷할 수 있습니다.

  - 디스크의 파티션 형식으로는 MBR(마스터 부트 레코드) 또는 GPT(GUID 파티션 테이블) 중 하나를 사용할 수 있습니다.

    디스크 감시는 클러스터 구성 데이터베이스의 복사본을 저장 하도록 지정 된 클러스터 저장소의 디스크. 장애 조치(failover) 클러스터에는 쿼럼 구성의 일부로 지정된 경우에만 디스크 미러링 모니터가 포함됩니다. 자세한 내용은 [저장소 공간 다이렉트에서 이해 쿼럼](../storage/storage-spaces/understand-quorum.md)합니다.

## <a name="hardware-requirements-for-hyper-v"></a>Hyper-V에 대한 하드웨어 요구 사항

클러스터된 가상 컴퓨터가 포함된 장애 조치(failover) 클러스터를 만드는 경우 클러스터 서버에서 Hyper-V 역할에 대한 하드웨어 요구 사항을 지원해야 합니다. Hyper-V를 사용하려면 다음이 포함된 64비트 프로세서가 필요합니다.

- 하드웨어 지원 가상화. 하드웨어 지원 가상화는 가상화 옵션, 특히 Intel VT(Intel Virtualization Technology) 또는 AMD-V(AMD Virtualization) 기술을 포함한 프로세서에서 사용할 수 있습니다.
- 하드웨어 적용 DEP(데이터 실행 방지)가 제공되고, 사용하도록 설정되어 있어야 합니다. 특히 Intel XD 비트(execute disable bit) 또는 AMD NX 비트(no execute bit)를 사용해야 합니다.

Hyper-V 역할에 대한 자세한 내용은 [Hyper-V 개요](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831531(v%3dws.11)>)를 참조하세요.

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>장애 조치(failover) 클러스터로 저장 영역 네트워크 배포

장애 조치 클러스터로 SAN(저장 영역 네트워크)을 배포하는 경우 이 지침을 따릅니다.

- **저장소 호환성 확인**: 제조업체 및 공급업체와 함께 저장소(저장소에 사용되는 드라이버, 펌웨어 및 소프트웨어 포함)가 현재 실행 중인 Windows Server 버전의 장애 조치(failover) 클러스터와 호환되는지 확인합니다.
- **저장 장치 분리, 장치당 클러스터 하나**: 서로 다른 클러스터의 서버가 같은 저장 장치에 액세스하면 안 됩니다. 대부분의 경우 하나의 클러스터 서버 집합에 사용되는 LUN은 LUN 마스킹 또는 영역 지정을 통해 다른 모든 서버에서 격리되어야 합니다.
- **다중 경로 I/O 소프트웨어 또는 조합된 네트워크 어댑터 사용 고려**: 가용성이 높은 저장소 패브릭에서 다중 경로 I/O 소프트웨어 또는 네트워크 어댑터 팀(부하 분산 및 장애 조치(failover), 즉 LBFO라고도 함)을 사용해 장애 조치(failover) 클러스터를 여러 호스트 버스 어댑터와 함께 배포할 수 있습니다. 이를 통해 최고 수준의 중복성 및 가용성이 제공됩니다. Windows Server 2012 R2 또는 Windows Server 2012에 대 한 다중 경로 솔루션에 Microsoft MPIO (Multipath I/O) 기반 해야 합니다. Windows Server에 운영 체제의 일부로 DSM(장치별 모듈)이 하나 이상 포함되어 있지만 대개 하드웨어 공급업체에서 하드웨어용 MPIO DSM을 제공합니다.

    LBFO에 대 한 자세한 내용은 참조 하십시오 [NIC 팀 개요](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming) Windows Server 기술 라이브러리에서.

    >[!IMPORTANT]
    >호스트 버스 어댑터 및 다중 경로 I/O 소프트웨어는 버전에 매우 민감할 수 있습니다. 클러스터에 대한 다중 경로 솔루션을 구축하는 경우 하드웨어 공급업체와 긴밀하게 협력하여 현재 실행 중인 Windows Server 버전에 대해 올바른 어댑터, 펌웨어 및 소프트웨어를 선택해야 합니다.

- **저장소 공간 사용 고려**: 배포 하려는 경우 serial attached SCSI (SAS) 클러스터 된 저장소를 저장소 공간을 사용 하도록 구성을 참조 하십시오 [Deploy Clustered Storage Spaces](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>) 요구 사항에 대 한 합니다.

## <a name="more-information"></a>자세한 정보

- [장애 조치(failover) 클러스터링](failover-clustering.md)
- [스토리지 공간](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831739(v%3dws.11)>)
- [고가용성을 위한 게스트 클러스터링을 사용 하 여](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)