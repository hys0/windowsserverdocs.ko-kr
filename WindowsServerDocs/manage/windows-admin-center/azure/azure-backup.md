---
title: Azure Backup를 사용 하 여 Windows 관리 센터에서 Windows Server 백업
description: Windows 관리 센터 (Project Honolulu)를 사용 하 여 Azure Backup로 Windows Server 백업
ms.technology: manage
ms.topic: article
author: saurabhsensharma
ms.author: saurse
ms.date: 03/25/2019
ms.localizationpriority: low
ms.prod: windows-server
ms.openlocfilehash: 77171e638fa1eb8c612bdc168868d8286ed23bb6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357399"
---
# <a name="backup-your-windows-servers-from-windows-admin-center-with-azure-backup"></a>Azure Backup를 사용 하 여 Windows 관리 센터에서 Windows Server 백업

>적용 대상: Windows 관리 센터 미리 보기, Windows 관리 센터

[Windows 관리 센터와 Azure의 통합에 대해 자세히 알아보세요.](../plan/azure-integration-options.md)

Windows 관리 센터는 Windows Server를 Azure에 백업 하는 프로세스를 간소화 하 고 우발적 이거나 악의적인 삭제, 손상 및 랜 섬 웨어 로부터 보호 합니다. 설치를 자동화하기 위해 Windows Admin Center 게이트웨이를 Azure에 연결할 수 있습니다.

다음 정보를 사용 하 여 windows Server에 대 한 백업을 구성 하 고 Windows 관리 센터에서 서버 볼륨과 Windows 시스템 상태를 백업 하는 백업 정책을 만들 수 있습니다.

## <a name="what-is-azure-backup-and-how-does-it-work-with-windows-admin-center"></a>Azure Backup 정의 및 Windows 관리 센터에서 어떻게 작동 하나요? 

