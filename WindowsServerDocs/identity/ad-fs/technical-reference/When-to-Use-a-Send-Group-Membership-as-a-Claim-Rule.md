---
ms.assetid: af16e847-47c2-461e-9df1-cc352a322043
title: "클레임은 일반적으로 보내기 그룹 구성원을 사용 하는 경우"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 10e027b4de463aad2b05eae40a622aebf8f12a3b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="when-to-use-a-send-group-membership-as-a-claim-rule"></a>클레임은 일반적으로 보내기 그룹 구성원을 사용 하는 경우
사용자 지정된 된 Activ 디렉터리 보안 그룹의 회원를 위한 새로운 보내는 클레임 값을 실행 하려는 경우이 규칙 Active Directory Federation Services \(AD FS\)에서 사용할 수 있습니다. 이 규칙을 사용 하는 경우 해당 그룹에 대 한 하나의 클레임 지정 하는 발생 하 고 다음 표에 설명 된 대로 규칙 논리 일치 하는 합니다.  
  
|규칙 옵션|규칙 논리|  
|---------------|--------------|  
|클레임 값 보내는|사용자의 그룹 구성원 같으면는 *지정된 그룹* 같음 발신 클레임 유형 및 *클레임 유형 지정 된*, 다음으로 기존 그룹 이름 값을 교체는 *값 주장 지정 보내는* 및 청구 문제 합니다.|  
  
다음 섹션에서는 주장 규칙에 대 한 기본 소개 합니다. 또한 보내기 그룹 구성원 클레임 일반적으로 사용 하는 경우에 대 한 세부 정보 제공 합니다.  
  
## <a name="about-claim-rules"></a>클레임은 규칙에 대 한  
클레임은 규칙 비즈니스 논리를 수신 클레임, 조건이 적용 됩니다 인스턴스를 나타냅니다 \ (경우 다음 y\ x) 조건에 따라 보내는 클레임은 생성 하 고 있습니다. 다음 목록에 대해 알아야 하는 팁 더 읽기 전에 규칙 주장 중요 한 개요가이 항목에서:  
  
-   Snap\에서 광고 FS 관리에 클레임 규칙 만들 수만 클레임 규칙 템플릿을 사용 하 여  
  
-   클레임 규칙 프로세스 들어오는 주장 클레임 공급자에서 직접 \ (Active Directory Federation Service\ 다른 등) 또는 수용 출력에서 변형 클레임 공급자 보안에 대 한 규칙 합니다.  
  
-   클레임은 규칙 해당된 규칙 설정 내에서 시간 순서로 클레임 발급 엔진에서 처리 됩니다. 규칙의 우선 순위를 설정 하 여 조정 해가면서 하거나 이전 규칙 해당된 규칙 설정 내에서 생성 되는 클레임 필터링 더 있습니다.  
  
-   청구 규칙 템플릿 항상 해야 하는 수신 클레임 종류를 지정할 수 있습니다. 그러나 규칙 하나를 사용 하 여 동일한 클레임 종류 여러 클레임 값을 처리할 수 있습니다.  
  
자세한 청구 규칙 및 청구 규칙 집합에 대 한 정보를 참조 [주장 규칙의 역할은](The-Role-of-Claim-Rules.md)합니다. 규칙은 처리 하는 방법에 대 한 자세한 내용은 참조 [클레임 엔진 The 역할](The-Role-of-the-Claims-Engine.md)합니다. 자세한 내용은 클레임 규칙 집합 처리 하는 방법을 참조 하세요. [클레임 파이프라인 The 역할](The-Role-of-the-Claims-Pipeline.md)합니다.  
  
## <a name="outgoing-claim-value"></a>클레임 값 보내는  
보내기 그룹 구성원을 클레임 규칙 템플릿으로 사용 하는 사용자가 지정 하는 그룹의 회원 있는지 여부에 따라 클레임을 실행할 수 있습니다.  
  
