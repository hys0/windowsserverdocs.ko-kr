---
title: "Windows 인증 건축물"
description: "Windows Server 보안"
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
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="windows-authentication-architecture"></a>Windows 인증 건축물

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

IT 전문가 위한이 개요 항목 기본 아키텍처 구성표 Windows 인증에 대해 설명합니다.

인증은 프로세스는 시스템이 사용자의 로그온 또는 로그인 정보를 확인 합니다. 사용자의 이름 및 암호는 권한이 있는 목록과 비교 하 고 시스템에서 일치 하는 발견 하면 해당 사용자에 대 한 사용 권한 목록에 지정 된 하는 범위까지 액세스 부여 됩니다.

Extensible 아키텍처의 일환으로, Windows Server 운영 체제 등이 포함 협상, Kerberos 프로토콜을 NTLM, Schannel (보안 채널) 요약 인증 보안 지원 공급자를 기본 집합을 구현 합니다. 이러한 공급자가 사용 프로토콜 사용자가, 컴퓨터 및 서비스의 인증을 사용 하 고 인증 프로세스를 안전 하 게에서 리소스에 액세스 권한이 있는 사용자 및 서비스를 사용 합니다.

Windows Server, 응용 프로그램 SSPI 추상 인증에 대 한 호출을 사용 하 여 사용자를 인증 합니다. 따라서 개발자 특정 인증 프로토콜 복잡 한 문제를 파악 또는 응용 프로그램에 인증 프로토콜 빌드 필요는 없습니다.

Windows Server 운영 체제에 Windows 보안 모델을 구성 하는 보안 구성 요소 집합 포함 되어 있습니다. 이러한 구성 요소 응용 프로그램 인증 및 승인 없이 리소스에 액세스할 수 있는지 확인 합니다. 다음 섹션 인증 아키텍처 요소 설명 합니다.

### <a name="local-security-authority"></a>로컬 보안 기관
로컬 보안 기관을 (LSA)는 로컬 컴퓨터에 사용자가 로그인 및 인증 하는 보호 하위 시스템 합니다. 또한 LSA 정보를 유지 모든 측면에 대 한 로컬 보안 컴퓨터에서 (이러한 측면 집합적으로 이라고 로컬 보안 정책이). 또한 이름 및 보안 Sid (식별자) 간의 번역에 대 한 다양 한 서비스를 제공합니다.

보안 정책 및 컴퓨터 시스템에 있는 계정 보안 하위 시스템은 추적 합니다. 경우 도메인 컨트롤러 이러한 정책 및 계정은 도메인 컨트롤러 있는 도메인에 적용 됩니다. 이러한 정책과 계정 Active Directory에 저장 됩니다. 사용자의 권한을 확인 하 고 생성 감사 메시지, LSA 하위 시스템 물체에 대 한 액세스를 유효성 검사에 대 한 서비스를 제공 합니다.

### <a name="security-support-provider-interface"></a>보안 지원 공급자 인터페이스
보안 지원 공급자 Interface (SSPI)은 API 인증, 메시지 무결성, 메시지 개인 정보 및 보안 품질 서비스에 대 한 모든 분산된 응용 프로그램 프로토콜에 대 한 통합된 보안 서비스 가져옵니다입니다.

SSPI 구현의는 일반적인 보안 서비스 API (gssapi가)입니다. SSPI는 분산된 응용 프로그램 호출할 수 보안 프로토콜에 대 한 모르게 인증된 된 연결을 얻을 수 있는 몇 가지 보안 공급자 중 하나는 메커니즘을 제공 합니다.

## <a name="see-also"></a>참조 하십시오

-   [보안 지원 공급자 인터페이스 구조](security-support-provider-interface-architecture.md)

-   [자격 증명 프로세스 Windows 인증](credentials-processes-in-windows-authentication.md)

-   [Windows 인증 기술 개요](https://technet.microsoft.com/library/dn169029.aspx)


