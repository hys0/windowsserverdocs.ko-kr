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
ms.sourcegitcommit: be0144eb59daf3269bebea93cb1c467d67e2d2f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/20/2018
ms.locfileid: "4080920"
---
# 개발 환경 준비

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

Windows Admin Center SDK로 확장 개발을 시작합니다!  이 문서의 위해 환경을 빌드 및 테스트 Windows Admin Center에 대 한 확장을 구동 하는 프로세스에 살펴보겠습니다.

> [!NOTE]
> Windows Admin Center SDK를 처음 사용하십니까?  [Extensions for Windows Admin Center용 확장](extensibility-overview.md)에 대해 알아보세요.

개발 환경을 준비하려면 다음 단계를 수행합니다.

## 필수 구성 요소 설치

SDK를 사용하여 개발을 시작하려면 다음과 같은 필수 구성 요소를 다운로드하고 설치합니다.

* [Windows Admin Center](https://aka.ms/WACDownloadPage) (GA 또는 미리 보기 버전)
* Visual Studio 또는 [Visual Studio Code](http://code.visualstudio.com)
* [노드 패키지 관리자](https://npmjs.com/get-npm) (8.12.0 이상)
* [Nuget](https://www.nuget.org/downloads)(확장 게시용)

> [!NOTE]
> 다음 단계를 수행하려면 개발자 모드에서 Windows Admin Center를 설치하고 실행해야 합니다. 개발자 모드를 통해 Windows Admin Center가 서명되지 않은 확장 패키지를 로드할 수 있습니다.
>
>  개발자 모드를 사용하려면 명령줄에서 DEV_MODE=1 매개 변수를 사용하여 Windows Admin Center를 설치합니다. 아래 예제에서는 ```<version>```을 설치하는 버전, 즉 ```WindowsAdminCenter1809.msi```로 변경합니다.
>
> ```msiexec /i WindowsAdminCenter<version>.msi DEV_MODE=1```

## 전역 종속성 설치

다음으로, 설치 또는 노드 패키지 관리자를 사용 하 여 프로젝트에 필요한 종속성을 업데이트 합니다. 이러한 종속성은 전역에 설치되며 모든 프로젝트에 대해 사용할 수 있습니다.

```
npm install -g npm

npm install -g @angular/cli@1.6.5

npm install -g gulp
npm install -g typescript
npm install -g tslint
npm install -g windows-admin-center-cli
```

>[!NOTE]
>그러나 1.6.5 보다 큰 버전을 설치 하는 경우 로컬 cli 버전이 설치 된 버전을 일치 하지 않습니다 gulp 빌드 단계에서 경고를 받게 됩니다 주의 @angular/cli의 최신 버전을 설치 수 있습니다.

## 다음 단계

사용자 환경을 준비 했으므로 콘텐츠 생성을 시작 준비가 되었습니다.

- [도구](develop-tool.md) 확장 만들기
- [솔루션](develop-solution.md) 확장 만들기
- [게이트웨이 플러그 인](develop-gateway-plugin.md) 만들기
- 자세한 내용은 [가이드](guides.md) 참고

## SDK 디자인 도구 키트

확인 하는 Windows Admin Center [SDK 디자인 도구 키트](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)하세요! 이 도구 키트는 Windows Admin Center 스타일, 컨트롤 및 페이지 템플릿을 사용 하 여 powerpoint에서 확장 머킹 신속 하 게 하기 위해 설계 되었습니다. 확장 수 모양을 확인 Windows Admin Center에서 코딩을 시작 하기 전에!

