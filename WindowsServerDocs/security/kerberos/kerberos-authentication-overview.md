---
title: "Kerberos 인증 개요"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 646c6309-e865-4be2-b415-44dd125af5c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 9f8878fb959c34663b1e1f3858fa7e0b6e7b6105
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="kerberos-authentication-overview"></a>Kerberos 인증 개요

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Kerberos는 호스트 또는 사용자의 신원을 확인 하는 데 사용 되는 인증 프로토콜입니다. 이 항목에서는 Windows 8 및 Windows Server 2012에서 Kerberos 인증에 대 한 설명입니다.

## <a name="BKMK_OVER"></a>기능 설명
The Windows Server operating systems implement the Kerberos version 5 authentication protocol and extensions for public key authentication, transporting authorization data, and delegation. 인증 Kerberos 클라이언트는 구현 보안 지원 공급자로 \(SSP\), 있으며 통해 액세스할 수 있는 보안 지원 공급자 인터페이스 \(SSPI\) 합니다. 초기 사용자 인증 Winlogon 단일 sign\ 켜 짐 건축물과 섞여 통합 되어 있습니다.

The Kerberos Key Distribution Center \(KDC\) is integrated with other Windows Server security services that run on the domain controller. KDC 보안 계정 데이터베이스도 도메인의 Active Directory Domain Services 데이터베이스를 사용합니다. Active Directory Domain Services 숲 또는 도메인에 기본 Kerberos 구현을 필요 합니다.

## <a name="kerb_tr_Kerb_Benefits"></a>실용적인 응용 프로그램
Kerberos domain\ 기반 인증을 위해 사용 하 여 얻은 혜택은 다음과 같습니다.

-   **위임된 인증 합니다.**

    Windows 운영 체제에서 실행 되는 서비스는 클라이언트를 대신 하 여 리소스에 액세스할 때 클라이언트 컴퓨터를 가장 수 있습니다. 대부분의 경우 서비스 로컬 컴퓨터 리소스에 액세스 하 여 클라이언트에 대 한 작업을 완료할 수 있습니다. 클라이언트 컴퓨터 서비스를 인증 NTLM 및 Kerberos 프로토콜 서비스 로컬 컴퓨터 클라이언트 가장 해야 한다는 인증 정보를 제공 합니다. 그러나 일부 분산된 응용 프로그램은 다른 컴퓨터에서 back\ 서비스에 연결할 때 front\ 종료 서비스 클라이언트 컴퓨터의 id를 사용 해야 않도록 설계 되었습니다. Kerberos 인증을 다른 서비스에 연결할 때의 클라이언트 대신해 서비스를 가능 하 게 위임 메커니즘을 지원 합니다.

-   **단일 로그인 합니다.**

    도메인 안이나는 숲 속의 인증 Kerberos 사용 하 여 사용자 또는 자격에 대 한 여러 요청 하지 않고 관리자가 허용 리소스에 대 한 서비스 액세스 수 있게 합니다. 초기 도메인 기호가에 Winlogon 통해 후 Kerberos 리소스에 액세스 하려고 때마다 숲 전체 자격 증명을 관리 합니다.

-   **상호 운용성 합니다.**

    Microsoft에 의해 Kerberos v 5 프로토콜 구현 하는 엔지니어링 작업 힘 인터넷 \(IETF\) 권장 되는 트랙 standards\ 사양 기반으로 합니다. 결과적으로, Windows 운영 체제 Kerberos 프로토콜 인증 Kerberos 프로토콜을 사용 하는 다른 네트워크 상호 운용성을 위한 기반을 배치 합니다. 또한 Microsoft는 구현 Kerberos 프로토콜에 대 한 Windows 프로토콜 설명서를 게시 합니다. 설명서 기술 요구 사항, 제한, 종속성 및 Microsoft의 구현 Kerberos 프로토콜에 대 한 프로토콜 동작 Windows\ 관련 포함 되어 있습니다.

-   **서버를 더 효율적 인증 합니다.**

    이전 Kerberos, NTLM 인증 사용할 수 있었습니다, 도메인 컨트롤러에 연결 하는 응용 프로그램 서버 요구 하는 모든 가지의 또는 서비스를 인증 합니다. Kerberos 프로토콜 갱신 세션 티켓 pass\ 쓰루 인증을 교체합니다. 서버 도메인 컨트롤러도 이동 하지 않아도 되며 \ (없는 경우 권한이 특성 인증서 \(PAC\)\) 확인 해야 합니다. 대신, 서버 자격 증명 클라이언트에서 표시를 검사 하 여 클라이언트 컴퓨터를 인증할 수 있습니다. 클라이언트 컴퓨터 특정 서버에 대 한 자격 증명을 한 번 얻을 하 고 네트워크 로그온 세션 전체 해당 자격 증명을 다시 사용할 수 있습니다.

-   **상호 인증 합니다.**

    Kerberos 프로토콜을 사용 하 여 네트워크 연결의 양쪽 끝 파티 다른 쪽 끝에 파티 것인지 엔터티 인지 확인할 수 있습니다. 서버의 신원을 확인 하거나 다른의 id 확인을 위해 가능 클라이언트 가능 하지 않습니다. NTLM 인증 서버 정품 것으로 간주이 있는 네트워크 환경을 위해 설계 되었습니다. Kerberos 프로토콜은 이러한 가정.

## <a name="see-also"></a>참조 하십시오
[Windows 인증 개요](../windows-authentication/windows-authentication-overview.md)


