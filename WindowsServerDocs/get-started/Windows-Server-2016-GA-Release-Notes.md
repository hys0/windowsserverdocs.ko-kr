---
title: 릴리스 정보 - Windows Server 2016의 주요 문제점
description: 충돌, 중단, 설치 실패, 데이터 손실 등을 방지하기 위한 해결책이 필요한 중요한 문제를 요약합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.date: 11/13/2018
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 134aab85-664f-4d44-87ef-9e5fd389071f
author: jaimeo
ms.author: jaimeo
ms.openlocfilehash: dec1ec184a147ef4fae64e9cc4384c0b6e4510b6
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749536"
---
# <a name="release-notes-important-issues-in-windows-server-2016"></a>릴리스 정보: Windows Server 2016의에서 주요 문제점

>적용 대상: Windows Server 2016

이러한 릴리스 정보는 Windows Server 2016을 비롯해 운영 체제 방지 하거나 문제를 해결 하는 방법을 알고 있는 경우에 가장 중요 한 문제를 요약 합니다. 이 릴리스의 계획된 변경 사항, 새로운 기능 및 해결 방법에 대한 자세한 내용은 [Windows Server 2016의 새로운 기능](whats-new-in-windows-server-2016.md) 및 해당하는 기능 팀의 공지를 참조하세요. 별도로 지정하지 않는 이상, 보고된 각 문제는 Windows Server 2016의 모든 버전 및 설치 옵션에 적용됩니다.

이 문서는 계속해서 업데이트됩니다. 해결 방법이 필요한 중요한 문제가 발견되면 그 내용이 추가되고 새로운 해결 방법 및 수정 사항이 제공됩니다.

## <a name="express-updates-available-starting-in-november-2018-new"></a>Express (신규) 2018 년 11 월부터 제공 되는 업데이트

