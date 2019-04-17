---
title: 장애 조치 클러스터링 하드웨어 요구 사항 및 저장소 옵션
description: 하드웨어 요구 사항 및 장애 조치 클러스터 만들기 (영문)에 대 한 저장 옵션입니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4706372b06d0554196b692c3ddcda145dee5bae5
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082483"
---
# <a name="failover-clustering-hardware-requirements-and-storage-options"></a>장애 조치 클러스터링 하드웨어 요구 사항 및 저장소 옵션

적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

장애 조치 클러스터를 만들려면 다음 하드웨어가 필요 합니다. Microsoft에서 지원 하려면 모든 하드웨어의 실행 중인 Windows Server 버전에 대 한 인증 해야 하 고 전체 장애 조치 클러스터 솔루션 유효성 검사 구성 마법사에서에서 모든 테스트를 통과 해야 합니다. 장애 조치 클러스터 유효성을 검사 하는 방법에 대 한 자세한 내용은 [장애 조치 클러스터에 대 한 하드웨어의 유효성을 검사](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>)를 참조 하십시오.

- **서버**: 일치 하는 동일 하거나 비슷한 구성 요소를 포함 하는 컴퓨터의 집합을 사용 하는 것이 좋습니다.
- **네트워크 어댑터 및 케이블 (네트워크 통신용)**: iSCSI를 사용 하는 경우 각 네트워크 어댑터 네트워크 통신 또는 iSCSI 둘 중 하나를 전용 해야 합니다.

    클러스터 노드를 연결 하는 네트워크 인프라에서 단일 오류 지점이 필요 하지 않습니다. 다중, 하 여 클러스터 노드를 연결할 수 등 고유한 네트워크입니다. 또는 조합 된 네트워크 어댑터, 중복 스위치, 중복 라우터 또는 단일 오류 지점을 제거 하는 비슷한 하드웨어 구성 되는 하나의 네트워크와 클러스터 노드를 연결할 수 있습니다.

    >[!NOTE]
    >단일 네트워크에 연결 된 클러스터 노드를 연결 하는 경우 네트워크에서 구성 마법사가 유효성 검사에서 중복 요구 사항을 전달 합니다. 그러나 마법사에서 보고서에는 네트워크 단일 오류 지점이 없어야 경고가 포함 됩니다.

- **장치 컨트롤러 또는 저장소에 대 한 적절 한 어댑터**:

  - **Serial Attached SCSI 또는 파이버 채널**: 클러스터 된 모든 서버에서 Serial Attached SCSI 또는 파이버 채널을 사용 하는, 저장소 스택의 요소를 모두 동일 해야 합니다. 필요한 다중 경로 I/O (MPIO) 소프트웨어 같을 수 있는지를 두고 모듈 DSM (장치별) 소프트웨어와 동일 합니다. 것이 좋습니다는 대용량 저장 장치 컨트롤러-호스트 버스 어댑터 (HBA), HBA 드라이버와 HBA 펌웨어-에 연결 되는 클러스터 저장소 같을 수 있습니다. 서로 다른 Hba를 사용 하는 경우 확인 해야 저장소 공급 업체와 해당 하는 지원 되는 또는 권장 구성을 수행 됩니다.
  - **iSCSI**: 하나 이상의 네트워크 어댑터 또는 Hba 클러스터 저장소 전용 클러스터 된 각 서버 iSCSI를 사용 하는 경우 있어야 합니다. ISCSI에 사용할 네트워크 네트워크 통신을 위해 안됩니다. 클러스터 된 모든 서버에서 사용 하 여 iSCSI 저장소 대상에 연결할 네트워크 어댑터, 동일 해야 하며 기가 비트 이더넷을 사용 하는 것이 좋습니다 이상입니다.
- **저장소**: Windows Server 2012 R2 또는 Windows Server 2012와 호환 되는 저장소를 공유 또는 [저장소 공간 직접](../storage/storage-spaces/storage-spaces-direct-overview.md) 사용 해야 합니다. 연결 된 공유 저장소를 사용할 수 있는 및 장애 조치 클러스터에서 구성 된 Hyper-v를 실행 하는 서버에 대 한 공유 저장소로 SMB 3.0 파일 공유를 사용할 수도 있습니다. 자세한 내용은 [배포 Hyper-v SMB 통해](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)을 참조 하십시오.

    대부분의 경우에서 연결 된 저장소 다중을 포함 해야, 하드웨어 수준에서 구성 된 디스크 (논리 단위 번호 또는 Lun)를 구분 합니다. 일부 클러스터에 대 한 디스크 하나 (이 하위 섹션의 끝에 설명 되어 있음) 디스크 미러링 모니터 서버로 작동 합니다. 다른 디스크 (클러스터 된 서비스 또는 응용 프로그램에 이전 버전)는 클러스터 된 역할에 필요한 파일을 포함 합니다. 저장소 요구 사항에는 다음이 포함 됩니다.

  - 장애 조치 클러스터링에 포함 된 기본 디스크 지원을 사용 하려면 기본 디스크를 하지 동적 디스크를 사용 합니다.
  - Ntfs 파티션의 서식을 지정 하는 것이 좋습니다. 클러스터 공유 볼륨 (CSV)를 사용 하는 경우 이러한 각 파티션을 NTFS 이어야 합니다.

    >[!NOTE]
    >쿼럼 구성에 대 한 디스크 미러링 모니터를 포함 하는 경우 NTFS 또는 복원 파일 시스템 (ReFS)와 디스크를 서식을 지정할 수 있습니다.

  - 디스크의 파티션 스타일에 대 한 마스터 부팅 (킬로바이트) 또는 GUID 파티션 테이블 (GPT) 중 하나를 사용할 수 있습니다.

    디스크 미러링 모니터 서버는 클러스터 구성 데이터베이스의 복사본을 저장 하기 위해 지정 된 클러스터 저장소의 디스크입니다. 장애 조치 클러스터 쿼럼 구성의 일부로이 경로 지정 하는 경우에 디스크 미러링 모니터를 있습니다. 자세한 내용은 [저장소 공간 직접에서 이해 쿼럼](../storage/storage-spaces/understand-quorum.md)를 참조 하십시오.

