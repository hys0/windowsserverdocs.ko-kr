---
ms.assetid: 
title: "클레임 ADFS 유형에 대 한 클라이언트 액세스"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1e37aded450555d293806d1ed8903a51e3df9424
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
#<a name="client-access-policy-claim-types-in-ad-fs"></a>클라이언트 액세스 정책 클레임 adfs 유형

추가 요청 컨텍스트 정보를 제공 하기 위해 클라이언트 액세스 정책을 ADFS 처리 하기 위해 요청 머리글 정보에서 생성 다음 청구 유형, 사용 합니다.  자세한 내용은 참조 [클레임 엔진 역할](../technical-reference/the-role-of-the-claims-engine.md)합니다.

##<a name="x-ms-forwarded-client-ip"></a>X MS-전달-클라이언트-IP

클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`

이 ADFS 클레임 요청 (예: Outlook 클라이언트) 사용자의 IP 주소를 구축 방향을 얻기 위한에서 "좋은 시도를"를 나타냅니다. 이 청구 요청을 전달 하는 모든 프록시의 주소를 포함 하 여 여러 개의 IP 주소를 포함 될 수 있습니다.  현재 있는 HTTP 머리글에서이 클레임 채워집니다만 Exchange Online을 인증 요청 Adfs에 전달 하는 경우 헤더를 채웁니다 하 여 설정 합니다. 클레임 값 다음 중 하나 될 수 있습니다.


- 하나 IP 주소-Exchange Online에 직접 연결 하는 클라이언트의 IP 주소

    >! [노트] 회사 네트워크에 대 한 클라이언트의 IP 주소 조직의 아웃 바운드 프록시 또는 게이트웨이 외부 인터페이스 IP 주소가 표시 됩니다.

- 하나 이상의 IP 주소
    - Exchange Online을 확인할 수 없는 연결 클라이언트의 IP 주소 HTTP 기반에 포함 될 수 있는 비 표준 헤더 요청 하 고 여러 클라이언트, 부하 분산와 프록시 시장에 지 원하는 x-전달 기능에 대 한 헤더 값에 따라 값이 설정 합니다.
    - 클라이언트 IP 주소와 요청 전달 하는 각 프록시의 주소가 표시 여러 IP 주소가 쉼표로 구분 됩니다.

    >! [노트] Exchange Online 인프라와 관련 된 IP 주소 목록에 표시 되지 않습니다.


>! [경고] Exchange Online IPV4 주소;만 현재 지원 IPV6 주소를 지원 하지 않습니다. 


## <a name="x-ms-client-application"></a>MS 클라이언트 응용 X

클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`

이 ADFS 클레임 느슨하게 사용 중인 응용 프로그램에 해당 하는 최종 클라이언트를 사용 하는 프로토콜을 나타냅니다.  현재 있는 HTTP 머리글에서이 클레임 채워집니다만 Exchange Online을 인증 요청 Adfs에 전달 하는 경우 헤더를 채웁니다 하 여 설정 합니다. 응용 프로그램에 따라 다음 중 하나를 값이이 청구 됩니다.



- Exchange Activesync 사용 하는 디바이스의 경우 값 Microsoft.Exchange.ActiveSync입니다. 
- Microsoft Outlook 클라이언트를 사용 하 여 다음 값 발생할 수 있습니다.
    - Microsoft.Exchange.Autodiscover
    - Microsoft.Exchange.OfflineAddressBook
    - Microsoft.Exchange.RPC
    - Microsoft.Exchange.WebServices
    - Microsoft.Exchange.Mapi
- 이 헤더에 대 한 기타 가능한 값은 다음과 같습니다.
    - Microsoft.Exchange.Powershell
    - Microsoft.Exchange.SMTP
    - Microsoft.Exchange.PopImap
    - Microsoft.Exchange.Pop
    - Microsoft.Exchange.Imap

## <a name="x-ms-client-user-agent"></a>X-MS-클라이언트-사용자 에이전트

클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`

이 ADFS 클레임 장치 종류 서비스에 액세스할 때 사용 하는 클라이언트를 표시 하는 문자열을 제공 합니다. 고객이 특정 장치 (예: 특정 유형의 스마트폰)에 액세스 하지 못하도록 하려는 경우 사용할 수 있습니다.  현재 있는 HTTP 머리글에서이 클레임 채워집니다만 Exchange Online을 인증 요청 Adfs에 전달 하는 경우 헤더를 채웁니다 하 여 설정 합니다. 포함 (하지만에 제한 되지는 않습니다)이이 클레임에 대 한 값 예제 아래 값 합니다.
>! [노트] 아래은 해당 x-ms-클라이언트 응용 프로그램은 "Microsoft.Exchange.ActiveSync" 클라이언트에 대 한 포함 될 수 ms 사용자 에이전트 x 값 가지

- 소용돌이/1.0
- Apple-iPad1C1/812.1
- Apple-iPhone3C1/811.2
- Apple-iPhone/704.11
- Moto-DROID2/4.5.1
- SAMSUNGSPHD700/100.202
- Android/0.3

>! [노트] 이 값은 비어 가능한 이기도 합니다.


## <a name="x-ms-proxy"></a>X MS 프록시

클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`

이 ADFS 클레임 요청 federation 서버 프록시 통해 전달 된 것을 나타냅니다.  이 청구 인증 요청 백 엔드 Federation 서비스를 전달 하는 경우 헤더를 채웁니다는 federation 프록시 서버 채워집니다. ADFS 다음 변환 클레임 합니다. 

클레임 값 요청 전달 federation 서버 프록시 DNS 이름입니다.

## <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-끝점-절대 경로 (활성와 수동)

클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`

이와 같은 클레임 (웹 브라우저 기반) 클라이언트가 "수동"와 "활성" (풍부한) 클라이언트의 요청을 확인 하는 데 사용할 수 있습니다. 이 통해 외부 Outlook 웹 액세스, SharePoint Online 또는 Office 365 포털 풍부한 클라이언트 Microsoft Outlook 등의 요청 차단 된 동안 허용 등의 응용 프로그램 브라우저 기반 요청 합니다.

클레임 값 요청을 받은 ADFS 서비스의 이름입니다.
