---
title: Windows 인증 아키텍처
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 07c9d6bb-9b03-407d-89b6-97c7551b256b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: fd6e2cbc233a91b62e3c8c9caf1154f91c3863ac
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855864"
---
# <a name="windows-authentication-architecture"></a>Windows 인증 아키텍처

>적용 대상: Windows Server (반기 채널), Windows Server 2016

IT 전문가 위한이 개요 항목에서는 Windows 인증에 대 한 기본 아키텍처 구성표를 설명합니다.

인증은 사용자의 로그온 또는 로그인 정보 시스템이 확인 하는 프로세스입니다. 사용자의 이름 및 암호를 승인된 목록과 비교 하 고 일치 하면 해당 사용자에 대 한 권한 목록에서 지정 된 범위에 액세스가 허용 됩니다.

Windows Server 운영 체제는 확장 가능한 아키텍처의 일부로, Negotiate, Kerberos, NTLM, Schannel (보안 채널) 프로토콜과 다이제스트를 포함 하는 인증 보안 지원 공급자의 기본 집합을 구현 합니다. 사용자, 컴퓨터 및 서비스의 인증을 사용 하는 이러한 공급자에서 사용 하는 프로토콜 및 인증 프로세스를 안전 하 게에서 리소스에 액세스할 권한이 있는 사용자 및 서비스를 사용 합니다.

Windows Server 응용 프로그램 인증에 대 한 호출을 추상화 하는 SSPI를 사용 하 여 사용자를 인증 합니다. 따라서 개발자 필요가 없습니다 응용 프로그램에 인증 프로토콜을 빌드하거나 특정 인증 프로토콜의 복잡성을 이해 합니다.

Windows Server 운영 체제의 Windows 보안 모델을 구성 하는 보안 구성 요소 집합이 포함 됩니다. 이러한 구성 요소 응용 프로그램 인증 및 권한 부여 없이 리소스에 액세스할 수 없는 있는지 확인 합니다. 다음 섹션에서는 인증 아키텍처의 요소를 설명합니다.

### <a name="local-security-authority"></a>로컬 보안 기관
로컬 보안 기관 (LSA)는 인증 하 고 로컬 컴퓨터에 사용자를 로그인 하는 보호 된 하위 시스템입니다. 또한 LSA 정보의 모든 측면에 대 한 로컬 보안 컴퓨터 (이러한 측면 이라고 통칭 로컬 보안 정책)를 유지 합니다. 또한 이름 및 보안 식별자 (Sid) 간의 변환에 대 한 다양 한 서비스를 제공합니다.

보안 정책 및 컴퓨터 시스템에 있는 계정에는 보안 하위 시스템의 추적 유지 합니다. 도메인의 경우 이러한 정책 및 계정 컨트롤러는 도메인 컨트롤러의 위치를 가리키는 도메인에 적용 됩니다. 이러한 정책 및 계정을 Active Directory에 저장 됩니다. 개체에 대 한 액세스의 유효성을 검사 하는 것에 대 한 서비스를 제공 하는 LSA 하위 시스템, 감사 메시지를 사용자 권한을 확인 하 고 생성 합니다.

### <a name="security-support-provider-interface"></a>보안 지원 공급자 인터페이스
보안 지원 공급자 인터페이스 (SSPI)는 API 인증, 메시지 무결성, 메시지 개인 정보 및 보안의 서비스 품질에 대 한 모든 배포 응용 프로그램 프로토콜에 대 한 통합된 보안 서비스입니다.

SSPI는의 일반 보안 서비스 API (GSSAPI) 구현입니다. SSPI는 분산된 응용 프로그램을 호출할 수의 보안 프로토콜 세부 지식 없이 인증된 된 연결을 가져오려면 여러 보안 공급자 중 하나는 메커니즘을 제공 합니다.

## <a name="see-also"></a>참조

-   [보안 지원 공급자 인터페이스 아키텍처](security-support-provider-interface-architecture.md)

-   [Windows 인증에서 자격 증명 프로세스](credentials-processes-in-windows-authentication.md)

-   [Windows 인증 기술 개요](https://technet.microsoft.com/library/dn169029.aspx)


