---
title: 인증 정책 및 인증 정책 사일로
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-credential-protection
ms.topic: article
ms.assetid: 7eb0e640-033d-49b5-ab44-3959395ad567
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 48171657b42ec8b6ba09aa6a35a2f898d6775d07
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857086"
---
# <a name="authentication-policies-and-authentication-policy-silos"></a>인증 정책 및 인증 정책 사일로

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한 이 항목에서는 인증 정책 사일로 및 해당 사일로로 계정을 제한할 수 있는 정책에 대해 설명합니다. 또한 인증 정책을 사용하여 계정 범위를 제한하는 방법에 대해 설명합니다.

인증 정책 사일로 및 이와 함께 적용되는 정책에서는 선택한 사용자, 컴퓨터 또는 서비스와만 관련된 높은 권한의 자격 증명을 시스템에 포함할 수 있는 방법을 제공합니다. Active Directory 관리 센터 및 Active Directory Windows PowerShell cmdlet을 사용하여 AD DS(Active Directory 도메인 서비스)에서 사일로를 정의하고 관리할 수 있습니다.

인증 정책 사일로는 관리자가 사용자 계정, 컴퓨터 계정 및 서비스 계정을 할당할 수 있는 컨테이너입니다. 그런 다음 해당 컨테이너에 적용된 인증 정책을 통해 계정 집합을 관리할 수 있습니다. 이는 관리자가 개별 계정에 대해 리소스 액세스를 추적할 필요성을 줄이고, 악의적인 사용자가 자격 증명 도난을 통해 다른 리소스에 액세스하는 것을 방지하도록 도와줍니다.

Windows Server 2012 r 2에 도입 된 기능을 통해 높은 권한의 사용자 집합을 호스트 하는 인증 정책 사일로를 만들 수 있습니다. 그런 다음 이 컨테이너에 대해 도메인에서 권한 있는 계정을 사용할 수 있는 위치를 제한하는 인증 정책을 할당할 수 있습니다. 계정이 보호된 사용자 보안 그룹에 속한 경우 Kerberos 프로토콜 단독 사용과 같은 추가 제어가 적용됩니다.

이러한 기능을 사용하면 우선 순위가 높은 계정 사용을 우선 순위가 높은 호스트로 제한할 수 있습니다. 예를 들어, 엔터프라이즈, 스키마 및 도메인 관리자가 포함된 새 포리스트 관리자 사일로를 만들 수 있습니다. 그런 다음 도메인 컨트롤러 및 도메인 관리자 콘솔 이외의 시스템에서 시도하는 암호 및 스마트 카드 기반 인증이 실패하도록 인증 정책으로 사일로를 구성할 수 있습니다.

인증 정책 사일로 및 인증 정책 구성에 대한 자세한 내용은 [보호된 계정을 구성하는 방법](how-to-configure-protected-accounts.md)을 참조하세요.

### <a name="about-authentication-policy-silos"></a>인증 정책 사일로 정보
인증 정책 사일로는 사일로로 제한할 수 있는 계정을 제어하며, 구성원에 적용할 인증 정책을 정의합니다. 조직의 요구 사항에 따라 사일로를 만들 수 있습니다. 사일로는 다음 표에서 스키마로 정의된 사용자, 컴퓨터 및 서비스에 대한 Active Directory 개체입니다.

**인증 정책 사일로에 대 한 Active Directory 스키마**

|표시 이름|설명|
|--------|--------|
|Authentication Policy Silo|이 클래스의 인스턴스는 할당된 사용자, 컴퓨터 및 서비스에 대한 인증 정책 및 관련 동작을 정의합니다.|
|Authentication Policy Silos|이 클래스의 컨테이너는 인증 정책 사일로 개체를 포함할 수 있습니다.|
|Authentication Policy Silo Enforced|인증 정책 사일로 적용 여부를 지정합니다.<p>적용하지 않으면 기본적으로 정책이 감사 모드로 설정됩니다. 잠재적인 성공과 실패를 나타내는 이벤트가 생성되지만 보호 기능은 시스템에 적용되지 않습니다.|
|Assigned Authentication Policy Silo Backlink|이 특성은 msDS-AssignedAuthNPolicySilo에 대한 역방향 연결입니다.|
|Authentication Policy Silo Members|AuthNPolicySilo에 할당되는 보안 주체를 지정합니다.|
|Authentication Policy Silo Members Backlink|이 특성은 msDS-AuthNPolicySiloMembers에 대한 역방향 연결입니다.|

