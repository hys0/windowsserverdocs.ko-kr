---
title: 디스크 정리를 사용 하 여 Windows server
description: 디스크 정리 도구를 특정 파일을 자동으로 정리 (Cleanmgr.exe)를 구성 하려면 명령줄 옵션을 사용 하는 방법에 알아봅니다.
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: fbec7cd2b8312f03998cfb27b739d0866d3a47c5
ms.sourcegitcommit: 545dcfc23a81943e129565d0ad188263092d85f6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67407663"
---
# <a name="using-disk-cleanup-on-windows-server"></a>디스크 정리를 사용 하 여 Windows server

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

디스크 정리 도구는 Windows Server 환경에서 불필요 한 파일을 지웁니다. 이 도구는 Windows Server 2019 및 Windows Server 2016에서 기본적으로 사용할 수 있지만 이전 버전의 Windows Server에서 사용 하도록 설정 하는 몇 가지 수동 단계를 수행 해야 할 수 있습니다.

디스크 정리 도구를 시작 하려면 Cleanmgr.exe 명령을 실행 하거나 선택 **시작**를 선택 **Windows 관리 도구**를 선택한 후 **디스크 정리**합니다.

사용 하 여 디스크 정리를 실행할 수도 있습니다는 [cleanmgr Windows 명령](../../administration/windows-commands/cleanmgr.md) 명령줄 옵션을 사용 하 여 특정 파일 정리 디스크 정리를 지정 합니다.

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>데스크톱 경험을 설치 하 여 이전 버전의 Windows Server에서 디스크 정리를 사용 하도록 설정

Windows Server 2012 R2를 실행 하는 서버에 데스크톱 경험을 설치 하는 추가 역할 및 기능 마법사를 사용 하려면 다음이 단계를 수행 하거나 이전에 설치 하는 디스크 정리 합니다.

1. 서버 관리자가 이미 열려 있으면 다음 단계로 이동합니다. 서버 관리자가 아직 열려 있지 않으면 다음 중 하나를 수행하여 엽니다.

   - Windows 바탕 화면에서 Windows 작업 표시줄의 **서버 관리자**를 클릭하여 서버 관리자를 시작합니다.

   - 로 이동 **시작** 서버 관리자 타일을 선택 합니다.

1. 에 **관리** 메뉴에서 추가 선택 **역할 및 기능**합니다.

1. 에 **시작 하기 전에** 페이지에서 설치 하려는 기능에 대 한 대상 서버 및 네트워크 환경이 준비 되어 있는지 확인 합니다. **다음**을 선택합니다.

1. 에 **설치 유형 선택** 페이지에서 선택 **역할 기반 또는 기능 기반 설치** 단일 서버의 모든 파트 기능을 설치 하려면. **다음**을 선택합니다.

1. **대상 서버 선택** 페이지에서 서버 풀의 서버를 선택하거나 오프라인 VHD를 선택합니다. **다음**을 선택합니다.

1. 에 **서버 역할 선택** 페이지에서 선택 **다음**합니다.

1. 에 **기능 선택** 페이지에서 선택 **사용자 인터페이스 및 인프라**를 선택한 후 **데스크톱 경험**합니다.

1. **데스크톱 환경에 필요한 기능 추가?** 를 선택 **추가 기능**합니다.

1. 설치를 진행 하 고 시스템이 다시 부팅 합니다.

1. 있는지 확인 합니다 **디스크 정리** 속성 대화 상자에서 옵션 단추 표시 됩니다.

   ![디스크 디스크 정리 옵션을 사용 하 여 속성 대화 상자](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>디스크 정리는 이전 버전의 Windows Server를 수동으로 추가

디스크 정리 도구 (cleanmgr.exe) 없는 또는 이전 버전 Windows Server 2012 R2의 데스크톱 경험 기능이 설치 된 경우가 아니라면 합니다.

Cleanmgr.exe를 사용 하려면 앞에서 설명한 대로 데스크톱 경험을 설치 하거나 서버, cleanmgr.exe 및 cleanmgr.exe.mui에 존재 하는 두 개의 파일을 복사 합니다. 다음 표를 사용 하 여 운영 체제에 대 한 파일을 찾습니다.

| 운영 체제  | Architecture  | 파일 위치  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64비트 | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr_31bf3856ad364e35_6.1.7600.16385_none_c9392808773cd7da\cleanmgr.exe 
| Windows Server 2008 R2 | 64비트 | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr.resources_31bf3856ad364e35_6.1.7600.16385_en-us_b9cb6194b257cc63\cleanmgr.exe.mui |

Cleanmgr.exe를 찾아 파일을 붙여 **%systemroot%\System32**합니다.

Cleanmgr.exe.mui 찾아 파일을 이동할 **%systemroot%\System32\en-US**합니다.

명령 프롬프트에서 Cleanmgr.exe를 실행 하 여 또는 클릭 하 여 디스크 정리 도구를 지금 시작할 수 있습니다 **시작** 입력 **Cleanmgr** 검색 표시줄에 있습니다.

디스크의 속성 대화 상자에 표시 되는 디스크 정리 단추가 하는 데스크톱 경험 기능을 설치 하려면도 해야 합니다.

## <a name="additional-references"></a>추가 참조

[Windows 10의 드라이브 공간을 확보 하기](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
