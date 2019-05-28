---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: SAML 2.0과의 향상된 상호 운용성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4148614ba35ce29f567edb08b94e115d3f9152e9
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189096"
---
# <a name="improved-interoperability-with-saml-20"></a>SAML 2.0과의 향상된 상호 운용성



  
Windows Server 2016에서 AD FS에는 여러 엔터티를 포함 하는 메타 데이터에 따라 트러스트 가져오기에 대 한 지원을 비롯 하 여 SAML 프로토콜 지원 추가 포함 되어 있습니다.  그러면 confederations InCommon 페더레이션 등 eGov 2.0 표준에 맞는 다른 구현에에서 참여 하도록 AD FS를 구성할 수 있습니다.   
  
새 기능을 그룹 클레임 공급자 트러스트 또는 신뢰 당사자를 기반으로 합니다. 각 그룹에 하나 이상의 EntityDescriptor 요소가 포함 된 eGov 2.0 프로필을 지정 하는 대로 EntitiesDescriptor (< md:EntitiesDescriptor >) 요소입니다.  그룹은 공통 권한 부여 규칙을 있고 개별 트러스트 개체와 같은 다른 모든 속성을 수정할 수 있습니다.  
  
AD FS를 신뢰 그룹을 가져온 후 AD FS 트러스트 메타 데이터 문서를 기반으로 하는 그룹으로 자동으로 업데이트 합니다.  
  
이러한 시나리오를 사용 하도록 설정 하는 것은 추가 및 제거 AdfsClaimsProviderTrustsGroup AdfsRelyingPartyTrustsGroup 개체를 사용 하는 새 PowerShell commandlet을 사용 하는 것으로 간단 합니다. 이렇게 하려면 아래 예제에 표시 된 대로 메타 데이터 URL 또는 파일을 사용 하 여 합니다.  
  
또한 AD FS 2016은 SAML 핵심 사양, 3.4.1.2 섹션에에서 설명 된 대로 영역 지정 매개 변수 지원 합니다. 이 요소에는 신뢰 당사자가 하나를 지정 또는 인증에 대 한 id 공급자를 더 요청할 수 있습니다.  
  
## <a name="examples"></a>예  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>참조  
  
EGov 2.0 프로필을 찾을 수 있습니다 [여기 있습니다.](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
SAML 핵심 사양 있습니다 [여기 있습니다.](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


