---
title: Kerberos 인증의 새로운 기능
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 7b046490c606cdf9e1436f503bf46a9cd4280ea9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831094"
---
# <a name="whats-new-in-kerberos-authentication"></a>What's New in Kerberos Authentication

>적용 대상: Windows Server 2016 및 Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>공용 키 신뢰 기반 클라이언트 인증에 대 한 KDC 지원

Windows Server 2016 부터는 Kdc는 공용 키 매핑 방법을 지원 합니다. 계정에 대 한 공개 키를 프로 비전 하는 경우 KDC Kerberos PKInit 해당 키를 사용 하 여 명시적으로 지원 합니다. 인증서 유효성을 검사 하지 않으므로 자체 서명 된 인증서는 지원 및 인증 메커니즘 보증 지원 되지 않습니다.

키 트러스트 UseSubjectAltName 설정과 관계 없이 계정을 구성 하는 경우는 것이 좋습니다.

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>RFC 8070 PKInit 새로 고침 확장에 대 한 Kerberos 클라이언트와 KDC 지원

Windows 10, 버전 1607 및 Windows Server 2016 부터는 Kerberos 클라이언트 시도 합니다 [RFC 8070 PKInit 새로 고침 확장](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/) 공개 키 기반 sign on에 대 한 합니다. 

Windows Server 2016 부터는 Kdc PKInit 새로 고침 확장을 지원할 수 있습니다. 기본적으로 Kdc PKInit 새로 고침 확장을 제공 하지 않습니다. 사용 하려면 도메인의 모든 Dc에 PKInit 새로 고침 확장 KDC 관리 템플릿 정책 설정에 대 한 새 KDC 지원을 사용 합니다. 구성 되 면 다음 옵션은 도메인 (DFL) Windows Server 2016 도메인 기능 수준 때 지원 됩니다.

- **사용 안 함**: KDC는 되지 PKInit 새로 고침 확장을 제공 하 고 새로 고침을 확인 하지 않고 유효한 인증 요청을 허용 합니다. 사용자는 새로운 공용 키 id SID를 받게 되지 됩니다.
- **지원 되는**: PKInit 새로 고침 확장 요청에서 지원 됩니다. PKInit 새로 고침 확장을 사용 하 여 성공적으로 인증 하는 Kerberos 클라이언트는 새로운 공용 키 id SID를 수신 합니다.
- **필수**: PKInit 새로 고침 확장은 성공적인 인증을 위해 필요 합니다. PKInit 새로 고침 확장을 지원 하지 않는 Kerberos 클라이언트는 공개 키 자격 증명을 사용 하는 경우에 항상 실패 합니다.

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>공개 키를 사용 하 여 인증에 대 한 도메인에 가입 된 장치 지원

부터 Windows 10 버전 1507 및 Windows Server 2016 도메인 가입 장치를 Windows Server 2016 도메인 컨트롤러 (DC)에 바인딩된 공개 키를 등록할 수 있으면, 다음 장치 인증을 받을 수 Kerberos 인증을 사용 하 여 공개 키 Windows Server 2016 DC입니다. 자세한 내용은 참조 하세요. [도메인에 가입 된 장치 공개 키 인증](Domain-joined-Device-Public-Key-Authentication.md)

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>서비스 사용자 이름 (Spn)에서 IPv4 및 IPv6 주소 호스트를 허용 하는 Kerberos 클라이언트

Windows 10 버전 1507 및 Windows Server 2016 부터는 Kerberos 클라이언트 Spn에서 IPv4 및 IPv6 호스트 이름을 지원 하도록 구성할 수 있습니다. 

레지스트리 경로:

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

Spn의 IP 주소가 호스트 이름에 대 한 지원을 구성 하려면 TryIPSPN 항목을 만듭니다. 이 항목은 기본적으로 레지스트리에 없습니다. 항목을 만든 후 DWORD 값을 1로 변경 합니다. 구성 되지 않은 경우에 IP 주소가 호스트 이름 시도 되지 됩니다.

SPN이 Active Directory에서 등록, 인증 Kerberos를 사용 하 여 성공 합니다. 

## <a name="kdc-support-for-key-trust-account-mapping"></a>키 트러스트 계정 매핑에 대 한 KDC 지원

Windows Server 2016부터 도메인 컨트롤러는 대체 (fallback) 기존 AltSecID 및 사용자 이름 (UPN) SAN 동작에서 뿐만 아니라 키 트러스트 계정 매핑을 지원 합니다. UseSubjectAltName로 설정 된 경우:

- 0: 명시적 매핑은 필요 합니다. 중 하나 여야 합니다.
    - 키 트러스트 (새로 추가 된 Windows Server 2016)
    - ExplicitAltSecID
- 1: 암시적 매핑을 허용 됨 (기본값):
    1. 키 트러스트를 구성 된 경우 계정에 대 한 다음 사용 됩니다 매핑에 대 한 (Windows Server 2016을 사용 하 여 새).
    2. 에 있는 UPN SAN AltSecID 매핑에 대 한 시도 됩니다.
    3. SAN에 UPN을 있으면 매핑에 대 한 UPN 시도 됩니다.

## <a name="see-also"></a>관련 항목

- [Kerberos 인증 개요](kerberos-authentication-overview.md)
