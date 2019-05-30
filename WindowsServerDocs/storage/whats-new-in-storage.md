---
ms.assetid: 0f2a7f7b-aca8-4e5d-ad67-4258e88bc52f
title: Windows Server에서 제공되는 저장소의 새로운 기능
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dongill
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 05/29/2019
ms.openlocfilehash: 5469d663f64fdb453e03863f409b675473d3f6aa
ms.sourcegitcommit: 8eea7aadbe94f5d4635c4ffedc6a831558733cc0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66308567"
---
# <a name="whats-new-in-storage-in-windows-server"></a>Windows Server에서 저장소의 새로운 기능

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server (반기 채널)

이 항목에서는 Windows Server 2019, Windows Server 2016에서에서 저장소의 새로운 기능과 변경 된 기능에 설명 하 고 Windows 서버 반기 채널 해제 합니다.

## <a name="whats-new-in-storage-in-windows-server-2019-and-windows-server-version-1903"></a>Windows Server 2019에 Windows Server 1903 버전 저장소의 새로운 기능

이 릴리스의 Windows Server는 다음과 같은 변경 및 기술에 추가합니다.

### <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>로컬 계정, 클러스터 및 Linux 서버에 이제 storage Migration Service 마이그레이션

저장소 마이그레이션 서비스를 사용 하면 쉽게 서버를 Windows Server의 최신 버전으로 마이그레이션할 수입니다. 서버에서 데이터를 인벤토리에 포함 하 고 데이터 및 구성을 새 서버로 전송 하는 그래픽 도구를 제공, 앱 또는 사용자가 아무 것도 변경할 필요가 없이 합니다.

이 버전의 Windows Server 마이그레이션을 오케스트레이션 하기 위해 사용 하는 경우에 다음과 같은 기능을 추가 했습니다.

- 새 서버에 로컬 사용자 및 그룹 마이그레이션
- 장애 조치 클러스터에서 저장소를 마이그레이션
- Samba를 사용 하는 Linux 서버에서 저장소를 마이그레이션하십시오.
- 보다 쉽게 Azure File Sync를 사용 하 여 Azure로 마이그레이션된 공유를 동기화
- Azure와 같은 새 네트워크로 마이그레이션

저장소 마이그레이션 서비스에 대 한 자세한 내용은 참조 하세요. [저장소 마이그레이션 서비스 개요](storage-migration-service/overview.md)합니다.

### <a name="system-insights-disk-anomaly-detection"></a>시스템 Insights 디스크 변칙 검색

[시스템 Insights](../manage/system-insights/overview.md) 로컬 Windows Server 시스템 데이터를 분석 하 고 서버의 기능에 대 한 정보를 제공 하는 예측 분석 기능입니다. 많은 기본 제공 기능을 제공 하지만 디스크 변칙 검색부터 Windows Admin Center 통해 추가 기능을 설치 하는 기능 추가 했습니다.

변칙 검색 디스크는 디스크 동작 하는 경우를 강조 표시 하는 새로운 기능 *다르게* 평소 보다 합니다. 다른 반드시 하는 동안 시스템에서 문제를 해결할 때에 이러한 비정상적인 분 표시 나쁘지 유용할 수 있습니다.

이 기능은 Windows Server 2019를 실행 하는 서버를 사용할 수도 있습니다.

### <a name="windows-admin-center-enhancements"></a>Windows Admin Center 향상 된 기능

Windows Admin Center 새 릴리스가, Windows Server에 새 기능을 추가 합니다. 최신 기능에 대 한 정보를 참조 하세요 [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md)합니다.

## <a name="whats-new-in-storage-in-windows-server-2019-and-windows-server-version-1809"></a>Windows Server 2019에 Windows Server 1809 버전 저장소의 새로운 기능

이 릴리스의 Windows Server는 다음과 같은 변경 및 기술에 추가합니다.

### <a name="manage-storage-with-windows-admin-center"></a>Windows Admin Center 사용 하 여 저장소 관리

[Windows Admin Center](../manage/windows-admin-center/overview.md) 은 서버, 클러스터, 저장소 공간 다이렉트 및 Windows 10 Pc를 사용 하 여 하이퍼 수렴 형 인프라를 관리 하기 위한 새 로컬로 배포 된, 브라우저 기반 앱. Windows 이외의 추가 비용 없이 제공 하 고 프로덕션 사용 준비가 된 것입니다.

