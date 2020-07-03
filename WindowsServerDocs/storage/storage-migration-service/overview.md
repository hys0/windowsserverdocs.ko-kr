---
title: Storage Migration Service 개요
description: Storage Migration Service를 사용 하면 저장소를 Windows Server 또는 Azure로 쉽게 마이그레이션할 수 있습니다. Windows 및 Linux 서버에서 데이터를 인벤토리에 추가한 다음 최신 서버 또는 Azure virtual machines로 데이터를 전송 하는 그래픽 도구를 제공 합니다. Storage Migration Service는 앱 및 사용자가 링크나 경로를 변경 하지 않고도 데이터에 액세스할 수 있도록 대상 서버에 서버의 id를 전송 하는 옵션을 제공 합니다.
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 03/26/2020
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 6ec1093a77b036cada9e54c82234d653362ce4d3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930103"
---
# <a name="storage-migration-service-overview"></a>Storage Migration Service 개요

>적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server (반기 채널)

Storage Migration Service를 사용 하면 저장소를 Windows Server 또는 Azure로 쉽게 마이그레이션할 수 있습니다. Windows 및 Linux 서버에서 데이터를 인벤토리에 추가한 다음 최신 서버 또는 Azure virtual machines로 데이터를 전송 하는 그래픽 도구를 제공 합니다. Storage Migration Service는 앱 및 사용자가 링크나 경로를 변경 하지 않고도 데이터에 액세스할 수 있도록 대상 서버에 서버의 id를 전송 하는 옵션을 제공 합니다.

