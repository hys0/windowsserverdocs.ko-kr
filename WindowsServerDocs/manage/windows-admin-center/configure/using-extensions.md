---
title: 설치 하 고 확장 관리
description: 설치 하 고 Windows Admin Center (Project Honolulu)의 확장 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c775dd5a3011115bbb031c0b9e4e24a8911d378e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296705"
---
# 설치 하 고 확장 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 확장 가능한 플랫폼인 각 연결 유형 및 도구는 설치, 제거 및 개별적으로 업데이트 하는 확장으로 만들어집니다. Microsoft와 다른 개발자가 게시 하는 새로운 확장에 대 한 검색 하 고 설치 하 고 전체 Windows Admin Center 설치를 업데이트 하지 않고도 개별적으로 업데이트할 수 있습니다. 또한 별도 NuGet 피드 또는 파일 공유를 구성한 조직 내에서 내부적으로 사용 하 여 확장을 배포 합니다.

## 확장 설치

Windows Admin Center는 피드 지정 된 NuGet에서 사용할 수 있는 확장을 표시 합니다. 기본적으로 Windows Admin Center 가리키는 피드 Microsoft 공식 NuGet Microsoft와 다른 개발자가 게시 하는 확장을 호스트 하는 경우

1. 왼쪽된 창에서 오른쪽 위 gt_ **설정** 단추를 클릭 하 고 **확장**을 클릭 합니다. 
2. **사용 가능한 확장** 탭 설치에 사용할 수 있는 확장 피드에 나열 됩니다.
3. **세부 정보** 창에서 확장 설명, 버전, 게시자 및 기타 정보를 보려면 확장을 클릭 합니다.
4. 확장을 설치 하려면 **설치** 를 클릭 합니다. 게이트웨이 모드에서이 이렇게 하려면으로 실행 해야 하는 경우 UAC 권한 상승 프롬프트를 사용 하 여 제공 됩니다. 설치가 완료 되 면 브라우저는 자동으로 새로 고칠 수 및 설치 된 새 확장을 사용 하 여 Windows Admin Center를 다시 로드 됩니다. 설치 하려는 확장 이전에 설치 된 확장에 대 한 업데이트 인 경우 업데이트를 설치 하려면 **최신 업데이트** 단추를 클릭 수 있습니다. 설치 된 확장을 보고 업데이트 **상태** 열에서 사용할 수 있는지 확인 하 여 **설치 된 확장** 탭으로 이동할 수 있습니다.

## 다른 피드에서 확장 설치

Windows Admin Center는 여러 피드를 지원 하며 보기를 한 번에 둘 이상의 피드에서 패키지를 관리할 수 있습니다. 모든 NuGet NuGet V2 Api를 지 원하는 피드 또는 파일 공유에서 확장을 설치 하기 위한 Windows Admin Center에 추가할 수 있습니다.

1. 왼쪽된 창에서 오른쪽 위 gt_ **설정** 단추를 클릭 하 고 **확장**을 클릭 합니다.
2. 오른쪽 창에서 **피드** 탭을 클릭 합니다.
3. 다른 피드를 추가 하려면 **추가** 단추를 클릭 합니다. NuGet 피드를 NuGet V2 피드 URL을 입력 합니다. NuGet 피드 공급자 또는 관리자 URL 정보를 제공 해야 합니다. 파일 공유에 대 한 파일의 전체 경로 입력 공유 확장 패키지 파일 (.nupkg) 저장 됩니다.
4. **추가**를 클릭합니다. 게이트웨이 모드에서이 이렇게 하려면으로 실행 해야 하는 경우 UAC 권한 상승 프롬프트를 사용 하 여 제공 됩니다.

**사용 가능한 확장** 목록에서 등록 된 모든 피드 확장 표시 됩니다. **패키지 피드** 열을 사용 하 여 각 확장은 어떤 피드를 확인할 수 있습니다.

## 확장 제거

이전에 설치 된 확장을 제거 하거나도 Windows Admin Center 설치의 일부로 미리 설치 된 모든 도구를 제거할 수 있습니다.

1. 왼쪽된 창에서 오른쪽 위 gt_ **설정** 단추를 클릭 하 고 **확장**을 클릭 합니다. 
2. **설치 된 확장** 탭 설치 된 모든 확장을 클릭 합니다.
3. 확장을 제거 하려면를 선택한 다음 **제거**를 클릭 합니다.

제거 후 완료, 브라우저는 자동으로 새로 고칠 수 및 Windows Admin Center 제거 확장명으로 다시 로드 됩니다. Windows Admin Center의 일환으로 사전 설치 된 도구를 제거한 경우 도구를 **사용할 수 있는 확장** 탭에서 다시 설치에 사용할 수 있는 됩니다.

