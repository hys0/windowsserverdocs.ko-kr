---
title: 다단계 인증 및 외부 인증 공급자 사용자 지정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: 23ec5acbe442527b4eb44c4b857e183b5e0c37ea
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865723"
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>다단계 인증 및 외부 인증 공급자 사용자 지정 



AD FS에서 다단계 인증에 대 한 지원으로 제공 됩니다\-의\-는\-상자입니다. 예를 들어 AD FS를 구성할 수 있습니다 사용 하 여 빌드된\-두 번째 단계 인증으로 인증서 인증에서. 또한 외부 인증 공급자를 사용할 수 있습니다. 이 접근 방식을 사용 하면 AD FS를 Azure Multi-factor Authentication과 같은 추가 서비스와 통합 하거나 고유한 공급자를 개발할 수 있습니다. 자세한 [내용은 솔루션 가이드: AD FS를 사용 하\-여 외부](https://technet.microsoft.com/library/dn280937.aspx) 인증 공급자를 등록 하는 방법에 대 한 자세한 내용은 다단계 Access Control를 사용 하 여 위험 관리를 확인 하세요.  
  
외부 인증 공급자는 AD FS 인증 UI를 작성 하는 제공 하는.css 파일에 정의 된 클래스를 사용 하는 것이 좋습니다. 다음 cmdlet을 사용하여 기본 웹 테마를 내보내고 .css 파일에 정의된 사용자 인터페이스 클래스 및 요소를 검사할 수 있습니다. .Css 파일의 기호의 개발에 사용할 수\-외부 인증 공급자의 사용자 인터페이스에서입니다.  
  

    Export-AdfsWebTheme -Name default -DirectoryPath C:\theme  
 
  
다음은 부호의 예로\-사용자 인터페이스에는 빨간색으로 강조 표시, 외부 인증 공급자가 있습니다. AD FS.css 파일의 UI 클래스를 사용 하는 사용자 인터페이스입니다.  
  
![AD FS와 MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)  
  
새 사용자 지정 인증 방법을 작성 하기 전에 콘텐츠 작성 요구 사항을 이해 하려면 AD FS 테마 및 스타일 정의 연구 하는 것이 좋습니다.  
  
-   사용자 지정 인증 방법에만 AD FS 로그인에 HTML 세그먼트만 작성\-페이지 및 전체가 아니라이 페이지에 있습니다. AD FS의 스타일 정의를 사용 하 여 일관성 있는 모양과 동작을 가져와야 합니다.  
  
![AD FS와 MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)  
  
-   AD FS 관리자는 AD FS 스타일을 사용자 지정할 수는 길어집니다. 을 선택합니다. 사용자 고유의 스타일을 하드코드하지 않는 것이 좋습니다. 대신, 가능 하면 AD FS 스타일을 사용 하 여 좋습니다.  
  
-   아웃\-의\-상자에서 AD FS 스타일 왼쪽 한로 제작한\-를\-오른쪽 \(왼쪽에서 오른쪽\) 스타일과 오른쪽 한\-를\-왼쪽 \(RTL\). 관리자가 둘 다는 사용자 지정할 수 있으며 언어를 제공할 수\-웹 테마 정의 통해 특정 스타일입니다. 각 스타일시트에는 개별 설명이 있는 세 개의 섹션이 있습니다.  
  
    -   **테마 스타일** \- 이러한 스타일은 사용할 수 없으며 사용할 수 없습니다. 이러한 스타일은 모든 페이지의 테마를 정의하는 데 사용됩니다. 다시 사용하지 못하도록 의도적으로 요소 ID로 정의되어 있습니다.  
  
    -   **공용 스타일** \- 콘텐츠에 사용 해야 하는 스타일입니다.  
  
    -   **폼 팩터 스타일** \- 이러한 스타일은 다양 한 폼 팩터에 대 한 스타일입니다. 콘텐츠가 휴대폰 및 태블릿과 같은 다양한 폼 팩터에서 작동하려면 이 섹션을 이해해야 합니다.  
  
자세한 내용은 [솔루션 가이드: Multi-factor\-Access Control](https://technet.microsoft.com/library/dn280937.aspx) 및 솔루션가이드를사용하여위험관리:[ 중요 한 응용 프로그램\-](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx)에 대 한 추가 multi-factor Authentication을 사용 하 여 위험을 관리 합니다.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md) 
