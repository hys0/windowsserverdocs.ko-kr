---
title: AD FS의 Azure AD UX 웹 테마
description: 다음 문서에서는 Azure AD 사용자 환경과 비슷하게 AD FS 양식 로그인을 변경 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f4dd1d45646475be3788cd6b615b1743976eedae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358407"
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Active Directory Federation Services에서 Azure AD UX 웹 테마 사용
AD FS forms 로그인은 현재 Azure/O365 로그인 환경을 반영 하지 않습니다.  최종 사용자에 게 보다 균일 하 고 원활한 환경을 제공 하기 위해 AD FS 서버에 적용할 수 있는 css 스타일 시트 팔 로우 웹 테마를 출시 했습니다.  현재 Windows Server 2016의 AD FS에 대 한 양식 로그인은 다음과 같습니다.

![현재 로그인](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


새 스타일 시트를 사용 하 여 사용자 환경은 Azure 및 Office 365 로그인 환경과 유사 하 게 보입니다.

## <a name="download-the-css-style-sheet"></a>CSS 스타일 시트 다운로드
다음 Github [위치](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi)에서 웹 테마를 다운로드할 수 있습니다.


## <a name="enabling-the-new-web-theme"></a>새 웹 테마 사용
새 웹 테마를 사용 하도록 설정 하려면 다음 절차를 수행 합니다.

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>AD FS에서 새 Azure AD UX 웹 테마를 사용 하도록 설정 하려면
1. 관리자 권한으로 PowerShell 시작
2. PowerShell을 사용 하 여 새 웹 테마 만들기: `New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3. Powershell: `Set-AdfsWebConfig -ActiveThemeName custom`
   ![PowerShell을 사용 하 여 새 테마를 활성 테마로 설정](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4. Https://<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm ![Sign-on으로 이동 하 여 로그인을 테스트](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

> ! 두고 Idpinitiatedsignon.aspx가 사용 하도록 설정 되었는지 확인 해야 합니다.  기본적으로 사용 하도록 설정 되어 있지 않습니다.  Idpinitiatedsignon.aspx를 사용 하도록 설정 하려면 다음 PowerShell 명령을 사용 합니다. `Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>이미지 권장 사항
가운데 표시 된 UI를 사용 하도록 설정 하면 동일한 이미지를 배경 및 로고에 사용할 수 있습니다 .이 이미지는 이미 회사 브랜딩을 Azure Active Directory 수 있습니다. 일반적으로 크기, 비율 및 형식에 대 한 동일한 권장 사항이 적용 됩니다.

### <a name="logo"></a>로고

설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
로고는 로그인 패널의 맨 위에 표시 됩니다. | 투명 JPG 또는 PNG<br>최대 높이: 36 px<br>최대 너비: 245 px | 여기에서 조직의 로고를 사용 합니다.<br>투명 이미지를 사용 합니다. 배경이 흰색이 된다고 가정 하지 마십시오.<br>이미지에서 로고 주위에 안쪽 여백을 추가 하지 마십시오. 그렇지 않으면 로고가 불균형 하 게 작게 보입니다.

### <a name="background"></a>배경

설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
이 옵션은 로그인 페이지의 배경에 표시 되며 볼 수 있는 공간의 가운데에 고정 되 고 브라우저 창에 맞도록 크기 조정 하 고 자릅니다.    <br>휴대폰과 같은 좁은 화면에서이 이미지는 표시 되지 않습니다.<br>페이지가 로드 될 때이 이미지에 0.55 불투명도가 적용 된 검은색 마스크가 적용 됩니다. | JPG 또는 PNG<br>이미지 크기: 1920 x 1080 px<br>파일 크기: &lt; 300 | <br>강력한 주제 포커스가 없는 이미지를 사용 합니다. 불투명 로그인 양식이이 이미지의 가운데 위에 나타나고 브라우저 창의 크기에 따라 이미지의 모든 부분을 처리할 수 있습니다.<br>빠른 로드 시간을 보장 하려면 파일 크기를 작게 유지 합니다.

## <a name="next-steps"></a>다음 단계
- [Windows Server 2016에서 사용자 지정 AD FS](AD-FS-Customization-in-Windows-Server-2016.md)
- [고급 사용자 지정](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [사용자 지정 웹 테마](Custom-Web-Themes-in-AD-FS.md)
