---
title: Azure Site Recovery를 사용하여 RDS의 재해 복구를 사용하도록 설정
description: Azure Site Recovery를 사용하여 RDS의 재해 복구를 사용하도록 설정하는 방법을 알아봅니다.
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
ms.openlocfilehash: 7aa25602c71e5d114be7ae59c5e3ce168844d700
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66446553"
---
# <a name="enable-disaster-recovery-of-rds-using-azure-site-recovery"></a>Azure Site Recovery를 사용하여 RDS의 재해 복구를 사용하도록 설정

>적용 대상: Windows Server(반기 채널), Windows Server 2019, Windows Server 2016

RDS 배포가 재해 복구를 위해 적절하게 구성되었는지 확인하려면 RDS 배포를 구성하는 모든 구성 요소를 보호해야 합니다.

- Active Directory
- SQL Server 계층
- RDS 구성 요소
- 네트워크 구성 요소

## <a name="configure-active-directory-and-dns-replication"></a>Active Directory 및 DNS 복제 구성

RDS 배포가 작동하려면 재해 복구 사이트에 Active Directory가 필요합니다. RDS 배포가 얼마나 복잡한지에 따라 두 가지 선택이 가능합니다.

- 옵션 1 - 전체 온-프레미스 사이트에 대해 적은 수의 애플리케이션과 단일 도메인 컨트롤러가 있고 전체 사이트에서 함께 장애가 발생할 경우 ASR-복제를 사용하여 도메인 컨트롤러를 보조 사이트에 복제합니다(사이트 간 및 사이트-Azure 시나리오 모두에 해당).
- 옵션 2 - 많은 수의 애플리케이션이 있고 Active Directory 포리스트를 실행 중이며 한 번에 몇 개의 애플리케이션을 장애 조치(failover)할 경우 재해 복구 사이트(보조 사이트 또는 Azure)에 추가 도메인 컨트롤러를 설정합니다.

재해 복구 사이트에서 도메인 컨트롤러를 사용할 수 있도록 설정하는 자세한 내용은 [Azure Site Recovery를 사용하여 Active Directory 및 DNS 보호](/azure/site-recovery/site-recovery-active-directory)를 참조하세요. 이 지침의 나머지 부분에 대해서는 해당 단계를 따랐으며 도메인 컨트롤러를 사용할 수 있다고 가정합니다.

## <a name="set-up-sql-server-replication"></a>SQL Server 복제 설정

SQL Server 복제를 설정하는 단계는 [SQL Server 재해 복구 및 Azure Site Recovery를 사용한 SQL Server 보호](/azure/site-recovery/site-recovery-sql)를 참조하세요.

## <a name="enable-protection-for-the-rds-application-components"></a>RDS 애플리케이션 구성 요소에 대한 보호를 사용하도록 설정

RDS 배포 유형에 따라 Azure Site Recovery의 여러 구성 요소 VM(아래 표 참조)에 대해 보호를 사용하도록 설정할 수 있습니다. VM이 Hyper-V에 배포되었는지, 또는 VMWare에 배포되었는지에 따라 관련 Azure Site Recovery 요소를 구성합니다.


|               배포 유형                |                                                                                                     보호 단계                                                                                                     |
|----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     개인용 가상 데스크톱(비관리형)     | 1. RDVH 역할이 설치된 상태에서 모든 가상화 호스트가 준비되었는지 확인합니다.    </br>2. 연결 브로커  </br>3. 개인 데스크톱 </br>4. 골드 템플릿 VM </br>5. 웹 액세스, 라이선스 서버 및 게이트웨이 서버 |
| 풀링된 가상 데스크톱(관리형, UPD 없음) |                    1. RDVH 역할이 설치된 상태에서 모든 가상화 호스트가 준비됩니다.  </br>2. 연결 브로커  </br>3. 골드 템플릿 VM </br>4. 웹 액세스, 라이선스 서버 및 게이트웨이 서버.                    |
|   RemoteApp 및 데스크톱 세션(UPD 없음)   |                                                          1. 세션 호스트  </br>2. 연결 브로커 </br>3. 웹 액세스, 라이선스 서버 및 게이트웨이 서버.                                                           |

