---
title: 보안 지원 공급자 인터페이스 아키텍처
description: Windows Server 보안
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827024"
---
# <a name="security-support-provider-interface-architecture"></a>보안 지원 공급자 인터페이스 아키텍처

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가 위한이 참조 항목에서는 보안 지원 공급자 인터페이스 (SSPI) 아키텍처 내에서 사용 되는 Windows 인증 프로토콜을 설명 합니다.

Microsoft 보안 지원 공급자 인터페이스 (SSPI)은 Windows 인증을 위한 기초입니다. 응용 프로그램 및 인프라 서비스 인증을 필요로 하는 SSPI를 사용 하 여 제공 합니다.

SSPI는의 일반 보안 서비스 API (GSSAPI) Windows Server 운영 체제의 구현입니다. GSSAPI에 대 한 자세한 내용은 RFC 2743 및 IETF RFC 데이터베이스에서 RFC 2744를 참조 하십시오.

기본 보안 지원 공급자 (Ssp) Windows에서 특정 인증 프로토콜을 호출 하는 Dll로 SSPI에 통합 됩니다. 이러한 기본 Ssp는 다음 섹션에 설명 되어 있습니다. SSPI를 사용 하 여 작동 하는 경우 추가 Ssp은 통합할 수 있습니다.

다음 그림에 표시 된 것과 같이 Windows에서 SSPI 클라이언트 컴퓨터와 서버 간의 기존 통신 채널을 통해 인증 토큰을 전달 하는 메커니즘을 제공 합니다. 두 컴퓨터 또는 장치를 안전 하 게 통신할 수 있도록 인증 경우 인증에 대 한 요청에서 현재 사용 중인 네트워크 프로토콜에 관계 없이 인증 프로세스를 완료 하는 SSPI로 라우팅됩니다. SSPI는 투명 한 이진 대형 개체를 반환합니다. 이러한 작업은 시점에서 SSPI 계층에 전달 될 수는 응용 프로그램 간에 전달 됩니다. 따라서 SSPI 보안 시스템 인터페이스를 변경 하지 않고 컴퓨터나 네트워크에서 사용할 수 있는 다양 한 보안 모델을 사용 하도록 응용을 프로그램을 수 있습니다.

