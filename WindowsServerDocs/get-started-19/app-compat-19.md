---
title: Windows Server 2019 및 Microsoft 서버 애플리케이션 호환성
description: Windows Server 2019 및 Microsoft 서버 애플리케이션의 호환성 표
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66442374"
---
# <a name="windows-server-2019-and-microsoft-server-application-compatibility"></a>Windows Server 2019 및 Microsoft 서버 애플리케이션 호환성

>적용 대상: 시작

다음 표는 Window Server 2019에서 설치 및 기능을 지원하는 Microsoft 서버 애플리케이션 목록을 보여 줍니다. 이 정보는 빠른 참조를 위한 것이며 개별 제품 사양, 요구 사항, 알림 또는 각 개별 서버 응용 프로그램에 대한 일반적인 전달 사항을 대체하지 않습니다. 호환성 및 옵션을 완전히 이해하려는 경우 각 제품에 대한 공식 설명서를 참조하세요.

타사 애플리케이션과의 Windows Server 호환성에 대한 자세한 내용을 원하는 소프트웨어 공급업체 파트너인 경우 [Windows Server 로고 인증 포털](https://commercialappcertification.microsoft.com/)을 방문하세요.

| **제품**                                                  | **Server Core에서 지원**             |   | **데스크톱 환경을 포함하는 서버에서 지원** | **릴리스 여부** |   | **제품 웹 링크**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | 예                                      |   | 예                                             | 예           |   | [Exchange Server 시스템 요구 사항](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integration Server 2016, CU3                            | 예                                      |   | 예                                             | 예            |   | [Host Integration Server 시스템 요구 사항](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | 예\*                                    |   | 예                                             | 예           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | 예\*                                    |   | 예                                             | 예           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | 예\*                                    |   | 예                                             | 예           |   | [SQL Server 2014 설치에 대한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | 예\*                                    |   | 예                                             | 예           |   | [SQL Server 2016 설치에 대한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | 예\*                                    |   | 예                                             | 예           |   | [SQL Server 2017 설치에 대한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager(버전 1806) | 관리형 클라이언트의 경우 예, 사이트 서버의 경우 아니요 |   | 관리형 클라이언트의 경우 예, 사이트 서버의 경우 아니요        | 예           |   | [System Center Configuration Manager 버전 1806의 새로운 기능](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | 예\*                                    |   | 예                                             | 예           |   | [System Center Operations Manager 시스템 요구 사항](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | 예\*                                    |   | 예                                             | 예           |   | [System Center Virtual Machine Manager 시스템 요구 사항](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | 아니오                                       |   | 예                                             | 예           |   | [System Center Data Protection Manager에 대한 환경 준비](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint Server 2016                                       | 아니오                                       |   | 예                                             | 예           |   | [SharePoint Server 2016에 대한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | 아니오                                       |   | 예                                             | 예           |   | [SharePoint Server 2019에 대한 하드웨어 및 소프트웨어 요구 사항](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | 아니오                                       |   | 예                                             | 예           |   | [Project Server 2016에 대한 소프트웨어 요구 사항](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Project Server 2019                                          | 아니오                                       |   | 예                                             | 예           |   | [Project Server 2019에 대한 소프트웨어 요구 사항](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| 비즈니스용 Skype 2019                                      | 아니오                                       |   | 예                                             | 예           |   | [비즈니스용 Skype 서버의 설치 요구 사항](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*제한 사항이 있거나 [Server Core 앱 호환성 FOD(Feature on Demand)](install-fod-19.md)가 필요할 수 있습니다.
특정 제품 또는 해당 FOD 설명서를 참조하세요.
