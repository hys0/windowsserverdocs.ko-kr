---
title: What's New in Kerberos Authentication
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: a0916abf1076b5f791a856f0c85f54ad17f6d64c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403476"
---
# <a name="whats-new-in-kerberos-authentication"></a>What's New in Kerberos Authentication

>적용 대상: Windows Server 2016 및 Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>공개 키 신뢰 기반 클라이언트 인증에 대 한 KDC 지원

Windows Server 2016부터 Kdc는 공개 키 매핑 방법을 지원 합니다. 공개 키가 계정에 대해 프로 비전 되 면 KDC는 해당 키를 사용 하 여 Kerberos PKInit를 명시적으로 지원 합니다. 인증서의 유효성을 검사 하지 않으므로 자체 서명 된 인증서가 지원 되며 인증 메커니즘 보증은 지원 되지 않습니다.

UseSubjectAltName 설정에 관계 없이 계정에 대해 구성 된 경우 키 트러스트가 선호 됩니다.

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>RFC 8070 PKInit Freshness 확장에 대 한 Kerberos 클라이언트 및 KDC 지원

Windows 10, 버전 1607 및 Windows Server 2016부터 Kerberos 클라이언트는 공개 키 기반 로그인에 대 한 [RFC 8070 PKInit freshness extension](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/) 을 시도 합니다. 

Windows Server 2016부터 Kdc는 PKInit freshness 확장을 지원할 수 있습니다. 기본적으로 Kdc는 PKInit freshness extension을 제공 하지 않습니다. 이 기능을 사용 하도록 설정 하려면 도메인의 모든 Dc에서 PKInit Freshness Extension KDC 관리 템플릿 정책 설정에 대 한 새 KDC 지원을 사용 합니다. 구성 된 경우 도메인이 Windows Server 2016 DFL (도메인 기능 수준) 인 경우 다음 옵션이 지원 됩니다.

- **사용 안 함**: KDC는 PKInit Freshness 확장을 제공 하지 않으며, 유효성 검사를 확인 하지 않고 유효한 인증 요청을 수락 합니다. 사용자는 새로운 공개 키 id SID를 받을 수 없습니다.
- **지원 됨**: PKInit Freshness Extension은 요청에서 지원 됩니다. Kerberos 클라이언트에서 PKInit Freshness 확장을 성공적으로 인증 하면 새로운 공개 키 id SID가 수신 됩니다.
- **필수**: PKInit Freshness Extension은 성공적인 인증을 위해 필요 합니다. PKInit Freshness Extension을 지원 하지 않는 Kerberos 클라이언트는 공개 키 자격 증명을 사용 하는 경우 항상 실패 합니다.

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>공개 키를 사용 하 여 인증에 대 한 도메인 가입 장치 지원

Windows 10 버전 1507 및 Windows Server 2016부터 도메인에 가입 된 장치가 Windows Server 2016 DC (도메인 컨트롤러)를 사용 하 여 바인딩된 공개 키를 등록할 수 있는 경우 장치는 Kerberos 인증을 사용 하 여 공개 키를 사용 하 여 인증할 수 있습니다. Windows Server 2016 DC 자세한 내용은 [도메인에 가입 된 장치 공개 키 인증](Domain-joined-Device-Public-Key-Authentication.md) 을 참조 하세요.

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos 클라이언트는 Spn (서비스 사용자 이름)에서 IPv4 및 IPv6 주소 호스트 이름을 허용 합니다.

Windows 10 버전 1507 및 Windows Server 2016부터 Spn에서 IPv4 및 IPv6 호스트 이름을 지원 하도록 Kerberos 클라이언트를 구성할 수 있습니다. 

레지스트리 경로:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

Spn의 IP 주소 호스트 이름에 대 한 지원을 구성 하려면 TryIPSPN 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 구성 되지 않은 경우 IP 주소 호스트 이름을 시도 하지 않습니다.

SPN이 Active Directory에 등록 되 면 Kerberos를 사용 하 여 인증이 성공 합니다. 

자세한 내용은 [IP 주소에 대 한 Kerberos 구성](configuring-kerberos-over-ip.md)문서를 확인 하세요.

## <a name="kdc-support-for-key-trust-account-mapping"></a>키 신뢰 계정 매핑에 대 한 KDC 지원

Windows Server 2016부터 도메인 컨트롤러는 키 신뢰 계정 매핑과 SAN 동작에서 기존 AltSecID 및 UPN (사용자 계정 이름)을 대체 하는 기능을 지원 합니다. UseSubjectAltName가로 설정 된 경우:

- 0: 명시적 매핑이 필요 합니다. 다음 중 하나가 있어야 합니다.
    - 키 신뢰 (Windows Server 2016에서 새로 만들기)
    - ExplicitAltSecID
- 1: 암시적 매핑이 허용 됩니다 (기본값).
    1. 계정에 대해 키 신뢰가 구성 된 경우 매핑에 사용 됩니다 (Windows Server 2016에서 새로 만들기).
    2. SAN에 UPN이 없으면 AltSecID이 매핑을 시도 합니다.
    3. SAN에 UPN이 있는 경우 매핑을 시도 합니다.

## <a name="see-also"></a>관련 항목

- [Kerberos 인증 개요](kerberos-authentication-overview.md)
