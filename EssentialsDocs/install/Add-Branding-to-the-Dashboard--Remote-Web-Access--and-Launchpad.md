---
title: 대시보드, 원격 웹 액세스 및 실행 패드에 브랜딩 추가
description: 대시보드, 원격 웹 액세스 및 실행 패드 화면에 브랜딩 자료를 추가 하는 방법입니다.
ms.date: 04/10/2014
ms.prod: windows-server
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 056c7264fc90adbf115c3c6587081a449240a98a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471088"
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>대시보드, 원격 웹 액세스 및 실행 패드에 브랜딩 추가

> 적용 대상: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

레지스트리에서 항목을 추가하여 여러 브랜딩을 추가할 수 있습니다. 운영 체제에 대 한 레지스트리의 모든 브랜딩 항목은 아래에 있습니다 `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM` .

공동 브랜딩 용도에 맞게 Windows Server Essentials 로고의 최소 너비는 **170 픽셀**이어야 하며 올바른 가로 세로 비율을 **96 DPI**로 유지 해야 합니다.

## <a name="to-add-branding-by-changing-the-registry"></a>레지스트리를 변경하여 브랜딩을 추가하려면

1. 서버에서 마우스를 화면 오른쪽 상단 구석으로 옮긴 후 **검색**을 클릭합니다.

2. 검색 상자에 **regedit**를 입력하고 **Regedit** 애플리케이션을 클릭합니다.

3. 탐색 창에서 **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft**, **Windows Server**를 차례로 확장합니다. **OEM** 키가 없는 경우 만들 수 있습니다.

    1. **Windows Server**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**를 클릭한 다음 **키**를 클릭합니다.

    2. 키 이름에 **OEM**을 입력합니다.

4. 필드 로고에 대 한 항목을 만드는 경우 다른 키를 만들어 로고의 언어 버전을 구분할 수 있습니다. 예를 들어 로고의 영어 버전과 독일어 버전을 모두 보유한 경우 en-us 키와 de-de 키를 만들 수 있습니다. 로고 파일은 모두 동일한 폴더에 저장되므로 각 언어별로 고유한 이름을 사용하여 로고 이미지 파일의 인스턴스를 제공해야 합니다. 예를 들어 DashboardLogo_en.png 및 DashboardLogo_de.png라는 파일을 만듭니다.

5. **OEM** 을 마우스 오른쪽 단추로 클릭 하거나 적절 한 언어 키를 마우스 오른쪽 단추로 클릭 하 고 **새로 만들기**를 클릭 한 다음 **문자열 값**을 클릭 합니다.

6. 문자열의 이름을 입력한 다음 Enter 키를 누릅니다. 문자열 이름 및 데이터 값에 대 한 자세한 내용은이 문서의 **레지스트리 문자열 및 값** 섹션을 참조 하십시오.

7. 문자열의 이름을 입력한 다음 Enter 키를 누릅니다. 문자열 이름 및 데이터 값에 대 한 자세한 내용은이 문서의 **레지스트리 문자열 및 값** 섹션을 참조 하십시오.

8. 새 문자열을 마우스 오른쪽 단추로 클릭한 다음 **수정**을 클릭합니다.

9. 문자열 이름과 연결된 테이블에서 값을 입력한 다음 **확인**을 클릭합니다.

10. 로고 이미지 또는 추가 된 링크에 대 한 항목을 만드는 경우 파일을에 복사 `%programFiles%\Windows Server\Bin\OEM` 합니다. OEM 디렉터리가 없으면 새로 만듭니다.

11. 고객이 서버를 소유한 후 원격 웹 액세스를 변경 하는 경우 다음과 같은 방법으로 원격 웹 액세스를 켜야 합니다.

    1. 대시보드에서 **설정**을 클릭한 다음 **원격 액세스** 탭을 클릭합니다.

    2. 원격 **액세스를** 설정 하는 경우 원격 액세스 **설정** 마법사의 **사용할 원격 액세스 기능 선택** 페이지에서 **구성**을 클릭 하 고 원격 웹 액세스 확인란의 선택을 취소 합니다.

    3. **구성**을 클릭합니다.

### <a name="registry-strings-and-values"></a>레지스트리 문자열 및 값

다음 표에서는 사용 가능한 문자열 이름 및 데이터 값에 대 한 정보를 제공 합니다.

