---
ms.assetid: 53ee93e2-09ea-4f8b-adb7-c24c59f055ea
title: "Adfs의 Uri 사용 방법"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 305bf0cece742c961604dacda7e27b8eac8065e5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
>적용 대상: Windows Server 2016, Windows Server 2012 r 2

# <a name="how-uris-are-used-in-ad-fs"></a>Adfs의 Uri 사용 방법
Uniform 리소스 식별자 \(URI\) 고유 식별자도 사용 되는 문자열을입니다.  Adfs에서 Uri 파트너 네트워크 주소 및 구성 개체를 식별 하는 데 사용 됩니다.  네트워크 파트너 주소를 식별 하는 데, URI URL 항상 됩니다.  구성 개체를 식별 하는 데, URN 또는 URL URI 수 있습니다.  Uri에 대 한 자세한 내용은 [RFC 2396](https://go.microsoft.com/fwlink/?LinkId=48289) 및 [RFC 3986](https://go.microsoft.com/fwlink/?LinkId=90453)합니다.  
  
## <a name="uris-as-partner-network-addresses"></a>Uri 파트너 네트워크 주소  
Adfs의 관리자가 처리 가장 자주 하는 네트워크 주소 Url는 다음과 같습니다.  
  
-   Url WS\ 연합, SAML, WS\ 신뢰, Federation 메타 데이터, WS\ MetadataExchange, 개인 정보 및 조직 Url 포함 Federation 서비스  
  
-   WS\ 연합, SAML, Federation 메타 데이터 Url 등 신뢰 파티 신뢰 Url  
  
-   WS\ 연합, SAML, Federation 메타 데이터 Url 등 클레임 공급자 신뢰를 Url  
  
## <a name="uris-as-object-identifiers"></a>Uri 개체 식별자로  
다음 표에서 가장 자주에서 처리 하는 관리자 adfs에서 식별자 설명 합니다.  
  
|식별자 이름|설명|비교|  
|-------------------|---------------|---------------|  
|Federation 서비스 id|이 식별자 Federation 서비스를 식별 하는 데 사용 됩니다.  클레임 클레임 공급자 문제 주장이 Federation 서비스 하 뿐만 아니라이 Federation 서비스에서 사용 하는 신뢰 당사자에서 사용 됩니다.|사용자 클레임이 Federation 서비스에 대 한 청구 공급자 로부터 요청 하면 Federation 서비스 식별자 클레임에 대 한 대상을 식별 하기 위해 사용 됩니다.<br /><br />이 Federation 서비스 클레임 공급자 로부터 클레임 받으면 클레임 해당 Federation 서비스 id를 찾아 그에 대 한 범위를 확인 합니다.<br /><br />당사자에는를 받을 때 클레임이 Federation 서비스에서 당사자는 클레임 발행인이 Federation 서비스 식별자와 일치 하는지 확인 합니다.|  
|파티 식별자를 사용합니다.|이 식별자 당사자가 Federation 서비스에 사용자의 신원을 확인 하는 데 사용 됩니다.  클레임 당사자를 실행할 때는 사용 됩니다.|했을 때 클레임이 Federation 서비스에서 당사자에 대 한를 신뢰 파티 식별자 당사자 대상 클레임을 식별 하기 위해 사용 됩니다.  이 비교 완료 일치 하는 \(see below\) 접두사 사용 합니다.<br /><br />당사자 클레임 받으면 클레임 대상에 대 한 되도록 보안 토큰에 해당 id를 확인 합니다.|  
|청구 공급자 식별자|이 식별자 클레임 공급자가 Federation 서비스를 식별 하는 데 사용 됩니다.  클레임 클레임 공급자 로부터 받을 때 사용 됩니다.|이 Federation 서비스 클레임 공급자 로부터 클레임에 수신 되 면이 Federation 서비스는 클레임 발행인이 클레임 공급자 식별자와 일치 하는지 확인 합니다.|  
|클레임 유형|이 식별자 클레임 유형의 정의 하는 데 사용 됩니다.  이 Federation 서비스, 청구 공급자와 보내고 클레임 받을 때 신뢰 당사자에서 사용 됩니다.|Federation 서비스 클레임 공급자 로부터 클레임 받으면 해당 클레임 공급자 보안와 관련 된 청구 규칙 관리자를 사용 하 여 클레임 형식을 비교를 클레임을 처리 합니다.  신뢰 파티 보안와 관련 된 청구 규칙 클레임 공급자 신뢰 규칙에서 나오는 클레임에서 클레임 유형은 비교 하려면 관리자를 사용 하 고 발급 하도록 요구 하는 결정할 수도 있습니다.|  
  
## <a name="uri-prefix-matching-for-relying-party-identifiers"></a>URI 접두사 신뢰 파티 식별자에 대 한와 일치 하는  
경로 URI 계층 구성 하 고 모두도 구분 "\ /"문자 또는 모두":" 문자.  따라서 경로 경로 섹션 구분 문자를 기반으로 분할 될 수 있습니다.  일치 하는 경우 접두사, 각 섹션 일치 규칙에 따라 전체 일치 해야 합니다. \ (이 규칙 matches\의 대/소문자를 제어 하는 데 사용). 일치 규칙에 대 한 자세한 내용은 참조 RFC의 위에 언급 된 것입니다.  
  
당사자를 Federation 서비스에 대 한 요청에 확인 된 ADFS ADFS 구성 데이터베이스에 일치 하는 신뢰 파티 보안 인지 확인 하려면 접두사 일치 논리를 사용 합니다.  
  
예를 들어 있는 경우 ADFS 구성 데이터베이스에 신뢰 파티 식별자 \(URI1\)는 신뢰 파티 식별자 들어오는에 접두사 요청 \(URI2\), 다음 충족 해야 합니다.  
  
-   구분 뒤에 \(slashes and colons\) 경로의 기관 또는 섹션에 무시 해야  
  
-   URI1 및 URI2 체계 및 권한 부분이 정확 하 게 소문자 일치 해야 합니다.  
  
-   각 경로 섹션 URI1의 정확한 일치 해야 \ (대/소문자 구분 chosen\에 따름) URI2 해당 경로 섹션을  
  
-   URI2 URI1, 보다 더 많은 경로 섹션 있을 수 있지만 URI1 URI2 보다 더 많은 경로 섹션 되어 있지 않아야  
  
-   URI1은 URI2 보다 더 많은 경로 섹션 여야 합니다.  
  
-   URI2 쿼리 문자열 정확 하 게 일치 해야 URI1 쿼리 문자열이 있는 경우  
  
-   URI2 조각 정확 하 게 일치 해야 URI1 조각 있으면  
  
다음 표에서 추가적인 예시를 제공합니다.  
  
|파티 식별자 ADFS 구성 데이터베이스에 의존합니다.|요청 메시지의 파티 식별자를 사용합니다.|식별자 일치 구성 식별자 요청?|이유|  
|------------------------------------------------------------|-----------------------------------------------|------------------------------------------------------------|----------|  
|http:///\/contoso.com|http:///\/contoso.com|진정한|일치|  
|http:///\/contoso.com\/|http:///\/contoso.com|진정한|뒤 슬래시는 무시 됩니다.|  
|http:///\/contoso.com|http:///\/contoso.com\/|진정한|뒤 슬래시는 무시 됩니다.|  
|http:///\/contoso.com|http:///\/contoso.com\/hr|진정한|URI1 옵션과 없는 경로 일치 구성표 URI2 권한을|  
|http:///\/contoso.com\/hr|http:///\/contoso.com\/hr\/web|진정한|첫 번째 경로 섹션와 일치, URI1에 두 번째 경로 섹션이 없음|  
|http:///\/contoso.com\/hr|http:///\/contoso.com\/hr\/web\/?m\=t|진정한|위의 같은 이유로 쿼리 문자열 하지 아무 것도 변경|  
|http:///\/contoso.com\/hr\/|http:///\/contoso.com\/hrw\/main|FALSE|섹션 1 URI1 경로 URI2 경로 섹션 1 일치 하지 않는|  
|http:///\/contoso.com\/hr|http:///\/contoso.com|FALSE|URI1은 URI2 보다 더 많은 경로 섹션에|  
|http:///\/contoso.com\/hr|http:///\/contoso.com\/hrweb|FALSE|첫 번째 경로 섹션 일치 하지 않는 경우|  
|http:///\/contoso.com\/?m\=t|http:///\/contoso.com\/?m\=f|FALSE|쿼리 문자열 부품 일치 하지 않는 경우|  
|https:\/\/contoso.com|http:///\/contoso.com|FALSE|구성표 부품 일치 하지 않는 경우|  
|http:///\/sts.contoso.com|http:///\/contoso.com|FALSE|기관 부품 일치 하지 않는 경우|  
|http:///\/contoso.com|http:///\/sts.contoso.com|FALSE|기관 부품 일치 하지 않는 경우|  
  

