---
title: 보안 지원 공급자 인터페이스 아키텍처
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 4db407b24b00bc8313d2e17f1fcf55d9fa160c8c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403305"
---
# <a name="security-support-provider-interface-architecture"></a>보안 지원 공급자 인터페이스 아키텍처

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 참조 항목에서는 SSPI (Security Support Provider Interface) 아키텍처에서 사용 되는 Windows 인증 프로토콜에 대해 설명 합니다.

Microsoft SSPI (Security Support Provider Interface)는 Windows 인증의 기반입니다. 인증이 필요한 응용 프로그램 및 인프라 서비스는 SSPI를 사용 하 여 제공 합니다.

SSPI는 Windows Server 운영 체제에서 GSSAPI (Generic Security Service API)의 구현입니다. GSSAPI에 대 한 자세한 내용은 IETF RFC 데이터베이스에서 RFC 2743 및 RFC 2744를 참조 하세요.

Windows에서 특정 인증 프로토콜을 호출 하는 기본 Ssp (보안 지원 공급자)는 Dll로 SSPI에 통합 됩니다. 이러한 기본 Ssp는 다음 섹션에 설명 되어 있습니다. SSPI를 사용 하 여 작업할 수 있는 경우 추가 Ssp를 통합할 수 있습니다.

다음 그림에 표시 된 것 처럼 Windows의 SSPI는 클라이언트 컴퓨터와 서버 간의 기존 통신 채널을 통해 인증 토큰을 전달 하는 메커니즘을 제공 합니다. 안전 하 게 통신할 수 있도록 두 컴퓨터 또는 장치를 인증 해야 하는 경우 인증 요청은 현재 사용 중인 네트워크 프로토콜과 관계 없이 인증 프로세스를 완료 하는 SSPI로 라우팅됩니다. SSPI는 투명 한 이진 개체를 반환 합니다. 이러한 응용 프로그램은 응용 프로그램 간에 전달 되며,이 시점에서 SSPI 계층으로 전달 될 수 있습니다. 따라서 SSPI를 통해 응용 프로그램은 보안 시스템에 대 한 인터페이스를 변경 하지 않고 컴퓨터 또는 네트워크에서 사용할 수 있는 다양 한 보안 모델을 사용할 수 있습니다.

![보안 지원 공급자 인터페이스 아키텍처를 보여 주는 다이어그램](../media/security-support-provider-interface-architecture/AuthN_SecuritySupportProviderInterfaceArchitecture.jpg)

다음 섹션에서는 SSPI와 상호 작용 하는 기본 Ssp에 대해 설명 합니다. Ssp는 보안 되지 않은 네트워크 환경에서 보안 통신을 승격 하는 Windows 운영 체제의 다양 한 방법으로 사용 됩니다.

