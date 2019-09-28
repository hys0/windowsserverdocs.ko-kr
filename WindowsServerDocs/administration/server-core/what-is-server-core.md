---
title: Server Core 란?
description: Windows Server의 Server Core 설치 옵션에 대 한 자세한 정보
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/20/2018
ms.openlocfilehash: 269be253367ba2bc692a5903e7d519a40f487d8b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383342"
---
# <a name="what-is-the-server-core-installation-option-in-windows-server"></a>Windows Server의 Server Core 설치 옵션은 무엇 인가요?

> 적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

Server Core 옵션은 Windows Server Standard edition 또는 Datacenter edition을 배포할 때 사용할 수 있는 최소 설치 옵션입니다. Server Core에는 대부분의 서버 역할이 포함 됩니다. Server Core에는 더 작은 디스크 공간이 있으므로 더 작은 코드 베이스 때문에 더 작은 공격 노출 영역이 있습니다. 

## <a name="server-core-vs-server-with-desktop-experience"></a>서버 (코어) 및 데스크톱 환경을 사용 하는 서버 
Windows Server를 설치할 때 선택한 서버 역할만 설치 합니다. 그러면 Windows Server의 전체 공간을 줄일 수 있습니다. 그러나 데스크톱 환경 포함 서버 설치 옵션은 종종 특정 사용 시나리오에 필요 하지 않은 많은 서비스 및 기타 구성 요소를 설치 합니다. 

Server Core를 사용 하면 일반적으로 사용 되는 특정 서버 역할의 지원에 필수적인 서비스 및 기타 기능이 제거 됩니다. 예를 들어 hyper-v 서버는 Windows PowerShell을 사용 하 여 명령줄에서 또는 Hyper-v 관리자를 사용 하 여 원격으로 Hyper-v의 거의 모든 측면을 관리할 수 있으므로 GUI (그래픽 사용자 인터페이스)가 필요 하지 않습니다. 

## <a name="the-server-core-difference---core-capabilities-without-the-frills"></a>Frills를 사용 하지 않는 Server Core 차이점-핵심 기능
시스템에 Server Core를 설치 하 고 처음으로 로그인 하면 약간의 문제가 있습니다. 데스크톱 환경 설치 옵션 및 Server Core를 사용 하는 서버의 주요 차이점은 Server Core에는 다음 GUI 셸 패키지가 포함 되지 않는다는 것입니다.

- Microsoft-Windows------패키지
- Microsoft-Windows-서버-Gui-관리 패키지
- Microsoft-Windows-Gui-RSAT-패키지
- Microsoft-Windows-Windows-Windows-Windows-PAL-Package

즉, Server Core에는 설계상 **데스크톱이 없습니다** . 기존 비즈니스 응용 프로그램 및 역할 기반 워크 로드를 지 원하는 데 필요한 기능을 유지 하면서 Server Core에는 기존 데스크톱 인터페이스가 없습니다. 대신, Server Core는 명령줄, PowerShell 또는 GUI 도구 (예: [RSAT](../../remote/remote-server-administration-tools.md) 또는 [Windows 관리 센터](../../manage/windows-admin-center/overview.md))를 통해 원격으로 관리할 수 있도록 설계 되었습니다.

Server Core는 UI 외에도 다음과 같은 방법으로 데스크톱 환경을 사용 하는 서버와 다릅니다.

- Server Core에 내게 필요한 옵션 도구가 없습니다.
- Server Core를 설정 하기 위한 OOBE (기본 제공 환경) 없음
- 오디오 지원 안 함

다음 표에서는 데스크톱 환경에서 Server Core vs Server에 *로컬로* 사용할 수 있는 응용 프로그램을 보여 줍니다. **중요**: 대부분의 경우 아래 "사용할 수 없음"으로 표시 된 응용 프로그램은 Windows 클라이언트 컴퓨터에서 원격으로 실행 하 여 Server Core 설치를 관리 하는 데 사용할 수 있습니다.

> [!NOTE]
> 이 목록은 빠른 참조용 이며 완전 한 목록이 아닙니다.


| 애플리케이션                     | Server Core     | 데스크톱 환경 포함 서버 |
|------------------------------------|-----------------|--------------------------------|
| 명령 프롬프트                     | available       | available                      |
| Windows PowerShell/Microsoft .NET | available       | available                      |
| Perfmon.exe                        | 사용할 수 없음  | available                      |
| Windbg (GUI)                         | 지원됨       | 지원됨                      |
| Resmon .exe                         | 사용할 수 없음   | available                      |
| Regedit.exe                            | available       | available                      |
| Fsutil .exe                         | available       | available                      |
| Disksnapshot .exe                   | 사용할 수 없음   | available                      |
| Diskpart.exe                       | available       | available                      |
| Diskmgmt.msc                       | 사용할 수 없음   | available                      |
| Devmgmt.msc .msc                        | 사용할 수 없음   | available                      |
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
| Taskmgr->networking                            | available       | available                      |
| Internet Explorer 또는 Edge          | 사용할 수 없음   | available                      |
| 기본 제공 도움말 시스템               | 사용할 수 없음   | available                      |
| Windows 10 Shell                   | 사용할 수 없음   | available                      |
| Windows Media Player               | 사용할 수 없음   | available                      |
| PowerShell                         | available       | available                      |
| PowerShell ISE                     | 사용할 수 없음   | available                      |
| PowerShell IME                     | available       | available                      |
| Mstsc                          | 사용할 수 없음   | available                      |
| 원격 데스크톱 서비스            | available       | available                      |
| Hyper-V 관리자                    | 사용할 수 없음  | available                      |


Server Core에 포함 *된* 기능에 대 한 자세한 내용은 [Windows Server-server core에 포함 된 역할, 역할 서비스 및 기능](server-core-roles-and-services.md)을 참조 하세요. Server Core에 포함 *되지* 않은 항목에 대 한 자세한 내용은 [server core에 포함 되지 않은 역할, 역할 서비스 및 기능](server-core-removed-roles.md) 을 참조 하세요.

## <a name="get-started-using-server-core"></a>Server Core를 사용 하 여 시작
다음 정보를 사용 하 여 Windows Server의 Server Core 설치 옵션을 설치, 구성 및 관리할 수 있습니다.

Server Core 설치: 
- [Server Core에 포함 된 역할, 역할 서비스 및 기능](server-core-roles-and-services.md)
- [Server Core에 없는 역할, 역할 서비스 및 기능](server-core-removed-roles.md)
- [Server Core 설치 옵션 설치](../../get-started/getting-started-with-server-core.md)
- [SConfig 도구를 사용 하 여 Server Core 구성](../../get-started/sconfig-on-ws2016.md)

Server Core 사용:
- [Windows PowerShell 또는 명령줄을 사용 하 여 기본 Server Core 관리 작업](server-core-administer.md)
- [Server Core 관리](server-core-manage.md)
- [패치 서버 코어](server-core-servicing.md)
- [메모리 덤프 파일 구성](server-core-memory-dump.md)