이 항목에서는 저장소 마이그레이션 서비스를 사용 하려는 이유, 마이그레이션 프로세스의 작동 방식, 원본 및 대상 서버에 대 한 요구 사항, [저장소 마이그레이션 서비스의 새로운 기능](#whats-new-in-storage-migration-service)등에 대해 설명 합니다.

## <a name="why-use-storage-migration-service"></a>저장소 마이그레이션 서비스를 사용 하는 이유

최신 하드웨어 또는 가상 컴퓨터로 마이그레이션할 서버 (또는 서버)가 많기 때문에 Storage Migration Service를 사용 합니다. Storage Migration Service는 다음 작업을 수행 하는 데 도움이 되도록 설계 되었습니다.

- 여러 서버 및 해당 데이터 인벤토리
- 원본 서버에서 파일, 파일 공유 및 보안 구성을 빠르게 전송
- 필요에 따라 사용자와 앱이 기존 데이터에 액세스 하기 위해 아무것도 변경 하지 않아도 되도록 원본 서버의 id를 사용 (절삭이 라고도 함) 할 수 있습니다.
- Windows 관리 센터 사용자 인터페이스에서 하나 또는 여러 마이그레이션 관리

![원본 서버에서 대상 서버, Azure Vm 또는 Azure File Sync로 파일 & 구성을 마이그레이션하는 저장소 마이그레이션 서비스를 보여 주는 다이어그램입니다.](media/overview/storage-migration-service-diagram.png)

**그림 1: 저장소 마이그레이션 서비스 원본 및 대상**

## <a name="how-the-migration-process-works"></a>마이그레이션 프로세스의 작동 방식

마이그레이션은 세 단계로 진행 됩니다.

1. 파일 및 구성에 대 한 정보를 수집 하는 **인벤토리 서버** (그림 2에 표시).
2. 원본 서버에서 대상 서버로 **데이터를 전송 (복사)** 합니다.
3. **새 서버로** 이동 합니다 (선택 사항).<br>대상 서버는 앱과 사용자가 아무것도 변경할 필요가 없도록 원본 서버의 이전 id를 가정 합니다. <br>원본 서버는 유지 관리 상태를 입력 합니다. 여기에는 항상 동일한 파일이 포함 되지만 (원본 서버에서는 파일을 제거 하지 않음) 사용자 및 앱에서 사용할 수 없습니다. 그런 다음 사용자의 편의를 위해 서버를 서비스 해제할 수 있습니다.

![스캔할 준비가 된 서버를 보여 주는 스크린샷 ](media/migrate/inventory.png)
 **그림 2: 저장소 마이그레이션 서비스 서버 인벤토리**

저장소 마이그레이션 서비스를 사용 하 여 현재 지원 되지 않는 Windows Server 2008 R2 서버와 같은 서버를 사용 하 고 저장소를 최신 서버로 이동 하는 방법을 보여 주는 비디오는 다음과 같습니다.

> [!VIDEO https://www.youtube.com/embed/h-Xc9j1w144]

## <a name="requirements"></a>요구 사항

저장소 마이그레이션 서비스를 사용 하려면 다음이 필요 합니다.

- **원본 서버** 또는 파일 및 데이터를 마이그레이션할 **장애 조치 (failover) 클러스터**
- 로 마이그레이션할 Windows Server 2019 (클러스터 또는 독립 실행형)을 실행 하는 **대상 서버** 입니다. Windows Server 2016 및 Windows Server 2012 R2도 작동 하지만 50% 저하 됨
- 마이그레이션을 관리 하기 위해 Windows Server 2019를 실행 하는 **orchestrator 서버**  <br>서버를 몇 대만 마이그레이션하고 서버 중 하나가 Windows Server 2019를 실행 하는 경우이를 orchestrator로 사용할 수 있습니다. 더 많은 서버를 마이그레이션하는 경우 별도의 orchestrator 서버를 사용 하는 것이 좋습니다.
- PowerShell을 사용 하 여 마이그레이션을 관리 하지 않는 한, ** [Windows 관리 센터](../../manage/windows-admin-center/understand/windows-admin-center.md) 를 실행 하는 PC 또는 서버** 에서 Storage migration Service 사용자 인터페이스를 실행 합니다. Windows 관리 센터와 Windows Server 2019 버전은 모두 버전 1809 이상 이어야 합니다.

Orchestrator와 대상 컴퓨터에는 2 개 이상의 코어 또는 두 개의 vCPUs와 최소 2gb의 메모리가 있는 것이 좋습니다. 인벤토리 및 전송 작업은 프로세서 및 메모리를 더 많이 사용 하 여 훨씬 더 빠릅니다.

### <a name="security-requirements-the-storage-migration-service-proxy-service-and-firewall-ports"></a>보안 요구 사항, 저장소 마이그레이션 서비스 프록시 서비스 및 방화벽 포트

- 원본 컴퓨터와 orchestrator 컴퓨터의 관리자 인 마이그레이션 계정
- 대상 컴퓨터와 orchestrator 컴퓨터의 관리자 인 마이그레이션 계정
- Orchestrator 컴퓨터에는 *인바운드*를 사용 하는 파일 및 프린터 공유 (SMB 인) 방화벽 규칙이 있어야 합니다.
- 원본 및 대상 컴퓨터에는 *인바운드* 를 사용 하도록 설정 된 다음 방화벽 규칙이 있어야 합니다 (이미 사용 하도록 설정 되어 있을 수 있음).
  - 파일 및 프린터 공유(SMB-In)
  - Netlogon 서비스 (NP-IN)
  - Windows Management Instrumentation(DCOM-In)
  - Windows Management Instrumentation(WMI-In)

  > [!TIP]
  > Windows Server 2019 컴퓨터에 Storage Migration Service 프록시 서비스를 설치 하면 해당 컴퓨터에 필요한 방화벽 포트가 자동으로 열립니다. 이렇게 하려면 Windows 관리 센터에서 대상 서버에 연결한 다음 **서버 관리자** (Windows 관리 센터) > **역할 및 기능**으로 이동 하 고 **저장소 마이그레이션 서비스 프록시**를 선택한 다음 **설치**를 선택 합니다.


- 컴퓨터가 Active Directory Domain Services 도메인에 속하는 경우 모두 동일한 포리스트에 속해 있어야 합니다. 또한 대상 서버는 원본 서버와 동일한 도메인에 있어야 합니다. 잘라낼 때 원본 도메인 이름을 대상으로 전송 하려는 경우에는 원본 서버와 동일한 도메인에 있어야 합니다. 는 기술적으로는 도메인 전체에서 작동 하지만 대상의 정규화 된 도메인 이름은 원본과 다릅니다.

### <a name="requirements-for-source-servers"></a>원본 서버에 대 한 요구 사항

원본 서버는 다음 운영 체제 중 하나를 실행 해야 합니다.

- Windows Server, 반기 채널
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2
- Windows Server 2008
- Windows Server 2003 R2
- Windows Server 2003
- Windows Small Business Server 2003 R2
- Windows Small Business Server 2008
- Windows Small Business Server 2011
- Windows Server 2012 Essentials
- Windows Server 2012 R2 Essentials
- Windows Server 2016 Essentials
- Windows Server 2019 Essentials
- Windows Storage Server 2008
- Windows Storage Server 2008 R2
- Windows Storage Server 2012
- Windows Storage Server 2012 R2
- Windows Storage Server 2016

참고: Windows Small Business Server 및 Windows Server Essentials는 도메인 컨트롤러입니다. Storage Migration Service는 아직 도메인 컨트롤러에서 이동할 수 없지만 파일의 인벤토리 및 전송에는 사용할 수 있습니다.

Orchestrator가 Windows Server, 버전 1903 이상을 실행 하거나 orchestrator가 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 가 설치 된 이전 버전의 windows server를 실행 하는 경우 다음과 같은 추가 원본 유형을 마이그레이션할 수 있습니다.

- Windows Server 2012, Windows Server 2012 R2, Windows Server 2016, Windows Server 2019을 실행 하는 장애 조치 (Failover) 클러스터
- Samba를 사용 하는 Linux 서버. 다음 사항을 테스트 했습니다.
    - CentOS 7
    - Debian GNU/Linux 8
    - RedHat Enterprise Linux 7.6
    - SUSE Linux Enterprise Server (SLES) 11 SP4
    - Ubuntu 16.04 LTS 및 12.04.5 LTS
    - Samba 4.8, 4.7, 4.3, 4.2 및 3.6

### <a name="requirements-for-destination-servers"></a>대상 서버에 대 한 요구 사항

대상 서버는 다음 운영 체제 중 하나를 실행 해야 합니다.

- Windows Server, 반기 채널
- Windows Server 2019
- Windows Server 2016
- Windows Server 2012 R2

> [!TIP]
> Windows server 2019 또는 Windows Server, 반기 채널 이상을 실행 하는 대상 서버는 이전 버전의 Windows Server의 전송 성능을 두 배로 향상 합니다. 이러한 성능 향상은 기본 제공 저장소 마이그레이션 서비스 프록시 서비스를 포함 하기 때문에 발생 합니다 .이 서비스는 아직 열려 있지 않은 경우에도 필요한 방화벽 포트를 엽니다.

## <a name="azure-vm-migration"></a>Azure VM 마이그레이션

Windows 관리 센터 버전 1910을 사용 하 여 Azure 가상 컴퓨터를 배포할 수 있습니다. 이렇게 하면 VM 배포가 Storage Migration Service에 통합 됩니다. 워크 로드를 배포 하기 전에 직접 Azure Portal에서 새 서버 및 Vm을 구축 하는 대신, 필요한 단계 및 구성이 누락 될 수 있습니다. Windows 관리 센터에서 Azure VM을 배포 하 고, 저장소를 구성 하 고, 도메인에 연결 하 고, 역할을 설치 하 고, 분산 시스템을 설정할 수 있습니다.

   Storage Migration Service를 사용 하 여 Azure Vm으로 마이그레이션하는 방법을 보여 주는 비디오는 다음과 같습니다.
   > [!VIDEO https://www.youtube-nocookie.com/embed/k8Z9LuVL0xQ]
   
이후 운영 체제로 마이그레이션하지 않고 가상 컴퓨터를 Azure로 리프트 앤 시프트 하려면 Azure Migrate를 사용 하는 것이 좋습니다. 자세한 내용은 [Azure Migrate 개요](https://go.microsoft.com/fwlink/?linkid=2056064)를 참조 하세요.

## <a name="whats-new-in-storage-migration-service"></a>저장소 마이그레이션 서비스의 새로운 기능

Windows 관리 센터 버전 1910은 Azure virtual machines를 배포 하는 기능을 추가 합니다. Azure VM 배포를 Storage Migration Service에 통합 합니다. 자세한 내용은 [AZURE VM 마이그레이션](#azure-vm-migration)을 참조 하세요.

Windows Server, 버전 1903 이상 또는 [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) 가 설치 된 이전 버전의 windows Server에서 Storage Migration Server orchestrator를 실행 하는 경우 다음과 같은 새로운 기능을 사용할 수 있습니다.

- 새 서버로 로컬 사용자 및 그룹 마이그레이션
- 장애 조치 (failover) 클러스터에서 저장소 마이그레이션, 장애 조치 클러스터로 마이그레이션 및 독립 실행형 서버와 장애 조치 (failover) 클러스터 간 마이그레이션
- 삼바를 사용하는 Linux 서버에서 스토리지 마이그레이션
- Azure 파일 동기화를 사용하여 마이그레이션된 공유를 Azure에 쉽게 동기화
- Azure와 같은 신규 네트워크로 마이그레이션

## <a name="additional-references"></a>추가 참조

- [저장소 마이그레이션 서비스를 사용 하 여 파일 서버 마이그레이션](migrate-data.md)
- [Storage Migration Services FAQ (질문과 대답)](faq.md)
- [저장소 마이그레이션 서비스의 알려진 문제](known-issues.md)
