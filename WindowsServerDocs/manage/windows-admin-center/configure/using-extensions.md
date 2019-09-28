---
title: 확장 설치 및 관리
description: Windows 관리 센터 (Project Honolulu)에서 확장 설치 및 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d49e25591c705afa217b2332ee48eb42c5c2f7ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357245"
---
# <a name="install-and-manage-extensions"></a>확장 설치 및 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터는 각 연결 형식 및 도구가 개별적으로 설치, 제거 및 업데이트할 수 있는 확장 가능한 플랫폼으로 빌드됩니다. Microsoft 및 다른 개발자가 게시 한 새 확장을 검색 하 여 전체 Windows 관리 센터 설치를 업데이트할 필요 없이 개별적으로 설치 하 고 업데이트할 수 있습니다. 별도의 NuGet 피드 또는 파일 공유를 구성 하 고 조직 내에서 내부적으로 사용할 확장을 배포할 수도 있습니다.

## <a name="installing-an-extension"></a>확장 설치

Windows 관리 센터에는 지정 된 NuGet 피드에서 사용할 수 있는 확장이 표시 됩니다. 기본적으로 Windows 관리 센터는 Microsoft 및 기타 개발자가 게시 한 확장을 호스트 하는 Microsoft 공식 NuGet 피드를 가리킵니다.

1. 왼쪽 창에서 > 오른쪽 위에 있는 **설정** 단추를 클릭 하 고 **확장**을 클릭 합니다. 
2. **사용 가능한 확장** 탭에는 설치에 사용할 수 있는 피드의 확장이 나열 됩니다.
3. 확장을 클릭 하 여 **세부 정보** 창에서 확장 설명, 버전, 게시자 및 기타 정보를 확인 합니다.
4. 확장을 설치 하려면 **설치** 를 클릭 합니다. 이 변경 작업을 수행 하기 위해 게이트웨이를 관리자 모드로 실행 해야 하는 경우 UAC 권한 상승 프롬프트가 표시 됩니다. 설치가 완료 되 면 브라우저가 자동으로 새로 고쳐지고 새 확장이 설치 된 Windows 관리 센터가 다시 로드 됩니다. 설치 하려는 확장이 이전에 설치 된 확장에 대 한 업데이트 인 경우 **최신 버전으로 업데이트** 단추를 클릭 하 여 업데이트를 설치할 수 있습니다. **설치** 된 확장 탭으로 이동 하 여 설치 된 확장을 보고 **상태** 열에서 업데이트를 사용할 수 있는지 확인할 수도 있습니다.

## <a name="installing-extensions-from-a-different-feed"></a>다른 피드에서 확장 설치

Windows 관리 센터는 여러 피드를 지원 하며 한 번에 둘 이상의 피드에서 패키지를 보고 관리할 수 있습니다. NuGet V2 Api 또는 파일 공유를 지 원하는 모든 NuGet 피드는에서 확장을 설치 하기 위해 Windows 관리 센터에 추가할 수 있습니다.

1. 왼쪽 창에서 > 오른쪽 위에 있는 **설정** 단추를 클릭 하 고 **확장**을 클릭 합니다.
2. 오른쪽 창에서 **피드** 탭을 클릭 합니다.
3. **추가** 단추를 클릭 하 여 다른 피드를 추가 합니다. NuGet 피드의 경우 NuGet V2 피드 URL을 입력 합니다. NuGet 피드 공급자나 관리자는 URL 정보를 제공할 수 있어야 합니다. 파일 공유의 경우 확장 패키지 파일 (. nupkg)이 저장 되는 파일 공유의 전체 경로를 입력 합니다.
4. **추가**를 클릭합니다. 이 변경 작업을 수행 하기 위해 게이트웨이를 관리자 모드로 실행 해야 하는 경우 UAC 권한 상승 프롬프트가 표시 됩니다.

**사용 가능한 확장** 목록에는 등록 된 모든 피드의 확장이 표시 됩니다. **패키지 피드** 열을 사용 하 여 각 확장의 피드가 무엇 인지 확인할 수 있습니다.

## <a name="uninstalling-an-extension"></a>확장 제거