-   [Kerberos 보안 지원 공급자](#BKMK_KerbSSP)

-   [NTLM 보안 지원 공급자](#BKMK_NTLMSSP)

-   [다이제스트 보안 지원 공급자](#BKMK_DigestSSP)

-   [Schannel 보안 지원 공급자](#BKMK_SchannelSSP)

-   [보안 지원 공급자 협상](#BKMK_NegoSSP)

-   [자격 증명 보안 지원 공급자](#BKMK_CredSSP)

-   [Negotiate 확장 보안 지원 공급자](#BKMK_NegoExtsSSP)

-   [PKU2U 보안 지원 공급자](#BKMK_PKU2USSP)

이 항목에도 포함 되어 있습니다.

[보안 지원 공급자 선택](security-support-provider-interface-architecture.md#BKMK_SecuritySupportProviderSelection)

### <a name="BKMK_KerbSSP"></a>Kerberos 보안 지원 공급자
이 SSP는 Microsoft에서 구현한 Kerberos 버전 5 프로토콜만 사용 합니다. 이 프로토콜은 네트워크 작업 그룹의 RFC 4120 및 초안 수정 버전을 기반으로 합니다. 암호 또는 스마트 카드를 사용 하는 대화형 로그온에 사용 되는 업계 표준 프로토콜입니다. Windows의 서비스에 대 한 기본 인증 방법 이기도 합니다.

Kerberos 프로토콜은 Windows 2000 이후의 기본 인증 프로토콜 이기 때문에 모든 도메인 서비스가 Kerberos SSP를 지원 합니다. 이러한 서비스는 다음과 같습니다.

-   LDAP (Lightweight Directory Access Protocol)를 사용 하는 Active Directory 쿼리

-   원격 프로시저 호출 서비스를 사용 하는 원격 서버 또는 워크스테이션 관리

-   인쇄 서비스

-   클라이언트-서버 인증

-   SMB (서버 메시지 블록) 프로토콜 (일반 인터넷 파일 시스템 또는 CIFS 라고도 함)을 사용 하는 원격 파일 액세스

-   분산 파일 시스템 관리 및 조회

-   인터넷 정보 서비스에 대 한 인트라넷 인증 (IIS)

-   IPsec (인터넷 프로토콜 보안)에 대 한 보안 기관 인증

-   도메인 사용자 및 컴퓨터에 대 한 인증서 서비스를 Active Directory 하는 인증서 요청

위치:%windir%\Windows\System32\kerberos.dll

이 공급자는이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전 및 windows Server 2003 및 windows XP에 기본적으로 포함 되어 있습니다.

**Kerberos 프로토콜 및 Kerberos SSP에 대 한 추가 리소스**

-   [Microsoft Kerberos (Windows)](https://msdn.microsoft.com/library/aa378747(VS.85).aspx)

-   [\[MS-KD\]: Kerberos 프로토콜 확장](https://msdn.microsoft.com/library/cc233855(PROT.10).aspx)

-   [\[MS SFU\]: Kerberos 프로토콜 확장: 사용자 서비스 및 제한 위임 프로토콜 사양](https://msdn.microsoft.com/library/cc246071(PROT.13).aspx)

-   [Kerberos SSP/AP (Windows)](https://msdn.microsoft.com/library/aa377942(VS.85).aspx)

-   Windows Vista의 [Kerberos 향상 기능](https://technet.microsoft.com/library/cc749438(v=ws.10).aspx)

-   Windows 7에 대 한 [Kerberos 인증의 변경 내용](https://technet.microsoft.com/library/dd560670(v=ws.10).aspx) 

-   [Kerberos 인증 기술 참조](https://technet.microsoft.com/library/cc739058(v=ws.10).aspx)

### <a name="BKMK_NTLMSSP"></a>NTLM 보안 지원 공급자
Ntlm SSP (NTLM 보안 지원 공급자)는 SSPI (Security Support Provider Interface)에서 NTLM 챌린지 응답 인증을 허용 하 고 무결성 및 기밀성 옵션을 협상 하는 데 사용 하는 이진 메시징 프로토콜입니다. NTLM은 서버 메시지 블록 또는 CIFS 인증, HTTP Negotiate 인증 (예: 인터넷 웹 인증) 및 원격 프로시저 호출 서비스를 비롯 하 여 SSPI 인증이 사용 되는 모든 위치에 사용 됩니다. NTLM SSP는 NTLM 및 ntlm 버전 2 (NTLMv2) 인증 프로토콜을 포함 합니다.

지원 되는 Windows 운영 체제는 NTLM SSP를 사용 하 여 다음을 수행할 수 있습니다.

-   클라이언트/서버 인증

-   인쇄 서비스

-   CIFS (SMB)를 사용 하 여 파일 액세스

-   보안 원격 프로시저 호출 서비스 또는 DCOM 서비스

Location:%windir%\Windows\System32\ msv1_0 .dll

이 공급자는이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전 및 windows Server 2003 및 windows XP에 기본적으로 포함 되어 있습니다.

**NTLM 프로토콜 및 NTLM SSP에 대 한 추가 리소스**

-   [MSV1_0 인증 패키지 (Windows)](https://msdn.microsoft.com/library/aa378753(VS.85).aspx)

-   Windows 7에서 [NTLM 인증의 변경 내용](https://technet.microsoft.com/library/dd566199(v=ws.10).aspx) 

-   [Microsoft NTLM (Windows)](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)

-   [NTLM 사용 가이드 감사 및 제한](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)

### <a name="BKMK_DigestSSP"></a>다이제스트 보안 지원 공급자
다이제스트 인증은 LDAP (Lightweight Directory Access Protocol) 및 웹 인증에 사용 되는 업계 표준입니다. 다이제스트 인증은 네트워크를 통해 MD5 해시 또는 메시지 다이제스트로 자격 증명을 전송 합니다.

다이제스트 SSP (Wdigest .dll)는 다음에 사용 됩니다.

-   Internet Explorer 및 인터넷 정보 서비스 (IIS) 액세스

-   LDAP 쿼리

위치:%windir%\Windows\System32\Digest.dll

이 공급자는이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전 및 windows Server 2003 및 windows XP에 기본적으로 포함 되어 있습니다.

**다이제스트 프로토콜 및 다이제스트 SSP에 대 한 추가 리소스**

-   [Microsoft Digest 인증 (Windows)](https://msdn.microsoft.com/library/aa378745(VS.85).aspx)

-   [\[MS-6psp\]: 다이제스트 프로토콜 확장](https://msdn.microsoft.com/library/cc227906(PROT.13).aspx)

### <a name="BKMK_SchannelSSP"></a>Schannel 보안 지원 공급자
보안 채널 (Schannel)은 사용자가 보안 웹 서버에 액세스 하려고 할 때와 같이 웹 기반 서버 인증에 사용 됩니다.

TLS 프로토콜, SSL 프로토콜, PCT (개인 통신 기술) 프로토콜 및 DTLS (데이터 그램 전송 계층) 프로토콜은 공개 키 암호화를 기반으로 합니다. Schannel은 이러한 모든 프로토콜을 제공 합니다. 모든 Schannel 프로토콜에서는 클라이언트/서버 모델이 사용됩니다. Schannel SSP는 공개 키 인증서를 사용하여 당사자를 인증합니다. 파티를 인증할 때 Schannel SSP는 다음과 같은 기본 설정 순서로 프로토콜을 선택 합니다.

-   TLS (전송 계층 보안) 버전 1.0

-   TLS (전송 계층 보안) 버전 1.1

-   TLS (전송 계층 보안) 버전 1.2

-   SSL (Secure Socket Layer) 버전 2.0

-   SSL (Secure Socket Layer) 버전 3.0

-   PCT (개인 통신 기술)

    **참고** PCT는 기본적으로 사용 하지 않도록 설정 되어 있습니다.

선택 된 프로토콜은 클라이언트와 서버에서 지원할 수 있는 기본 인증 프로토콜입니다. 예를 들어 서버에서 모든 Schannel 프로토콜을 지원 하 고 클라이언트에서 SSL 3.0 및 SSL 2.0만 지 원하는 경우 인증 프로세스는 SSL 3.0를 사용 합니다.

DTLS는 응용 프로그램에 의해 명시적으로 호출 될 때 사용 됩니다. DTLS 및 Schannel 공급자가 사용 하는 기타 프로토콜에 대 한 자세한 내용은 [Schannel Security Support Provider Technical Reference](../tls/schannel-security-support-provider-technical-reference.md)를 참조 하십시오.

위치:%windir%\Windows\System32\Schannel.dll

이 공급자는이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전 및 windows Server 2003 및 windows XP에 기본적으로 포함 되어 있습니다.

> [!NOTE]
> TLS 1.2은 Windows Server 2008 R2 및 Windows 7의이 공급자에서 도입 되었습니다. DTLS는 Windows Server 2012 및 Windows 8의이 공급자에서 도입 되었습니다.

**TLS 및 SSL 프로토콜 및 Schannel SSP에 대 한 추가 리소스**

-   [보안 채널 (Windows)](https://msdn.microsoft.com/library/aa380123(VS.85).aspx)

-   [TLS/SSL 기술 참조](https://technet.microsoft.com/library/cc784149(v=ws.10).aspx)

-   [\[MS TLSP\]: TLS (Transport Layer Security) 프로필](https://msdn.microsoft.com/library/dd207968(PROT.13).aspx)

### <a name="BKMK_NegoSSP"></a>보안 지원 공급자 협상
간단 하 고 보호 된 GSS-API 협상 메커니즘 (SPNEGO)은 특정 인증 프로토콜을 협상 하는 데 사용할 whichcan Negotiate SSP의 기반을 형성 합니다. 응용 프로그램에서 SSPI를 호출 하 여 네트워크에 로그온 하는 경우 요청을 처리할 SSP를 지정할 수 있습니다. 응용 프로그램에서 Negotiate SSP를 지정 하는 경우 요청을 분석 하 고 고객 구성 보안 정책에 따라 적절 한 공급자를 선택 하 여 요청을 처리 합니다.

SPNEGO는 RFC 2478에 지정 되어 있습니다.

지원 되는 버전의 Windows 운영 체제에서 Negotiate security support provider는 Kerberos 프로토콜 및 NTLM을 선택 합니다. Negotiate는 인증에 관련 된 시스템 중 하나에서 해당 프로토콜을 사용할 수 없거나 호출 응용 프로그램에서 Kerberos 프로토콜을 사용 하는 데 충분 한 정보를 제공 하지 않는 한 기본적으로 Kerberos 프로토콜을 선택 합니다.

위치:%windir%\Windows\System32\lsasrv.dll

이 공급자는이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전 및 windows Server 2003 및 windows XP에 기본적으로 포함 되어 있습니다.

**Negotiate SSP에 대 한 추가 리소스**

-   [Microsoft Negotiate (Windows)](https://msdn.microsoft.com/library/aa378748(VS.85).aspx)

-   [\[MS-SPNG\]: 간단 하 고 보호 된 GSS-SPNEGO (API 협상 메커니즘) 확장](https://msdn.microsoft.com/library/cc247021(PROT.13).aspx)

-   [\[N2HT\]: Negotiate and Nego2 HTTP Authentication Protocol Specification](https://msdn.microsoft.com/library/dd303576(PROT.13).aspx)

### <a name="BKMK_CredSSP"></a>자격 증명 보안 지원 공급자
CredSSP (Credential Security Service Provider)는 새 터미널 서비스 및 원격 데스크톱 서비스 세션을 시작할 때 SSO (Single Sign-On) 사용자 환경을 제공 합니다. CredSSP를 통해 응용 프로그램은 클라이언트의 정책을 기반으로 클라이언트 컴퓨터에서 클라이언트 쪽 ssp를 사용 하 여 사용자 자격 증명을 대상 서버 (서버 쪽 SSP를 통해)에 위임할 수 있습니다. CredSSP 정책은 그룹 정책를 사용 하 여 구성 되 고 자격 증명 위임은 기본적으로 해제 되어 있습니다.

위치:%windir%\Windows\System32\credssp.dll

이 공급자는이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전에 기본적으로 포함 되어 있습니다.

**SSP 자격 증명에 대 한 추가 리소스**

-   [\[MS-CSSP\]: CredSSP (Credential Security Support Provider) 프로토콜 사양](https://msdn.microsoft.com/library/cc226764(PROT.13).aspx)

-   [터미널 서비스 로그온을 위한 자격 증명 보안 서비스 공급자 및 SSO](https://technet.microsoft.com/library/cc749211(v=ws.10).aspx)

### <a name="BKMK_NegoExtsSSP"></a>Negotiate 확장 보안 지원 공급자
Negotiate 확장 (NegoExts)은 Microsoft 및 기타 소프트웨어 회사에서 구현 하는 응용 프로그램 및 시나리오에 대해 NTLM 또는 Kerberos 프로토콜 이외의 Ssp 사용을 협상 하는 인증 패키지입니다.

Negotiate 패키지에 대 한이 확장을 통해 다음과 같은 시나리오를 수행할 수 있습니다.

-   **페더레이션된 시스템 내의 리치 클라이언트 가용성.** 문서는 SharePoint 사이트에서 액세스할 수 있으며 전체 기능을 갖춘 Microsoft Office 응용 프로그램을 사용 하 여 편집할 수 있습니다.

-   **Microsoft Office services에 대 한 풍부한 클라이언트 지원.** 사용자는 Microsoft Office 서비스에 로그인 하 고 완전 한 기능을 갖춘 Microsoft Office 응용 프로그램을 사용할 수 있습니다.

-   **호스팅된 Microsoft Exchange Server 및 Outlook.** Exchange Server가 웹에서 호스트 되기 때문에 도메인 트러스트가 설정 되지 않았습니다. Outlook에서는 Windows Live 서비스를 사용 하 여 사용자를 인증 합니다.

-   **클라이언트 컴퓨터와 서버 간의 리치 클라이언트 가용성.** 운영 체제의 네트워킹 및 인증 구성 요소가 사용 됩니다.

Windows Negotiate 패키지는 NegoExts SSP를 Kerberos 및 NTLM과 동일한 방식으로 처리 합니다. NegoExts .dll은 시작 시 LSA (로컬 시스템 기관)에 로드 됩니다. 요청의 원본에 따라 인증 요청이 수신 되 면 NegoExts는 지원 되는 Ssp 사이에서 협상 합니다. 자격 증명 및 정책을 수집 하 고 암호화 한 다음 해당 정보를 보안 토큰이 생성 된 적절 한 SSP로 보냅니다.

NegoExts에서 지 원하는 Ssp는 Kerberos 및 NTLM과 같은 독립 실행형 Ssp가 아닙니다. 따라서 NegoExts SSP 내에서 어떤 이유로 든 인증 방법이 실패할 경우 인증 실패 메시지가 표시 되거나 로깅됩니다. 재협상 또는 대체 인증 방법이 가능 하지 않습니다.

위치:%windir%\Windows\System32\negoexts.dll

이 공급자는 Windows Server 2008 및 Windows Vista를 제외 하 고이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전에 기본적으로 포함 되어 있습니다.

### <a name="BKMK_PKU2USSP"></a>PKU2U 보안 지원 공급자
PKU2U 프로토콜은 Windows 7 및 Windows Server 2008 r 2에서 SSP로 도입 및 구현 되었습니다. 이 SSP는 Windows 7에 도입 된 홈 그룹 이라는 미디어 및 파일 공유 기능을 사용 하 여 피어 투 피어 인증을 지원 합니다. 이 기능을 사용 하면 도메인의 구성원이 아닌 컴퓨터를 공유할 수 있습니다.

위치:%windir%\Windows\System32\pku2u.dll

이 공급자는 Windows Server 2008 및 Windows Vista를 제외 하 고이 항목의 시작 부분에 있는 **적용 대상** 목록에 지정 된 버전에 기본적으로 포함 되어 있습니다.

**PKU2U 프로토콜 및 PKU2U SSP에 대 한 추가 리소스**

-   [온라인 Id 통합 소개](https://technet.microsoft.com/library/dd560662(v=ws.10).aspx)

## <a name="BKMK_SecuritySupportProviderSelection"></a>보안 지원 공급자 선택
Windows SSPI는 설치 된 보안 지원 공급자를 통해 지원 되는 모든 프로토콜을 사용할 수 있습니다. 그러나 모든 운영 체제에서 Windows Server를 실행 하는 지정 된 컴퓨터와 동일한 SSP 패키지를 지원 하기 때문에 클라이언트와 서버는 모두에서 지 원하는 프로토콜을 사용 하도록 협상 해야 합니다. Windows Server는 클라이언트 컴퓨터와 응용 프로그램이 가능한 경우 강력한 표준 기반 프로토콜인 Kerberos 프로토콜을 사용 하도록 선호 하지만 운영 체제는 Kerberos를 지원 하지 않는 클라이언트 컴퓨터와 클라이언트 응용 프로그램을 계속 허용 합니다. 인증할 프로토콜입니다.

인증을 수행 하려면 두 통신 컴퓨터가 둘 다 지원할 수 있는 프로토콜에 동의 해야 합니다. SSPI를 통해 모든 프로토콜을 사용할 수 있도록 하려면 각 컴퓨터에 적절 한 SSP가 있어야 합니다. 예를 들어 Kerberos 인증 프로토콜을 사용 하는 클라이언트 컴퓨터와 서버는 모두 Kerberos v5를 지원 해야 합니다. Windows Server는 **EnumerateSecurityPackages** 함수를 사용 하 여 컴퓨터에서 지원 되는 ssp와 해당 ssp의 기능을 식별 합니다.

인증 프로토콜 선택은 다음 두 가지 방법 중 하나로 처리할 수 있습니다.

1.  [단일 인증 프로토콜](#BKMK_SingleAuth)

2.  [Negotiate 옵션](#BKMK_Negotiate)

### <a name="BKMK_SingleAuth"></a>단일 인증 프로토콜
서버에 사용할 수 있는 단일 프로토콜이 지정 된 경우 클라이언트 컴퓨터에서 지정 된 프로토콜을 지원 해야 합니다. 그렇지 않으면 통신이 실패 합니다. 허용 되는 단일 프로토콜이 지정 된 경우 인증 교환은 다음과 같이 수행 됩니다.

1.  클라이언트 컴퓨터는 서비스에 대 한 액세스를 요청 합니다.

2.  서버는 요청에 응답 하 고 사용할 프로토콜을 지정 합니다.

3.  클라이언트 컴퓨터는 회신의 내용을 검사 하 여 지정 된 프로토콜을 지원 하는지 확인 합니다. 클라이언트 컴퓨터에서 지정 된 프로토콜을 지원 하면 인증이 계속 됩니다. 클라이언트 컴퓨터에서 프로토콜을 지원 하지 않는 경우 클라이언트 컴퓨터에 리소스에 액세스할 수 있는 권한이 있는지 여부에 관계 없이 인증이 실패 합니다.

### <a name="BKMK_Negotiate"></a>Negotiate 옵션
Negotiate 옵션을 사용 하면 클라이언트와 서버가 허용 가능한 프로토콜을 찾도록 허용할 수 있습니다. 이는 간단 하 고 보호 된 GSS-API 협상 메커니즘 (SPNEGO)을 기반으로 합니다. 인증 프로토콜에 대 한 협상 옵션으로 인증을 시작 하면 SPNEGO 교환이 다음과 같이 수행 됩니다.

1.  클라이언트 컴퓨터는 서비스에 대 한 액세스를 요청 합니다.

2.  서버는 첫 번째 선택 된 프로토콜을 기반으로 하 여 지원할 수 있는 인증 프로토콜 목록과 인증 시도 또는 응답을 사용 하 여 응답 합니다. 예를 들어 서버에서 Kerberos 프로토콜 및 NTLM을 나열 하 고 Kerberos 인증 응답을 보낼 수 있습니다.

3.  클라이언트 컴퓨터는 회신의 내용을 검사 하 여 지정 된 프로토콜을 지원 하는지 여부를 확인 합니다.

    -   클라이언트 컴퓨터가 기본 설정 프로토콜을 지 원하는 경우 인증을 계속 진행 합니다.

    -   클라이언트 컴퓨터가 기본 설정 프로토콜을 지원 하지 않지만 서버에 나열 된 다른 프로토콜 중 하나를 지원 하는 경우 클라이언트 컴퓨터를 사용 하 여 서버에서 지 원하는 인증 프로토콜을 확인 하 고 인증을 진행 합니다.

    -   클라이언트 컴퓨터에서 나열 된 프로토콜을 모두 지원 하지 않는 경우 인증 교환이 실패 합니다.

## <a name="see-also"></a>참고 항목
[Windows 인증 아키텍처](https://technet.microsoft.com/library/dn169024(v=ws.10).aspx)


