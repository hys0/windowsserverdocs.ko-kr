---
title: 연결 요청 정책
description: 이 항목에서는 Windows Server 2016의 네트워크 정책 서버 연결 요청 정책에 대 한 개요를 제공 합니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 4ec45e0c-6b37-4dfb-8158-5f40677b0157
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 021cef4a220b183f6580bca75bc6db68aba893cf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316234"
---
# <a name="connection-request-policies"></a>연결 요청 정책

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 nps 연결 요청 정책을 사용 하 여 NPS를 RADIUS 서버, RADIUS 프록시 또는 둘 다로 구성 하는 방법을 배울 수 있습니다.

>[!NOTE]
>이 항목 외에 다음 연결 요청 정책 설명서를 사용할 수 있습니다.
> - [연결 요청 정책 구성](nps-crp-configure.md)
> - [원격 RADIUS 서버 그룹 구성](nps-crp-rrsg-configure.md)

연결 요청 정책은 네트워크 관리자가 연결 요청에 대 한 인증 및 권한 부여를 수행 하는 RADIUS(Remote Authentication Dial-In User Service) (RADIUS) 서버를 지정 하는 데 사용할 수 있는 조건 및 설정 집합입니다. NPS (네트워크 정책 서버)를 실행 하는 서버가 RADIUS 클라이언트에서 수신 합니다. RADIUS 계정에 사용 되는 RADIUS 서버를 지정 하도록 연결 요청 정책을 구성할 수 있습니다.

RADIUS 클라이언트에서 전송 된 일부 RADIUS 요청 메시지가 로컬로 처리 되 고 (NPS가 RADIUS 서버로 사용 됨) 다른 유형의 메시지가 다른 RADIUS 서버에 전달 되도록 연결 요청 정책을 만들 수 있습니다 (NPS는 RADIUS 프록시로 사용 됨).

연결 요청 정책을 사용 하면 다음과 같은 요소에 따라 NPS를 RADIUS 서버로 사용 하거나 RADIUS 프록시로 사용할 수 있습니다. 

- 요일 및 요일
- 연결 요청의 영역 이름입니다.
- 요청 된 연결의 유형입니다.
- RADIUS 클라이언트의 IP 주소입니다.

RADIUS 액세스-들어오는 메시지의 설정이 NPS에 구성 된 연결 요청 정책 중 하나 이상과 일치 하는 경우에만 NPS에서 요청 메시지를 처리 하거나 전달 합니다. 

정책 설정이 일치 하 고 정책에서 NPS가 메시지를 처리 해야 하는 경우 NPS는 RADIUS 서버 역할을 하며 연결 요청을 인증 하 고 권한을 부여 합니다. 정책 설정이 일치 하 고 정책에서 NPS가 메시지를 전달 해야 하는 경우 NPS는 RADIUS 프록시로 작동 하 고 처리를 위해 원격 RADIUS 서버에 연결 요청을 전달 합니다.

들어오는 RADIUS 액세스 요청 메시지의 설정이 하나 이상의 연결 요청 정책에 일치 하지 않으면 액세스 거부 메시지가 RADIUS 클라이언트로 전송 되 고 네트워크에 연결 하려는 사용자 또는 컴퓨터의 액세스가 거부 됩니다.

## <a name="configuration-examples"></a>구성 예

다음 구성 예제에서는 연결 요청 정책을 사용 하는 방법을 보여 줍니다.

### <a name="nps-as-a-radius-server"></a>RADIUS 서버로 작동하는 NPS

기본 연결 요청 정책은 유일 하 게 구성 된 정책입니다. 이 예에서 NPS는 RADIUS 서버로 구성 되며 모든 연결 요청은 로컬 NPS에 의해 처리 됩니다. NPS는 계정이 NPS 도메인 및 트러스트 된 도메인의 도메인에 있는 사용자를 인증 하 고 권한을 부여할 수 있습니다.


### <a name="nps-as-a-radius-proxy"></a>RADIUS 프록시로 작동하는 NPS

기본 연결 요청 정책이 삭제 되 고 두 개의 서로 다른 도메인에 요청을 전달 하기 위해 두 개의 새 연결 요청 정책이 생성 됩니다. 이 예제에서 NPS는 RADIUS 프록시로 구성 됩니다. NPS는 로컬 서버에서 연결 요청을 처리 하지 않습니다. 대신, 원격 RADIUS 서버 그룹의 구성원으로 구성 된 NPS 또는 다른 RADIUS 서버에 대 한 연결 요청을 전달 합니다.