2018 년 11 월부터 "업데이트 Tuesday" 업데이트, Windows 게시 다시 [Express 업데이트](express-updates.md) Windows Server 2016에 대 한 합니다. Windows Server 2016 업데이트에 대 한 두 개의 패키지를 다시 한 번 표시 됩니다 WSUS 및 System Center Configuration Manager (SCCM)를 사용 하는 경우: 전체 업데이트 및 Express 업데이트 합니다. 서버 환경에 대 한 Express를 사용 하려는 경우 오프 되었는지 확인 하려면 서버는 2017 년 11 월 (KB # 4048953) Express 업데이트를 올바르게 설치 되도록 이후 전체 업데이트 해야 합니다. Express 2017 11B 업데이트 (KB # 4048953) 이후 업데이트 되지 않은 서버에 대 한 업데이트를 시도 하면 대역폭과 CPU 리소스가 무한 루프를 사용 하는 반복 된 오류가 표시 됩니다. 이 시나리오에 표시 되 면 Express 업데이트 푸시를 중지 하 고 대신 오류 루프를 중지 하려면 최신 전체 업데이트를 푸시하십시오.

## <a name="server-core-installation-option"></a>Server Core 설치 옵션

[comment]: # (ID: 370; 제출자: amason; 상태: 로그 오프)

Server Core 설치 옵션을 사용하여 Windows Server 2016을 설치하면 인쇄 서버 역할이 설치되지 않은 경우에도 기본적으로 인쇄 스풀러가 설치되어 시작됩니다.

이 문제를 피하려면 먼저 부팅한 후 인쇄 스풀러를 사용하지 않도록 설정합니다.

## <a name="containers"></a>컨테이너

[comment]: # (ID: 371; 제출자: taylorb; 상태: 로그 오프)
- 컨테이너를 사용 하기 전에 설치 [Windows 10 버전 1607 용 서비스 스택 업데이트: 2016 년 8 월 23 일](https://support.microsoft.com/en-us/kb/3176936) 또는 사용할 수 있는 모든 이후 업데이트 합니다. 빌딩, 오류를 비롯 한 여러 가지 문제가 발생할 수 있습니다 시작 또는 실행과 컨테이너 및 유사 오류가 고, 그렇지 "Win32에서 CreateProcess 실패: RPC 서버 사용할 수 없는 경우 "

[comment]: # (ID: 373; 제출자: plang; 상태: 로그 오프)
- Windows 컨테이너에서 NanoServerPackage OneGet 공급자가 작동하지 않습니다. 이를 해결하려면 서로 다른 컴퓨터(컨테이너 아님)에서 Find-NanoServerPackage 및 Save-NanoServerPackage를 사용하여 필요한 패키지를 다운로드합니다. 그런 다음 패키지를 컨테이너에 복사한 후 설치합니다.

## <a name="device-guard"></a>Device Guard

[comment]: # (ID: 369; 제출자: nirb; 상태: 로그 오프)
코드 무결성의 가상화 기반 보호 또는 보호된 가상 컴퓨터(코드 무결성의 가상화 기반 보호를 사용하는)를 사용하는 경우 이러한 기술이 일부 디바이스 및 응용 프로그램과 호환되지 않을 수 있음을 알고 있어야 합니다. 프로덕션 시스템에서 기능을 사용하도록 설정하기 전에 이러한 구성을 랩에서 테스트해야 합니다. 테스트하지 않을 경우 예기치 않은 데이터 손실 또는 중지 오류가 발생할 수 있습니다.

## <a name="microsoft-exchange"></a>Microsoft Exchange

[comment]: # (ID: 375; 제출자: wgries; 상태: 로그 오프)
Windows Server 2016에서 Microsoft Exchange 2016 CU3를 실행하려고 하면 IIS 호스트 프로세스 W3WP.exe에서 오류가 발생합니다. 현재로서는 해결 방법이 없습니다. 지원되는 픽스가 제공될 때까지 Windows Server 2016에서의 Exchange 2016 CU3 배포를 연기해야 합니다.

## <a name="remote-server-administration-tools-rsat"></a>RSAT(원격 서버 관리 도구)

[comment]: # (ID: 374; 제출자: ryanpu; 상태: 로그 오프)
RSAT를 사용 하는 Hyper-v 및 virtual machines를 사용 하도록 설정된 가상 신뢰할 수 있는 플랫폼 모듈 (보호 된 가상 컴퓨터 포함) 및 다음 버전의 설치 Windows 10 1 주년 업데이트 보다 이전 버전을 실행 하는 경우 Windows에 대 한 제공 Server 2016 가상 컴퓨터를 시작 하려는 시도가 실패 합니다.

이 문제를 방지하려면 RSAT를 설치하기 전에 클라이언트 컴퓨터를 Windows 10 1주년 업데이트(이상)로 업그레이드합니다. 문제가 이미 발생했다면 RSAT를 제거하고 클라이언트를 Windows 10 1주년 업데이트로 업그레이드한 후 RSAT를 다시 설치합니다.

## <a name="shielded-virtual-machines"></a>실드 된 가상 컴퓨터

[comment]: # (ID: 369; 제출자: nirb; 상태: 로그 오프)  
- 프로덕션 환경에서 보호된 가상 컴퓨터를 배포하기 전에 사용 가능한 모든 업데이트를 설치해야 합니다.

- 코드 무결성의 가상화 기반 보호 또는 보호된 가상 컴퓨터(코드 무결성의 가상화 기반 보호를 사용하는)를 사용하는 경우 이러한 기술이 일부 디바이스 및 응용 프로그램과 호환되지 않을 수 있음을 알고 있어야 합니다. 프로덕션 시스템에서 기능을 사용하도록 설정하기 전에 이러한 구성을 랩에서 테스트해야 합니다. 테스트하지 않을 경우 예기치 않은 데이터 손실 또는 중지 오류가 발생할 수 있습니다.

## <a name="start-menu"></a>시작 메뉴

[comment]: # (ID: 372; 제출자: samli; 상태: 로그 오프)
이 문제는 데스크톱 환경 옵션으로 서버에 설치된 Windows Server 2016에 영향을 줍니다.

폴더 내에 있는 바로 가기 항목에 추가 하는 응용 프로그램을 설치 하는 경우는 **시작** 메뉴에서 로그 아웃 하 고 다시 로그인 될 때까지 바로 가기가 작동 하지 않습니다.

기본 [Windows Server 2016](Windows-Server-2016.md) 허브로 다시 돌아갑니다.

## <a name="storport-performance"></a>Storport 성능

시스템에 따라 Windows Server 2012 R2이 아니라 Windows Server 2016을 새로 설치해 실행할 때 저장소 성능이 저하되는 경우가 발생할 수 있습니다.  플랫폼의 보안성과 안정성을 개선하기 위해 Windows Server 2016 개발 과정에서 많은 변경이 이루어졌습니다. Windows Defender 기본 지원과 같은 일부 변경은 I/O 경로를 연장하여 특정 워크로드 및 패턴에서 I/O 성능을 저하시키는 결과를 초래하기도 합니다. Microsoft는 시스템에서 중요한 보호 계층 역할을 한다는 점에서 Windows Defender를 비활성화하지 않도록 권장하고 있습니다.  

## <a name="copyright"></a>저작권

이 문서는 "있는 그대로" 제공됩니다. URL 및 기타 인터넷 웹 사이트 참조를 포함하여 이 설명서의 내용 및 의견은 예고 없이 변경될 수 있습니다.  

이 설명서는 Microsoft 제품의 지적 재산에 대한 법적 권한을 제공하지 않습니다. 이 설명서는 내부 참조용으로만 복사 및 사용할 수 있습니다.  

&copy;2016 Microsoft Corporation. All rights reserved.  

Microsoft, Active Directory, Hyper-V, Windows 및 Windows Server는 미국, 대한민국 및/또는 기타 국가에서의 Microsoft Corporation 등록 상표 또는 상표입니다.  

이 제품에는 부분적으로 Independent JPEG Group의 작업을 기반으로 하는 그래픽 필터 소프트웨어가 포함되어 있습니다.  

1.0
