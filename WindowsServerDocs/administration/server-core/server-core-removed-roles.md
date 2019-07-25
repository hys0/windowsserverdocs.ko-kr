---
title: Windows Server에서 제공 하지 않는 역할, 역할 서비스 및 기능-Server Core
description: Windows Server의 Server Core 설치 옵션에 포함 되지 않은 역할 및 기능에 대해 알아봅니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: ce5107e8e0ab573df7588428db65c8b223cf1f13
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476511"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>Windows Server에서 제공 하지 않는 역할, 역할 서비스 및 기능-Server Core

> 적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

Windows Server의 Server Core 설치 옵션에서 다음 역할, 역할 서비스 및 기능이 제거 되었습니다. 이 정보를 사용 하 여 사용자 환경에 대 한 Server Core 옵션이 작동 하는지 파악할 수 있습니다.

> [!NOTE]
> [Server Core에 포함](server-core-roles-and-services.md)된 역할, 역할 서비스 및 기능 목록을 볼 수도 있습니다. 매우 큰 목록이 며, 최상의 결과를 위해 원하는 특정 역할이 나 기능에 해당 하는 목록을 검색 합니다.

## <a name="roles-not-in-server-core"></a>Server Core에 없는 역할

- 팩스
- MultiPointServerRole
- NPAS
- APPEND

## <a name="role-services-not-in-server-core"></a>Server Core에 없는 역할 서비스
일부 원격 데스크톱 역할 서비스는 Server Core (연결 브로커, 라이선스, 가상화 호스트)에 포함 되지만 다른 사용자 (게이트웨이, RD 세션 호스트, 웹 액세스)는 포함 되지 않습니다.

- 인쇄-스캔-서버
- 인쇄-인터넷
- RDS-게이트웨이
- RDS-서버
- RDS-웹 액세스
- 웹 관리 콘솔
- Lgcy-콘솔
- WDS-배포
- WDS-Transport *(Windows Server 버전 1803 이전)*

## <a name="features-not-in-server-core"></a>Server Core에 없는 기능

- 비트-IIS-Ext
- BitLocker-네트워크 잠금 해제
- 직접 재생
- 인터넷-인쇄-클라이언트
- LPR 포트 모니터
- MSMQ-멀티 캐스팅
- CMAK
- 원격 지원
- RSAT-SMTP
- RSAT-RemoteAdminTool
- RSAT-서버
- RSAT-NLB
- RSAT-SNMP
- RSAT-WINS
- Hyper-v-도구
- RSAT-RDS-도구
- RSAT-RDS-게이트웨이
- RSAT-RDS-진단-UI
- RDS-라이선스-UI
- Updateservices-api-UI
- RSAT-ADCS
- RSAT-ADCS-관리
- RSAT-온라인-응답기
- RSAT-ADRMS
- RSAT-팩스
- RSAT-파일-서비스
- RSAT-DFS-관리-Con
- RSAT-FSRM-관리
- RSAT-NFS-관리자
- RSAT-NPAS
- RSAT-인쇄 서비스
- RSAT-VA-도구
- WDS-AdminPack
- SMTP-서버
- TFTP-클라이언트
- WebDAV-리디렉터
- 생체 인식-프레임 워크
- Windows-Defender-Gui
- Windows-Identity-Foundation
- PowerShell-ISE
- 검색-서비스
- Windows-TIFF-IFilter
- 무선-네트워킹
- XPS 뷰어

