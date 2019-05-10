---
title: Server Core 란?
description: Windows Server의 Server Core 설치 옵션에 알아봅니다
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 08229e458d0aa0c8e8397f0f053f37a207a1aea5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885604"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Windows Server의 Server Core 설치 옵션은 무엇입니까?

> 적용 대상: Windows Server (반기 채널) 및 Windows Server 2016

Server Core 옵션에는 Windows Server의 Standard 또는 Datacenter edition을 배포 하는 경우 사용할 수 있는 최소한의 설치 옵션이입니다. Server Core는 대부분의 전부는 아니지만 서버 역할을 포함합니다. Server Core에는 더 작은 디스크 공간, 및 따라서 인해 작은 코드 베이스를 더 작은 공격 노출 영역을 있습니다. 

## <a name="server-core-vs-server-with-desktop-experience"></a>(코어) 서버 및 데스크톱 환경 포함 서버 
Windows Server를 설치할 때 선택한-Windows Server에 대 한 전체 공간을 줄일 수 있는 서버 역할만 설치 합니다. 그러나 데스크톱 환경 설치 옵션을 사용 하 여 서버를 여러 서비스 및 기타 구성 요소를 특정 사용 시나리오에 필요한 수 없는 경우가 많습니다 계속 설치 합니다. 

Server Core 고려해 야 하는 위치입니다: Server Core 설치는 모든 서비스를 제거 하 고 서버 역할을 사용 하는 반드시 필요 하지 않은 특정 지원을 위해 일반적으로 다른 기능입니다. 예를 들어 Hyper-v 서버를 Windows PowerShell을 사용 하 여 또는 Hyper-v 관리자를 사용 하 여 명령줄에서 거의 모든 측면의 Hyper-v를 관리할 수 있습니다 때문에 그래픽 사용자 인터페이스 (GUI)를 필요 하지 않습니다. 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Server Core 차이-간단히 없이 핵심 기능
처음으로 로그인을 시스템에서 Server Core 설치를 완료 하면 관심이 다소의 외에 대 한 합니다. 데스크톱 환경 설치 옵션을 사용 하 여 서버 및 Server Core의 주요 차이점은 Server Core는 다음 GUI 셸을 패키지에 포함 되지 않습니다.

- Microsoft-Windows-Server-Shell-Package
- Microsoft-Windows-Server-Gui-Mgmt-Package
- Microsoft-Windows-Server-Gui-RSAT-Package
- Microsoft-Windows-Cortana-PAL-Desktop-Package

즉, **없습니다 데스크톱** 설계상의 Server Core에서. 의 기존 비즈니스 응용 프로그램 및 역할 기반 워크 로드를 지 원하는 데 필요한 기능을 유지 관리할 Server Core는 기존의 데스크톱 인터페이스가 없는 합니다. 대신, Server Core은 명령줄, PowerShell 또는 GUI 도구를 통해 원격으로 관리할 수 (같은 [RSAT](../../remote/remote-server-administration-tools.md) 하거나 [Windows Admin Center](../../manage/windows-admin-center/overview.md)).

UI를 외에도 Server Core도 다른 데스크톱 환경 포함 서버에서 다음과 같은 방법으로:

- Server Core에는 내게 필요한 옵션 도구 없는 합니다.
- Server Core를 설정 하기 위한 없습니다 OOBE (out-의--경험)
- 오디오 지원 기능도 없습니다

다음 표에서 사용할 수 있는 응용 프로그램을 보여 줍니다 *로컬로* Server Core 또는 데스크톱 환경 포함 서버에 있습니다. **중요 한**: 대부분의 경우 "사용할 수 없음" 아래에서 실행할 수 있습니다 원격으로 Windows 클라이언트 컴퓨터 것으로 표시 되며 Server Core 설치를 관리 하는 데 사용 하는 응용 프로그램입니다.

> [!NOTE]
> 이 목록은 전체 목록 이어야 하는 데 사용할 수 없습니다 하 하는 빠른 참조-위한 것입니다.


| 애플리케이션                     | Server Core     | 데스크톱 환경 포함 서버 |
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
| Windows 업데이트 (GUI)                 | 사용할 수 없음 | available                      |
| Windows 탐색기                   | 사용할 수 없음   | available                      |
| 작업 표시줄                            | 사용할 수 없음   | available                      |
| 작업 표시줄 알림              | 사용할 수 없음   | available                      |
| taskmgr                            | available       | available                      |
| Internet Explorer 또는 Microsoft Edge          | 사용할 수 없음   | available                      |
| 기본 제공 도움말 시스템               | 사용할 수 없음   | available                      |
| Windows 10 Shell                   | 사용할 수 없음   | available                      |
| Windows Media Player               | 사용할 수 없음   | available                      |
| PowerShell                         | available       | available                      |
| PowerShell ISE                     | 사용할 수 없음   | available                      |
| PowerShell IME                     | available       | available                      |
| Mstsc.exe                          | 사용할 수 없음   | available                      |
| 원격 데스크톱 서비스            | available       | available                      |
| Hyper-V 관리자                    | 사용할 수 없음  | available                      |


항목에 대 한 자세한 내용은 *됩니다* 참조를 Server Core에 포함 [역할, 역할 서비스 및 Windows Server에서 Server Core에 포함 된 기능](server-core-roles-and-services.md)합니다. 항목에 대 한 자세한 *아닙니다* 참조를 Server Core에 포함 [역할, 역할 서비스 및 Server Core에 포함 되지 않은 기능](server-core-removed-roles.md)

## <a name="get-started-using-server-core"></a>Server Core를 사용 하 여 시작
다음 정보를 사용 하 여 설치, 구성 및 Windows Server의 Server Core 설치 옵션을 관리 합니다.

Server Core 설치: 
- [역할, 역할 서비스 및 Server Core에 포함 된 기능](server-core-roles-and-services.md)
- [역할, 역할 서비스 및 Server Core에 없는 기능](server-core-removed-roles.md)
- [Server Core 설치 옵션을 설치 합니다.](../../get-started/getting-started-with-server-core.md)
- [SConfig 도구를 사용 하 여 Server Core 구성](../../get-started/sconfig-on-ws2016.md)

Server Core를 사용합니다.
- [Windows PowerShell 또는 명령줄을 사용 하 여 기본 Server Core 관리 작업](server-core-administer.md)
- [Server Core 관리](server-core-manage.md)
- [Server Core 패치](server-core-servicing.md)
- [메모리 덤프를 구성 합니다.](server-core-memory-dump.md)