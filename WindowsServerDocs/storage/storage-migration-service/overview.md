---
Title: 저장소 서비스 마이그레이션 개요
description: 저장소 마이그레이션 서비스를 사용 하면 쉽게 서버를 Windows Server의 최신 버전으로 마이그레이션할 수입니다. 서버에서 데이터를 인벤토리에 포함 하 고 데이터 및 구성을 새 서버로 전송 하는 그래픽 도구를 제공, 앱 또는 사용자가 아무 것도 변경할 필요가 없이 합니다.
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 05/21/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: fd99058036a5b8041e4c65ca120c6a7e68b2df8d
ms.sourcegitcommit: c8cc0b25ba336a2aafaabc92b19fe8faa56be32b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/21/2019
ms.locfileid: "65976654"
---
# <a name="storage-migration-service-overview"></a>저장소 서비스 마이그레이션 개요

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server (반기 채널)

저장소 마이그레이션 서비스를 사용 하면 쉽게 서버를 Windows Server의 최신 버전으로 마이그레이션할 수입니다. 서버에서 데이터를 인벤토리에 포함 하 고 데이터 및 구성을 새 서버로 전송 하는 그래픽 도구를 제공, 앱 또는 사용자가 아무 것도 변경할 필요가 없이 합니다.

저장소 마이그레이션 서비스를 사용 하는 이유, 마이그레이션 프로세스의 작동 방식 및 원본 및 대상 서버에 대 한 요구 사항은이 항목에 설명 합니다.

## <a name="why-use-storage-migration-service"></a>저장소 마이그레이션 서비스를 사용 하는 이유

서버 (또는 서버가 많은) 최신 하드웨어 또는 가상 컴퓨터를 마이그레이션하려는 가져온 때문에 저장소 마이그레이션 서비스를 사용 합니다. 저장소 마이그레이션 서비스는 다음을 수행 하는 데 설계 되었습니다.

- 여러 서버 및 해당 데이터를 인벤토리
- 원본 서버에서 파일, 파일 공유 및 보안 구성을 신속 하 게 전송
- 필요에 따라 사용자 및 앱에 기존 데이터를 액세스 하려면 아무 것도 변경할 필요가 없습니다 있도록 (라고도 통해 cutting) 원본 서버의 id를 인계
- Windows Admin Center 사용자 인터페이스에서 하나 이상의 마이그레이션 관리

![마이그레이션 파일 저장소 마이그레이션 서비스 및 대상 서버, Azure Vm 또는 Azure File Sync는 원본 서버에서 구성을 보여 주는 다이어그램입니다.](media\overview\storage-migration-service-diagram.png)

**그림 1: 저장소 마이그레이션 서비스 원본 및 대상**

## <a name="how-the-migration-process-works"></a>마이그레이션 프로세스의 작동 원리

마이그레이션 3 단계 프로세스입니다.

1. **서버 인벤토리** 파일과 (그림 2에 표시) 하는 구성에 대 한 정보를 수집 합니다.
2. **(복사) 데이터 전송** 대상 서버에 원본 서버에서.
3. **새 서버로 전환할** (선택 사항).<br>대상 서버 앱 및 사용자가 아무 것도 변경할 필요가 없습니다 있도록 원본 서버의 이전 identities을 가정 합니다. <br>원본 서버 상태가 유지 관리를 계속 포함 된 동일한 항상 파일 (되지 제거 파일 원본 서버에서) 있지만 사용자 및 앱에 사용할 수 없습니다. 그런 다음 편리한 시간에 서버를 서비스 해제할 수 있습니다.

![검색할 준비 서버를 보여 주는 스크린 샷](media/migrate/inventory.png)
**그림 2: 서버 인벤토리 하는 저장소 마이그레이션 서비스**

## <a name="requirements"></a>요구 사항

저장소 마이그레이션 서비스를 사용 하려면 다음이 필요 합니다.

- A **원본 서버** 파일과 데이터를 마이그레이션하려면
- A **대상 서버** 마이그레이션하려면 Windows Server 2019 실행-Windows Server 2016 및 Windows Server 2012 R2도 작동 되지만 약 50% 더 느리게
- **오 케 스트레이 터 server** 마이그레이션을 관리 하는 Windows Server 2019 실행  <br>소수의 서버가 마이그레이션하는 경우 Windows Server 2019를 실행 중인 서버 중 하나는 오 케 스트레이 터로는 사용할 수 있습니다. 더 많은 서버를 마이그레이션하는 경우에 별도 orchestrator 서버를 사용 하는 것이 좋습니다.
- A **실행 서버 또는 PC [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md)**  마이그레이션을 관리 하기 위해 PowerShell 사용 하려는 경우가 아니면 저장소 마이그레이션 서비스 사용자 인터페이스를 실행 합니다. Windows Admin Center 및 Windows Server 2019 버전 둘 다 이상 이어야 합니다 1809 버전입니다.

