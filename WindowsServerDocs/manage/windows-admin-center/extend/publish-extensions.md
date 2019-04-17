---
title: Windows Admin Center 용 확장 게시
description: Windows Admin Center (Project Honolulu)에 대 한 확장 게시
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 762bd4613fa8ad6cdfb5b44745a7ce78b331499d
ms.sourcegitcommit: 3883eebbba70bfea0221e510863ee1a724a5f926
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/29/2018
ms.locfileid: "5783755"
---
# 확장 게시

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

확장을 개발한 후에 게시 하 고 테스트 하거나 사용 하 여 다른 사용자에 게 사용할 수 있도록 합니다. 대상과 게시 하는 목적에 따라 단계 및 게시에 대 한 요구 사항 아래 소개 하는 몇 가지 옵션이 있습니다.

## 게시 옵션

Windows Admin Center를 지 원하는 패키지를 구성할 수 있는 원본에 대 한 세 가지 옵션을 가지 있습니다.
* Microsoft의 공개 Windows Admin Center NuGet 피드
* 고유한 개인 NuGet 피드
* 로컬 또는 네트워크 파일 공유

### Windows Admin Center 확장 피드를 게시 합니다.

기본적으로 Windows Admin Center는 NuGet에 연결 된 피드 microsoft Windows Admin Center 제품 팀에서 유지 관리 합니다. Microsoft에서 개발한 새로운 확장의 초기 미리 보기 버전은이 피드를 게시 되 고 Windows Admin Center 사용자에 게 사용할 수 있습니다. 계획을 빌드하고 확장을 공개적으로 해제 하는 외부 개발자가이 피드를 게시 하려면 [요청을 제출할](#publishing-your-extension-to-the-windows-admin-center-feed) 수도 있습니다.

### 다른 NuGet에 게시 피드

고유한 NuGet 많은 [호스팅 서비스를 개인 원본을 설정 또는 NuGet을 사용 하 여 다양 한 옵션](https://docs.microsoft.com/nuget/hosting-packages/overview)중 하나를 사용 하 여 확장을 게시 하려면 피드를 만들 수 있습니다. NuGet 피드 NuGet v2 API를 지원 해야 합니다. Windows Admin Center 피드 인증 현재 지원 되지 않으므로, 피드 누구 든 지에 대 한 읽기 액세스를 허용 하도록 구성 해야 합니다.

### 파일 공유에 게시

확장에 대 한 액세스를 조직에 또는 제한 된 그룹의 사용자를 제한 하려면 피드 확장으로 SMB 파일 공유를 사용할 수 있습니다. 이 경우 대화에 대 한 액세스를 허용 하는 것에 대 한 파일 공유 및 폴더 권한 적용 됩니다.

## 확장 릴리스 준비

읽고 개발 항목에서는 다음을 고려 있는지 확인 합니다.

- [도구의 가시성 제어](guides/dynamic-tool-display.md)
- [문자열 및 지역화](guides/strings-localization.md)

### 미리 보기 릴리스를 해제 하는 것이 좋습니다.

좋습니다 평가 위해 확장의 미리 보기 버전을 해제 하는 경우 있습니다.

- 확장의 제목.nuspec 파일에서의 끝에 "(미리 보기)"를 추가 합니다.
- .Nuspec 파일 확장명의 설명에 대 한 제한을 설명 합니다.

## 확장 패키지 만들기

Windows Admin Center에서 NuGet 패키지 및 배포 하 고 다운로드 하는 확장에 대 한 피드를 사용 합니다.  패키지를 전달할 순서로 플러그 인 및 확장 포함 된 NuGet 패키지를 생성 해야 합니다.  단일 패키지로는 UI 확장 뿐만 아니라 게이트웨이 플러그 인 포함 될 수 있으며 다음 섹션에서는 안내 하는 프로세스.

### 1. 확장을 작성 합니다.

확장을 패키징하 면 시작, 파일 시스템에 새 디렉터리를 만들 준비가 되는 즉시 콘솔과 CD를 엽니다.  이 모든 nuspec 및 콘텐츠 디렉터리를 패키지를 구성 하는 포함 하는 데 사용할 수 있는 루트 디렉터리 됩니다.  이 문서의 기간에 대 한 "NuGet 패키지로"이이 폴더는 참조 합니다.

#### UI 확장

UI 확장에 필요한 모든 콘텐츠를 수집 프로세스를 시작 하려면 도구에서 "빌드 gulp"를 실행 하 고 빌드를 성공적으로 수행 되 고 있는지 확인 합니다.  (Src 디렉터리의 동일한 수준)에서 확장의 루트 디렉터리에 있는 "bundle" 라는 폴더에 함께 모든 구성 요소를 패키지 하는 프로세스입니다.  이 디렉터리와 모든 복사의 경우 "NuGet 패키지" 폴더에 붙여 넣습니다.

#### 게이트웨이 플러그 인

(이 될 수 있음 Visual Studio를 열고 작성 단추를 클릭 하기만) 빌드 인프라를 사용 하 여 컴파일 및 플러그를 빌드하십시오.  플러그를 표시 하는 dll을 빌드 출력 디렉터리를 엽니다 복사한 "패키지" 호출 "NuGet 패키지" 디렉터리 내에 새 폴더에 배치 합니다.  FeatureInterface dll, 코드를 표시 하는 dll 방금 복사할 필요가 없습니다.

### 2..nuspec 파일 만들기

NuGet 패키지를 만들려면 먼저.nuspec 파일을 작성 해야 합니다. .Nuspec 파일이 NuGet 패키지 메타 데이터를 포함 하는 XML 매니페스트입니다. 이 매니페스트는 소비자에 게 정보를 제공 하 고 패키지를 빌드하는 데 사용 됩니다.  이 파일을 "NuGet 패키지" 폴더의 루트에 배치 합니다.

예제.nuspec 파일과 필요 하거나 권장 속성 목록은 다음과 같습니다. 전체 스키마 [.nuspec 참조](https://docs.microsoft.com/nuget/reference/nuspec)를 참조 하세요. 선택한 파일 이름 사용 하 여 프로젝트의 루트 폴더에.nuspec 파일을 저장 합니다.

> [!IMPORTANT]
> ```<id>``` .nuspec 파일의 값과 일치 해야 합니다 ```"name"``` 프로젝트의 값 ```manifest.json``` 게시 된 확장 그렇지 않으면 파일을 Windows Admin Center에서 성공적으로 로드 되지 않습니다.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <packageTypes>
      <packageType name="WindowsAdminCenterExtension" />
    </packageTypes>  
    <id>contoso.project.extension</id>
    <version>1.0.0</version>
    <title>Contoso Hello Extension</title>
    <authors>Contoso</authors>
    <owners>Contoso</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <projectUrl>https://msft-sme.myget.org/feed/windows-admin-center-feed/package/nuget/contoso.sme.hello-extension</projectUrl>
    <licenseUrl>http://YourLicenseLink</licenseUrl>
    <iconUrl>http://YourLogoLink</iconUrl>
    <description>Hello World extension by Contoso</description>
    <copyright>(c) Contoso. All rights reserved.</copyright> 
    <tags></tags>
  </metadata>
  <files>
    <file src="bundle\**\*.*" target="ux" />
    <file src="package\**\*.*" target="gateway" />
  </files>
</package>
```

#### 필요 하거나 권장 속성

| 속성 이름 | 필수 / 권장 | 설명 |
| ---- | ---- | ---- |
| 패키지 유형 | 필수 | Windows Admin Center 확장에 대해 정의 된 NuGet 패키지 유형인 "WindowsAdminCenterExtension"를 사용 합니다. |
| id | 필수 | 피드 내 고유한 패키지 식별자. 이 값은 프로젝트의 manifest.json 파일에 "name" 값과 일치 해야 합니다.  지침 [선택 패키지 고유 식별자를](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number) 참조 하세요. |
| title | 피드 Windows Admin Center를 게시 하는 데 필요한 | Windows Admin Center 확장 관리자에 표시 되는 패키지 이름입니다. |
| 버전 | 필수 | 확장 버전입니다. [의미 체계 버전 관리 (SemVer 규칙)을](http://semver.org/spec/v1.0.0.html) 사용 하 여 권장 하지만 필요 없습니다. |
| 작성자 | 필수 | 회사를 대신 하 여을 게시 하는 경우에 회사 이름을 사용 합니다. |
| description | 필수 | 확장의 기능에 대 한 설명을 제공 합니다. |
| iconUrl | 피드 Windows Admin Center를 게시 하는 경우 권장 사항 | 확장 관리자를 표시할 아이콘에 대 한 URL입니다. |
| projectUrl | 피드 Windows Admin Center를 게시 하는 데 필요한 | 확장의 웹 사이트 URL입니다. 별도 웹 사이트가 없는 경우에 피드 NuGet 패키지 웹 페이지에 대 한 URL을 사용 합니다. |
| licenseUrl | 피드 Windows Admin Center를 게시 하는 데 필요한 | 확장의 최종 사용자 사용권 계약 URL입니다. |
| 파일 | 필수 | 이러한 두 설정 UI 확장 및 게이트웨이 플러그 인에 대 한 Windows Admin Center에서 예상 하는 폴더 구조를 설정 합니다. |

### 3. 확장 NuGet 패키지 빌드

위에서 만든.nuspec 파일을 사용 하 여 NuGet 패키지.nupkg 파일을 업로드 하 고 피드 NuGet에 게시할 수 있는 만들가 있습니다.

1. [NuGet 클라이언트 도구 웹 사이트](https://docs.microsoft.com/nuget/install-nuget-client-tools)에서 nuget.exe CLI 도구를 다운로드 합니다.
2. .Nupkg 파일을 만들려면 "nuget.exe 팩 [.nuspec 파일 이름]"를 실행 합니다.

### 4. 확장 NuGet 패키지를 서명합니다.

확장에 포함 된 모든.dll 파일은 신뢰할 수 있는 인증 기관 (CA)에서 인증서로 서명 해야 합니다. 기본적으로 Windows Admin Center는 프로덕션 모드에서 실행 중일 때 실행 되 고 서명 되지 않은.dll 파일을 차단 됩니다.

또한 좋습니다 패키지의 무결성을 보장 확장 NuGet 패키지를 서명 있지만 필수 단계 하는 것은 아닙니다.

### 5. 확장 NuGet 패키지를 테스트 합니다.

확장 패키지 테스트를 위해 준비 되었습니다! NuGet 피드를.nupkg 파일을 업로드 하거나 파일 공유에 복사 합니다. 을 보고 하려면 다른 피드 또는 파일 공유에서 패키지를 다운로드 합니다 필요한 [피드 구성을 변경](../configure/using-extensions.md#installing-extensions-from-a-different-feed) 하 고 NuGet 피드 또는 파일을 공유할 수 있습니다. 테스트 하는 경우에 속성을 올바르게 확장 관리자에 표시 되 고 성공적으로 설치 하 고 확장을 제거할 수 있는지 확인 합니다.

## Windows Admin Center를 게시 하는 확장 피드

배포 피드 Windows Admin Center를 게시 하 여 확장 사용 가능한 하 게 만들 하는 Windows Admin Center 사용자에 게 수 있습니다. Windows Admin Center SDK 미리 보기에 여전히 존재 하므로 개발 문제를 해결 및, 품질 제품을 제공할 수 있는지 확인 하 고 사용자에 게 경험와 밀접 하 게 작동 하도록 하겠습니다.

확장의 초기 버전을 릴리스하기 전에 하는 확장 검토 요청을 제출 하면 Microsoft 적어도 2 ~ 3 주 검토 충분히 확보 하는 릴리스 전에 하 고 필요한 경우 확장을 변경 하는 것이 좋습니다. 확장을 게시할 준비가 되 면 검토를 위해 우리에 게 보낼 필요 하며 승인 되 면 사용자에 대 한 피드를 게시 합니다 했습니다.

그런 다음 확장에 대 한 업데이트를 해제 하려는 리뷰에 대 한 다른 요청을 제출 해야 합니다. 변경 범위에 따라 업데이트 리뷰에 대 한 소요 시간이 짧은 수 일반적으로 해야 합니다.

### Microsoft는 확장 검토 요청 제출

확장 검토 요청을 제출 하려면 다음 정보를 입력 하 고 [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request)를 메일로 보낼 합니다. 우리는 주 메일 응답 합니다.

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### 검토 및 게시를 위해 확장 패키지를 제출 합니다.

[확장 패키지를 만들기](#creating-an-extension-package) 위한 지침에 따라 및.nuspec 파일 제대로 정의 되 고 파일은 서명 했는지 확인 합니다. 또한 다음과 같은 프로젝트 웹 사이트 수 있는 것이 좋습니다.

- 자세한 설명은 스크린샷 또는 비디오를 포함 하 여 확장
- 피드백 또는 질문을 수신 하도록 메일 주소 또는 웹 사이트 기능

확장을 게시할 준비가 되 면 [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review) 에 게 메일 보내기 및 보내주세요 확장 패키지 하는 방법에 지침을 제공할 예정입니다. 패키지를 받은 후 검토 하 고 승인 되 면 피드 Windows Admin Center에 게시 하겠습니다.