---
title: Windows 인증 개요
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 485a0774-0785-457f-a964-0e9403c12bb1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 2021ccf1e0015cc910f43966f9400e6bd56a230c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870974"
---
# <a name="windows-authentication-overview"></a>Windows 인증 개요

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가를 위한 이 탐색 항목에는 제품 평가, 시작 가이드, 절차, 디자인 및 배포 가이드, 기술 참조, 명령 참조 등 Windows 인증 및 로그온 기술에 대한 설명서 리소스가 나열되어 있습니다.

## <a name="feature-description"></a>기능 설명
인증은 개체, 서비스 또는 사용자의 ID를 확인하는 프로세스입니다. 개체 인증의 목표는 개체가 올바른지 확인하는 데 있습니다. 서비스나 사용자 인증의 목표는 제시된 자격 증명이 정확한지 확인하는 데 있습니다.

네트워킹 컨텍스트에서 인증은 네트워크 응용 프로그램이나 리소스에 대해 ID를 증명하는 행위입니다. 일반적으로 id가 공개 키 암호화-또는 공유 키와 마찬가지로-사용자만 아는 키 중 하나를 사용 하는 암호화 작업을 통해 증명 됩니다. 인증 교환의 서버 쪽에서는 서명된 데이터를 알려진 암호화 키와 비교하여 인증 시도의 유효성을 검사합니다.

암호화 키를 안전한 중앙 위치에 저장하면 인증 프로세스를 쉽게 확장하고 유지 관리할 수 있습니다. Active Directory Domain Services를 권장 하 고 id 정보를 저장할 때는 기본 기술인 \(사용자의 자격 증명이 암호화 키를 포함 하 여\)입니다. 기본 NTLM 및 Kerberos 구현에는 Active Directory가 필요합니다.

공개 키 인증서를 토큰 같은 사용자가 소유한 항목을 사용 하는 더 강력한 보안 메커니즘으로 암호--같은 사용자만 아는 항목을 기반으로 하는 사용자를 식별 하는 간단한 로그온에서 인증 기술을 범위 및 생체 인식 합니다. 비즈니스 환경에서 서비스나 사용자는 단일 위치 또는 여러 위치에서 다양한 유형의 서버에 있는 여러 응용 프로그램이나 리소스에 액세스할 수 있습니다. 이러한 이유로, 인증은 다른 플랫폼 및 다른 Windows 운영 체제의 환경을 지원해야 합니다.

Kerberos, NTLM, Transport Layer Security를 포함 하 여 인증 프로토콜의 기본 집합을 구현 하는 Windows 운영 체제\/Secure Sockets Layer \(TLS\/SSL\), 및의 일부로 다이제스트를 확장 가능한 아키텍처입니다. 또한 몇몇 프로토콜은 협상, CredSSP(Credential Security Support Provider) 등의 인증 패키지에 결합됩니다. 이러한 프로토콜 및 패키지를 통해 사용자, 컴퓨터 및 서비스를 인증할 수 있고 권한이 부여된 사용자와 서비스는 인증 프로세스를 통해 안전하게 리소스에 액세스할 수 있습니다.

다음을 포함하여 Windows 인증에 대한 자세한 내용은

-   [Windows 인증 개념](windows-authentication-concepts.md)

-   [Windows 로그온 시나리오](windows-logon-scenarios.md)

-   [Windows 인증 아키텍처](windows-authentication-architecture.md)

-   [보안 지원 공급자 인터페이스 아키텍처](security-support-provider-interface-architecture.md)

-   [Windows 인증에서 자격 증명 프로세스](credentials-processes-in-windows-authentication.md)

-   [Windows 인증에 사용 되는 그룹 정책 설정](group-policy-settings-used-in-windows-authentication.md)

참조 된 [Windows 인증 기술 개요](windows-authentication-technical-overview.md)합니다.

