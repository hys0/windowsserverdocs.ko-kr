---
title: AD FS 문제 해결-Fiddler
description: 이 문서에서는 AD FS의 WS-FEDERATION 교환에 대 한 심층 추적을 보여 줍니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d263f48aadff7c77cba44a2328d472ebbe5dfbbf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407213"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>AD FS 문제 해결-Fiddler
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>1 단계 및 2 단계
이는 추적의 시작입니다.  이 프레임에는 다음이 표시 됩니다. ![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

요구

- 신뢰 당사자에 대 한 HTTP GET (http://sql1.contoso.com/SampApp)

응답이

- 응답은 HTTP 302 (리디렉션)입니다.  응답 헤더의 전송 데이터는를 리디렉션할 위치 (https://sts.contoso.com/adfs/ls) )를 표시 합니다.
- 리디렉션 URL에는 RP 응용 프로그램에서 WS 페더레이션 로그인 요청을 작성 하 고이를 AD FS의/adfs/ls/끝점으로 전송 했음을 알리는 wa = wsignin 1.0이 포함 되어 있습니다.  이를 리디렉션 바인딩 이라고 합니다.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>3 단계 및 4 단계

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

요구

- AD FS 서버에 대 한 HTTP GET (sts. .com)

응답이

- 응답은 자격 증명을 묻는 메시지입니다.  이는 폼 인증을 사용 중임을 나타냅니다.
- 응답의 웹 보기를 클릭 하 여 자격 증명 프롬프트를 볼 수 있습니다.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>5 단계와 6 단계

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

요구

- 사용자 이름 및 암호를 사용 하는 HTTP POST입니다.  
- 자격 증명을 제공 합니다.  요청의 원시 데이터를 살펴보면 자격 증명을 볼 수 있습니다.

응답이

- 응답이 발견 되 고 MSIAuth 암호화 된 쿠키가 생성 되어 반환 됩니다.  클라이언트에서 생성 한 SAML 어설션의 유효성을 검사 하는 데 사용 됩니다.  이를 "인증 쿠키" 라고도 하며 AD FS Idp 경우에만 제공 됩니다.


## <a name="step-7-and-8"></a>7 단계와 8 단계
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

요구

- 이제 인증을 했으므로 AD FS 서버에 다른 HTTP GET을 수행 하 고 인증 토큰을 제공 합니다.

응답이

- 응답은 제공 된 자격 증명을 기반으로 AD FS 사용자를 인증 했음을 의미 하는 HTTP OK입니다.
- 또한 3 개의 쿠키를 다시 클라이언트로 설정 합니다.
    - MSISAuthenticated에는 클라이언트가 인증 된 시간에 대 한 b a s e 64로 인코딩된 타임 스탬프 값이 포함 됩니다.
    - MSISLoopDetectionCookie는 무한 리디렉션 루프에서 페더레이션 서버로 종료 된 클라이언트를 중지 하기 위해 AD FS 무한 루프 검색 메커니즘에 사용 됩니다. 쿠키 데이터는 b a s e 64로 인코딩된 타임 스탬프입니다.
    - MSISSignout는 SSO 세션을 위해 방문한 IdP 및 모든 RPs를 추적 하는 데 사용 됩니다. 이 쿠키는 WS-FEDERATION 로그 아웃을 호출할 때 활용 됩니다. Base64 디코더를 사용 하 여이 쿠키의 내용을 볼 수 있습니다.
    
## <a name="step-9-and-10"></a>9 단계와 10 단계
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png) 요청:

- HTTP POST

응답이

- 응답이 발견 되었습니다.

## <a name="step-11-and-12"></a>11 단계 및 12 단계
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png) 요청:

- HTTP GET

응답이

- 응답이 양호 합니다.

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)