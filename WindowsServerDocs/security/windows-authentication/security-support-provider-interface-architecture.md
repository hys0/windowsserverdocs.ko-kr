---
title: "보안 지원 공급자 인터페이스 구조"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: de09e099-5711-48f8-adbd-e7b8093a0336
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 8b0a74089c5d8a88a380f8a56e3b9e03b84081c1
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="security-support-provider-interface-architecture"></a>보안 지원 공급자 인터페이스 구조

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 용 참조 여기서 보안 공급자 SSPI (지원 인터페이스) 아키텍처 내에서 사용 되는 Windows 인증 프로토콜에 설명 합니다.

Microsoft 보안 지원 공급자 Interface (SSPI)는 Windows 인증 foundation 합니다. 응용 프로그램 및 인증을 요구 infrastructure 서비스 제공을 SSPI 사용 합니다.

SSPI 구현의는 일반적인 보안 서비스 API (gssapi가) Windows Server 운영 체제에서입니다. Gssapi가 대 한 자세한 내용은 RFC 2743 및 RFC 2744 IETF RFC 데이터베이스에를 참조 하십시오.

기본 보안 지원 되는 공급자 (규칙이) Windows의 특정 인증 프로토콜 호출 Dll으로 SSPI에 통합 됩니다. 이러한 기본 규칙이 다음 섹션에 설명 되어 있습니다. 추가 규칙이 SSPI와 작동 하는 경우 포함 될 수 있습니다.

다음 이미지에서와 같이 Windows의 SSPI 인증 토큰 클라이언트 컴퓨터와 서버 기존 통신 채널을 통해 전달 하는 장치를 제공 합니다. 두 개의 컴퓨터나 디바이스를 안전 하 게 통신할 수 있도록 인증을 할 때 인증에 대 한 요청을 SSPI에서 현재 사용 중인 네트워크 프로토콜에 관계 없이 인증 프로세스를 완료 하는 전달 됩니다. SSPI 투명 이진 큰 개체를 반환합니다. 이러한 응용 프로그램, SSPI 계층을 전달할 수 있습니다 시점 간에 전달 됩니다. 따라서 SSPI 응용 프로그램을 인터페이스의 보안 시스템을 변경 하지 않고 컴퓨터 또는 네트워크에 사용할 수 있는 다양 한 보안 모델을 사용할 수 있습니다.

