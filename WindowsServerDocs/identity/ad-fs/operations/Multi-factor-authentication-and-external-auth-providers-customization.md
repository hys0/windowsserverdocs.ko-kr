---
title: "다중 요소 인증 및 외부 인증이 공급자 사용자 지정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: 6d06c017601003e3b93df32f5fa50190ce54541d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>다중 요소 인증 및 외부 인증이 공급자 사용자 지정 

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Adfs의 다단계 인증에 대 한 지원은 of\ the\ 상자 out\ 제공 됩니다. 예를 들어, 인증서를 사용 하도록 built\에서 두 번째 요소 인증 ADFS 구성할 수 있습니다. 외부 인증이 공급자 사용할 수 있습니다. 이 수를 통해 ADFS Azure 다단계 인증와 같은 추가 서비스를 통합 하 또는 사용자 공급자를 개발할 수 있습니다. 참조 [솔루션 가이드: Multi\ 팩터 액세스 제어 관리 위험](https://technet.microsoft.com/library/dn280937.aspx) Adfs을 사용 하 여 외부 인증이 공급자를 등록 하는 방법에 대 한 자세한 내용은 합니다.  
  
ADFS 작성 인증 UI를 제공 하는.css 파일에 정의 된 클래스 외부 인증이 공급자를 사용 하는 것이 좋습니다. 기본 웹 테마 내보내고와 검사 하 여 사용자 인터페이스 클래스.css 파일에 정의 된 요소 다음 cmdlet을 사용할 수 있습니다. .Css 파일 외부 인증 공급자의 sign\에서 사용자 인터페이스의 개발에 사용할 수 있습니다.  
  

    Export-AdfsWebTheme -Name default -DirectoryPath C:\theme  
 
  
다음은 외부 인증이 공급자가 빨간색를 강조 표시 된 sign\에서 사용자 인터페이스의 예입니다. 사용자 인터페이스 UI 클래스 ADFS.css 파일에 사용 합니다.  
  
![ADFS 및 MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)  
  
새로운 사용자 지정 인증 방법으로 작성 하기 전에 제작 요구 사항 콘텐츠를 이해 하는 ADFS 테마 및 스타일 정의 연구 하는 것이 좋습니다.  
  
-   전체 페이지가 아니라 페이지의 sign\ Adfs에서 된 HTML 분할만 작성자에 사용자 지정 인증 방법을 합니다. Adfs의 스타일 정의 일관 된 모양을 및 동작을 사용 해야 합니다.  
  
![ADFS 및 MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)  
  
-   ADFS 관리자 ADFS 스타일 사용자 지정할 수 있는 주의 해야 합니다. . 권장 되지 않습니다 코딩 원하는 스타일 합니다. 대신 사용 가능할 때마다 ADFS 스타일 좋습니다.  
  
-   Out\ of\ the 상자 ADFS 스타일 한 left\ to\ 오른쪽 \(LTR\) 스타일과 하나 right\ to\ 왼쪽 \(RTL\)로 작성 합니다. 관리자 둘 다를 사용자 지정할 수와 language\ 관련 스타일 웹 테마 정의 통해 제공할 수 있습니다. 각 스타일 시트 해당 설명 된 세 섹션 사항은 다음과 같습니다.  
  
    -   **테마 스타일** \-이러한 스타일 하지 않아야 하 고 사용할 수 없습니다. 이러한 스타일은 모든 페이지에 걸쳐 테마를 정의할 것입니다. 정의 된 요소 ID로 고의로 다시 사용 되지 됩니다.  
  
    -   **일반적인 스타일** \-의 콘텐츠에 대 한 사용 해야 하는 스타일입니다.  
  
    -   **폼 팩터와 스타일** \-다른 폼 요소에 대 한 스타일입니다. 이 섹션 작동 하는지 확인 콘텐츠를 다른 폼 팩터와 예를 들어, 휴대폰 및 태블릿을 이해 해야 합니다.  
  
자세한 내용은 참조 [솔루션 가이드: Multi\ 팩터 액세스 제어 관리 위험](https://technet.microsoft.com/library/dn280937.aspx) 및 [솔루션 가이드: 관리 위험 민감한 응용 프로그램에 대 한 추가 Multi\ 요소 인증 된](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx)합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md) 
