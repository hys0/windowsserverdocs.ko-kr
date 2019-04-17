---
title: Azure Backup을 사용 하 여 Windows 관리 센터에서 Windows Server 백업
description: Azure 백업으로 백업 Windows 서버를 사용 하 여 Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: saurabhsensharma
ms.author: saurse
ms.date: 03/25/2019
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 3983d0b65bc69ef9fd40f3c8e196d40534b1b8f9
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296982"
---
# Azure Backup을 사용 하 여 Windows 관리 센터에서 Windows Server 백업

>적용 대상: Windows Admin Center Preview, Windows Admin Center

[Windows Admin Center와 Azure를 통합하는 방법에 대해 알아보세요.](../plan/azure-integration-options.md)

Windows Admin Center는 Azure에 Windows Server 백업 및 우발적 또는 악성 삭제, 손상 및도 랜 섬 웨어 로부터 보호할 수는 프로세스를 간소화 합니다. 설치를 자동화하기 위해 Windows Admin Center 게이트웨이를 Azure에 연결할 수 있습니다.

다음 정보를 사용 하 여 백업 하면 Windows Server에 대 한 구성 하 고 Windows 관리 센터에서 Windows 시스템 상태와 서버의 볼륨을 백업 하는 백업 정책을 만듭니다.

## Azure 백업 무엇 이며 Windows Admin Center를 사용 하 여 어떻게 작동 합니까? 

