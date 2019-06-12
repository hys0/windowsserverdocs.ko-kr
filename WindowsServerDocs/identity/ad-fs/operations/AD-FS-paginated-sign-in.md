---
title: AD FS 로그인 페이지를 매긴
description: 이 문서에서는 AD FS 2019에 대 한 새 로그인 환경을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c528b9c4e944849b7ed9a2fc5213a7b263be70c7
ms.sourcegitcommit: ccc802338b163abdad2e53b55f39addcfea04603
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66687382"
---
# <a name="ad-fs-paginated-sign-in"></a>AD FS 로그인 페이지를 매긴


Windows Server 2019에 AD FS에 대 한 로그인 UI를 새롭게 디자인 했습니다.  이제 AD FS 로그인 해야 Azure AD의 동일한 모양과 느낌입니다.  사용자가 더 일관 된 로그인 환경을 통합 가운데 맞춤 및 페이지가 매겨진 사용자 흐름을 제공 합니다.

## <a name="whats-changing"></a>무엇이 변경
Windows Server 2012 R2 및 2016에서 AD FS에서 로그인 화면은 코드는 다음과 같았습니다.

![oldsignin](media/AD-FS-paginated-sign-in/signin1.png)

화면 오른쪽에 있는 단일 폼을 표시에서 이동 합니다.

Windows Server 2019에 AD FS에서 이러한은 볼 수 있는 주요 디자인 변경 내용:


- **UI 중심**합니다. 이전에 위에 표시 된 대로 로그인 UI 화면 오른쪽에 존재 합니다. UI 프런트 엔드 및 센터 환경을 현대화를 안내 합니다.
- **페이지 매김**합니다. 긴 입력 양식을 제공 하는 대신는 로그인 환경을 통해 단계별 안내는 새 흐름을 통합 한 것입니다. 원격 분석이이 방법을 사용 하 여 고객 갖고 더 성공적인 로그인을 표시 합니다. 또한 제공 우리와 같은 다양 한 인증 방법을 authentication 전화를 통합 하는 데 더 많은 유연성.

![newsignin](media/AD-FS-paginated-sign-in/signin2.png)

첫 번째 페이지에서 사용자 이름을 입력 하 라는 나타납니다. "로그인 유지" 하는 옵션을 선택할 수 있습니다 로그인 프롬프트의 빈도 줄이고 안전 상태일 때 로그인 상태를 유지 합니다. (이 옵션이 기본적으로 비활성화 됩니다.)

![newsignin](media/AD-FS-paginated-sign-in/signin3.png)

두 번째 페이지에서 관리자가 구성한 인증 옵션을 사용 하 여 표시 될 수 있습니다. 기본 외부 인증 수 있도록 설정 된 경우이 포함 됩니다도 합니다.

![newsignin](media/AD-FS-paginated-sign-in/signin4.png)

세 번째 페이지에서 ("암호"를 선택 하는 인증 옵션으로 가정) 암호를 입력 하 라는 메시지가 표시 됩니다.

## <a name="how-to-get-the-new-experience"></a>새 환경을 하는 방법

### <a name="new-installation-of-ad-fs"></a>AD FS의 새 설치
AD FS에 새 고객 인 경우에 기본적으로 새 디자인을 받게 됩니다.

### <a name="upgrading-a-farm"></a>팜을 업그레이드
기존 고객 AD FS 2012 R2 또는 2016 인 경우에 AD FS 2019에 서버를 업그레이드 하 고 2019에 FBL 사용 후 새 디자인을 받으려면 두 가지가 있습니다.

- Powershell을 통해 새 로그인을 허용 합니다. 페이지 매김을 사용 하도록 설정 하려면 다음 명령을 실행 합니다. ``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - Powershell을 통해 또는 AD FS 서버 관리자를 통해 기본으로 외부 인증을 사용 하도록 설정 합니다. 이 기능을 사용 하는 경우 새 페이지 매긴된 로그인 페이지 설정 됩니다.
AD FS에 새 고객 인 경우에 기본적으로 새 디자인을 받게 됩니다. 그러나 AD FS 2012 r 2를 사용 하 여 기존 고객 또는 2016 인 경우 일부의 단계가 있습니다 새 디자인을 수신 하는 데 필요 합니다. ``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>사용자 지정
AD FS 2019에 대 한 사용자 지정에 대 한 옵션이 적용 합니다.
참조에 대 한 다른 문서에 대 한 일부 링크는 다음과 같습니다.

사용자에 게 해당 서버를 AD FS 2019 업그레이드 계획이 없지만 여전히 새 디자인을 원하는 •: [Active Directory Federation Services에서 Azure AD UX 웹 테마를 사용 하 여](azure-ux-web-theme-in-ad-fs.md)

• 사용자 지정을 위한 중앙 위치: [AD FS 사용자 로그인 사용자 지정](ad-fs-user-sign-in-customization.md)
