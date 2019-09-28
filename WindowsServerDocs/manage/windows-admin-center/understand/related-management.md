---
title: Windows Admin Center 관련 관리 솔루션
description: Windows Admin Center가 다른 Microsoft 모니터링 및 관리 솔루션/제품(프로젝트 호노룰루)과 비교되고 이러한 제품을 보완하는 방법
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d681e5007cd3ae3c14de774df0bc85abc23b51d7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406831"
---
# <a name="windows-admin-center-and-related-management-solutions-from-microsoft"></a>Windows Admin Center 및 Microsoft의 관련 관리 솔루션

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

[Windows Admin Center](windows-admin-center.md)는 RDP(원격 데스크톱)를 사용하여 문제 해결 또는 구성을 위해 서버에 연결했을 수 있는 상황을 위해 기존의 기본 제공 서버 관리 도구가 발전한 것입니다. 기존의 다른 Microsoft 관리 솔루션을 대신하기 위해 만들어진 것은 아니며 아래에 설명된 것처럼 이러한 솔루션을 보완하는 데 사용됩니다.

## <a name="remote-server-administration-tools-rsat"></a>RSAT(원격 서버 관리 도구)

[RSAT(원격 서버 관리 도구)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)는 Windows Server에서 선택적 역할 및 기능을 관리하는 GUI 및 PowerShell 도구의 컬렉션입니다. RSAT에는 Windows Admin Center에 없는 많은 기능이 있습니다. 앞으로 RSAT에서 가장 자주 사용되는 도구 중 일부를 Windows Admin Center에 추가할 수 있습니다. 관리를 위해 GUI가 필요한 모든 새 Windows Server 역할 또는 기능은 Windows Admin Center에서 제공될 예정입니다.

## <a name="intune"></a>Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune)은 정책 세트를 기준으로 iOS, Android, Windows 및 macOS 디바이스를 관리할 수 있는 클라우드 기반 엔터프라이즈 이동성 관리 서비스입니다. Intune는 직원이 정보를 액세스 및 공유하는 방법을 제어하여 회사 정보를 보호할 수 있도록 지원하는 데 중점을 둡니다. 반면, Windows Admin Center는 정책 기반 기능이 아니며, 원격 PowerShell 및 WinRM을 통한 WMI를 사용하여 Windows 10 및 Windows Server 시스템의 임시 관리를 사용하도록 설정합니다.

## <a name="azure-stack"></a>Azure 스택

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/)은 데이터 센터에서 Azure 서비스를 제공할 수 있는 하이브리드 클라우드 플랫폼입니다. Azure Stack은 PowerShell 또는 기존 Azure 서비스를 액세스 및 관리하는 데 사용되는 기존 Azure Portal과 비슷한 관리자 포털을 사용하여 관리됩니다. Windows Admin Center는 Azure Stack 인프라를 관리하기 위한 기능이 아니며, [Azure IaaS 가상 머신](../azure/manage-azure-vms.md)(Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 실행)을 관리하거나 Azure Stack 환경에 배포된 개별 물리적 서버의 문제를 해결하는 데 사용할 수 있습니다.

## <a name="system-center"></a>System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center)는 전체 데이터 센터를 배포, 구성, 관리, 모니터링하기 위한 온-프레미스 데이터 센터 관리 솔루션입니다. Windows Admin Center에서는 특정 서버에 드릴다운하여 보다 세분화된 도구로 관리하거나 문제를 해결할 수 있지만 System Center에서는 작업 환경의 모든 시스템 상태를 확인할 수 있습니다.

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **재해석된 "기본 제공" 플랫폼 및 도구** | **데이터 센터 관리 및 모니터링** |
| Windows Server 라이선스에 포함 – MMC 및 다른 기존의 기본 제공 도구와 마찬가지로 **추가 비용이 필요 없음**, | 환경 및 플랫폼에서 추가적인 가치를 제공하기 위한 **포괄적인** 솔루션 제품군 |
| **어디서나** Windows Server 인스턴스의 **경량**, 브라우저 기반 원격 관리, RDP의 대안 | Hyper-V, VMware 및 Linux를 비롯한 **이기종** 시스템을 **대규모로** 관리 및 모니터링 |
|문제 해결, 구성 및 유지 관리를 위해 단일 서버 및 단일 클러스터를 **심층** 드릴다운|인프라 프로비저닝. 자동화 및 셀프 서비스. 인프라 및 워크로드 모니터링의 **풍부한 기능**|
|**개별** 2~4 노드 **HCI** 클러스터의 관리 최적화, Hyper-V, 직접 스토리지 공간 및 SDN 통합|SCVMM을 사용하여 **완전 복구**에서 **데이터 센터 규모의**  Hyper-V, Windows Server 클러스터 배포 및 관리|
|**HCI에서 모니터링** 기능만 지원, 클러스터 상태 서비스에 내역 저장. 자사 및 타사 **관리 도구 확장**을 위한 확장 가능 플랫폼|경고, 알림, 모니터링, 타사 워크로드 모니터링 기능을 포함하는 SCOM의 **포괄적이면서** & **확장 가능한 모니터링** 플랫폼, 기록을 위한 SQL|
|**하이브리드**에 대한 가장 쉬운 브리지. 데이터 보호, 복제, 업데이트 등에 대한 다양한 Azure 서비스 등록 및 사용|**기본 제공** 데이터 보호, 복제, 업데이트(DPM/VMM/SCCM). Log Analytics와 서비스 맵의 하이브리드 통합|
|Windows Server의 **주요 플랫폼 기능**: 스토리지 마이그레이션 서비스, 스토리지 복제본, 시스템 인사이트 등|**추가 플랫폼**: Orchestrator/SMA의 자동화. SCSM 및 다른 서비스 관리 도구와의 통합|

#### <a name="each-delivers-targeted-value-independently-better-together-with-complementary-capabilities"></a>각각이 독립적으로 목표 값 전달, 보완 기능으로 **시너지 효과 발생**