즉, 사용자에 게 그룹 보안 경우에 클레임 한이 규칙 템플릿 문제 관리자 지정 된 Active Directory 그룹에 맞는 \(SID\) ID 합니다. 인증 Active Directory 도메인 서비스 \(AD DS\) 하는 모든 사용자는 들어오는 그룹에 속해 있는 각 그룹에 대 한 주장 SID 해야 합니다. 기본적으로 수용 변환 규칙의 Active Directory 클레임 공급자 신뢰에서 SID 주장 이러한 그룹을 통해 전달 합니다. 클레임 발급 기준으로 Sid가 AD DS의 사용자 그룹을 찾는 보다 훨씬 더 빨라지고 이러한 그룹을 사용 하 여 합니다.  
  
이 규칙 하나의 클레임만 사용 하는 경우 전송, Active Directory 선택한 그룹에 따라 합니다. 예를 들어, 사용자가 도메인 관리자 보안 그룹의 회원 "관리자" 값 그룹 청구 보내라는 됩니다 규칙을 만들려면이 규칙 템플릿을 사용할 수 있습니다.  
  
## <a name="configuring-this-rule-on-a-claims-provider-trust"></a>이 규칙 클레임 공급자 신뢰에서 구성  
관리자가 그룹 Sid 매우 AD DS Active Directory를 제외한 모든 클레임 공급자에 대 한 일반적인는 클레임 공급자 로부터 수신 하는 경우에이 규칙 종류 클레임 공급자 신뢰 수용 변환 규칙에 사용 해야 합니다.  
  
## <a name="how-to-create-this-rule"></a>이 규칙 만드는 방법  
클레임으로 전송 LDAP 그룹 구성원을 사용 하 여 규칙 snap\에서 광고 FS 관리에서 템플릿 또는 클레임 규칙 언어 중 하나를 사용 하 여이 규칙 만듭니다. 이 규칙 템플릿을 다음과 같은 구성 옵션을 제공합니다.  
  
-   클레임은 규칙 이름을 지정합니다  
  
-   선택을 사용 하 여 사용자의 그룹 선택  
  
-   보내는 클레임 유형 선택  
  
-   거는 기능은 발신 이름 ID 형식을 선택 \ (사용 하지 않는 이름 ID 보내는 클레임 입력 field\에서 선택 됩니다 때에)  
  
-   보내는 클레임 지정  
  
이 규칙 만드는 방법에 대 한 자세한 내용은 참조 [규칙 클레임으로 전송 그룹 구성원을 만들어](https://technet.microsoft.com/en-us/library/ee913569.aspx)합니다.  
  
## <a name="using-the-claim-rule-language"></a>클레임은 규칙 언어를 사용 하 여  
그룹 SID 이외의 SID 들어오는에 따라 클레임 실행 하려는 경우 변환 들어오는 클레임 규칙 템플릿을 사용 합니다. 관리자는 사용자의 회원은 모든 그룹의 이름을 검색 하려는 경우 보내기 LDAP 특성 클레임 규칙 템플릿으로 대신 사용와 **토큰 그룹** 특성 합니다.  
  
### <a name="example-how-to-issue-group-claims-based-on-the-users-group-membership"></a>예: 사용자의 그룹 구성원에 따라 그룹 클레임 실행 하는 방법  
다음 규칙 SID 들어오는 그룹에 따라 사용자에 대 한 주장 그룹 문제:  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-21-397933417-626991126-188441444-512", Issuer == "AD AUTHORITY"]  
=> issue(Type = "http://schemas.xmlsoap.org/claims/Group", Value = "administrators", Issuer = c.Issuer, OriginalIssuer = c.OriginalIssuer, ValueType = c.ValueType);  
```  
  
## <a name="additional-references"></a>추가 참조  
[LDAP 특성 클레임 파일로 보낼 규칙 만들기](https://technet.microsoft.com/library/dd807115.aspx)  
  

