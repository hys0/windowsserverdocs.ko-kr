---
title: Windows Admin Center 관련 관리 솔루션
description: Windows Admin Center와 비교 하 고 다른 Microsoft 모니터링 및 관리 솔루션/제품 (Project Honolulu)를 보완 하는 방법
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f7bf0e32b1156fe361c79ac4ccd0e3536df767e2
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296715"
---
# Windows Admin Center 및 Microsoft에서 관리 관련된 솔루션

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

[Windows Admin Center](windows-admin-center.md) 는 기존의 기본 서버 관리 도구를 사용한 경우 원격 데스크톱 (RDP) 문제 해결 소프트웨어나 구성에 대 한 서버에 연결 하는 경우입니다. 기존의 다른 Microsoft 관리 솔루션; 대체 하기 위한 용도로 하지는 대신 아래 설명 된 대로 이러한 솔루션을 보완 합니다.

## RSAT(원격 서버 관리 도구)

[원격 서버 관리 도구 (RSAT)은](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools) Windows Server의 선택적 역할 및 기능을 관리 하기 위한 GUI 및 PowerShell 도구 모음입니다. RSAT에 Windows Admin Center에 없는 많은 기능이 있습니다. 수 가장 자주 사용 되는 도구 중 일부에서 추가 RSAT Windows Admin Center를 나중에 합니다. 모든 새 Windows Server 역할 또는 기능 관리에 대 한 GUI를 필요로 하는 Windows Admin Center에서 됩니다.

## Intune

[Intune](https://www.microsoft.com/cloud-platform/microsoft-intune) , 정책에 따라 iOS, Android, Windows 및 macOS 장치를 관리할 수 있는 클라우드 기반 엔터프라이즈 이동성 관리 서비스입니다. Intune는 직원이 액세스 하 고 정보를 공유 하는 방법을 제어 하 여 회사 정보를 보호 하는 것에 중점을 둡니다. 반면, Windows Admin Center는 정책 기반 아니지만 WinRM을 통해 원격 PowerShell 및 WMI를 사용 하 여 Windows 10 및 Windows Server 시스템의 임시 관리할 수 있습니다.

## Azure 스택

[Azure Stack](https://azure.microsoft.com/overview/azure-stack/) 데이터 센터에서 Azure 서비스를 제공할 수 있는 하이브리드 클라우드 플랫폼입니다. Azure 스택 PowerShell 또는 유사한 기존 Azure portal에 액세스 하 고 기존 Azure 서비스를 관리 하는 데 사용 하는 관리자 포털을 사용 하 여 관리 됩니다. Windows Admin Center Azure Stack 인프라를 관리 하기 위한 되지 있지만 [Azure IaaS 가상 컴퓨터 관리](../azure/manage-azure-vms.md) (Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 실행)를 사용 하거나 개별 물리적 문제 해결 Azure Stack 환경에 배포 된 서버입니다.

## System Center

[System Center](https://www.microsoft.com/cloud-platform/system-center) 는 온-프레미스 데이터 센터 관리 솔루션 배포, 구성, 관리에 대 한 전체 데이터 센터를 모니터링 합니다. System Center를 통해 Windows Admin Center를 사용 하면 특정 서버를 관리 하거나 보다 세밀 하 게 도구를 사용 하 여 문제 해결에 드릴 다운 하는 동안 사용자 환경에 있는 모든 시스템의 상태를 확인할 수 있습니다.

| Windows Admin Center                 | System Center                      |
|--------------------------------------|------------------------------------|
| **작업 새롭게 구축 했습니다 "기본" 플랫폼 & 도구** | **데이터 센터 관리 & 모니터링** |
| Windows Server 라이선스 – **추가 비용 없이**, MMC 및 기타 기존의 기본 제공 도구와 마찬가지로 포함 된 | **종합적인 환경 및 플랫폼 간에 추가 값에 대 한 솔루션** |
| **경량**, 브라우저 기반 원격 관리, Windows Server의 **아무 곳 이나**; RDP 하지 않아도 | _AMP_ 모니터 **이기종** 시스템 **규모에서**Hyper-v, VMware, Linux 등 관리 |
|**심층** 단일 서버 & 단일 클러스터 드릴 다운 & 유지 관리 구성 문제 해결|인프라 프로 비전 합니다. 자동화 및 셀프 서비스입니다.  인프라와 **폭** 모니터링 워크 로드|
|Hyper-v, 저장소 공간 다이렉트 및 SDN 통합의 **개별** 2-4 노드 **HCI** 클러스터의 최적화 된 관리|배포 & Hyper-v, SCVMM과 **베어 메탈** **데이터 센터** 배율로 Windows 서버 클러스터 관리|
|**모니터링 HCI에** 만 사용 합니다; 클러스터 상태 관리 서비스는 기록을 저장합니다. 첫 번째 및 제 3 자 **관리자 도구 확장** 에 대 한 확장 가능한 플랫폼|**확장 가능한** & SCOM, 경고, 알림, 모니터링, 타사 워크 로드와 플랫폼**확장 가능한 모니터링** SQL 기록|
|**하이브리드**; 쉬운 브리지 온 보 딩 하 고 다양 한 데이터 보호, 복제, 업데이트 등에 대 한 Azure 서비스 사용|**기본 제공** 데이터 보호, 복제, 업데이트 (SCCM/DPM/VMM). 하이브리드 Log Analytics 및 지도 서비스 통합|
|Windows server **플랫폼 기능** : 저장소 마이그레이션 서비스, 저장소 복제본, 시스템 인 사이트입니다.|**다른 플랫폼**: Orchestrator/SMA에서 자동화 합니다. 다른 SCSM &를 사용 하 여 통합 서비스 관리 도구|

#### 대상된 가치를 독립적으로; 전달 각 **시너지** 와 기능을 보완 합니다.
