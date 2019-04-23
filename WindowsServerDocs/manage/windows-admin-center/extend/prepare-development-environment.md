---
title: 개발 환경 준비
description: 개발 환경 Windows Admin Center SDK 준비(Project Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 09/18/2018
ms.prod: windows-server-threshold
ms.openlocfilehash: 7b1a0672ee374f3e2d1339c43576db0e5cabdc36
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834764"
---
# <a name="prepare-your-development-environment"></a>개발 환경 준비

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center SDK로 확장 개발을 시작합니다!  이 문서에서는 환경의 구성 및 빌드하고 Windows Admin Center 대 한 확장을 테스트를 실행 하는 프로세스를 설명 합니다.

> [!NOTE]
> Windows Admin Center SDK를 처음 사용하십니까?  [Extensions for Windows Admin Center용 확장](extensibility-overview.md)에 대해 알아보세요.

개발 환경을 준비하려면 다음 단계를 수행합니다.

## <a name="install-prerequisites"></a>필수 구성 요소 설치

SDK를 사용하여 개발을 시작하려면 다음과 같은 필수 구성 요소를 다운로드하고 설치합니다.

* [Windows Admin Center](https://aka.ms/WACDownloadPage) (GA 또는 미리 보기 버전)
* Visual Studio 또는 [Visual Studio Code](http://code.visualstudio.com)
* [Node Package Manager](https://npmjs.com/get-npm) (8.12.0 이상)
* [Nuget](https://www.nuget.org/downloads)(확장 게시용)

> [!NOTE]
> 다음 단계를 수행하려면 개발자 모드에서 Windows Admin Center를 설치하고 실행해야 합니다. 개발자 모드를 통해 Windows Admin Center가 서명되지 않은 확장 패키지를 로드할 수 있습니다.
>
>  개발자 모드를 사용하려면 명령줄에서 DEV_MODE=1 매개 변수를 사용하여 Windows Admin Center를 설치합니다. 아래 예제에서는 ```<version>```을 설치하는 버전, 즉 ```WindowsAdminCenter1809.msi```로 변경합니다.
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## <a name="install-global-dependencies"></a>전역 종속성 설치

다음으로, 설치 또는 Node Package Manager를 사용 하 여 프로젝트에 필요한 종속성을 업데이트 합니다. 이러한 종속성은 전역에 설치되며 모든 프로젝트에 대해 사용할 수 있습니다.

```
npm install -g npm

npm install -g @angular/cli@1.6.5

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>그러나 이후 버전을 설치할 수 있습니다 @angular/cli, 1.6.5 보다 큰 버전을 설치 하면 로컬 cli 버전을 설치 된 버전과 일치 하지 않음을 gulp 빌드 단계에서 경고가 수신 됩니다 고려해 야 합니다.

## <a name="next-steps"></a>다음 단계

이제는 환경의 준비 된 콘텐츠를 만들 준비가 되었습니다.

- [도구](develop-tool.md) 확장 만들기
- [솔루션](develop-solution.md) 확장 만들기
- [게이트웨이 플러그 인](develop-gateway-plugin.md) 만들기
- 자세한 내용은 [가이드](guides.md) 참고

## <a name="sdk-design-toolkit"></a>SDK 디자인 도구 키트

이 Windows Admin Center 확인해 [SDK 디자인 도구 키트](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)! 이 도구 키트는 Windows Admin Center 스타일, 컨트롤 및 페이지 템플릿을 사용 하 여 PowerPoint의 확장 프로그램을 신속 하 게 모형을 수 있도록 설계 되었습니다. 새로운 확장 다음과 같을 수 있습니다 Windows Admin Center 코딩을 시작 하기 전에 확인 하세요.

