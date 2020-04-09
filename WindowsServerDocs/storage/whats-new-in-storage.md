---
ms.assetid: 0f2a7f7b-aca8-4e5d-ad67-4258e88bc52f
title: Windows Server에서 제공되는 저장소의 새로운 기능
ms.prod: windows-server
ms.author: jgerend
manager: dongill
ms.technology: storage
ms.topic: article
author: jasongerend
ms.date: 05/29/2019
ms.openlocfilehash: 0de83c8642629b3a7ff21c9accadec5f9331178e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80820856"
---
# <a name="whats-new-in-storage-in-windows-server"></a>Windows Server에서 제공 되는 저장소의 새로운 기능

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server(반기 채널)

이 항목에서는 Windows Server 2019, Windows Server 2016 및 Windows Server 반기 채널 릴리스 저장소의 새로운 기능 및 변경 된 기능에 대해 설명 합니다.

## <a name="whats-new-in-storage-in-windows-server-version-1903"></a>Windows Server에서 제공 되는 저장소의 새로운 기능 버전 1903

이 Windows Server 릴리스에는 다음과 같은 변경 내용과 기술이 추가 되었습니다.

### <a name="storage-migration-service-now-migrates-local-accounts-clusters-and-linux-servers"></a>스토리지 마이그레이션 서비스로 로컬 계정, 클러스터 및 Linux 서버 마이그레이션 가능

스토리지 마이그레이션 서비스를 사용하면 서버를 Windows Server의 최신 버전으로 쉽게 마이그레이션할 수 있습니다. 서버의 데이터를 조사한 다음, 데이터 및 구성을 새로운 서버로 전송하는 그래픽 도구가 제공됩니다. 앱이나 사용자가 아무것도 변경할 필요가 없습니다.

이 버전의 Windows Server를 사용하여 마이그레이션을 오케스트레이션하는 경우, 다음과 같은 기능이 추가됩니다.

- 새 서버로 로컬 사용자 및 그룹 마이그레이션
- 장애 조치 (failover) 클러스터에서 스토리지 마이그레이션
- 삼바를 사용하는 Linux 서버에서 스토리지 마이그레이션
- Azure 파일 동기화를 사용하여 마이그레이션된 공유를 Azure에 쉽게 동기화
- Azure와 같은 신규 네트워크로 마이그레이션

스토리지 마이그레이션 서비스에 대한 자세한 내용은 [스토리지 마이그레이션 서비스 개요](storage-migration-service/overview.md)를 참조하세요.

### <a name="system-insights-disk-anomaly-detection"></a>시스템 인사이트 디스크 이상 탐지

[시스템 인사이트](../manage/system-insights/overview.md)는 Windows Server 시스템 데이터를 로컬에서 분석하고 서버의 기능에 대한 인사이트를 제공하는 예측 분석 기능입니다. 여기에는 여러 가지 기본 제공 기능이 있지만 Windows Admin Center를 통해 디스크 이상 탐지를 비롯한 추가 기능을 설치할 수 있는 기능이 추가되었습니다.

디스크 이상 탐지는 디스크가 평소와 다르게 작동할 때 강조 표시하는 새로운 기능입니다. 다르게 작동한다고 꼭 나쁜 것은 아니지만, 비정상적인 순간을 보면 시스템 문제를 해결할 때 도움이 될 수 있습니다.

이 기능은 Windows Server 2019를 실행하는 서버에서도 사용할 수 있습니다.

### <a name="windows-admin-center-enhancements"></a>Windows Admin Center 고급 기능

Windows Admin Center의 새로운 릴리스가 출시되면서 Windows Server에 새로운 기능이 추가되었습니다. 최신 기능에 대한 자세한 내용은 [Windows Admin Center](../manage/windows-admin-center/understand/windows-admin-center.md)를 참조하세요.

## <a name="whats-new-in-storage-in-windows-server-2019-and-windows-server-version-1809"></a>Windows Server 2019 및 Windows Server, 버전 1809에서 제공 되는 저장소의 새로운 기능

이 Windows Server 릴리스에는 다음과 같은 변경 내용과 기술이 추가 되었습니다.