**Azure Backup** 은 Microsoft 클라우드에서 데이터를 백업 (또는 보호) 하 고 복원 하는 데 사용할 수 있는 Azure 기반 서비스입니다. Azure Backup는 기존 온-프레미스 또는 오프 사이트 백업 솔루션을 안정적이 고, 안전 하며, 비용 경쟁적인 클라우드 기반 솔루션으로 대체 합니다.
[Azure Backup에 대해 자세히 알아보세요](https://docs.microsoft.com/azure/backup/backup-overview).

Azure Backup은 적절 한 컴퓨터, 서버 또는 클라우드에서 다운로드 하 여 배포 하는 여러 구성 요소를 제공 합니다. 배포 하는 구성 요소 또는 에이전트는 보호할 내용에 따라 달라 집니다. 온-프레미스 또는 Azure에서 데이터를 보호 하는지 여부에 관계 없이 모든 Azure Backup 구성 요소는 Azure의 Recovery Services 자격 증명 모음에 데이터를 백업 하는 데 사용할 수 있습니다.

Windows 관리 센터에서 Azure Backup의 통합은 볼륨 및 Windows 시스템 상태 온-프레미스 Windows 실제 또는 가상 서버를 백업 하는 데 적합 합니다. 따라서 파일 서버, 도메인 컨트롤러 및 IIS 웹 서버를 백업 하는 포괄적인 메커니즘이 사용 됩니다.

Windows 관리 센터는 기본 **백업** 도구를 통해 Azure Backup 통합을 제공 합니다. **백업** 도구는 서버 백업을 신속 하 게 시작 하 고, 일반적인 백업 및 복원 작업을 수행 하 고, Windows 서버의 전체 백업 상태를 모니터링 하는 설정, 관리 및 모니터링 환경을 제공 합니다.

## <a name="prerequisites-and-planning"></a>필수 구성 요소 및 계획

- 하나 이상의 활성 구독이 있는 Azure 계정
- 백업 하려는 대상 Windows 서버는 Azure에 대 한 인터넷 액세스 권한이 있어야 합니다.
- [Windows 관리 센터 게이트웨이를 Azure에 연결](azure-integration.md)

Windows Server를 백업 하는 워크플로를 시작 하려면 서버 연결을 열고 **백업** 도구를 클릭 하 고 아래에 설명 된 단계를 수행 합니다.

## <a name="setup-azure-backup"></a>설치 Azure Backup
Azure Backup 아직 사용 하도록 설정 되지 않은 서버 연결에 대 한 **백업** 도구를 클릭 하면 **Azure Backup 시작** 화면이 표시 됩니다. **Azure Backup 설정** 단추를 클릭 합니다. 그러면 Azure Backup 설치 마법사가 열립니다. 마법사의 아래에 나열 된 단계에 따라 서버를 백업 합니다.

Azure Backup 이미 구성 되어 있으면 **백업** 도구를 클릭 하면 **백업 대시보드가**열립니다. 대시보드에서 수행할 수 있는 작업 및 작업을 검색 하려면 ([관리 및 모니터링](#management-and-monitoring)) 섹션을 참조 하세요.

### <a name="step-1-login-to-microsoft-azure"></a>1단계: Microsoft Azure 로그인
Azure 계정에 로그인 합니다. 

> [!NOTE]
> Windows 관리 센터 게이트웨이를 Azure에 연결한 경우 Azure에 자동으로 로그인 됩니다. **로그 아웃** 을 클릭 하 여 다른 사용자로 추가로 로그인 할 수 있습니다.

### <a name="step-2-set-up-azure-backup"></a>2단계: Azure Backup 설정
아래에서 설명 하는 Azure Backup에 대 한 적절 한 설정을 선택 합니다.

 - **구독 Id:** Azure에 Windows Server를 백업 하는 데 사용 하려는 Azure 구독입니다. Azure 리소스 그룹과 같은 모든 Azure 자산은 Recovery Services 자격 증명 모음이 선택 된 구독에 생성 됩니다.
 - **자격 증명 모음** 서버 백업이 저장 되는 Recovery Services 자격 증명 모음입니다. 기존 자격 증명 모음에서 선택 하거나 Windows 관리 센터에서 새 자격 증명 모음을 만들 수 있습니다.  
 - **리소스 그룹:** Azure 리소스 그룹은 리소스 컬렉션에 대 한 컨테이너입니다. Recovery Services 자격 증명 모음이 만들어지거나 지정 된 리소스 그룹에 포함 됩니다. 기존 리소스 그룹을 선택 하거나 Windows 관리 센터에서 새 리소스 그룹을 만들 수 있습니다.
 - **위치:** Recovery Services 자격 증명 모음을 만들 Azure 지역입니다. Windows 서버에 가장 가까운 Azure 지역을 선택 하는 것이 좋습니다.

### <a name="step-3-select-backup-items-and-schedule"></a>3단계: 백업 항목 및 일정 선택

- 서버에서 백업 하려는 항목을 선택 합니다. Windows 관리 센터를 사용 하면 백업을 위해 선택한 데이터의 예상 크기를 제공 하는 동시에 **볼륨** 및 **windows 시스템 상태** 를 조합 하 여 선택할 수 있습니다.

> [!NOTE]
> 첫 번째 백업은 선택한 모든 데이터의 전체 백업입니다. 그러나 후속 백업은 본질적으로 증분 되며 이전 백업 이후 데이터 변경 내용만 전송 합니다.

- 시스템 상태 및/또는 볼륨에 대 한 여러 사전 설정 **백업 일정** 에서 선택 합니다.

### <a name="step-4-enter-encryption-passphrase"></a>4단계: 암호화 암호 입력

- 원하는 **암호화 암호** (최소 16 자)를 입력 합니다.  **Azure Backup** 은 사용자가 구성 하 고 사용자가 관리 하는 암호화 암호를 사용 하 여 백업 데이터를 보호 합니다. Azure Backup에서 데이터를 복구 하려면 암호화 암호가 필요 합니다.

> [!NOTE]
> 암호는 다른 서버 또는 [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/quick-create-portal)같은 안전한 오프 사이트 위치에 저장 해야 합니다. Microsoft에서는 암호를 저장 하지 않으며 암호를 분실 하거나 잊어버린 경우 암호를 검색 하거나 다시 설정할 수 없습니다.

- 모든 설정을 검토 하 고 **적용** 을 클릭 합니다.

그러면 Windows 관리 센터에서 다음 작업을 수행 합니다.

1. Azure 리소스 그룹이 아직 없는 경우 새로 만듭니다.
2. 지정 된 대로 Azure Recovery Services 자격 증명 모음 만들기
3. Microsoft Azure Recovery Services 에이전트를 설치 하 고 자격 증명 모음에 등록 합니다.
4. 선택한 옵션에 따라 백업 및 보존 일정을 만들고 Windows Server와 연결 합니다.

## <a name="management-and-monitoring"></a>관리 및 모니터링

Azure Backup 성공적으로 설정 되 면 기존 서버 연결에 대 한 백업 도구를 열 때 **백업 대시보드가** 표시 됩니다. **백업 대시보드에서** 다음 작업을 수행할 수 있습니다.

- **Azure에서 자격 증명 모음에 액세스 합니다.** Azure의 자격 증명 모음으로 이동 하 여 [다양 한 관리 작업](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server) 을 수행할 수 있도록 **백업 대시보드의** **개요** 탭에서 **Recovery Services 자격 증명 모음** 을 클릭 합니다.
- **임시 백업 수행:** **지금 백업** 을 클릭 하 여 임시 백업을 수행 합니다. 
- **작업 모니터링 및 경고 알림 구성:** 대시보드의 **작업** 탭으로 이동 하 여 진행 중인 작업 또는 과거 작업을 모니터링 하 고 실패 한 작업 또는 다른 백업 관련 경고에 대 한 전자 메일을 받도록 [경고 알림을 구성](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server#configuring-notifications-for-alerts) 합니다.
- **복구 지점과 데이터 복구를 확인 합니다.** Azure에서 데이터를 복구 하는 단계에 대해 대시보드의 **복구 위치** 탭을 클릭 하 여 복구 지점의 내용을 확인 하 고 **데이터 복구** 를 클릭 합니다.