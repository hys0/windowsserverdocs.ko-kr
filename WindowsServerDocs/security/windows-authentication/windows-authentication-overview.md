---
title: "Windows 인증 개요"
description: "Windows Server 보안"
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
ms.openlocfilehash: c2ec55ed6b09628d1d80a24be766259980e84d6e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="windows-authentication-overview"></a>Windows 인증 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 탐색 항목 시작된 가이드, 절차, 디자인 및 배포 가이드, 기술 참조 및 명령 참조 제품 평가 포함 하는 Windows 인증과 로그온 기술에 대 한 설명서 리소스 나열 됩니다.

## <a name="feature-description"></a>기능 설명
인증은 프로세스 개체, 서비스 또는 사용자의 신원을 확인 합니다. 개체 인증할 때 정품 인지 확인 하기 위해 목표가입니다. 서비스 또는 사람 인증할 때 목표는 제시한 자격 증명이 인증 확인 합니다.

네트워킹 컨텍스트에서 인증 신원을 네트워크 응용 프로그램이 나 리소스에 증명 하는 작업입니다. 일반적으로 신원은 암호화 키 공개 암호화-또는 공유 키와 같이 사용자만 아는-키를 사용 하 여 작업으로 입증입니다. 인증 거래소의 서버 쪽 인증 시도 유효성을 검사 하기 알려진된 암호화 키를 서명된 된 데이터를 비교 합니다.

확장 하 고 관리 하기 쉬운 인증 프로세스를 사용 하면 암호화 키 안전 하 게 한곳에 저장 합니다. Active Directory Domain Services 권장 되는 id 정보를 저장 하기 위한 기본 기술을 \ (사용자의 credentials\ 있는 암호화 키를 포함 한). Active Directory NTLM 기본 및 Kerberos 구현 필요 합니다.

인증 방법 사용자만 아는-암호와 같은 사용자에 게-토큰과 공개 키 인증서 생체 인식와 같은 항목을 사용 하는 강력한 보안 메커니즘을 내용을 기반으로 사용자를 식별 하는 간단한 로그온에서 다양 합니다. 비즈니스 환경 서비스 또는 사용자 여러 응용 프로그램이 나 리소스 다양 한 곳에서 나 여러 위치에서 서버에 액세스할 수 있습니다. 이러한 이유로 인증 환경 및 다른 Windows 운영 체제에 대 한 다른 플랫폼에 대 한 지원 해야 합니다.

Windows 운영 체제 구현 인증 프로토콜을 Kerberos NTLM 등의 기본 설정 Transport Layer Security\/Secure 주소 \(TLS\/SSL\) 및 extensible 아키텍처의 일환으로 요약입니다. 또한 일부 프로토콜 자격 증명 보안 지원 공급자 협상 등 인증 패키지도 결합 됩니다. 이러한 프로토콜 및 패키지 사용자가, 컴퓨터 및 서비스의 인증을 사용합니다. 인증 프로세스를 안전 하 게에서 리소스에 액세스 권한이 있는 사용자 및 서비스에 있습니다.

Windows 인증 등 대 한 자세한 내용은

-   [Windows 인증 개념](windows-authentication-concepts.md)

-   [Windows 로그온 시나리오](windows-logon-scenarios.md)

-   [Windows 인증 건축물](windows-authentication-architecture.md)

-   [보안 지원 공급자 인터페이스 구조](security-support-provider-interface-architecture.md)

-   [자격 증명 프로세스 Windows 인증](credentials-processes-in-windows-authentication.md)

-   [Windows 인증에 사용 되는 그룹 정책 설정](group-policy-settings-used-in-windows-authentication.md)

참조는 [Windows 인증 기술 개요](windows-authentication-technical-overview.md)합니다.

## <a name="practical-applications"></a>실용적인 응용 프로그램
Windows 인증 출처를 신뢰할 수 있는 정보를 가져오는 것 같은 다른 컴퓨터 사용자 또는 컴퓨터 개체의 여부를 확인 하는 데 사용 됩니다. Windows는 아래에 설명 된 대로이 목표를 달성 하기 위해 다양 한 방법을 제공 합니다.

