---
title: AD FS 문제 해결-클레임 발급
description: 이 문서에서는 AD FS에서 토큰 발급 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ea0e6112f00f9cace6a0c580661a5319b5adaea5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366245"
---
# <a name="ad-fs-troubleshooting---claims-issuance"></a>AD FS 문제 해결-클레임 발급
클레임은 한 주체가 자신 또는 다른 주체에 대해 수행 하는 문입니다.  클레임은 신뢰 당사자에 의해 발급 되며 하나 이상의 값이 지정 된 다음 AD FS 서버에서 발급 한 보안 토큰에 패키지 됩니다.  이 프로세스에는 몇 가지 이동 부분이 있으므로 클레임 발급을 이러한 주요 부분으로 나눌 수 있습니다.

>[!NOTE]  
>[ADFS 도움말](https://adfshelp.microsoft.com) 사이트의 [ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) 를 사용 하 여 클레임 문제 해결에 도움을 받을 수 있습니다.   

## <a name="token-request"></a>토큰 요청
신뢰 당사자로 이동 하는 경우 토큰 요청과 AD FS으로 리디렉션됩니다.  요청에서 문제가 발생할 수 있습니다.  가장 중요 한 점은 다음과 같습니다.

### <a name="the-request-formatting-with-3rd-parties-particularly-saml"></a>타사 (특히 SAML)를 사용한 요청 형식

### <a name="pre-formated-urls-that-have-typos"></a>오타가 있는 미리 포맷 된 Url
Federaion 신뢰 당사자 로부터 토큰을 발급 하는 경우 토큰 요청은 URL 쿼리 문자열 매개 변수와 함께 제공 됩니다.  AD FS 리디렉션할 때 신뢰 당사자가 해당 URL에 올바른 매개 변수를 지정 하지 않으면 요청에 문제가 발생할 수 있습니다.


토큰 형식을 verifiy 웹 디버거 도구를 사용할 수 있습니다.


## <a name="token-response"></a>토큰 응답

## <a name="authentication"></a>인증

## <a name="claim-rule-processing"></a>클레임 규칙 처리