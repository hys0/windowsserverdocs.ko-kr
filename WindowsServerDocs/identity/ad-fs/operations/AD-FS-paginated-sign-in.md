---
title: 페이지를 매긴 로그인 AD FS
description: 이 문서에서는 AD FS 2019에 대 한 새로운 로그인 환경을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 09/19/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ca13ebe29b0a9260302599110f333d166681abdb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358561"
---
# <a name="ad-fs-paginated-sign-in"></a>페이지를 매긴 로그인 AD FS


Windows Server 2019에 AD FS 로그인 UI를 다시 디자인 했습니다.  이제 AD FS 로그인은 Azure AD의 모양과 느낌을 갖습니다.  이를 통해 사용자는 중앙에 있고 페이지가 매겨진 사용자 흐름을 통합 하 여 보다 일관 된 로그인 환경을 제공할 수 있습니다.

## <a name="whats-changing"></a>변경 내용
Windows Server 2012 R2 및 2016의 AD FS 로그인 화면이 다음과 같이 보입니다.

![oldsignin](media/AD-FS-paginated-sign-in/signin1.png)

화면 오른쪽에 있는 단일 폼을 표시 하지 않습니다.

Windows Server 2019의 AD FS에는 다음과 같은 주요 디자인 변경 내용이 표시 됩니다.


- **가운데에 맞춘 UI**입니다. 이전에는 위에 표시 된 것 처럼 화면 오른쪽에 로그인 UI가 있었습니다. UI front 및 center를 이동 하 여 환경을 현대화 했습니다.
- **페이지 매김**. 입력 하는 긴 형식을 제공 하는 대신, 로그인 환경을 단계별로 안내 하는 새로운 흐름이 통합 되었습니다. 이 접근 방식을 사용 하면 고객의 로그인이 성공적으로 완료 된 것을 볼 수 있습니다. 또한 미국 전화 팩터 인증과 같은 다양 한 인증 방법을 통합 하는 데 더 많은 유연성을 제공 합니다.

![newsignin](media/AD-FS-paginated-sign-in/signin2.png)

첫 번째 페이지에서 사용자 이름을 입력 하 라는 메시지가 표시 됩니다. 로그인 프롬프트의 빈도를 줄이고 안전 하 게 로그인 된 상태를 유지 하기 위해 "로그인 유지" 옵션을 선택할 수도 있습니다. 이 옵션은 기본적으로 사용 하지 않도록 설정 되어 있습니다.

![newsignin](media/AD-FS-paginated-sign-in/signin3.png)

두 번째 페이지에서 관리자에 의해 구성 된 인증 옵션이 표시 됩니다. 외부 인증을 주 복제본으로 허용 하는 경우에도 포함 됩니다.

![newsignin](media/AD-FS-paginated-sign-in/signin4.png)

세 번째 페이지에서 암호를 입력 하 라는 메시지가 표시 됩니다 (인증 옵션으로 "암호"를 선택 했다고 가정).

## <a name="how-to-get-the-new-experience"></a>새 환경을 얻는 방법

### <a name="new-installation-of-ad-fs"></a>AD FS 새로 설치
새 고객이 AD FS 하는 경우 기본적으로 새로운 디자인을 받게 됩니다.

### <a name="upgrading-a-farm"></a>팜 업그레이드
기존 고객 AD FS 2012 R2 또는 2016 인 경우 서버를 AD FS 2019로 업그레이드 한 후 새 설계를 수신 하 고 FBL를 2019로 설정 하는 두 가지 방법이 있습니다.

- Powershell을 통해 새 로그인을 허용 합니다. 페이지 매김을 사용 하려면 다음 명령을 실행 합니다.``Set-AdfsGlobalAuthenticationPolicy -EnablePaginatedAuthenticationPages $true``

 - Powershell 또는 AD FS 서버 관리자를 통해 기본으로 외부 인증을 사용 하도록 설정 합니다. 이 기능을 사용 하도록 설정 하면 페이지가 매겨진 새 로그인 페이지가 활성화 됩니다.
새 고객이 AD FS 하는 경우 기본적으로 새로운 디자인을 받게 됩니다. 그러나 AD FS 2012 R2 또는 2016를 사용 하는 기존 고객의 경우 새 설계를 수신 하기 위해 수행 해야 하는 몇 가지 단계가 있습니다.``Set-AdfsGlobalAuthenticationPolicy -AllowAdditionalAuthenticationAsPrimary $true``

## <a name="customization"></a>사용자 지정
사용자 지정 옵션은 AD FS 2019에도 적용 됩니다.
다음은 참조용으로 다른 문서에 대 한 링크입니다.

• 서버를 AD FS 2019로 업그레이드할 계획이 없지만 새 디자인을 원하는 경우: [Active Directory Federation Services에서 Azure AD UX 웹 테마 사용](azure-ux-web-theme-in-ad-fs.md)

• 사용자 지정할 중앙 위치: [AD FS 사용자 로그인 사용자 지정](ad-fs-user-sign-in-customization.md)
