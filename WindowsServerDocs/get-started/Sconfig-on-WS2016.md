---
title: Sconfig.cmd로 Windows Server의 Server Core 설치 구성
description: Sconfig.cmd 사용 방법 설명
ms.prod: windows-server
ms.date: 10/17/2017
ms.technology: server-general
ms.topic: article
ms.assetid: e6cac074-c6fc-46dd-9664-fa0342c0a5e8
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: e6c218b08cc39edd9b3d93ae78b0b5c7aa293858
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2020
ms.locfileid: "80826676"
---
# <a name="configure-a-server-core-installation-of-windows-server-2016-or-windows-server-version-1709-with-sconfigcmd"></a>Sconfig.cmd로 Windows Server 2016 또는 Windows Server, 버전 1709의 Server Core 설치 구성

> 적용 대상: Windows Server(반기 채널) 및 Windows Server 2016

Windows Server 2016 및 Windows Server, 버전 1709에서는 서버 구성 도구(Sconfig.cmd)를 사용하여 Server Core 설치의 몇 가지 일반적인 측면을 구성하고 관리할 수 있습니다. 이 도구를 사용하려면 Administrators 그룹의 구성원이어야 합니다.

Server Core 및 데스크톱 환경 포함 서버(Windows Server 2016 전용)에서 Sconfig.cmd를 사용할 수 있습니다.

## <a name="start-the-server-configuration-tool"></a>서버 구성 도구 시작

1. 시스템 드라이브로 변경합니다.

2. `Sconfig.cmd`를 입력하고 Enter 키를 누릅니다. 서버 구성 도구 인터페이스가 열립니다.

    ![Sconfig.cmd 사용자 인터페이스 스크린샷](media/mainsconfigpage.png)

## <a name="domainworkgroup-settings"></a>도메인/작업 그룹 설정

현재 도메인/작업 그룹 설정은 기본 서버 구성 도구 화면에 표시됩니다. 주 메뉴에서 **도메인/작업 그룹** 설정 페이지에 액세스한 후 지침을 수행하고 필요한 정보를 제공하여 도메인이나 작업 그룹에 가입할 수 있습니다.

