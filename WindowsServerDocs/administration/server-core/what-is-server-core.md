---
title: Server Core 란?
description: Windows Server의 Server Core 설치 옵션에 대 한 설명
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 08229e458d0aa0c8e8397f0f053f37a207a1aea5
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1718537"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Windows Server의 Server Core 설치 옵션 이란?

> 적용 대상: Windows Server (세미콜론 연간 회의 채널) 및 Windows Server 2016

Server Core 옵션에는 Standard 또는 Datacenter 버전의 Windows Server를 배포 하는 경우 사용할 수 있는 최소 설치 옵션이입니다. Server Core 대부분 모두는 아니지만 서버 역할을 포함합니다. Server Core를 더 작은 디스크 공간 및 더 작은 코드 베이스로 인해를 더 작은 공격 대상 영역에 있습니다. 

## <a name="server-core-vs-server-with-desktop-experience"></a>서버 (코어) vs 데스크톱 경험 포함 된 서버 
Windows Server를 설치 하면 선택-Windows 서버에 대 한 전체 공간을 줄일 수 있는 서버 역할만 설치 합니다. 그러나 데스크톱 경험 설치 옵션을 사용 하 여 서버를 다양 한 서비스 및 기타 구성 요소를 특정 사용 시나리오에는 필요 하지 자주는 여전히 설치 합니다. 

이것은 Server Core 재생에 제공 되는 위치: 모든 서비스를 제거 하는 Server Core 설치 및 서버 역할을 사용 하는 일반적으로 특정 지원에 대 한 중요 하지 않은 다른 기능입니다. 예, Windows PowerShell을 사용 하 여 또는 원격으로 Hyper-v 관리자를 사용 하 여 명령줄에서 Hyper-v의 거의 모든 측면을 관리할 수 있습니다 때문에 Hyper-v 서버 그래픽 사용자 인터페이스 (GUI)를 필요 하지 않습니다. 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Server Core 차이-의 없이 핵심 기능
처음에 대 한 시스템 및 로그인에 Server Core 설치를 마쳤으면 중인 보안 컨텍스트로 실행의 비트에 대 한 합니다. 데스크톱 경험 설치 옵션을 사용 하 여 서버 및 서버 코어 간의 주요 차이점은 Server Core 다음 GUI 셸 패키지에 포함 되지 않습니다.

- Microsoft Windows-서버-셸-패키지
- Microsoft-Windows-Server-Gui-Mgmt-Package
- Microsoft-Windows-Server-Gui-RSAT-Package
- Microsoft-Windows-Cortana-PAL-Desktop-Package

즉, 방법이 **없는 데스크톱** 의 Server Core 디자인 합니다. 기존의 비즈니스 응용 프로그램 및 역할 기반 작업을 지원 하기 위해 필요한 기능을 유지 관리 하는 동안 Server Core는 기존의 데스크톱 인터페이스를 되어있지 않습니다. 대신, Server Core는 명령줄, PowerShell, 또는 (예: [RSAT](../../remote/remote-server-administration-tools.md) 또는 [Windows 관리 센터](../../manage/windows-admin-center/overview.md)) GUI 도구를 통해 원격으로 관리 하도록 설계 되었습니다.

UI 없음 외에도 Server Core도 점에서 데스크톱 경험을 사용 하 여 서버에서 다음:

- Server Core 모든 내게 필요한 옵션 도구 없습니다
- Server Core를 설정 하기 위한 없음 OOBE (out (영문)--상자-체감)
- 오디오 지원 되지 않습니다

다음 표는 응용 프로그램은 사용할 수 있는 *로컬로* Server Core vs 데스크톱 경험 포함 된 서버에서를 보여줍니다. **중요**: 대부분의 경우 "아래" 사용할 수 없음으로 실행될수 원격으로 Windows 클라이언트 컴퓨터에서 것으로 표시 되며 Server Core 설치를 관리 하는 데 사용 되는 응용 프로그램입니다.

