---
title: 역할, 역할 서비스 및 Windows Server-Server Core에 없는 기능
description: 역할 및 Windows Server의 Server Core 설치 옵션에 포함 되지 않은 기능을 소개 합니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 308bc8a5d25e2ec67438f0ee03cbfce6f7411ca2
ms.sourcegitcommit: 4b9b21ca1f366388a78ead7413cb581f2b23d4c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/09/2018
ms.locfileid: "2604791"
---
# 역할, 역할 서비스 및 Windows Server-Server Core에 없는 기능

> 적용 대상: Windows Server (세미콜론 연간 회의 채널) 및 Windows Server 2016

Windows Server의 Server Core 설치 옵션에서 다음 역할, 역할 서비스 및 기능이 제거 되었습니다. Server Core 옵션 환경에 대해 작동 하는 경우 포트당를이 정보를 사용 합니다.

> [!NOTE]
> 복사본을 [Server Core에 포함 된](server-core-roles-and-services.md)해당 역할, 역할 서비스 및 기능 목록의 볼 수 있습니다. 이 매우 큰 목록 있으므로 최상의 결과 특정 역할 또는 기능에 관심이 대 한 해당 그룹을 검색 합니다.

## Server Core에 없는 역할

- 팩스
- MultiPointServerRole
- NPAS
- WDS

## Server Core에 없는 역할 서비스
다른 사용자에 게는 아니지만 일부 원격 데스크톱 역할 서비스 (연결 브로커, 라이선스, 가상화 호스트), Server Core에 포함 되었는지 여부를 지정 하는 메모 (게이트웨이, RD 세션 호스트 Web Access).

- 인쇄-스캔-서버
- 인터넷 인쇄
- RDS 게이트웨이
- RDS RD 서버
- RDS 웹 액세스
- 웹 관리 콘솔
- 웹 Lgcy-관리 콘솔
- WDS 배포
- *Windows Server 버전 1803) (이전* WDS 전송

## Server Core에 없는 기능

- 비트-IIS-Ext
- BitLocker NetworkUnlock
- 직접 재생
- 인터넷 인쇄 클라이언트
- LPR 포트 모니터
- MSMQ 멀티 캐스팅
- CMAK
- 원격 지원
- RSAT SMTP
- RSAT-기능-도구-BitLocker-RemoteAdminTool
- RSAT 비트 서버
- RSAT NLB
- RSAT SNMP
- RSAT WINS
- 하이퍼-V-도구
- RSAT-RDS-도구
- RSAT-RDS 게이트웨이
- RSAT-RDS-라이선스-진단-UI
- RDS 라이선스 UI
- UpdateServices UI
- RSAT ADC
- RSAT-ADC-관리
- 온라인 응답자 RSAT
- RSAT ADRMS
- RSAT 팩스
- RSAT-파일-서비스
- DFS 관리 사기 RSAT
- RSAT-FSRM-관리
- RSAT NFS 관리자
- RSAT NPAS
- RSAT-인쇄-서비스
- RSAT-VA-도구
- WDS AdminPack
- SMTP 서버
- TFTP 클라이언트
- WebDAV 리디렉터
- 생체 인식 프레임 워크
- Windows Defender Gui
- Windows-Identity-Foundation
- PowerShell ISE
- 검색 서비스
- Windows-TIFF-IFilter
- 무선 네트워킹
- XPS 뷰어

