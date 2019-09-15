---
title: Windows Server에서 제공 하지 않는 역할, 역할 서비스 및 기능-Server Core
description: Windows Server의 Server Core 설치 옵션에 포함 되지 않은 역할 및 기능에 대해 알아봅니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: 882410792c7b8df8a8275c357d64fc17c9f3479e
ms.sourcegitcommit: feec5cbe983c8c5800ccd4fc214914084fcceaba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/13/2019
ms.locfileid: "70975256"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>Windows Server에서 제공 하지 않는 역할, 역할 서비스 및 기능-Server Core

> 적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

Windows Server의 Server Core 설치 옵션에서 다음 역할, 역할 서비스 및 기능이 제거 되었습니다. 이 정보를 사용 하 여 사용자 환경에 대 한 Server Core 옵션이 작동 하는지 파악할 수 있습니다.

> [!NOTE]
> [Server Core에 포함](server-core-roles-and-services.md)된 역할, 역할 서비스 및 기능 목록을 볼 수도 있습니다. 매우 큰 목록이 며, 최상의 결과를 위해 원하는 특정 역할이 나 기능에 해당 하는 목록을 검색 합니다.

## <a name="roles-not-in-server-core"></a>Server Core에 없는 역할

- 팩스 서버 (**팩스**)
- MultiPoint 서비스 (**MultiPointServerRole**)
- **NPAS**(네트워크 정책 및 액세스 서비스)
- Windows 배포 서비스 (**WDS**) *(Windows Server 버전 1803 이전)*

## <a name="role-services-not-in-server-core"></a>Server Core에 없는 역할 서비스
일부 원격 데스크톱 역할 서비스는 Server Core (연결 브로커, 라이선스, 가상화 호스트)에 포함 되지만 다른 사용자 (게이트웨이, RD 세션 호스트, 웹 액세스)는 포함 되지 않습니다.

- 인쇄 및 문서 서비스 \ 분산된 스캔 서버 (**인쇄-스캔-서버**)
- 인쇄 및 문서 서비스 \ 인터넷 인쇄 (**인쇄-인터넷**)
- 원격 데스크톱 서비스 \ 원격 데스크톱 게이트웨이 (**RDS-게이트웨이**)
- 원격 데스크톱 서비스 \ 원격 데스크톱 세션 호스트 (**RDS-서버**)
- 원격 데스크톱 서비스 \ 원격 데스크톱 웹 액세스 (**RDS-웹 액세스**)
- 역할 서비스 웹 서버 (IIS) \ 관리 도구 \ IIS 관리 콘솔 (**웹**관리 콘솔)
- 역할 서비스 웹 서버 (IIS) \ 관리 도구 \ IIS 6 관리 호환성 \ IIS 6 관리 콘솔 (**Lgcy**)
- Windows 배포 서비스 \ 배포 서버 (**WDS 배포**)
- Windows 배포 서비스 \ 전송 서버 (**WDS-전송**) *(Windows Server 버전 1803 이전)*

## <a name="features-not-in-server-core"></a>Server Core에 없는 기능
- Background Intelligent Transfer Service (비트) \ IIS 서버 확장 (**비트-iis-Ext**)
- BitLocker 네트워크 잠금 해제 (**bitlocker-네트워크 잠금 해제**)
- 직접 재생 (**직접 재생**)
- 인터넷 인쇄 클라이언트 (**인터넷-인쇄-클라이언트**)
- LPR 포트 모니터 (**Lpr 포트 모니터**)
- 메시지 큐 \ 메시지 큐 서비스 \ 멀티 캐스팅 지원 (**MSMQ-멀티 캐스트**)
- RAS**CMAK**(연결 관리자 관리 키트)
- 원격 지원 (**원격 지원**)
- 원격 서버 관리 도구 \ 기능 관리 도구 \ SMTP 서버 도구 (**RSAT-smtp**)
- 원격 서버 관리 도구 \ 기능 관리 도구 \ BitLocker 드라이브 암호화 관리 유틸리티 \ BitLocker 드라이브 암호화 도구 (**RSAT-RemoteAdminTool**)
- 원격 서버 관리 도구 \ 기능 관리 도구 \ BITS 서버 확장 도구 (**RSAT-서버**)
- 원격 서버 관리 도구 \ 기능 관리 도구 \ 네트워크 부하 분산 도구 (**RSAT-NLB**)
- 원격 서버 관리 도구 \ 기능 관리 도구 \ SNMP 도구 (**RSAT-snmp**)
- 원격 서버 관리 도구 \ 기능 관리 도구 \ WINS 서버 도구 (**RSAT-wins**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ Hyper-v 관리 도구 \ hyper-v GUI 관리 도구 (**hyper-v-도구**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 원격 데스크톱 서비스 도구 \ 원격 데스크톱 게이트웨이 도구 (**RSAT-RDS-tools**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 원격 데스크톱 서비스 도구 \ 원격 데스크톱 게이트웨이 도구 (**RSAT-RDS-게이트웨이**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 원격 데스크톱 서비스 도구 \ 원격 데스크톱 라이선싱 진단 도구 도구 (**RSAT-RDS-라이선스-진단-UI**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 원격 데스크톱 서비스 도구 \ 원격 데스크톱 라이선싱 도구 (**RDS-라이선스**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ Windows Server Update Services Tools \ User Interface Management Console (**updateservices-api-UI**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ Active Directory 인증서 서비스 도구 (**RSAT-ADCS**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ Active Directory 인증서 서비스 도구 \ 인증 기관 관리 도구 (**RSAT-ADCS-Mgmt**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ Active Directory 인증서 서비스 도구 \ 온라인 응답기 도구 (**RSAT-online-응답기**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ Active Directory Rights Management Services 도구 (**RSAT-ADRMS**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 팩스 서버 도구 (**RSAT-팩스**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 파일 서비스 도구 (**RSAT-파일-서비스**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 파일 서비스 도구 \ DFS 관리 도구 (**RSAT-dfs-관리-Con**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 파일 서비스 도구 \ 파일 서버 리소스 관리자 도구 (**RSAT-관리**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 파일 서비스 도구 \ 네트워크 파일 시스템 관리 도구에 대 한 서비스 (**RSAT-NFS-관리자**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 네트워크 정책 및 액세스 서비스 도구 (**RSAT-NPAS**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 인쇄 및 문서 서비스 도구 (**RSAT-인쇄-서비스**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ 볼륨 정품 인증 도구 (**RSAT-VA-도구**)
- 원격 서버 관리 도구 \ 역할 관리 도구 \ Windows 배포 서비스 도구 (**WDS-AdminPack**)
- 단순 TCP/IP 서비스 (**단순-TCPIP**)
- SMTP 서버 (**Smtp 서버**)
- TFTP 클라이언트 (**Tftp 클라이언트**)
- WebDAV 리디렉터 (**webdav**리디렉터)
- Windows 생체 인식 프레임워크 (**생체 인식 프레임 워크**)
- Windows defender의 windows Defender 기능 \ GUI (**windows-Defender-GUI**)
- Windows Identity Foundation 3.5 (**windows-identity-foundation**)
- Windows PowerShell \ Windows PowerShell ISE (**POWERSHELL ISE**)
- Windows Search Service (**검색 서비스**)
- Windows TIFF IFilter (**windows-tiff-IFilter**)
- 무선 LAN 서비스 (**무선 네트워킹**)
- XPS 뷰어 (**Xps 뷰어**)
