---
title: AD FS의 클라이언트 액세스 클레임 유형
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d73995b118ec41ffc892700858d20798f637d83b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857486"
---
# <a name="client-access-policy-claim-types-in-ad-fs"></a>AD FS의 클라이언트 액세스 정책 클레임 유형

추가 요청 컨텍스트 정보를 제공 하기 위해 클라이언트 액세스 정책은 요청 헤더 정보에서 처리할 AD FS 생성 하는 다음과 같은 클레임 유형을 사용 합니다.  자세한 내용은 [클레임 엔진의 역할](../technical-reference/the-role-of-the-claims-engine.md)을 참조 하세요.

## <a name="x-ms-forwarded-client-ip"></a>X-MS 전달-클라이언트-IP

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

이 AD FS 클레임은 요청을 수행 하는 사용자의 IP 주소 (예: Outlook 클라이언트)를 확인의 "최상의 시도"를 나타냅니다. 이 클레임은 요청을 전달한 모든 프록시의 주소를 포함 하 여 여러 IP 주소를 포함할 수 있습니다.  이 클레임은 현재 Exchange Online 에서만 설정 되는 HTTP 헤더에서 채워지며, AD FS에 인증 요청을 전달할 때 헤더를 채웁니다. 클레임의 값은 다음 중 하나일 수 있습니다.


- 단일 IP 주소-Exchange Online에 직접 연결 되는 클라이언트의 IP 주소

    >! 두고 회사 네트워크에 있는 클라이언트의 IP 주소는 조직의 아웃 바운드 프록시 또는 게이트웨이의 외부 인터페이스 IP 주소로 표시 됩니다.

- 하나 이상의 IP 주소
  - Exchange Online에서 연결 하는 클라이언트의 IP 주소를 확인할 수 없는 경우에는 HTTP 기반 요청에 포함할 수 있고 시장의 여러 클라이언트, 부하 분산 장치 및 프록시에서 지원 되는 비표준 헤더 인 x 전달-헤더의 값을 기반으로 값을 설정 합니다.
  - 클라이언트 IP 주소와 요청을 전달한 각 프록시의 주소를 나타내는 여러 IP 주소가 쉼표로 구분 됩니다.

    >! 두고 Exchange Online 인프라와 관련 된 IP 주소는 목록에 표시 되지 않습니다.


>! 내용의 Exchange Online은 현재 IPV4 주소만 지원 합니다. IPV6 주소는 지원 하지 않습니다. 


## <a name="x-ms-client-application"></a>X-y-클라이언트 응용 프로그램

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

이 AD FS 클레임은 사용 중인 응용 프로그램에 느슨하게 해당 하는 최종 클라이언트에서 사용 하는 프로토콜을 나타냅니다.  이 클레임은 현재 Exchange Online 에서만 설정 되는 HTTP 헤더에서 채워지며, AD FS에 인증 요청을 전달할 때 헤더를 채웁니다. 응용 프로그램에 따라이 클레임의 값은 다음 중 하나가 됩니다.



- Exchange Active Sync를 사용 하는 장치의 경우 값은 Microsoft. Exchange. 
- Microsoft Outlook 클라이언트를 사용 하면 다음 값 중 하나가 발생할 수 있습니다.
    - Microsoft에서 자동 검색
    - OfflineAddressBook
    - Microsoft. Exchange. RPC
    - WebServices
    - Microsoft Exchange. Mapi
- 이 헤더에 사용할 수 있는 다른 값은 다음과 같습니다.
    - Microsoft. Exchange Powershell
    - Microsoft Exchange. SMTP
    - PopImap
    - Microsoft Exchange Pop
    - Microsoft Exchange. Imap

## <a name="x-ms-client-user-agent"></a>X-y-사용자-에이전트

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

이 AD FS 클레임은 클라이언트에서 서비스에 액세스 하는 데 사용 하는 장치 유형을 나타내는 문자열을 제공 합니다. 고객이 특정 유형의 스마트폰 등 특정 장치에 대 한 액세스를 차단 하려는 경우에 사용할 수 있습니다.  이 클레임은 현재 Exchange Online 에서만 설정 되는 HTTP 헤더에서 채워지며, AD FS에 인증 요청을 전달할 때 헤더를 채웁니다. 이 클레임에 대 한 값 예에는 아래 값이 포함 됩니다 (이에 국한 되지 않음).
>! 두고 다음은 x-m s-응용 프로그램이 "Microsoft. s s. m s. m s. m s s" 인 클라이언트에 대해 x-y (사용자 에이전트) 값이 포함 될 수 있는 예입니다.

- 소용돌이/1.0
- IPad1C1/812.1
- IPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>! 두고 이 값이 비어 있을 수도 있습니다.


## <a name="x-ms-proxy"></a>X-MS 프록시

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

이 AD FS 클레임은 요청이 페더레이션 서버 프록시를 통해 전달 되었음을 나타냅니다.  이 클레임은 페더레이션 서비스 백 엔드에 인증 요청을 전달할 때 헤더를 채우는 페더레이션 서버 프록시로 채워집니다. 그런 다음 AD FS 클레임으로 변환 합니다. 

클레임의 값은 요청을 전달한 페더레이션 서버 프록시의 DNS 이름입니다.

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-y-절대 경로 (활성 vs 수동)

클레임 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

이 클레임 유형은 "active" (리치) 클라이언트와 "passive" (웹 브라우저 기반) 클라이언트에서 시작 되는 요청을 확인 하는 데 사용할 수 있습니다. 이렇게 하면 Microsoft Outlook과 같은 리치 클라이언트에서 들어오는 요청이 차단 되는 동안 Outlook 웹 액세스, SharePoint Online 또는 Office 365 포털과 같은 브라우저 기반 응용 프로그램의 외부 요청이 허용 됩니다.

클레임의 값은 요청을 받은 AD FS 서비스의 이름입니다.
