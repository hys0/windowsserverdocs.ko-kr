---
title: 확장 설치 및 관리
description: Windows Admin Center에서 확장을 설치하고 관리합니다(Project Honolulu).
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 7c1a70e36dfac9b23ded8f920ffcc8cccbfff023
ms.sourcegitcommit: 06ae7c34c648538e15c4d9fe330668e7df32fbba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78371121"
---
# <a name="install-and-manage-extensions"></a>확장 설치 및 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center는 각 연결 형식 및 도구를 개별적으로 설치, 제거 및 업데이트할 수 있는 확장인 확장 가능한 플랫폼으로 빌드됩니다. Microsoft 및 다른 개발자가 게시한 새 확장을 검색하고, 전체 Windows Admin Center 설치를 업데이트하지 않고도 개별적으로 설치하고 업데이트할 수 있습니다. 또한 별도의 NuGet 피드 또는 파일 공유를 구성하고, 조직 내에서 내부적으로 사용할 확장을 배포할 수도 있습니다.

## <a name="installing-an-extension"></a>확장 설치

Windows Admin Center에는 지정된 NuGet 피드에서 사용할 수 있는 확장이 표시됩니다. Windows Admin Center는 기본적으로 Microsoft 및 다른 개발자가 게시한 확장을 호스팅하는 Microsoft 공식 NuGet 피드를 가리킵니다.

1. 오른쪽 위에서 **설정** 단추를 클릭하고, 왼쪽 창에서 **확장**을 클릭합니다. 
2. **사용 가능한 확장** 탭에서 설치에 사용할 수 있는 피드의 확장이 나열됩니다.
3. 확장을 클릭하여 **세부 정보** 창에서 확장 설명, 버전, 게시자 및 기타 정보를 봅니다.
4. **설치**를 클릭하여 확장을 설치합니다. 게이트웨이를 관리자 모드로 실행하여 이 변경 작업을 수행해야 하는 경우 UAC 권한 상승 프롬프트가 표시됩니다. 설치가 완료되면 브라우저가 자동으로 새로 고쳐지고, 새 확장이 설치된 Windows Admin Center가 다시 로드됩니다. 설치하려는 확장이 이전에 설치한 확장에 대한 업데이트인 경우 **최신으로 업데이트** 단추를 클릭하여 해당 업데이트를 설치할 수 있습니다. 또한 **설치된 확장** 탭으로 이동하여 설치된 확장을 보고, **상태** 열에서 업데이트를 사용할 수 있는지 확인할 수도 있습니다.

## <a name="installing-extensions-from-a-different-feed"></a>다른 피드에서 확장 설치

Windows Admin Center는 여러 피드를 지원하며, 여러 피드에서 한 번에 패키지를 보고 관리할 수 있습니다. NuGet V2 API 또는 파일 공유를 지원하는 모든 NuGet 피드를 Windows Admin Center에 추가하여 확장을 설치할 수 있습니다.

1. 오른쪽 위에서 **설정** 단추를 클릭하고, 왼쪽 창에서 **확장**을 클릭합니다.
2. 오른쪽 창에서 **피드** 탭을 클릭합니다.
3. **추가** 단추를 클릭하여 다른 피드를 추가합니다. NuGet 피드의 경우 NuGet V2 피드 URL을 입력합니다. NuGet 피드 공급자 또는 관리자는 URL 정보를 제공할 수 있어야 합니다. 파일 공유의 경우 확장 패키지 파일(.nupkg)이 저장된 파일 공유의 전체 경로를 입력합니다.
4. **추가**를 클릭합니다. 게이트웨이를 관리자 모드로 실행하여 이 변경 작업을 수행해야 하는 경우 UAC 권한 상승 프롬프트가 표시됩니다.

**사용 가능한 확장** 목록에는 등록된 모든 피드의 확장이 표시됩니다. **패키지 피드** 열을 사용하여 각 확장의 피드를 확인할 수 있습니다.

## <a name="uninstalling-an-extension"></a>확장 제거

