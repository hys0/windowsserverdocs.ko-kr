---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: 홈 영역 검색 사용자 지정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5a151e46e566d9f5459419771cbd476bb26c248d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357957"
---
# <a name="home-realm-discovery-customization"></a>홈 영역 검색 사용자 지정


먼저 AD FS 클라이언트는 리소스를 요청할 때 리소스 페더레이션 서버는 클라이언트의 영역에 대 한 정보가 없습니다. 리소스 페더레이션 서버에서 사용 하 여 AD FS 클라이언트에 응답 한 **클라이언트 영역 검색** 페이지에서 사용자 목록에서 홈 영역을 선택 합니다. 목록 값은 클레임 공급자 트러스트의 표시 이름 속성에서 채워집니다. 다음 Windows PowerShell cmdlet을 사용 하 여 수정 하 고 AD FS 홈 영역 검색 환경을 사용자 지정 합니다.  
  
![홈 영역](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> 로컬 Active Directory에 대해 표시되는 클레임 공급자 이름은 페더레이션 서비스 표시 이름입니다.  
  



## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>특정 메일 접미사를 사용하도록 ID 공급자 구성  
조직에서는 여러 클레임 공급자와 페더레이션할 수 있습니다. 이제는 관리자가 no__t-0box 기능을 제공 하 여 클레임 공급자가 지 원하는 접미사 (예: @us.contoso.com, @eu.contoso.com)를 나열 하 고이를 접미사 @ no__t 기반 검색에 사용할 수 있도록 합니다. AD FS 이 구성을 사용 하 여 최종 사용자가 자신의 조직 계정을 입력할 수 및 AD FS는 해당 클레임 공급자를 자동으로 선택 합니다.  
  
Id 공급자를 구성 하려면 \(IDP\), 와 같은 `fabrikam`, 을 특정 전자 메일 접미사를 사용 하 여 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
>[!NOTE]
> 두 AD FS 서버 간에 페더레이션 하는 경우 클레임 공급자 트러스트에 대 한 PromptLoginFederation 속성을 ForwardPromptAndHintsOverWsFederation로 설정 합니다.  이는 AD FS에서 login_hint 및 프롬프트 매개 변수를 IDP로 전달 하는 것입니다.  다음 PowerShell cmdlet을 실행 하 여이 작업을 수행할 수 있습니다.
>
>`Set-AdfsclaimsProviderTrust -PromptLoginFederation ForwardPromptAndHintsOverWsFederation`

## <a name="configure-an-identity-provider-list-per-relying-party"></a>신뢰 당사자별 ID 공급자 목록 구성  
일부 시나리오에서는 조직에서 클레임 공급자의 하위 집합만 홈 영역 검색 페이지에 표시하여 최종 사용자가 응용 프로그램에 특정한 클레임 공급자만 볼 수 있도록 구성하기를 원할 수 있습니다.  
  
신뢰 별 IDP 목록을 구성 하려면 파티 \(RP\), 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  
 
`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") ` 

  
## <a name="bypass-home-realm-discovery-for-the-intranet"></a>인트라넷에 대한 홈 영역 검색 무시  
대부분의 조직에서는 해당 방화벽 내에서 액세스하는 사용자에 대해서만 로컬 Active Directory를 지원합니다. 이러한 경우 관리자는 인트라넷에 대 한 홈 영역 검색 무시 하도록 AD FS를 구성할 수 있습니다.  
  
인트라넷에 대 한 HRD를 무시 하려면 다음 Windows PowerShell cmdlet 및 구문을 사용 합니다.  
  

`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true ` 
 
  
> [!IMPORTANT]  
> 참고는 신뢰 당사자에 대 한 id 공급자 목록 구성 된 경우 경우에는 이전 설정이 사용 되 고 AD FS 홈 영역 검색을 계속 표시의 인트라넷에서 사용자가 액세스 \(HRD\) 페이지입니다. 이 경우 HRD를 무시하려면 이 신뢰 당사자에 대한 IDP 목록에 "Active Directory"도 추가해야 합니다.  

## <a name="additional-references"></a>추가 참조 
[사용자 로그인 사용자 지정 AD FS](AD-FS-user-sign-in-customization.md)  
