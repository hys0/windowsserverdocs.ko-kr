---
title: 역할, 역할 서비스 및 Windows Server에서 Server Core에 없는 기능
description: 역할 및 Windows Server 용 Server Core 설치 옵션에 포함 되지 않습니다 하는 기능에 알아봅니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 308bc8a5d25e2ec67438f0ee03cbfce6f7411ca2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825534"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>역할, 역할 서비스 및 Windows Server에서 Server Core에 없는 기능

> 적용 대상: Windows Server (반기 채널) 및 Windows Server 2016

Windows Server의 Server Core 설치 옵션에서 다음 역할, 역할 서비스 및 기능 제거 되었습니다. Server Core 옵션을 사용자 환경에 작동 하는 경우를 파악 하는 데이 정보를 사용 합니다.

> [!NOTE]
> 역할, 역할 서비스의 목록을 볼 수 있습니다 하는 기능 [Server Core에 포함 된](server-core-roles-and-services.md)합니다. 이 매우 큰 목록 따라서 최상의 결과 특정 역할 또는 기능에 관심이 있다면 해당 목록을 검색 합니다.

## <a name="roles-not-in-server-core"></a>Server Core에 없는 역할

- 팩스
- MultiPointServerRole
- NPAS
- WDS

## <a name="role-services-not-in-server-core"></a>Server Core에 없는 역할 서비스
참고 (연결 브로커, 라이선스, 가상화 호스트)를 Server Core에서 일부 원격 데스크톱 역할 서비스가 포함 되어 있지만 일부는 (웹 액세스 게이트웨이 RD 세션 호스트).

- 서버-인쇄-검색
- 인터넷 인쇄
- RDS-Gateway
- RDS-RD-Server
- RDS-Web-Access
- Web-Mgmt-Console
- Web-Lgcy-Mgmt-Console
- WDS 배포
- WDS 전송 *(이전 Windows Server 버전 1803)*

## <a name="features-not-in-server-core"></a>Server Core에 없는 기능

- --Ext IIS 비트
- BitLocker-NetworkUnlock
- Direct-Play
- 인터넷 인쇄 클라이언트
- LPR-Port-Monitor
- MSMQ-Multicasting
- CMAK
- 원격 지원
- RSAT-SMTP
- RSAT-Feature-Tools-BitLocker-RemoteAdminTool
- RSAT-Bits-Server
- RSAT-NLB
- RSAT-SNMP
- RSAT-WINS
- 하이퍼-V-도구
- RSAT-RDS-Tools
- RSAT-RDS-Gateway
- RSAT-RDS-Licensing-Diagnosis-UI
- RDS-Licensing-UI
- UpdateServices-UI
- RSAT-ADCS
- RSAT-ADCS-Mgmt
- RSAT-온라인 응답자
- RSAT-ADRMS
- RSAT-Fax
- RSAT-File-Services
- RSAT-DFS-Mgmt-Con
- RSAT-FSRM-Mgmt
- RSAT-NFS-Admin
- RSAT-NPAS
- RSAT-Print-Services
- RSAT-VA-도구
- WDS-AdminPack
- SMTP-Server
- TFTP 클라이언트
- WebDAV-Redirector
- 생체 인식 프레임 워크
- Windows-Defender-Gui
- Windows-Identity-Foundation
- PowerShell-ISE
- Search-Service
- Windows-TIFF-IFilter
- 무선 네트워킹
- XPS-Viewer

