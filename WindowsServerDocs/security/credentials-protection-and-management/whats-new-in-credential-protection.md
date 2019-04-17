---
title: "자격 증명 보호의 새로운 기능"
description: "Windows Server 보안"
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0556c606b987a69eae663b0196467f532d5a307a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2017
---
# <a name="whats-new-in-credential-protection"></a>자격 증명 보호의 새로운 기능

## <a name="credential-guard-for-signed-in-user"></a>사용자의 로그인 자격 증명 보호

Windows 10 버전 1507, 부터는 Kerberos 및 NTLM 사용 virtualization 기반 보안 로그온 한 사용자에 로그온 세션 Kerberos 및 NTLM 비밀 정보를 보호 하기 위해 합니다. 

자격 증명 관리자 일부 터 Windows 10 버전 1511이 릴리스, 보안 virtualization 기반 도메인 자격 증명 종류의 저장 된 자격 증명을 보호 하기 위해 사용 합니다. 원격 데스크톱을 사용 하 여 원격 호스트에에 로그인 자격 증명 하 고 저장 된 도메인 자격 증명 되지 전달 됩니다. UEFI 잠금 없이 보호 자격 증명을 사용할 수 있습니다.

일부 터 Windows 10 버전 1607 격리 된 사용자 모드에 포함 되어 Hyper-v 있으므로 더 이상 설치 별도로 자격 증명 가드 배포를 위해 합니다.

[자격 증명 보호에 대 한 자세한](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/credential-guard)합니다.


## <a name="remote-credential-guard-for-signed-in-user"></a>사용자의 로그인에 대 한 원격 자격 증명 보호

원격 자격 증명 가드 클라이언트 디바이스에서 Kerberos 및 NTLM 비밀 정보를 보호 하 여 원격 데스크톱을 사용 하는 경우 사용자의 로그인 자격 증명을 보호로 Windows 10 버전 1607 시작 합니다. 사용자로 네트워크 리소스를 평가 하 원격 호스트 인증 요청 비밀 정보를 사용 하는 클라이언트 장치가 필요 합니다.

Windows 10 버전을 1703 부터는 원격 데스크톱을 사용 하는 경우 원격 자격 증명 가드 제공된 사용자 자격을 보호 합니다.

[원격 자격 증명 보호에 대 한 자세한](https://technet.microsoft.com/en-us/itpro/windows/keep-secure/remote-credential-guard)합니다.

## <a name="domain-protections"></a>도메인 보호

도메인 보호 Active Directory 도메인이 필요합니다.

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>도메인 가입 장치 지원 공개 키를 사용 하 여 인증에 대 한

도메인에 가입 하는 디바이스를 Windows Server 2016 DC (도메인 컨트롤러)와 바인딩된 공개 키를 등록할 수 있으면 Windows 10 버전 1507 및 Windows Server 2016 년부터, 디바이스 수 인증 되 고 Windows Server 2016 dc Kerberos PKINIT 인증을 사용 하는 공개 키 합니다.

Windows Server 2016 부터는 Kdc Kerberos 주요 신뢰를 사용 하 여 인증을 지원 합니다.  

[도메인 가입 디바이스 및 Kerberos 주요 신뢰 공개 키 지원에 대 한 자세한](https://technet.microsoft.com/en-us/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)합니다.

### <a name="pkinit-freshness-extension-support"></a>확장 지원이 PKINIT 새로 고침

Windows 10 버전 1507 및 Windows Server 2016부터, Kerberos 클라이언트 PKInit 새로 고침 확장 공개 키-기반된 로그인-기능에 대 한 시도 합니다. 

Windows Server 2016 부터는 Kdc PKInit 새로 고침 확장을 지원할 수 있습니다.  기본적으로 Kdc PKInit 새로 고침 확장을 제공 하지 않습니다. 

[PKINIT 새로 고침 확장 지원에 대 한 자세한](https://technet.microsoft.com/en-us/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)합니다.

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>공개 주요만 사용자의 NTLM 비밀 정보를 배포합니다.

Windows Server 2016 도메인 기능 수준을 (DFL)부터, Dc 공개 키만 사용자의 NTLM 비밀 배포 지원할 수 있습니다. 이 기능은 unavailble DFLs 아래에 있습니다.

> [!WARNING] 
> DC 되어 업데이트 되었습니다 이상 2016 년 11 월 8 일 서비스 실행 하기 전에 활성화 NTLM 비밀 위험 DC 충돌을 배포 된 도메인에 도메인 컨트롤러를 추가 합니다. 

구성: 새 도메인에 대 한이 기능은 기본적으로 활성화 됩니다. 기존 도메인에 대 한 Active Directory 관리 센터에서 구성 합니다. 

1. Active Directory 관리 센터에서 도메인 왼쪽된 창에서 마우스 오른쪽 단추로 클릭 하 고 선택 **속성**합니다.

    ![도메인 속성](../media/Credentials-Protection-And-Management/domain-properties.png)
    
2. 선택 **배포 만료 NTLM 비밀 로그인 하는 동안, Microsoft Passport 또는 스마트 카드 로그온 대화형에 사용 하는 데 필요한 사용자에 대 한 사용**합니다.

    ![Autoroll 만료 NTLM 비밀 정보](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. 클릭 **확인**합니다. 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>사용자가 도메인에 가입 하는 특정 디바이스를 제한 하는 경우 네트워크 NTLM 허용

Windows Server 2016 도메인 기능 수준 (DFL) Dc로 시작 하는 사용자가 특정으로 제한 도메인에 가입 장치 때 수 있도록 네트워크 NTLM 지원할 수 있습니다. 이 기능은 낮은 DFLs에서 사용할 수 없습니다.

구성: 인증 정책에서 클릭 **NTLM 허용 네트워크 인증 사용자를 제한 된 경우 디바이스를 선택한**합니다. 

[인증 정책에 대 한 자세한](https://technet.microsoft.com/en-us/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos)합니다.
