---
title: AD FS에서 WIA (Windows 통합 인증)를 사용 하도록 브라우저 구성
description: 이 문서에서는 AD FS에서 WIA를 사용 하도록 브라우저를 구성 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 576ec407e244485441e99ed831b4ed9a0dac198c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358254"
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>AD FS에서 WIA (Windows 통합 인증)를 사용 하도록 브라우저 구성

기본적으로 WIA (Windows 통합 인증)는 Windows Server 2012 r 2의 Active Directory Federation Services (AD FS)에서를 사용 하는 응용 프로그램에 대해 조직의 내부 네트워크 (인트라넷) 내에서 발생 하는 인증 요청에 대해 사용 하도록 설정 됩니다. 브라우저의 인증입니다.

이제 AD FS 2016에는 향상 된 기본 설정이 포함 되어 있습니다 .이 설정을 통해 Edge 브라우저에서 WIA를 수행할 뿐만 아니라 (잘못 된) Windows Phone를 catch 할 수 있습니다.

    =~Windows\s*NT.*Edge

위의 경우에는 자주 업데이트 되더라도 일반적인 Edge 시나리오를 지원 하기 위해 개별 사용자 에이전트 문자열을 더 이상 구성할 필요가 없습니다.

다른 브라우저의 경우 사용 중인 브라우저에 따라 필요한 값을 추가 하도록 **Wiasupporteduseragents** AD FS 속성을 구성 합니다.  아래 절차를 사용할 수 있습니다.



### <a name="view-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 설정 보기
**Wiasupporteduseragents** 는 WIA를 지 원하는 사용자 에이전트를 정의 합니다. AD FS는 브라우저 컨트롤 또는 브라우저에서 로그인을 수행할 때 사용자 에이전트 문자열을 분석 합니다.

다음 PowerShell 예제를 사용 하 여 현재 설정을 볼 수 있습니다.

```powershell
    Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![WIA 지원](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 설정 변경
기본적으로 새 AD FS 설치의 집합이 생성 하는 사용자 에이전트 문자열 일치 합니다. 그러나 이러한 될 수 있습니다 최신 브라우저 및 장치 변경 내용을 기반으로 합니다. 특히, Windows 장치 조금씩와 유사한 사용자 에이전트 문자열을 토큰에 있습니다. 다음 Windows PowerShell 예에서는 현재 집합을 원활 하 게 WIA를 지원 합니다. 현재 시중에는 장치에 대 한 최상의 지침을 제공 합니다.

```powershell
    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")
```

위의 명령을 AD FS만 설명 되어 있는 다음 사용 사례 wia 확인 됩니다.

사용자 에이전트|사용 사례|
-----|-----|
MSIE 6.0|IE 6.0|
7\.0; MSIE Windows NT|IE 7, IE 인트라넷 영역에 있습니다. "Windows NT" 조각 데스크톱 운영 체제에서 전송 됩니다.|
MSIE 8.0|IE 8.0 (장치가 없으면이 전송, 보다 구체적인 해야 하므로)|
MSIE 9.0|IE 9.0 (장치가 보내기이 더 해야이 더 구체적인)|
10.0; MSIE Windows NT 6|Windows XP 및 데스크톱 운영 체제의 최신 버전 IE 10.0</br></br>Windows Phone 8.0 장치 (기본 설정에서 모바일 설정)를 전송 하기 때문에 제외 됩니다.</br></br>사용자 에이전트: Mozilla/5.0 (호환 가능; MSIE 10.0; Windows Phone 8.0; Trident/6.0; IEMobile/10.0; 암 누릅니다 NOKIA Lumia 920)|
Windows NT 6.3; Trident/7.0</br></br>Windows NT 6.3; Win64; x64; Trident/7.0</br></br>Windows NT 6.3; W O W 64입니다. Trident/7.0| Windows 8.1 데스크톱 운영 체제, 다른 플랫폼|
Windows NT 6.2; Trident/7.0</br></br>Windows NT 6.2; Win64; x64; Trident/7.0</br></br>Windows NT 6.2; W O W 64입니다. Trident/7.0|Windows 8 데스크톱 운영 체제를 서로 다른 플랫폼|
Windows NT 6.1; Trident/7.0</br></br>Windows NT 6.1; Win64; x64; Trident/7.0</br></br>Windows NT 6.1; W O W 64입니다. Trident/7.0|Windows 7 데스크톱 운영 체제, 다른 플랫폼|
MSIPC| Microsoft 정보 보호 및 제어 클라이언트|
Windows Rights Management 클라이언트|Windows Rights Management 클라이언트|
