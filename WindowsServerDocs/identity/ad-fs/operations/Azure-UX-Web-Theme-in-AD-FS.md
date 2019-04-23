---
title: AD FS에서 azure AD UX 웹 테마
description: 다음 문서에는 Azure AD 사용자 환경 비슷하도록 AD FS 폼 로그인 변경 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8d6afd7829c92382815e95b8c43a054b000359e2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887884"
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Active Directory Federation Services에서 Azure AD UX 웹 테마를 사용 하 여
AD FS 로그인 폼에서 현재 미러링 하지 Azure/O365 로그인 환경입니다.  최종 사용자를 더 균일 하 고 원활한 환경을 제공 하려면 다음 연계 스타일 시트 웹 테마를 AD FS 서버에 적용할 수 있는 릴리스 했습니다.  현재 폼 로그인에 다음 형태의 Windows Server 2016에서 AD FS에 대 한 합니다.

![현재 로그인](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


새 스타일 시트를 사용 하 여 사용자 환경을 더 가깝습니다 Azure 및 Office 365 로그인 환경을 살펴보겠습니다.

## <a name="download-the-css-style-sheet"></a>CSS 스타일 시트를 다운로드 합니다.
다음 Github에서 웹 테마를 다운로드할 수 있습니다 [위치](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi)합니다.


## <a name="enabling-the-new-web-theme"></a>새 웹 테마를 사용 하도록 설정
새 웹 테마를 사용 하도록 설정 하려면 다음 절차를 따르십시오.

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>AD FS에서 새 Azure AD UX 웹 테마를 사용 하도록 설정 하려면
1.  관리자 권한으로 PowerShell을 시작 합니다.
2.  PowerShell을 사용 하 여 새 웹 테마를 만듭니다.  `New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3.  PowerShell을 사용 하 여 활성 테마도 새 테마를 설정 합니다.  `Set-AdfsWebConfig -ActiveThemeName custom`
![PowerShell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4.  Https://로 이동 하 여 로그인을 테스트<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm ![로그온](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

> ! [참고] 해당 idpinitiatedsignon를 사용 하도록 설정 되었는지 확인 해야 합니다.  기본적으로 사용 되지 않습니다.  Idpinitiatedsignon 사용 하도록 설정 하려면 다음 PowerShell 명령을 사용 하 여:  `Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>권장 사항 이미지
가운데 맞춤된 UI를 사용 하도록 설정 하면 배경 및 로고 했던 이미 Azure Active Directory 회사 브랜딩에 대 한 동일한 이미지를 사용 하 여 할 수 있습니다. 일반적으로 크기, 비율 및 형식에 대 한 권장 사항이 적용지 않습니다.

### <a name="logo"></a>로고
설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
로고는 로그인 패널 맨 위에 표시 됩니다. | 투명 JPG 또는 PNG<br>최대 높이: 36 px<br>최대 너비: 245 px | 여기에서 조직의 로고를 사용 합니다.<br>투명 이미지를 사용 합니다. 배경을 흰색 된다고 가정 하지 마십시오.<br>이미지에서 로고 주위에 안쪽 여백을 추가 하지 않거나 로고가 불균형적으로 작게 보입니다.

### <a name="background"></a>배경
설명 | 제약 조건 | 권장 사항
------- | ------- | ----------
이 볼 수 있는 공간을 크기 조정 하 고 브라우저 창에 맞게 자릅니다의 가운데에 고정은 로그인 페이지의 배경에 옵션이 표시 됩니다.    <br>전화와 같은 좁은 화면에서는이 이미지는 표시 되지 않습니다.<br>0.55 불투명도 검은색 마스크는 페이지가 로드 될 때이 이미지 위에 적용 됩니다. | JPG 또는 PNG<br>이미지 크기: 1920x1080px<br>파일 크기: &lt; 300KB | <br>이미지를 사용 하 여 강력한 제목 포커스가 없는 곳입니다. 불투명 로그인 양식이이 이미지의 가운데 위로 표시 되며 브라우저 창의 크기에 따라 이미지의 모든 부분을 덮을 수 있습니다.<br>빠른 로드 시간을 보장 하려면 작은 파일 크기를 유지 합니다.

## <a name="next-steps"></a>다음 단계
- [Windows Server 2016에서에서 AD FS 사용자 지정 합니다.](AD-FS-Customization-in-Windows-Server-2016.md)
- [고급 사용자 지정](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [사용자 지정 웹 테마](Custom-Web-Themes-in-AD-FS.md)
