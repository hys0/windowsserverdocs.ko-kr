---
title: AD FS-Fiddler-WS-페더레이션 문제 해결
description: 이 문서에서는 AD FS 사용 하 여 Ws-federation 교환의 자세한 추적을 보여 줍니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: be1c9f466ec13272d10f0fb9ca31cf326a1ec29a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846904"
---
# <a name="ad-fs-troubleshooting---fiddler---ws-federation"></a>AD FS-Fiddler-WS-페더레이션 문제 해결
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler9.png)

## <a name="step-1-and-2"></a>1 단계와 2
이 추적의 시작입니다.  이 프레임에서 다음을 참조 했습니다. ![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler1.png)

요청:

- 이 신뢰 당사자 (HTTP GET http://sql1.contoso.com/SampApp)

응답:

- 응답은 HTTP 302 (리디렉션).  응답 헤더에 전송 데이터 (리디렉션하는 위치를 보여 줍니다. https://sts.contoso.com/adfs/ls)
- Wa를 포함 하는 리디렉션 URL = wsignin 1.0 RP 응용 프로그램에 Ws-federation 로그인 요청을 작성 있고 AD FS의 /adfs/ls 끝점으로 전송 하는이 사용자에 게 알려줍니다.  바인딩 리디렉션로 알려져 있습니다.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler2.png)

## <a name="step-3-and-4"></a>3-4 단계

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler3.png)

요청:

- 이 AD FS server(sts.contoso.com)에 HTTP GET

응답:

- 응답은 자격 증명을 확인 합니다.  Forms authnetication 사용 한다고 나타냅니다.
- 응답의 WebView를 클릭 하 여 메시지를 표시 하는 자격 증명을 확인할 수 있습니다.
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler6.png)

## <a name="step-5-and-6"></a>5와 6 단계

![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler4.png)

요청:

- 사용자 이름 및 암호 사용 하 여 HTTP POST입니다.  
- 에서는 자격 증명을 제공합니다.  요청에 원시 데이터를 확인 하 여 자격 증명을 확인할 수 있습니다.

응답:

- 응답에는 발견 하 고 암호화 된 쿠키가 만들어져 반환 MSIAuth입니다.  클라이언트에서 생성 된 SAML 어설션의 유효성을 검사 하는이 사용 됩니다.  "인증 쿠키가"이 라고도 하 고만 AD FS Idp 때 표시 됩니다.


## <a name="step-7-and-8"></a>7 및 8 단계
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler5.png)

요청:

- 에서는 인증 했으므로 AD FS 서버에 다른 HTTP GET을 수행 하 고 인증 토큰을 제공

응답:

- 응답은 AD FS에서 제공 된 자격 증명에 따라 사용자를 인증 하는 HTTP OK
- 또한 클라이언트에 다시 3 쿠키를 설정
    - MSISAuthenticated는 클라이언트를 인증 하는 경우에 대 한 base64로 인코딩된 타임 스탬프 값을 포함 합니다.
    - MSISLoopDetectionCookie 중지 클라이언트에서 페더레이션 서버에는 무한 리디렉션 루프 종료 하는 AD FS 무한 루프 검색 메커니즘이 사용 됩니다. 쿠키 데이터가 base64로 인코딩된 타임 스탬프입니다.
    - MSISSignout IdP를 추적 하는 모든 RPs에 SSO 세션에 대 한 방문을 이 쿠키는 Ws-federation 로그 아웃 호출 될 때 사용 됩니다. Base64 디코더를 사용 하 여이 쿠키의 내용을 볼 수 있습니다.
    
## <a name="step-9-and-10"></a>단계 9 및 10
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler7.png) 요청:

- HTTP POST

응답:

- 응답은를 찾았습니다.

## <a name="step-11-and-12"></a>11 및 12 단계
![](media/ad-fs-tshoot-fiddler-ws-fed/fiddler8.png) 요청:

- HTTP GET

응답:

- 응답은 확인

## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)