|받는 사람...|기능|설명|
|----|------|--------|
|인증 된 Active Directory 도메인에 있습니다|Kerberos|Microsoft Windows&nbsp;Kerberos 5 버전 인증 프로토콜을 공개 키 인증에 대 한 확장 서버 운영 체제를 구현 합니다. 보안 지원 공급자로 인증 Kerberos 클라이언트는 구현 \(SSP\) 보안 지원 공급자 인터페이스 \(SSPI\)를 통해 액세스할 수 있습니다. 초기 사용자 인증 Winlogon 단일 sign\ 켜 짐 건축물과 섞여 통합 되어 있습니다. 도메인 컨트롤러에서 실행 되는 다른 Windows Server 보안 서비스 Kerberos 키 메일 센터 \(KDC\) 통합 되어 있습니다. KDC 보안 계정 데이터베이스도 도메인의 Active Directory 디렉터리 서비스 데이터베이스를 사용합니다. Active Directory 기본 Kerberos 구현을 필요 합니다.<br /><br />추가 리소스에 대 한 참고 [Kerberos 인증 개요](../kerberos/kerberos-authentication-overview.md)합니다.|
|웹에서 보안 인증|TLS\/SSL Schannel 보안 지원 공급자에서 구현 될 때|Transport Layer Security \(TLS\) 프로토콜 버전 1.0 민 1.1, 1.2 주소 \(SSL\) 프로토콜 버전 2.0 및 데이터 그램 Transport Layer Security 3.0 프로토콜 버전 1.0, 그리고 개인 커뮤니케이션 전송 \(PCT\) 프로토콜 버전 1.0 키 공개 암호화를 기반으로 합니다. 보안 채널 \(Schannel\) 공급자 인증 프로토콜 제품군 이러한 프로토콜을 제공합니다. 모든 Schannel 프로토콜 클라이언트 및 서버 모델을 사용 합니다.<br /><br />추가 리소스에 대 한 참고 [TLS-SSL & #40; Schannel SSP & #41; 개요](../tls/tls-ssl-schannel-ssp-overview.md)합니다.|
|웹 서비스 또는 응용 프로그램에 인증|통합된 Windows 인증<br /><br />요약 인증|For additional resources, see [Integrated Windows Authentication](https://technet.microsoft.com/library/cc758557(v=WS.10.aspx and [Digest Authentication](https://technet.microsoft.com/library/cc738318(v=ws.10).aspx), and [Advanced Digest Authentication](https://technet.microsoft.com/library/cc783131(v=ws.10).aspx).|
|레거시 응용 프로그램에 인증|NTLM|NTLM는 인증 challenge\ 응답 스타일 인증 protocol.In 추가, NTLM 프로토콜 필요에 따라 제공 메시지 무결성 및에 서명 하 고 봉인 NTLM의 기능을 통해 기밀성 특히 세션 보안에 대 한 합니다.<br /><br />추가 리소스에 대 한 참고 [NTLM 개요](../kerberos/ntlm-overview.md)합니다.|
|다단계 인증 활용 하는 방법|스마트 카드 지원<br /><br />생체 지원|스마트 카드는, 서명 하 고 보안 하기 주기 e\ 메일 클라이언트 인증 도메인에 로그온 하는 등의 작업을 위한 솔루션 보안 코드를 제공 하는 노트북 부정 tamper\ 방지 합니다.<br /><br />생체 인식 측정 고유 해당 사용자를 식별 하기 위해 사용자의 실제는 변경 되지 않는 특징에 의존 합니다. 지문도 백만 대의 개인용 컴퓨터 및 주변 기기에 포함 된 지문 생체 인식 디바이스의 가장 자주 사용 되는 생체 인식 특성 중 하나입니다.<br /><br />추가 리소스에 대 한 참고 [스마트 카드 기술 참조](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)합니다. |
|로컬 관리, 저장소 및 자격 증명을 다시 사용할 제공|자격 증명 관리<br /><br />로컬 보안 기관<br /><br />암호|Windows에서 자격 증명 관리 안전 하 게 자격 증명을 저장 하는 것을 보장 합니다. 자격 증명은 보안 데스크톱에서 수집 된 \ (예: 로컬 또는 도메인 access\), 앱 또는 웹 사이트를 통해 올바른 자격 증명을 때마다 제공한 되도록는 리소스에 액세스 합니다.<br /><br />
|기존 시스템을 최신 인증 보호 연장|인증에 대 한 연장된 보호|이 기능은 인증이 \(IWA\)를 사용 하 여 네트워크 연결 인증할 때 보호 및 처리 자격 증명 향상 시킵니다.|

## <a name="software-requirements"></a>소프트웨어 요구 사항
Windows 인증은 Windows 운영 체제의 이전 버전과 호환 되도록 설계 되었습니다. 그러나 각 릴리스에 개선 반드시 이전 버전에 적용 되지 않습니다. 자세한 내용은 특정 기능에 대 한 설명서를 참조 하세요.

## <a name="server-manager-information"></a>서버 관리자 정보
많은 인증 기능 서버 관리자를 사용 하 여 설치할 수 있는 그룹 정책을 사용 하 여 구성할 수 있습니다. Windows 생체 프레임 워크 기능이 서버 관리자를 사용 하 여 설치 됩니다. 웹 서버 \(IIS\), Active Directory Domain Services 등 인증 방법에 의존 하는 다른 서버 역할 서버 관리자를 사용 하 여 설치할 수 있습니다.

## <a name="related-resources"></a>관련된 리소스

|인증 기술|리소스|
|----------------|-------|
|Windows 인증|[Windows 인증 기술 개요](../windows-authentication/windows-authentication-technical-overview.md)<br />버전, 일반 인증 개념, 로그온 시나리오, 지원 되는 버전와 해당 설정에 대 한 아키텍처 간의 차이점을 해결 한 항목이 있습니다.|
|Kerberos|[Kerberos 인증 개요](../kerberos/kerberos-authentication-overview.md)<br /><br />[Kerberos 위임 개요를 제한](../kerberos/kerberos-constrained-delegation-overview.md)<br /><br />[Kerberos Authentication Technical Reference](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)\(2003\)<br /><br />[Kerberos Survival Guide](https://social.technet.microsoft.com/wiki/contents/articles/4209.kerberos-survival-guide.aspx) \(TechNet Wiki\)|
|TLS\/SSL 및 DTLS \ (Schannel 보안 지원 provider\)|[TLS-SSL & #40; Schannel SSP & #41; 개요](../tls/tls-ssl-schannel-ssp-overview.md)<br /><br />[Schannel 보안 지원 공급자 기술 참조](../tls/schannel-security-support-provider-technical-reference.md)|
|요약 인증|[Digest Authentication Technical Reference](https://technet.microsoft.com/library/cc782794(v=ws.10).aspx)\(2003\)|
|NTLM|[NTLM 개요](../kerberos/ntlm-overview.md)<br />과거와 현재 리소스에 대 한 링크를 포함합니다.|
|PKU2U|[Windows에서 PKU2U 소개](https://technet.microsoft.com/library/dd560634(v=ws.10).aspx)|
|스마트 카드|[스마트 카드 기술 참조](https://technet.microsoft.com/itpro/windows/keep-secure/smart-card-windows-smart-card-technical-reference)<br /><br />
|자격 증명|[자격 증명 보호 및 관리](../credentials-protection-and-management/credentials-protection-and-management.md)<br />과거와 현재 리소스에 대 한 링크를 포함합니다.<br /><br />[암호 개요](../kerberos/passwords-overview.md)<br />과거와 현재 리소스에 대 한 링크를 포함합니다.|


