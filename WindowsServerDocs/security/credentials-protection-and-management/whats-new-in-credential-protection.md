---
title: 자격 증명 보호의 새로운 기능
description: Windows Server 보안
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f297
author: gitmichiko
ms.author: michikos
manager: dongill
ms.date: 03/06/2017
ms.openlocfilehash: 2351be82ad1d8b9af17715ce363836f57c71ea66
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386915"
---
# <a name="whats-new-in-credential-protection"></a>자격 증명 보호의 새로운 기능

## <a name="credential-guard-for-signed-in-user"></a>로그인 한 사용자에 대 한 Credential Guard

Windows 10 버전 1507부터 Kerberos 및 NTLM은 가상화 기반 보안을 사용 하 여 로그인 한 사용자 로그온 세션의 Kerberos & NTLM 암호를 보호 합니다. 

Windows 10, 버전 1511부터 자격 증명 관리자는 가상화 기반 보안을 사용 하 여 도메인 자격 증명 형식의 저장 된 자격 증명을 보호 합니다. 로그인 한 자격 증명과 저장 된 도메인 자격 증명은 원격 데스크톱을 사용 하 여 원격 호스트에 전달 되지 않습니다. Credential Guard를 UEFI 잠금 없이 사용 하도록 설정할 수 있습니다.

Windows 10, 버전 1607부터 격리 된 사용자 모드가 Hyper-v에 포함 되어 있으므로 더 이상 자격 증명 보호 배포를 위해 별도로 설치 되지 않습니다.

[Credential Guard에 대해 자세히 알아보세요](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard).


## <a name="remote-credential-guard-for-signed-in-user"></a>로그인 한 사용자에 대 한 원격 Credential Guard

Windows 10, 버전 1607부터 원격 Credential Guard는 클라이언트 장치에서 Kerberos 및 NTLM 비밀을 보호 하 여 원격 데스크톱을 사용할 때 로그인 한 사용자 자격 증명을 보호 합니다. 원격 호스트에서 네트워크 리소스를 사용자로 평가 하려면 인증 요청에서 클라이언트 장치에 암호를 사용 해야 합니다.

Windows 10 버전 1703부터 원격 Credential Guard는 원격 데스크톱을 사용할 때 제공 된 사용자 자격 증명을 보호 합니다.

[원격 credential guard에 대해 자세히 알아보세요](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard).

## <a name="domain-protections"></a>도메인 보호

도메인 보호를 위해서는 Active Directory 도메인이 필요 합니다.

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>공개 키를 사용 하 여 인증에 대 한 도메인 가입 장치 지원

Windows 10 버전 1507 및 Windows Server 2016부터 도메인 가입 장치에서 Windows Server 2016 DC (도메인 컨트롤러)를 사용 하 여 바인딩된 공개 키를 등록할 수 있는 경우 장치는 Kerberos PKINIT를 사용 하 여 공개 키를 사용 하 여 인증할 수 있습니다. Windows Server 2016 DC에 대 한 인증

Windows Server 2016부터 Kdc는 Kerberos 키 신뢰를 사용 하 여 인증을 지원 합니다.  

[Kerberos 키 신뢰 & 도메인에 가입 된 장치에 대 한 공개 키 지원에 대해 자세히 알아보세요](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication).

### <a name="pkinit-freshness-extension-support"></a>PKINIT Freshness extension 지원

Windows 10, 버전 1507 및 Windows Server 2016부터 Kerberos 클라이언트는 공개 키 기반 로그인을 위해 PKInit freshness extension을 시도 합니다. 

Windows Server 2016부터 Kdc는 PKInit freshness 확장을 지원할 수 있습니다.  기본적으로 Kdc는 PKInit freshness 확장을 제공 하지 않습니다. 

[PKINIT freshness extension 지원에](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)대해 자세히 알아보세요.

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>공개 키만 사용자의 NTLM 비밀으로 롤링

Windows Server 2016 DFL (도메인 기능 수준)부터 Dc는 공개 키 전용 사용자의 NTLM 암호 롤링을 지원할 수 있습니다. 이 기능은 하위 unavailble 됩니다.

> [!WARNING] 
> DC가 11 월 8 2016 일 이상으로 업데이트 되기 전에 롤링 NTLM 비밀이 설정 된 도메인에 도메인 컨트롤러를 추가 하는 것은 DC가 충돌 하는 위험을 실행 합니다. 

구성: 새 도메인의 경우이 기능은 기본적으로 사용 하도록 설정 됩니다. 기존 도메인의 경우 Active Directory 관리 센터에서 구성 해야 합니다. 

1. Active Directory 관리 센터의 왼쪽 창에서 도메인을 마우스 오른쪽 단추로 클릭 하 고 **속성**을 선택 합니다.

    ![도메인 속성](../media/Credentials-Protection-And-Management/domain-properties.png)

2. **대화형 로그온에 Microsoft Passport 또는 스마트 카드를 사용 해야 하는 사용자에 대해 로그온 중에 만료 되는 NTLM 비밀 롤링 사용을**선택 합니다.

    ![Autoroll 만료 NTLM 비밀](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. **확인**을 클릭합니다. 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>사용자가 특정 도메인에 가입 된 장치로 제한 될 때 네트워크 NTLM 허용

Windows Server 2016 DFL (도메인 기능 수준) 부터는 사용자가 특정 도메인에 가입 된 장치로 제한 될 때 Dc에서 네트워크 NTLM을 허용 하도록 지원할 수 있습니다. 이 기능은 하위에서 사용할 수 없습니다.

구성: **사용자가 선택한 장치로 제한 된 경우 인증 정책에서 NTLM 네트워크 인증 허용**을 클릭 합니다. 

[인증 정책에 대해 자세히 알아보세요](https://technet.microsoft.com/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos).
