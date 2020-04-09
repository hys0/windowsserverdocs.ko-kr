---
title: 자격 증명 보호 및 관리
description: Windows Server 보안
ms.prod: windows-server
ms.technology: security-credential-protection
ms.topic: article
ms.assetid: e457229c-0126-40fe-948c-101c943e1b57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: c836da8f83510e6547e0e182ac06fd2151dd9c41
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857066"
---
# <a name="credentials-protection-and-management"></a>자격 증명 보호 및 관리

>적용 대상: Windows Server(반기 채널), Windows Server 2016

IT 전문가를 위한이 항목에서는 Windows Server 2012 r 2에 도입 된 기능 및 방법에 대해 설명 하 고 자격 증명 보호 및 도메인 인증 제어를 위한 Windows 8.1 자격 증명 도난을 줄이기 위해 설명 합니다.

## <a name="BKMK_CredentialsProtectionManagement"></a>
### <a name="restricted-admin-mode-for-remote-desktop-connection"></a>원격 데스크톱 연결에 대한 제한된 관리자 모드
제한된 관리자 모드에서는 서버에 자격 증명을 전송하지 않고 원격 호스트 서버에 대화형으로 로그온하는 방법을 제공합니다. 이 방법을 사용하면 서버가 손상된 경우 초기 연결 프로세스 중에 자격 증명이 수집되지 않습니다.

관리자 자격 증명으로 이 모드를 사용하면 원격 데스크톱 클라이언트에서 자격 증명을 보내지 않고 이 모드를 지원하는 호스트에 대화형으로 로그온합니다. 호스트에서 연결하는 사용자 계정에 관리자 권한이 있으며 제한된 관리자 모드를 지원한다는 것을 확인하면 연결에 성공합니다. 그렇지 않으면 연결 시도에 실패합니다. 제한된 관리자 모드에서는 어떤 경우에도 일반 텍스트 또는 다른 형식의 재사용 가능한 자격 증명을 원격 컴퓨터에 보내지 않습니다.

### <a name="lsa-protection"></a>LSA 보호
LSASS(Local Security Authority Subsystem Service) 프로세스 내에 상주하는 LSA(로컬 보안 기관)는 사용자의 로컬 및 원격 로그인에 대한 유효성을 검사하고 로컬 보안 정책을 적용합니다. Windows 8.1 운영 체제에서는 보호 되지 않은 프로세스에의 한 코드 삽입을 방지 하기 위해 LSA에 대 한 추가 보호 기능을 제공 합니다. 이로 인해 LSA에서 저장 및 관리하는 자격 증명에 대한 보안이 강화됩니다. LSA에 대 한이 보호 된 프로세스 설정은 Windows 8.1에서 구성할 수 있지만 Windows RT 8.1에서는 기본적으로 켜져 있으며 변경할 수 없습니다.

LSA 보호 구성에 대한 자세한 내용은 [Configuring Additional LSA Protection](configuring-additional-lsa-protection.md)을 참조하세요.

### <a name="protected-users-security-group"></a>보호된 사용자 보안 그룹
이 새 도메인 글로벌 그룹은 Windows Server 2012 R2 및 Windows 8.1를 실행 하는 장치 및 호스트 컴퓨터에서 구성할 수 없는 새 보호 기능을 트리거합니다. 보호 된 사용자 그룹은 Windows Server 2012 R2 도메인의 도메인 컨트롤러 및 도메인에 대 한 추가 보호를 사용 하도록 설정 합니다. 이는 사용자가 손상되지 않은 컴퓨터에서 네트워크의 컴퓨터에 로그인하는 경우 사용 가능한 자격 증명 유형을 크게 줄여 줍니다.

보호된 사용자 그룹의 구성원은 다음 인증 방법을 통해 추가로 제한됩니다.

-   보호된 사용자 그룹의 구성원은 Kerberos 프로토콜을 통해서만 서명할 수 있습니다. NTLM, 다이제스트 인증 또는 CredSSP를 사용하여 계정을 인증할 수 없습니다. Windows 8.1를 실행 하는 장치에서는 암호가 캐시 되지 않으므로 이러한 Ssp (보안 지원 공급자) 중 하나를 사용 하는 장치는 계정이 보호 된 사용자 그룹의 구성원 인 경우 도메인 인증에 실패 합니다.

-   Kerberos 프로토콜은 사전 인증 프로세스에서 보다 약한 DES 또는 RC4 암호화 종류를 사용하지 않습니다. 즉, 해당 도메인이 최소한 AES 암호 제품군을 지원하도록 구성되어야 합니다.

-   Kerberos 제한 또는 제한 되지 않은 위임으로 사용자 계정을 위임할 수 없습니다. 즉, 사용자가 보호된 사용자 그룹의 구성원인 경우 다른 시스템에 대한 이전 연결이 실패할 수 있습니다.

-   ADAC(Active Directory 관리 센터)를 통해 액세스한 인증 정책 및 사일로를 사용하여 기본 Kerberos TGT(허용 티켓) 수명 설정(4시간)을 구성할 수 있습니다. 즉, 4시간이 경과한 경우 사용자가 다시 인증을 받아야 합니다.

> [!WARNING]
> 서비스 및 컴퓨터 계정은 보호된 사용자 그룹의 구성원이 될 수 없습니다. 암호 또는 인증서를 호스트에서 항상 사용할 수 있으므로, 이 그룹에는 로컬 보호 기능이 제공되지 않습니다. 보호 된 사용자 그룹에 추가 된 모든 서비스 또는 컴퓨터에 대해 "사용자 이름 또는 암호가 잘못 되었습니다." 오류가 발생 하 여 인증이 실패 합니다.

이 그룹에 대한 자세한 내용은 [보호된 사용자 보안 그룹](protected-users-security-group.md)을 참조하세요.

### <a name="authentication-policy-and-authentication-policy-silos"></a>인증 정책 및 인증 정책 사일로
포리스트 기반 Active Directory 정책은 도입 되었으며 Windows Server 2012 R2 도메인 기능 수준을 사용 하는 도메인의 계정에 적용할 수 있습니다. 이러한 인증 정책은 사용자가 로그인하는 데 사용할 수 있는 호스트를 제어할 수 있습니다. 보호된 사용자 보안 그룹과 함께 작동하며 관리자는 계정 인증을 위한 액세스 제어 조건을 적용할 수 있습니다. 이러한 인증 정책은 관련 계정을 격리하여 네트워크 범위를 제한합니다.

새 Active Directory 개체 클래스인 인증 정책을 사용 하면 Windows Server 2012 R2 도메인 기능 수준에서 도메인의 계정 클래스에 인증 구성을 적용할 수 있습니다. 인증 정책은 Kerberos AS 또는 TGS 교환 중에 적용됩니다. Active Directory 계정 클래스는 다음과 같습니다.

-   사용자

-   컴퓨터

-   관리 서비스 계정

-   그룹 관리 서비스 계정

자세한 내용은 [인증 정책 및 인증 정책 사일로](authentication-policies-and-authentication-policy-silos.md)를 참조하세요.

보호된 계정을 구성하는 방법에 대한 자세한 내용은 [보호된 계정을 구성하는 방법](how-to-configure-protected-accounts.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
LSA 및 LSASS에 대한 자세한 내용은 [Windows 로그온 및 인증 기술 개요](https://technet.microsoft.com/library/dn169029(v=ws.10).aspx)를 참조하세요.



