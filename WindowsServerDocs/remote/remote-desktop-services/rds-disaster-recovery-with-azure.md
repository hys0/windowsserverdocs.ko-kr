---
title: Azure 재해 복구를 사용하여 RDS에 대해 재해 복구 설정
description: RDS 배포의 재해 복구에 Azure 재해 복구를 사용하는 방법 알아보기
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 06/12/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: 514262fde3b433baf89fe8f5a0cf8b04ef267354
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387540"
---
# <a name="set-up-disaster-recovery-for-rds-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 RDS에 대해 재해 복구 설정

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

Azure Site Recovery를 사용하여 원격 데스크톱 서비스 배포를 위한 재해 복구 솔루션을 만들 수 있습니다. 

[Azure Site Recovery](/azure/site-recovery/site-recovery-overview)는 가상 머신의 복제, 장애 조치(failover) 및 복구를 오케스트레이션하여 재해 복구 기능을 제공하는 Azure 기반 서비스입니다. Azure Site Recovery는 다양한 가상 머신 및 애플리케이션을 프라이빗/퍼블릭 또는 호스터 클라우드로 일관되게 복제하고, 보호하며, 원활하게 장애 조치(failover)하기 위한 다양한 복제 기술을 지원합니다. 

다음 정보를 사용하여 재해 복구 솔루션을 만들고 유효한지 검사합니다.

## <a name="disaster-recovery-deployment-options"></a>재해 복구 배포 옵션

Hyper-V 또는 VMWare를 실행 중인 가상 머신 또는 물리적 서버에서 RDS를 배포할 수 있습니다. Azure Site Recovery는 보조 사이트 또는 Azure로의 온-프레미스 및 가상 배포를 둘 다 보호할 수 있습니다. 다음 표에서는 사이트 간 및 사이트에서 Azure로의 재해 복구 시나리오에서 지원되는 다양한 RDS 배포를 보여 줍니다.

| 배포 유형                          | Hyper-V 사이트 간 | Hyper-V 사이트와 Azure 간 | VMWare 사이트와 Azure 간 | 물리적 사이트와 Azure 간 |
|------------------------------------------|----------------------|-----------------------|---------------------|----------------------|-----------------------|------------------------|
| 풀링된 가상 데스크톱(비관리형)       |예|아니오|아니오|아니오 |
| 풀링된 가상 데스크톱(관리형, UPD 없음) | 예|아니오|아니오|아니오|
| RemoteApp 및 데스크톱 세션(UPD 없음) | 예|예|예|예  |

## <a name="prerequisites"></a>필수 구성 요소

배포를 위해 Azure Site Recovery를 구성하려면 먼저 다음 요구 사항을 충족해야 합니다.

- [온-프레미스 RDS 배포](rds-deploy-infrastructure.md)를 만듭니다.
- [Azure Site Recovery Services 자격 증명 모음](/azure/site-recovery/site-recovery-vmm-to-azure#create-a-recovery-services-vault)을 Microsoft Azure 구독에 추가합니다.
- Azure를 복구 사이트로 사용하려는 경우 VM에서 [Azure Virtual Machine Readiness Assessment 도구](https://azure.microsoft.com/downloads/vm-readiness-assessment/)를 실행하여 Azure VMM 및 Azure Site Recovery Services와 호환되는지 확인합니다.
 
## <a name="implementation-checklist"></a>구현 검사 목록

나중에 RDS 배포를 위해 Azure Site Recovery Services를 사용하도록 설정하는 다양한 단계를 다루겠지만 여기서는 개괄적인 구현 단계를 설명합니다.

| **1단계 - 재해 복구를 위해 VM 구성**                                                                                                                                                                                               |
|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Hyper-V - Microsoft Azure Site Recovery Provider를 다운로드합니다. VMM 서버 또는 Hyper-V 호스트에 설치합니다. 자세한 내용은 [Azure Site Recovery를 사용하여 Azure로 복제하기 위한 필수 구성 요소](/azure/site-recovery/site-recovery-prereq)를 참조하세요.                                                                                                                             |
| VMWare - 보호 서버, 구성 서버 및 마스터 대상 서버 구성                                                                                                                                                      |
| **2단계 - 리소스 준비**                                                                                                                                                                                                           |
| [Azure Storage 계정](/azure/storage/storage-create-storage-account)을 추가합니다.                                                                                                                                                                                                              |
| Hyper-V - Microsoft Azure Recovery Services 에이전트를 다운로드하고 Hyper-V 호스트 서버에 설치합니다.                                                                                                                                     |
| VMWare - 모든 VM에 모바일 서비스가 설치되어 있는지 확인합니다.                                                                                                                                                                           |
| [VMM 클라우드, Hyper-V 사이트 또는 VMWare 사이트에서 VM에 대한 보호를 사용하도록 설정](rds-enable-dr-with-asr.md)합니다.                                                                                                                                                                    |
| **3단계 - 복구 계획 디자인**                                                                                                                                                                                                        |
| 리소스 매핑 - Azure VNET에 온-프레미스 네트워크를 매핑합니다.                                                                                                                                                                              |
| [복구 계획을 만듭니다](rds-disaster-recovery-plan.md). |
| 테스트 장애 조치(failover)를 만들어 복구 계획을 테스트합니다. 모든 VM이 Active Directory와 같은 필수 리소스에 액세스할 수 있는지 확인합니다. 네트워크 리디렉션이 RDS에 대해 구성되고 작동 중인지 확인합니다. 복구 계획 테스트에 대한 자세한 단계는 [테스트 장애 조치(failover) 실행](/azure/site-recovery/site-recovery-test-failover-to-azure)을 참조하세요.|
| **4단계 - 재해 복구 드릴 실행.**                                                                                                                                                                                                     |
| 계획되었거나 계획되지 않은 장애 조치(failover)를 사용하여 재해 복구 드릴을 실행합니다. 모든 VM이 Active Directory와 같은 필수 리소스에 액세스할 수 있는지 확인합니다. 모든 VM이 Active Directory와 같은 필수 리소스에 액세스할 수 있는지 확인합니다. 장애 조치(failover) 및 드릴을 실행하는 방법에 대한 자세한 단계는 [Site Recovery의 장애 조치(failover)](/azure/site-recovery/site-recovery-failover)를 참조하세요.|


