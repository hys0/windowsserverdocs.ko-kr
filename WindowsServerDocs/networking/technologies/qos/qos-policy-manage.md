---
title: QoS 정책 관리
description: 이 항목에서는 Windows Server 2016에서 QoS (서비스 품질) 정책을 만들고 관리 하는 방법에 대 한 지침을 제공 합니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 04fdfa54-6600-43d4-8945-35f75e15275a
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 36c30372b6cac40b603658eca9636a265801fb1a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315447"
---
# <a name="manage-qos-policy"></a>QoS 정책 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

이 항목을 사용 하 여 qos 정책 마법사를 사용 하 여 QoS 정책을 생성, 편집 또는 삭제 하는 방법에 대해 알아볼 수 있습니다.

>[!NOTE]
>  이 항목 외에도 다음과 같은 QoS 정책 관리 설명서를 사용할 수 있습니다.
> 
>  - [QoS 정책 이벤트 및 오류](qos-policy-errors.md)

Windows 운영 체제에서 QoS 정책은 표준 기반 QoS의 기능을 그룹 정책의 관리 효율성과 결합 합니다. 이러한 조합을 구성 하면 QoS 정책을 그룹 정책 개체에 쉽게 적용할 수 있습니다. Windows에는 다음 작업을 수행 하는 데 도움이 되는 QoS 정책 마법사가 포함 되어 있습니다.