Active Directory 관리 콘솔 또는 Windows PowerShell을 사용하여 인증 정책 사일로를 구성할 수 있습니다. 자세한 내용은 [보호된 계정을 구성하는 방법](how-to-configure-protected-accounts.md)을 참조하세요.

### <a name="about-authentication-policies"></a>인증 정책 정보
인증 정책은 계정 유형에 대한 Kerberos 프로토콜 TGT(허용 티켓) 수명 속성 및 인증 액세스 제어 조건을 정의합니다. 이 정책은 인증 정책 사일로라는 AD DS 컨테이너를 기반으로 하며 이를 제어합니다.

인증 정책은 다음을 제어합니다.

-   계정의 TGT 수명(갱신할 수 없도록 설정됨)

-   디바이스 계정이 암호 또는 인증서를 사용하여 로그인하기 위해 충족해야 하는 조건

-   사용자 및 디바이스가 계정의 일부로 실행되는 서비스의 인증을 받기 위해 충족해야 하는 조건입니다.

Active Directory 계정 유형은 다음 중 하나로 호출자의 역할을 결정 합니다.

-   **사용자**

    사용자는 항상 NTLM을 사용한 인증 시도를 기본적으로 거부하는 보호된 사용자 보안 그룹의 구성원이어야 합니다.

    사용자 계정의 TGT 수명을 더 짧은 값으로 설정하거나 디바이스를 사용자 계정에서 로그인할 수 있는 디바이스로 제한하도록 정책을 구성할 수 있습니다. 인증 정책에서 다양한 식을 구성하여 사용자 및 해당 디바이스가 서비스의 인증을 받기 위해 충족해야 하는 조건을 제어할 수 있습니다.

    자세한 내용은 [보호된 사용자 보안 그룹](protected-users-security-group.md)을 참조하세요.

-   **출력소**

    독립 실행형 관리 서비스 계정, 그룹 관리 서비스 계정 또는 이 두 가지 유형의 서비스 계정에서 파생된 사용자 지정 계정 개체가 사용됩니다. 정책은 관리 서비스 계정 자격 증명을 Active Directory id가 있는 특정 장치로 제한 하는 데 사용 되는 장치의 액세스 제어 조건을 설정할 수 있습니다. 서비스는 보호된 사용자 보안 그룹의 구성원일 수 없습니다. 이 그룹의 구성원인 경우 들어오는 모든 인증이 실패하기 때문입니다.

-   **컴퓨터별**

    컴퓨터 계정 개체 또는 컴퓨터 계정 개체에서 파생된 사용자 지정 계정 개체가 사용됩니다. 정책에서 사용자 및 디바이스 속성에 따라 계정에 대한 인증을 허용하는 데 필요한 액세스 제어 조건을 설정할 수 있습니다. 컴퓨터는 보호된 사용자 보안 그룹의 구성원일 수 없습니다. 이 그룹의 구성원인 경우 들어오는 모든 인증이 실패하기 때문입니다. 기본적으로 NTLM 인증 사용이 거부됩니다. 컴퓨터 계정에는 TGT 수명을 구성할 수 없습니다.

> [!NOTE]
> 인증 정책 사일로에 정책을 연결하지 않고 계정 집합에 대한 인증 정책을 설정할 수 있습니다. 이 전략은 단일 계정을 보호하려는 경우에 사용할 수 있습니다.

**인증 정책에 대 한 Active Directory 스키마**

사용자, 컴퓨터 및 서비스에 대한 Active Directory 개체의 정책은 다음 표에서 스키마로 정의되어 있습니다.