## 확장 인터넷 연결 없이 컴퓨터에 설치

Windows Admin Center 인터넷에 연결 되지 않은 컴퓨터 또는 프록시 뒤에 있는 컴퓨터에 설치 된 경우 액세스 하 고 확장 피드 Windows 관리 센터에서 설치할 못할 수 있습니다. 수동으로 또는 PowerShell 스크립트를 사용 하 여 확장 패키지를 다운로드 하 고 파일 공유 또는 로컬 드라이브에서 패키지를 검색 하려면 Windows Admin Center를 구성할 수 있습니다.

### 수동으로 확장 패키지를 다운로드

1. 인터넷에 연결 되어 있는 다른 컴퓨터에서 웹 브라우저를 열고 다음 URL로 이동 합니다.[https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

  * Msft sme.myget.org 및 확장 패키지를 보려면 로그인에서 계정을 만들고 해야 할 수 있습니다.

2. 설치 패키지 세부 정보 페이지를 표시 하려면 패키지의 이름을 클릭 합니다.
3. 패키지 세부 정보 페이지의 오른쪽 창에서 **다운로드** 링크를 클릭 하 고 확장에 대 한.nupkg 파일을 다운로드 합니다.
4. 다운로드 하려는 모든 패키지에 대 한 2 및 3 단계를 반복 합니다.
5. Windows Admin Center에 설치 된 컴퓨터에서 액세스할 수 있는 파일 공유 또는 컴퓨터의 로컬 디스크에 패키지 파일을 복사 합니다.
6. [다른 피드에서 확장을 설치 지침을 따릅니다](#installing-extensions-from-a-different-feed).

### PowerShell 스크립트를 사용 하 여 패키지를 다운로드합니다.

피드 NuGet에서 NuGet 패키지를 다운로드 하기 위한 인터넷에서 사용할 수 있는 많은 스크립트가 있습니다. [스크립트 정보가 Galloway 제공한](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)microsoft 수석 프로그램 관리자를 사용 하겠습니다.

1. [블로그 게시물](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)에 설명 된 대로 NuGet 패키지 또는 복사 스크립트를 설치 하 고 PowerShell ISE에 스크립트를 붙여 넣습니다.
2. 편집에 NuGet 스크립트의 첫 번째 줄 바꿈의 v2 URL입니다. 피드 공식 Windows 관리 센터에서 패키지를 다운로드 하는 경우 아래 URL을 사용 합니다.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. 스크립트를 실행 하 고 다음 로컬 폴더로 피드에서 모든 NuGet 패키지가 다운로드 됩니다: %USERPROFILE%\Documents\NuGetLocal
4. [다른 피드에서 확장을 설치 지침을 따릅니다](#installing-extensions-from-a-different-feed).

## PowerShell 사용 하 여 확장 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 미리 보기 게이트웨이 확장을 관리 하는 PowerShell 모듈을 포함 합니다.

```powershell
# Add the module to the current session
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ExtensionTools"
# Available cmdlets: Get-Feed, Add-Feed, Remove-Feed, Get-Extension, Install-Extension, Uninstall-Extension, Update-Extension

# List feeds
Get-Feed "https://wac.contoso.com"

# Add a new extension feed
Add-Feed -GatewayEndpoint "https://wac.contoso.com" -Feed "\\WAC\our-private-extensions"

# Remove an extension feed
Remove-Feed -GatewayEndpoint "https://wac.contoso.com" -Feed "\\WAC\our-private-extensions"

# List all extensions
Get-Extension "https://wac.contoso.com"

# Install an extension (locate the latest version from all feeds and install it)
Install-Extension -GatewayEndpoint "https://wac.contoso.com" "msft.sme.containers"

# Install an extension (latest version from a specific feed, if the feed is not present, it will be added)
Install-Extension -GatewayEndpoint "https://wac.contoso.com" "msft.sme.containers" -Feed "https://aka.ms/sme-extension-feed"

# Install an extension (install a specific version)
Install-Extension "https://wac.contoso.com" "msft.sme.certificate-manager" "0.133.0"

# Uninstall-Extension
Uninstall-Extension "https://wac.contoso.com" "msft.sme.containers"

# Update-Extension
Update-Extension "https://wac.contoso.com" "msft.sme.containers"
```

### [Windows Admin Center SDK를 사용 하 여 확장 빌드에 대해 자세히 알아봅니다](../extend/extensibility-overview.md).