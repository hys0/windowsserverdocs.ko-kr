---
title: 개발 환경 준비
description: 개발 환경 Windows Admin Center SDK 준비(Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.prod: windows-server
ms.openlocfilehash: 2aff8c0e43c6813c543511e643471c9cd9bcc292
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357038"
---
# <a name="prepare-your-development-environment"></a>개발 환경 준비

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows 관리 센터 SDK를 사용 하 여 확장 개발을 시작 해 보겠습니다.  이 문서에서는 Windows 관리 센터에 대 한 확장을 빌드 및 테스트 하기 위해 환경을 준비 하 고 실행 하는 프로세스에 대해 설명 합니다.

> [!NOTE]
> Windows Admin Center SDK를 처음 사용하십니까?  [Extensions for Windows Admin Center용 확장](extensibility-overview.md)에 대해 알아보세요.

개발 환경을 준비하려면 다음 단계를 수행합니다.

## <a name="install-prerequisites"></a>필수 구성 요소 설치

SDK를 사용하여 개발을 시작하려면 다음과 같은 필수 구성 요소를 다운로드하고 설치합니다.

* [Windows 관리 센터](https://aka.ms/WACDownloadPage) (GA 또는 preview 버전)
* Visual Studio 또는 [Visual Studio Code](http://code.visualstudio.com)
* [노드 패키지 관리자](https://npmjs.com/get-npm) (8.12.0 이상)
* [Nuget](https://www.nuget.org/downloads)(확장 게시용)

> [!NOTE]
> 다음 단계를 수행하려면 개발자 모드에서 Windows Admin Center를 설치하고 실행해야 합니다. 개발자 모드를 통해 Windows Admin Center가 서명되지 않은 확장 패키지를 로드할 수 있습니다.
>
>  개발자 모드를 사용하려면 명령줄에서 DEV_MODE=1 매개 변수를 사용하여 Windows Admin Center를 설치합니다. 아래 예제에서는 ```<version>```을 설치하는 버전, 즉 ```WindowsAdminCenter1809.msi```로 변경합니다.
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## <a name="install-global-dependencies"></a>전역 종속성 설치

그런 다음 노드 패키지 관리자를 사용 하 여 프로젝트에 필요한 종속성을 설치 하거나 업데이트 합니다. 이러한 종속성은 전역에 설치되며 모든 프로젝트에 대해 사용할 수 있습니다.

```
npm install -g npm

npm install -g @angular/cli@1.6.5

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>최신 버전의 @angular/cli를 설치할 수 있지만 1.6.5 보다 큰 버전을 설치 하는 경우 gulp 빌드 단계에서 로컬 cli 버전이 설치 된 버전과 일치 하지 않는다는 경고가 표시 됩니다.

## <a name="next-steps"></a>다음 단계

이제 환경이 준비 되었으므로 콘텐츠 만들기를 시작할 준비가 되었습니다.

- [도구](develop-tool.md) 확장 만들기
- [솔루션](develop-solution.md) 확장 만들기
- [게이트웨이 플러그 인](develop-gateway-plugin.md) 만들기
- 자세한 내용은 [가이드](guides.md) 참고

## <a name="sdk-design-toolkit"></a>SDK 디자인 도구 키트

Windows 관리 센터 [SDK 디자인 도구 키트](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)를 확인 하세요. 이 도구 키트는 PowerPoint에서 Windows 관리 센터 스타일, 컨트롤 및 페이지 템플릿을 사용 하 여 확장을 빠르게 시작 하는 데 도움이 되도록 설계 되었습니다. 코딩을 시작 하기 전에 Windows 관리 센터에서 확장의 모양을 확인 하세요.

