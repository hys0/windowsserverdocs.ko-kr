---
ms.assetid: 53ee93e2-09ea-4f8b-adb7-c24c59f055ea
title: AD FS에서 URI를 사용하는 방법
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2ae91b16448c5acd61712332310544c1fd66789f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385493"
---
# <a name="how-uris-are-used-in-ad-fs"></a>AD FS에서 URI를 사용하는 방법
\(Uri\) (Uniform resource identifier)는 고유 식별자로 사용 되는 문자 문자열입니다.  AD FS에서 URI는 파트너 네트워크 주소와 구성 개체를 모두 식별하는 데 사용됩니다.  파트너 네트워크 주소를 식별하는 데 사용되는 경우 URI는 항상 URL이고,  구성 개체를 식별하는 데 사용되는 경우 URI는 URN 또는 URL일 수 있습니다.  URI에 대한 자세한 내용은 [RFC 2396](https://go.microsoft.com/fwlink/?LinkId=48289) 및 [RFC 3986](https://go.microsoft.com/fwlink/?LinkId=90453)을 참조하세요.  
  
## <a name="uris-as-partner-network-addresses"></a>파트너 네트워크 주소로서의 URI  
다음은 AD FS에서 관리자가 가장 자주 처리하는 네트워크 주소 URL입니다.  
  
-   Ws\-Federation, SAML, ws\-Trust, 페더레이션 메타 데이터, WS\-ws-metadataexchange, 개인 정보 및 조직 url을 포함 하는 페더레이션 서비스의 url  
  
-   Ws-federation\-, SAML 및 페더레이션 메타 데이터 url을 비롯 한 신뢰 당사자 트러스트의 url  
  
-   WS\-federation, SAML 및 페더레이션 메타 데이터 url을 포함 한 클레임 공급자 트러스트의 url  
  
## <a name="uris-as-object-identifiers"></a>개체 식별자로서의 URI  
다음 표에서는 AD FS에서 관리자가 가장 자주 처리하는 식별자에 대해 설명합니다.  
  
|식별자 이름|설명|비교|  
|-------------------|---------------|---------------|  
|페더레이션 서비스 식별자|이 식별자는 페더레이션 서비스를 식별하는 데 사용됩니다.  이 식별자는 이 페더레이션 서비스에 클레임을 발급하는 클레임 공급자뿐만 아니라 이 페더레이션 서비스의 클레임을 사용하는 신뢰 당사자에서 사용됩니다.|사용자가 클레임 공급자로부터 이 페더레이션 서비스에 대한 클레임을 요청하면 페더레이션 서비스 식별자가 클레임의 대상을 식별하는 데 사용됩니다.<br /><br />이 페더레이션 서비스는 클레임 공급자로부터 클레임을 받으면 해당 페더레이션 서비스 식별을 조회하여 클레임의 범위에 포함되는지 확인합니다.<br /><br />신뢰 당사자는 이 페더레이션 서비스에서 클레임을 받으면 클레임의 발급자가 페더레이션 서비스 식별자와 일치하는지 확인합니다.|  
|신뢰 당사자 식별자|이 식별자는 이 페더레이션 서비스에 대한 신뢰 당사자를 식별하는 데 사용되며,  신뢰 당사자에 대한 클레임을 발급하는 경우에도 사용됩니다.|사용자가 이 페더레이션 서비스에서 신뢰 당사자에 대한 클레임을 요청하면 신뢰 당사자 식별자는 클레임의 대상으로 지정되어야 하는 신뢰 당사자를 식별하는 데 사용됩니다.  이 비교는 아래 \(\)참조 접두사 일치를 사용 하 여 수행 됩니다.<br /><br />신뢰 당사자는 클레임을 받으면 보안 토큰에서 식별자를 확인하여 클레임의 대상으로 지정되었는지 확인합니다.|  
|클레임 공급자 식별자|이 식별자는 이 페더레이션 서비스에 대한 클레임 공급자를 식별하는 데 사용되며,  클레임 공급자로부터 클레임을 받을 때도 사용됩니다.|이 페더레이션 서비스는 클레임 공급자에서 클레임을 받으면 클레임의 발급자가 클레임 공급자 식별자와 일치하는지 확인합니다.|  
|클레임 형식|이 식별자는 클레임의 형식을 정의하는 데 사용되며,  클레임을 보내고 받을 때 이 페더레이션 서비스, 클레임 공급자 및 신뢰 당사자에서 사용됩니다.|페더레이션 서비스가 클레임 공급자에서 클레임을 받으면 관리자는 해당 클레임 공급자 트러스트와 관련된 클레임 규칙을 사용하여 클레임 형식을 비교하고 클레임을 처리할 수 있습니다.  또한 신뢰 당사자 트러스트와 관련된 클레임 규칙을 사용하여 관리자는 클레임 공급자 트러스트 규칙에서 나오는 클레임의 형식을 비교하고 발급할 클레임을 결정할 수 있습니다.|  
  
## <a name="uri-prefix-matching-for-relying-party-identifiers"></a>신뢰 당사자 식별자에 대한 URI 접두사 일치  
URI의 경로 구문은 계층적으로 구성 되며 모든 "\/" 문자 또는 모든 ":" 문자로 구분 됩니다.  따라서 경로는 구분 문자에 따라 경로 섹션으로 분할할 수 있습니다.  접두사 일치를 사용할 경우 각 섹션은 일치 규칙 \(에 따라 전체 일치 해야 합니다. 이러한 규칙은 일치\)하는 대/소문자를 제어 합니다. 일치 규칙에 대 한 자세한 내용은 위에서 설명한 RFC를 참조 하세요.  
  
신뢰 당사자가 페더레이션 서비스에 대한 요청에서 식별되면 AD FS는 접두사 일치 논리를 사용하여 AD FS 구성 데이터베이스에 일치하는 신뢰 당사자 트러스트가 있는지 확인합니다.  
  
예를 들어 AD FS \(구성 데이터베이스의 신뢰 당사자 식별자가 들어오는 요청의 \(신뢰\) 당사자 식별자에 대 한 URI1 경우 다음을 충족 해야 합니다.\)URI2  
  
-   경로 섹션 \(또는 기관의 후행\) 구분 기호 슬래시 및 콜론은 무시 해야 합니다.  
  
-   URI1과 URI2의 체계 및 기관 부분은 대/소문자에 관계없이 정확히 일치해야 합니다.  
  
-   URI1의 각 경로 섹션은 URI2의 해당 경로 \(섹션에서 선택\) 하는 대/소문자 구분을 기준으로 정확히 일치 해야 합니다.  
  
-   URI2에는 URI1보다 경로 섹션이 더 많을 수 있지만 URI1에는 URI2보다 경로 섹션이 더 많으면 안 됩니다.  
  
-   URI1에는 URI2보다 경로 섹션이 더 많을 수 없습니다.  
  
-   URI1에 쿼리 문자열이 있는 경우 URI2 쿼리 문자열과 정확히 일치해야 합니다.  
  
-   URI1에 조각이 있는 경우 URI2 조각과 정확히 일치해야 합니다.  
  
다음 표에서는 추가 예제를 제공합니다.  
  
|AD FS 구성 데이터베이스의 신뢰 당사자 식별자|요청 메시지의 신뢰 당사자 식별자|요청 식별자가 구성 식별자와 일치하는지 여부|Reason|  
|------------------------------------------------------------|-----------------------------------------------|------------------------------------------------------------|----------|  
|http:\/\/contoso.com|http:\/\/contoso.com|true|정확히 일치|  
|http:\/\/contoso.com\/|http:\/\/contoso.com|true|후행 슬래시가 무시됩니다.|  
|http:\/\/contoso.com|http:\/\/contoso.com\/|true|후행 슬래시가 무시됩니다.|  
|http:\/\/contoso.com|http:\/\/contoso.comhr\/|true|URI1에 경로가 없으며 URI2의 체계 및 기관과 일치합니다.|  
|http:\/\/contoso.comhr\/|http:\/\/contoso.comhr\/web\/|true|첫 번째 경로 섹션이 일치하며, URI1 에는 두 번째 경로 섹션이 없습니다.|  
|http:\/\/contoso.comhr\/|http:\/\/contoso.comhr\/web\/?m\=t\/|true|위와 동일한 이유로 쿼리 문자열에서 아무것도 변경 되지 않습니다.|  
|http:\/\/contoso.comhr\/\/|http:\/\/contoso.com\/hrw\/main|FALSE|URI1 경로 섹션 1이 URI2 경로 섹션 1과 일치하지 않습니다.|  
|http:\/\/contoso.comhr\/|http:\/\/contoso.com|FALSE|URI1에 URI2보다 더 많은 경로 섹션이 있습니다.|  
|http:\/\/contoso.comhr\/|http:\/\/contoso.com\/hrweb|FALSE|첫 번째 경로 섹션이 일치하지 않습니다.|  
|http:\/\/contoso.com?\/mt\=|http:\/\/contoso.com?\/mf\=|FALSE|쿼리 문자열 부분이 일치하지 않습니다.|  
|https:\/\/contoso.com|http:\/\/contoso.com|FALSE|체계 부분이 일치하지 않습니다.|  
|http:\/\/sts.contoso.com|http:\/\/contoso.com|FALSE|기관 부분이 일치하지 않습니다.|  
|http:\/\/contoso.com|http:\/\/sts.contoso.com|FALSE|기관 부분이 일치하지 않습니다.|  
  