Windows Admin Center Windows Server 2019에 다른 버전의 Windows 실행 하는 별도 다운로드 수 있지만 새 이므로 않으려는 놓칠 수 있습니다...

### <a name="storage-migration-service"></a>저장소 마이그레이션 서비스

저장소 마이그레이션 서비스는 서버를 Windows Server의 최신 버전으로 쉽게 마이그레이션할 수 있는 새로운 기술입니다. 서버의 데이터를 인벤토리화하는 그래픽 도구를 제공하며, 데이터 및 구성을 최신 서버로 전송한 다음, 선택적으로 이전 서버의 ID를 새로운 서버로 이동하여 앱 및 사용자가 아무 것도 변경할 필요가 없도록 합니다. 자세한 내용은 [저장소 마이그레이션 서비스](storage-migration-service/overview.md)를 참조하세요.

### <a id="storage-spaces-direct"></a>저장소 공간 다이렉트 (Windows Server 2019만 해당)

향상 된 Windows Server 2019에서 저장소 공간 다이렉트는 여러 가지 (저장소 공간 다이렉트에 포함 되지 Windows Server 반기 채널):

- **중복 제거 및 ReFS 볼륨에 대 한 압축**

    중복 제거 및 ReFS 파일 시스템에 대 한 압축을 사용 하 여 동일한 볼륨에 10 배 더 많은 데이터를 저장 합니다. (있기 [하나만 클릭](https://www.youtube.com/watch?v=PRibTacyKko&feature=youtu.be) 를 Windows Admin Center 사용 하 여 켭니다.) 다중 스레드 사후 처리 아키텍처 유지 성능에 미치는 영향을 최소화 하는 동안 절감 비율이 최대화 하는 선택적 압축을 사용 하 여 가변 크기 청크 저장소입니다. 볼륨을 지 원하는 최대 64TB 및 각 파일의 첫 번째 4TB 중복 제거 됩니다.

- **영구 메모리에 대 한 기본 지원**

    Intel® Optane™ DC PM 및 NVDIMM-N을 포함한 영구 메모리 모듈에 대한 기본 저장소 공간 다이렉트 지원으로 전례가 없는 수준으로 성능이 개선됩니다. 영구 메모리를 캐시로 사용하여 활성 작업 집합을 가속하거나 용량으로 사용하여 마이크로초 단위의 낮은 대기 시간을 일관적으로 보장합니다. PowerShell 또는 Windows Admin Center에서 다른 드라이브와 마찬가지로 영구 메모리를 관리합니다.

- **2-노드 가장자리 하이퍼 수렴 형 인프라에 대 한 중첩 된 복원 력**

    RAID 5+1에서 영감을 얻은 새로운 소프트웨어 복원력 옵션을 통해 두 가지 하드웨어 오류를 한 번에 해결합니다. 중첩된 복원력을 사용하여 2-노드 저장소 공간 다이렉트 클러스터는 하나의 서버 노드가 중단되고 드라이브가 다른 서버 노드에서 오류가 발생하는 경우에도 앱 및 가상 컴퓨터에 대해 지속적으로 액세스 가능한 저장소를 제공할 수 있습니다.

- **감시로 플래시 드라이브를 USB를 사용 하 여 두 서버 클러스터**

    라우터를 꽂는 저렴 한 비용 USB 플래시 드라이브를 사용 하 여 두 서버 클러스터에서 미러링 모니터 서버 역할을 합니다. 서버가 다운 하 고 다음 백업에서 USB 드라이브 클러스터 인식 하는 경우 서버는 최신 데이터를 갖습니다. 자세한 내용은 참조는 [Microsoft 블로그의 저장소](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/)합니다.

- **Windows Admin Center**

    Windows Admin Center의 [전용 대시보드](../manage/windows-admin-center/use/manage-hyper-converged.md) 및 환경을 통해 저장소 공간 다이렉트를 관리 및 모니터링합니다. 클릭 몇 번으로 볼륨 만들기, 열기, 확장 또는 삭제가 가능합니다. 전체 클러스터부터 개별 SSD 또는 HDD의 IOPS 및 IO 대기 시간과 같은 성능을 모니터링합니다. Windows Server 2016 및 Windows Server 2019의 경우 추가 비용 없이 사용 가능합니다.

- **성능 기록**

    [기본 제공 기록](storage-spaces/performance-history.md)을 통해 리소스 사용률 및 성능을 간편하게 확인합니다. 컴퓨팅, 메모리, 네트워크 및 저장소에 걸친 50개 이상의 필수 카운터가 자동으로 수집되어 클러스터에 최대 1년 동안 저장됩니다. 무엇보다 설치 후 구성할 필요 없이 바로 작동합니다. Windows Admin Center에서 시각화하거나 PowerShell에서 쿼리 및 처리합니다.

- **최대 4 확장 클러스터 당 PB**

    몇 페타바이트까지 확장이 가능해 미디어, 백업 및 보관 사용 사례에 적합합니다. Windows Server 2019에서 저장소 공간 다이렉트는 최대 4PB(페타바이트)를 지원합니다. 4PB는 저장소 풀당 4,000 테라바이트의 원시 용량입니다. 관련 용량 지침 또한 증가했습니다. 예를 들어 전보다 2배 더 많은 볼륨(32개 대신 64개)과 볼륨당 용량(32TB 대신 64TB)을 확보할 수 있습니다. 에 여러 클러스터를 함께 붙이기 위한을 [클러스터 설정](storage-spaces/cluster-sets.md) 하나의 저장소 네임 스페이스 내에서 더 큰 확장에 대 한 합니다. 자세한 내용은 참조는 [Microsoft 블로그의 저장소](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/)합니다.

- **패리티 미러 가속 2 배 빠릅니다.**

    미러-가속 패리티를 사용하여 부분 미러 및 부분 패리티 저장소 공간 다이렉트 볼륨(예: RAID-1과 RAID-5/6의 혼합)을 만들어 두 가지 모두 사용할 수 있습니다. (있기 [생각 보다 쉽게](https://www.youtube.com/watch?v=R72QHudqWpE) Windows Admin Center.) Windows Server 2019에 패리티 미러 가속의 성능은 두 배 이상 Windows Server 2016을 기준으로 최적화 덕분입니다.

- **드라이브 대기 시간 이상 값 검색**

    Microsoft Azure에서 오랫동안 성공적이었던 접근 방식의 영감을 받아 사전 모니터링 및 기본 제공 아웃라이어 감지를 통해 대기 시간이 비정상적인 드라이브를 식별합니다. 평균 대기 시간 또는 더욱 구체적으로 99번째 백분위 대기 시간 사용 여부와 무관하게 느린 드라이브는 PowerShell 및 Windows Admin Center에서 '비정상적인 대기 시간' 상태로 레이블 지정됩니다.

- **수동으로 내결함성을 향상 시키려면 볼륨 할당을 구분**

    이 통해 수동으로 저장소 공간 다이렉트의 볼륨 할당을 구분 하는 관리자. 이렇게 하면 특정 조건에서 내결함성을 크게 높일 수 있도록 하지만 적용 일부 추가 관리 고려 사항 및 복잡성입니다. 자세한 내용은 참조 하세요. [볼륨 할당을 구분](storage-spaces/delimit-volume-allocation.md)합니다.

### <a name="storage-replica2019"></a>저장소 복제본

향상 된 기능을 여러 가지 [저장소 복제본](storage-replica/storage-replica-overview.md) 이 릴리스에서:

#### <a name="storage-replica-in-windows-server-standard-edition"></a>Windows Server Standard Edition에서에서 저장소 복제본

이제 Windows Server Datacenter Edition 외에 Standard Edition을 사용 하 여 저장소 복제본을 사용할 수 있습니다. Windows Server Standard Edition에서 실행 되는 저장소 복제본에 다음과 같은 제한 사항이 있습니다.

- 저장소 복제본 볼륨 개수에 제한 없이 대신 단일 볼륨을 복제합니다.
- 볼륨은 크기가 무제한 대신 최대 2TB의 크기를 가질 수 있습니다.

#### <a name="storage-replica-log-performance-improvements"></a>저장소 복제본 로그 성능 향상

또한 향상 저장소 복제본 로그에서 복제를 추적 하는 방법에 복제 처리량 및 대기 시간, 모든 플래시 저장소 뿐만 아니라 서로 간에 복제 하는 저장소 공간 다이렉트 클러스터에서 특히 개선.

복제 그룹의 모든 멤버는 성능 향상된을 활용 하려면 Windows Server 2019을 실행 해야 합니다.

#### <a name="test-failover"></a>테스트 장애 조치(failover)

이제 일시적으로 테스트를 위해 대상 서버에서 복제 된 저장소의 스냅숏을 탑재 하거나 백업 목적으로 합니다. Microsoft 업데이트에 대한 자세한 내용은 [저장소 복제본 관련 질문과 대답](https://aka.ms/srfaq)을 참조하세요.

#### <a name="windows-admin-center-support"></a>Windows Admin Center 지원

복제의 그래픽 관리에 대 한 지원은 이제 사용할 수 있는 Windows Admin Center 서버 관리자 도구를 통해입니다. 복제 서버-투-서버, 클러스터 간 뿐만 아니라 확장 클러스터 복제 포함 됩니다.

#### <a name="miscellaneous-improvements"></a>기타 개선 사항

저장소 복제본에는 다음과 같은 개선 사항이 포함 됩니다.

-   자동 장애 조치 이제 발생할 수 있도록 변경 비동기 확장 클러스터 동작
-   여러 버그 수정

### <a name="smb"></a>SMB

- **SMB1 및 게스트 인증 제거**: Windows Server는 더 이상 기본적으로 SMB1 클라이언트와 서버를 설치합니다. 추가로 SMB2 이상의 게스트 인증 기능이 기본적으로 해제됩니다. 자세한 내용은 [SMBv1이 Windows 10, 버전 1709 및 Windows Server, 버전 1709에 기본적으로 설치되지 않음](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server)을 검토하세요. 

- **SMB2/SMB3 보안과 호환성**: 레거시 응용 프로그램에 대 한 SMB2 + oplock 해제 수 있을 뿐만 아니라 서명 또는 클라이언트에서 각 연결 단위로 암호화를 요구 하는 기능을 포함 하 여 보안 및 응용 프로그램 호환성에 대 한 옵션이 추가 되었습니다. 자세한 내용은 SMBShare PowerShell 모듈 도움말을 검토하세요.

### <a name="data-deduplication"></a>데이터 중복 제거

- **이제 데이터 중복 제거 지원 ReFS**: 더 이상 ReFS 사용 하 여 최신 파일 시스템의 장점 및 데이터 중복 제거 간에 선택 해야 합니다: 이제 ReFS를 설정할 수 없습니다. 어디서 나 데이터 중복 제거 활성화할 수 없습니다. ReFS를 통해 저장소 효율이 95% 증가합니다.
- **데이터 중복 제거 된 볼륨에 최적화 된 수신/송신 API**: 개발자 기술 자료 데이터 중복 제거 볼륨의 경우 서버 간에 데이터를 이동 하는 효율적으로 데이터를 저장 하는 방법에 대 한 및 클러스터를 효율적으로 활용을 사용할 수 있습니다.

### <a name="file-server-resource-manager"></a>파일 서버 리소스 관리자

Windows Server 2019 서비스를 시작 하면 모든 볼륨에서 파일 서버 리소스 관리자 서비스는 변경 저널 (USN 저널 라고도 함)를 만들지 못하게 방지 하는 기능을 포함 합니다. 이를 통해 각 볼륨의 공간을 절약할 수 있지만 실시간 파일 분류를 사용할 수 없게 됩니다. 자세한 내용은 [파일 서버 리소스 관리자 개요](fsrm/fsrm-overview.md)를 참조하십시오.

## <a name="whats-new-in-storage-in-windows-server-version-1803"></a>Windows Server, 버전 1803에서에서 저장소의 새로운 기능

### <a name="file-server-resource-manager"></a>파일 서버 리소스 관리자

Windows Server 버전 1803 포함 파일 서버 리소스 관리자 변경 저널 (USN 저널 라고도 함)를 만들지 못하게 방해할 수 모든 볼륨에 서비스를 시작 합니다. 이를 통해 각 볼륨의 공간을 절약할 수 있지만 실시간 파일 분류를 사용할 수 없게 됩니다. 자세한 내용은 [파일 서버 리소스 관리자 개요](fsrm/fsrm-overview.md)를 참조하십시오.

## <a name="whats-new-in-storage-in-windows-server-version-1709"></a>Windows Server 1709 버전 저장소의 새로운 기능

Windows Server 버전 1709 반기 채널의 첫 번째 Windows Server 릴리스에서 합니다. 반기 채널 Software Assurance 혜택 이며 6 개월 마다 새 버전으로 18 개월 동안 프로덕션 환경에서 완전히 지원 됩니다.

자세한 내용은 [Windows Server 반기 채널 개요](../get-started/semi-annual-channel-overview.md)를 참조하세요.

### <a name="storage-replica"></a>저장소 복제본

저장소 복제본에서 추가 재해 복구 보호는 이제 포함 하도록 확장 됩니다.

- **테스트 장애 조치**: 대상 저장소를 탑재하는 옵션이 이제 테스트 장애 조치 기능을 통해 이용 가능합니다. 테스트 및 백업을 목적으로 대상 노드에 있는 복제된 저장소의 스냅숏을 일시적으로 탑재할 수 있습니다. Microsoft 업데이트에 대한 자세한 내용은 [저장소 복제본 관련 질문과 대답](https://aka.ms/srfaq)을 참조하세요.
- **Windows Admin Center 지원**: 복제의 그래픽 관리에 대 한 지원은 이제 사용할 수 있는 Windows Admin Center 서버 관리자 도구를 통해입니다. 복제 서버-투-서버, 클러스터 간 뿐만 아니라 확장 클러스터 복제 포함 됩니다.

저장소 복제본에는 다음과 같은 개선 사항이 포함 됩니다.

-   자동 장애 조치 이제 발생할 수 있도록 변경 비동기 확장 클러스터 동작
-   여러 버그 수정

### <a name="smb"></a>SMB

- **SMB1 및 게스트 인증 제거**: Windows Server 버전 1709 이상 SMB1 클라이언트와 서버는 기본적으로 설치 합니다. 추가로 SMB2 이상의 게스트 인증 기능이 기본적으로 해제됩니다. 자세한 내용은 [SMBv1이 Windows 10, 버전 1709 및 Windows Server, 버전 1709에 기본적으로 설치되지 않음](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server)을 검토하세요. 

- **SMB2/SMB3 보안과 호환성**: 레거시 응용 프로그램에 대 한 SMB2 + oplock 해제 수 있을 뿐만 아니라 서명 또는 클라이언트에서 각 연결 단위로 암호화를 요구 하는 기능을 포함 하 여 보안 및 응용 프로그램 호환성에 대 한 옵션이 추가 되었습니다. 자세한 내용은 SMBShare PowerShell 모듈 도움말을 검토하세요.

### <a name="data-deduplication"></a>데이터 중복 제거

- **이제 데이터 중복 제거 지원 ReFS**: 더 이상 ReFS 사용 하 여 최신 파일 시스템의 장점 및 데이터 중복 제거 간에 선택 해야 합니다: 이제 ReFS를 설정할 수 없습니다. 어디서 나 데이터 중복 제거 활성화할 수 없습니다. ReFS를 통해 저장소 효율이 95% 증가합니다.
- **데이터 중복 제거 된 볼륨에 최적화 된 수신/송신 API**: 개발자 기술 자료 데이터 중복 제거 볼륨의 경우 서버 간에 데이터를 이동 하는 효율적으로 데이터를 저장 하는 방법에 대 한 및 클러스터를 효율적으로 활용을 사용할 수 있습니다.

## <a name="whats-new-in-storage-in-windows-server-2016"></a>Windows Server 2016에서 제공되는 저장소의 새로운 기능

### <a name="s2d"></a>저장소 공간 다이렉트  
저장소 공간 다이렉트는 로컬 저장소가 있는 서버를 사용하여 확장 가능한 고가용성 저장소를 구축하도록 지원합니다. 이는 소프트웨어 정의 저장소 시스템의 배포 및 관리를 간소화하고 SATA SSD 및 NVMe 디스크 장치와 같이 이전에 공유 디스크를 사용하는 클러스터형 저장소 공간에서는 불가능했던 새로운 등급의 디스크 장치를 사용합니다.  

**이와 같은 변경을 통해 더해지는 가치**  
저장소 공간 다이렉트는 서비스 공급자와 기업이 로컬 저장소가 있는 산업 표준 서버를 사용하여 확장 가능한 고가용성 소프트웨어 정의 저장소를 구축할 수 있도록 지원합니다. 로컬 저장소가 있는 서버를 사용하면 복잡성이 감소하고, 확장성이 증가하며, SATA SSD와 같은 이전에 사용할 수 없었던 저장 장치를 사용하여 플래시 저장소 또는 NVMe SSD의 비용을 절감하고 성능을 개선할 수 있습니다.  

저장소 공간 다이렉트를 사용하면 공유 SAS 패브릭이 필요 없으므로 배포 및 구성이 간소화됩니다. 대신 빠르고 대기 시간이 낮은 CPU 효율적인 저장소에 SMB3 및 SMB 다이렉트(RDMA)를 활용함으로써 네트워크를 저장소 패브릭으로 사용합니다. 규모를 확장하려면 서버를 추가하여 저장소 용량 및 I/O 성능을 높이기만 하면 됩니다.  
자세한 내용은 [Windows Server 2016의 저장소 공간 다이렉트](storage-spaces/storage-spaces-direct-overview.md)를 참조하세요.  

**달라진 기능**  
이 기능은 Windows Server 2016의 새로운 기능입니다.  

### <a name="storage-replica"></a>저장소 복제본

저장소 복제본을 통해 사이트 간에 장애 조치(failover) 클러스터를 확장할 뿐만 아니라 재해 복구를 위해 서버 또는 클러스터 간에 저장소에 상관없는 블록 수준의 동기 복제를 사용할 수 있습니다. 동기 복제를 사용하면 파일 시스템 수준에서 데이터가 손실되지 않고 크래시 일관성이 있는 볼륨을 사용하여 실제 사이트의 데이터를 미러링할 수 있습니다. 비동기 복제는 대도시 범위를 넘어 사이트를 확장합니다(데이터가 손실될 수도 있음).  

**이와 같은 변경을 통해 더해지는 가치**  
저장소 복제를 사용하면 다음을 수행할 수 있습니다.  

* 중요 업무용 워크로드의 계획된 중단 및 계획되지 않은 중단을 위한 단일 공급업체 재해 복구 솔루션을 제공합니다.
* 안정성, 확장성 및 성능이 검증된 SMB3 전송을 사용합니다.
* 대도시 거리로 Windows 장애 조치(failover) 클러스터를 확장합니다.
* 저장소 및 클러스터링에 Hyper-V, 저장소 복제본, 저장소 공간, 클러스터, 스케일 아웃 파일 서버, SMB3, 중복 제거 및 ReFS/NTFS와 같은 종단 간 Microsoft 소프트웨어를 사용합니다.
* 다음과 같이 비용 및 복잡성을 줄입니다. 
    * 하드웨어 제약이 없으므로 DAS 또는 SAN과 같은 특정 저장소 구성에 대한 요구 사항이 없습니다.
    * 상용 저장소 및 네트워킹 기술을 허용합니다.
    * 장애 조치(Failover) 클러스터 관리자를 통해 개별 노드 및 클러스터에 대한 그래픽 관리가 용이합니다.
    * Windows PowerShell을 통한 포괄적인 대규모 스크립팅 옵션을 포함합니다. 
* 가동 중지 시간을 줄이고, Windows의 고유한 안정성 및 생산성을 높입니다.  
* 지원 가능성, 성능 메트릭 및 진단 기능을 제공합니다.  

자세한 내용은 [Windows Server 2016의 저장소 복제본](storage-replica/storage-replica-overview.md)을 참조하세요.  

**달라진 기능**  
이 기능은 Windows Server 2016의 새로운 기능입니다.  

### <a name="storage-qos"></a>저장소 서비스 품질  
이제 저장소 QoS(서비스 품질)를 사용하여 중앙에서 종단 간 저장소 성능을 모니터링하고 Windows Server 2016의 Hyper-V 및 CSV 클러스터를 통해 관리 정책을 만들 수 있습니다.  

**이와 같은 변경을 통해 더해지는 가치**  
이제 CSV 클러스터에서 저장소 QoS 정책을 만들고 Hyper-V 가상 컴퓨터에서 하나 이상의 가상 디스크에 할당할 수 있습니다. 워크로드와 저장소 로드 변동에 따라 정책을 준수하도록 저장소 성능이 자동으로 재조정됩니다.  

* 각 정책은 가상 하드 디스크, 단일 가상 컴퓨터 또는 가상 컴퓨터 그룹, 서비스, 테넌트 등 데이터 흐름 모음에 적용할 예약(최소값) 및/또는 제한(최대값)을 지정할 수 있습니다.  
* Windows PowerShell 또는 WMI를 사용하여 다음 작업을 수행할 수 있습니다.  
    * CSV 클러스터에서 정책을 만듭니다.
    * CSV 클러스터에서 사용할 수 있는 정책을 열거합니다.
    * Hyper-V 가상 컴퓨터의 가상 하드 디스크에 정책을 할당합니다. 
    * 각 흐름의 성능 및 정책 내 상태를 모니터링합니다.  
* 여러 가상 하드 디스크에서 동일한 정책을 공유하는 경우 정책 최소값 및 최대값 설정 내에서 수요를 충족하도록 성능이 고르게 분산됩니다. 따라서 정책을 사용하여 하나의 가상 하드 디스크, 하나의 가상 컴퓨터, 서비스를 구성하는 여러 가상 컴퓨터 또는 한 테넌트가 소유한 모든 가상 컴퓨터를 관리할 수 있습니다.  

**달라진 기능**  
이 기능은 Windows Server 2016의 새로운 기능입니다. 최소 예약 관리, 단일 명령을 통한 클러스터 전반의 모든 가상 디스크의 흐름 모니터링 및 중앙 집중식 정책 기반 관리는 이전 버전의 Windows Server에서는 불가능했습니다.  

자세한 내용은 [저장소 서비스 품질](storage-qos/storage-qos-overview.md)을 참조하세요.

### <a name="dedup"></a>데이터 중복 제거  
| 기능 | 새로운 기능 또는 업데이트된 기능 | 설명 |
|---------------|----------------|-------------|
| [대규모 볼륨 지원](data-deduplication/whats-new.md#large-volume-support) | 업데이트됨 | Windows Server 2016 이전에는 특별히 예상되는 변동에 대비해 볼륨의 크기를 조정해야 했으며, 10TB가 넘는 볼륨은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서는 데이터 중복 제거 기능이 **최대 64TB**의 볼륨 크기를 지원합니다. |
| [대용량 파일 지원](data-deduplication/whats-new.md#large-file-support) | 업데이트됨 | Windows Server 2016 이전에는 크기가 1TB에 가까운 파일은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서 **최대 1TB**의 파일이 완벽하게 지원됩니다. |
| [Nano Server에 대 한 지원](data-deduplication/whats-new.md#nano-server-support) | 단추를 사용하여 새 | 데이터 중복 제거는 Windows Server 2016의 새로운 Nano Server 배포 옵션에서 사용할 수 있으며 완전히 지원됩니다. |
| [간소화 된 백업 지원](data-deduplication/whats-new.md#simple-backup-support) | 단추를 사용하여 새 | Windows Server 2012 R2에서는 Microsoft의 [Data Protection Manager](https://technet.microsoft.com/library/hh758173.aspx)와 같은 가상화된 백업 응용 프로그램이 일련의 수동 구성 단계를 통해 지원되었습니다. Windows Server 2016에서는 가상화된 백업 응용 프로그램에 대한 중복 제거의 원활한 배포를 위해 새로운 기본 사용 유형인 "백업"이 추가되었습니다. |
| [클러스터 OS 롤링 업그레이드 지원](data-deduplication/whats-new.md#cluster-upgrade-support) | 단추를 사용하여 새 | 데이터 중복 제거는 Windows Server 2016의 [클러스터 OS 롤링 업그레이드](..//failover-clustering/cluster-operating-system-rolling-upgrade.md) 기능을 완전히 지원합니다. |

### <a name="smb-hardening-improvements"></a>SYSVOL 및 NETLOGON 연결에 대 한 향상 된 SMB 강화  
Active Directory 도메인 서비스에 연결된 Windows 10 및 Windows Server 2016 클라이언트에서는 도메인 컨트롤러의 기본 SYSVOL 및 NETLOGON 공유에 SMB 서명 및 상호 인증(예: Kerberos)이 필요합니다.   

**이와 같은 변경을 통해 더해지는 가치**  
이 변경으로 메시지 가로채기 공격의 가능성이 줄어듭니다.   

**달라진 기능**  
SMB 서명 및 상호 인증을 사용할 수 없는 경우 Windows 10 또는 Windows Server 2016 컴퓨터는 도메인 기반 그룹 정책 및 스크립트를 처리하지 않습니다.  

> [!NOTE]  
> 이러한 설정에 대한 레지스트리 값은 기본적으로 존재하지 않지만 그룹 정책 또는 다른 레지스트리 값으로 재정의될 때까지 강화 규칙은 계속 적용됩니다.  

이러한 향상 된 보안 기능-에 대 한 자세한 내용은 라고도 UNC 강화 라고도 Microsoft 기술 자료 문서를 참조 하세요 [3000483](https://support.microsoft.com/kb/3000483) 고 [MS15 011 & MS15 014: 보안 강화 그룹 정책](https://blogs.technet.microsoft.com/srd/2015/02/10/ms15-011-ms15-014-hardening-group-policy)합니다.  

### <a name="work-folders"></a>클라우드 폴더
향상 된 변경 알림 작업 폴더 서버가 Windows Server 2016 및 작업 폴더 클라이언트가 실행 중인 경우에 Windows 10입니다.

**이와 같은 변경을 통해 더해지는 가치**<br>
Windows Server 2012 R2의 경우 파일 변경을 작업 폴더 서버와 동기화하면 클라이언트는 해당 변경에 대해 알리지 않고 업데이트될 때까지 최대 10분을 기다립니다.  Windows Server 2016을 사용 하는 경우 작업 폴더 서버가 즉시 Windows 10 클라이언트 알리고 파일 변경 내용이 즉시 동기화 합니다.

**달라진 기능**<br>
이 기능은 Windows Server 2016의 새로운 기능입니다. 이 기능을 사용하려면 Windows Server 2016 작업 폴더 서버 및 클라이언트가 Windows 10이어야 합니다.

이전 클라이언트를 사용하거나 클라우드 폴더 서버가 Windows Server 2012 R2인 경우 클라이언트가 10분마다 변경 내용을 계속 폴링합니다.

### <a name="refs"></a>ReFS 
ReFS가 다음 번 반복으로 대규모 저장소 배포에 대하여 다양한 작업을 지원하며 데이터의 안정성, 복원력, 확장성을 제공합니다.     

**이와 같은 변경을 통해 더해지는 가치**<br>
ReFS로 향상되는 기능은 다음과 같습니다.

* ReFS는 새로운 저장소 계층 기능을 구현하여 성능을 향상시키고 저장소 용량을 늘립니다. 새로운 기능의 이점은 다음과 같습니다.
    * 동일한 가상 디스크에 여러 복원력 유형 포함(예: 성능 계층에서 미러링, 용량 계층에서 패리티 사용)
    * 유동적인 작업 집합에 대한 응답성 향상  
* 블록 복제를 도입하면 .vhdx 검사점 병합 작업과 같은 VM 작업의 성능이 크게 향상됩니다.
* 새로운 ReFS 검사 도구를 이용하면 유출된 저장소의 복구가 가능하며 치명적인 손상으로부터 데이터를 복구하는 데 도움이 됩니다. 

**달라진 기능**<br>
Windows Server 2016에서 처음으로 제공하는 기능입니다. 

## <a name="see-also"></a>참조  
* [Windows Server 2016의 새로운 기능](../get-started/what-s-new-in-windows-server-2016.md)  