![보안 지원을 공급자 인터페이스 아키텍처를 보여 주는 다이어그램](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

다음 섹션에서는 SSPI와 상호 작용 하는 기본 규칙이 설명 합니다. 규칙이 비보안 네트워크 환경에서 보안 통신 올리려면 Windows 운영 체제의 다른 방법으로 사용 됩니다.

-   [Kerberos 보안 지원 공급자](#BKMK_KerbSSP)

-   [보안 지원 NTLM 공급자](#BKMK_NTLMSSP)

-   [요약 보안 지원 공급자](#BKMK_DigestSSP)

-   [Schannel 보안 지원 공급자](#BKMK_SchannelSSP)

-   [보안 지원 공급자 협상합니다](#BKMK_NegoSSP)

-   [자격 증명 보안 지원 공급자](#BKMK_CredSSP)

-   [확장 보안 지원 공급자 협상합니다](#BKMK_NegoExtsSSP)

-   [PKU2U 보안 지원 공급자](#BKMK_PKU2USSP)

이 항목에도 포함 되어 있습니다.

[보안 지원 공급자 선택](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Kerberos 보안 지원 공급자
이 SSP Kerberos 5 버전 프로토콜을 사용 하 여 Microsoft에 의해 구현 합니다. 이 프로토콜 네트워크 작업 그룹의 RFC 4120 및 초안 수정 내용을 기반으로 합니다. 것은 산업 표준 프로토콜 대화형 로그온에 대 한 암호를 또는 스마트 카드와 함께 사용할입니다. Windows의 서비스에 대 한 기본 설정된 인증 방법을 이기도합니다.

모든 도메인 서비스는 메시지만 Kerberos 프로토콜 지났습니다 기본 인증 프로토콜 Windows 2000, 때문에 지원 이러한 서비스는 다음과 같습니다.

-   LDAP(Lightweight Directory Access Protocol) (LDAP) 사용 하는 active Directory 쿼리

-   원격 프로시저 호출 서비스를 사용 하 여 원격 서버 또는 워크스테이션 관리

-   인쇄 서비스

-   클라이언트 서버 인증

-   블록 SMB (서버 메시지) 프로토콜 (일반 또는 CIFS 라고도 함)를 사용 하 여 원격 파일 액세스

-   분산된 파일 시스템 관리 및 추천

-   인트라넷 인증을 정보 IIS (인터넷 서비스)

-   인터넷 프로토콜 보안에 대 한 보안 기관 인증

-   사용자 도메인와 컴퓨터에 대 한 Active Directory 인증서 서비스에 인증서를 요청

위치: %windir%\Windows\System32\kerberos.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어 있는 **에 적용 됩니다** 이 항목을 및 Windows Server 2003와 Windows XP의 시작 부분에 목록 합니다.

**추가 Kerberos Kerberos SSP 및 리소스**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-KILE\]: Kerberos 프로토콜 확장](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS-SFU\]: Kerberos 프로토콜 확장: 사용자와 제한 된 위임 프로토콜 사양에 대 한 서비스](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   [향상 된 기능 Kerberos](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx) Windows vista

-   [Kerberos 인증에서 변경 사항](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) windows 7 

-   [Kerberos 인증 기술 참조](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>보안 지원 NTLM 공급자
NTLM Security 지원 공급자 (NTLM SSP)은 NTLM 시도 응답 인증 수 있도록 하 고 무결성 및 기밀성 옵션 협상 보안 지원 공급자 Interface (SSPI)에서 사용 되는 프로토콜 어디서 나 메시지 이진입니다. NTLM은 SSPI 인증을 사용 서버 메시지 블록 또는 CIFS 인증, HTTP 협상할 인증 (예를 들어, 인터넷 웹 인증), 및 원격 프로시저 호출 서비스에 대 한 등 어디서 나 사용 됩니다. NTLM 및 NTLM 버전 (NTLMv2) 2 NTLM SSP 포함 인증 프로토콜 합니다.

지원 되는 Windows 운영 체제 다음에 대 한 NTLM SSP 사용할 수 있습니다.

-   클라이언트/서버 인증

-   인쇄 서비스

-   CIFS SMB ()를 사용 하 여 파일 액세스

-   보안 원격 프로시저 호출 서비스나 DCOM 서비스

위치: %windir%\Windows\System32\msv1_0.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어 있는 **에 적용 됩니다** 이 항목을 및 Windows Server 2003와 Windows XP의 시작 부분에 목록 합니다.

**NTLM SSP 및 NTLM 프로토콜에 대 한 추가 리소스**

-   [MSV1_0 인증 패키지 (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   [NTLM 인증에서 변경 사항](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx) Windows 7에서 

-   [Microsoft Windows 등 NTLM](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [감사 및 NTLM 사용 가이드 제한](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>요약 보안 지원 공급자
요약 인증은 LDAP(Lightweight Directory Access Protocol) (LDAP) 및 웹 인증에 사용 되는 산업 표준을 합니다. 요약 인증 m d 5 해시 또는 메시지 요약으로 네트워크 자격 증명을 전송 합니다.

다음에 대 한 요약 SSP (Wdigest.dll) 사용 됩니다.

-   Internet Explorer 및 정보 IIS (인터넷 서비스) 액세스

-   LDAP 쿼리

위치: %windir%\Windows\System32\Digest.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어 있는 **에 적용 됩니다** 이 항목을 및 Windows Server 2003와 Windows XP의 시작 부분에 목록 합니다.

**요약 SSP 및 요약 프로토콜에 대 한 추가 리소스**

-   [(Microsoft 요약 인증)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-DPSP\]: 다이제스트 프로토콜 확장](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Schannel 보안 지원 공급자
사용자가 보안 웹 서버에 액세스 하려고 할 때와 같은 웹 기반 서버 인증을 위해는 Schannel (보안 채널) 사용 됩니다.

TLS 프로토콜을 SSL, 개인 커뮤니케이션 기술 (PCT) 프로토콜 및 데이터 그램 Transport Layer (DTLS) 프로토콜 키 공개 암호화를 기반으로 합니다. Schannel 이러한 모든 프로토콜을 제공합니다. 모든 Schannel 프로토콜 서버 클라이언트/모델을 사용 합니다. Schannel SSP 공개 키 인증서를 사용 하 여 자 인증 합니다. 자 인증, Schannel SSP 우선 순위 다음에 사용 되는 프로토콜인을 선택 합니다.

-   TLS (Layer Security) 버전 1.0 전송

-   전송 TLS (Layer Security) 1.1

-   TLS (Layer Security) 1.2 버전 전송

-   Secure Socket SSL 버전 2.0

-   Secure Socket 층 (SSL) 3.0 버전

-   개인 커뮤니케이션 기술 (PCT)

    **참고** PCT는 기본적으로 사용할 수 없습니다.

프로토콜을 선택 하는 클라이언트 및 서버를 지원할 수 있는 기본 인증 프로토콜 합니다. 예를 들어 서버 모든 Schannel 프로토콜을 지원 하 고 SSL 3.0 및 SSL 2.0 클라이언트를 지원, 인증 프로세스 SSL 3.0를 사용 합니다.

응용 프로그램에서 명시적으로 호출 DTLS 사용 됩니다. DTLS Schannel 공급자가 사용 되는 다른 프로토콜에 대 한 자세한 내용은 참조 [Schannel 보안 지원 공급자 기술 참조](../tls/schannel-security-support-provider-technical-reference.md)합니다.

위치: %windir%\Windows\System32\Schannel.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어 있는 **에 적용 됩니다** 이 항목을 및 Windows Server 2003와 Windows XP의 시작 부분에 목록 합니다.

> [!NOTE]
> Windows Server 2008 R2 및 Windows 7에서이 공급자에 TLS 1.2 도입 되었습니다. Windows 8 및 Windows Server 2012에서이 공급자에 DTLS 도입 되었습니다.

**Schannel SSP 및 TLS 및 SSL 프로토콜에 대 한 추가 리소스**

-   [보안 채널 (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [TLS/SSL 기술 참조](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS-TLSP\]: Layer Security (TLS) 프로필 전송](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>보안 지원 공급자 협상합니다
간단 하 고 보호 GSS-API 협상 메커니즘 (SPNEGO) 협상할 SSP에 대 한 기본 형성 whichcan 특정 인증 프로토콜 협상할 하는 데 사용 됩니다. 응용 프로그램에 네트워크에 로그온 할 때 SSPI 전화 하면 요청을 처리할 수 SSP 지정할 수 있습니다. 응용 프로그램 지정 협상할 SSP, 요청을 분석 하 고 고객이 구성 보안 정책에 따라 요청을 처리 하기 위한 작업이 적절 한 공급자 선택 합니다.

SPNEGO는 RFC 2478 지정 됩니다.

Windows 운영 체제의 지원 되는 버전 보안 협상 공급자 선택 NTLM 사이의 Kerberos 프로토콜을 지원 합니다. 선택 협상할 해당 프로토콜은 인증에 관련 된 시스템 중 한 곳에서 사용할 수 없는 호출 응용 프로그램 Kerberos 프로토콜을 사용 하 여 충분 한 정보를 제공 하지 않은 경우가 아니면 Kerberos 기본적으로 프로토콜 합니다.

위치: %windir%\Windows\System32\lsasrv.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어 있는 **에 적용 됩니다** 이 항목을 및 Windows Server 2003와 Windows XP의 시작 부분에 목록 합니다.

**추가 협상할 SSP 리소스**

-   [Microsoft Windows 등 협상](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: 간단 하 고 보호 GSS-API 협상 메커니즘 (SPNEGO) 확장](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[MS-N2HT\]: 협상할 및 Nego2 HTTP 인증 사양 프로토콜](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>자격 증명 보안 지원 공급자
자격 증명 보안 서비스 공급자 (CredSSP) 새 Terminal Services 및 원격 데스크톱 서비스 세션을 시작 하는 경우 단일 로그온 (SSO) 사용자 환경을 제공 합니다. CredSSP은 클라이언트의 정책에 따라 (서버 쪽 SSP)을 통해 대상 서버에 사용자의 자격 증명을 위임 클라이언트 컴퓨터에서 (클라이언트 측 SSP 통해) 응용 프로그램이 있습니다. 그룹 정책을 사용 하 여 CredSSP 정책을 구성 및 자격 증명 위임 기본적으로 꺼져 있습니다.

위치: %windir%\Windows\System32\credssp.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 된는 **에 적용 됩니다** 이 항목의 시작 부분에 목록입니다.

**자격 증명 SSP에 대 한 추가 리소스**

-   [\[MS-CSSP\]: 보안 지원 (CredSSP) 공급자 프로토콜 사양 자격 증명](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [보안 서비스 공급자와 SSO for Terminal 자격 증명 로그온 서비스](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>확장 보안 지원 공급자 협상합니다
확장 협상할 (NegoExts)는 인증 패키지 협상 규칙이 NTLM 또는 Kerberos 프로토콜을 사용 하는 응용 프로그램 및 시나리오에서 구현 Microsoft와 기타 소프트웨어 회사에 대 한 합니다.

이 확장 협상 패키지에 다음과 같은 경우 가능합니다.

-   **연결 된 시스템 내에서 다양 한 클라이언트 공급 일** 문서 SharePoint 사이트에 액세스할 수 있으며 모든 기능을 갖춘 Microsoft Office 응용 프로그램을 사용 하 여 편집할 수 있습니다.

-   **Microsoft Office 서비스에 대 한 다양 한 클라이언트 지원 합니다.** 사용자가 Microsoft Office 서비스에 로그인 하 고 모든 기능을 갖춘 Microsoft Office 응용 프로그램을 사용할 수 있습니다.

-   **호스트 된 Microsoft Exchange Server 및 Outlook 합니다.** 웹에서 Exchange Server 호스트 때문에 도메인 신뢰 하지 있습니다. Outlook은 Windows Live 서비스를 사용 하 여 사용자를 인증 합니다.

-   **다양 한 수정 클라이언트 컴퓨터와 클라이언트 가용성 합니다.** 운영 체제의 네트워킹과 인증 구성 요소 사용 됩니다.

Windows 협상할 패키지 Kerberos 및 NTLM와 마찬가지로 NegoExts SSP 동일한 방식으로 처리 합니다. NegoExts.dll 시작 시 로컬 시스템 기관 (LSA)으로 로드 됩니다. 인증 요청 요청의 원본에 따라 수신 되 면 NegoExts 협상 지원된 규칙이 간에 합니다. 자격 증명 및 정책에를 암호화 하 고 해당 정보 적절 한 SSP 보안 토큰을 만들 위치를 보냅니다를 수집 합니다.

NegoExts에서 지 원하는 규칙이 Kerberos NTLM 등 독립 실행형 규칙이 되지 않습니다. 따라서 NegoExts SSP 내 어떤 이유로 든 인증 방법을 실패 하면 인증 오류 메시지가 표시 되거나 될 기록 합니다. 인증 재협상 또는 대체 방법이 더 될 수 있습니다.

위치: %windir%\Windows\System32\negoexts.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어 있는 **에 적용 됩니다** Windows Server 2008 및 Windows Vista 제외 하 고이 항목의 시작 부분에 목록 합니다.

### <a name="BKMK_PKU2USSP"></a>PKU2U 보안 지원 공급자
PKU2U 프로토콜 도입 하 고 Windows 7 및 Windows Server 2008 R2 SSP으로 구현 되었습니다. 이 SSP 미디어 및 파일 공유 홈 그룹을 Windows 7에서 도입 이라는 기능을 통해 특히 피어 투 피어 인증을 수 있습니다. 이 기능 도메인의 회원 없는 컴퓨터 간에 공유를 허용 합니다.

위치: %windir%\Windows\System32\pku2u.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어 있는 **에 적용 됩니다** Windows Server 2008 및 Windows Vista 제외 하 고이 항목의 시작 부분에 목록 합니다.

**PKU2U SSP 및 PKU2U 프로토콜에 대 한 추가 리소스**

-   [온라인 Id 통합 소개](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>보안 지원 공급자 선택
Windows SSPI 설치 된 보안 지원 공급자를 통해 지원 프로토콜 중 하나를 사용할 수 있습니다. 그러나 운영 체제 Windows Server 실행 지정된 컴퓨터와 동일한 SSP 패키지를 지원 하므로 클라이언트 및 서버를 지 원하는 모두 프로토콜을 사용 하도록 조정 해야 합니다. Windows Server 클라이언트 컴퓨터와 가능한 하지만 운영 체제 계속 허용 클라이언트 컴퓨터와 클라이언트 응용 프로그램을 실시 하는데 Kerberos 프로토콜을 지원 하지 않는 경우 강력한 표준 기반 프로토콜 Kerberos 프로토콜을 사용 하 여 응용 프로그램 선호 합니다.

인증 수 있는 장소 두 통신 전에 컴퓨터 데 동의 해야 프로토콜을 모두 지원할 수 있습니다. 각 컴퓨터 SSPI을 통해 사용할 수 없는 모든 프로토콜에 대 한 적절 한 SSP 되어 있어야 예를 들어 클라이언트 컴퓨터 및 서버가 Kerberos 인증 프로토콜을 사용 하 여 둘 다 지원 해야 Kerberos v 5. Windows Server는 함수를 사용 하 여 **EnumerateSecurityPackages** 지 기능 컴퓨터 및 작업에서 지원 되는 규칙이 식별 하는 합니다.

인증 프로토콜 선택 다음과 같은 두 가지 방법 중 하나에서 처리 수 있습니다.

1.  [하나의 인증 프로토콜](#BKMK_SingleAuth)

2.  [협상할 옵션](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>하나의 인증 프로토콜
서버에 지정 된 단일도 괜찮나요 프로토콜이 때 지정 된 프로토콜이 나 통신 실패 클라이언트 컴퓨터 지원 해야 합니다. 단일도 괜찮나요 프로토콜 지정 된 인증 교환 수행 다음과 같은 됩니다.

1.  클라이언트 컴퓨터 서비스에 대 한 액세스를 요청합니다.

2.  서버 요청에 응답 하 고 사용 되는 프로토콜을 지정 합니다.

3.  클라이언트 컴퓨터 회신 및를 지정한 프로토콜을 지원 하는지 확인의 콘텐츠를 검사 합니다. 인증 계속 경우 클라이언트 컴퓨터에서 지정된 프로토콜을 지원 합니다. 클라이언트 컴퓨터 프로토콜을 지원 하지 클라이언트 컴퓨터 리소스에 액세스할 수 있는 권한이 있는지 여부에 관계 없이 인증 실패 합니다.

### <a name="BKMK_Negotiate"></a>협상할 옵션
클라이언트 및 서버 시도할도 괜찮나요 프로토콜을 찾을 수 있도록 협상 옵션을 사용할 수 있습니다. 이 간단 하 고 보호 GSS-API 협상 메커니즘 (SPNEGO)에 따라 됩니다. 인증 인증 프로토콜을 결정 하는 옵션을 시작 SPNEGO exchange 수행 다음과 같은 됩니다.

1.  클라이언트 컴퓨터 서비스에 대 한 액세스를 요청합니다.

2.  서버 인증 프로토콜 지원할 수 있는 인증 요구 또는 그 첫 번째 선택 하는 프로토콜에 따라 응답 목록을으로 회신 합니다. 예를 들어, 서버가 Kerberos 프로토콜 및 NTLM 나열 하 고 Kerberos 인증 답장을 보내려면 될 수 있습니다.

3.  클라이언트 컴퓨터 회신 및를 지정 프로토콜을 지원 하는지 확인의 콘텐츠를 검사 합니다.

    -   클라이언트 컴퓨터의 기본 프로토콜을 지 원하는 경우 인증 진행 됩니다.

    -   클라이언트 컴퓨터의 기본 프로토콜을 지원 하지 한다면 서버에서 나열 된 다른 프로토콜 중 하나를 지원지 않습니다 클라이언트 컴퓨터 서버를 인증 프로토콜을 지원 하 고 인증 진행 되는 알 수 있습니다.

    -   클라이언트 컴퓨터 나열된 프로토콜을 지원 하지 않는 경우에 인증 교환 실패 합니다.

## <a name="see-also"></a>참조 하십시오
[Windows 인증 건축물](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


