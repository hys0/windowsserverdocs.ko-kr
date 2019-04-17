---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: "홈 영역 검색 사용자 지정"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 328c313b2d5bf174f6e6af20cd91ac9620edac82
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="home-realm-discovery-customization"></a>홈 영역 검색 사용자 지정

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

먼저 ADFS 클라이언트 리소스를 요청 하면 리소스 federation 서버에 클라이언트의 영역에 대 한 정보가 없습니다. 리소스 federation 서버가 응답 ADFS 클라이언트 사용에 **클라이언트 영역 검색** 페이지에서 사용자 목록에서 홈 영역을 선택 합니다. 목록을 값은 신뢰 클레임 공급자의 디스플레이 name 속성에서 채워집니다. 다음 Windows PowerShell cmdlet를 사용 하 여 수정 하 고 광고 FS Home 영역 검색 환경을 사용자 지정 합니다.  
  
![홈 영역](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> 로컬 Active Directory에 대 한 표시 된 청구 공급자 이름을 federation 서비스 표시 이름 주의 해야 합니다.  
  
## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>특정 메일 접미사 사용 하 여 Id 공급자 구성  
조직 여러 클레임 공급자와 연결 수 있습니다. ADFS 이제 나열 된 접미사 하려면 관리자 in\ 상자 기능을 제공 @us.contoso.com, @eu.contoso.com즉, 청구 공급자가 지원 하 고 suffix\ 기반 검색을 사용 하도록 설정 합니다. 이 구성 최종 사용자가 자신의 조직 계정에 입력할 수 및 ADFS 자동으로 해당 클레임 공급자를 선택 합니다.  
  
Id 공급자 구성 하려면 \(IDP\)와 같은 `fabrikam`, 사용 하 여 특정 메일 접미사 다음 Windows PowerShell cmdlet 및 구문 사용 합니다.  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
  
## <a name="configure-an-identity-provider-list-per-relying-party"></a>의존 당 id 공급자 목록 구성 파티  
일부 시나리오에는 조직 청구 공급자의 일부만 홈 영역 검색 페이지에 표시 되도록 응용 프로그램에 관련 된 청구 공급자 볼 최종 사용자가 좋습니다.  
  
의존 당 IDP 목록 구성 \(RP\) 파티, 다음 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  
 
`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") ` 

  
## <a name="bypass-home-realm-discovery-for-the-intranet"></a>사용 안 함 Home 영역에 대 한 검색 인트라넷  
대부분의 조직 해당 지역 Active Directory 해당 방화벽 내에서 액세스 하는 사용자에 대 한 지원 합니다. 이러한 경우, 관리자 ADFS 홈 영역 검색 인트라넷을 무시 하도록 구성할 수 있습니다.  
  
HRD 인트라넷에 대 한 않으려면 다음과 같은 Windows PowerShell cmdlet와 구문을 사용 합니다.  
  

`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true ` 
 
  
> [!IMPORTANT]  
> 주세요 메모를 하는 경우에 의존 하는 것에 대 한 id 공급자 목록 자 구성 되어, 이전 설정에 사용 하도록 설정한 경우에 및 인트라넷에서 사용자 액세스 ADFS 홈 영역 검색 \(HRD\) 페이지 여전히 표시 됩니다. 이 경우 HRD 사용이 당사자에 대 한 "Active Directory" IDP 목록에 추가가 있는지 확인 해야 합니다.  

## <a name="additional-references"></a>추가 참조 
[광고 FS 사용자 지정 로그인](AD-FS-user-sign-in-customization.md)  
