---
title: Windows 관리 센터에 대 한 확장 게시
description: Windows 관리 센터의 게시 확장 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 24beb287aa35757e1f8057920e8fd95828baf83b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385197"
---
# <a name="publishing-extensions"></a>확장 게시

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

확장을 개발한 후에는 해당 확장을 게시 하 고 다른 사용자가 테스트 하거나 사용할 수 있도록 합니다. 사용자의 게시 목적과 게시 목적에 따라 다음과 같은 몇 가지 옵션을 사용 하 여 게시에 대 한 단계 및 요구 사항을 확인할 수 있습니다.

## <a name="publishing-options"></a>게시 옵션

Windows 관리 센터에서 지 원하는 구성 가능한 패키지 원본에 대 한 세 가지 기본 옵션이 있습니다.
* Microsoft의 공용 Windows 관리 센터 NuGet 피드
* 사용자 고유의 개인 NuGet 피드
* 로컬 또는 네트워크 파일 공유

### <a name="publishing-to-the-windows-admin-center-extension-feed"></a>Windows 관리 센터 확장 피드에 게시 하는 중

기본적으로 Windows 관리 센터는 Microsoft의 Windows 관리 센터 제품 팀에서 유지 관리 하는 NuGet 피드에 연결 됩니다. Microsoft에서 개발한 새 확장의 초기 미리 보기 버전은이 피드에 게시 되 고 Windows 관리 센터 사용자가 사용할 수 있습니다. 확장 빌드 및 릴리스 확장을 계획 하는 외부 개발자는이 피드에 게시 하 [는 요청을 제출할](#publishing-your-extension-to-the-windows-admin-center-feed) 수도 있습니다.

### <a name="publishing-to-a-different-nuget-feed"></a>다른 NuGet 피드에 게시

[전용 소스를 설정 하거나 nuget 호스팅 서비스를 사용](https://docs.microsoft.com/nuget/hosting-packages/overview)하는 다양 한 옵션 중 하나를 사용 하 여 확장을 게시 하는 사용자 고유의 nuget 피드를 만들 수도 있습니다. NuGet 피드는 NuGet v2 API를 지원 해야 합니다. Windows 관리 센터는 현재 피드 인증을 지원 하지 않으므로 모든 사용자에 대 한 읽기 액세스를 허용 하도록 피드를 구성 해야 합니다.

### <a name="publishing-to-a-file-share"></a>파일 공유에 게시

조직 또는 제한 된 사용자 그룹에 대 한 확장의 액세스를 제한 하기 위해 SMB 파일 공유를 확장 피드로 사용할 수 있습니다. 이 경우 피드에 대 한 액세스를 허용 하기 위해 파일 공유 및 폴더 권한이 적용 됩니다.

## <a name="preparing-your-extension-for-release"></a>릴리스에 대 한 확장 준비

다음 개발 항목을 읽고 고려 하십시오.

- [도구의 가시성 제어](guides/dynamic-tool-display.md)
- [문자열 및 지역화](guides/strings-localization.md)

### <a name="consider-releasing-as-a-preview-release"></a>미리 보기 릴리스로 릴리스 고려

평가 목적으로 확장의 미리 보기 버전을 릴리스 하는 경우 다음을 수행 하는 것이 좋습니다.

- Nuspec 파일에서 확장 제목의 끝에 "(미리 보기)"를 추가 합니다.
- Nuspec 파일에서 확장의 설명에 대 한 제한 사항을 설명 합니다.

## <a name="creating-an-extension-package"></a>확장 패키지 만들기

Windows 관리 센터는 NuGet 패키지 및 피드를 활용 하 여 확장을 배포 하 고 다운로드 합니다.  패키지를 배송할 수 있도록 플러그 인 및 확장을 포함 하는 NuGet 패키지를 생성 해야 합니다.  단일 패키지에는 인터페이스 확장 및 게이트웨이 플러그 인이 모두 포함 될 수 있으며, 다음 섹션에서는이 프로세스를 안내 합니다.

### <a name="1-build-your-extension"></a>1. 확장 빌드

확장 패키지를 시작할 준비가 되 면 바로 파일 시스템에 새 디렉터리를 만들고, 콘솔을 열고, CD로 이동 합니다.  패키지를 구성 하는 모든 nuspec 및 콘텐츠 디렉터리를 포함 하는 데 사용할 루트 디렉터리입니다.  이 문서를 진행 하는 동안이 폴더를 "NuGet 패키지"로 참조 합니다.

#### <a name="ui-extensions"></a>UI 확장

UI 확장에 필요한 모든 콘텐츠를 수집 하는 프로세스를 시작 하려면 도구에서 "gulp build"를 실행 하 고 빌드에 성공 했는지 확인 합니다.  이 프로세스는 확장의 루트 디렉터리 (src 디렉터리의 동일한 수준)에 있는 "번들" 이라는 폴더에 모든 구성 요소를 함께 패키지 합니다.  이 디렉터리와 모든 콘텐츠를 "NuGet 패키지" 폴더에 복사 합니다.

#### <a name="gateway-plugins"></a>게이트웨이 플러그 인

빌드 인프라 사용 (Visual Studio를 열고 빌드 단추를 클릭 하는 것 처럼 간단할 수 있음), 플러그 인 컴파일 및 빌드.  빌드 출력 디렉터리를 열고 플러그 인을 나타내는 Dll을 복사 하 여 "Package" 라는 "NuGet Package" 디렉터리 내의 새 폴더에 넣습니다.  FeatureInterface dll은 복사할 필요가 없습니다. 코드를 나타내는 Dll만 있으면 됩니다.

### <a name="2-create-the-nuspec-file"></a>2. Nuspec 파일 만들기

NuGet 패키지를 만들려면 먼저. nuspec 파일을 만들어야 합니다. Nuspec 파일은 NuGet 패키지 메타 데이터를 포함 하는 XML 매니페스트입니다. 이 매니페스트는 패키지를 빌드하고 소비자에게 정보를 제공하는 데 사용됩니다.  이 파일을 "NuGet 패키지" 폴더의 루트에 저장 합니다.

다음은 nuspec 파일 및 필수 또는 권장 속성 목록입니다. 전체 스키마는 [. nuspec 참조](https://docs.microsoft.com/nuget/reference/nuspec)를 참조 하세요. 원하는 파일 이름으로 프로젝트의 루트 폴더에 nuspec 파일을 저장 합니다.

> [!IMPORTANT]
> Nuspec 파일의 ```"name"``` ```manifest.json``` 값은 프로젝트 파일의 값과 일치 해야 합니다. 그렇지 않으면 게시 된 확장 프로그램이 Windows 관리 센터에서 로드 되지 않습니다. ```<id>```

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

#### <a name="required-or-recommended-properties"></a>필수 또는 권장 속성

| 속성 이름 | 필수/권장 | 설명 |
| ---- | ---- | ---- |
| PackageType | 필수 | Windows 관리 센터 확장에 대해 정의 된 NuGet 패키지 유형인 "Windowsadmin중앙 확장"을 사용 합니다. |
| id | 필수 | 피드 내의 고유한 패키지 식별자입니다. 이 값은 프로젝트의 매니페스트. json 파일의 "name" 값과 일치 해야 합니다.  지침은 [고유한 패키지 식별자 선택](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number)을 참조하세요. |
| title | Windows 관리 센터 피드에 게시 하는 데 필요 합니다. | Windows 관리 센터 확장 관리자에 표시 되는 패키지의 이름입니다. |
| version | 필수 | 확장 버전입니다. [의미 체계 버전 관리 (SemVer 규칙)](http://semver.org/spec/v1.0.0.html) 를 사용 하는 것이 좋지만 필수는 아닙니다. |
| authors | 필수 | 회사를 대신 하 여 게시 하는 경우 회사 이름을 사용 합니다. |
| description | 필수 | 확장 기능에 대 한 설명을 제공 합니다. |
| iconUrl | Windows 관리 센터 피드에 게시할 때 권장 됨 | 확장 관리자에 표시할 아이콘의 URL입니다. |
| projectUrl | Windows 관리 센터 피드에 게시 하는 데 필요 합니다. | 확장의 웹 사이트에 대 한 URL입니다. 별도의 웹 사이트가 없는 경우 NuGet 피드에서 패키지 웹 페이지의 URL을 사용 합니다. |
| licenseUrl | Windows 관리 센터 피드에 게시 하는 데 필요 합니다. | 확장의 최종 사용자 사용권 계약에 대 한 URL입니다. |
| files | 필수 | 이러한 두 설정은 Windows 관리 센터에서 UI 확장 및 게이트웨이 플러그 인에 대해 예상 하는 폴더 구조를 설정 합니다. |

### <a name="3-build-the-extension-nuget-package"></a>3. 확장 NuGet 패키지 빌드

위에서 만든 nuspec 파일을 사용 하 여 nuget 피드에 업로드 하 고 게시할 수 있는 nupkg 파일을 만듭니다.

1. Nuget [클라이언트 도구 웹 사이트](https://docs.microsoft.com/nuget/install-nuget-client-tools)에서 nuget.exe CLI 도구를 다운로드 합니다.
2. "Nuget.exe pack [. nuspec file name]"을 실행 하 여 nupkg 파일을 만듭니다.

### <a name="4-signing-your-extension-nuget-package"></a>4. 확장 NuGet 패키지 서명

확장에 포함 된 모든 .dll 파일은 신뢰할 수 있는 CA (인증 기관)의 인증서를 사용 하 여 서명 해야 합니다. 기본적으로 서명 되지 않은 .dll 파일은 프로덕션 모드에서 실행 되는 Windows 관리 센터에서 실행 되지 않습니다.

또한 패키지의 무결성을 보장 하기 위해 확장 NuGet 패키지에 서명 하는 것이 좋지만이는 필수 단계가 아닙니다.

### <a name="5-test-your-extension-nuget-package"></a>5. 확장 NuGet 패키지 테스트

이제 확장 패키지를 테스트할 준비가 되었습니다. Nupkg 파일을 NuGet 피드에 업로드 하거나 파일 공유에 복사 합니다. 다른 피드 또는 파일 공유에서 패키지를 보고 다운로드 하려면 NuGet 피드 또는 파일 공유를 가리키도록 [피드 구성을 변경](../configure/using-extensions.md#installing-extensions-from-a-different-feed) 해야 합니다. 테스트할 때 확장 관리자에서 속성이 올바르게 표시 되 고 확장을 성공적으로 설치 하 고 제거할 수 있는지 확인 합니다.

## <a name="publishing-your-extension-to-the-windows-admin-center-feed"></a>Windows 관리 센터 피드에 확장 게시

Windows 관리 센터 피드에 게시 하면 모든 Windows 관리 센터 사용자가 확장을 사용할 수 있도록 설정할 수 있습니다. Windows 관리 센터 SDK는 아직 미리 보기 상태 이므로 사용자와 긴밀 하 게 협력 하 여 개발 문제를 해결 하 고 사용자에 게 품질 제품 및 환경을 제공할 수 있는지 확인 하는 것이 좋습니다.

확장의 초기 버전을 릴리스하기 전에 Microsoft에 릴리스 전 최소 2-3 주 동안 확장 검토 요청을 제출 하 여 검토 하는 데 충분 한 시간을 확보 하 고 필요한 경우 확장을 변경 하는 것이 좋습니다. 확장을 게시할 준비가 되 면 검토를 위해 해당 확장을 보내 주시기 바랍니다. 승인 되 면 피드에 게시 합니다.

그런 다음, 확장에 대 한 업데이트를 해제 하려는 경우 검토에 대 한 다른 요청을 제출 해야 합니다. 변경 범위에 따라 일반적으로 업데이트 검토의 소요 시간이 짧아집니다.

### <a name="submit-an-extension-review-request-to-microsoft"></a>Microsoft에 확장 검토 요청 제출

확장 검토 요청을 제출 하려면 다음 정보를 입력 하 고에 [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request)전자 메일로 보냅니다. 일주일 이내에 전자 메일에 회신 합니다.

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### <a name="submit-your-extension-package-for-review-and-publishing"></a>검토 및 게시를 위해 확장 패키지 제출

[확장 패키지를 만들기](#creating-an-extension-package) 위해 위의 지침을 따르고 nuspec 파일이 올바르게 정의 되었고 파일이 서명 되었는지 확인 합니다. 또한 다음을 포함 하는 프로젝트 웹 사이트를 포함 하는 것이 좋습니다.

- 스크린샷 또는 비디오를 포함 하는 확장에 대 한 자세한 설명
- 의견이 나 질문을 수신 하는 전자 메일 주소 또는 웹 사이트 기능

확장을 게시할 준비가 되 면에 [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review) 전자 메일을 보내면 확장 패키지를 전송 하는 방법에 대 한 지침을 제공 합니다. 패키지가 수신 되 면 검토 하 고 승인 되 면 Windows 관리 센터 피드에 게시 합니다.