![보안 지원 공급자 인터페이스 아키텍처를 보여 주는 다이어그램](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

다음 섹션에서는 SSPI 사용 하 여 상호 작용 하는 기본 Ssp를 설명 합니다. Ssp는 비보안 네트워크 환경에서 보안 통신을 승격 하려면 다음 Windows 운영 체제에서 다른 방법으로 사용 됩니다.

-   [Kerberos 보안 지원 공급자](#BKMK_KerbSSP)

-   [NTLM 보안 지원 공급자](#BKMK_NTLMSSP)

-   [다이제스트 보안 지원 공급자](#BKMK_DigestSSP)

-   [Schannel 보안 지원 공급자](#BKMK_SchannelSSP)

-   [보안 지원 공급자를 협상 합니다.](#BKMK_NegoSSP)

-   [Credential Security Support Provider](#BKMK_CredSSP)

-   [확장 보안 지원 공급자를 협상 합니다.](#BKMK_NegoExtsSSP)

-   [PKU2U Security Support Provider](#BKMK_PKU2USSP)

이 항목에도 포함 합니다.

[보안 지원 공급자 선택](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Kerberos 보안 지원 공급자
이 SSP는 Microsoft가 구현한 대로 Kerberos 버전 5 프로토콜을 사용 합니다. 이 프로토콜은 네트워크 작업 그룹의 RFC 4120와 초안 버전을 기반으로 합니다. 대화형 로그온에 대 한 암호 또는 스마트 카드를 사용 하 여 사용 되는 업계 표준 프로토콜입니다. Windows에서 서비스에 대 한 기본 인증 방법 이기도합니다.

모든 도메인 서비스는 Kerberos SSP 지원 되었으므로 Kerberos 프로토콜 기본 인증 프로토콜이 Windows 2000 년 이후로, 이러한 서비스는 다음과 같습니다.

-   LDAP Lightweight Directory Access Protocol ()를 사용 하는 active Directory 쿼리

-   원격 프로시저 호출 서비스를 사용 하는 원격 서버 또는 워크스테이션 관리

-   인쇄 서비스

-   클라이언트-서버 인증

-   (일반 인터넷 파일 시스템 또는 CIFS 라고도 함) 서버 메시지 블록 (SMB) 프로토콜을 사용 하 여 원격 파일 액세스

-   분산된 파일 시스템 관리 및 조회

-   인터넷 정보 서비스 (IIS)에 대 한 인트라넷 인증

-   인터넷 프로토콜 보안 (IPsec)에 대 한 보안 기관 인증

-   도메인 사용자 및 컴퓨터에 대 한 Active Directory 인증서 서비스에 인증서 요청

Location: %windir%\Windows\System32\kerberos.dll

에 지정 된 버전에서 기본적으로이 공급자가 포함 되어는 **적용할** 이 항목에서는 및 Windows Server 2003 및 Windows XP의 시작 부분에 있는 목록입니다.

**Kerberos 프로토콜 및 Kerberos SSP에 대 한 추가 리소스**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-KILE\]: Kerberos 프로토콜 확장](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS-SFU\]: 섹션(영문)을 사용자 서비스 및 제한 위임 프로토콜 사양](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   [Kerberos 기능이 향상](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx) Windows vista

-   [Kerberos 인증의 변경 내용](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) Windows 7에 대 한 

-   [Kerberos 인증 기술 참조](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>NTLM 보안 지원 공급자
NTLM 보안 지원 공급자 (SSP (NTLM)은 NTLM 챌린지-응답 인증을 허용 하 고 무결성 및 기밀성 옵션 협상 보안 지원 공급자 인터페이스 (SSPI)에서 사용 되는 프로토콜 메시지는 이진입니다. 서버 메시지 블록 또는 CIFS 인증, HTTP Negotiate 인증 (예를 들어 인터넷 웹 인증) 및 원격 프로시저 호출 서비스를 포함 하 여 SSPI 인증을 사용 하는 경우 항상 NTLM이 사용 됩니다. NTLM 및 NTLM 버전 2 (NTLMv2)을 포함 하는 NTLM SSP 인증 프로토콜입니다.

지원 되는 Windows 운영 체제는 다음에 대 한 NTLM SSP를 따르면 됩니다.

-   클라이언트/서버 인증

-   인쇄 서비스

-   CIFS (SMB)를 사용 하 여 파일 액세스

-   원격 프로시저 호출 서비스 또는 DCOM 서비스 보호

Location: %windir%\Windows\System32\msv1_0.dll

에 지정 된 버전에서 기본적으로이 공급자가 포함 되어는 **적용할** 이 항목에서는 및 Windows Server 2003 및 Windows XP의 시작 부분에 있는 목록입니다.

**NTLM 프로토콜 및 NTLM SSP에 대 한 추가 리소스**

-   [MSV1_0 인증 패키지 (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   [NTLM 인증의 변경 내용](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx) Windows 7에서 

-   [Microsoft NTLM (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [감사 및 제한 NTLM 사용 가이드](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>다이제스트 보안 지원 공급자
다이제스트 인증은 LDAP Lightweight Directory Access Protocol () 및 웹 인증에 사용 되는 업계 표준입니다. 다이제스트 인증 MD5 해시 또는 메시지 다이제스트가로 네트워크를 통해 자격 증명을 전송 합니다.

다이제스트 SSP (Wdigest.dll)는 다음 용도로 사용 됩니다.

-   Internet Explorer 및 인터넷 정보 서비스 (IIS)에 대 한 액세스

-   LDAP 쿼리

Location: %windir%\Windows\System32\Digest.dll

에 지정 된 버전에서 기본적으로이 공급자가 포함 되어는 **적용할** 이 항목에서는 및 Windows Server 2003 및 Windows XP의 시작 부분에 있는 목록입니다.

**다이제스트 프로토콜 및 다이제스트 SSP에 대 한 추가 리소스**

-   [Microsoft 다이제스트 인증 (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-DPSP\]: 다이제스트 프로토콜 확장](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Schannel 보안 지원 공급자
보안 채널 (Schannel)는 사용자가 보안 웹 서버에 액세스 하려고 할 때와 같은 웹 기반 서버 인증에 사용 됩니다.

TLS 프로토콜, SSL 프로토콜, 기술 PCT (Private Communications) 프로토콜 및 데이터 그램 전송 계층 (DTLS) 프로토콜을 기반으로 공개 키 암호화 합니다. Schannel 이러한 모든 프로토콜을 제공합니다. 모든 Schannel 프로토콜에서는 클라이언트/서버 모델이 사용됩니다. Schannel SSP는 공개 키 인증서를 사용하여 당사자를 인증합니다. 당사자를 인증할 때 Schannel SSP는 다음 우선 순위에서 프로토콜을 선택 합니다.

-   전송 계층 보안 (TLS) 버전 1.0

-   전송 계층 보안 (TLS) 버전 1.1

-   전송 계층 보안 (TLS) 버전 1.2

-   보안 소켓 레이어 (SSL) 버전 2.0

-   보안 소켓 레이어 (SSL) 버전 3.0

-   Private Communications Technology PCT)

    **참고** PCT 기본적으로 비활성화 됩니다.

선택한 프로토콜에는 클라이언트와 서버에서 지원할 수 있는 기본 인증 프로토콜이입니다. 예를 들어, 하는 서버는 모든 Schannel 프로토콜을 지원 하 고 클라이언트는 SSL 3.0 및 SSL 2.0 지원, 인증 프로세스는 SSL 3.0을 사용 합니다.

DTLS는 응용 프로그램에서 명시적으로 호출 하는 경우에 사용 됩니다. DTLS 및 Schannel 공급자에서 사용 되는 다른 프로토콜에 대 한 자세한 내용은 참조 하세요. [Schannel 보안 지원 공급자 기술 참조](../tls/schannel-security-support-provider-technical-reference.md)합니다.

Location: %windir%\Windows\System32\Schannel.dll

에 지정 된 버전에서 기본적으로이 공급자가 포함 되어는 **적용할** 이 항목에서는 및 Windows Server 2003 및 Windows XP의 시작 부분에 있는 목록입니다.

> [!NOTE]
> TLS 1.2는 Windows Server 2008 R2 및 Windows 7에는이 공급자에서 도입 되었습니다. DTLS는 Windows Server 2012 및 Windows 8에는이 공급자에서 도입 되었습니다.

**TLS 및 SSL 프로토콜 및 Schannel SSP에 대 한 추가 리소스**

-   [보안 채널 (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [TLS/SSL 기술 참조](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS-TLSP\]: 전송 계층 보안 (TLS) 프로필](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>보안 지원 공급자를 협상 합니다.
간편 하 고 Protected GSS-API Negotiation 메커니즘 (SPNEGO) 협상 SSP에 대 한 기본을 형성 whichcan 특정 인증 프로토콜을 협상 하는 데 사용할 수 있습니다. 응용 프로그램 네트워크에 로그온 하는 SSPI를 호출할 때 요청을 처리할 SSP를 지정할 수 있습니다. 협상 SSP를 지정 하는 응용 프로그램에서 요청을 분석 하 고 고객이 구성한 보안 정책을 기반으로 요청을 처리 하는 데 적절 한 공급자를 선택 합니다.

SPNEGO는 2478 RFC에에서 지정 됩니다.

지원 되는 Windows 운영 체제 버전, 보안 협상 공급자 선택 Kerberos 프로토콜 및 NTLM 사이 지원 합니다. 선택 협상 인증을 관련 된 시스템 중 하나에서 해당 프로토콜을 사용할 수 없는 호출 응용 프로그램 Kerberos 프로토콜을 사용 하도록 충분 한 정보를 제공 하지 않은 경우가 아니면 기본적으로 Kerberos 프로토콜입니다.

Location: %windir%\Windows\System32\lsasrv.dll

에 지정 된 버전에서 기본적으로이 공급자가 포함 되어는 **적용할** 이 항목에서는 및 Windows Server 2003 및 Windows XP의 시작 부분에 있는 목록입니다.

**협상 SSP에 대 한 추가 리소스**

-   [Microsoft 협상 (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: 간단 하 고 Protected GSS-API 협상 메커니즘 (SPNEGO) 확장](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[MS-N2HT\]: 협상 및 Nego2 HTTP 인증 프로토콜 사양](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>Credential Security Support Provider
Credential Security Service Provider (CredSSP) 새 터미널 서비스 및 원격 데스크톱 서비스 세션을 시작 하는 경우는 single sign-on (SSO) 사용자 환경을 제공 합니다. CredSSP는 클라이언트의 정책에 따라 (서버 쪽 SSP)를 통해 대상 서버에 응용 프로그램을 (클라이언트 쪽 SSP를 사용)가 클라이언트 컴퓨터에서 사용자의 자격 증명을 위임할 수 있습니다. CredSSP 정책은 그룹 정책을 사용 하 여 구성 됩니다 하 고 자격 증명을 위임할 기본적으로 해제 됩니다.

Location: %windir%\Windows\System32\credssp.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어는 **에 적용 됩니다** 이 항목의 시작 부분에 있는 목록입니다.

**자격 증명 SSP에 대 한 추가 리소스**

-   [\[MS-CSSP\]: 자격 증명 보안 지원 공급자 (CredSSP) 프로토콜 사양](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [터미널에 대 한 보안 서비스 공급자와 SSO 자격 증명 로그온 서비스](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>확장 보안 지원 공급자를 협상 합니다.
확장을 협상 (NegoExts)은 응용 프로그램 및 시나리오 구현한 Microsoft 및 기타 소프트웨어 회사에 대 한 협상 Ssp가 아닌 NTLM 또는 Kerberos 프로토콜을 사용 하는 인증 패키지 있습니다.

이 확장 협상 패키지에 다음과 같은 시나리오를 허용합니다.

-   **페더레이션된 시스템 내에서 다양 한 클라이언트 가용성입니다.** 문서를 SharePoint 사이트에 액세스할 수 있습니다 하 고 모든 기능을 갖춘 Microsoft Office 응용 프로그램을 사용 하 여 편집할 수 있습니다.

-   **Microsoft Office 서비스에 대 한 리치 클라이언트를 지원 합니다.** 사용자는 Microsoft Office 서비스에 로그인 하 고 모든 기능을 갖춘 Microsoft Office 응용 프로그램을 사용할 수 있습니다.

-   **Hosted Microsoft Exchange Server 및 Outlook입니다.** Exchange Server는 웹에서 호스트 되므로 설정 도메인 트러스트 되지 않은 경우 Outlook에서 사용자를 인증 하도록 Windows Live 서비스를 사용 합니다.

-   **클라이언트 컴퓨터와 서버 간에 다양 한 클라이언트 가용성입니다.** 운영 체제의 네트워킹 및 인증 구성 요소가 사용 됩니다.

Kerberos 및 NTLM에 대해서와 마찬가지로 동일한 방식으로 NegoExts SSP를 처리 하는 Windows 협상 패키지 합니다. NegoExts.dll 시작 시 로컬 시스템 기관 (LSA)에 로드 됩니다. 인증 요청을 받으면 요청의 원본을 기반으로 NegoExts 지원 되는 Ssp 사이 협상 합니다. 정책을 확인 하 고 자격 증명을 암호화 하 고 보안 토큰을 만들 위치를 적절 한 ssp 해당 정보를 보냅니다를 수집 합니다.

NegoExts 지 Ssp Kerberos 및 NTLM 같은 독립 실행형 Ssp 않습니다. 따라서 NegoExts SSP 내의 어떤 이유로 인증 메서드가 실패할 때는 인증 오류 메시지는 표시 하거나 기록 합니다. 재협상 또는 대체 (fallback) 인증 방법이 더 있을 수 있습니다.

위치: %windir%\Windows\System32\negoexts.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어는 **에 적용 됩니다** Windows Server 2008 및 Windows Vista를 제외한이 항목의 시작 부분에 있는 목록입니다.

### <a name="BKMK_PKU2USSP"></a>PKU2U Security Support Provider
PKU2U 프로토콜 도입 되었으며 Windows 7 및 Windows Server 2008 R2에서 SSP으로 구현 합니다. 이 SSP에는 Windows 7에 도입 된 홈 그룹 이라는 기능을 공유 하는 파일 및 미디어를 통해 특히 피어-투-피어 인증을 설정 합니다. 도메인의 구성원이 아닌 컴퓨터 간에 공유 기능을 허용 합니다.

Location: %windir%\Windows\System32\pku2u.dll

이 공급자에 지정 된 버전에서 기본적으로 포함 되어는 **에 적용 됩니다** Windows Server 2008 및 Windows Vista를 제외한이 항목의 시작 부분에 있는 목록입니다.

**PKU2U 프로토콜과 PKU2U SSP에 대 한 추가 리소스**

-   [온라인 Id 통합 소개](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>보안 지원 공급자 선택
Windows SSPI 설치 보안 지원 공급자를 통해 지원 되는 프로토콜 중 하나를 사용할 수 있습니다. 그러나 일부 운영 체제에서 Windows Server를 실행 하는 지정 된 컴퓨터와 동일한 SSP 패키지를 지원 하므로 클라이언트와 서버 둘 다 지 원하는 프로토콜을 사용 하려면 협상 해야 합니다. 클라이언트 컴퓨터와 클라이언트 컴퓨터 및 클라이언트는 Kerberos를 지원 하지 않는 응용 프로그램을 허용 하지만 운영 체제 계속 하는 경우 Kerberos 프로토콜을 강력한 표준 기반 프로토콜을 사용 하도록 응용 프로그램에서 선호 하는 Windows Server 인증 프로토콜입니다.

두 곳 통신 인증 수행 되기 전 컴퓨터는 프로토콜을 동의 해야 합니다 모두 지원할 수 있습니다. SSPI를 통해 사용할 수 있으려면 모든 프로토콜에 대 한 각 컴퓨터에는 적절 한 SSP가 있어야 합니다. 예를 들어, 클라이언트 컴퓨터 및 Kerberos 인증 프로토콜을 사용 하는 서버를 모두 지원 해야 Kerberos v5 합니다. 함수를 사용 하 여 Windows Server **EnumerateSecurityPackages** 기능의 해당 Ssp는 Ssp는 컴퓨터 및에 지를 식별 하는 합니다.

인증 프로토콜 선택 다음 두 가지 방법 중 하나에서 처리할 수 있습니다.

1.  [단일 인증 프로토콜](#BKMK_SingleAuth)

2.  [옵션을 협상 합니다.](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>단일 인증 프로토콜
서버에서 허용 하는 단일 프로토콜을 지정 하면 클라이언트 컴퓨터의 지정 된 프로토콜 또는 통신 실패를 지원 해야 합니다. 에서는 단일 허용 프로토콜을 지정 하면 인증 교환이 이루어지는 다음과 같습니다.

1.  클라이언트 컴퓨터를 서비스에 대 한 액세스를 요청합니다.

2.  서버 요청에 응답 하 고 사용 되는 프로토콜을 지정 합니다.

3.  클라이언트 컴퓨터에 지정된 된 프로토콜을 지원 하는지 여부를 확인 하 고 응답의 내용을 검사 합니다. 인증을 계속 하는 경우 클라이언트 컴퓨터는 지정 된 프로토콜을 지원 합니다. 클라이언트 컴퓨터는 프로토콜을 지원 하지 않는 클라이언트 컴퓨터 리소스에 액세스할 수 있는 권한이 있는지 여부에 관계 없이 인증이 실패 합니다.

### <a name="BKMK_Negotiate"></a>옵션을 협상 합니다.
클라이언트와 서버에 허용 되는 프로토콜을 찾으려고 시도 허용 하도록 negotiate 옵션을 사용할 수 있습니다. 이 간단한 및 Protected GSS-API Negotiation 메커니즘 (SPNEGO)에 기반 합니다. 인증 프로토콜을 협상 하는 옵션을 사용 하 여 인증을 시작 하는 경우 SPNEGO 교환이 이루어지는 다음과 같습니다.

1.  클라이언트 컴퓨터를 서비스에 대 한 액세스를 요청합니다.

2.  서버 목록 지원할 수 있는 인증 프로토콜 및 인증 챌린지 또는 응답을 해당 첫 번째 선택 된 프로토콜을 기반으로 응답 합니다. 예를 들어 서버 NTLM 및 Kerberos 프로토콜을 나열 및 Kerberos 인증 응답을 보낼 수 있습니다.

3.  클라이언트 컴퓨터에 지정 된 프로토콜 중 하나를 지원 하는지 여부를 확인 하 고 응답의 내용을 검사 합니다.

    -   클라이언트 컴퓨터는 기본 프로토콜을 지 원하는 경우에 인증이 진행 됩니다.

    -   클라이언트 컴퓨터는 기본 프로토콜을 지원 하지 않지만 서버에서 나열 된 다른 프로토콜 중 하나에서는, 하는 경우 클라이언트 컴퓨터에 원하는 지 원하는 인증 프로토콜 및 인증을 진행 하는 서버 수 있습니다.

    -   클라이언트 컴퓨터는 나열 된 프로토콜 지원 하지 않는 경우 인증 교환이 실패 합니다.

## <a name="see-also"></a>참조
[Windows 인증 아키텍처](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