이전에 설치한 모든 확장을 제거 하거나 Windows 관리 센터 설치의 일부로 사전 설치 된 모든 도구를 제거할 수 있습니다.

1. 왼쪽 창에서 > 오른쪽 위에 있는 **설정** 단추를 클릭 하 고 **확장**을 클릭 합니다. 
2. **설치 된 확장 탭을** 클릭 하면 설치 된 모든 확장을 볼 수 있습니다.
3. 제거할 확장을 선택 하 고 **제거**를 클릭 합니다.

제거가 완료 되 면 브라우저가 자동으로 새로 고쳐지고 확장이 제거 된 상태에서 Windows 관리 센터가 다시 로드 됩니다. Windows 관리 센터의 일부로 사전 설치 된 도구를 제거한 경우 **사용 가능한 확장** 탭에서이 도구를 다시 설치할 수 있습니다.

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>인터넷에 연결 되지 않은 컴퓨터에 확장 설치

인터넷에 연결 되어 있지 않거나 프록시 뒤에 있는 컴퓨터에 Windows 관리 센터를 설치 하는 경우 Windows 관리 센터 피드에서 확장을 액세스 및 설치 하지 못할 수 있습니다. 수동으로 또는 PowerShell 스크립트를 사용 하 여 확장 패키지를 다운로드 하 고 Windows 관리 센터를 구성 하 여 파일 공유 또는 로컬 드라이브에서 패키지를 검색할 수 있습니다.

### <a name="manually-downloading-extension-packages"></a>수동으로 확장 패키지 다운로드

1. 인터넷에 연결 된 다른 컴퓨터에서 웹 브라우저를 열고 다음 URL로 이동 합니다. [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

   * Msft-sme.myget.org에서 계정을 만들고 로그인 하 여 확장 패키지를 확인 해야 할 수 있습니다.

2. 설치 하려는 패키지의 이름을 클릭 하 여 패키지 세부 정보 페이지를 표시 합니다.
3. 패키지 세부 정보 페이지의 오른쪽 창에서 **다운로드** 링크를 클릭 하 고 확장에 대 한 nupkg 파일을 다운로드 합니다.
4. 다운로드 하려는 모든 패키지에 대해 2 단계와 3 단계를 반복 합니다.
5. Windows 관리 센터가 설치 된 컴퓨터 또는 컴퓨터의 로컬 디스크에서 액세스할 수 있는 파일 공유에 패키지 파일을 복사 합니다.
6. [지침에 따라 다른 피드에서 확장을 설치](#installing-extensions-from-a-different-feed)합니다.

### <a name="downloading-packages-with-a-powershell-script"></a>PowerShell 스크립트를 사용 하 여 패키지 다운로드

Nuget 피드에서 NuGet 패키지를 다운로드 하는 데 사용할 수 있는 많은 스크립트가 인터넷에서 제공 됩니다. Microsoft에서 [Jon Galloway](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), 선임 프로그램 관리자가 제공 하는 스크립트를 사용 합니다.

1. [블로그 게시물](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)에 설명 된 대로 스크립트를 NuGet 패키지로 설치 하거나 스크립트를 복사 하 여 PowerShell ISE에 붙여 넣습니다.
2. 스크립트의 첫 번째 줄을 NuGet 피드의 v2 URL로 편집 합니다. Windows 관리 센터 공식 피드에서 패키지를 다운로드 하는 경우 아래 URL을 사용 합니다.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. 스크립트를 실행 하면 피드의 모든 NuGet 패키지가 다음 로컬 폴더에 다운로드 됩니다.%USERPROFILE%\Documents\NuGetLocal
4. [지침에 따라 다른 피드에서 확장을 설치](#installing-extensions-from-a-different-feed)합니다.

## <a name="manage-extensions-with-powershell"></a>PowerShell을 사용 하 여 확장 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터 미리 보기에는 게이트웨이 확장을 관리 하는 PowerShell 모듈이 포함 되어 있습니다.

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

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdkextendextensibility-overviewmd"></a>[Windows 관리 센터 SDK를 사용 하 여 확장을 빌드하는 방법에 대해 자세히 알아보세요](../extend/extensibility-overview.md).