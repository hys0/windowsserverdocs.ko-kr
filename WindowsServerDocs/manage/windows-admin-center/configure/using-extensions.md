---
title: 설치 하 고 확장 관리
description: 설치 하 고 Windows Admin Center (프로젝트 브라 티)에서 확장 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9038fd480ed105aed3949b0c48dffc7eab94f970
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445888"
---
# <a name="install-and-manage-extensions"></a>설치 하 고 확장 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

여기서 각 연결 형식 및 도구 설치, 제거 및 개별적으로 업데이트할 수 있는 확장은 확장 가능 플랫폼으로 서 Windows Admin Center 빌드됩니다. Microsoft 및 다른 개발자가 새 확장에 대 한 검색 및 설치 하 고 전체 Windows Admin Center 설치를 업데이트 하지 않고 개별적으로 업데이트할 수 있습니다. 또한 별도 NuGet 피드를 구성 또는 파일 공유를 조직 내에서 내부적으로 사용 하는 확장을 배포 합니다.

## <a name="installing-an-extension"></a>확장 설치

Windows Admin Center 지정된 NuGet 피드에서 사용 가능한 확장 프로그램을 표시 됩니다. 기본적으로 Windows Admin Center 가리키는 Microsoft 공식 NuGet 피드에 Microsoft 및 다른 개발자가 확장을 호스트 하는 경우

1. 클릭 합니다 **설정을** 오른쪽 위에 있는 단추 > 왼쪽된 창에서 클릭 **확장**합니다. 
2. 합니다 **사용 가능한 확장** 탭에는 설치에 사용할 수 있는 피드에서 확장 나열 됩니다.
3. 확장인 확장 설명, 버전, 게시자 및 기타 정보를 보려면 클릭 합니다 **세부 정보** 창입니다.
4. 클릭 **설치** 확장을 설치 합니다. 게이트웨이이 변경을 수행 하려면 관리자 모드에서 실행 해야, UAC 권한 상승 프롬프트를 사용 하 여 나타납니다. 설치가 완료 되 면 브라우저는 자동으로 새로 고쳐집니다 후 새 확장이 설치 된 Windows Admin Center 다시 로드 됩니다. 확장 하려고 하는 경우 설치는 이전에 설치 된 확장에 대 한 업데이트를 클릭할 수는 **최신 업데이트** 업데이트를 설치 하는 단추입니다. 로 이동할 수 있습니다 합니다 **설치 된 확장** 업데이트에 표시 되 면 설치 보기 확장 및 참조 탭의 **상태** 열입니다.

## <a name="installing-extensions-from-a-different-feed"></a>다른 피드에서 확장 설치

Windows Admin Center 여러 피드를 지원 하며 확인 하 고 한 번에 둘 이상의 피드에서 패키지를 관리할 수 있습니다. NuGet 피드 지 NuGet V2 Api 또는 파일 공유에서 확장을 설치 하기 위한 Windows Admin Center 추가할 수 있습니다.

1. 클릭 합니다 **설정을** 오른쪽 위에 있는 단추 > 왼쪽된 창에서 클릭 **확장**합니다.
2. 오른쪽 창에서를 클릭 합니다 **피드** 탭 합니다.
3. 클릭 합니다 **추가** 다른 피드에 추가 하는 단추입니다. NuGet 피드, NuGet V2 피드 URL을 입력 합니다. NuGet 피드 공급자 또는 관리자 URL 정보를 제공할 수 있어야 합니다. 파일 공유에 대 한 파일의 전체 경로 입력 합니다. 저장 된 확장 패키지 파일 (.nupkg) 공유 합니다.
4. **추가**를 클릭합니다. 게이트웨이이 변경을 수행 하려면 관리자 모드에서 실행 해야, UAC 권한 상승 프롬프트를 사용 하 여 나타납니다.

합니다 **사용 가능한 확장** 등록 된 모든 피드에서 확장 목록에 표시 됩니다. 피드를 사용 하 여 각 확장은 확인할 수 있습니다 합니다 **패키지 피드** 열입니다.

## <a name="uninstalling-an-extension"></a>확장 제거

