---
title: Windows Admin Center 대 한 확장 게시
description: Windows Admin Center (프로젝트 브라 티)에 대 한 확장 게시
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 762bd4613fa8ad6cdfb5b44745a7ce78b331499d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820424"
---
# <a name="publishing-extensions"></a>확장 게시

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

확장 프로그램을 개발한 후에 게시 하 고 테스트를 사용 하 여 다른 사용자에 게 사용할 수 있도록 해야 합니다. 대상 및 게시 하는 목적에 따라 게시에 대 한 요구 사항 및 단계와 함께 아래 소개 하는 몇 가지 옵션이 있습니다.

## <a name="publishing-options"></a>게시 옵션

가지 Windows Admin Center 지 구성할 수 있는 패키지 원본에 대 한 세 가지 기본 옵션이 있습니다.
* Microsoft의 공용 Windows Admin Center NuGet 피드
* 사용자 고유의 개인 NuGet 피드
* 로컬 또는 네트워크 파일 공유

### <a name="publishing-to-the-windows-admin-center-extension-feed"></a>피드 Windows Admin Center 확장 게시

기본적으로 Windows Admin Center 연결에 nuget 피드에 microsoft Windows Admin Center 제품 팀에서 유지 관리 합니다. Microsoft에서 개발한 새 확장의 초기 미리 보기 버전은이 피드에 게시 된 Windows Admin Center 사용자가 사용할 수 있습니다. 빌드 및 확장을 공개적으로 릴리스를 계획 하는 외부 개발자가 있을 수 있습니다 [요청할](#publishing-your-extension-to-the-windows-admin-center-feed) 이 피드에 게시 합니다.

### <a name="publishing-to-a-different-nuget-feed"></a>다른 NuGet에 게시 피드

사용자 고유의 NuGet 피드 많은 중 하나를 사용 하 여 확장을 게시를 만들 수도 있습니다 [전용 소스를 설정 또는 서비스를 호스트 하는 NuGet을 사용 하 여 다양 한 옵션](https://docs.microsoft.com/nuget/hosting-packages/overview)합니다. NuGet 피드의 NuGet v2 API를 지원 해야 합니다. Windows Admin Center 현재 피드 인증을 지원 하지 않으므로 피드는 모든 사용자에 대 한 읽기 액세스를 허용 하도록 구성 해야 합니다.

### <a name="publishing-to-a-file-share"></a>파일 공유에 게시

확장 프로그램의 액세스를 제한 된 사용자 그룹 또는 조직에 제한 피드 확장으로 SMB 파일 공유를 사용할 수 있습니다. 이 경우에 파일 공유 및 폴더 권한은 피드에 대 한 액세스를 허용 하는 데 적용 됩니다.

## <a name="preparing-your-extension-for-release"></a>확장 프로그램 릴리스 준비

읽기 및 다음 개발 항목에 있는지 확인 합니다.

- [도구의 표시 유형을 제어합니다](guides/dynamic-tool-display.md)
- [문자열 및 지역화](guides/strings-localization.md)

### <a name="consider-releasing-as-a-preview-release"></a>미리 보기 릴리스로 해제 하는 것이 좋습니다.

평가 목적에 대 한 확장 프로그램의 미리 보기 버전을 릴리스 하는 경우 좋습니다 있습니다.

- 확장 프로그램의 제목.nuspec 파일에서의 끝에 "(미리 보기)"를 추가
- .Nuspec 파일에서 확장의 설명에 제한 사항을 설명 합니다.

## <a name="creating-an-extension-package"></a>확장 패키지 만들기

Windows Admin Center NuGet 패키지 및 배포 확장을 다운로드 한 피드를 활용 합니다.  배송할 패키지에 대 한 순서 대로 플러그 인 및 확장 프로그램을 포함 하는 NuGet 패키지를 생성 해야 합니다.  단일 패키지에는 UI 확장 뿐만 아니라 게이트웨이 플러그 인을 모두 포함 될 수 있습니다 하 고 다음 섹션에서는 안내 하는 프로세스입니다.

### <a name="1-build-your-extension"></a>1. 빌드 확장

확장 프로그램을 패키징 시작, 파일 시스템에 새 디렉터리를 만들 준비가 되는 즉시 콘솔과 CD를 엽니다.  이 사용 하 여 모든 nuspec 및 콘텐츠 디렉터리는 패키지를 포함 하는 루트 디렉터리 됩니다.  이 문서의 기간에 대 한이 폴더 "NuGet 패키지"로 참조 됩니다.

#### <a name="ui-extensions"></a>UI 확장

UI 확장 프로그램에 필요한 모든 콘텐츠를 수집에 프로세스를 시작 하려면 "gulp 빌드" 하는 도구에서 실행 하 고 빌드에 성공 해야 합니다.  같은 수준에서 src 디렉터리의 확장 프로그램의 루트 디렉터리에 있는 모든 구성 요소가 함께 "번들" 라는 폴더를 패키지 하는 프로세스입니다.  이 디렉터리와 모든 복사의 내용을 "NuGet Package" 폴더에 있습니다.

#### <a name="gateway-plugins"></a>게이트웨이 플러그 인

(때문일 작성 단추를 클릭 하 여 Visual Studio를 열고) 빌드 인프라를 사용 하 여 컴파일 및 플러그 인을 작성 합니다.  빌드 출력 디렉터리를 엽니다 플러그 인을 나타내는 dll을 복사 하 고 "NuGet 패키지" 디렉터리 "패키지" 라는 새 폴더에 넣습니다.  코드를 나타내는 dll만 FeatureInterface dll을 복사할 필요가 없습니다.

### <a name="2-create-the-nuspec-file"></a>2. .Nuspec 파일 만들기

NuGet 패키지를 만들려면 먼저.nuspec 파일을 작성 해야 합니다. .Nuspec 파일은 NuGet 패키지 메타 데이터가 포함 된 XML 매니페스트입니다. 이 매니페스트 패키지를 만들 수와 소비자에 게 정보를 제공에 사용 됩니다.  "NuGet Package" 폴더의 루트에이 파일을 배치 합니다.

.Nuspec 파일의 예 및 필수 또는 권장 되는 속성 목록은 다음과 같습니다. 전체 스키마에 대 한 참조를 [.nuspec 참조](https://docs.microsoft.com/nuget/reference/nuspec)합니다. 사용자가 선택한 파일 이름 사용 하 여 프로젝트의 루트 폴더로.nuspec 파일을 저장 합니다.

> [!IMPORTANT]
> 합니다 ```<id>``` .nuspec 파일의 값과 일치 해야 합니다 ```"name"``` 프로젝트의 값 ```manifest.json``` 게시 된 확장 프로그램 파일, 그러지 않으면 Windows Admin Center 성공적으로 로드 되지 않습니다.

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

| 속성 이름 | 필요한 / 권장 | 설명 |
| ---- | ---- | ---- |
| packageType | 필수 | NuGet 패키지 형식인 Windows Admin Center 확장에 대 한 정의 "WindowsAdminCenterExtension"를 사용 합니다. |
| id | 필수 | 피드 내에서 고유한 패키지 식별자입니다. 이 값은 manifest.json 파일 프로젝트의 "name" 값과 일치 해야 합니다.  참조 [고유한 패키지 식별자 선택](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number) 지침에 대 한 합니다. |
| title | 피드 Windows Admin Center 게시 하는 데 필요한 | Windows Admin Center 확장 관리자에 표시 되는 패키지에 대 한 이름입니다. |
| version | 필수 | 확장 버전입니다. 사용 하 여 [유의 적 버전 (SemVer 규칙)](http://semver.org/spec/v1.0.0.html) 를 권장 하지만 필요 하지 않습니다. |
| 작성자 | 필수 | 회사를 대신 하 여 게시 하는 경우에 회사 이름을 사용 합니다. |
| description | 필수 | 확장의 기능에 대 한 설명을 제공 합니다. |
| iconUrl | 피드 Windows Admin Center 게시할 때이 좋습니다. | 확장 관리자에 표시할 아이콘에 대 한 URL입니다. |
| projectUrl | 피드 Windows Admin Center 게시 하는 데 필요한 | 확장 프로그램의 웹 사이트 URL입니다. 별도 웹 사이트에 있지 않은 경우에 NuGet 피드에 패키지 웹 페이지에 대 한 URL을 사용 합니다. |
| licenseUrl | 피드 Windows Admin Center 게시 하는 데 필요한 | 확장 프로그램의 최종 사용자 사용권 계약에 대 한 URL입니다. |
| 파일 | 필수 | 이러한 두 설정이 Windows Admin Center UI 확장 및 게이트웨이 플러그 인에 대해 필요로 하는 폴더 구조를 설정 합니다. |

### <a name="3-build-the-extension-nuget-package"></a>3. 빌드 확장 NuGet 패키지

위에서 만든.nuspec 파일을 사용 하 여, 이제 만듭니다 NuGet 패키지.nupkg 파일을 업로드 하 고 NuGet 피드에 게시할 수 있습니다.

1. Nuget.exe CLI 도구를 다운로드 합니다 [NuGet 클라이언트 도구 웹 사이트](https://docs.microsoft.com/nuget/install-nuget-client-tools)합니다.
2. .Nupkg 파일을 만들려면 "nuget.exe 팩 [.nuspec 파일 이름]"를 실행 합니다.

### <a name="4-signing-your-extension-nuget-package"></a>4. 확장 NuGet 패키지 서명

확장 프로그램에 포함 된 모든.dll 파일은 신뢰할 수 있는 인증 기관 (CA)에서 인증서로 서명 되어야 합니다. 기본적으로 Windows Admin Center 프로덕션 모드에서 실행 중인 경우 실행 되 고 부호 없는.dll 파일을 차단 됩니다.

또한 좋습니다는 패키지의 무결성을 보장 하려면 확장 NuGet 패키지를 서명 하지만 필수 단계가 아닙니다.

### <a name="5-test-your-extension-nuget-package"></a>5. 확장 NuGet 패키지를 테스트 합니다.

확장 패키지를 테스트할 준비가 완료 되었습니다! NuGet 피드에.nupkg 파일을 업로드 하거나 파일 공유에 복사 합니다. 를 보고 하려면 다른 피드 또는 파일 공유에서 패키지를 다운로드 해야 [피드 구성을 변경](../configure/using-extensions.md#installing-extensions-from-a-different-feed) 파일 공유 또는 NuGet 피드를 가리킵니다. 를 테스트할 때에 속성이 올바르게 확장 관리자에 표시 됩니다 및 성공적으로 설치 하 고 확장 프로그램을 제거할 수 있는지 확인 합니다.

## <a name="publishing-your-extension-to-the-windows-admin-center-feed"></a>피드 Windows Admin Center 확장 게시

피드 Windows Admin Center 게시 하 여 할 수 있습니다 확장 사용 가능한 모든 Windows Admin Center 사용자. Windows Admin Center SDK 미리 보기 상태에서 이므로 개발 문제를 해결, 고품질 제품을 배달할 수 있는지 확인 하 고 사용자에 게 발생 하는 데 사용자와 긴밀 하 게 협력 하고자 합니다.

확장 프로그램의 초기 버전 릴리스해야 하는 확장 프로그램 검토 요청을 제출 하면 Microsoft 적어도 2 ~ 3 주 충분 한 시간을 검토할 수 있도록 하는 릴리스 전에 및 필요한 경우 확장 프로그램을 변경 하는 것이 좋습니다. 확장 게시 될 준비가 되 면 검토를 위해 우리에 게 보내도록 해야 및 승인 되 면를 피드에 게시 됩니다 것입니다.

그런 다음 확장 프로그램에 대 한 업데이트를 해제 하려는 경우에 검토에 대 한 다른 요청을 제출 해야 합니다. 변경의 범위에 따라 업데이트 검토의 소요 시간이 짧은 이어야 일반적으로 합니다.

### <a name="submit-an-extension-review-request-to-microsoft"></a>Microsoft 확장 검토 요청을 제출

확장 프로그램 검토 요청을 제출 하려면 다음 정보를 입력 하 고 전자 메일을 파일로 보냅니다 [ wacextensionrequest@microsoft.com ](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request)합니다. 에서는 1 주일 내 전자 메일에 회신 합니다.

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### <a name="submit-your-extension-package-for-review-and-publishing"></a>검토 및 게시에 대 한 확장 패키지를 제출 합니다.

위의 지침을 따라야 [확장 패키지를 만드는](#creating-an-extension-package) .nuspec 파일은 제대로 정의 및 파일은 서명 됩니다. 또한 다음을 포함 하는 프로젝트 웹 사이트 있다고 것이 좋습니다.

- 자세한 설명은 스크린샷 또는 비디오를 포함 하 여 확장
- 의견이 나 질문을 수신 하도록 전자 메일 주소 또는 웹 사이트 기능

확장 프로그램을 게시할 준비가 되었을 때 전자 메일을 보내 [ wacextensionrequest@microsoft.com ](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review) 및 확장 패키지를 보내 하는 방법에 지침을 제공 합니다. 패키지에 수신 되 면 검토 하 고 승인 되 면 피드 Windows Admin Center 게시 합니다.