권장 하는 오 케 스트레이 터 및 대상 컴퓨터에 두 개 이상의 코어 또는 두 개의 Vcpu 및 최소 2GB의 메모리. 인벤토리 및 전송 작업은 더 많은 프로세서 및 메모리를 사용 하 여 훨씬 더 빠릅니다.

### <a name="security-requirements"></a>보안 요구 사항

- 마이그레이션 계정 관리자가 원본 컴퓨터와 오 케 스트레이 터 컴퓨터입니다.
- 마이그레이션 계정 관리자가 대상 컴퓨터와 오 케 스트레이 터 컴퓨터입니다.
- 오 케 스트레이 터 컴퓨터에 파일 및 프린터 공유 (Smb-in) 방화벽 규칙을 사용할 수 있어야 합니다. *인바운드*합니다.
- 원본 및 대상 컴퓨터에 설정 된 다음 방화벽 규칙 있어야 *인바운드* (하지만 이미 사용 하도록 설정 하 고 있을 수 있습니다).
  - 파일 및 프린터 공유(SMB-In)
  - Netlogon 서비스 (Np-in)
  - Windows Management Instrumentation (Dcom-in)
  - WMI(Windows Management Instrumentation)(WMI-In)
  
  > [!TIP]
  > Windows Server 2019 컴퓨터 저장소 마이그레이션 서비스 프록시 서비스를 자동으로 설치 컴퓨터에 필요한 방화벽 포트를 엽니다.
- 컴퓨터는 Active Directory Domain Services 도메인에 속할 경우 해야 모든 속한 동일한 포리스트에 있습니다. 대상 서버를 통해 잘라내기 때 원본의 도메인 이름 대상에 전송 하려는 경우 원본 서버와 동일한 도메인에 수도 있어야 합니다. 단독형 기술적 작동 도메인에 걸쳐 하지만 대상의 정규화 된 도메인 이름을 원본에서 다른 됩니다...

### <a name="requirements-for-source-servers"></a>원본 서버에 대 한 요구 사항

원본 서버는 다음 운영 체제 중 하나를 실행 해야 합니다.

- Windows Server 반기 채널
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- Windows Server 2008
- Windows Server 2003 R2
- Windows Server 2003

Orchestrator 1903 이상 버전의 Windows Server를 실행 중인 경우 추가 원본 유형은 마이그레이션할 수 있습니다.

- 장애 조치(failover) 클러스터
- Samba를 사용 하는 Linux 서버. 다음 테스트 했습니다.
    - 7.6 RedHat Enterprise Linux, CentOS 7, 8 Debian, Ubuntu 16.04 및 12.04.5, SUSE Linux Enterprise Server 11 (SLES) SP4
    - Samba 4.x, 3.6.x

### <a name="requirements-for-destination-servers"></a>대상 서버에 대 한 요구 사항

대상 서버는 다음 운영 체제 중 하나를 실행 해야 합니다.

- Windows Server 반기 채널
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> Windows Server 2019 또는 Windows Server를 실행 하는 대상 서버를 반기 채널 버전 1809 이상 경우 이전 버전의 Windows Server의 전송 성능을 double 이 성능 향상도 필요한 방화벽 포트는 아직 수행 하지 않은 경우 열을 열 수 있는 기본 제공 저장소 마이그레이션 서비스 프록시 서비스의 포함 되었기 때문입니다.

## <a name="whats-new-in-storage-migration-service"></a>저장소 마이그레이션 서비스의 새로운 기능

Windows Server 버전 1903에 오 케 스트레이 터 서버에서 실행 하는 경우 다음과 같은 새로운 기능을 추가 합니다.

- 새 서버에 로컬 사용자 및 그룹 마이그레이션
- 장애 조치 클러스터에서 저장소를 마이그레이션
- Samba를 사용 하는 Linux 서버에서 저장소를 마이그레이션하십시오.
- 보다 쉽게 Azure File Sync를 사용 하 여 Azure로 마이그레이션된 공유를 동기화
- Azure와 같은 새 네트워크로 마이그레이션

## <a name="see-also"></a>참조

- [저장소 마이그레이션 서비스를 사용 하 여 파일 서버 마이그레이션](migrate-data.md)
- [저장소 마이그레이션 서비스 질문과 대답 (FAQ)](faq.md)
- [Storage Migration Service의 알려진 문제](known-issues.md)
