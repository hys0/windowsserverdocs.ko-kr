---
title: "Kerberos 인증의 새로운 기능"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 7b046490c606cdf9e1436f503bf46a9cd4280ea9
ms.sourcegitcommit: 2782a80a916f8432c030af76e860a72f08481899
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/13/2018
---
# <a name="whats-new-in-kerberos-authentication"></a>Kerberos 인증의 새로운 기능

>적용 대상: Windows Server 2016 및 Windows 10

## <a name="kdc-support-for-public-key-trust-based-client-authentication"></a>클라이언트 공개 키 신뢰 기반 인증을 위한 KDC 지원

Windows Server 2016 부터는 Kdc 키 매핑 공개 하는 방법을 지원 합니다. 공개 키가 있는 계정에 대 한 프로 비전을 KDC Kerberos PKInit 명시적으로 해당 키를 사용 하 여을 지원 합니다. 인증서 유효성 이므로 자체 서명된 인증서가 지원 및 인증 메커니즘 보증 지원 되지 않습니다.

키를 신뢰 것 UseSubjectAltName 설정과 관계 없이 계정에 대 한 구성 된 경우이 좋습니다.

## <a name="kerberos-client-and-kdc-support-for-rfc-8070-pkinit-freshness-extension"></a>Kerberos 클라이언트 및 KDC RFC 8070 PKInit 새로 고침 확장에 대 한 지원

Windows 10 버전 1607 및 Windows Server 2016 부터는 Kerberos 클라이언트 시도 [RFC 8070 PKInit 새로 고침 확장](https://datatracker.ietf.org/doc/draft-ietf-kitten-pkinit-freshness/) 공개 키 기반 기호 기능에 대 한 합니다. 

Windows Server 2016 부터는 Kdc PKInit 새로 고침 확장을 지원할 수 있습니다. 기본적으로 Kdc PKInit 새로 고침 확장을 제공 하지 않습니다. 기능을 사용 하려면 새로운 KDC 지원 도메인에 있는 모든 Dc PKInit 새로 고침 확장 KDC 관리 템플릿 정책 설정에 대 한 사용 합니다. 구성, Windows Server 2016 도메인 기능 (DFL) 수준을 도메인이 때 다음 옵션 지원 됩니다.

- **사용 안 함**: The KDC 하지 PKInit 새로 고침 확장을 제공 하 고 유효성을 검사 하지 않고 유효한 인증 요청을 허용 합니다. 사용자가 신선한 공개 키 id SID 받습니다 하지 않습니다.
- **지원 되는**: PKInit 새로 고침 확장 요청에 대해 지원 됩니다. 성공적으로 인증 PKInit 새로 고침 확장 된 Kerberos 클라이언트 신선한 공개 키 id SID를 받게 됩니다.
- **필요한**: PKInit 새로 고침 확장 성공적으로 인증을 위한 필요 합니다. 공개 키 자격 증명을 사용할 때에 항상 PKInit 새로 고침 확장을 지원 하지 않는 Kerberos 클라이언트 되지 것입니다.

## <a name="domain-joined-device-support-for-authentication-using-public-key"></a>도메인 가입 장치 지원 공개 키를 사용 하 여 인증에 대 한

도메인 가입 장치는 Windows Server 2016 DC (도메인 컨트롤러)와 바인딩된 공개 키를 등록할 수 있으면 Windows 10 버전 1507 및 Windows Server 2016 년부터, 다음 디바이스 인증을 받을 수 Kerberos 인증 Windows Server 2016 DC을 사용 하 여 공개 키. 자세한 내용은 참조 [도메인에 가입 장치 공개 키 인증](Domain-joined-Device-Public-Key-Authentication.md)

## <a name="kerberos-clients-allow-ipv4-and-ipv6-address-hostnames-in-service-principal-names-spns"></a>Kerberos 클라이언트 IPv4 및 IPv6 주소 호스트 이름을 (Spn) 서비스 사용자 이름에 허용

Windows 10 버전 1507 및 Windows Server 2016 부터는 Kerberos 클라이언트 Spn IPv4 및 IPv6 호스트 이름을 지원 하도록 구성할 수 있습니다. 

레지스트리 경로 다음과 같습니다.

HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\Kerberos\Parameters

호스트 IP 주소 이름에 대 한 지원을으로 Spn를 구성 하려면 TryIPSPN 항목을 만듭니다. 기본적으로이 항목의에서 존재 하지 않습니다. 항목을 만든 후 1 DWORD 값을 변경 합니다. 구성 되지 호스트 IP 주소 이름을 시도 하지 됩니다.

SPN Active Directory에 등록 되어 있으면 인증 성공 Kerberos 사용 합니다. 

## <a name="kdc-support-for-key-trust-account-mapping"></a>KDC 키 신뢰 계정 간의 대 한 지원

Windows Server 2016 부터는 도메인 컨트롤러는 계정 간의 키 신뢰할 기존 AltSecID 및 사용자 이름 UPN (계정)를 대체 산 동작에서에 대 한 지원 합니다. UseSubjectAltName로 설정 된 경우 다음과 같습니다.

- 0: 명시적 매핑이 필요 합니다. 다음 중 하나 해야 합니다.
    - (Windows Server 2016)와 새로운 신뢰 키
    - ExplicitAltSecID
- 1: 암묵적인 매핑이 (기본)를 사용할 수 있습니다.
    1. 키 신뢰를 구성 된 계정에 대 한 경우 다음 것은에 사용 매핑 (Windows Server 2016의 새로운).
    2. 산에 없는 UPN 있으면 지도 대 한 AltSecID 시도 됩니다.
    3. 산에 UPN 있으면 지도 대 한 UPN 시도 됩니다.

## <a name="see-also"></a>참조 하십시오

- [Kerberos 인증 개요](kerberos-authentication-overview.md)