**Azure Backup** 는 백업 (또는 보호) 하는 데 사용할 수 Azure 기반 서비스 및 Microsoft 클라우드에서 데이터를 복원 합니다. Azure 백업 기존 온-프레미스 또는 외부 백업 솔루션 클라우드 기반 솔루션을 신뢰할 수 있는 안전 하 고 경쟁 비용으로 바꿉니다.
[Azure 백업에 자세히 알아봅니다](https://docs.microsoft.com/azure/backup/backup-overview).

다운로드 하 고 적절 한 컴퓨터에 배포 하는 여러 구성 요소를 제공 하는 azure 백업 서버 또는 클라우드에서 합니다. 구성 요소 또는 에이전트 배포 하는 보호 하려는에 따라 다릅니다. Azure에서는 복구 서비스 자격 증명 모음에 데이터를 백업 하 (데이터 온-프레미스를 보호 하는 여부에 관계 없이 또는 Azure에) 모든 Azure 백업 구성 요소를 사용할 수 있습니다.

통합 Windows 관리 센터에서 Azure 백업 볼륨 및 Windows 시스템 상태 온-프레미스 Windows 물리적 또는 가상 서버 백업에 이상적입니다. 따라서 파일 서버, 도메인 컨트롤러 및 IIS 웹 서버를 백업 하는 포괄적인 메커니즘에 대 한 있습니다.

Windows Admin Center는 네이티브 **백업** 도구를 통해 Azure 백업 통합을 노출합니다. **백업** 도구 설치, 관리 및 일반적인 백업 및 복원 작업을 신속 하 게 서버 백업 시작 환경을 모니터링, 제공 및 Windows Server의 전체 백업 상태를 모니터링 합니다.

## 필수 구성 요소 및 계획

- 하나 이상의 활성 구독이 있는 Azure 계정
- 대상 하려는 Windows Server 백업 Azure에 인터넷 액세스 해야 합니다.
- [Windows Admin Center 게이트웨이를 Azure에 연결](azure-integration.md)

Windows Server 백업 워크플로 시작 하려면 서버 연결, **백업** 도구를 클릭 하 고 아래에 설명 된 단계를 수행 합니다.

## Azure 백업 설치
Azure 백업 되어 있지 않은 아직 서버 연결에 대 한 **백업** 도구를 클릭할 때 **Azure 백업 시작** 화면이 표시 됩니다. **Azure 백업 설정** 단추를 클릭 합니다. 이렇게 하면 Azure 백업 설치 마법사를 열립니다. 서버 백업 마법사의 아래에 나열 된 단계를 따릅니다.

Azure 백업 이미 구성 되어 **백업** 도구를 클릭 **백업 대시보드**열 됩니다. 작업 및 대시보드에서 수행할 수 있는 작업 ([관리 및 모니터링](#management-and-monitoring)) 섹션을 참조 하세요.

### Microsoft Azure에 1 단계: 로그인
하면 Azure 계정에 로그인 합니다. 

> [!NOTE]
> Windows Admin Center 게이트웨이를 Azure에 연결한 경우 하면 해야 자동으로 로그인 azure 합니다. 클릭 수 **로그 아웃** 에 추가로 다른 사용자로 합니다.

### 2 단계: Azure 백업 설정
아래 설명 된 대로 Azure 백업에 대 한 적절 한 설정 선택

 - **구독 Id:** Azure에 Windows Server 백업 하는 데 사용할 Azure 구독입니다. Azure 리소스 그룹과 같은 모든 Azure 자산을 복구 서비스 자격 증명 모음 선택한 구독에서 생성 됩니다.
 - **자격 증명 모음:** 복구 서비스 자격 증명 모음은 서버에 백업을 저장 됩니다. 기존 보관소에서 선택할 수 또는 Windows Admin Center는 새 자격 증명 모음 만들어집니다.  
 - **리소스 그룹:** Azure 리소스 그룹은 리소스의 컬렉션에 대 한 컨테이너입니다. 복구 서비스 자격 증명 모음을 만들거나 지정 된 리소스 그룹에 포함 합니다. 기존 리소스 그룹에서 선택할 수 또는 Windows Admin Center 새로 만들어야 합니다.
 - **위치:** 복구 서비스 자격 증명 모음 만들어지는 Azure 지역입니다. Windows Server에 가장 가까운 Azure 지역을 선택 하는 것이 좋습니다.

### 3 단계: 백업 항목 및 일정 선택

- 서버에서 백업를 선택 합니다. Windows Admin Center를 사용 하면 백업에 대 한 선택 된 데이터의 예상된 크기를 제공 하는 동안 **Windows 시스템 상태** 와 **볼륨** 의 조합에서 선택할 수 있습니다.

> [!NOTE]
> 첫 번째 백업 선택 된 모든 데이터의 전체 백업이입니다. 그러나 후속 백업은 본질적으로 증분 되며 이전 백업 이후 변경 내용만 데이터를 전송 합니다.

- 여러 미리 설정 된 **백업 일정** 에서 시스템 상태 및/또는 볼륨을 선택 합니다.

### 4 단계: 암호화 암호를 입력 합니다.

- 선택한 (최소 16 자)는 **암호화 암호** 를 입력 합니다.  **Azure 백업** 사용자 구성 하 고 사용자가 관리 암호화 암호를 사용 하 여 백업 데이터를 보호합니다. Azure 백업에서 데이터를 복구 하는 암호화 공유 암호 필요 합니다.

> [!NOTE]
> 암호가 다른 서버 또는 [Azure 키 자격 증명 모음](https://docs.microsoft.com/azure/key-vault/quick-create-portal)같은 안전한 장소에 저장 해야 합니다. Microsoft 하지는 암호를 저장 및 수 없는 검색 않거나를 분실 하거나 잊어버린 경우는 암호를 다시 설정 합니다.

- 모든 설정을 검토 하 고 **적용**

Windows Admin Center는 다음 작업을 수행할 수

1. 이미 존재 하지 않는 경우 Azure 리소스 그룹 만들기
2. 지정 된 대로 Azure 복구 서비스 보관소 생성
3. 설치 하 고 자격 증명 모음 Microsoft Azure 복구 서비스 에이전트 등록
4. 선택한 옵션에 따라 백업 및 보존 일정을 만들고 Windows 서버와 연결 해야 합니다.

## 관리 및 모니터링

성공적으로 설치 Azure 백업 있는 경우, 기존 서버 연결에 대 한 백업 도구를 열 때 **백업 대시보드** 를 볼 수 있습니다. **백업 대시보드** 에서 다음 작업을 수행할 수 있습니다.

- **액세스 Azure에서 자격 증명 모음:** Azure에서 자격 증명 모음 [다양 한 관리 작업을](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server) 수행 수행 될 **백업 대시보드** **개요** 탭에서 **복구 서비스 자격 증명 모음** 링크를 클릭 수 있습니다.
- **임시 백업을 수행:** **이제 백업** 특별 한 백업에서 클릭 합니다. 
- **모니터 작업 및 구성 경고 알림:** 지난 작업 및 [경고 알림 구성](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server#configuring-notifications-for-alerts) 에 대 한 전자 메일을 받을 수 실패 작업 또는 다른 백업 관련된 알림 또는 이동할 지속적인 모니터링 하려면 대시보드의 **작업** 탭 합니다.
- **보기 복구 지점 및 복구 데이터:** 대시보드의 복구 지점 보고 Azure에서 데이터를 복구 하려면 단계에 대 한 **데이터 복구** 를 클릭 하 고 **복구 지점** 탭을 클릭 합니다.