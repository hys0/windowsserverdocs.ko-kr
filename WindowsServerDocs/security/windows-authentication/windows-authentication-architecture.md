---
title: Windows 인증 아키텍처
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-windows-auth
ms.topic: article
ms.assetid: 07c9d6bb-9b03-407d-89b6-97c7551b256b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: f2a2b9db60842ba7889116cf35163c579d9131d1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861726"
---
# <a name="windows-authentication-architecture"></a>Windows 인증 아키텍처

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 개요 항목에서는 Windows 인증에 대 한 기본 아키텍처 체계에 대해 설명 합니다.

인증은 시스템이 사용자의 로그온 또는 로그인 정보의 유효성을 검사 하는 프로세스입니다. 사용자의 이름과 암호는 권한이 부여 된 목록과 비교 되며, 시스템에서 일치 하는 항목을 검색 하면 해당 사용자의 사용 권한 목록에 지정 된 범위에 대 한 액세스가 부여 됩니다.

확장 가능한 아키텍처의 일부로 Windows Server 운영 체제에서는 Negotiate, Kerberos 프로토콜, NTLM, Schannel (보안 채널) 및 다이제스트를 포함 하는 기본 인증 보안 지원 공급자 집합을 구현 합니다. 이러한 공급자가 사용 하는 프로토콜을 통해 사용자, 컴퓨터 및 서비스를 인증 하 고 인증 프로세스를 통해 권한 있는 사용자와 서비스가 안전한 방식으로 리소스에 액세스할 수 있습니다.

Windows Server에서 응용 프로그램은 인증을 위한 추상 호출을 사용 하 여 사용자를 인증 합니다. 따라서 개발자는 특정 인증 프로토콜의 복잡성을 이해 하거나 응용 프로그램에 인증 프로토콜을 빌드할 필요가 없습니다.

Windows Server 운영 체제에는 Windows 보안 모델을 구성 하는 보안 구성 요소 집합이 포함 되어 있습니다. 이러한 구성 요소는 응용 프로그램이 인증 및 권한 부여 없이 리소스에 액세스할 수 없도록 합니다. 다음 섹션에서는 인증 아키텍처의 요소에 대해 설명 합니다.

### <a name="local-security-authority"></a>로컬 보안 기관
LSA (로컬 보안 기관)는 사용자를 인증 하 고 로컬 컴퓨터에 로그인 하는 보호 된 하위 시스템입니다. 또한 LSA는 컴퓨터에서 로컬 보안의 모든 측면에 대 한 정보를 유지 관리 합니다 (이러한 측면을 전체적으로 로컬 보안 정책 이라고 함). 또한 이름 및 Sid (보안 식별자) 간의 변환에 대 한 다양 한 서비스를 제공 합니다.

보안 하위 시스템은 컴퓨터 시스템에 있는 보안 정책 및 계정을 추적 합니다. 도메인 컨트롤러의 경우 이러한 정책 및 계정은 도메인 컨트롤러가 있는 도메인에 적용 되는 계정입니다. 이러한 정책 및 계정은 Active Directory에 저장 됩니다. LSA 하위 시스템은 개체에 대 한 액세스를 확인 하 고 사용자 권한을 확인 하 고 감사 메시지를 생성 하는 서비스를 제공 합니다.

### <a name="security-support-provider-interface"></a>보안 지원 공급자 인터페이스
SSPI (Security Support Provider Interface)는 배포 응용 프로그램 프로토콜에 대 한 인증, 메시지 무결성, 메시지 개인 정보 및 보안 서비스 품질에 대 한 통합 보안 서비스를 얻는 API입니다.

SSPI는 GSSAPI (Generic Security Service API)의 구현입니다. SSPI는 배포 응용 프로그램이 보안 프로토콜의 세부 정보를 알지 못해도 인증 된 연결을 얻기 위해 여러 보안 공급자 중 하나를 호출할 수 있는 메커니즘을 제공 합니다.

## <a name="see-also"></a>참고 항목

-   [보안 지원 공급자 인터페이스 아키텍처](security-support-provider-interface-architecture.md)

-   [Windows 인증의 자격 증명 프로세스](credentials-processes-in-windows-authentication.md)

-   [Windows 인증 기술 개요](https://technet.microsoft.com/library/dn169029.aspx)