### <a name="manage-storage-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 저장소 관리

[Windows 관리 센터](../manage/windows-admin-center/overview.md) 는 서버, 클러스터, 스토리지 공간 다이렉트 및 Windows 10 pc를 사용 하는 하이퍼 수렴 형 인프라를 관리 하기 위해 로컬로 배포 된 새로운 브라우저 기반 앱입니다. Windows 외에 추가 비용이 발생 하지 않으며 프로덕션에 사용할 준비가 되었습니다.

Windows 관리 센터는 windows Server 2019 및 다른 버전의 Windows에서 실행 되는 별도의 다운로드 이지만 새로운 기능으로 서,이를 놓치지 않으려고 합니다.

### <a name="storage-migration-service"></a>저장소 마이그레이션 서비스

저장소 마이그레이션 서비스는 서버를 Windows Server의 최신 버전으로 쉽게 마이그레이션할 수 있는 새로운 기술입니다. 서버의 데이터를 인벤토리화하는 그래픽 도구를 제공하며, 데이터 및 구성을 최신 서버로 전송한 다음, 선택적으로 이전 서버의 ID를 새로운 서버로 이동하여 앱 및 사용자가 아무 것도 변경할 필요가 없도록 합니다. 자세한 내용은 [스토리지 마이그레이션 서비스](storage-migration-service/overview.md)를 참조하세요.

### <a name="storage-spaces-direct-windows-server-2019-only"></a><a id="storage-spaces-direct"></a>스토리지 공간 다이렉트 (Windows Server 2019에만 해당)

Windows Server 2019에는 다양 한 스토리지 공간 다이렉트 향상 된 기능이 있습니다 (스토리지 공간 다이렉트 Windows Server, 반기 채널에는 포함 되어 있지 않음).

