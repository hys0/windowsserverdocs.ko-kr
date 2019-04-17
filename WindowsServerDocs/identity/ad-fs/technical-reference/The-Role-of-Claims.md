---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: "클레임 역할"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 98765deaba67ffdc0ee18b6d8ef573e531d739cc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-claims"></a>클레임 역할
Id claims\ 기반 모델 클레임 federation 과정에서 가장 중요 재생, 모든 Web\ 기반 인증과 요청의 결과 결정 하는 핵심 구성 요소는 합니다. 이 모델 디지털 id 및 권한 안전 하 게 표시할 수 있도록 또는 *클레임*, 보안 및 표준화 방식으로 enterprise 경계 전체 합니다.  
  
## <a name="what-are-claims"></a>클레임은 무엇입니까?  
간단한 형식으로 클레임은 정말 놀라 *문을* \ (예: 이름, id를 group\), 사용자가 인터넷에 아무 곳 이나 있는 claims\ 기반 응용 프로그램에 대 한 액세스 권한을 부여에 기본적으로 사용 되는 대 한 설명 합니다. 각 문의 해당 하는 *값* 클레임에 저장 된 합니다.  
  
### <a name="how-claims-are-sourced"></a>클레임은 소스가 하는 방법  
Active Directory Federation Services \(AD FS\)에 어떤 클레임 연합된 파트너 간에 교환 정의 합니다. 그러나이 수행 하기 먼저 채울 하거나 해야 검색된 값 또는 계산된 값 클레임 소스 합니다. 각 청구 값 사용자, 그룹 또는 엔터티의 값을 나타냅니다 및 두 가지 방법 중 하나에 발생 합니다.  
  
1.  클레임 구성 하는 가치는 검색 때 특성 스토어에서 예를 들어, Active Directory 사용자 계정의 속성에서 판매 부서 특성 값을 검색할 때 합니다. 자세한 내용은 참조 [The 특성 스토어 역할](The-Role-of-Attribute-Stores.md)합니다.  
  
2.  때 수신 클레임 값 규칙에 표시 되는 논리에 따라 다른 값을 변환 됩니다. 예를 들어, 보내는 클레임으로 전송 되기 전에 들어오는 도메인 관리자의 주장 하는 경우 새로운 관리자 값으로 변환 됩니다. 자세한 내용은 참조 [The 클레임 규칙 역할](The-Role-of-Claim-Rules.md)합니다.  
  
클레임 e\ 메일 주소, 사용자 계정 이름 \(UPN\), 그룹 구성원 시간 및 기타 계정 특성 포함 될 수 있습니다.  
  
### <a name="how-claims-flow"></a>클레임 플로 방법  
다른 자 호스트 하는 Web\ 기반 응용 프로그램에 대 한 권한 작업을 수행 하 여 클레임 값에 의존 합니다. 이러한 자 라고 *신뢰 당사자* snap\에서 광고 FS 관리에서 합니다. Federation 서비스는 많은 사용자 간에 신뢰 중개 담당 합니다. 처리 라고도 클레임 소스 처음에 조직에서 클레임 신뢰할 수 있는 교환 흐름을 지원 하도록 설계 되어 *공급자 주장* snap\에를 신뢰 AD FS 관리에서 합니다. 당사자에는 이러한 클레임 승인 결정을 내릴 수 사용 합니다.  
  
이 프로세스를 사용 하 여 클레임 흐름 라고는 *클레임 파이프라인*합니다. 세 가지 단계를 통해 클레임 파이프라인 클레임 흐름에서:  
  
1.  클레임 공급자 로부터 받은 클레임 수용 변환 규칙 클레임 공급자 신뢰에서 처리 됩니다. 이 규칙 클레임 공급자에서 어떤 클레임 수 있도록 허용을 결정 합니다.  
  
2.  승인 변환 규칙 출력 발급 부여 규칙 입력으로 사용 됩니다. 이 규칙은 사용자가 당사자에 액세스할 수 있는지 여부를 결정 합니다.  
  
3.  승인 변환 규칙 출력 발급 변환 규칙 입력으로 사용 됩니다. 이 규칙 당사자에 보낼 수 있는 클레임 결정 합니다.  
  
자세한 내용은 참조 [클레임 파이프라인 The 역할](The-Role-of-the-Claims-Pipeline.md)  
  
### <a name="how-claims-are-issued"></a>클레임 발급 방법  
클레임은 규칙으로 작성할 때 들어오는 클레임 클레임 규칙에 대 한 소스 규칙 클레임 공급자 신뢰 또는 신뢰 파티 신뢰를 작성 하는 있는지 여부에 따라 다릅니다. 청구 공급자 보안에 대 한 청구 규칙으로 작성할 때 들어오는 클레임은 신뢰할 수 있는 청구 공급자 로부터 Federation 서비스에 전송 클레임입니다. 신뢰 파티 보안에 대 한 규칙으로 작성할 때 들어오는 클레임은 해당 클레임 공급자 신뢰 클레임 규칙 출력 하는 클레임입니다. 수신 청구 및 보내는 청구에 대 한 자세한 내용은 참조 [클레임 파이프라인 The 역할](The-Role-of-the-Claims-Pipeline.md) 및 [클레임 엔진 The 역할](The-Role-of-the-Claims-Engine.md)합니다.  
  
