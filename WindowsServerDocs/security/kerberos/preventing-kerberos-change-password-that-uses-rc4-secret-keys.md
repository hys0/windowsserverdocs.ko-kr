---
title: "않아 Kerberos r c 4 비밀 키를 사용 하는 암호 변경"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 3cfa4ae2442f0cd1e3e4110a355da675fa2d61db
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>않아 Kerberos r c 4 비밀 키를 사용 하는 암호 변경

>적용 대상: (세미콜론 연간 채널) Windows Server, Windows Server 2016, Windows Server 2008 R2 및 Windows Server 2008

IT 전문가 위한이 여기서 Kerberos 프로토콜 악의적인 사용자가 사용자의 계정을 제어 발생할 수 있는 몇 가지 제한이 설명 합니다. 공격자 사용자도 인증 하거나 공격자가 사용자의 비밀 키를 알고 있는 경우 해당 사용자의 암호를 변경할 수 이란 업계 내 잘 알려져 Kerberos 네트워크 인증 서비스 (v 5) 표준 (RFC 4120)에 제한이 있습니다.

사용자의에서 파생 된 Kerberos 비밀 키 (r c 4 및 고급 암호화 표준 [AES] 기본적으로)의 소유 RFC 4757 당 Kerberos 암호 변경 교환 중 검증 됩니다. 사용자의 일반 암호를 키 메일 센터 (KDC)를 제공 하지 및 Active Directory 도메인 컨트롤러는 기본적으로 계정에 대 한 일반 암호의 복사본을가지고 있지 않습니다. 도메인 컨트롤러 Kerberos 암호화 종류를 지원 하지 않는 경우 암호를 변경 하려면 해당 비밀 키를 사용할 수 없습니다. 

이 항목의 왼쪽 끝에 적용 됩니다. 목록에 지정 된 Windows 운영 체제의 세 가지 방법으로 Kerberos r c 4 비밀 키를 사용 하 여 암호를 변경 하는 기능을 차단할 수 있습니다.

- 사용자를 구성 스마트 카드 계정 옵션이 포함 된 계정을 로그온 해야 합니다. 이렇게만 r c 4 인증 서비스 (AS 요청) 요청을 거부 되도록 유효한 스마트 카드를 사용 하 여 로그인 하는 사용자를 제한 합니다. 계정에 계정 옵션을 설정 하려면 클릭 속성 계정에서 마우스 오른쪽 단추로 클릭 하 고 계정을 탭을 클릭 합니다. 

- 모든 도메인 컨트롤러에서 Kerberos에 대 한 지원을 r c 4 사용 하지 않도록 설정 합니다. Windows Server 2008 도메인 기능 수준 모든 Kerberos 클라이언트, 응용 프로그램 서버 및 신뢰 관계 도메인에서 AES를 지원 해야 있는 환경 최소가 필요 합니다. Windows Server 2008 및 Windows Vista에서 AES에 대 한 지원 도입 되었습니다.

    [!NOTE]
    시스템을 다시 발생할 수 있는 r c 4 비활성화 알려진된 문제가 있습니다. 다음 핫픽스 참조 하십시오.
    - [Windows Server 2012 r 2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - 이전 버전의 Windows Server에 사용할 수 없음 핫픽스는

- 이상 또는 Windows Server 2012 R2 도메인 기능 수준으로 설정 하는 도메인을 배포 하 고 사용자에 게 사용자 보호 보안 그룹의 회원 구성 합니다. 이 기능을 멈추게 할 Kerberos 프로토콜에만 이상 r c 4 사용을 하기 때문에 다음에서 리소스를 참조 [참고](#see-also) 섹션.

## <a name="see-also"></a>참조 하십시오

- Windows Server 2012 R2 도메인에 r c 4 암호화 유형의 사용 방지 하는 방법에 대 한 정보를 참조 하세요. [사용자가 보안 그룹 보호](/../credentials-protection-and-management/protected-users-security-group.md), 및 [계정 보호 구성 하는 방법을](/../credentials-protection-and-management/how-to-configure-protected-accounts.md)합니다.

- RFC 4120 RFC 4757에 대 한 설명을 볼 [IETF 문서](http://tools.ietf.org/html/)합니다.
