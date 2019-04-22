---
title: 방지 Kerberos RC4 비밀 키를 사용 하는 암호를 변경 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 3cfa4ae2442f0cd1e3e4110a355da675fa2d61db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816274"
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>Kerberos가 RC4 비밀 키를 사용하는 암호를 변경하지 못하도록 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2008 R2 및 Windows Server 2008

IT 전문가 위한이 항목에서는 몇 가지 제한 사항이 사용자 계정 제어 악의적인 사용자에 게 발생할 수 있는 Kerberos 프로토콜에 설명 합니다. 잘 알려진 업계에 공격자 사용자로 인증 하거나 공격자가 사용자의 비밀 키를 알고 있는 경우 해당 사용자의 암호를 변경 합니다. 여기서는 Kerberos 네트워크 인증 서비스 (V5) 표준 (RFC 4120)에 제한이 있습니다.

소유 사용자의 암호에서 파생 된 Kerberos 비밀 키 (RC4 및 Advanced Encryption Standard [AES] 기본적으로)의 RFC 4757 마다 Kerberos 암호 변경 교환 중 유효성이 검사 됩니다. 사용자의 일반 텍스트 암호를 키 배포 센터 (KDC)를 제공 하지 않습니다. 기본적으로 Active Directory 도메인 컨트롤러 계정에 대 한 일반 텍스트 암호의 복사본을가지고 있지 않기를 도메인 컨트롤러는 Kerberos 암호화 종류를 지원 하지 않으면, 암호를 변경 하려면 해당 비밀 키를 사용할 수 없습니다. 

이 항목의 시작 부분에 적용 됩니다. 목록에 지정 된 Windows 운영 체제에서 RC4 비밀 키를 사용 하 여 Kerberos를 사용 하 여 암호를 변경 하는 기능을 차단 하는 방법은 세 가지가 있습니다.

- 사용자 구성 대화형 로그온에 스마트 카드 계정 옵션을 포함 하도록 계정이 필요 합니다. 이 사용자만 RC4 인증 서비스 요청 (AS 않아) 거부 됩니다 있도록 유효한 스마트 카드를 로그인을 제한 합니다. 계정에서 계정 옵션을 설정 하려면 계정 속성 클릭 마우스 오른쪽 단추로 클릭 하 고 계정 탭을 클릭 합니다. 

- 모든 도메인 컨트롤러에서 Kerberos에 대 한 RC4 지원을 사용 하지 않도록 설정 합니다. 이 최소 Windows Server 2008 도메인 기능 수준 및 모든 Kerberos 클라이언트, 응용 프로그램 서버와 도메인 간의 트러스트 관계 AES를 지원 해야 합니다는 환경에 필요 합니다. Aes 지원 Windows Server 2008 및 Windows Vista에서 도입 되었습니다.

    [!NOTE]
    시스템이 다시 시작 될 수 있습니다 RC4를 사용 하지 않도록 설정 하는 알려진된 문제가 있습니다. 다음 핫픽스를 참조 하세요.
    - [Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - 이전 버전의 Windows Server에 대 한 핫픽스가 없습니다 수

- Windows Server 2012 R2 도메인 기능 수준을 이상으로, 도메인 집합을 배포 하 고 보호 된 사용자 보안 그룹의 구성원으로 사용자를 구성 합니다. Kerberos 프로토콜에서 이상의 RC4 사용을 방해 하는이 기능을 하기 때문에 다음에서 리소스를 참조 하세요 [참고](#see-also) 섹션입니다.

## <a name="see-also"></a>관련 항목

- Windows Server 2012 R2 도메인에서 RC4 암호화 종류의 사용을 방지 하는 방법에 대 한 정보를 참조 하세요 [Protected Users Security Group](/../credentials-protection-and-management/protected-users-security-group.md), 및 [How to Configure Protected Accounts](/../credentials-protection-and-management/how-to-configure-protected-accounts.md)합니다.

- RFC 4120 및 RFC 4757에 대 한 설명을 참조 하세요 [IETF 문서](http://tools.ietf.org/html/)합니다.