## <a name="what-are-claim-types"></a>클레임은 형식이 있나요?  
클레임 유형 클레임 가치에 대 한 상황에 맞는 제공합니다. 일반적으로 Uniform 리소스 식별자 \(URI\)로 표시 됩니다. ADFS 모든 클레임 종류를 지원할 수 있는 하 고 다음 표에 클레임 형식을 기본적으로 구성 됩니다.  
  
|이름|설명|URI|  
|--------|---------------|-------|  
|E\ 메일 주소|사용자의 e\ 메일 주소|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/emailaddress|  
|이름|사용자의 이름이|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/givenname|  
|이름|사용자의 고유한 이름|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/name|  
|UPN|사용자는 사용자의 \(UPN\) 표시 된 이름|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/upn|  
|일반 이름|사용자의 일반적인 이름|http:///\/schemas.xmlsoap.org\/claims\/CommonName|  
|광고 FS 1.x E\ 메일 주소|ADFS 1.1 또는 ADFS 1.0와 상호 작용할 때 사용자의 e\ 메일 주소|http:///\/schemas.xmlsoap.org\/claims\/EmailAddress|  
|그룹|사용자 있는 그룹|http:///\/schemas.xmlsoap.org\/claims\/Group|  
|광고 FS 1.x UPN|ADFS 1.1 또는 ADFS 1.0와 상호 작용할 때 사용자의 UPN|http:///\/schemas.xmlsoap.org\/claims\/UPN|  
|역할|사용자가 역할|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/role|  
|성|사용자의 성|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/surname|  
|PPID|사용자의 개인 식별자|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/privatepersonalidentifier|  
|이름 식별자|사용자의 SAML 이름 식별자|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/nameidentifier|  
|인증 방법|사용자를 인증에 사용 하는 방법|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/authenticationmethod|  
|거부 SID 그룹만|사용자의 deny\ 전용 그룹 SID|http:///\/schemas.xmlsoap.org\/ws\/2005\/05\/identity\/claims\/denyonlysid|  
|거부 주 SID만|사용자의 deny\ 전용 기본 SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarysid|  
|기본 그룹 SID|Deny\ 전용 주 그룹 SID 사용자의|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/denyonlyprimarygroupsid|  
|그룹 SID|사용자의 그룹 SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/groupsid|  
|주 그룹 SID|사용자의 기본 그룹 SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarygroupsid|  
|주 SID|사용자의 기본 SID|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/primarysid|  
|Windows 계정 이름|도메인 계정 이름을 형태의 사용자의<domain>\\<user>|http:///\/schemas.microsoft.com\/ws\/2008\/06\/identity\/claims\/windowsaccountname|  
  
## <a name="what-are-claim-descriptions"></a>클레임 설명을 이란 무엇 인가요?  
클레임 설명을 나타낼 목록이 클레임 종류 federation 메타 데이터에 ADFS 지원 하 고 있는 게시 될 수 있습니다. 위의 표에 설명 클레임 종류의 snap\ AD FS 관리에서 클레임 설명을으로 구성 됩니다.  
  
클레임 설명 federation 메타 데이터를 게시할 수 있는 컬렉션 ADFS 구성 데이터베이스에 저장 됩니다. 이러한 주장 설명을 Federation 서비스의 다양 한 구성 요소 사용 됩니다.  
  
각 청구 설명 클레임 유형 URI, 이름, 게시 상태 및 설명을 포함 되어 있습니다. 클레임 설명 컬렉션을 사용 하 여 관리할 수 있습니다는 **주장 설명을** 노드 snap\에서 광고 FS 관리에서 합니다. 기능을 사용 하 여 snap\ 클레임 설명 게시 상태를 수정할 수 있습니다. 다음 설정을 사용할 수 있습니다.  
  
-   **이 Federation 서비스를 사용할 수 있는 클레임 형식으로 federation 메타 데이터에이 청구를 게시** \(Publish as Accepted\)-이 Federation 서비스에서 다른 클레임 공급자의 수락 클레임 종류를 나타냅니다.  
  
-   **이 Federation 서비스를 보낼 수 있는 클레임 형식으로 federation 메타 데이터에이 청구를 게시** \(Publish as Sent\)-이 Federation 서비스에서 제공 되는 클레임 유형 나타냅니다. 이러한 경우 클레임 Federation 서비스 전송 하는 것과 다른 사람에 게 게시 합니다. 실제 클레임 유형 클레임 공급자에서 보낸이 목록의 일부 많습니다.  
  
클레임 형식의 게시 상태를 설정 하는 방법에 대 한 자세한 내용은 참조 [주장 설명을 추가](https://technet.microsoft.com/library/dd807051.aspx) AD FS 배포 가이드에 있습니다.  
  
### <a name="when-generating-federation-metadata"></a>Federation 메타 데이터를 생성 하는 경우  
Federation 메타 데이터 게시 하기에 표시 하는 모든 클레임 설명을 포함 되어 있습니다.  
  
### <a name="when-claims-rules-are-processed"></a>청구 규칙은 처리  
클레임 설명에 대 한 구성 정보를 유지 하면 더 쉽습니다 클레임에 대 한 규칙 구성할 수 있습니다. 청구 공급자 조직에서 사용할 수 있는 클레임 규칙에 대 한 자세한 내용은 참조 [주장 규칙의 역할은](The-Role-of-Claim-Rules.md)합니다.  
  

