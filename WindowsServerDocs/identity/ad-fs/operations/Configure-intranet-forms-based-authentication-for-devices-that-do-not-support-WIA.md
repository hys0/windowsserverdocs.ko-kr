---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: "인트라넷 인증 WIA 지원 하지 않는 디바이스에 대 한 구성"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c78dc702cbff8eab487c6c077dfe57b0f0663342
ms.sourcegitcommit: 5012c078b410f59261edf0cc917393467243a5c7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>인트라넷 인증 WIA 지원 하지 않는 디바이스에 대 한 구성

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

기본적으로 통합 인증 (WIA Windows) 있는지의 Active Directory Federation Services (ADFS)에서 Windows Server 2012 r 2에서 조직의 내부 네트워크 (인트라넷) 브라우저를 사용 하 여 해당 인증에 대 한 모든 응용 프로그램 내에서 발생 하는 인증 요청 합니다. 예를 들어, WS Federation를 사용 하는 브라우저 기반 응용 프로그램이 나 SAML 프로토콜 및 다양 한 응용 프로그램은 OAuth 프로토콜을 사용 하는 수 있습니다. WIA 수동으로 자격 증명을 입력할 필요 없이 응용 프로그램에 원활 하 게 로그온 최종 사용자에 게 제공 합니다. 그러나 일부 장치 및 브라우저 WIA 지원할 수 있습니다. 및 따라서 이러한 디바이스에서 인증이 요청이 실패 합니다. 또한, ntlm 협상할 일부 브라우저에 경험 적합 하지 않습니다. 이러한 디바이스 및 브라우저 폼 기반 인증을 대체 하는 것이 좋습니다.

Windows Server 2016 및 Windows Server 2012 r 2에 ADFS 지원 인증을 대체 하는 에이전트 사용자 목록에를 구성 하는 기능 관리자를 제공 합니다. 두 개의 구성으로 대체 수 있게 됩니다.


- **WIASupportedUserAgentStrings** 속성은 `Set-ADFSProperties` commandlet
- **WindowsIntegratedFallbackEnabled** 속성은 `Set-AdfsGlobalAuthenticationPolicy` commmandlet

**WIASupportedUserAgentStrings** 정의 사용자 에이전트 WIA을 지원 합니다. Adfs는 로그인 브라우저나 브라우저 컨트롤에서 수행할 때 사용자 에이전트 문자열을 분석 합니다. 사용자 에이전트 문자열의 구성 요소 일치 하지 않는 경우에서 구성 된 사용자 상담원 문자열의 구성 요소 **WIASupportedUserAgentStrings** 속성 Adfs는로 대체 폼 기반 인증을 제공 하는 제공는 **WindowsIntegratedFallbackEnabled** 플래그가 실제로 설정 되어 있습니다.

기본적으로 새 ADFS 설치 사용자 에이전트 문자열 일치 만든 집합을 있습니다. 그러나 이러한 수 있습니다 최신 브라우저 및 디바이스에 변경 내용을 기반으로 합니다. 특히, Windows 디바이스는 토큰에서 조금씩와 유사한 사용자 에이전트 문자열 있습니다. 다음 Windows PowerShell 예제 원활 하 게 WIA 지원에 오늘 출시 하는 디바이스의 현재 집합에 대 한 최상의 지침을 제공 합니다.

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

위의 명령을 ADFS wia 사용 하 여 다음과 같은 경우에만 적용는 있는지 확인 합니다.

사용자 에이전트|사용 하는 경우|
-----|-----|
6.0 MSIE|IE 6.0|
MSIE 7.0; Windows NT|IE 7, 인트라넷 영역에서 IE 합니다. 데스크톱 운영 체제에서 "Windows" NT 조각 전송 됩니다.|
MSIE 8.0|IE 8.0 (장치가이 보내기, 하므로 더 많은 특정 해야 할)|
MSIE 9.0|IE 9.0 (장치가 보내기, 더 자세한로 필요)|
MSIE 10.0; Windows NT 6|Windows XP와 새로운 버전의 데스크톱 운영 체제에 대 한 IE 10.0</br></br>수신자 때문에 Windows Phone 8.0 장치 (모바일에 설정 기본 설정)는 제외</br></br>사용자 에이전트: Mozilla/5.0 (호환 됩니다. MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; 암; 터치 합니다. NOKIA; Lumia 920)|
Windows NT 6.3; Trident/7.0</br></br>Windows NT 6.3; W i n 64; x64; Trident/7.0</br></br>Windows NT 6.3; W; O W 64 Trident/7.0| Windows 8.1 데스크톱 운영 체제, 다양 한 플랫폼|
Windows NT 6.2; Trident/7.0</br></br>Windows NT 6.2; W i n 64; x64; Trident/7.0</br></br>Windows NT 6.2; W; O W 64 Trident/7.0|Windows 8 데스크톱 운영 체제, 다양 한 플랫폼|
Windows NT 6.1; Trident/7.0</br></br>Windows NT 6.1; W i n 64; x64; Trident/7.0</br></br>Windows NT 6.1; W; O W 64 Trident/7.0|Windows 7 데스크톱 운영 체제, 다양 한 플랫폼|
MSIPC| Microsoft의 정보 보호 및 클라이언트 제어|
Windows 권한 관리 클라이언트|Windows 권한 관리 클라이언트|

참에 WindowsIntegratedFallbackEnabled 플래그 설정 WIASupportedUserAgents 문자열에서 언급 했던 것과 다른 사용자 상담원에 따라 양식 인증 대체 시스템을 사용 하도록 설정 하려면

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

또한 폼 기반 인증 인트라넷 활성화 되어 있는지 확인 합니다.

## <a name="configuring-wia-for-chrome"></a>Chrome에 대 한 WIA 구성
Chrome 또는 다른 사용자 에이전트 WIA 원하는 ADFS 구성에 추가할 수 있습니다. 이 통해 Adfs에 의해 보호 리소스에 액세스할 때 수동으로 자격 증명을 입력할 필요 없이 응용 프로그램에 원활 하 게 로그온 합니다. WIA 크롬에서 사용 하도록 설정 하려면 다음 단계를 따르세요.

ADFS 구성에서 사용자 에이전트 문자열 Chrome에 대 한 추가

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + “Chrome”)
    
Chrome에 대 한 사용자 에이전트 문자열 ADFS 속성에서 이제 설정 되어 있는지 확인

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

![auth 구성](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> 새 브라우저와 디바이스 출시 되 면 사용자 에이전트 해당 기능을 조정 하 고 브라우저와 디바이스 메일로 사용 하는 경우 사용자의 인증 환경을 최적화 하기 위해 ADFS 구성에 따라 업데이트는 것이 좋습니다. 특히 것이 좋습니다 다시 평가 하 않도록는 **WIASupportedUserAgents** WIA에 대 한 새 디바이스나 브라우저 형식을 지원 매트릭스를 추가할 때 adfs에서 설정 합니다.


