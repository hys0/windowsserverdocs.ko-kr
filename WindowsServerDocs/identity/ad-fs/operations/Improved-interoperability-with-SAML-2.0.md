---
ms.assetid: 80b5335b-fa02-4944-900c-5fe4f5c6111d
title: SAML 2.0과의 향상된 상호 운용성
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d72636d77fe3240caab66dcab8657225d291bec6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407546"
---
# <a name="improved-interoperability-with-saml-20"></a>SAML 2.0과의 향상된 상호 운용성



  
Windows Server 2016의 AD FS에는 여러 엔터티를 포함 하는 메타 데이터를 기반으로 하는 트러스트 가져오기에 대 한 지원을 비롯 한 추가 SAML 프로토콜 지원이 포함 됩니다.  그러면 confederations InCommon 페더레이션 등 eGov 2.0 표준에 맞는 다른 구현에에서 참여 하도록 AD FS를 구성할 수 있습니다.   
  
새 기능은 신뢰 당사자 또는 클레임 공급자 트러스트 그룹을 기반으로 합니다. 각 그룹은 하나 이상의 EntityDescriptor 요소를 포함 하는 eGov 2.0 profile에 지정 된 EntitiesDescriptor (< md: EntitiesDescriptor >) 요소입니다.  그룹에는 일반적인 권한 부여 규칙이 있으며, 다른 모든 속성은 개별 신뢰 개체 처럼 수정할 수 있습니다.  
  
신뢰 그룹을 AD FS으로 가져오면 AD FS에서 메타 데이터 문서를 기반으로 트러스트를 그룹으로 자동 업데이트 합니다.  
  
이러한 시나리오를 사용 하는 것은 AdfsClaimsProviderTrustsGroup 및 AdfsRelyingPartyTrustsGroup 개체를 추가 및 제거 하는 새 PowerShell commandlet을 사용 하는 것 만큼 간단 합니다. 아래 예제에 표시 된 것 처럼 메타 데이터 URL 또는 파일을 사용 하 여이 작업을 수행할 수 있습니다.  
  
또한 AD FS 2016은 SAML 핵심 사양 섹션인 3.4.1.2 섹션에 설명 된 대로 범위 지정 매개 변수를 지원 합니다. 이 요소를 사용 하면 신뢰 당사자가 인증 요청에 대해 하나 이상의 id 공급자를 지정할 수 있습니다.  
  
## <a name="examples"></a>예  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataUrl "https://www.contosoconsortium.com/metadata/metadata.xml"   
```  
  
  
  
```  
Add-AdfsClaimsProviderTrustsGroup -MetadataFile "C:\metadata.xml"   
```  
  
## <a name="references"></a>참조  
  
EGov 2.0 프로필은 여기에서 찾을 수 있습니다 [.](https://kantarainitiative.org/confluence/download/attachments/60817482/kantara-report-egov-saml2-profile-2.0.pdf?version=1&modificationDate=1345580916000&api=v2)  
  
SAML 핵심 사양은 여기에서 찾을 수 있습니다 [.](https://docs.oasis-open.org/security/saml/v2.0/saml-core-2.0-os.pdf)   


