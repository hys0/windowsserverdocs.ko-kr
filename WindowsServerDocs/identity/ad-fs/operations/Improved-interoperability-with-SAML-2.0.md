---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: "SAML 2.0 상호 운용성을 향상된"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4f55eaacec8ee0eb41e1980f1aa15c6256f8b979
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="improved-interoperability-with-saml-20"></a>SAML 2.0 상호 운용성을 향상된

>Windows Server 2016 적용 됩니다.

  
Windows Server 2016에 ADFS 여러 엔터티 포함 된 메타 데이터를 기반 신뢰를 가져오는 대 한 지원을 포함 하 여 추가 SAML 프로토콜 지원을 포함 되어 있습니다.  이 통해 ADFS InCommon 연합과 표준 2.0 eGov에 맞는 다른 구현 같은 confederations 참여를 구성할 수 있습니다.   
  
새로운 기능: 그룹 당사자 또는 클레임 제공자 신뢰를 기반으로 합니다. 각 그룹 하나 또는 여러 EntityDescriptor 요소를 포함 하는 eGov에 지정 된 2.0 프로필으로 (< md:EntitiesDescriptor >) EntitiesDescriptor 요소입니다.  그룹 일반적인 인증 규칙 한 개별 신뢰 개체와 같은 다른 모든 속성을 수정할 수 있습니다.  
  
신뢰 그룹 ADFS 가져오고, ADFS 메타 데이터 문서에 따라 그룹으로는 신뢰 자동으로 업데이트 됩니다.  
  
이러한 시나리오를 사용 하기만 하면 새 PowerShell commandlets 추가 및 제거 AdfsClaimsProviderTrustsGroup AdfsRelyingPartyTrustsGroup 개체 하는 사용 하 여입니다. 이렇게 아래의 예제 에서처럼 URL 메타 데이터 또는 파일을 사용 하 여 합니다.  
  
또한 광고 FS 2016에는 SAML Core 사양 3.4.1.2 섹션에에서 설명 된 대로 매개 범위 내에 대 한 지원 합니다. 이 요소를 지정 당사자가 의존 나 인증에 대 한 더 많은 id 공급자를 요청할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>참조  
  
EGov 2.0 프로필 있습니다 [여기 합니다.](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
SAML Core 설정을 찾을 수 [여기 합니다.](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