도메인 사용자가 로컬 Administrators 그룹에 추가되지 않은 경우 도메인 사용자를 사용하여 컴퓨터 이름을 변경하는 등 시스템 내용을 변경할 수 없습니다. 도메인 사용자를 로컬 Administrators 그룹에 추가하려면 컴퓨터를 다시 시작하도록 허용합니다. 그런 다음, 로컬 관리자로 컴퓨터에 로그인하고 이 문서의 뒷부분에 나오는 [로컬 관리자 설정](#local-administrator-settings) 섹션의 단계를 수행합니다.

> [!NOTE]
> 도메인이나 작업 그룹 구성원 자격에 변경 내용을 적용하려면 서버를 다시 시작해야 합니다. 단, 서버가 여러 번 다시 시작되지 않도록 하려면 원하는 내용을 모두 변경한 후에 서버를 다시 시작할 수 있습니다. 기본적으로, 실행 중인 가상 컴퓨터는 Hyper-V 서버를 다시 시작하기 전에 자동으로 저장됩니다.

## <a name="computer-name-settings"></a>컴퓨터 이름 설정

현재 컴퓨터 이름은 기본 서버 구성 도구 화면에 표시됩니다. 주 메뉴의 **컴퓨터 이름** 설정 페이지에 액세스하여 지침을 수행하여 컴퓨터 이름을 변경할 수 있습니다.

> [!NOTE]
> 도메인이나 작업 그룹 구성원 자격에 변경 내용을 적용하려면 서버를 다시 시작해야 합니다. 단, 서버가 여러 번 다시 시작되지 않도록 하려면 원하는 내용을 모두 변경한 후에 서버를 다시 시작할 수 있습니다. 기본적으로, 실행 중인 가상 컴퓨터는 Hyper-V 서버를 다시 시작하기 전에 자동으로 저장됩니다.

## <a name="local-administrator-settings"></a>로컬 관리자 설정

로컬 Administrators 그룹에 사용자를 추가하려면 주 메뉴에서 **로컬 관리자 추가** 옵션을 사용합니다. 도메인에 가입된 컴퓨터에서는 도메인\사용자 이름 형식으로 사용자를 입력하고 도메인에 가입되지 않은 컴퓨터(작업 그룹 컴퓨터)에서는 사용자 이름만 입력합니다. 변경 내용은 바로 적용됩니다.

## <a name="network-settings"></a>네트워크 설정

DHCP 서버에서 자동으로 할당되도록 IP 주소를 구성하거나 고정 IP 주소를 수동으로 할당할 수 있습니다. 이 옵션을 통해 서버의 DNS 서버 설정도 구성할 수 있습니다.

> [!NOTE]
> 이제 네트워킹 Windows PowerShell cmdlet을 통해 이 옵션 및 기타 여러 옵션을 사용할 수 있습니다. 자세한 내용은 Windows Server 라이브러리에서 [네트워크 어댑터 Cmdlet](https://docs.microsoft.com/powershell/module/netadapter/?view=win10-ps) (영문)을 참조하세요.

## <a name="windows-update-settings"></a>Windows 업데이트 설정

현재 Windows 업데이트 설정은 기본 서버 구성 도구 화면에 표시됩니다. 주 메뉴의 **Windows 업데이트 설정** 구성 옵션에서 자동 또는 수동 업데이트를 사용하도록 서버를 구성할 수 있습니다.

**자동 업데이트** 가 선택되면 시스템이 매일 오전 3시에 업데이트를 확인하고 설치합니다. 설정은 바로 적용됩니다. **수동** 업데이트가 선택되면 시스템이 업데이트를 자동으로 확인하지 않습니다.

언제든지 주 메뉴의 **업데이트 다운로드 및 설치** 옵션에서 적용 가능한 업데이트를 다운로드하고 설치할 수 있습니다.

**다운로드만** 옵션은 업데이트를 검사하고 사용 가능한 모든 업데이트를 다운로드한 다음, 알림 센터를 통해 설치할 준비가 되었다고 알립니다. 기본 옵션입니다.

## <a name="remote-desktop-settings"></a>원격 데스크톱 설정

현재 원격 데스크톱 설정 상태는 기본 서버 구성 도구 화면에 표시됩니다. **원격 데스크톱** 주 메뉴 옵션에 액세스하고 화면에 나오는 지침을 수행하여 다음과 같은 원격 데스크톱 설정을 구성할 수 있습니다.

- 네트워크 수준 인증으로 원격 데스크톱을 실행하는 클라이언트에 대해 원격 데스크톱 사용

- 모든 버전의 원격 데스크톱을 실행하는 클라이언트에 대해 원격 데스크톱 사용

- 원격 기능 사용 안 함

## <a name="date-and-time-settings"></a>날짜 및 시간 설정

**날짜 및 시간** 주 메뉴 옵션에 액세스하여 날짜 및 시간 설정을 액세스 및 변경할 수 있습니다.

## <a name="telemetry-settings"></a>원격 분석 설정

이 옵션을 사용하여 Microsoft에 전송되는 데이터를 구성할 수 있습니다.

## <a name="windows-activation-settings"></a>Windows 정품 인증 설정

이 옵션을 사용하여 Windows 정품 인증을 구성할 수 있습니다.

## <a name="to-enable-remote-management"></a>원격 관리를 사용하도록 설정하려면

**원격 관리 구성** 주 메뉴 옵션에서 여러 원격 관리 시나리오를 사용하도록 설정할 수 있습니다.

- Microsoft Management Console 원격 관리

- Windows PowerShell

- 서버 관리자  

## <a name="to-log-off-restart-or-shut-down-the-server"></a>서버를 로그오프, 다시 시작 또는 종료하려면

서버를 로그오프, 다시 시작 또는 종료하려면 주 메뉴에서 해당 메뉴 항목에 액세스합니다. 이러한 옵션은 **Windows 보안** 메뉴에서도 사용할 수 있으며, 이 보안 메뉴는 Ctrl+Alt+Del을 눌러 언제든지 모든 애플리케이션에서 액세스할 수 있습니다.  

## <a name="to-exit-to-the-command-line"></a>명령줄로 나가려면
  
**명령줄로 끝내기** 옵션을 선택하고 Enter 키를 눌러 명령줄로 나갈 수 있습니다. 서버 구성 도구로 돌아오려면 **Sconfig.cmd**를 입력한 다음, Enter 키를 누릅니다.