- **ReFS 볼륨에 대한 중복 제거 및 압축**

    ReFS 파일 시스템에 대 한 중복 제거 및 압축을 사용 하 여 동일한 볼륨에 최대 10 배 더 많은 데이터를 저장 합니다. (Windows 관리 센터를 사용 하 여 설정 하는 [한 번만 클릭 하면](https://www.youtube.com/watch?v=PRibTacyKko&feature=youtu.be) 됩니다.) 선택적인 압축을 사용 하는 가변 크기 청크 저장소는 절약 률을 최대화 하 고, 다중 스레드 후 처리 아키텍처는 성능 영향을 최소화 합니다. 는 최대 64 TB의 볼륨을 지원 하 고 각 파일의 첫 4 TB를 중복 제거 합니다.

- **영구 메모리에 대한 기본 지원**

    Intel® Optane™ DC PM 및 NVDIMM-N을 포함한 영구 메모리 모듈에 대한 기본 저장소 공간 다이렉트 지원으로 전례가 없는 수준으로 성능이 개선됩니다. 영구 메모리를 캐시로 사용하여 활성 작업 집합을 가속하거나 용량으로 사용하여 마이크로초 단위의 낮은 대기 시간을 일관적으로 보장합니다. PowerShell 또는 Windows Admin Center에서 다른 드라이브와 마찬가지로 영구 메모리를 관리합니다.

- **에지에서 2개 노드 하이퍼 컨버지드 인프라에 대한 중첩된 복원력**

    RAID 5+1에서 영감을 얻은 새로운 소프트웨어 복원력 옵션을 통해 두 가지 하드웨어 오류를 한 번에 해결합니다. 중첩된 복원력을 사용하여 2-노드 저장소 공간 다이렉트 클러스터는 하나의 서버 노드가 중단되고 드라이브가 다른 서버 노드에서 오류가 발생하는 경우에도 앱 및 가상 컴퓨터에 대해 지속적으로 액세스 가능한 저장소를 제공할 수 있습니다.

- **USB 플래시 드라이브를 감시로 사용하는 2개 서버 클러스터**

    라우터에 연결 된 저렴 한 USB 플래시 드라이브를 사용 하 여 두 서버 클러스터에서 미러링 모니터 서버로 작동 합니다. 서버 작동이 중단 되 고 백업 되 면 USB 드라이브 클러스터에서 최신 데이터가 있는 서버를 알 수 있습니다. 자세한 내용은 [Microsoft 블로그에서 저장소](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/)를 참조 하세요.

- **Windows Admin Center**

    Windows Admin Center의 [전용 대시보드](../manage/windows-admin-center/use/manage-hyper-converged.md) 및 환경을 통해 저장소 공간 다이렉트를 관리 및 모니터링합니다. 클릭 몇 번으로 볼륨 만들기, 열기, 확장 또는 삭제가 가능합니다. 전체 클러스터부터 개별 SSD 또는 HDD의 IOPS 및 IO 대기 시간과 같은 성능을 모니터링합니다. Windows Server 2016 및 Windows Server 2019의 경우 추가 비용 없이 사용 가능합니다.

- **성능 기록**

    [기본 제공 기록](storage-spaces/performance-history.md)을 통해 리소스 사용률 및 성능을 간편하게 확인합니다. 컴퓨팅, 메모리, 네트워크 및 저장소에 걸친 50개 이상의 필수 카운터가 자동으로 수집되어 클러스터에 최대 1년 동안 저장됩니다. 무엇 보다도, 설치, 구성 또는 시작할 필요가 없습니다. Windows Admin Center에서 시각화하거나 PowerShell에서 쿼리 및 처리합니다.

- **클러스터당 최대 4PB까지 확장**

    몇 페타바이트까지 확장이 가능해 미디어, 백업 및 보관 사용 사례에 적합합니다. Windows Server 2019에서 저장소 공간 다이렉트는 최대 4PB(페타바이트)를 지원합니다. 4PB는 저장소 풀당 4,000 테라바이트의 원시 용량입니다. 관련 용량 지침 또한 증가했습니다. 예를 들어 전보다 2배 더 많은 볼륨(32개 대신 64개)과 볼륨당 용량(32TB 대신 64TB)을 확보할 수 있습니다. 하나의 저장소 네임 스페이스 내에서 훨씬 더 큰 규모를 위해 여러 클러스터를 [클러스터 집합](storage-spaces/cluster-sets.md) 에 연결 합니다. 자세한 내용은 [Microsoft 블로그에서 저장소](https://blogs.technet.microsoft.com/filecab/2018/06/27/windows-server-summit-recap/)를 참조 하세요.

- **2배 빠른 미러 가속 패리티**

    미러-가속 패리티를 사용하여 부분 미러 및 부분 패리티 저장소 공간 다이렉트 볼륨(예: RAID-1과 RAID-5/6의 혼합)을 만들어 두 가지 모두 사용할 수 있습니다. Windows 관리 센터에서 [생각 하는 것 보다 쉽습니다](https://www.youtube.com/watch?v=R72QHudqWpE) . Windows Server 2019에서 미러 가속 패리티의 성능은 최적화 덕분에 Windows Server 2016에 비해 두 배가 넘습니다.

- **드라이브 대기 시간 아웃라이어 감지**

    자동 관리 모니터링 및 기본 제공 이상 값 검색을 사용 하 여 비정상적인 대기 시간으로 드라이브를 쉽게 식별 하 고 Microsoft Azure의 장기적이 고 성공적인 접근 방식으로 아이디어를 제공 합니다. 평균 대기 시간 또는이에 해당 하는 99 번째 백분위 수와 같은 다소 미묘한 지에 대 한 짧은 드라이브는 PowerShell에서 자동으로 레이블이 지정 되 고 Windows 관리 센터에는 ' 비정상적인 대기 시간 ' 상태가 됩니다.

- **내결함성을 강화하기 위해 수동으로 볼륨의 할당을 구분**

    이를 통해 관리자는 스토리지 공간 다이렉트 볼륨의 할당을 수동으로 구분할 수 있습니다. 이렇게 하면 특정 조건에 따라 내결함성이 크게 향상 되지만 몇 가지 추가 관리 고려 사항과 복잡성이 적용 됩니다. 자세한 내용은 [볼륨의 할당을 구분 하는](storage-spaces/delimit-volume-allocation.md)방법을 참조 하세요.

### <a name="storage-replica"></a><a name="storage-replica2019"></a>저장소 복제본

이 릴리스에서는 [저장소 복제본](storage-replica/storage-replica-overview.md) 에 대 한 몇 가지 향상 된 기능이 있습니다.

#### <a name="storage-replica-in-windows-server-standard-edition"></a>Windows Server Standard Edition의 저장소 복제본

이제 Datacenter Edition 외에도 Windows Server, Standard Edition에서 저장소 복제본을 사용할 수 있습니다. Windows Server Standard Edition에서 실행 되는 저장소 복제본에는 다음과 같은 제한 사항이 있습니다.

- 저장소 복제본은 볼륨 수를 제한 없이 단일 볼륨을 복제 합니다.
- 볼륨 크기는 무제한이 아니라 최대 2tb입니다.

#### <a name="storage-replica-log-performance-improvements"></a>저장소 복제본 로그 성능 향상

또한 저장소 복제본 로그가 복제를 추적 하 여 복제 처리량과 대기 시간을 개선 하 고, 특히 모든 플래시 저장소에서 서로 복제 하는 스토리지 공간 다이렉트 클러스터를 개선 했습니다.

향상 된 성능을 얻으려면 복제 그룹의 모든 구성원이 Windows Server 2019를 실행 해야 합니다.

#### <a name="test-failover"></a>테스트 장애 조치(failover)

이제 테스트 또는 백업을 위해 대상 서버에서 복제 된 저장소의 스냅숏을 일시적으로 탑재할 수 있습니다. 자세한 내용은 [스토리지 복제본에 대한 질문과 대답](https://aka.ms/srfaq)을 참조하세요.

#### <a name="windows-admin-center-support"></a>Windows Admin Center 지원

이제 서버 관리자 도구를 통해 Windows 관리 센터에서 복제의 그래픽 관리를 지원할 수 있습니다. 서버 간 복제, 클러스터 간 복제 및 확장 클러스터 복제도 포함 됩니다.

#### <a name="miscellaneous-improvements"></a>기타 개선 사항

저장소 복제본에는 다음과 같은 향상 된 기능도 포함 되어 있습니다.

-   자동 장애 조치 (failover)가 발생 하도록 비동기 확장 클러스터 동작을 변경 합니다.
-   여러 버그 수정

### <a name="smb"></a>SMB

- **Smb1 및 게스트 인증 제거**: Windows Server는 기본적으로 SMB1 클라이언트 및 서버를 더 이상 설치 하지 않습니다. 추가로 SMB2 이상의 게스트 인증 기능이 기본적으로 해제됩니다. 자세한 내용은 [SMBv1이 Windows 10, 버전 1709 및 Windows Server, 버전 1709에 기본적으로 설치되지 않음](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server)을 검토하세요. 

- **SMB2/SMB3 보안 및 호환성**: 클라이언트로부터 연결당 기본 서명 필요 또는 암호화는 물론 레거시 응용 프로그램을 위한 SMB2+의 oplock을 사용하지 않도록 설정하는 기능을 포함한 보안 및 응용 프로그램 호환성을 위한 추가 옵션이 추가되었습니다. 자세한 내용은 SMBShare PowerShell 모듈 도움말을 검토하세요.

### <a name="data-deduplication"></a>데이터 중복 제거

- **데이터 중복 제거가 이제 ReFS에서 지원**: 더 이상 ReFS가 포함된 최신 파일 시스템의 이점과 데이터 중복 제거 사이에서 선택해야 할 필요가 없습니다. 이제 ReFS를 사용하도록 설정할 수 있는 곳 어디에서나 데이터 중복 제거를 사용하도록 설정할 수 있습니다. ReFS를 통해 저장소 효율이 95% 증가합니다.
- **중복 제거된 볼륨으로의 최적화된 송/수신을 위한 DataPort API**: 이제 개발자는 데이터를 효율적으로 저장하여 볼륨, 서버 및 클러스터 사이에서 데이터를 효율적으로 이동하는 방법에 관한 데이터 중복 제거의 지식을 활용할 수 있습니다.

### <a name="file-server-resource-manager"></a>파일 서버 리소스 관리자

Windows Server 2019에는 서비스가 시작 될 때 파일 서버 리소스 관리자 서비스에서 모든 볼륨에 변경 저널 (USN 저널이 라고도 함)을 만들 수 없도록 하는 기능이 포함 되어 있습니다. 이를 통해 각 볼륨의 공간을 절약할 수 있지만 실시간 파일 분류를 사용할 수 없게 됩니다. 자세한 내용은 [파일 서버 리소스 관리자 개요](fsrm/fsrm-overview.md)를 참조하세요.

## <a name="whats-new-in-storage-in-windows-server-version-1803"></a>Windows Server에서 제공 되는 저장소의 새로운 기능 버전 1803

### <a name="file-server-resource-manager"></a>파일 서버 리소스 관리자

Windows Server, 버전 1803에는 서비스가 시작 될 때 파일 서버 리소스 관리자 서비스에서 모든 볼륨에 변경 저널 (USN 저널이 라고도 함)을 만들 수 없도록 하는 기능이 포함 되어 있습니다. 이를 통해 각 볼륨의 공간을 절약할 수 있지만 실시간 파일 분류를 사용할 수 없게 됩니다. 자세한 내용은 [파일 서버 리소스 관리자 개요](fsrm/fsrm-overview.md)를 참조하세요.

## <a name="whats-new-in-storage-in-windows-server-version-1709"></a>Windows Server에서 제공 되는 저장소의 새로운 기능 버전 1709

Windows Server, 버전 1709은 반기 채널의 첫 번째 Windows Server 릴리스입니다. 반기 채널은 소프트웨어 보증 혜택 이며, 6 개월 마다 새 버전을 사용 하 여 18 개월 동안 프로덕션 환경에서 완벽 하 게 지원 됩니다.

자세한 내용은 [Windows Server 반기 채널 개요](../get-started/semi-annual-channel-overview.md)를 참조하세요.

### <a name="storage-replica"></a>저장소 복제본

저장소 복제본을 통해 추가 된 재해 복구 보호는 이제 다음을 포함 하도록 확장 됩니다.

- **테스트 장애 조치**: 대상 스토리지를 탑재하는 옵션이 이제 테스트 장애 조치 기능을 통해 이용 가능합니다. 테스트 및 백업을 목적으로 대상 노드에 있는 복제된 저장소의 스냅숏을 일시적으로 탑재할 수 있습니다. 자세한 내용은 [스토리지 복제본에 대한 질문과 대답](https://aka.ms/srfaq)을 참조하세요.
- **Windows 관리 센터 지원**: 이제 서버 관리자 도구를 통해 Windows 관리 센터에서 복제에 대 한 그래픽 관리 지원을 사용할 수 있습니다. 서버 간 복제, 클러스터 간 복제 및 확장 클러스터 복제도 포함 됩니다.

저장소 복제본에는 다음과 같은 향상 된 기능도 포함 되어 있습니다.

-   자동 장애 조치 (failover)가 발생 하도록 비동기 확장 클러스터 동작을 변경 합니다.
-   여러 버그 수정

### <a name="smb"></a>SMB

- **SMB1 및 게스트 인증 제거**: Windows Server, 버전 1709에서는 더 이상 SMB1 클라이언트 및 서버를 기본적으로 설치하지 않습니다. 추가로 SMB2 이상의 게스트 인증 기능이 기본적으로 해제됩니다. 자세한 내용은 [SMBv1이 Windows 10, 버전 1709 및 Windows Server, 버전 1709에 기본적으로 설치되지 않음](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows-10-rs3-and-windows-server)을 검토하세요. 

- **SMB2/SMB3 보안 및 호환성**: 클라이언트로부터 연결당 기본 서명 필요 또는 암호화는 물론 레거시 응용 프로그램을 위한 SMB2+의 oplock을 사용하지 않도록 설정하는 기능을 포함한 보안 및 응용 프로그램 호환성을 위한 추가 옵션이 추가되었습니다. 자세한 내용은 SMBShare PowerShell 모듈 도움말을 검토하세요.

### <a name="data-deduplication"></a>데이터 중복 제거

- **데이터 중복 제거가 이제 ReFS에서 지원**: 더 이상 ReFS가 포함된 최신 파일 시스템의 이점과 데이터 중복 제거 사이에서 선택해야 할 필요가 없습니다. 이제 ReFS를 사용하도록 설정할 수 있는 곳 어디에서나 데이터 중복 제거를 사용하도록 설정할 수 있습니다. ReFS를 통해 저장소 효율이 95% 증가합니다.
- **중복 제거된 볼륨으로의 최적화된 송/수신을 위한 DataPort API**: 이제 개발자는 데이터를 효율적으로 저장하여 볼륨, 서버 및 클러스터 사이에서 데이터를 효율적으로 이동하는 방법에 관한 데이터 중복 제거의 지식을 활용할 수 있습니다.

## <a name="whats-new-in-storage-in-windows-server-2016"></a>Windows Server 2016에서 제공되는 저장소의 새로운 기능

### <a name="storage-spaces-direct"></a><a name="s2d"></a>스토리지 공간 다이렉트  
저장소 공간 다이렉트는 로컬 저장소가 있는 서버를 사용하여 확장 가능한 고가용성 저장소를 구축하도록 지원합니다. 이는 소프트웨어 정의 저장소 시스템의 배포 및 관리를 간소화하고 SATA SSD 및 NVMe 디스크 장치와 같이 이전에 공유 디스크를 사용하는 클러스터형 저장소 공간에서는 불가능했던 새로운 등급의 디스크 장치를 사용합니다.  

**이와 같은 변경을 통해 더해지는 가치**  
저장소 공간 다이렉트는 서비스 공급자와 기업이 로컬 저장소가 있는 산업 표준 서버를 사용하여 확장 가능한 고가용성 소프트웨어 정의 저장소를 구축할 수 있도록 지원합니다. 로컬 저장소가 있는 서버를 사용하면 복잡성이 감소하고, 확장성이 증가하며, SATA SSD와 같은 이전에 사용할 수 없었던 저장 장치를 사용하여 플래시 저장소 또는 NVMe SSD의 비용을 절감하고 성능을 개선할 수 있습니다.  

저장소 공간 다이렉트를 사용하면 공유 SAS 패브릭이 필요 없으므로 배포 및 구성이 간소화됩니다. 대신 빠르고 대기 시간이 낮은 CPU 효율적인 저장소에 SMB3 및 SMB 다이렉트(RDMA)를 활용함으로써 네트워크를 저장소 패브릭으로 사용합니다. 규모를 확장하려면 서버를 추가하여 저장소 용량 및 I/O 성능을 높이기만 하면 됩니다.  
자세한 내용은 [Windows Server 2016의 저장소 공간 다이렉트](storage-spaces/storage-spaces-direct-overview.md)를 참조하세요.  

**달라진 기능**  
이 기능은 Windows Server 2016의 새로운 기능입니다.  

### <a name="storage-replica"></a><a name="storage-replica"></a>저장소 복제본

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

### <a name="storage-quality-of-service"></a><a name="storage-qos"></a>저장소 서비스 품질  
이제 스토리지 QoS(서비스 품질)를 사용하여 중앙에서 엔드투엔드 스토리지 성능을 모니터링하고 Windows Server 2016의 Hyper-V 및 CSV 클러스터를 통해 관리 정책을 만들 수 있습니다.  

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

### <a name="data-deduplication"></a><a name="dedup"></a>데이터 중복 제거  
| 기능 | 새로운 기능 또는 업데이트된 기능 | 설명 |
|---------------|----------------|-------------|
| [대용량 볼륨에 대 한 지원](data-deduplication/whats-new.md#large-volume-support) | 업데이트됨 | Windows Server 2016 이전에는 특별히 예상되는 변동에 대비해 볼륨의 크기를 조정해야 했으며, 10TB가 넘는 볼륨은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서는 데이터 중복 제거 기능이 **최대 64TB**의 볼륨 크기를 지원합니다. |
| [큰 파일 보고서에 대 한 지원](data-deduplication/whats-new.md#large-file-support) | 업데이트됨 | Windows Server 2016 이전에는 크기가 1TB에 가까운 파일은 중복 제거에 적합하지 않았습니다. Windows Server 2016에서 **최대 1TB**의 파일이 완벽하게 지원됩니다. |
| [Nano Server에 대 한 지원](data-deduplication/whats-new.md#nano-server-support) | 새로 만들기 | 데이터 중복 제거는 Windows Server 2016의 새로운 Nano Server 배포 옵션에서 사용할 수 있으며 완전히 지원됩니다. |
| [간소화 된 백업 지원](data-deduplication/whats-new.md#simple-backup-support) | 새로 만들기 | Windows Server 2012 R2에서는 Microsoft의 [Data Protection Manager](https://technet.microsoft.com/library/hh758173.aspx)와 같은 가상화된 백업 응용 프로그램이 일련의 수동 구성 단계를 통해 지원되었습니다. Windows Server 2016에서는 가상화된 백업 응용 프로그램에 대한 중복 제거의 원활한 배포를 위해 새로운 기본 사용 유형인 "백업"이 추가되었습니다. |
| [클러스터 OS 롤링 업그레이드 지원](data-deduplication/whats-new.md#cluster-upgrade-support) | 새로 만들기 | 데이터 중복 제거는 Windows Server 2016의 [클러스터 OS 롤링 업그레이드](..//failover-clustering/cluster-operating-system-rolling-upgrade.md) 기능을 완전히 지원합니다. |

### <a name="smb-hardening-improvements-for-sysvol-and-netlogon-connections"></a><a name="smb-hardening-improvements"></a>SYSVOL 및 NETLOGON 연결에 대 한 SMB 강화 기능 향상  
Active Directory 도메인 서비스에 연결된 Windows 10 및 Windows Server 2016 클라이언트에서는 도메인 컨트롤러의 기본 SYSVOL 및 NETLOGON 공유에 SMB 서명 및 상호 인증(예: Kerberos)이 필요합니다.   

**이와 같은 변경을 통해 더해지는 가치**  
이 변경으로 메시지 가로채기 공격의 가능성이 줄어듭니다.   

**달라진 기능**  
SMB 서명 및 상호 인증을 사용할 수 없는 경우 Windows 10 또는 Windows Server 2016 컴퓨터는 도메인 기반 그룹 정책 및 스크립트를 처리하지 않습니다.  

> [!NOTE]  
> 이러한 설정에 대한 레지스트리 값은 기본적으로 존재하지 않지만 그룹 정책 또는 다른 레지스트리 값으로 재정의될 때까지 강화 규칙은 계속 적용됩니다.  

이러한 향상된 보안 기능(UNC 강화라고도 함)에 대한 자세한 내용은 Microsoft 기술 자료 문서 [3000483](https://support.microsoft.com/kb/3000483) 및 [MS15-011 및 MS15-014: 그룹 정책 강화](https://blogs.technet.microsoft.com/srd/2015/02/10/ms15-011-ms15-014-hardening-group-policy)를 참조하세요.  

### <a name="work-folders"></a>클라우드 폴더
클라우드 폴더 서버가 Windows Server 2016를 실행 하 고 작업 폴더 클라이언트가 Windows 10 인 경우 변경 알림이 개선 되었습니다.

**이와 같은 변경을 통해 더해지는 가치**<br>
Windows Server 2012 R2의 경우 파일 변경을 작업 폴더 서버와 동기화하면 클라이언트는 해당 변경에 대해 알리지 않고 업데이트될 때까지 최대 10분을 기다립니다.  Windows Server 2016를 사용 하는 경우 클라우드 폴더 서버는 즉시 Windows 10 클라이언트에 알리고 파일 변경 내용이 즉시 동기화 됩니다.

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

## <a name="see-also"></a>참고 항목  
* [Windows Server 2016의 새로운 기능](../get-started/what-s-new-in-windows-server-2016.md)  