> [!NOTE]
> 이 목록은 전체 목록은 수 있도록 제작 되지 하는 빠른 참조 (영문)-위한 것입니다.


| Application                     | Server Core     | 데스크톱 환경 포함 서버 |
|------------------------------------|-----------------|--------------------------------|
| 명령 프롬프트                     | available       | available                      |
| Windows PowerShell / Microsoft.NET | available       | available                      |
| Perfmon.exe                        | 사용할 수 없음  | available                      |
| Windbg (GUI)                         | 지원됨       | 지원됨                      |
| Resmon.exe                         | 사용할 수 없음   | available                      |
| Regedit                            | available       | available                      |
| Fsutil.exe                         | available       | available                      |
| Disksnapshot.exe                   | 사용할 수 없음   | available                      |
| Diskpart.exe                       | available       | available                      |
| Diskmgmt.msc                       | 사용할 수 없음   | available                      |
| Devmgmt.msc                        | 사용할 수 없음   | available                      |
| 서버 관리자                     | 사용할 수 없음  | available                      |
| Mmc.exe                            | 사용할 수 없음   | available                      |
| Eventvwr                           | 사용할 수 없음  | available                      |
| Wevtutil (이벤트 쿼리)           | available       | available                      |
| Services.msc                       | 사용할 수 없음   | available                      |
| 제어판                      | 사용할 수 없음   | available                      |
| Windows Update (GUI)                 | 사용할 수 없음 | available                      |
| Windows 탐색기                   | 사용할 수 없음   | available                      |
| 작업 표시줄                            | 사용할 수 없음   | available                      |
| 작업 표시줄 알림              | 사용할 수 없음   | available                      |
| Taskmgr                            | available       | available                      |
| Internet Explorer 또는 지          | 사용할 수 없음   | available                      |
| 기본 제공 도움말 시스템               | 사용할 수 없음   | available                      |
| Windows 10 셸                   | 사용할 수 없음   | available                      |
| Windows Media Player               | 사용할 수 없음   | available                      |
| PowerShell                         | available       | available                      |
| PowerShell ISE                     | 사용할 수 없음   | available                      |
| PowerShell IME                     | available       | available                      |
| Mstsc.exe                          | 사용할 수 없음   | available                      |
| 원격 데스크톱 서비스            | available       | available                      |
| Hyper-V 관리자                    | 사용할 수 없음  | available                      |


어떤 *은* Server Core에 포함 하는 방법에 대 한 자세한 내용은 [역할, 역할 서비스 및 Windows Server-Server Core에에서 포함 된 기능을](server-core-roles-and-services.md)참조 하십시오. 하 고 어떤 *없는* Server Core에 포함 하는 방법에 대 한 정보, [역할, 역할 서비스 및 서버 코어에 포함 되지 않은 기능을](server-core-removed-roles.md) 참조 하십시오.

## <a name="get-started-using-server-core"></a>Server Core를 사용 하 여 시작
설치, 구성 및 Windows Server의 Server Core 설치 옵션을 관리 하려면 다음 정보를 사용 합니다.

Server Core 설치 합니다. 
- [역할, 역할 서비스 및 서버 코어에 포함 된 기능](server-core-roles-and-services.md)
- [역할, 역할 서비스 및 서버 코어에 없는 기능](server-core-removed-roles.md)
- [Server Core 설치 옵션을 설치 합니다.](../../get-started/getting-started-with-server-core.md)
- [SConfig 도구를 사용 하 여 서버 핵심 구성](../../get-started/sconfig-on-ws2016.md)

Server Core를 사용 하 여:
- [Windows PowerShell 또는 명령줄을 사용 하 여 기본 Server Core 관리 작업](server-core-administer.md)
- [Server Core 관리](server-core-manage.md)
- [Server Core에 패치를 적용](server-core-servicing.md)
- [메모리 덤프 파일 구성](server-core-memory-dump.md)