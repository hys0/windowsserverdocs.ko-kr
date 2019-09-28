---
title: RC4 비밀 키를 사용 하는 Kerberos 변경 암호 방지
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 64018f7f118086f3d290cb1ffa9b8d2b3e81c27c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386272"
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>Kerberos가 RC4 비밀 키를 사용하는 암호를 변경하지 못하도록 설정

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2008 R2 및 Windows Server 2008

IT 전문가를 위한이 항목에서는 악의적인 사용자가 사용자 계정을 제어할 수 있는 Kerberos 프로토콜의 몇 가지 제한 사항에 대해 설명 합니다. 공격자가 사용자의 비밀 키를 알고 있는 경우 공격자가 사용자로 인증 하거나 해당 사용자의 암호를 변경 하는 경우 업계 내에서 잘 알려진 Kerberos V5 (네트워크 인증 서비스) 표준 (RFC 4120)에 제한이 있습니다.

RFC 4757에 따라 Kerberos 암호 변경 교환 중에 사용자의 암호 파생 Kerberos 비밀 키 (RC4 및 AES(Advanced Encryption Standard) [AES])의 소유를 확인 합니다. 사용자의 일반 텍스트 암호는 키 배포 센터 (KDC)에 제공 되지 않으며 기본적으로 Active Directory 도메인 컨트롤러에는 계정에 대 한 일반 텍스트 암호 복사본이 없습니다. 도메인 컨트롤러에서 Kerberos 암호화 유형을 지원 하지 않는 경우 암호를 변경 하는 데 해당 비밀 키를 사용할 수 없습니다. 

이 항목의 시작 부분에 있는 적용 대상 목록에 지정 된 Windows 운영 체제에서 RC4 비밀 키와 함께 Kerberos를 사용 하 여 암호를 변경 하는 기능을 차단 하는 세 가지 방법이 있습니다.

- 계정 옵션을 포함 하도록 사용자 계정 구성 대화형 로그온에 스마트 카드 필요 이렇게 하면 사용자가 유효한 스마트 카드로 로그인 하 여 RC4 인증 서비스 요청 (요청)이 거부 되도록 제한 됩니다. 계정에 대 한 계정 옵션을 설정 하려면 계정을 마우스 오른쪽 단추로 클릭 하 고 속성을 클릭 한 다음 계정 탭을 클릭 합니다. 

- 모든 도메인 컨트롤러에서 Kerberos에 대 한 RC4 지원을 사용 하지 않도록 설정 합니다. 이를 위해서는 최소한 Windows Server 2008 도메인 기능 수준 및 도메인에 대 한 모든 Kerberos 클라이언트, 응용 프로그램 서버 및 트러스트 관계가 AES를 지원 해야 합니다. AES에 대 한 지원은 Windows Server 2008 및 Windows Vista에서 도입 되었습니다.

    [!NOTE]
    RC4를 사용 하지 않도록 설정 하면 시스템이 다시 시작 될 수 있는 알려진 문제가 발생 합니다. 다음 핫픽스를 참조 하세요.
    - [Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - 이전 버전의 Windows Server에는 핫픽스를 사용할 수 없습니다.

- Windows Server 2012 R2 도메인 기능 수준 이상으로 설정 된 도메인을 배포 하 고 사용자를 보호 된 사용자 보안 그룹의 구성원으로 구성 합니다. 이 기능은 Kerberos 프로토콜의 RC4 사용 보다 많은 것을 중단 하기 때문에 다음 [참고](#see-also) 항목 섹션의 리소스를 참조 하세요.

## <a name="see-also"></a>관련 항목

- Windows Server 2012 R2 도메인에서 RC4 암호화 유형을 사용 하는 것을 방지 하는 방법에 대 한 자세한 내용은 [보호 된 사용자 보안 그룹](/../credentials-protection-and-management/protected-users-security-group.md)및 [보호 된 계정을 구성 하는 방법](/../credentials-protection-and-management/how-to-configure-protected-accounts.md)을 참조 하세요.

- RFC 4120 및 RFC 4757에 대 한 설명은 [IETF 문서](http://tools.ietf.org/html/)를 참조 하세요.