이전에 설치한 확장을 모두 제거하거나 Windows Admin Center 설치의 일부로 미리 설치된 도구를 모두 제거할 수도 있습니다.

1. 오른쪽 위에서 **설정** 단추를 클릭하고, 왼쪽 창에서 **확장**을 클릭합니다. 
2. **설치된 확장** 탭을 클릭하여 설치된 모든 확장을 봅니다.
3. 제거할 확장을 선택한 다음, **제거**를 클릭합니다.

제거가 완료되면 브라우저가 자동으로 새로 고쳐지고, 확장이 제거된 Windows Admin Center가 다시 로드됩니다. Windows Admin Center의 일부로 미리 설치된 도구를 제거하면 **사용 가능한 확장** 탭에서 해당 도구를 다시 설치할 수 있습니다.

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>인터넷에 연결되지 않은 컴퓨터에 확장 설치

Windows Admin Center가 인터넷에 연결되어 있지 않거나 프록시 뒤에 있는 컴퓨터에 설치되는 경우 Windows Admin Center 피드에서 확장에 액세스하여 설치하지 못할 수 있습니다. 수동으로 또는 PowerShell 스크립트를 사용하여 확장 패키지를 다운로드하고, 파일 공유 또는 로컬 드라이브에서 패키지를 검색하도록 Windows Admin Center를 구성할 수 있습니다.

### <a name="manually-downloading-extension-packages"></a>수동으로 확장 패키지 다운로드

1. 인터넷에 연결된 다른 컴퓨터에서 웹 브라우저를 열고, [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) URL로 이동합니다. 

   * 계정을 msft-sme.myget.org에 만들고 로그인하여 확장 패키지를 확인해야 할 수 있습니다.

2. 설치하려는 패키지의 이름을 클릭하여 패키지 세부 정보 페이지를 봅니다.
3. 패키지 세부 정보 페이지의 오른쪽 창에서 **다운로드** 링크를 클릭하여 확장에 대한 .nupkg 파일을 다운로드합니다.
4. 다운로드하려는 모든 패키지에 대해 2단계와 3단계를 반복합니다.
5. 패키지 파일을 Windows Admin Center가 설치된 컴퓨터 또는 컴퓨터의 로컬 디스크에서 액세스할 수 있는 파일 공유에 복사합니다.
6. [지침에 따라 다른 피드의 확장을 설치합니다](#installing-extensions-from-a-different-feed).

### <a name="downloading-packages-with-a-powershell-script"></a>PowerShell 스크립트를 사용하여 패키지 다운로드

인터넷에는 NuGet 피드에서 NuGet 패키지를 다운로드하는 데 사용할 수 있는 스크립트가 많이 있습니다. 여기서는 Microsoft의 수석 프로그램 관리자인 [Jon Galloway가 제공한 스크립트](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)를 사용합니다.

1. [블로그 게시물](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)에서 설명한 대로 스크립트를 NuGet 패키지로 설치하거나, 스크립트를 복사하여 PowerShell ISE에 붙여넣습니다.
2. 스크립트의 첫 번째 줄을 NuGet 피드의 v2 URL로 편집합니다. Windows Admin Center 공식 피드에서 패키지를 다운로드하는 경우 아래 URL을 사용합니다.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. 스크립트를 실행합니다. 그러면 모든 NuGet 패키지를 피드에서 %USERPROFILE%\Documents\NuGetLocal 로컬 폴더로 다운로드합니다.
4. [지침에 따라 다른 피드의 확장을 설치합니다](#installing-extensions-from-a-different-feed).

## <a name="manage-extensions-with-powershell"></a>PowerShell을 사용하여 확장 관리

Windows Admin Center 미리 보기에는 게이트웨이 확장을 관리하는 PowerShell 모듈이 포함되어 있습니다.

[!INCLUDE [ps-extensions](../includes/ps-extensions.md)]

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdk"></a>[Windows Admin Center SDK를 사용하여 확장을 빌드하는 방법에 대해 자세히 알아보세요](../extend/extensibility-overview.md).