이전에 설치한 모든 확장을 제거 하거나도 Windows Admin Center 설치의 일부로 미리 설치 된 도구를 제거할 수 있습니다.

1. 클릭 합니다 **설정을** 오른쪽 위에 있는 단추 > 왼쪽된 창에서 클릭 **확장**합니다. 
2. 클릭 합니다 **설치 된 확장** 설치 된 모든 확장 보기를 탭 합니다.
3. 제거 클릭 확장 선택 **제거**합니다.

제거 후 완료 하 고 브라우저가 자동으로 새로 고쳐집니다 Windows Admin Center 확장명이 제거를 사용 하 여 다시 로드 됩니다. 도구에서 성공할 수 Windows Admin Center 일부로 미리 설치 된 도구를 제거한 경우 합니다 **사용 가능한 확장** 탭 합니다.

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>인터넷 연결이 없는 컴퓨터에서 확장을 설치합니다.

Windows Admin Center 인터넷에 연결 되어 있지 않습니다 또는 프록시 뒤에 있는 컴퓨터에 설치 하는 경우 액세스 하 고 피드 Windows Admin Center 확장을 설치할 못할 수 있습니다. 수동으로 또는 PowerShell 스크립트를 사용 하 여 확장 패키지를 다운로드 하 고 로컬 드라이브 또는 파일 공유에서 패키지를 검색할 Windows Admin Center 구성할 수 있습니다.

### <a name="manually-downloading-extension-packages"></a>확장 패키지를 수동으로 다운로드

1. 인터넷에 연결 된 다른 컴퓨터에서 웹 브라우저를 열고 다음 URL로 이동: [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

   * Msft sme.myget.org 및 확장 패키지를 보려면 로그인에 계정을 만들고 해야 합니다.

2. 패키지 세부 정보 페이지가 설치 하려는 패키지의 이름을 클릭 합니다.
3. 클릭 합니다 **다운로드** 패키지 세부 정보 페이지의 오른쪽 창에서 연결 하 고 확장 하 여.nupkg 파일을 다운로드 합니다.
4. 다운로드 하려는 모든 패키지에 대 한 2와 3 단계를 반복 합니다.
5. Windows Admin Center 설치 된 컴퓨터에서 액세스할 수 있는 파일 공유 또는 컴퓨터의 로컬 디스크에 패키지 파일을 복사 합니다.
6. [다른 피드에서 확장을 설치 하려면 지침에 따라](#installing-extensions-from-a-different-feed)합니다.

### <a name="downloading-packages-with-a-powershell-script"></a>PowerShell 스크립트를 사용 하 여 패키지를 다운로드합니다.

NuGet 피드의 NuGet 패키지를 다운로드 하는 것에 대 한 인터넷에서 사용할 수 있는 많은 스크립트 있습니다. 사용 하 여 합니다 [Jon Galloway 제공한 스크립트](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), Microsoft의 선임 프로그램 관리자입니다.

1. 에 설명 된 대로 합니다 [블로그 게시물](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), NuGet 패키지로 설치 된 스크립트 또는 복사 및 PowerShell ISE에 스크립트를 붙여넣습니다.
2. NuGet 스크립트의 첫 번째 줄 바꿈 편집의 v2 URL입니다. 공식 Windows Admin Center 패키지를 피드를 다운로드 하는 경우 아래 URL을 사용 합니다.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. 스크립트를 실행 하 고 피드에서 모든 NuGet 패키지를 다음 로컬 폴더로 다운로드: %USERPROFILE%\Documents\NuGetLocal
4. [다른 피드에서 확장을 설치 하려면 지침에 따라](#installing-extensions-from-a-different-feed)합니다.

## <a name="manage-extensions-with-powershell"></a>PowerShell 사용 하 여 확장 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center 미리 보기에 게이트웨이 확장을 관리 하기 위한 PowerShell 모듈을 포함 합니다.

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

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdkextendextensibility-overviewmd"></a>[Windows Admin Center SDK를 사용 하 여 확장을 구축 하는 방법에 대 한 자세한](../extend/extensibility-overview.md)합니다.