## <a name="practical-applications"></a>유용한 팁
Windows 인증은 정보가 신뢰할 수 있는 출처(특정 사용자 또는 다른 컴퓨터 등의 컴퓨터 개체)에서 가져온 것인지 확인하는 데 사용됩니다. Windows에서는 아래에 설명하는 것처럼 이 목표를 달성하기 위한 여러 가지 서로 다른 방법을 제공합니다.

|받는 사람...|기능|설명|
|----|------|--------|
|Active Directory 도메인 내에서의 인증|Kerberos|Microsoft Windows&nbsp;Kerberos 버전 5 인증 프로토콜 및 공개 키 인증에 대 한 확장을 구현 하는 서버 운영 체제입니다. Kerberos 인증 클라이언트 security support provider로 구현 됩니다 \(SSP\) 보안 지원 공급자 인터페이스를 통해 액세스할 수 있습니다 \(SSPI\)합니다. 초기 사용자 인증은 Winlogon single와 통합 됩니다\-아키텍처입니다. Kerberos Key Distribution Center \(KDC\) 도메인 컨트롤러에서 실행 되는 다른 Windows Server 보안 서비스와 통합 됩니다. KDC는 도메인의 Active Directory 디렉터리 서비스 데이터베이스를 보안 계정 데이터베이스로 사용합니다. 기본 Kerberos 구현에는 Active Directory가 필요합니다.<br /><br />추가 리소스는 [Kerberos 인증 개요](../kerberos/kerberos-authentication-overview.md)를 참조하십시오.|
|웹의 보안 인증|TLS\/Schannel Security Support Provider에서 구현 될 때 SSL|전송 계층 보안 \(TLS\) 버전 1.0, 1.1 및 1.2와 Secure Sockets Layer 프로토콜 \(SSL\) 프로토콜, 버전 2.0 / 3.0, 데이터 그램 전송 계층 보안 프로토콜 버전 1.0 및 Private 통신 전송 \(PCT\) 프로토콜 버전 1.0, 공개 키 암호화를 기반으로 합니다. 보안 채널 \(Schannel\) 공급자 인증 프로토콜 제품군 이러한 프로토콜을 제공 합니다. 모든 Schannel 프로토콜은 클라이언트 및 서버 모델을 사용합니다.<br /><br />추가 리소스를 참조 하세요 [TLS-SSL &#40;Schannel SSP&#41; 개요](../tls/tls-ssl-schannel-ssp-overview.md)합니다.|
|웹 서비스 또는 응용 프로그램에 대한 인증|windows 통합 인증<br /><br />다이제스트 인증|추가 리소스는 [Windows 통합 인증](https://technet.microsoft.com/library/cc758557(v=WS.10).aspx), [다이제스트 인증](https://technet.microsoft.com/library/cc738318(v=ws.10).aspx) 및 [고급 다이제스트 인증](https://technet.microsoft.com/library/cc783131(v=ws.10).aspx)을 참조하십시오.|
|레거시 응용 프로그램에 대한 인증|NTLM|NTLM은 챌린지\-응답 스타일 인증 프로토콜입니다. 인증을 하는 것 외에도 NTLM 프로토콜이 필요에 따라 메시지 무결성 및 기밀성 NTLM의 기능 서명 및 봉인을 통한 특히 세션 보안을 위한 제공 합니다.<br /><br />추가 리소스는 [NTLM 개요](../kerberos/ntlm-overview.md)를 참조하십시오.|
|다단계 인증 사용|스마트 카드 지원<br /><br />생체 인식 지원|스마트 카드는 한 변조\-클라이언트 인증, 도메인에 로그온 하는 등의 작업에 대 한 보안 솔루션을 제공 하는 이식 가능 하 고 정보 훼손에 강하도록 방법은 코드 서명 및 e 보안\-메일입니다.<br /><br />생체 인식은 변경되지 않는 특정 사용자의 물리적 특성을 측정하여 해당 사용자를 고유하게 식별합니다. 가장 널리 사용되는 생체 인식 특성은 지문으로, 현재 PC 및 주변 장치에는 매우 다양한 지문 생체 인식 장치가 포함되어 있습니다.<br /><br />추가 리소스를 참조 하세요 [스마트 카드 기술 참조](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)합니다. |
|자격 증명에 대해 로컬 관리, 저장 및 다시 사용 지원|자격 증명 관리<br /><br />로컬 보안 기관<br /><br />암호|Windows의 자격 증명 관리를 통해 자격 증명을 안전하게 저장할 수 있습니다. 보안 된 데스크톱에서 자격 증명 수집 됩니다 \(로컬 또는 도메인 액세스에 대 한\), 앱 또는 웹 사이트를 통해 리소스에 액세스할 때마다 자격 증명이 제공 됩니다 있도록 합니다.<br /><br />
|최신 인증 보호 기능을 레거시 시스템으로 확장|인증에 대한 확장된 보호|통합 Windows 인증을 사용 하 여 네트워크 연결을 인증 하는 경우이 기능은 보호 및 자격 증명 처리 향상 \(IWA\)합니다.|

## <a name="software-requirements"></a>소프트웨어 요구 사항
Windows 인증은 이전 버전의 Windows 운영 체제와 호환되도록 설계되었습니다. 그러나 각 릴리스의 개선된 기능이 이전 버전에 반드시 적용되는 것은 아닙니다. 자세한 내용은 해당 기능의 설명서를 참조하세요.

## <a name="server-manager-information"></a>서버 관리자 정보
대부분의 인증 기능은 그룹 정책(서버 관리자를 사용해 설치 가능)을 통해 구성할 수 있습니다. Windows 생체 인식 프레임워크 기능은 서버 관리자를 통해 설치됩니다. 웹 서버와 같은 인증 방법에 따라 달라 집니다 기타 서버 역할도 \(IIS\) 서버 관리자를 사용 하 여 Active Directory Domain Services를 설치할 수도 있습니다.

## <a name="related-resources"></a>관련 자료

|인증 기술|리소스|
|----------------|-------|
|Windows 인증|[Windows 인증 기술 개요](../windows-authentication/windows-authentication-technical-overview.md)<br />버전, 일반 인증 개념, 로그온 시나리오, 지원 되는 버전 및 해당 설정에 대 한 아키텍처의 차이점을 다루는 항목을 포함 합니다.|
|Kerberos|[Kerberos 인증 개요](../kerberos/kerberos-authentication-overview.md)<br /><br />[Kerberos 제한 위임 개요](../kerberos/kerberos-constrained-delegation-overview.md)<br /><br />[Kerberos 인증 기술 참조](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)\(2003\)<br /><br />[Kerberos 유지 가이드](https://social.technet.microsoft.com/wiki/contents/articles/4209.kerberos-survival-guide.aspx) \(TechNet Wiki\)|
|TLS\/SSL 및 DTLS \(Schannel 보안 지원 공급자\)|[TLS-SSL &#40;Schannel SSP&#41; 개요](../tls/tls-ssl-schannel-ssp-overview.md)<br /><br />[Schannel 보안 지원 공급자 기술 참조](../tls/schannel-security-support-provider-technical-reference.md)|
|다이제스트 인증|[다이제스트 인증 기술 참조](https://technet.microsoft.com/library/cc782794(v=ws.10).aspx)\(2003\)|
|NTLM|[NTLM 개요](../kerberos/ntlm-overview.md)<br />현재 및 과거의 리소스에 대 한 링크를 포함합니다.|
|PKU2U|[Windows의 PKU2U 소개](https://technet.microsoft.com/library/dd560634(v=ws.10).aspx)|
|스마트 카드|[스마트 카드 기술 참조](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)<br /><br />
|자격 증명|[자격 증명 보호 및 관리](../credentials-protection-and-management/credentials-protection-and-management.md)<br />현재 및 과거의 리소스에 대 한 링크를 포함합니다.<br /><br />[암호 개요](../kerberos/passwords-overview.md)<br />현재 및 과거의 리소스에 대 한 링크를 포함합니다.|