|형식|표시 이름|설명|
|----|--------|--------|
|정책|Authentication Policy|이 클래스의 인스턴스는 할당된 보안 주체에 대한 인증 정책 동작을 정의합니다.|
|정책|인증 정책|이 클래스의 컨테이너는 인증 정책 개체를 포함할 수 있습니다.|
|정책|Authentication Policy Enforced|인증 정책 적용 여부를 지정합니다.<p>적용하지 않으면 기본적으로 정책이 감사 모드로 설정되며, 잠재적인 성공과 실패를 나타내는 이벤트가 생성되지만 보호 기능은 시스템에 적용되지 않습니다.|
|정책|Assigned Authentication Policy Backlink|이 특성은 msDS-AssignedAuthNPolicy에 대한 역방향 연결입니다.|
|정책|Assigned Authentication Policy|이 보안 주체에 적용할 AuthNPolicy를 지정합니다.|
|사용자|User Authentication Policy|이 사일로 개체에 할당된 사용자에게 적용할 AuthNPolicy를 지정합니다.|
|사용자|User Authentication Policy Backlink|이 특성은 msDS-UserAuthNPolicy에 대한 역방향 연결입니다.|
|사용자|ms-DS-User-Allowed-To-Authenticate-To|이 특성은 사용자 계정으로 실행되는 서비스의 인증을 받을 수 있는 보안 주체 집합을 결정하는 데 사용됩니다.|
|사용자|ms-DS-User-Allowed-To-Authenticate-From|이 특성은 사용자 계정에서 로그인할 수 있는 디바이스 집합을 결정하는 데 사용됩니다.|
|사용자|User TGT Lifetime|사용자에게 발급된 Kerberos TGT의 최대 수명(초)을 지정합니다. 결과 TGT는 갱신할 수 없습니다.|
|컴퓨터|Computer Authentication Policy|이 사일로 개체에 할당된 컴퓨터에 적용할 AuthNPolicy를 지정합니다.|
|컴퓨터|Computer Authentication Policy Backlink|이 특성은 msDS-ComputerAuthNPolicy에 대한 역방향 연결입니다.|
|컴퓨터|ms-DS-Computer-Allowed-To-Authenticate-To|이 특성은 컴퓨터 계정으로 실행되는 서비스의 인증을 받을 수 있는 보안 주체 집합을 결정하는 데 사용됩니다.|
|컴퓨터|Computer TGT Lifetime|컴퓨터에 발급된 Kerberos TGT의 최대 수명(초)을 지정합니다. 이 설정을 변경하지 않는 것이 좋습니다.|
|Service|Service Authentication Policy|이 사일로 개체에 할당된 서비스에 적용할 AuthNPolicy를 지정합니다.|
|Service|Service Authentication Policy Backlink|이 특성은 msDS-ServiceAuthNPolicy에 대한 역방향 연결입니다.|
|Service|ms-DS-Service-Allowed-To-Authenticate-To|이 특성은 서비스 계정으로 실행되는 서비스의 인증을 받을 수 있는 보안 주체 집합을 결정하는 데 사용됩니다.|
|Service|ms-DS-Service-Allowed-To-Authenticate-From|이 특성은 서비스 계정에서 로그인할 수 있는 디바이스 집합을 결정하는 데 사용됩니다.|
|Service|Service TGT Lifetime|서비스에 발급된 Kerberos TGT의 최대 수명(초)을 지정합니다.|

Active Directory 관리 콘솔 또는 Windows PowerShell을 사용하여 각 사일로에 대한 인증 정책을 구성할 수 있습니다. 자세한 내용은 [보호된 계정을 구성하는 방법](how-to-configure-protected-accounts.md)을 참조하세요.

## <a name="how-it-works"></a>작동 방식
이 섹션에서는 인증 정책 사일로 및 인증 정책이 Windows의 Kerberos 프로토콜 구현 및 보호된 사용자 보안 그룹과 함께 작동하는 방식에 대해 설명합니다.