| 브랜딩 위치 | 설명 | 문자열 이름 | 데이터 값 |
|--|--|--|--|
| 대시보드 로고 | 대시보드에 로고 이미지를 추가합니다. 대시보드 로고 형식은 .png여야 하며, 로고 크기는 350 x 38 픽셀 이하여야 합니다.<p>**중요:** 로고를 사용 하 여 대시보드를 공동 브랜드 하려면 OPK DVD에 제공 된 아트 워크 타일을 편집 하 고 적절 한 공백 요구 사항을 준수 하는 동안 이미지에 회사 로고를 추가 해야 합니다. | DashboardLogo | 로고 이미지 파일의 이름을 입력 합니다. |
| DashboardClientLogo | 대시보드 클라이언트 로그인 화면에 로고 이미지를 추가 합니다. | DashboardClientLogo | 로고 이미지 파일의 이름을 입력 합니다. |
| 웹 사이트 배경 그림 | 원격 웹 액세스 로그인 페이지에 표시 되는 배경 이미지를 변경 합니다. 일반적인 해상도는 다음과 같이 나타납니다.<ul><li>**1024x768 픽셀** -이 해상도는 로그인 페이지를 정확 하 게 채웁니다.</li><li>**800x600 픽셀** -이 해상도는 페이지에서 이미지를 가운데에 배치 하 고 검은색 테두리가 표시 됩니다.</li><li>**1280x720 픽셀** -이 해상도는 이미지를 가운데에 맞춥니다. 1024x720를 초과 하는 픽셀은 표시 되지 않습니다. | LogonBackground | 배경 이미지 파일의 이름을 입력 합니다. |
| 웹 사이트 제목 | 원격 웹 액세스 사이트의 제목을 Windows Server Essentials에서 지정 된 제목으로 바꿉니다. | WebsiteName | 새 원격 웹 액세스 사이트 제목을 입력 합니다. |
| 웹 사이트 로고 | 원격 웹 액세스 사이트의 기본 로고를 변경합니다. 로고의 예상 크기는 32 x 32 픽셀입니다. 로고가이 크기 보다 작거나 크면 이러한 크기와 일치 하도록 늘어나거나 줄어듭니다. | WebsiteLogo | 로고 이미지 파일의 이름 입력 |
| 첨부한 웹 사이트 로고 | 파트너 로고가 원격 웹 액세스 사이트에 표시 되는 Microsoft 로고 바로 아래에 표시 됩니다. 로고의 예상 크기는 200 x 50 픽셀입니다. 로고가 이 크기보다 큰 경우에는 원래 가로 세로 비율을 유지하면서 크기에 맞게 줄입니다. 로고가 이 크기보다 작은 경우에는 200 x 50 픽셀 영역 내에서 중심에 위치하며 크기나 가로 세로 비율 모두 변경되지 않습니다. | OEMLogo | 로고 이미지 파일의 이름을 입력 합니다. |
| 웹 사이트 홈 페이지 및 로그인 페이지의 링크 | 원격 웹 액세스 사이트의 로그인 페이지 및 홈 페이지에 대 한 링크를 추가 합니다. 링크 정보를 포함 하는 XML 파일은 폴더에 위치 해야 합니다 `%programFiles%\Windows Server\Bin\OEM` . | LinksXML | 요소 및 설명 목록은 LinksXML 요소 표를 참조하세요. |
| 실행 패드 로고 | 실행 패드에 로고 이미지를 추가합니다. 실행 패드 로고는 .png 형식이어야 하며 64픽셀을 넘지 않아야 합니다. | LaunchpadLogo | 로고 이미지 파일의 이름을 입력 합니다. |

#### <a name="xml-linking-format"></a>XML 링크 형식

웹 사이트 **홈** 페이지와 로그인 페이지에서 링크의 서식을 다음과 같이 지정 해야 합니다.

```xml
<OemLinks>
    <LogonLinks>
        <Link Name=LogonLinkName>
        <Text>LogonLinkDescription</Text>
        <Url>LogonLinkURL</Url>
        <Icon>LinkIcon</Icon>
        </Link>
    </LogonLinks>

    <HomepageLinks>
        <Link Name=HomepageLinkName>
        <Text>HomepageLinkDescription</Text>
        <Url>HomepageLinkURL</Url>
        <Icon>HomepageLinkIcon</Icon>
        </Link>
    </HomepageLinks>
</OemLinks>
```

### <a name="linksxml-elements"></a>LinksXML 요소

| LinksXML 요소 | 설명 |
|--|--|
| LogonLinks | 로그인 링크에 대 한 부모 항목입니다. |
| 링크 이름 | 로그인 링크 이름입니다. |
| 텍스트 | 로그인 페이지 링크로 표시 되는 텍스트입니다. |
| URL | 로그인 페이지 링크로 확인 되는 URL입니다. |
| 아이콘 | 로그인 링크에 대 한 아이콘 파일의 이름입니다. 이 파일은 .xml 파일과 동일한 폴더 위치에 있어야 합니다. 아이콘 이미지는 16x16 픽셀 및 .png 형식 이어야 합니다. 아이콘을 제공 하지 않으면 기본 링크 아이콘 이미지가 사용 됩니다. |
| HomepageLinks | **홈** 페이지의 부모 항목입니다. |
| 링크 이름 | **홈** 페이지 링크 이름입니다. |
| 텍스트 | **홈** 페이지 링크로 표시 되는 텍스트입니다. |
| URL | **홈** 페이지 링크로 확인 되는 URL입니다. |
| 아이콘 | **홈** 페이지 링크에 대 한 아이콘 파일의 이름입니다. 이 파일은 .xml 파일과 동일한 폴더 위치에 있어야 합니다. 아이콘 이미지는 16x16 픽셀 및 .png 형식 이어야 합니다. 아이콘을 제공 하지 않으면 기본 **홈** 페이지 링크 아이콘 이미지가 사용 됩니다. |

## <a name="additional-references"></a>추가 참조

- [이미지 만들기 및 사용자 지정](Creating-and-Customizing-the-Image.md)

- [추가 사용자 지정](Additional-Customizations.md)

- [배포용 이미지 준비](Preparing-the-Image-for-Deployment.md)

- [사용자 환경 테스트](Testing-the-Customer-Experience.md)