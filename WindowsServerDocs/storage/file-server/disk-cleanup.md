---
title: Windows Server에서 디스크 정리 사용
description: 명령줄 옵션을 사용 하 여 특정 파일을 자동으로 정리 하도록 디스크 정리 도구 (Cleanmgr)를 구성 하는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: 2de3452a3528122beb26f403fb0c73d7ff13efd7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402115"
---
# <a name="using-disk-cleanup-on-windows-server"></a>Windows Server에서 디스크 정리 사용

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

디스크 정리 도구는 Windows Server 환경에서 불필요 한 파일을 지웁니다. 이 도구는 Windows Server 2019 및 Windows Server 2016에서 기본적으로 사용할 수 있지만, 이전 버전의 Windows Server에서 사용 하도록 설정 하려면 몇 가지 수동 단계를 수행 해야 할 수도 있습니다.

디스크 정리 도구를 시작 하려면 Cleanmgr 명령을 실행 하거나 **시작**, **Windows 관리 도구**를 차례로 선택한 다음 **디스크 정리**를 선택 합니다.

[Cleanmgr Windows 명령을](../../administration/windows-commands/cleanmgr.md) 사용 하 여 디스크 정리를 실행 하 고 명령줄 옵션을 사용 하 여 디스크 정리가 특정 파일을 정리 하도록 지정할 수도 있습니다.

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>데스크톱 경험을 설치 하 여 이전 버전의 Windows Server에서 디스크 정리 사용

역할 및 기능 추가 마법사를 사용 하 여 Windows Server 2012 R2 또는 이전 버전을 실행 하는 서버에 데스크톱 환경을 설치 하는 경우 다음 단계를 수행 하 여 디스크 정리도 설치 합니다.

1. 서버 관리자가 이미 열려 있으면 다음 단계로 이동합니다. 서버 관리자가 아직 열려 있지 않으면 다음 중 하나를 수행하여 엽니다.

   - Windows 바탕 화면에서 Windows 작업 표시줄의 **서버 관리자**를 클릭하여 서버 관리자를 시작합니다.

   - **시작** 으로 이동 하 여 서버 관리자 타일을 선택 합니다.

1. **관리** 메뉴에서 **역할 및 기능**추가를 선택 합니다.

1. **시작 하기 전** 페이지에서 설치 하려는 기능에 대 한 대상 서버 및 네트워크 환경이 준비 되어 있는지 확인 합니다. **다음**을 선택합니다.

1. **설치 유형 선택** 페이지에서 **역할 기반 또는 기능 기반 설치** 를 선택 하 여 모든 파트 기능을 단일 서버에 설치 합니다. **다음**을 선택합니다.

1. **대상 서버 선택** 페이지에서 서버 풀의 서버를 선택하거나 오프라인 VHD를 선택합니다. **다음**을 선택합니다.

1. **서버 역할 선택** 페이지에서 **다음**을 선택 합니다.

1. **기능 선택** 페이지에서 **사용자 인터페이스 및 인프라**를 선택 하 고 **데스크톱 환경**을 선택 합니다.

1. **데스크톱 환경에 필요한 기능 추가**에서 **기능 추가**를 선택 합니다.

1. 설치를 계속 하 고 시스템을 다시 부팅 합니다.

1. 속성 대화 상자에 **디스크 정리** 옵션 단추가 표시 되는지 확인 합니다.

   ![디스크 정리 옵션을 사용 하는 디스크 속성 대화 상자](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>이전 버전의 Windows Server에 수동으로 디스크 정리 추가

데스크톱 경험 기능이 설치 되어 있지 않으면 디스크 정리 도구 (cleanmgr)가 Windows Server 2012 R2 이전 버전에 없습니다.

Cleanmgr를 사용 하려면 앞에서 설명한 대로 데스크톱 경험을 설치 하거나 서버에 이미 있는 파일 두 개 (cleanmgr 및 cleanmgr)를 복사 합니다. 다음 표를 사용 하 여 운영 체제에 대 한 파일을 찾을 수 있습니다.

| 운영 체제  | 아키텍처  | 파일 위치  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64비트 | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr_31bf3856ad364e35_6.1.7600.16385_none_c9392808773cd7da\cleanmgr.exe 
| Windows Server 2008 R2 | 64비트 | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr.resources_31bf3856ad364e35_6.1.7600.16385_en-us_b9cb6194b257cc63\cleanmgr.exe.mui |

Cleanmgr를 찾아 파일을 **%systemroot%\System32**로 이동 합니다.

Cleanmgr를 찾아 파일을 **%systemroot%\System32\en-US**로 이동 합니다.

이제 명령 프롬프트에서 Cleanmgr를 실행 하거나 **시작** 을 클릭 하 고 검색 창에 **Cleanmgr** 를 입력 하 여 디스크 정리 도구를 시작할 수 있습니다.

디스크의 속성 대화 상자에 디스크 정리 단추가 표시 되도록 하려면 데스크톱 경험 기능을 설치 해야 합니다.

## <a name="additional-references"></a>추가 참조

[Windows 10에서 드라이브 공간 확보](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
