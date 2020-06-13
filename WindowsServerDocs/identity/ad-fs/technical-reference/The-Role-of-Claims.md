---
ms.assetid: 22f53391-8c6a-4873-a1f4-08b4760ea621
title: 클레임의 역할
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 661f1b3f227a3e04c1328798a632b10b55df1c20
ms.sourcegitcommit: 7200143aa787c7ac05ae0e012263b1c9a95b87ed
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721751"
---
# <a name="the-role-of-claims"></a>클레임의 역할

클레임 \- 기반 id 모델에서 클레임은 페더레이션 프로세스에서 pivotal 역할을 수행 하 고, 모든 웹 \- 기반 인증 및 권한 부여 요청의 결과를 결정 하는 핵심 구성 요소입니다. 이 모델을 사용하면 조직에서 보안 및 엔터프라이즈 경계에 표준화된 방식으로 디지털 ID와 권한 또는 *클레임*을 안전하게 적용할 수 있습니다.

## <a name="what-are-claims"></a>클레임이란?

가장 간단한 형태의 클레임 *은 단순히* \( 사용자에 대 한 이름, id, 그룹 \) 등 사용자에 대 한 액세스 권한을 부여 하는 것입니다 .이는 주로 \- 인터넷에 있는 클레임 기반 응용 프로그램에 대 한 액세스 권한을 부여 하는 데 사용 됩니다. 각 문은 클레임에 저장된 *값*에 해당합니다.

### <a name="how-claims-are-sourced"></a>클레임 소싱 방식

Active Directory Federation Services AD FS 페더레이션 서비스는 \( \) 페더레이션된 파트너 간에 교환 되는 클레임을 정의 합니다. 그러나 이렇게 하려면 먼저 검색된 값 또는 계산된 값으로 클레임을 채우거나 소싱해야 합니다. 각 클레임 값은 사용자, 그룹 또는 엔터티의 값을 나타내며 다음 두 가지 방법 중 하나로 소싱됩니다.

1.  클레임을 구성하는 값이 특성 저장소에서 검색되는 경우(예: 특성 값 Sales Department가 Active Directory 사용자 계정의 속성에서 검색되는 경우). 자세한 내용은 [특성 저장소의 역할](The-Role-of-Attribute-Stores.md)을 참조하세요.

2.  들어오는 클레임의 값이 규칙에 표현된 논리에 따라 다른 값으로 변환되는 경우(예: 값이 Domain Admins인 들어오는 클레임이 나가는 클레임으로 전송되기 전에 새 값 Administrators로 변환되는 경우). 자세한 내용은 [클레임 규칙의 역할](The-Role-of-Claim-Rules.md)을 참조하세요.

클레임에는 전자 \- 메일 주소, UPN (사용자 계정 이름) \( \) , 그룹 구성원 자격, 기타 계정 특성 등의 값이 포함 될 수 있습니다.

### <a name="how-claims-flow"></a>클레임의 흐름 방식

다른 당사자는 클레임 값을 사용 하 여 \- 호스트 하는 웹 기반 응용 프로그램에 대 한 권한 부여 작업을 수행 합니다. 이러한 당사자를 AD FS 관리 스냅인에서 *신뢰 당사자* 라고 \- 합니다. 페더레이션 서비스는 서로 다른 여러 당사자 간 트러스트의 조정을 담당합니다. 초기에 클레임을 원본으로 하는 조직에서 신뢰할 수 있는 클레임 교환을 처리 하 고 전달 하도록 설계 되었습니다 .이는 AD FS 관리에서 *클레임 공급자* 라고도 하는 \- 신뢰 당사자에 게 있습니다. 그런 다음 신뢰 당사자는 이러한 클레임을 사용하여 권한 부여 결정을 내립니다.

이 프로세스를 사용하는 클레임 흐름을 *클레임 파이프라인*이라고 합니다. 클레임 파이프라인을 통한 클레임 흐름에는 세 가지 단계가 있습니다.

