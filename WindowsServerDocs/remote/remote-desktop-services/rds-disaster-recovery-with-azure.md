---
title: Azure 재해 복구를 사용 하 여 RDS에 대 한 재해 복구 설정
description: RDS 배포에 대 한 재해 복구를 위한 Azure 재해 복구를 사용 하는 방법 알아보기
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 06/12/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 561a515e23d12cc3397c40fd885550e735ed4d27
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878174"
---
# <a name="set-up-disaster-recovery-for-rds-using-azure-site-recovery"></a>Azure Site Recovery를 사용 하 여 RDS에 대 한 재해 복구 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 데스크톱 서비스 배포에 대 한 재해 복구 솔루션을 만드는 Azure Site Recovery를 사용할 수 있습니다. 

[Azure Site Recovery](/azure/site-recovery/site-recovery-overview) 복제, 장애 조치 및 virtual machines의 복구를 오케스트레이션 하 여 재해 복구 기능을 제공 하는 Azure 기반 서비스입니다. Azure Site Recovery는 다양 한 가상 머신을 장애 조치 및 응용 프로그램을 개인/공개 또는 호스팅 서비스 공급자의 클라우드 원활 하 게 일관 되 게 복제 하 고, 보호, 복제 기술을 지원 합니다. 

다음 정보를 사용 하 여 재해 복구 솔루션의 유효성을 검사 합니다.

## <a name="disaster-recovery-deployment-options"></a>재해 복구 배포 옵션

Hyper-v 또는 VMWare를 실행 중인 가상 컴퓨터 또는 물리적 서버에서 RDS를 배포할 수 있습니다. Azure Site Recovery는 온-프레미스와 Azure 또는 보조 사이트로 가상 배포를 모두 보호할 수 있습니다. 다음 표에서 다양 한 사이트 간 및 사이트에서 Azure로 재해 recvoery 시나리오에서 RDS 배포를 지원 합니다.

| 배포 유형                          | Hyper-v 사이트 및 사이트 간 | Hyper-v 사이트-Azure | VMWare 사이트-Azure | 실제 사이트-Azure |
|------------------------------------------|----------------------|-----------------------|---------------------|----------------------|-----------------------|------------------------|
| 풀링된 가상 데스크톱 (관리 되지 않는)       |예|아니오|아니요|아니요 |
| 풀링된 가상 데스크톱 (관리, UPD 없음) | 예|아니오|아니요|아니오|
| Remoteapp 및 데스크톱 세션 (UPD 없음) | 예|예|예|예  |

## <a name="prerequisites"></a>사전 요구 사항

배포를 위한 Azure Site Recovery를 구성할 수 있습니다, 전에 다음 요구 사항을 충족 하는지 확인 합니다.

- 만들기는 [온-프레미스 RDS 배포](rds-deploy-infrastructure.md)합니다.
- 추가 [Azure Site Recovery Services 자격 증명 모음](/azure/site-recovery/site-recovery-vmm-to-azure#create-a-recovery-services-vault) Microsoft Azure 구독에 있습니다.
- 복구 사이트로 Azure를 사용 하려는 경우 실행 합니다 [Azure Virtual Machine Readiness Assessment 도구](https://azure.microsoft.com/downloads/vm-readiness-assessment/) 에서 Vm을 Azure Vm 및 Azure Site Recovery Services와 호환 되는지를 확인 합니다.
 
## <a name="implementation-checklist"></a>구현 검사 목록

보다 세부적으로 RDS 배포에 대 한 Azure Site Recovery Services를 사용 하도록 설정 하는 다양 한 단계를 다룹니다 하지만 높은 수준의 구현 단계는 다음과 같습니다.

| **1 단계-재해 복구를 위한 Vm 구성**                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 하이퍼-V-Microsoft Azure Site Recovery Provider 다운로드 합니다. VMM 서버 또는 Hyper-v 호스트에 설치 합니다. 참조 [Azure Site Recovery를 사용 하 여 Azure로 복제를 위한 필수 구성 요소](/azure/site-recovery/site-recovery-prereq) 정보에 대 한 합니다.                                                                                                                             |
| VMWare 서버 보호를 구성 서버 및 마스터 대상 서버를 구성 합니다.                                                                                                                                                      |
| **2 단계-리소스 준비**                                                                                                                                                                                                           |
| 추가 된 [Azure Storage 계정](/azure/storage/storage-create-storage-account)합니다.                                                                                                                                                                                                              |
| 하이퍼-V-Microsoft Azure Recovery Services 에이전트를 다운로드 하 고 Hyper-v 호스트 서버에 설치 합니다.                                                                                                                                     |
| VMWare-모든 Vm에 모바일 서비스가 설치 되어 있는지 확인 합니다.                                                                                                                                                                           |
| [VMM 클라우드, Hyper-v 사이트 또는 VMWare 사이트에서 Vm에 대 한 보호를 사용 하도록 설정](rds-enable-dr-with-asr.md)합니다.                                                                                                                                                                    |
| **3 단계-복구 계획을 디자인 합니다.**                                                                                                                                                                                                        |
| 리소스를-Azure Vnet에 맵 온-프레미스 네트워크에 매핑하십시오.                                                                                                                                                                              |
| [복구 계획을 만들](rds-disaster-recovery-plan.md)합니다. |
| 테스트 장애 조치를 만들어 복구 계획을 테스트 합니다. 모든 Vm에는 Active Directory와 같은 필요한 리소스에 액세스할 수 있는지 확인 합니다. 리디렉션 구성 된 네트워크 및 rds.에 대 한 작업 확인 복구 계획 테스트는 자세한 단계를 참조 하세요. [테스트 장애 조치 실행](/azure/site-recovery/site-recovery-test-failover-to-azure)|
| **4 단계-재해 복구 훈련을 실행 합니다.**                                                                                                                                                                                                     |
| 계획 되거나 계획 되지 않은 장애 조치를 사용 하 여 재해 복구 훈련을 실행 합니다. 모든 Vm에 Active Directory와 같은 필요한 리소스에 액세스할 수 있는지 확인 합니다. 모든 Vm에 Active Directory와 같은 필요한 리소스에 액세스할 수 있는지 확인 합니다. 장애 조치 및 훈련을 실행 하는 방법에 대 한 자세한 단계를 참조 하세요 [Site Recovery에서 장애 조치](/azure/site-recovery/site-recovery-failover)합니다.|


