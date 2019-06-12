---
title: Windows Server 2019 및 Microsoft Server application 호환성
description: Windows Server 2019 및 Microsoft 서버 응용 프로그램에 대 한 호환성 표
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
ms.openlocfilehash: 8dcaff6ab8a296790158f59035bd4a5c1a093cbd
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442374"
---
# <a name="windows-server-2019-and-microsoft-server-application-compatibility"></a>Windows Server 2019 및 Microsoft Server application 호환성

>적용 대상: Windows Server 2019

이 표에서 창 Server 2019에 설치 및 기능을 지 원하는 Microsoft 서버 응용 프로그램을 나열 합니다. 이 정보는 빠른 참조를 위한 것이며 개별 제품 사양, 요구 사항, 알림 또는 각 개별 서버 응용 프로그램에 대한 일반적인 전달 사항을 대체하지 않습니다. 호환성 및 옵션을 완전히 이해하려는 경우 각 제품에 대한 공식 설명서를 참조하세요.

타사 응용 프로그램을 사용 하 여 Windows Server 호환성에 대 한 자세한 내용은 소프트웨어 공급 업체 파트너 라면 방문 합니다 [상용 응용 프로그램 인증 포털](https://commercialappcertification.microsoft.com/)합니다.

| **Product**                                                  | **Server Core에서 지원**             |   | **데스크톱 환경 포함 서버 지원** | **출시?** |   | **제품 웹 링크**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | 예                                      |   | 예                                             | 예           |   | [Exchange Server 시스템 요구 사항](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integration Server 2016 CU3                            | 예                                      |   | 예                                             | 예            |   | [호스트 Integration Server에 대 한 시스템 요구 사항](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | 예\*                                    |   | 예                                             | 예           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | 예\*                                    |   | 예                                             | 예           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | 예\*                                    |   | 예                                             | 예           |   | [SQL Server 2014 설치를 위한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | 예\*                                    |   | 예                                             | 예           |   | [SQL Server 2016 설치를 위한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | 예\*                                    |   | 예                                             | 예           |   | [Hardware and Software Requirements for Installing SQL Server 2017](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (버전 1806) | 사이트 서버와 더 관리 되는 클라이언트로 예 |   | 사이트 서버와 더 관리 되는 클라이언트로 예        | 예           |   | [System Center Configuration Manager의 1806 버전의 새로운 기능](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | 예\*                                    |   | 예                                             | 예           |   | [System Center Operations Manager에 대 한 시스템 요구 사항](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | 예\*                                    |   | 예                                             | 예           |   | [System Center Virtual Machine Manager 대 한 시스템 요구 사항](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | 아니요                                       |   | 예                                             | 예           |   | [System Center Data Protection Manager에 대 한 환경 준비](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint Server 2016                                       | 아니요                                       |   | 예                                             | 예           |   | [SharePoint Server 2016에 대 한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | 아니오                                       |   | 예                                             | 예           |   | [SharePoint Server 2019에 대 한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | 아니요                                       |   | 예                                             | 예           |   | [Project Server 2016에 대 한 소프트웨어 요구 사항](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Project Server 2019                                          | 아니요                                       |   | 예                                             | 예           |   | [프로젝트 서버 2019에 대 한 소프트웨어 요구 사항](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| 비즈니스 2019 Skype                                      | 아니요                                       |   | 예                                             | 예           |   | [Business Server 용 Skype에 대 한 필수 구성 요소를 설치 합니다.](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*제한 될 수 또는 필요할 수 있습니다 합니다 [Server Core 응용 프로그램 호환성 기능에서 FOD (주문형)](install-fod-19.md)합니다.
특정 제품 또는 해당 FOD 설명서를 참조 하십시오.