1.  클레임 공급자로부터 받은 클레임은 클레임 공급자 트러스트의 수용 변환 규칙에 의해 처리됩니다. 이러한 규칙은 클레임 공급자가 수용하는 클레임을 결정합니다.

2.  수용 변환 규칙의 출력은 발급 권한 부여 규칙의 입력으로 사용됩니다. 이러한 규칙은 사용자가 신뢰 당사자에 액세스할 수 있는지 여부를 결정합니다.

3.  수용 변환 규칙의 출력은 발급 변환 규칙의 입력으로 사용됩니다. 이러한 규칙은 신뢰 당사자에게 전송되는 클레임을 결정합니다.

자세한 내용은 [클레임 파이프라인의 역할](The-Role-of-the-Claims-Pipeline.md)을 참조하세요.

### <a name="how-claims-are-issued"></a>클레임 발급 방식

클레임 규칙을 작성할 때 클레임 규칙에 대한 들어오는 클레임의 소스는 클레임 공급자 트러스트에 대한 규칙을 작성하는지 또는 신뢰 당사자 트러스트에 대한 규칙을 작성하는지에 따라 달라집니다. 클레임 공급자 트러스트에 대한 클레임 규칙을 작성하는 경우 들어오는 클레임은 신뢰할 수 있는 클레임 공급자가 페더레이션 서비스로 전송한 클레임입니다. 신뢰 당사자 트러스트에 대한 규칙을 작성하는 경우 들어오는 클레임은 적용 가능한 클레임 공급자 트러스트의 클레임 규칙에 의해 출력된 클레임입니다. 들어오는 클레임과 나가는 클레임에 대한 자세한 내용은 [클레임 파이프라인의 역할](The-Role-of-the-Claims-Pipeline.md) 및 [클레임 엔진의 역할](The-Role-of-the-Claims-Engine.md)을 참조하세요.

## <a name="what-are-claim-types"></a>클레임 유형이란?

클레임 유형은 클레임 값에 대한 컨텍스트를 제공하며, 일반적으로 Uniform Resource Identifier URI로 표시 됩니다 \( \) . AD FS는 모든 클레임 유형을 지원할 수 있으며, 기본적으로 다음 표에 나와 있는 클레임 유형으로 구성 됩니다.

|Name|설명|URI|
|--------|---------------|-------|
|전자 \- 메일 주소|\-사용자의 전자 메일 주소입니다.|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ emailaddress|
|이름|사용자의 지정된 이름입니다.|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ givenname|
|Name|사용자의 고유한 이름입니다.|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ 이름|
|UPN|\(사용자의 upn (사용자 계정 이름) \)|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ upn|
|일반 이름|사용자의 일반 이름입니다.|http: \/ \/schemas.xmlSoap.org \/ 클레임 \/ CommonName|
|AD FS 1.x 전자 \- 메일 주소|\-AD FS 1.1 또는 ADFS 1.0과 상호 운용할 때 사용 되는 사용자의 전자 메일 주소|http: \/ \/schemas.xmlSoap.org \/ 클레임 \/ EmailAddress|
|그룹|사용자가 구성원으로 속해 있는 그룹입니다.|http: \/ \/schemas.xmlSoap.org \/ 클레임 \/ 그룹|
|AD FS 1.x UPN|AD FS 1.1 또는 AD FS 1.0과 상호 운용할 때 사용되는 사용자의 UPN입니다.|http: \/ \/schemas.xmlSoap.org \/ 클레임 \/ UPN|
|역할|사용자의 역할입니다.|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ identity \/ 클레임 \/ 역할|
|Surname|사용자의 성입니다.|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ 성|
|PPID|사용자의 개인 식별자입니다.|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ privatepersonalidentifier|
|이름 식별자|사용자의 SAML 이름 식별자입니다.|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ nameidentifier|
|인증 방법|사용자를 인증하는 데 사용되는 방법입니다.|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ identity \/ 클레임 \/ authenticationmethod|
|거부 전용 그룹 SID|\-사용자의 거부 전용 그룹 SID입니다.|http: \/ \/schemas.xmlsoap.org \/ ws \/ 2005 \/ 05 \/ identity \/ 클레임 \/ denyonlysid|
|거부 전용 주 SID|\-사용자의 거부 전용 주 SID입니다.|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ identity \/ 클레임 \/ denyonlyprimarysid|
|거부 전용 주 그룹 SID|\-사용자의 거부 전용 주 그룹 SID입니다.|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ identity \/ 클레임 \/ denyonlyprimarygroupsid|
|그룹 SID|사용자의 그룹 SID입니다.|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ identity \/ 클레임 \/ 그룹 sid|
|주 그룹 SID|사용자의 주 그룹 SID입니다.|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ id \/ 클레임 \/ primarygroupsid|
|주 SID|사용자의 주 SID입니다.|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ id \/ 클레임 \/ primarysid|
|Windows 계정 이름|형식의 사용자에 대 한 도메인 계정 이름\<domain\>\\\<user\>|http: \/ \/ schemas.microsoft.com \/ ws \/ 2008 \/ 06 \/ identity \/ 클레임 \/ windowsaccountname|

