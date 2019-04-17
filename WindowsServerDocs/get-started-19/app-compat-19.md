---
title: Windows Server 2019 및 Microsoft Server application 호환성
description: Windows Server 2019 및 Microsoft 서버 응용 프로그램 호환성 표
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2afe7c32-1fda-4441-989b-4115dabdcd34
author: coreyp
ms.author: coreyp-at-msft
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: e8bb8cda003ca151216e3b86d5884dfd05e73e6d
ms.sourcegitcommit: 5d55c3ebd1ceee7229ea9a9989c69cf93757ed88
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2019
ms.locfileid: "9256946"
---
# Windows Server 2019 및 Microsoft Server application 호환성

>적용 대상: WindowsServer 2019

이 표에서 Microsoft 서버 응용 프로그램 지원 Window Server 2019에서 설치 및 기능을 보여 줍니다. 이 정보는 빠른 참조를 위한 것이며 개별 제품 사양, 요구 사항, 알림 또는 각 개별 서버 응용 프로그램에 대한 일반적인 전달 사항을 대체하지 않습니다. 호환성 및 옵션을 완전히 이해하려는 경우 각 제품에 대한 공식 설명서를 참조하세요.

Microsoft가 아닌 타사 응용 프로그램과 Windows Server 호환성에 대 한 자세한 정보를 찾고 소프트웨어 공급 업체 파트너 인 경우 [상용 앱 인증 포털](https://commercialappcertification.microsoft.com/)을 방문 하세요.
| **제품**                                                  | **Server Core에서 지원**             |   | **데스크톱 환경 포함 서버에서 지원** | **릴리스 여부** |   | **제품 웹 링크**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | 예                                      |   | 예                                             | 예           |   | [Exchange Server 시스템 요구 사항](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integration Server 2016 CU3                            | 예                                      |   | 예                                             | 아니요            |   | [호스트 Integration Server 시스템 요구 사항](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | Yes\ *                                    |   | 예                                             | 예           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | Yes\ *                                    |   | 예                                             | 예           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | Yes\ *                                    |   | 예                                             | 예           |   | [SQL Server 2014 설치에 대한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | Yes\ *                                    |   | 예                                             | 예           |   | [하드웨어 및 SQL Server 2016을 설치 하기 위한 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | Yes\ *                                    |   | 예                                             | 예           |   | [하드웨어 및 SQL Server 2017을 설치 하기 위한 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (버전 1806) | 사이트 서버와 더 관리 되는 클라이언트 예 |   | 사이트 서버와 더 관리 되는 클라이언트 예        | 예           |   | [버전 1806 System Center Configuration Manager의에서 새로운 기능](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | Yes\ *                                    |   | 예                                             | 예           |   | [System Center Operations Manager에 대 한 시스템 요구 사항](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | Yes\ *                                    |   | 예                                             | 예           |   | [System Center 가상 컴퓨터 Manager에 대 한 시스템 요구 사항](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | 아니요                                       |   | 예                                             | 예           |   | [System Center Data Protection Manager에 대 한 환경 준비](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint Server 2016                                       | 아니요                                       |   | 예                                             | 예           |   | [SharePoint Server 2016에 대한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | 아니요                                       |   | 예                                             | 예           |   | [SharePoint Server 2019에 대 한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | 아니요                                       |   | 예                                             | 예           |   | [Project Server 2016에 대한 소프트웨어 요구 사항](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Project Server 2019                                          | 아니요                                       |   | 예                                             | 예           |   | [프로젝트 Server 2019에 대 한 소프트웨어 요구 사항](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| 비즈니스 2019 Skype                                      | 아니요                                       |   | 예                                             | 예           |   | [비즈니스 서버에 대 한 Skype에 대 한 필수 구성 요소 설치](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*May 제한이 또는 필요할 합니다 [Server Core 앱 호환성 Feature on Demand (FOD). ](install-fod-19.md)
특정 제품 또는 FOD 설명서를 참조 하십시오.