-  [QoS 정책 만들기](#bkmk_createpolicy)

-  [QoS 정책 보기, 편집 또는 삭제](#bkmk_editpolicy)

##  <a name="create-a-qos-policy"></a><a name="bkmk_createpolicy"></a>QoS 정책 만들기

QoS 정책을 만들기 전에 네트워크 트래픽을 관리 하는 데 사용 되는 두 가지 주요 QoS 제어를 이해 하는 것이 중요 합니다.

- DSCP 값

-   스로틀 률

### <a name="prioritizing-traffic-with-dscp"></a>DSCP를 사용 하 여 트래픽 우선 순위 우선 순위

이전 lob (기간 업무) 응용 프로그램 예제에서 설명한 것 처럼 **Dscp 값 지정** 을 사용 하 여 아웃 바운드 네트워크 트래픽의 우선 순위를 정의 하 여 특정 dscp 값으로 QoS 정책을 구성할 수 있습니다. 

RFC 2474에 설명 된 대로, DSCP는 IPv4 패킷의 TOS 필드와 i p v 6의 Traffic 클래스 필드 내에서 0에서 63 사이의 값을 지정할 수 있도록 허용 합니다. 네트워크 라우터는 DSCP 값을 사용 하 여 네트워크 패킷을 분류 하 고 적절 하 게 큐에 대기 합니다.
  
> [!NOTE]
>  기본적으로 Windows 트래픽의 DSCP 값은 0입니다.
  
큐의 개수 및 우선 순위 지정 동작은 사용자 조직이 갖춘 QoS 전략의 일환으로 정해져야 합니다. 예를 들어 조직에서 대기 시간이 중요 한 트래픽, 제어 트래픽, 업무상 중요 한 트래픽, 최상의 트래픽 및 대량 데이터 전송 트래픽 등 5 개의 큐를 갖도록 선택할 수 있습니다.  
  
### <a name="throttling-traffic"></a>트래픽 제한

DSCP 값과 함께 제한은 네트워크 대역폭을 관리 하는 또 다른 주요 컨트롤입니다. 앞에서 설명한 것 처럼 **제한 시간 지정** 설정을 사용 하 여 아웃 바운드 트래픽에 대 한 특정 스로틀 속도로 QoS 정책을 구성할 수 있습니다. QoS 정책은 제한을 사용 하 여 나가는 네트워크 트래픽을 지정 된 스로틀 속도로 제한 합니다. 트래픽을 효과적으로 관리하기 위해 DSCP 표시와 제한을 함께 사용할 수도 있습니다.

>[!NOTE]
>기본적으로 **스로틀 속도 지정** 확인란은 선택되어 있지 않습니다.

QoS 정책을 만들려면 GPMC (그룹 정책 관리 콘솔) 도구 내에서 GPO (그룹 정책 개체)의 설정을 편집 합니다. 그러면 GPMC가 그룹 정책 개체 편집기를 엽니다.

QoS 정책에는 고유한 이름을 지정해야 합니다. 서버 및 최종 사용자에 게 정책을 적용 하는 방법은 그룹 정책 개체 편집기에 QoS 정책이 저장 되는 위치에 따라 달라 집니다.

- 컴퓨터 구성 \ Settings\QoS 정책의 QoS 정책은 현재 로그온 한 사용자에 관계 없이 컴퓨터에 적용 됩니다. 일반적으로 서버 컴퓨터에는 컴퓨터 기반 QoS 정책을 사용합니다.

- 사용자 구성 Settings\QoS 정책의 QoS 정책은 로그온 한 후에 사용자가 로그온 한 컴퓨터에 관계 없이 사용자에 게 적용 됩니다.

#### <a name="to-create-a-new-qos-policy-with-the-qos-policy-wizard"></a>QoS 정책 마법사를 사용 하 여 새 QoS 정책을 만들려면

-   그룹 정책 개체 편집기에서 **QoS 정책** 노드 중 하나를 마우스 오른쪽 단추로 클릭 한 다음 **새 정책 만들기**를 클릭 합니다.

### <a name="wizard-page-1---policy-profile"></a>마법사 페이지 1-정책 프로필

QoS 정책 마법사의 첫 번째 페이지에서 정책 이름을 지정 하 고 QoS가 나가는 네트워크 트래픽을 제어 하는 방법을 구성할 수 있습니다.

#### <a name="to-configure-the-policy-profile-page-of-the-qos-based-policy-wizard"></a>QoS 기반 정책 마법사의 정책 프로필 페이지를 구성하려면

1. **정책 이름**에 QoS 정책의 이름을 입력합니다. 이름은 정책을 고유 하 게 식별 해야 합니다.

2. 필요에 따라 dscp **값 지정** 을 사용 하 여 dscp 표시를 사용 하도록 설정 하 고 0에서 63 사이의 dscp 값을 구성 합니다.

3. 선택적으로 트래픽 제한을 사용하고 스로틀 속도를 구성하는 데 **스로틀 속도 지정**을 사용할 수 있습니다. 스로틀 속도 값은 1 보다 커야 하며 초당 킬로바이트 단위 \(KBps\) 또는 초당 메가바이트\)\(지정할 수 있습니다.

4. **다음**을 클릭합니다.

### <a name="wizard-page-2---application-name"></a>마법사 페이지 2-응용 프로그램 이름

QoS 정책 마법사의 두 번째 페이지에서 모든 응용 프로그램, 실행 파일 이름으로 식별 되는 특정 응용 프로그램, 경로 및 응용 프로그램 이름 또는 특정 URL에 대 한 요청을 처리 하는 HTTP 서버 응용 프로그램에 정책을 적용할 수 있습니다.

- **모든 응용 프로그램** 은 QoS 정책 마법사의 첫 번째 페이지에 있는 트래픽 관리 설정이 모든 응용 프로그램에 적용 되도록 지정 합니다.

- **이 실행 파일 이름이 있는 응용 프로그램만** QoS 정책 마법사의 첫 번째 페이지에 있는 트래픽 관리 설정이 특정 응용 프로그램에 대 한 것 임을 지정 합니다. 실행 파일 이름은 .exe 파일 이름 확장명으로 끝나야 합니다.

- **이 URL에 대 한 요청에 응답 하는 http 서버 응용** 프로그램만 QoS 정책 마법사의 첫 번째 페이지에 있는 트래픽 관리 설정이 특정 HTTP 서버 응용 프로그램에만 적용 되도록 지정 합니다.

선택적으로 애플리케이션의 경로를 입력할 수 있습니다. 애플리케이션 경로를 지정하려면 경로에 애플리케이션 이름을 포함하십시오. 경로에는 환경 변수가 포함 될 수 있습니다. 경로는 예를 들어 %ProgramFiles%\My Application Path\MyApp.exe나 c:\program files\my application path\myapp.exe가 될 수 있습니다.

>[!NOTE]
>응용 프로그램 경로에는 기호화 된 링크로 확인 되는 경로를 포함할 수 없습니다.

URL은 `http[s]://<hostname\>:<port\>/<url-path>`형식의 [RFC 1738](https://tools.ietf.org/html/rfc1738)을 준수 해야 합니다. `‘*'`와일드 카드, `<hostname>` 및/또는 `<port>`(예: `https://training.\*/, https://\*.\*`)를 사용할 수 있지만 와일드 카드는 `<hostname>` 또는 `<port>`의 부분 문자열을 나타낼 수 없습니다.

즉, `https://my\*site/`와 `https://\*training\*/` 모두 유효 하지 않습니다. 

필요에 따라 **하위 디렉터리 및 파일 포함** 을 선택 하 여 URL 뒤의 모든 하위 디렉터리 및 파일에 대해 일치를 수행할 수 있습니다. 예를 들어이 옵션을 선택 하 고 URL을 `https://training`하는 경우 QoS 정책은 적절 한 일치 항목` https://training/video` 대 한 요청을 고려 합니다.

#### <a name="to-configure-the-application-name-page-of-the-qos-policy-wizard"></a>QoS 정책 마법사의 응용 프로그램 이름 페이지를 구성 하려면

1. **이 QoS 정책이 적용**되는 대상에서 **모든 응용 프로그램** 을 선택 하거나 **이 실행 파일 이름이 있는 응용 프로그램만**을 선택 합니다.

2. **이 실행 파일 이름이 있는 응용 프로그램만**을 선택한다면 .exe 파일 이름 확장명으로 끝나는 실행 파일 이름을 지정합니다.

3. **다음**을 클릭합니다.

### <a name="wizard-page-3---ip-addresses"></a>마법사 페이지 3-IP 주소

QoS 정책 마법사의 세 번째 페이지에서 다음을 포함 하 여 QoS 정책에 대 한 IP 주소 조건을 지정할 수 있습니다.

- 모든 원본 IPv4 또는 IPv6 주소나 특정 원본 IPv4 또는 IPv6 주소

- 모든 대상 IPv4 또는 IPv6 주소 또는 특정 대상 IPv4 또는 IPv6 주소

**다음 원본 IP 주소에만** 또는 **다음 대상 IP 주소에만**을 선택하면 다음 중 한 항목을 입력해야 합니다.

- `192.168.1.1`와 같은 IPv4 주소

- 네트워크 접두사 길이 표기법을 사용 하는 IPv4 주소 접두사 (예: `192.168.1.0/24`

- IPv6 주소 (예: `3ffe:ffff::1`

- IPv6 주소 접두사 (예: `3ffe:ffff::/48`

다음 **원본 ip 주소에 대해서만** 둘 다를 선택 하 고 **다음 대상 ip 주소에**대해서만 선택 하는 경우 주소 또는 주소 접두사는 모두 IPv4 또는 IPv6 기반 이어야 합니다.

이전 마법사 페이지에서 HTTP 서버 응용 프로그램에 대 한 URL을 지정한 경우이 마법사 페이지의 QoS 정책에 대 한 원본 IP 주소가 회색으로 표시 됩니다. 

원본 IP 주소는 HTTP 서버 주소 이며 여기서 구성할 수 없기 때문입니다. 반면에 대상 IP 주소를 지정 하 여 정책을 사용자 지정할 수 있습니다. 이렇게 하면 동일한 HTTP 서버 응용 프로그램을 사용 하 여 다른 클라이언트에 대해 다른 정책을 만들 수 있습니다.

#### <a name="to-configure-the-ip-addresses-page-of-the-qos-policy-wizard"></a>QoS 정책 마법사의 IP 주소 페이지를 구성 하려면

1. **이 QoS 정책이 적용 되** 는 대상 (원본)에서 **모든 원본 ip 주소** 또는 **다음 Ip 원본 주소에 대해서만**을 선택 합니다.

2. **다음 IP 원본 주소만**선택한 경우 IPv4 또는 IPv6 주소 또는 접두사를 지정 합니다.

3. **이 QoS 정책이 적용 되** 는 대상 (대상)에서 **모든 대상 주소** 또는 **다음 IP 대상 주소에 대해서만을 선택 합니다.**

4. **다음 IP 대상 주소만**을 선택한 경우 원본 주소에 지정 된 주소 또는 접두사 유형에 해당 하는 IPv4 또는 IPv6 주소 또는 접두사를 지정 합니다.

5.  **다음**을 클릭합니다.  

### <a name="wizard-page-4---protocols-and-ports"></a>마법사 페이지 4-프로토콜 및 포트

QoS 정책 마법사의 네 번째 페이지에서 마법사의 첫 번째 페이지에 있는 설정에 의해 제어 되는 트래픽 유형 및 포트를 지정할 수 있습니다. 다음과 같이 지정할 수 있습니다.  
-   TCP 트래픽이나 UDP 트래픽(또는 둘 다)  

-   모든 원본 포트, 원본 포트의 범위, 특정 원본 포트

-   모든 대상 포트, 대상 포트 범위 또는 특정 대상 포트  

#### <a name="to-configure-the-protocols-and-ports-page-of-the-qos-policy-wizard"></a>QoS 정책 마법사의 프로토콜 및 포트 페이지를 구성 하려면

1. **이 QoS 정책이 적용되는 프로토콜 선택**에서 **TCP**, **UDP** 또는 **TCP 및 UDP**를 선택합니다.

2. **원본 포트 번호 지정**에서 **모든 원본 포트부터** 또는 **이 원본 포트 번호부터**를 선택합니다.

3. **이 원본 포트 번호에서**선택한 경우 1에서 65535 사이의 포트 번호를 입력 합니다.

     필요에 따라 포트 범위를 "*low*:*High*" 형식으로 지정할 수 있습니다. 여기서 *Low* 및 *High* 는 포트 범위의 하 한과 상한을 나타냅니다. *Low* 및 *High* 는 각각 1에서 65535 사이의 숫자 여야 합니다. 콜론 (:) 문자와 숫자 사이에는 공백이 없어야 합니다.

4. **대상 포트 번호 지정**에서 **모든 대상 포트까지** 또는 **이 대상 포트 번호까지**를 선택합니다.

5. 이전 단계에서 **이 대상 포트 번호부터**를 선택한 경우 1에서 65535 사이의 숫자를 써서 포트 번호를 입력합니다.

새 QoS 정책 만들기를 완료 하려면 QoS 정책 마법사의 **프로토콜 및 포트** 페이지에서 **마침** 을 클릭 합니다. 완료 되 면 새 QoS 정책이 그룹 정책 개체 편집기의 세부 정보 창에 나열 됩니다.  
  
사용자 또는 컴퓨터에 QoS 정책 설정을 적용 하려면 QoS 정책이 있는 GPO를 도메인, 사이트 또는 OU (조직 구성 단위)와 같은 Active Directory Domain Services 컨테이너에 연결 합니다.  
  
##  <a name="view-edit-or-delete-a-qos-policy"></a><a name="bkmk_editpolicy"></a>QoS 정책 보기, 편집 또는 삭제

위에 설명 된 QoS 정책 마법사 페이지는 정책의 속성을 보거나 편집할 때 표시 되는 속성 페이지에 해당 합니다.  
  
### <a name="to-view-the-properties-of-a-qos-policy"></a>QoS 정책의 속성을 보려면  
  
-   그룹 정책 개체 편집기의 세부 정보 창에서 정책 이름을 마우스 오른쪽 단추로 클릭 한 다음 **속성**을 클릭 합니다.  
  
     그룹 정책 개체 편집기에 다음 탭이 포함 된 속성 페이지가 표시 됩니다.  
  
    -   정책 프로필  
  
    -   Application Name  
  
    -   IP 주소  
  
    -   프로토콜 및 포트  
  
### <a name="to-edit-a-qos-policy"></a>QoS 정책을 편집하려면  
  
-   그룹 정책 개체 편집기의 세부 정보 창에서 정책 이름을 마우스 오른쪽 단추로 클릭 한 다음 **기존 정책 편집**을 클릭 합니다.  
  
     그룹 정책 개체 편집기는 **기존 QoS 정책 편집** 대화 상자를 표시 합니다.  
  
### <a name="to-delete-a-qos-policy"></a>QoS 정책을 삭제하려면  
  
-   그룹 정책 개체 편집기의 세부 정보 창에서 정책 이름을 마우스 오른쪽 단추로 클릭 하 고 **정책 삭제**를 클릭 합니다.  
  
### <a name="qos-policy-gpmc-reporting"></a>QoS 정책 GPMC 보고 

조직 전체에 여러 QoS 정책을 적용 한 후에는 정책이 적용 되는 방식을 정기적으로 검토 하는 것이 유용 하거나 필요할 수 있습니다. GPMC 보고를 사용 하 여 특정 사용자 또는 컴퓨터에 대 한 QoS 정책의 요약을 볼 수 있습니다.  
  
#### <a name="to-run-the-group-policy-results-wizard-for-a-report-of-qos-policies"></a>QoS 정책 보고서에 대해 그룹 정책 결과 마법사를 실행 하려면  
  
-   GPMC에서 **그룹 정책 결과** 노드를 마우스 오른쪽 단추로 클릭 한 다음 **그룹 정책 결과 마법사** 의 메뉴 옵션을 선택 합니다.  
  
그룹 정책 결과가 생성 되 면 **설정** 탭을 클릭 합니다. **설정** 탭에서 QoS 정책은 "컴퓨터 구성 \ Settings\QoS 정책" 및 "사용자 구성 Settings\QoS 정책" 노드에서 찾을 수 있습니다.  
  
**설정** 탭의 qos 정책 이름에 해당 하는 qos 정책 이름에 해당 하는 DSCP 값, 제한 율, 정책 조건 및 적용 된 GPO는 동일한 행에 나열 됩니다.  
  
그룹 정책 결과 보기는 적용 된 GPO를 고유 하 게 식별 합니다. 여러 Gpo에 동일한 QoS 정책 이름을 가진 QoS 정책이 있는 경우 GPO 우선 순위가 가장 높은 GPO가 적용 됩니다. 이 GPO는 우위에 있는 GPO입니다. 낮은 우선 순위 GPO에 연결 된 충돌 하는 QoS 정책 (정책 이름으로 식별 됨)은 적용 되지 않습니다. 참고 GPO 우선 순위는 사이트, 도메인 또는 OU에 배포 되는 QoS 정책을 적절 하 게 정의 합니다. 배포 후에는 사용자 또는 컴퓨터 수준에서 [QoS 정책 우선 순위 규칙](#BKMK_precedencerules) 에 따라 허용 및 차단 되는 트래픽이 결정 됩니다.  
  
QoS 정책의 DSCP 값, 스로틀 율 및 정책 조건도 그룹 정책 개체 편집기 (GPOE)에서 볼 수 있습니다.  
  
### <a name="advanced-settings-for-roaming-and-remote-users"></a>로밍 및 원격 사용자에 대 한 고급 설정  
QoS 정책을 사용 하는 목적은 기업의 네트워크에서 트래픽을 관리 하는 것입니다. 모바일 시나리오에서 사용자는 엔터프라이즈 네트워크에서 트래픽을 보내거나 받을 수 있습니다. QoS 정책은 기업 네트워크와는 관련이 없지만, Windows 8, Windows 7 또는 Windows Vista 용 엔터프라이즈에 연결 된 네트워크 인터페이스 에서만 QoS 정책을 사용할 수 있습니다.  
  
예를 들어 사용자가 커피숍에서 VPN (가상 사설망)을 통해 휴대용 컴퓨터를 기업 네트워크에 연결할 수 있습니다. VPN의 경우 실제 네트워크 인터페이스 (예: 무선)에 QoS 정책이 적용 되지 않습니다. 그러나 VPN 인터페이스는 엔터프라이즈에 연결 하기 때문에 QoS 정책을 적용 합니다. 사용자가 나중에 AD DS 트러스트 관계가 없는 다른 엔터프라이즈 네트워크에 들어가면 QoS 정책을 사용 하지 않습니다.  
  
이러한 모바일 시나리오는 서버 워크 로드에는 적용 되지 않습니다. 예를 들어 여러 네트워크 어댑터가 있는 서버는 엔터프라이즈 네트워크의에 지에 있을 수 있습니다. IT 부서는 QoS 정책에서 엔터프라이즈를 egresses 하는 트래픽을 제한 하도록 선택할 수 있습니다. 그러나이 송신 트래픽을 보내는이 네트워크 어댑터는 엔터프라이즈 네트워크에 다시 연결 되지 않을 수도 있습니다. 이러한 이유로 QoS 정책은 Windows Server 2012를 실행 하는 컴퓨터의 모든 네트워크 인터페이스에서 항상 사용 하도록 설정 됩니다.  
  
> [!NOTE]
>  선택적 적용은이 문서의 다음에 설명 된 고급 QoS 설정이 아니라 QoS 정책에만 적용 됩니다.  
  
### <a name="advanced-qos-settings"></a>고급 QoS 설정

고급 QoS 설정은 IT 관리자가 컴퓨터 네트워크 사용량과 DSCP 표시를 관리할 수 있는 추가 제어 기능을 제공 합니다. 고급 QoS 설정은 컴퓨터 수준 에서만 적용 되는 반면 QoS 정책은 컴퓨터 수준과 사용자 수준 모두에서 적용 될 수 있습니다.

#### <a name="to-configure-advanced-qos-settings"></a>Advanced QoS 설정을 구성 하려면

1.  **컴퓨터 구성**을 클릭 한 다음 **그룹 정책에서 Windows 설정**을 클릭 합니다.
  
2.  **QoS 정책**을 마우스 오른쪽 단추로 클릭 한 다음 **고급 qos 설정**을 클릭 합니다.

     다음 그림은 **인바운드 TCP 트래픽** 및 **DSCP 표시 재정의**의 두 가지 고급 QoS 설정 탭을 보여 줍니다.
  
> [!NOTE]
>  고급 QoS 설정은 컴퓨터 수준 그룹 정책 설정입니다.
  
#### <a name="advanced-qos-settings-inbound-tcp-traffic"></a>고급 QoS 설정: 인바운드 TCP 트래픽

**인바운드 Tcp 트래픽은** 수신자 측에서 TCP 대역폭 소비를 제어 하지만 QoS 정책은 아웃 바운드 TCP 및 UDP 트래픽에 영향을 줍니다. 

**인바운드 Tcp 트래픽** 탭에서 더 낮은 처리량 수준을 설정 하면 tcp는 보급 된 tcp 수신 기간의 크기를 제한 합니다. 이 설정의 효과는 더 높은 대역폭 또는 대기 시간 (대역폭 지연 제품)이 있는 TCP 연결의 처리량 속도 및 링크 사용률을 증가 시킵니다. 기본적으로 Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터는 최대 처리량 수준으로 설정 됩니다.
  
Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 및 Windows Vista 이전 버전의 windows에서 TCP 수신 창이 변경 되었습니다. 이전 버전의 Windows에서는 TCP 수신 측 기간이 최대 64 킬로바이트 (KB)로 제한 되는 반면, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 및 Windows Vista에서는 자동으로 수신 측 창의 크기를 최대 16mb (MB)로 제한 합니다. ). 인바운드 TCP 트래픽 제어에서 TCP 수신 창이 증가할 수 있는 최대값을 설정 하 여 인바운드 처리량 수준을 제어할 수 있습니다. 수준은 다음 최대값에 해당 합니다. 
  
|인바운드 처리량 수준|최대값|  
|------------------------|-------|  
|0|64KB|
|1|256KB|
|2|1MB|
|3|16mb|

실제 창 크기는 네트워크 상태에 따라 최대값 보다 작거나 같은 값일 수 있습니다.

###### <a name="to-set-the-tcp-receive-side-window"></a>TCP 수신 측 창을 설정 하려면

1. 그룹 정책 개체 편집기에서 **로컬 컴퓨터 정책**, **Windows 설정**을 차례로 클릭 하 고 **qos 정책**을 마우스 오른쪽 단추로 클릭 한 다음 **고급 QoS 설정**을 클릭 합니다.
  
2. **Tcp 수신 처리량**에서 **Tcp 수신 처리량 구성**을 선택한 다음 원하는 처리량 수준을 선택 합니다.

3.  OU에 GPO를 연결 합니다.

#### <a name="advanced-qos-settings-dscp-marking-override"></a>고급 QoS 설정: DSCP 표시 재정의

DSCP 표시 재정의는 응용 프로그램의 기능을 지정 하 여 QoS 정책에 지정 된 것과 다른 DSCP 값을 지정 하거나 "표시" 합니다. 응용 프로그램에서 DSCP 값을 설정할 수 있도록 지정 하면 0이 아닌 DSCP 값을 설정할 수 있습니다. 

**무시**를 지정 하 여 qos api를 사용 하는 응용 프로그램은 dscp 값을 0으로 설정 하 고 QOS 정책만 dscp 값을 설정할 수 있습니다. 

기본적으로 Windows Server 2016, windows 10, windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 및 Windows Vista를 실행 하는 컴퓨터는 응용 프로그램에서 DSCP 값을 지정할 수 있습니다. QoS Api를 사용 하지 않는 응용 프로그램 및 장치는 재정의 되지 않습니다.

##### <a name="wireless-multimedia-and-dscp-values"></a>무선 멀티미디어 및 DSCP 값

Wi-fi [동맹](https://go.microsoft.com/fwlink/?LinkId=160769) 은 wi-fi 무선 네트워크에서 전송 되는 네트워크 트래픽의 우선 순위를 정하는\) WMM_AC \(4 개의 액세스 범주를 정의 하는 무선 멀티미디어\) \(에 대 한 인증을 설정 했습니다.\- 액세스 범주에는 음성, 비디오, 최상의 작업 및 배경\)의 가장 높은 우선 순위에 \(포함 됩니다. 각각 .VO.MSECND.NET, VI, be 및 BK으로 축약 됩니다. WMM 사양은 네 가지 액세스 범주 각각에 해당 하는 DSCP 값을 정의 합니다.
  
|DSCP 값|WMM 액세스 범주|
|----------|-------------------|
|48-63|음성 (.VO.MSECND.NET)|
|32-47|비디오 (VI)|
|24-31, 0-7|최고 노력|
|8-23|배경 (BK)|

이러한 DSCP 값을 사용 하는 QoS 정책을 만들 수 있습니다. 이러한 DSCP 값을 사용 하는 휴대용 컴퓨터에 대 한 wi-fi 인증을 사용 하는\-에 대 한 wi-fi 인증 된\-™에 대 한 wi-fi 인증
  
### <a name="qos-policy-precedence-rules"></a><a name="BKMK_precedencerules"></a>QoS 정책 우선 순위 규칙

GPO의 우선 순위와 마찬가지로 QoS 정책에는 여러 QoS 정책이 특정 트래픽 집합에 적용 될 때 충돌을 해결 하기 위한 선행 규칙이 있습니다. 아웃 바운드 TCP 또는 UDP 트래픽의 경우 한 번에 하나의 QoS 정책만 적용할 수 있습니다. 즉, 제한 비율을 합산 하는 등의 QoS 정책에는 누적 효과가 없습니다.

일반적으로 가장 일치 하는 조건을 가진 QoS 정책이 적용 됩니다. 여러 QoS 정책이 적용 되는 경우 규칙은 세 가지 범주인 사용자 수준 및 컴퓨터 수준으로 분류 됩니다. application 및 network 5 중; 네트워크 5 중 사이에 있습니다.

*Network 5 중*는 원본 ip 주소, 대상 ip 주소, 원본 포트, 대상 포트 및 프로토콜 \(TCP/UDP\)를 의미 합니다.  

 **사용자 수준 QoS 정책이 컴퓨터 수준 QoS 정책 보다 우선 적용 됩니다.**

이 규칙은 특히 사용자 그룹 기반 정책에 대 한 QoS Gpo의 네트워크 관리자 관리를 용이 하 게 합니다. 예를 들어 네트워크 관리자가 사용자 그룹에 대 한 QoS 정책을 정의 하려는 경우 GPO를 만들어 해당 그룹에 배포할 수 있습니다. 사용자가 로그온 한 컴퓨터 및 해당 컴퓨터에 충돌 하는 QoS 정책이 정의 되어 있는지 걱정 하지 않아도 됩니다. 충돌이 있는 경우 사용자 수준 정책이 항상 우선 적용 되기 때문입니다.

> [!NOTE]
>  사용자 수준 QoS 정책은 해당 사용자가 생성 하는 트래픽에만 적용 됩니다. 특정 컴퓨터의 다른 사용자와 컴퓨터 자체에는 해당 사용자에 대해 정의 된 QoS 정책이 적용 되지 않습니다.

 **Application 특이성 및 network 5 중 보다 우선 합니다.**

여러 QoS 정책이 특정 트래픽과 일치 하는 경우 보다 구체적인 정책이 적용 됩니다. 응용 프로그램을 식별 하는 정책 중에서 보내는 응용 프로그램의 파일 경로를 포함 하는 정책은 응용 프로그램 이름 (경로 없음)만 식별 하는 다른 정책 보다 특정 한 것으로 간주 됩니다. 응용 프로그램을 포함 하는 여러 정책이 여전히 적용 되는 경우 우선 순위 규칙은 network 5 중를 사용 하 여 가장 일치 하는 항목을 찾습니다.

또는 겹치지 않는 조건을 지정 하 여 여러 QoS 정책이 동일한 트래픽에 적용 될 수 있습니다. 응용 프로그램의 조건과 network 5 중 사이에 응용 프로그램을 지정 하는 정책이 보다 구체적으로 간주 되어 적용 됩니다. 

예를 들어 policy_A는 응용 프로그램 이름 (app.config)만 지정 하 고 policy_B은 대상 IP 주소 192.168.1.0/24를 지정 합니다. 이러한 QoS 정책이 충돌 하면 192.168.4.0/24\)범위 내에 있는 IP 주소에 트래픽을 전송 \(policy_A 적용 됩니다.

 **네트워크 5 중 내에서 더 많은 특이성가 우선적으로 적용 됩니다.**

Network 5 중 내의 정책 충돌에 대해 가장 일치 하는 조건이 적용 되는 정책이 우선적으로 적용 됩니다. 예를 들어 policy_C는 원본 IP 주소 "any", 대상 IP 주소 10.0.0.1, 원본 포트 "any", 대상 포트 "any" 및 프로토콜 "TCP"를 지정 하는 것으로 가정 합니다. 

다음으로 policy_D 원본 IP 주소 "any", 대상 IP 주소 10.0.0.1, 원본 포트 "any", 대상 포트 80 및 프로토콜 "TCP"를 지정 합니다. 그런 다음 policy_C 및 policy_D 대상 10.0.0.1:80과 일치 하는지 확인 합니다. QoS 정책은 가장 구체적인 일치 조건으로 정책을 적용 하기 때문에 policy_D는이 예제에서 우선적으로 적용 됩니다.  
  
그러나 QoS 정책에는 동일한 수의 조건이 있을 수 있습니다. 예를 들어, 여러 정책은 각각 네트워크 5 중 하나 (동일 하지는 않음)를 지정할 수 있습니다. 네트워크 5 중 사이에서 다음 순서는 높은 우선 순위에서 낮은 우선 순위입니다.

- 원본 IP 주소

- 대상 IP 주소

- 원본 포트

- 대상 포트

- 프로토콜(TCP 또는 UDP)

IP 주소와 같은 특정 조건 내에서 보다 구체적인 IP 주소는 더 높은 우선 순위로 처리 됩니다. 예를 들어 IP 주소 192.168.4.1은 192.168.4.0/24 보다 더 구체적입니다.

적용 되는 정책을 이해 하는 조직의 기능을 간소화 하기 위해 가능한 한 QoS 정책을 설계 합니다.

이 가이드의 다음 항목에 대해서는 [QoS 정책 이벤트 및 오류](qos-policy-errors.md)를 참조 하세요.

이 가이드의 첫 번째 항목은 [QoS (서비스 품질) 정책](qos-policy-top.md)을 참조 하세요.