## <a name="what-are-claim-descriptions"></a>클레임 설명이란?

클레임 설명은 AD FS에서 지원 하며 페더레이션 메타 데이터에 게시 될 수 있는 클레임 유형의 목록을 나타냅니다. 위의 표에 언급 된 클레임 유형은 AD FS 관리 스냅인에서 클레임 설명으로 구성 됩니다 \- .

페더레이션 메타데이터에 게시되는 클레임 설명의 컬렉션은 AD FS 구성 데이터베이스에 저장됩니다. 이러한 클레임 설명은 페더레이션 서비스의 여러 구성 요소에서 사용됩니다.

각 클레임 설명은 클레임 유형 URI, 이름, 게시 상태 및 설명을 포함합니다. AD FS 관리 스냅인의 **클레임 설명** 노드를 사용 하 여 클레임 설명 컬렉션을 관리할 수 있습니다 \- . 스냅인을 사용 하 여 클레임 설명의 게시 상태를 수정할 수 있습니다 \- . 다음 설정을 사용할 수 있습니다.

- **페더레이션 메타 데이터의이 클레임을이 페더레이션 서비스에서 수락할 수 있는 클레임 유형으로 게시 합니다** \( . 승인 된 상태로 게시 \) -이 페더레이션 서비스에서 다른 클레임 공급자가 수락 하는 클레임 유형을 나타냅니다.

- **페더레이션 메타 데이터의이 클레임을이 페더레이션 서비스에서 보낼 수 있는 클레임 유형으로 게시 합니다** \( . 보낸 사람 게시 \) -이 페더레이션 서비스에서 제공 하는 클레임 유형을 나타냅니다. 페더레이션 서비스는 이 클레임 유형을 보내려는 클레임 유형으로 게시합니다. 클레임 공급자가 보낸 실제 클레임 유형은 이 목록의 하위 집합에 속하는 경우가 많습니다.

클레임 유형의 게시 상태를 설정 하는 방법에 대 한 자세한 내용은 AD FS 배포 가이드에서 [클레임 설명 추가](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/add-a-claim-description) 를 참조 하세요.

### <a name="when-generating-federation-metadata"></a>페더레이션 메타데이터를 생성하는 경우

페더레이션 메타데이터는 게시용으로 표시된 모든 클레임 설명을 포함합니다.

### <a name="when-claims-rules-are-processed"></a>클레임 규칙이 처리되는 경우

클레임 설명에 대한 구성 정보를 유지하면 클레임에 대한 규칙을 보다 쉽게 구성할 수 있습니다. 클레임 공급자 조직에서 사용할 수 있는 클레임 규칙에 대한 자세한 내용은 [클레임 규칙의 역할](The-Role-of-Claim-Rules.md)을 참조하세요.