## <a name="hardware-requirements-for-hyper-v"></a>Hyper-v에 대 한 하드웨어 요구 사항

클러스터 된 가상 컴퓨터를 포함 하는 장애 조치 클러스터를 만드는 경우 클러스터 서버는 Hyper-v 역할에 대 한 하드웨어 요구를 지원 해야 합니다. Hyper-v에는 다음을 포함 하는 64 비트 프로세서가 필요 합니다.

- 하드웨어 지원 가상화 이 가상화 옵션이 포함 된 프로세서에서 사용할 수 있는-프로세서 같이 Intel 가상화 기술 (Intel VT) 또는 Amd-v (AMD) AMD 가상화 기술을 사용 합니다.
- 하드웨어 강제 DEP 데이터 실행 방지 ()는 사용할 수 있고 사용 하도록 설정 이어야 합니다. Intel XD 비트 사용 하도록 설정 해야 특히 (실행 불능 비트) 또는 AMD NX 비트 (execute 비트 없음).

Hyper-v 역할에 대 한 자세한 내용은 [Hyper-v 개요](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831531(v%3dws.11)>)를 참조 하십시오.

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>장애 조치 클러스터와 함께 저장 영역 네트워크를 배포합니다.

장애 조치 클러스터 저장 영역 네트워크 (SAN)를 배포할 때 다음이 지침을 따르십시오.

- **저장소의 호환성을 확인**: 제조업체 및 공급 업체 드라이버, 펌웨어 및의 저장에 사용 되는 소프트웨어를 포함 하는 저장소와 호환 되는 장애 조치 클러스터의 실행 중인 Windows Server 버전에서 사용 하 여 확인 합니다.
- **저장 장치 격리, 장치당 클러스터**: 서로 다른 클러스터에 서버를에서 같은 저장 장치에 액세스할 수 여야 합니다. 대부분의 경우에서 하나의 클러스터 서버 집합에 사용 되는 LUN LUN 마스킹 또는 영역 지정을 통해 다른 모든 서버에서 격리 해야 합니다.
- **다중 경로 I/O 소프트웨어를 사용 하 여 또는 네트워크 어댑터 협력 하 여 고려 해야할**: 가용성이 높은 저장소 구성에서는 다중 경로 I/O 소프트웨어를 사용 하 여 여러 호스트 버스 어댑터를 사용 하 여 장애 조치 클러스터를 배포 하거나 수 네트워크 어댑터 (라고도 함 부하 팀 구성 분산 및 장애 조치 또는 LBFO)입니다. 가장 높은 수준의 중복 및 가용성을 제공 합니다. Windows Server 2012 R2 또는 Windows Server 2012에 대 한 다중 경로 솔루션에 Microsoft I/O MPIO (다중 경로)를 기반 해야 합니다. 일반적으로 하드웨어 공급 업체는 Windows Server 운영 체제의 일부로 하나 이상의 DSMs를 제공 하 고 있지만, 하드웨어에 대 한 MPIO 장치별 모듈 DSM ()를 제공 해야 합니다.

    LBFO 하는 방법에 대 한 자세한 내용은 Windows Server 기술 라이브러리에서 [NIC 팀 구성 개요](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming) 참조 하십시오.

    >[!IMPORTANT]
    >호스트 버스 어댑터 및 다중 경로 I/O 소프트웨어 버전에 매우 중요 한 될 수 있습니다. 클러스터에 대 한 다중 경로 솔루션을 구현 하는 경우 올바른 어댑터, 펌웨어 및 소프트웨어를 실행 하는 Windows server 버전에 대 한 선택 하드웨어 공급 업체와 밀접 하 게 작동 합니다.

- **저장소 공간을 사용 하 여 고려 해야할**: 저장 공간을 사용 하 여 구성 된 직렬 연결된 SCSI (SAS) 클러스터 저장소를 배포 하려는 경우 [클러스터 된 저장소 공간 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>) 요구 사항에 대 한 참조입니다.

## <a name="more-information"></a>자세한 정보

- [장애 조치(failover) 클러스터링](failover-clustering.md)
- [저장소 공간](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831739(v%3dws.11)>)
- [고가용성을 위한 게스트 클러스터링 사용](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)