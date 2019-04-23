---
ms.assetid: ''
title: 클라이언트 액세스에서에서 클레임 유형은 AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e37aded450555d293806d1ed8903a51e3df9424
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839144"
---
#<a name="client-access-policy-claim-types-in-ad-fs"></a>클라이언트 액세스 정책에서에서 클레임 유형은 AD FS

추가 요청 컨텍스트 정보를 제공 하려면 클라이언트 액세스 정책 처리에 대 한 요청 헤더 정보에서 AD FS를 생성 하는 다음 클레임 유형을 사용 합니다.  자세한 내용은 참조 [클레임 엔진의 역할](../technical-reference/the-role-of-the-claims-engine.md)입니다.

##<a name="x-ms-forwarded-client-ip"></a>X-MS-전달-클라이언트-IP

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

이 AD FS 클레임에서 요청을 만드는 사용자 (예: Outlook 클라이언트)의 IP 주소를 부분도 "최상의 시도를"를 나타냅니다. 이 클레임 요청을 전달 하는 모든 프록시의 주소를 포함 하 여 여러 IP 주소를 포함할 수 있습니다.  현재 HTTP 헤더에서이 클레임 채워집니다만 설정한 Exchange Online을 AD fs 인증 요청을 전달 하는 경우 헤더를 채웁니다. 클레임의 값 중 하나일 수 있습니다.


- 단일 IP 주소-Exchange Online에 직접 연결 된 클라이언트의 IP 주소

    >! [참고] 회사 네트워크에서 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.

- 하나 이상의 IP 주소
    - Exchange Online는 연결 중인 클라이언트의 IP 주소를 확인할 수 없으면, HTTP 기반에 포함 될 수 있는 비표준 헤더를 요청 하 고 많은 클라이언트, 부하 분산 장치에서 지원 되는 x-전달 기능에 대 한 헤더의 값에 따라 값을 설정 하 고 시장에서 프록시를 제공 합니다.
    - 클라이언트 IP 주소 및 요청을 전달 하는 각 프록시 주소를 나타내는 여러 IP 주소를 쉼표로 구분 됩니다.

    >! [참고] Exchange Online 인프라와 관련 된 IP 주소 목록에 표시 되지 않습니다.


>! [경고] Exchange Online만 IPV4 주소는 현재 지원 IPV6 주소를 지원 하지 않습니다. 


## <a name="x-ms-client-application"></a>X-MS-Client-Application

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

이 AD FS 클레임 느슨하게 사용 중인 응용 프로그램에 해당 하는 최종 클라이언트에 의해 사용 된 프로토콜을 나타냅니다.  현재 HTTP 헤더에서이 클레임 채워집니다만 설정한 Exchange Online을 AD fs 인증 요청을 전달 하는 경우 헤더를 채웁니다. 응용 프로그램에 따라이 클레임의 값 중 하나로 설정 됩니다.



- Exchange Active Sync를 사용 하는 장치의 경우 Microsoft.Exchange.ActiveSync 가치가 있습니다. 
- 다음 값 중 하나에서 Microsoft Outlook 클라이언트 사용 될 수 있습니다.
    - Microsoft.Exchange.Autodiscover
    - Microsoft.Exchange.OfflineAddressBook
    - Microsoft.Exchange.RPC
    - Microsoft.Exchange.WebServices
    - Microsoft.Exchange.Mapi
- 이 헤더에 대 한 다른 가능한 값은 다음과 같습니다.
    - Microsoft.Exchange.Powershell
    - Microsoft.Exchange.SMTP
    - Microsoft.Exchange.PopImap
    - Microsoft.Exchange.Pop
    - Microsoft.Exchange.Imap

## <a name="x-ms-client-user-agent"></a>X-MS-Client-User-Agent

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

이 AD FS 클레임에는 클라이언트는 서비스에 액세스 하는 데 사용 하는 장치 유형을 나타내는 문자열을 제공 합니다. 이 고객은 특정 장치 (예: 스마트폰의 특정 유형)에 대 한 액세스를 방지 하려는 경우 사용할 수 있습니다.  현재 HTTP 헤더에서이 클레임 채워집니다만 설정한 Exchange Online을 AD fs 인증 요청을 전달 하는 경우 헤더를 채웁니다. 포함 (하지만에 제한 되지 않습니다)이이 클레임에 대 한 예제 값 아래의 값입니다.
>! [참고] 다음은 x ms-사용자 에이전트 값을 해당 x-ms-클라이언트 응용 프로그램은 "Microsoft.Exchange.ActiveSync" 클라이언트에 대 한 포함 될 수 있습니다의 예

- 소용돌이/1.0
- Apple-iPad1C1/812.1
- Apple-iPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>! [참고] 이 값은 비워 둘 수 이기도 합니다.


## <a name="x-ms-proxy"></a>X-MS-Proxy

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

이 AD FS 클레임 요청에 페더레이션 서버 프록시를 통해 전달 되는 것을 나타냅니다.  이 클레임은 페더레이션 서비스를 백 엔드로 인증 요청을 전달 하는 경우 헤더를 채우는 페더레이션 서버 프록시에 의해 채워집니다. AD FS이 클레임을 다음 변환합니다. 

클레임의 값에는 요청을 전달한 페더레이션 서버 프록시의 DNS 이름입니다.

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-끝점-절대 경로 (활성 및 수동)

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

이 클레임 유형이 "수동" (웹 브라우저 기반) 클라이언트와 "활성" (진한) 클라이언트에서 시작 된 요청을 결정 하는 데 사용할 수 있습니다. 따라서 Outlook Web Access, SharePoint Online 또는 Office 365 포털에서 Microsoft Outlook 등의 다양 한 클라이언트에서 보내는 요청을 차단 하는 동안 수와 같은 브라우저 기반 응용 프로그램에서 외부 요청을 수 있습니다.

클레임의 값에는 요청을 수신 하는 AD FS 서비스의 이름입니다.
