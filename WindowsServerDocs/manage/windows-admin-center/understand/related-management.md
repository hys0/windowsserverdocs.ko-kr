---
title: Windows Admin Center 관련 관리 솔루션
description: Windows Admin Center 비교 하 고 다른 Microsoft 모니터링 및 관리 솔루션/제품 (프로젝트 브라 티)을 보완 하는 방법
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 385a066cb828f58d698c2ca47e0553e996a77733
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847324"
---
# <a name="windows-admin-center-and-related-management-solutions-from-microsoft"></a>Windows Admin Center 및 Microsoft에서 관련 된 관리 솔루션

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

[Windows Admin Center](windows-admin-center.md) 는 기존의 기본 서버 위치 사용 원격 데스크톱 (RDP) 문제 해결 또는 구성 서버에 연결 하는 상황에 대 한 관리 도구입니다. 다른 기존 Microsoft 관리 솔루션의 이름을 바꾸려면 위한 대신이 아래 설명 된 대로 이러한 솔루션을 보완 합니다.

## <a name="remote-server-administration-tools-rsat"></a>RSAT(원격 서버 관리 도구)

[원격 서버 관리 도구 (RSAT)](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools) 은 Windows Server에서 선택적 역할 및 기능을 관리 하는 GUI 및 PowerShell 도구 집합이 있습니다. RSAT은 Windows Admin Center 없는 많은 기능이 있습니다. 에서는를 추가할 수는 가장 자주 사용 되는 도구 중 일부를 rsat에서 Windows Admin Center 나중에. 모든 새 Windows Server 역할 또는 기능 관리를 위한 GUI를 필요로 하는 Windows Admin Center 있게 됩니다.

## <a name="intune"></a>Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) 는 정책 집합에 따라 iOS, Android, Windows, 및 macOS 장치를 관리할 수 있는 클라우드 기반 엔터프라이즈 이동성 관리 서비스입니다. Intune는 직원에 게 액세스 하 고 정보를 공유 하는 방법을 제어 하 여 회사 정보를 보호 하는 데 사용할에 중점을 둡니다. 반면 Windows Admin Center 정책 기반 이며 되지 않지만 원격 PowerShell 및 WMI를 사용 하 여 WinRM을 통해 Windows 10 및 Windows Server 시스템으로 임시 관리할 수 있습니다.

## <a name="azure-stack"></a>Azure Stack

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) 는 데이터 센터에서 Azure 서비스를 제공할 수 있는 하이브리드 클라우드 플랫폼입니다. Azure Stack PowerShell 또는 기존 Azure portal에 액세스 하 고 기존 Azure 서비스를 관리 하는 데 비슷한 관리자 포털을 사용 하 여 관리 됩니다. 사용할 수 있지만 Windows Admin Center Azure Stack 인프라를 관리 하는 데 사용할 수 없습니다 [Azure IaaS 가상 머신 관리](../configure/manage-azure-vms.md) (Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 실행) 또는 문제 해결 개별 물리적 서버를 Azure Stack 환경에 배포 합니다.

## <a name="system-center"></a>System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center) 온-프레미스 데이터 센터 관리 솔루션을 배포, 구성, 관리, 전체 데이터 센터 모니터링 됩니다. System Center를 사용 하면 Windows Admin Center 사용 하면 드릴 다운 특정 서버를 관리 하거나 보다 세분화 된 도구를 사용 하 여 문제를 해결 하는 동안 사용자 환경에서 모든 시스템의 상태를 볼 수 있습니다.

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **새롭게 구축 된 "기본" 플랫폼 및 도구** | **데이터 센터 관리 및 모니터링** |
| Windows Server 라이선스 – 포함 된 **추가 비용 없이**MMC 및 다른 기존 상자에서 도구와 마찬가지로, | **포괄적인** 환경 및 플랫폼에서 추가 값에 대 한 솔루션 제품군 |
| **경량**, Windows Server 인스턴스의 원격 관리 브라우저 기반 **어디서 나**rdp 대체; | 관리 및 모니터링 **이기종** 체제 **대규모로**, Hyper-v, VMware, Linux 등 |
|**심층** 단일 서버 및 단일 클러스터에 대해 드릴 다운 문제 해결, 구성 및 유지 관리|인프라를 프로 비전 합니다. 자동화 및 셀프 서비스;  인프라 및 워크 로드 모니터링 **너비**|
|관리를 최적화 **개별** 2 ~ 4 노드 **HCI** 클러스터, Hyper-v, 저장소 공간 다이렉트 및 SDN 통합|배포 및 관리 Hyper-v, Windows Server 클러스터에서 **데이터 센터 크기 조정** 에서 **완전 복구** SCVMM을 사용 하 여|
|**HCI에서 모니터링** 클러스터 상태 관리 서비스의 기록을 저장만;. 첫 번째 및 세 번째 파티에 대 한 확장 가능한 플랫폼 **관리 도구 확장**|**Extensible** & **확장 가능한 모니터링** SCOM에서 경고, 알림, 모니터링, 타사 워크 로드를 사용 하 여 플랫폼 기록에 대 한 SQL|
|가장 쉬운 방법은 브리지 **하이브리드**온 보 딩; 다양 한 데이터 보호, 복제, 업데이트 등에 대 한 Azure 서비스를 사용 하 여|**기본 제공** 데이터 보호, 복제, 업데이트 (DPM/VMM/SCCM). 서비스 맵은 Log Analytics와 하이브리드 통합|
|**플랫폼 기능 단계인** 의 Windows Server: 저장소 마이그레이션 서비스, 저장소 복제본에 대 한 시스템 정보 활용, 등입니다.|**추가 플랫폼**: 오 케 스트레이 터/SMA의 자동화입니다. SCSM 및 다른 서비스 관리 도구와의 통합|

#### <a name="each-delivers-targeted-value-independently-better-together-with-complementary-capabilities"></a>대상된 값을 독립적으로; 제공 각 **시너지 효과** 보완 기능을 사용 하 여 합니다.