-   [인증 사일로 및 정책과 함께 Kerberos 프로토콜을 사용 하는 방법](#BKMK_HowKerbUsed)

-   [사용자 로그인 제한 작동 방식](#BKMK_HowRestrictingSignOn)

-   [서비스 티켓 발급 제한 방법](#BKMK_HowRestrictingServiceTicket)

**보호 된 계정**

보호 된 사용자 보안 그룹은 Windows Server 2012 R2 및 Windows 8.1를 실행 하는 장치 및 호스트 컴퓨터와 Windows Server 2012 r 2를 실행 하는 주 도메인 컨트롤러가 있는 도메인의 도메인 컨트롤러에서 구성할 수 없는 보호를 트리거합니다. Windows에서 지원되는 인증 방법의 변경으로 인해 보호된 사용자 보안 그룹의 구성원은 계정의 도메인 기능 수준에 따라 추가로 보호됩니다.

-   보호된 사용자 보안 그룹의 구성원은 NTLM, 다이제스트 인증 또는 CredSSP 기본 자격 증명 위임을 사용하여 인증할 수 없습니다. 이러한 Ssp (보안 지원 공급자) 중 하나를 사용 하는 Windows 8.1를 실행 하는 장치에서는 계정이 보호 된 사용자 보안 그룹의 구성원 인 경우 도메인에 대 한 인증이 실패 합니다.

-   Kerberos 프로토콜은 사전 인증 프로세스에서 보다 약한 DES 또는 RC4 암호화 종류를 사용하지 않습니다. 즉, 해당 도메인이 최소한 AES 암호화 종류를 지원하도록 구성되어야 합니다.

-   Kerberos 제한 또는 제한 되지 않은 위임으로 사용자 계정을 위임할 수 없습니다. 즉, 사용자가 보호된 사용자 보안 그룹의 구성원인 경우 다른 시스템에 대한 이전 연결이 실패할 수 있습니다.

-   Active Directory 관리 센터를 통해 액세스할 수 있는 인증 정책 및 사일로를 사용하여 기본 Kerberos TGT 수명 설정(4시간)을 구성할 수 있습니다. 즉, 4시간이 경과한 경우 사용자가 다시 인증을 받아야 합니다.

이 보안 그룹에 대한 자세한 내용은 [보호된 사용자 그룹 작동 방식](protected-users-security-group.md#BKMK_HowItWorks)을 참조하세요.

**사일로 및 인증 정책**

인증 정책 사일로와 인증 정책에서는 기존 Windows 인증 인프라를 활용합니다. NTLM 프로토콜 사용이 거부되고 최신 암호화 종류를 지원하는 Kerberos 프로토콜이 사용됩니다. 인증 정책은 계정에 구성 가능한 제한을 적용할 수 있는 방법을 제공하고 서비스 및 컴퓨터 계정에 대한 제한을 제공하여 보호된 사용자 보안 그룹을 보완합니다. 인증 정책은 Kerberos 프로토콜 AS(인증 서비스) 또는 TGS(Ticket-Granting Service) 교환 중에 적용됩니다. Windows에서 Kerberos 프로토콜을 사용하는 방법 및 인증 정책 사일로와 인증 정책을 지원하기 위해 변경된 사항에 대한 자세한 내용은 다음을 참조하세요.

-   [Kerberos 버전 5 인증 프로토콜의 작동 방식](https://technet.microsoft.com/library/cc772815(v=ws.10).aspx)

-   [Kerberos인증의 변경 내용](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) (Windows Server 2008 R2 및 Windows 7)

### <a name="how-the-kerberos-protocol-is-used-with-authentication-policy-silos-and-policies"></a><a name="BKMK_HowKerbUsed"></a>인증 정책 사일로 및 정책과 함께 Kerberos 프로토콜을 사용 하는 방법
도메인 계정이 인증 정책 사일로에 연결된 경우 사용자가 로그인하면 보안 계정 관리자는 해당 사일로가 포함된 인증 정책 사일로의 클레임 유형을 값으로 추가합니다. 계정의 이 클레임에서 대상 사일로에 대한 액세스를 제공합니다.

인증 정책이 적용되는 경우 도메인 계정에 대한 인증 서비스 요청이 도메인 컨트롤러에 수신되면 도메인 컨트롤러는 수명이 구성된 갱신할 수 없는 TGT를 반환합니다(도메인 TGT 수명이 더 짧지 않은 경우).

> [!NOTE]
> 도메인 계정은 구성된 TGT 수명이 있어야 하며, 정책에 직접 연결되거나 사일로 구성원 자격을 통해 간접적으로 연결됩니다.

인증 정책이 감사 모드에 있는 경우 도메인 계정에 대한 인증 서비스 요청이 도메인 컨트롤러에 수신되면 도메인 컨트롤러는 오류가 있는 경우 경고를 기록할 수 있도록 디바이스에 인증이 허용되는지 확인합니다. 감사된 인증 정책은 프로세스를 변경하지 않으므로 정책 요구 사항을 충족하지 않으면 인증 요청에 실패합니다.

> [!NOTE]
> 도메인 계정은 정책에 직접 연결되거나 사일로 구성원 자격을 통해 간접적으로 연결됩니다.

인증 정책이 적용되고 인증 서비스가 아머링된 경우 도메인 계정에 대한 인증 서비스 요청이 도메인 컨트롤러에 수신되면 도메인 컨트롤러는 디바이스에 인증이 허용되는지 확인합니다. 실패한 경우 도메인 컨트롤러는 오류 메시지를 반환하고 이벤트를 기록합니다.

> [!NOTE]
> 도메인 계정은 정책에 직접 연결되거나 사일로 구성원 자격을 통해 간접적으로 연결됩니다.

인증 정책이 감사 모드에 있고 도메인 컨트롤러에서 도메인 계정에 대해 티켓 부여 서비스 요청을 수신 하는 경우 도메인 컨트롤러는 요청의 티켓 권한 특성 인증서 (PAC) 데이터를 기반으로 인증이 허용 되는지 확인 하 고 실패 한 경우 경고 메시지를 기록 합니다. PAC는 사용자가 속해 있는 그룹, 사용자의 권한, 사용자에게 적용되는 정책 등 다양한 유형의 권한 부여 데이터를 포함합니다. 이 정보는 사용자의 액세스 토큰을 생성 하는 데 사용 됩니다. 사용자, 장치 또는 서비스에 대 한 인증을 허용 하는 적용 된 인증 정책 인 경우 도메인 컨트롤러는 요청의 티켓 PAC 데이터를 기반으로 인증이 허용 되는지 확인 합니다. 실패한 경우 도메인 컨트롤러는 오류 메시지를 반환하고 이벤트를 기록합니다.

> [!NOTE]
> 도메인 계정은 사용자, 디바이스 또는 서비스에 대한 인증을 허용하는 감사된 인증 정책에 직접 연결되거나 사일로 구성원 자격을 통해 연결됩니다.

사일로의 모든 구성원에 대해 단일 인증 정책을 사용하거나, 사용자, 컴퓨터 및 관리 서비스 계정에 대해 별도의 정책을 사용할 수 있습니다.

Active Directory 관리 콘솔 또는 Windows PowerShell을 사용하여 각 사일로에 대한 인증 정책을 구성할 수 있습니다. 자세한 내용은 [보호된 계정을 구성하는 방법](how-to-configure-protected-accounts.md)을 참조하세요.

### <a name="how-restricting-a-user-sign-in-works"></a><a name="BKMK_HowRestrictingSignOn"></a>사용자 로그인 제한 작동 방식
이러한 인증 정책은 계정에 적용되기 때문에 서비스에서 사용하는 계정에도 적용됩니다. 서비스에 대한 암호 사용을 특정 호스트로 제한하려는 경우 이 설정이 유용합니다. 예를 들어 그룹 관리 서비스 계정은 호스트가 Active Directory Domain Services에서 암호를 검색할 수 있도록 구성됩니다. 그러나 초기 인증 시에는 모든 호스트에서 암호를 사용할 수 있습니다. 액세스 제어 조건을 적용하면 암호를 검색할 수 있는 호스트 집합으로만 암호를 제한하여 추가 보호 계층을 실현할 수 있습니다.

시스템, 네트워크 서비스 또는 다른 로컬 서비스 id로 실행 되는 서비스는 네트워크 서비스에 연결 하는 경우 호스트의 컴퓨터 계정을 사용 합니다. 컴퓨터 계정은 제한할 수 없습니다. 따라서 서비스에서 Windows 호스트용이 아닌 컴퓨터 계정을 사용하는 경우에는 서비스를 제한할 수 없습니다.

사용자 로그인을 특정 호스트로 제한 하려면 도메인 컨트롤러에서 호스트 id의 유효성을 검사 해야 합니다. Kerberos 아머링(동적 액세스 제어의 일부)과 함께 Kerberos 인증을 사용하면 사용자를 인증하는 호스트의 TGT에 키 배포 센터가 제공됩니다. 이 아머링된 TGT의 콘텐츠는 호스트가 허용되는지 여부를 확인하는 액세스 검사를 완료하는 데 사용됩니다.

사용자가 Windows에 로그인하거나 애플리케이션의 자격 증명 프롬프트에 해당 도메인 자격 증명을 입력하면 Windows에서는 기본적으로 아머링되지 않은 AS-REQ를 도메인 컨트롤러로 보냅니다. 사용자가 아머링을 지원하지 않는 컴퓨터(예: Windows 7 또는 Windows Vista를 실행하는 컴퓨터)에서 요청을 보낸 경우 요청에 실패합니다.

다음 목록에서는 이 프로세스에 대해 설명합니다.

-   Windows Server 2012 r 2를 실행 하는 도메인의 도메인 컨트롤러는 사용자 계정에 대해 쿼리를 실행 하 고, 아머 링 요청이 필요한 초기 인증을 제한 하는 인증 정책으로 구성 되었는지 여부를 확인 합니다.

-   도메인 컨트롤러가 요청을 거부합니다.

-   아머 링이 필요 하므로 사용자는 Windows 8.1 또는 Windows 8을 실행 하는 컴퓨터를 사용 하 여 로그인을 시도할 수 있습니다 .이 컴퓨터는 Kerberos 아머 링 (armoring)을 지원 하 여 로그인 프로세스를 다시 시도할 수 있습니다.

-   Windows에서 도메인이 Kerberos 아머링을 지원하는지 검색한 후 아머링된 AS-REQ를 보내 로그인 요청을 다시 시도합니다.

-   도메인 컨트롤러는 요청을 아머 링 하는 데 사용 된 TGT의 클라이언트 운영 체제 id 정보 및 구성 된 액세스 제어 조건을 사용 하 여 액세스 검사를 수행 합니다.

-   액세스 검사에 실패한 경우 도메인 컨트롤러가 요청을 거부합니다.

운영 체제에서 Kerberos 아머링을 지원하는 경우에도 액세스 제어 요구 사항을 적용할 수 있으며, 이 경우 이를 충족해야 액세스 권한이 부여됩니다. 사용자가 Windows에 로그인하거나 애플리케이션의 자격 증명 프롬프트에 해당 도메인 자격 증명을 입력하면 Windows에서는 기본적으로 아머링되지 않은 AS-REQ를 도메인 컨트롤러로 보냅니다. 사용자가 아머 링을 지 원하는 컴퓨터 (예: Windows 8.1 또는 Windows 8)에서 요청을 보내는 경우 인증 정책은 다음과 같이 평가 됩니다.

1.  Windows Server 2012 r 2를 실행 하는 도메인의 도메인 컨트롤러는 사용자 계정에 대해 쿼리를 실행 하 고, 아머 링 요청이 필요한 초기 인증을 제한 하는 인증 정책으로 구성 되었는지 여부를 확인 합니다.

2.  도메인 컨트롤러는 구성 된 액세스 제어 조건 및 요청을 아머 링 하는 데 사용 되는 시스템의 id 정보를 사용 하 여 액세스 검사를 수행 합니다. 액세스 검사에 성공합니다.

    > [!NOTE]
    > 레거시 작업 그룹 제한이 구성된 경우 이러한 제한도 충족해야 합니다.

3.  도메인 컨트롤러가 아머링된 응답(AS-REP)으로 회신하고 인증이 계속됩니다.

### <a name="how-restricting-service-ticket-issuance-works"></a><a name="BKMK_HowRestrictingServiceTicket"></a>서비스 티켓 발급 제한 방법
계정이 허용 되지 않는 경우 TGT가 있는 사용자가 서비스의 SPN (서비스 사용자 이름)으로 식별 되는 서비스에 대 한 인증을 요구 하는 응용 프로그램을 여는 등의 방식으로 서비스에 연결 하려고 시도 하면 다음 시퀀스가 발생 합니다.

1.  SPN에서 SPN1에 연결하려고 시도하면 Windows에서 SPN1에 대한 서비스 티켓을 요청하는 도메인 컨트롤러에 TGS-REQ를 보냅니다.

2.  Windows Server 2012 r 2를 실행 하는 도메인의 도메인 컨트롤러는 조회을 조회 하 여 서비스에 대 한 Active Directory Domain Services 계정을 찾고 해당 계정이 서비스 티켓 발급을 제한 하는 인증 정책으로 구성 되었는지 확인 합니다.

3.  도메인 컨트롤러는 TGT의 사용자 id 정보 및 구성 된 액세스 제어 조건을 사용 하 여 액세스 검사를 수행 합니다. 액세스 검사에 실패합니다.

4.  도메인 컨트롤러가 요청을 거부합니다.

계정이 인증 정책에 의해 설정 된 액세스 제어 조건을 충족 하 고 TGT가 있는 사용자가 서비스의 SPN으로 식별 되는 서비스에 대 한 인증을 요구 하는 응용 프로그램을 여는 등의 방식으로 서비스에 연결 하려고 시도 하는 경우 계정이 허용 되는 경우 다음 시퀀스가 발생 합니다.

1.  SPN1에 연결하려고 시도하면 Windows에서 SPN1에 대한 서비스 티켓을 요청하는 도메인 컨트롤러에 TGS-REQ를 보냅니다.

2.  Windows Server 2012 r 2를 실행 하는 도메인의 도메인 컨트롤러는 조회을 조회 하 여 서비스에 대 한 Active Directory Domain Services 계정을 찾고 해당 계정이 서비스 티켓 발급을 제한 하는 인증 정책으로 구성 되었는지 확인 합니다.

3.  도메인 컨트롤러는 TGT의 사용자 id 정보 및 구성 된 액세스 제어 조건을 사용 하 여 액세스 검사를 수행 합니다. 액세스 검사에 성공합니다.

4.  도메인 컨트롤러가 TGS(Ticket-Granting Service) 응답(TGS-REP)으로 요청에 회신합니다.

## <a name="associated-error-and-informational-event-messages"></a><a name="BKMK_ErrorandEvents"></a>관련 오류 및 정보 이벤트 메시지
다음 표에서는 인증 정책 사일로에 적용되는 인증 정책 및 보호된 사용자 보안 그룹과 관련된 이벤트를 설명합니다.

이러한 이벤트는 응용 프로그램 및 서비스 로그( **Microsoft\Windows\Authentication**)에 기록됩니다.

이러한 이벤트를 사용하는 문제 해결 단계는 [인증 정책 문제 해결](how-to-configure-protected-accounts.md#troubleshoot-authentication-policies) 및 [보호된 사용자와 관련된 이벤트 문제 해결](how-to-configure-protected-accounts.md#troubleshoot-events-related-to-protected-users)을 참조하세요.

|이벤트 ID 및 로그|설명|
|----------|--------|
|101<p>**AuthenticationPolicyFailures-DomainController**|이유: 인증 정책이 구성되어 있어 NTLM 로그인에 실패했습니다.<p>액세스 제어 제한이 필요한데 이러한 제한은 NTLM에 적용할 수 없으므로 NTLM 인증에 실패했음을 나타내는 이벤트가 도메인 컨트롤러에 기록됩니다.<p>계정, 디바이스, 정책 및 사일로 이름이 표시됩니다.|
|105<p>**AuthenticationPolicyFailures-DomainController**|이유: 특정 디바이스의 인증이 허용되지 않아 Kerberos 제한에 실패했습니다.<p>디바이스가 적용된 액세스 제어 제한을 충족하지 않아 Kerberos TGT가 거부되었음을 나타내는 이벤트가 도메인 컨트롤러에 기록됩니다.<p>계정, 디바이스, 정책, 사일로 이름 및 TGT 수명이 표시됩니다.|
|305<p>**AuthenticationPolicyFailures-DomainController**|이유: 특정 디바이스의 인증이 허용되지 않아 잠재적으로 Kerberos 제한에 실패했습니다.<p>감사 모드에서, 디바이스가 액세스 제어 제한을 충족하지 않아 Kerberos TGT가 거부되는지 여부를 확인하는 정보 이벤트가 도메인 컨트롤러에 기록됩니다.<p>계정, 디바이스, 정책, 사일로 이름 및 TGT 수명이 표시됩니다.|
|106<p>**AuthenticationPolicyFailures-DomainController**|이유: 사용자 또는 디바이스가 서버의 인증을 받을 수 없어 Kerberos 제한에 실패했습니다.<p>사용자, 디바이스 또는 둘 다가 적용된 액세스 제어 제한을 충족하지 않아 Kerberos 서비스 티켓이 거부되었음을 나타내는 이벤트가 도메인 컨트롤러에 기록됩니다.<p>디바이스, 정책 및 사일로 이름이 표시됩니다.|
|306<p>**AuthenticationPolicyFailures-DomainController**|이유: 사용자 또는 디바이스가 서버의 인증을 받을 수 없어 Kerberos 제한에 실패했을 수 있습니다.<p>감사 모드에서, 사용자, 디바이스 또는 둘 다가 적용된 액세스 제어 제한을 충족하지 않아 Kerberos 서비스 티켓이 거부됨을 나타내는 정보 이벤트가 도메인 컨트롤러에 기록됩니다.<p>디바이스, 정책 및 사일로 이름이 표시됩니다.|

## <a name="see-also"></a>참고 항목
[보호된 계정을 구성하는 방법](how-to-configure-protected-accounts.md)

[자격 증명 보호 및 관리](credentials-protection-and-management.md)

[보호된 사용자 보안 그룹](protected-users-security-group.md)


