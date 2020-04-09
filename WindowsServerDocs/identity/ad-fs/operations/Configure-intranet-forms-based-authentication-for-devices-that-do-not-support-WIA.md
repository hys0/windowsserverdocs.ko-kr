---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: WIA를 지원 하지 않는 디바이스에 대 한 인트라넷 폼 기반 인증 구성
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 7db040d98317cee67e78493b2210f33279221aa9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817046"
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>WIA를 지원 하지 않는 디바이스에 대 한 인트라넷 폼 기반 인증 구성


기본적으로 windows Server 2012 r 2의 Active Directory Federation Services (AD FS)에서 브라우저를 사용 하 여 해당 인증에 대해 브라우저를 사용 하는 응용 프로그램에 대 한 인증 요청에 대 한 windows Server r 2에서 WIA (Windows 통합 인증)가 사용 됩니다. 예를 들어 WS-FEDERATION 또는 SAML 프로토콜을 사용 하는 브라우저 기반 응용 프로그램 및 OAuth 프로토콜을 사용 하는 다양 한 응용 프로그램이 있을 수 있습니다. WIA 수동으로 자격 증명을 입력 하지 않고도 최종 사용자가 애플리케이션에 원활 하 게 로그온을 제공 합니다. 그러나 일부 디바이스 및 브라우저 WIA를 지원할 수 있습니다. 및 결과적으로 이러한 디바이스에서 인증 요청 실패 합니다. 또한, NTLM을 협상 하는 특정 브라우저에서 경험은 바람직하지 않습니다. 이러한 디바이스 및 브라우저에 대 한 폼 기반 인증으로 대체 하는 것이 좋습니다.

Windows Server 2016 및 Windows Server 2012 r 2에서 AD FS 폼 기반 인증에 대 한 대체 (fallback)를 지 원하는 사용자 에이전트 목록을 구성 하는 기능으로는 관리자를 제공 합니다. 두 구성에 의해 대체가 이루어집니다.


- **WIASupportedUserAgentStrings** 의 속성은 `Set-ADFSProperties` commandlet
- `Set-AdfsGlobalAuthenticationPolicy`의 **WindowsIntegratedFallbackEnabled** 속성입니다.

**WIASupportedUserAgentStrings** WIA를 지원 합니다. 사용자 에이전트를 정의 합니다. AD FS는 브라우저 컨트롤 또는 브라우저에서 로그인을 수행할 때 사용자 에이전트 문자열을 분석 합니다. 사용자 에이전트 문자열의 구성 요소에 구성 된 사용자 에이전트 문자열의 구성 요소 중 하나라도 일치 하지 않는 **WIASupportedUserAgentStrings** 속성, AD FS로 대체 됩니다 제공 하는 폼 기반 인증을 제공 하는 **WindowsIntegratedFallbackEnabled** 플래그가 True로 설정 됩니다.

기본적으로 새 AD FS 설치의 집합이 생성 하는 사용자 에이전트 문자열 일치 합니다. 그러나 이러한 될 수 있습니다 최신 브라우저 및 디바이스 변경 내용을 기반으로 합니다. 특히, Windows 디바이스 조금씩와 유사한 사용자 에이전트 문자열을 토큰에 있습니다. 다음 Windows PowerShell 예에서는 현재 집합을 원활 하 게 WIA를 지원 합니다. 현재 시중에는 디바이스에 대 한 최상의 지침을 제공 합니다.

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

위의 명령을 AD FS만 설명 되어 있는 다음 사용 사례 wia 확인 됩니다.

사용자 에이전트|사용 사례|
-----|-----|
MSIE 6.0|IE 6.0|
7\.0; MSIE Windows NT|IE 7, IE 인트라넷 영역에 있습니다. "Windows NT" 조각은 데스크톱 운영 체제에서 전송 됩니다.|
MSIE 8.0|IE 8.0 (디바이스가 없으면이 전송, 보다 구체적인 해야 하므로)|
MSIE 9.0|IE 9.0 (디바이스가 보내기이 더 해야이 더 구체적인)|
10.0; MSIE Windows NT 6|Windows XP 및 데스크톱 운영 체제의 최신 버전 IE 10.0</br></br>Windows Phone 8.0 디바이스 (기본 설정에서 모바일 설정)를 전송 하기 때문에 제외 됩니다.</br></br>사용자 에이전트: Mozilla/5.0 (호환; 10.0; MSIE Windows Phone 8.0; Trident/6.0; IEMobile/10.0; ARM; 터치; NOKIA; Lumia 920)|
Windows NT 6.3; Trident/7.0</br></br>Windows NT 6.3; Win64; x64; Trident/7.0</br></br>Windows NT 6.3; W O W 64입니다. Trident/7.0| Windows 8.1 데스크톱 운영 체제, 다른 플랫폼|
Windows NT 6.2; Trident/7.0</br></br>Windows NT 6.2; Win64; x64; Trident/7.0</br></br>Windows NT 6.2; W O W 64입니다. Trident/7.0|Windows 8 데스크톱 운영 체제를 서로 다른 플랫폼|
Windows NT 6.1; Trident/7.0</br></br>Windows NT 6.1; Win64; x64; Trident/7.0</br></br>Windows NT 6.1; W O W 64입니다. Trident/7.0|Windows 7 데스크톱 운영 체제, 다른 플랫폼|
MSIPC| Microsoft 정보 보호 및 제어 클라이언트|
Windows Rights Management 클라이언트|Windows Rights Management 클라이언트|

WIASupportedUserAgents 문자열에 언급 된 것과 다른 사용자 에이전트에 대 한 양식 기반 인증으로 대체 (fallback)를 사용 하려면 WindowsIntegratedFallbackEnabled 플래그를 true로 설정

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

또한 인트라넷에 사용 하는 양식 기반 인증이 설정 되어 있는지 확인 합니다.

## <a name="configuring-wia-for-chrome"></a>WIA Chrome에 대 한 구성
Chrome 또는 다른 사용자 에이전트를 지 원하는 WIA AD FS 구성에 추가할 수 있습니다. 이 통해 AD FS에서 보호 되는 리소스에 액세스할 때 자격 증명을 수동으로 입력 하지 않고도 애플리케이션에 로그온 합니다. 크롬에서 WIA를 사용 하도록 설정 하려면 다음 단계를 수행 합니다.

AD FS 구성에서 Windows 기반 플랫폼에서 Chrome에 대 한 사용자 에이전트 문자열을 추가 합니다.

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + "Mozilla/5.0 (Windows NT)")

또한 Apple macOS에서 Chrome의 경우와 마찬가지로 AD FS 구성에 다음 사용자 에이전트 문자열을 추가 합니다.

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + "Mozilla/5.0 (Macintosh; Intel Mac OS X)")

이제 Chrome에 대 한 사용자 에이전트 문자열이 AD FS 속성에서 설정 되어 있는지 확인 합니다.

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

(여기에 새 스크린샷 필요) 인증을 구성 ![](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> 새 브라우저와 장치를 출시 하면 해당 사용자 에이전트의 기능을 조정 하 고 AD FS 구성을 적절 하 게 업데이트 하 여 브라우저와 장치를 사용할 때 사용자의 인증 환경을 최적화 하는 것이 좋습니다. 구체적으로 말하면, 것이 좋습니다 다시 평가 하는 **WIASupportedUserAgents** wia 지원 매트릭스에 새 장치 또는 브라우저 종류를 추가 하는 경우 AD FS에서 설정 합니다.

