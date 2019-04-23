---
title: 클레임 발급을 AD FS 문제 해결-
description: 이 문서에서는 AD FS 사용 하 여 토큰 발급 문제를 해결 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fdf8851fe9b35f82191458ba3313fda2dc3ee4cf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839664"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>클레임 발급을 AD FS 문제 해결-
클레임은 문을 하나의 주제는 자신 또는 다른 방법에 대 한 제목입니다.  클레임을 신뢰 당사자가 발급 한와 하나 이상의 값을 지정 하 고 AD FS 서버에서 발급 한 보안 토큰에 패키지화 합니다.  이 프로세스에 몇 가지 움직이는 부분 이기 때문에 이러한 주요 부분으로 클레임 발급을 나눌 수 있습니다.

>[!NOTE]  
>사용할 수 있습니다 [ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) 에 [ADFS 도움말](https://adfshelp.microsoft.com) 문제를 해결 하는 데 도움이 되는 사이트 문제를 클레임 합니다.   

## <a name="token-request"></a>토큰 요청
신뢰 당사자로 이동할 때 리디렉션되 며 토큰 요청을 사용 하 여 AD fs 합니다.  요청을 사용 하 여 문제가 발생할 수 있습니다.  가장 주목할 만한 것:

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>제 3 자와 (특히 SAML)를 사용 하 여 서식 지정 요청

### <a name="pre-formated-urls-that-have-typos"></a>오타가 있는 사전으로 포맷 된 Url
신뢰 당사자 WS Federaion에서에서 토큰을 발급 하는 경우 URL 쿼리 문자열 매개 변수를 사용 하 여 해당 토큰 요청 제공 됩니다.  AD FS에 대 한 리디렉션을 수행 하는 경우 신뢰 당사자는 URL에 올바른 매개 변수를 지정 하지 않으면 요청을 사용 하 여 문제를 발생할 수 있습니다 것.


토큰 형식 확인 하려면, 웹 디버거 도구를 사용할 수 있습니다.


## <a name="token-response"></a>토큰 응답

## <a name="authentication"></a>인증

## <a name="claim-rule-processing"></a>클레임 규칙 처리