### <a name="nps-as-both-radius-server-and-radius-proxy"></a>RADIUS 서버와 RADIUS 프록시로 모두 NPS

기본 연결 요청 정책 외에도, 트러스트 되지 않은 도메인의 NPS 또는 다른 RADIUS 서버에 대 한 연결 요청을 전달 하는 새 연결 요청 정책이 만들어집니다. 이 예제에서는 정책에 대 한 순서가 지정 된 목록에 프록시 정책이 먼저 표시 됩니다. 연결 요청이 프록시 정책과 일치 하는 경우 연결 요청은 원격 RADIUS 서버 그룹의 RADIUS 서버로 전달 됩니다. 연결 요청이 프록시 정책과 일치 하지 않지만 기본 연결 요청 정책과 일치 하는 경우 NPS는 로컬 서버에서 연결 요청을 처리 합니다. 연결 요청이 두 정책과 일치 하지 않으면 삭제 됩니다.

### <a name="nps-as-radius-server-with-remote-accounting-servers"></a>원격 계정 서버를 사용 하는 RADIUS 서버로 서의 NPS

이 예에서 로컬 NPS는 계정을 수행 하도록 구성 되지 않으며, RADIUS 계정 메시지가 원격 RADIUS 서버 그룹의 NPS 또는 다른 RADIUS 서버에 전달 되도록 기본 연결 요청 정책이 수정 됩니다. 계정 메시지가 전달 되는 경우에도 인증 및 권한 부여 메시지가 전달 되지 않고 로컬 NPS는 로컬 도메인 및 모든 트러스트 된 도메인에 대해 이러한 기능을 수행 합니다.


### <a name="nps-with-remote-radius-to-windows-user-mapping"></a>원격 RADIUS를 사용 하 여 Windows 사용자 매핑 NPS

이 예제에서 NPS는 인증 요청을 원격 RADIUS 서버에 전달 하는 동시에 권한 부여에 대 한 로컬 Windows 사용자 계정을 사용 하 여 각 개별 연결 요청에 대 한 radius 프록시로 RADIUS 서버 역할을 합니다. 이 구성은 연결 요청 정책의 조건으로 원격 RADIUS에서 Windows 사용자 매핑 특성을 구성 하 여 구현 합니다. 또한 원격 RADIUS 서버에서 인증을 수행 하는 원격 사용자 계정과 동일한 이름을 가진 사용자 계정을 로컬에서 만들어야 합니다.

## <a name="connection-request-policy-conditions"></a>연결 요청 정책 조건

연결 요청 정책 조건은 들어오는 RADIUS 액세스 요청 메시지의 특성과 비교한 하나 이상의 RADIUS 특성입니다. 여러 조건이 있는 경우 NPS에서 정책을 적용 하려면 연결 요청 메시지 및 연결 요청 정책의 모든 조건이 일치 해야 합니다.


다음은 연결 요청 정책에서 구성할 수 있는 사용 가능한 조건 특성입니다.

### <a name="connection-properties-attribute-group"></a>연결 속성 특성 그룹

연결 속성 특성 그룹에는 다음과 같은 특성이 포함 되어 있습니다.

