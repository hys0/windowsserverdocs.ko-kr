---
title: Azure Site Recovery를 사용 하 여 RDS의 재해 복구를 사용 하도록 설정
description: Azure Site Recovery를 사용 하 여 RDS의 재해 복구를 사용 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 05/05/2017
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.openlocfilehash: e3f9db4afb37452b4fd5d0229b385492b915fe45
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859014"
---
# <a name="enable-disaster-recovery-of-rds-using-azure-site-recovery"></a>Azure Site Recovery를 사용 하 여 RDS의 재해 복구를 사용 하도록 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016

재해 복구를 위해 RDS 배포에 적절 하 게 구성 되어 있는지을 보장 하려면 모든 RDS 배포를 구성 하는 구성 요소를 보호 해야 합니다.

- Active Directory
- SQL Server 계층
- RDS 구성 요소
- 네트워크 구성 요소
 
## <a name="configure-active-directory-and-dns-replication"></a>Active Directory 및 DNS 복제 구성

RDS 배포에 대 한 재해 복구 사이트에서 Active Directory 작동에 필요 합니다. 얼마나 복잡 RDS 배포에 따라 두 가지 선택 해야 합니다.

- 옵션 1-응용 프로그램의 작은 수 있고 단일 도메인 컨트롤러에 전체 온-프레미스 사이트를 함께 전체 사이트에 대해 실패 한 됩니다에 대 한 ASR 복제를 사용 (true 둘 다에 대 한 보조 사이트로 도메인 컨트롤러에 복제 하는 경우 사이트 간 및 사이트-Azure 시나리오).
- 옵션 2-응용 프로그램의 많은 및 Active Directory 포리스트를 실행 하는 것 장애 조치는 몇 가지 응용 프로그램 번 재해 복구 사이트에서 추가 도메인 컨트롤러를 설정 하는 경우 (보조 사이트 또는 Azure).

참조 [Active Directory 보호 및 Azure Site Recovery를 사용 하 여 DNS](/azure/site-recovery/site-recovery-active-directory) 재해 복구 사이트에서 도메인 컨트롤러를 사용할 수 있도록 대 한 자세한 내용은 합니다. 이 지침의 나머지 부분에서 이러한 단계를 수행 했다면 사용할 수 있는 도메인 컨트롤러를 가정 합니다.

## <a name="set-up-sql-server-replication"></a>SQL Server 복제 설정

참조 [SQL Server 재해 복구 및 Azure Site Recovery를 사용 하 여 SQL Server 보호](/azure/site-recovery/site-recovery-sql) SQL Server 복제를 설정 하는 단계입니다.

## <a name="enable-protection-for-the-rds-application-components"></a>RDS 응용 프로그램 구성 요소에 대 한 보호를 사용 하도록 설정

RDS 배포 유형에 따라 다양 한 구성 요소 Vm (아래 표에 나열 된)으로 Azure Site Recovery에 대 한 보호를 사용할 수 있습니다. Hyper-v 또는 VMWare Vm에 배포 되는 여부에 따라 Azure Site Recovery 관련 요소를 구성 합니다.

| 배포 유형                              | 보호 단계                                                                                                                                                                                      |
|----------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 개인용 가상 데스크톱 (관리 되지 않는)         |  1. 모든 가상화 호스트 RDVH 역할이 설치 된 준비 되는지 확인 합니다.    </br>2. 연결 브로커입니다.  </br>3. 개인 데스크톱입니다. </br>4. 골드 템플릿 Vm입니다. </br>5. 웹 액세스, 라이선스 서버와 게이트웨이 서버 |
| 풀링된 가상 데스크톱 (없습니다 UPD를 사용 하 여 관리 됨) |  1. 모든 가상화 호스트 RDVH 역할이 설치 된 준비가 되었습니다.  </br>2. 연결 브로커입니다.  </br>3. 골드 템플릿 Vm입니다. </br>4. 웹 액세스, 라이선스 서버와 게이트웨이 서버입니다.                                  |
| Remoteapp 및 데스크톱 세션 (UPD 없음)     |  1. 세션 호스트입니다.  </br>2. 연결 브로커입니다. </br>3. 웹 액세스, 라이선스 서버와 게이트웨이 서버입니다.                                                                                                          |                                                                                                                                      |

