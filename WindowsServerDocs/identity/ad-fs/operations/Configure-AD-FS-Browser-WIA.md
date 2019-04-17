---
title: "브라우저 Adfs와 통합 된 인증 (WIA Windows)를 사용 하도록 구성"
description: "이 문서에서는 ADFS WIA 사용 하는 브라우저 구성 하는 방법에 설명"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.custom: it-pro
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f7d43931d1fe4958a539ff1b728e4cc154d06248
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="configure-browsers-to-use-windows-integrated-authentication-wia-with-ad-fs"></a>브라우저 Adfs와 통합 된 인증 (WIA Windows)를 사용 하도록 구성

기본적으로 통합 인증 (WIA Windows) 있는지의 Active Directory Federation Services (ADFS)에서 Windows Server 2012 r 2에서 조직의 내부 네트워크 (인트라넷) 브라우저를 사용 하 여 해당 인증에 대 한 모든 응용 프로그램 내에서 발생 하는 인증 요청 합니다.

이제 AD FS 2016에 할 일 동안도 하지 WIA Edge 브라우저를 사용 하는 향상 된 기본 설정이 (올바르게) 즐기거나 하지 Windows Phone도:

    =~Windows\s*NT.*Edge

더 이상 자주 업데이트 되어 있지만 일반적인 Edge 시나리오를 지원 하기 위해 사용자 상담원 문자열을 구성 해야 할 위의 의미 합니다.

다른 브라우저에 대 한 구성 ADFS 속성 **WiaSupportedUserAgents** 사용 하는 브라우저에 따라 필요한 값을 추가할 수 있습니다.  아래 절차를 사용할 수 있습니다.



### <a name="view-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 설정 보기
**WIASupportedUserAgents** 정의 사용자 에이전트 WIA을 지원 합니다. Adfs는 로그인 브라우저나 브라우저 컨트롤에서 수행할 때 사용자 에이전트 문자열을 분석 합니다.

다음 PowerShell 예제를 사용 하 여 현재 설정을 볼 수 있습니다.

```powershell
    $strings = Get-AdfsProperties | select -ExpandProperty WiaSupportedUserAgents
```

![WIA 지원](../operations/media/Configure-AD-FS-Browser-WIA/wiasupport.png)

### <a name="change-wiasupporteduseragent-settings"></a>WIASupportedUserAgent 설정 변경
기본적으로 새 ADFS 설치 사용자 에이전트 문자열 일치 만든 집합을 있습니다. 그러나 이러한 수 있습니다 최신 브라우저 및 디바이스에 변경 내용을 기반으로 합니다. 특히, Windows 디바이스는 토큰에서 조금씩와 유사한 사용자 에이전트 문자열 있습니다. 다음 Windows PowerShell 예제 원활 하 게 WIA 지원에 오늘 출시 하는 디바이스의 현재 집합에 대 한 최상의 지침을 제공 합니다.

```powershell
    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")
```

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
Windows NT 6.1; Trident/7.0</br></br>Windows NT 6.1; W i n 64; x64; Trident/7.0</br></br>Windows NT 6.1; W; O W 64 Trident/7.0|Windows 7 데스크톱 운영 체제, 다른 platoforms|
MSIPC| Microsoft의 정보 보호 및 클라이언트 제어|
Windows 권한 관리 클라이언트|Windows 권한 관리 클라이언트|