- **프레임 프로토콜**. 들어오는 패킷에 대 한 프레이밍 유형을 지정 하는 데 사용 됩니다. 예를 들면 PPP (지점 간 프로토콜), SLIP (Serial Line Internet Protocol), 프레임 릴레이 및 X. 25가 있습니다.
- **서비스 유형**입니다. 요청 되는 서비스의 유형을 지정 하는 데 사용 됩니다. 예를 들면 예를 들어, 예를 들어, 예를 들어, 예를 들어, 예를 들어, 예를 들면 RADIUS 서비스 유형에 대 한 자세한 내용은 RFC 2865, "원격 인증 전화 접속 사용자 서비스 (RADIUS)"를 참조 하십시오.
- **터널 유형**입니다. 요청 클라이언트에 의해 생성 되는 터널의 유형을 지정 하는 데 사용 됩니다. 터널 유형에는 PPTP (지점 간 터널링 프로토콜) 및 l2tp(계층 2 터널링 프로토콜 (L2TP)이 포함 됩니다.

### <a name="day-and-time-restrictions-attribute-group"></a>날짜 및 시간 제한 특성 그룹 

날짜 및 시간 제한 특성 그룹에는 날짜 및 시간 제한 특성이 포함 됩니다. 이 특성을 사용 하 여 요일을 지정 하 고 연결 시도 시간을 지정할 수 있습니다. 날짜 및 시간은 NPS의 날짜 및 시간을 기준으로 합니다.

### <a name="gateway-attribute-group"></a>게이트웨이 특성 그룹

게이트웨이 특성 그룹에는 다음 특성이 포함 됩니다.

- **스테이션 ID 라고**합니다. 네트워크 액세스 서버의 전화 번호를 지정 하는 데 사용 됩니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 영역 코드를 지정할 수 있습니다.
- **NAS 식별자**입니다. 네트워크 액세스 서버 이름을 지정 하는 데 사용 됩니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 NAS 식별자를 지정할 수 있습니다.
- **NAS IPv4 주소**입니다. 네트워크 액세스 서버 (RADIUS 클라이언트)의 IPv4 (인터넷 프로토콜 버전 4) 주소를 지정 하는 데 사용 됩니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 IP 네트워크를 지정할 수 있습니다.
- **NAS IPv6 주소**입니다. 네트워크 액세스 서버 (RADIUS 클라이언트)의 IPv6 (인터넷 프로토콜 버전 6) 주소를 지정 하는 데 사용 됩니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 IP 네트워크를 지정할 수 있습니다.
- **NAS 포트 유형**입니다. Access 클라이언트에서 사용 하는 미디어 유형을 지정 하는 데 사용 됩니다. 예를 들면, 아날로그 전화선 (비동기), ISDN (Integrated Services Digital Network), 터널 또는 Vpn (가상 사설망), IEEE 802.11 무선 및 이더넷 스위치가 있습니다.

### <a name="machine-identity-attribute-group"></a>컴퓨터 Id 특성 그룹

컴퓨터 Id 특성 그룹은 컴퓨터 Id 특성을 포함 합니다. 이 특성을 사용 하 여 정책에서 클라이언트를 식별 하는 방법을 지정할 수 있습니다.

### <a name="radius-client-properties-attribute-group"></a>RADIUS 클라이언트 속성 특성 그룹

RADIUS 클라이언트 속성 특성 그룹에는 다음과 같은 특성이 포함 되어 있습니다.

- **호출 스테이션 ID**입니다. 호출자가 사용 하는 전화 번호를 지정 하는 데 사용 됩니다 (액세스 클라이언트). 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 영역 코드를 지정할 수 있습니다.  802.1 x 인증에서 MAC 주소는 일반적으로 채워지고 클라이언트와 일치할 수 있습니다.  이 필드는 일반적으로 ' 자격 증명의 유효성을 검사 하지 않고 사용자 수락 '에 대해 연결 요청 정책이 구성 된 경우 Mac 주소 무시 시나리오에 사용 됩니다.  
- **클라이언트 이름**입니다. 인증을 요청 하는 RADIUS 클라이언트 컴퓨터의 이름을 지정 하는 데 사용 됩니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 클라이언트 이름을 지정할 수 있습니다.
- **클라이언트 IPv4 주소**입니다. 네트워크 액세스 서버 (RADIUS 클라이언트)의 IPv4 주소를 지정 하는 데 사용 됩니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 IP 네트워크를 지정할 수 있습니다.
- **클라이언트 IPv6 주소**입니다. 네트워크 액세스 서버 (RADIUS 클라이언트)의 IPv6 주소를 지정 하는 데 사용 됩니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용 하 여 IP 네트워크를 지정할 수 있습니다.
- **클라이언트 공급 업체**. 인증을 요청 하는 네트워크 액세스 서버의 공급 업체를 지정 하는 데 사용 됩니다. 라우팅 및 원격 액세스 서비스를 실행 하는 컴퓨터는 Microsoft NAS 제조업체입니다. 이 특성을 사용 하 여 서로 다른 NAS 제조업체에 대 한 별도의 정책을 구성할 수 있습니다. 이 특성은 문자열입니다. 패턴 일치 구문을 사용할 수 있습니다.

### <a name="user-name-attribute-group"></a>사용자 이름 특성 그룹

사용자 이름 특성 그룹은 사용자 이름 특성을 포함 합니다. 이 특성을 사용 하 여 RADIUS 메시지에서 access 클라이언트에서 제공한 사용자 이름과 일치 해야 하는 사용자 이름 또는 사용자 이름 부분을 지정할 수 있습니다. 이 특성은 일반적으로 영역 이름 및 사용자 계정 이름을 포함 하는 문자열입니다. 패턴 일치 구문을 사용 하 여 사용자 이름을 지정할 수 있습니다.

## <a name="connection-request-policy-settings"></a>연결 요청 정책 설정

연결 요청 정책 설정은 들어오는 RADIUS 메시지에 적용 되는 속성 집합입니다. 설정은 다음 속성 그룹으로 구성 됩니다.

- 인증
- 계정
- 특성 조작
- 요청 전달
- 고급

다음 섹션에서는 이러한 설정에 대 한 추가 세부 정보를 제공 합니다.

### <a name="authentication"></a>인증

이 설정을 사용 하면 모든 네트워크 정책에 구성 된 인증 설정을 재정의할 수 있으며 네트워크에 연결 하는 데 필요한 인증 방법과 유형을 지정할 수 있습니다.

>[!IMPORTANT]
>네트워크 정책에서 구성 하는 인증 방법 보다 보안 수준이 낮은 연결 요청 정책에서 인증 방법을 구성 하는 경우 네트워크 정책에서 구성 하는 보다 안전한 인증 방법이 재정의 됩니다. 예를 들면 보안 된 확장 가능 인증 프로토콜을 사용 해야 하는 네트워크 정책 (Microsoft 챌린지 핸드셰이크 인증 프로토콜 버전 2 \(PEAP-CHAP v2\)(보안 무선에 대 한 암호 기반 인증 방법)을 사용 하는 경우 인증 되지 않은 액세스를 허용 하도록 연결 요청 정책을 구성할 수도 있습니다. 그러면 PEAP-CHAP v2를 사용 하 여 인증 해야 하는 클라이언트가 없습니다. 이 예제에서 네트워크에 연결 하는 모든 클라이언트에는 인증 되지 않은 액세스 권한이 부여 됩니다.

### <a name="accounting"></a>계정

이 설정을 사용 하 여 원격 radius 서버 그룹에서 계정 정보를 NPS 또는 다른 RADIUS 서버에 전달 하도록 연결 요청 정책을 구성할 수 있습니다.

>[!NOTE]
>여러 RADIUS 서버가 있고 하나의 중앙 RADIUS 계정 데이터베이스에 저장 된 모든 서버에 대 한 계정 정보를 원하는 경우 각 RADIUS 서버에서 정책에 있는 연결 요청 정책 계정 설정을 사용 하 여 계정 데이터를 전달할 수 있습니다. 단일 NPS 또는 계정 서버로 지정 된 다른 RADIUS 서버에 대 한 모든 서버.

연결 요청 정책 계정 설정은 로컬 NPS의 계정 구성에 독립적으로 작동 합니다. 즉, 로컬 파일 또는 Microsoft SQL Server 데이터베이스에 대 한 RADIUS 계정 정보를 기록 하도록 로컬 NPS를 구성 하는 경우, 원격 RADIUS에 계정 메시지를 전달 하도록 연결 요청 정책을 구성 하는지 여부에 관계 없이이 작업을 수행 합니다. 서버 그룹.

계정 정보를 원격으로 기록 하 고 로컬로 기록 하지 않으려는 경우에는 계정을 수행 하지 않도록 로컬 NPS를 구성 하 고, 원격 RADIUS 서버 그룹에 계정 데이터를 전달 하는 연결 요청 정책에도 계정을 구성 해야 합니다.

### <a name="attribute-manipulation"></a>특성 조작

다음 특성 중 하나의 텍스트 문자열을 조작 하는 찾기 및 바꾸기 규칙 집합을 구성할 수 있습니다.

- 사용자 이름
- 호출 스테이션 ID
- 호출 스테이션 ID

찾기 및 바꾸기 규칙 처리는 RADIUS 메시지가 인증 및 계정 설정에 적용 되기 전에 앞의 특성 중 하나에 대해 발생 합니다. 특성 조작 규칙은 단일 특성에만 적용 됩니다. 각 특성에 대 한 특성 조작 규칙을 구성할 수 없습니다. 또한 조작할 수 있는 특성의 목록은 정적 목록입니다. 조작에 사용할 수 있는 특성 목록에 추가할 수 없습니다.

>[!NOTE]
>MS-CHAP v2 인증 프로토콜을 사용 하는 경우 연결 요청 정책이 RADIUS 메시지를 전달 하는 데 사용 되는 경우 사용자 이름 특성을 조작할 수 없습니다. 백슬래시 (\) 문자를 사용 하 고 조작은 왼쪽에 있는 정보에만 영향을 주는 경우에만 예외가 발생 합니다. 백슬래시 문자는 일반적으로 도메인 이름 (백슬래시 문자 왼쪽에 있는 정보) 및 도메인 내 사용자 계정 이름 (백슬래시 문자 오른쪽에 있는 정보)을 나타내는 데 사용 됩니다. 이 경우 도메인 이름을 수정 하거나 대체 하는 특성 조작 규칙만 허용 됩니다.

사용자 이름 특성에서 영역 이름을 조작 하는 방법에 대 한 예제는 [NPS에서 정규식 사용](nps-crp-reg-expressions.md)항목의 "사용자 이름 특성에서 영역 이름을 조작 하는 방법" 섹션을 참조 하세요.

### <a name="forwarding-request"></a>요청 전달

RADIUS 액세스 요청 메시지에 사용 되는 다음 전달 요청 옵션을 설정할 수 있습니다.

- **이 서버에서 요청을 인증**합니다. 이 설정을 사용 하면 NPS는 Windows NT 4.0 도메인, Active Directory 또는 로컬 SAM (보안 계정 관리자) 사용자 계정 데이터베이스를 사용 하 여 연결 요청을 인증 합니다. 또한이 설정은 nps에서 구성 된 일치 하는 네트워크 정책을 사용자 계정의 전화 접속 속성과 함께 사용 하 여 연결 요청에 권한을 부여 하도록 지정 합니다. 이 경우 NPS는 RADIUS 서버로 수행 하도록 구성 됩니다.

- **다음 원격 RADIUS 서버 그룹에 요청을 전달**합니다. 이 설정을 사용 하면 NPS는 지정 된 원격 RADIUS 서버 그룹으로 연결 요청을 전달 합니다. NPS가 액세스 요청 메시지에 해당 하는 유효한 액세스 허용 메시지를 수신 하면 연결 시도가 인증 되 고 권한이 부여 된 것으로 간주 됩니다. 이 경우 NPS는 RADIUS 프록시로 작동 합니다.

- **자격 증명의 유효성을 검사 하지 않고 사용자를 수락**합니다. 이 설정을 사용 하면 NPS는 네트워크에 연결 하려는 사용자의 id를 확인 하지 않으며 NPS는 사용자 또는 컴퓨터에 네트워크에 연결할 수 있는 권한이 있는지 확인 하지 않습니다. NPS가 인증 되지 않은 액세스를 허용 하도록 구성 되 고 연결 요청을 수신 하는 경우 NPS는 액세스 허용 메시지를 RADIUS 클라이언트에 즉시 보내고 사용자 또는 컴퓨터에 네트워크 액세스 권한이 부여 됩니다. 이 설정은 사용자 자격 증명이 인증 되기 전에 액세스 클라이언트가 터널링 되는 일부 강제 터널링 유형에 사용 됩니다.

>[!NOTE]
>액세스 클라이언트의 인증 프로토콜이 MS-CHAP v2 또는 EAP-TLS (Extensible Authentication Protocol-Transport Layer Security) 인 경우이 인증 옵션을 사용할 수 없습니다. 둘 다 상호 인증을 제공 합니다. 상호 인증에서 액세스 클라이언트는 인증 서버 (NPS)에 대 한 유효한 액세스 클라이언트 임을 증명 하 고 인증 서버는 액세스 클라이언트에 대 한 유효한 인증 서버 임을 증명 합니다. 이 인증 옵션을 사용 하면 액세스 허용 메시지가 반환 됩니다. 그러나 인증 서버는 액세스 클라이언트에 대 한 유효성 검사를 제공 하지 않으며 상호 인증이 실패 합니다.

정규식을 사용 하 여 지정 된 영역 이름을 가진 RADIUS 메시지를 원격 RADIUS 서버 그룹으로 전달 하는 라우팅 규칙을 만드는 방법에 대 한 예제는 [NPS에서 정규식 사용](nps-crp-reg-expressions.md)항목의 "프록시 서버에서 radius 메시지 전달에 대 한 예제" 섹션을 참조 하세요.

### <a name="advanced"></a>고급

고급 속성을 설정 하 여 다음과 같은 일련의 RADIUS 특성을 지정할 수 있습니다.

- Radius 인증 또는 계정 서버로 NPS를 사용 하는 경우 RADIUS 응답 메시지에 추가 됩니다. 네트워크 정책 및 연결 요청 정책 모두에 특성이 지정 된 경우 RADIUS 응답 메시지에서 전송 되는 특성은 두 특성 집합의 조합입니다.
- Radius 인증 또는 계정 프록시로 NPS를 사용 하는 경우 RADIUS 메시지에 추가 됩니다. 전달 되는 메시지에 특성이 이미 있으면 연결 요청 정책에 지정 된 특성의 값으로 대체 됩니다. 

또한 **고급** 범주의 연결 요청 정책 **설정** 탭에서 구성에 사용할 수 있는 일부 특성은 특수 기능을 제공 합니다. 예를 들어 두 사용자 계정 데이터베이스 간의 연결 요청에 대 한 인증 및 권한 부여를 분할 하려는 경우 **원격 RADIUS에서 Windows 사용자 매핑 특성을** 구성할 수 있습니다.

**원격 radius에서 Windows 사용자 매핑** 특성은 원격 radius 서버에서 인증 된 사용자에 대해 windows 권한 부여를 수행 하도록 지정 합니다. 즉, 원격 RADIUS 서버는 원격 사용자 계정 데이터베이스의 사용자 계정에 대 한 인증을 수행 하지만 로컬 NPS는 로컬 사용자 계정 데이터베이스의 사용자 계정에 대 한 연결 요청에 권한을 부여 합니다. 이 방법은 방문자의 네트워크 액세스를 허용 하려는 경우에 유용 합니다.

예를 들어 파트너 조직의 방문자는 자신의 파트너 조직 RADIUS 서버에서 인증을 받은 다음 조직의 Windows 사용자 계정을 사용 하 여 네트워크의 게스트 LAN (local area network)에 액세스할 수 있습니다.

특수 기능을 제공 하는 다른 특성은 다음과 같습니다.

- **Ms 격리-IPFilter 및 ms-검역-시간 제한**입니다. 이러한 특성은 라우팅 및 원격 액세스 VPN 배포를 사용 하 여 NAQC (네트워크 액세스 격리 제어)를 배포할 때 사용 됩니다.
- **Passport-사용자-매핑-UPN-접미사** 이 특성을 사용 하면 Windows Live™ ID 사용자 계정 자격 증명을 사용 하 여 연결 요청을 인증할 수 있습니다.
- **터널 태그**. 이 특성은 Vlan (virtual local area network)을 배포할 때 NAS에서 연결을 할당 해야 하는 VLAN ID 번호를 지정 합니다.

## <a name="default-connection-request-policy"></a>기본 연결 요청 정책

기본 연결 요청 정책은 NPS를 설치할 때 만들어집니다. 이 정책에는 다음과 같은 구성이 있습니다.

- 인증이 구성 되지 않았습니다.
- 계정이 원격 RADIUS 서버 그룹에 계정 정보를 전달 하도록 구성 되어 있지 않습니다.
- 특성은 원격 RADIUS 서버 그룹에 대 한 연결 요청을 전달 하는 특성 조작 규칙으로 구성 되지 않습니다.
- 전달 요청은 로컬 NPS에서 연결 요청이 인증 되 고 권한이 부여 되도록 구성 됩니다.
- 고급 특성이 구성 되지 않았습니다.

기본 연결 요청 정책은 NPS를 RADIUS 서버로 사용 합니다. RADIUS 프록시로 작동 하도록 NPS를 실행 하는 서버를 구성 하려면 원격 RADIUS 서버 그룹도 구성 해야 합니다. 새 연결 요청 정책 마법사를 사용 하 여 새 연결 요청 정책을 만드는 동안 새 원격 RADIUS 서버 그룹을 만들 수 있습니다. 기본 연결 요청 정책을 삭제 하거나 기본 연결 요청 정책이 NPS에서 마지막으로 처리 한 정책 목록에 마지막으로 배치 하 여 해당 정책을 처리 하는지 확인할 수 있습니다.

>[!NOTE]
>NPS와 원격 액세스 서비스를 같은 컴퓨터에 설치 하 고 원격 액세스 서비스를 Windows 인증 및 계정으로 구성 하는 경우 원격 액세스 인증 및 계정 요청을 RADIUS 서버로 전달할 수 있습니다. . 원격 액세스 인증 및 계정 요청이 원격 RADIUS 서버 그룹에 전달 하도록 구성 된 연결 요청 정책과 일치 하는 경우이 문제가 발생할 수 있습니다.
