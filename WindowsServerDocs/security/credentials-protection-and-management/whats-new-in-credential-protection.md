---
title: 자격 증명 보호의 새로운 기능
description: Windows Server 보안
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
ms.openlocfilehash: 475b6a0b24b811008ee213c1604d98d9aa9eb092
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447028"
---
# <a name="whats-new-in-credential-protection"></a>자격 증명 보호의 새로운 기능

## <a name="credential-guard-for-signed-in-user"></a>Credential Guard 로그인 한 사용자에 대 한

부터는 Windows 10 버전 1507, Kerberos 및 NTLM 사용 하 여 가상화 기반 보안에서 로그인 한 사용자 로그온 세션의 Kerberos 및 NTLM 암호를 보호 합니다. 

Windows 10 버전 1511부터 자격 증명 관리자 도메인 자격 증명 형식의 저장 된 자격 증명을 보호 하기 위해 가상화 기반 보안을 사용 합니다. 로그인 자격 증명 및 저장 된 도메인 자격 증명이 원격 데스크톱을 사용 하 여 원격 호스트에 전달 되지 않습니다. Credential Guard UEFI 잠금 없이 사용할 수 있습니다.

Windows 10 버전 1607부터 격리 된 사용자 모드 포함 되므로 Hyper-v가 설치 된이 더 이상 별도로 설치 된 Credential Guard 배포에 대 한 합니다.

[Credential Guard 자세히 알아보려면](https://technet.microsoft.com/itpro/windows/keep-secure/credential-guard)합니다.


## <a name="remote-credential-guard-for-signed-in-user"></a>로그인 한 사용자에 대 한 원격 Credential Guard

Windows 10 버전 1607부터 클라이언트 장치에서 Kerberos 및 NTLM 암호를 보호 하 여 원격 데스크톱을 사용 하는 경우 원격 Credential Guard 로그인 한 사용자 자격 증명을 보호 합니다. 사용자로 네트워크 리소스를 평가 하기 위해 원격 호스트에 대 한 인증 요청에 암호를 사용 하도록 클라이언트 장치가 필요 합니다.

Windows 10 버전 1703부터 원격 데스크톱을 사용 하는 경우 원격 Credential Guard 제공 된 사용자 자격 증명을 보호 합니다.

[원격 credential guard에 자세히 알아보려면](https://technet.microsoft.com/itpro/windows/keep-secure/remote-credential-guard)합니다.

## <a name="domain-protections"></a>도메인 보호

도메인 보호가 Active Directory 도메인이 필요합니다.

### <a name="domain-joined-device-support-for-authentication-using-public-key"></a>공개 키를 사용 하 여 인증에 대 한 도메인에 가입 된 장치 지원

부터 Windows 10 버전 1507 및 Windows Server 2016 도메인 가입 장치를 Windows Server 2016 도메인 컨트롤러 (DC)에 바인딩된 공개 키를 등록할 수 있으면, 다음 장치 인증을 받을 수 PKINIT Kerberos를 사용 하 여 공개 키 Windows Server 2016 DC로 인증 합니다.

Windows Server 2016 부터는 Kdc Kerberos 키 트러스트를 사용 하 여 인증을 지원 합니다.  

[도메인에 가입 된 장치 및 Kerberos 키 트러스트에 대 한 공개 키 지원에 자세히 알아보려면](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)합니다.

### <a name="pkinit-freshness-extension-support"></a>PKINIT 새로 고침 확장 지원

Windows 10, 버전 1507 및 Windows Server 2016 부터는 Kerberos 클라이언트 공개 키 기반된-sign on에 대 한 PKInit 새로 고침 확장을 시도 합니다. 

Windows Server 2016 부터는 Kdc PKInit 새로 고침 확장을 지원할 수 있습니다.  기본적으로 Kdc PKInit 새로 고침 확장을 제공 하지 않습니다. 

[PKINIT 새로 고침 확장 지원에 자세히 알아보려면](https://technet.microsoft.com/windows-server-docs/security/kerberos/whats-new-in-kerberos-authentication)합니다.

### <a name="rolling-public-key-only-users-ntlm-secrets"></a>공개 키만 사용자의 NTLM 암호 롤링

(DFL) Windows Server 2016 도메인 기능 수준부터 Dc 공개 키만 사용자의 NTLM 암호 롤링 지원할 수 있습니다. 이 기능은 더 낮은 DFLs에서 unavailble입니다.

> [!WARNING] 
> 롤링 DC로 업데이트 되었습니다 이상 2016 년 11 월 8 일 서비스 실행 전에 사용 하도록 설정 하는 NTLM 암호 DC 충돌의 위험이 있는 도메인에 도메인 컨트롤러를 추가 합니다. 

구성: 새 도메인에 대 한이 기능은 기본적으로 사용 됩니다. 기존 도메인에 대 한 Active Directory 관리 센터에서 구성 되어야 합니다. 

1. Active Directory 관리 센터에서 왼쪽된 창에서 도메인을 마우스 오른쪽 단추로 누르고 **속성**합니다.

    ![도메인 속성](../media/Credentials-Protection-And-Management/domain-properties.png)

2. 선택 **롤링 만료 NTLM 암호 로그인 중에 대화형 로그온에 대 한 Microsoft Passport 또는 스마트 카드를 사용 하는 데 필요한 사용자에 게 사용**합니다.

    ![Autoroll 만료 NTLM 암호](../media/Credentials-Protection-And-Management/autoroll-ntlm.png)

3. **확인**을 클릭합니다. 

### <a name="allowing-network-ntlm-when-user-is-restricted-to-specific-domain-joined-devices"></a>사용자가 특정 도메인에 가입 된 장치를 제한 하는 경우 네트워크 NTLM 허용

Windows Server 2016 도메인 기능 수준 (DFL) Dc로 시작 하는 사용자가 특정 제한 된 도메인에 가입 된 장치 허용 네트워크 NTLM을 지원할 수 있습니다. 이 기능은 더 낮은 DFLs에서 사용할 수 없습니다.

구성: 인증 정책에서 클릭 **NTLM 허용 네트워크 인증 사용자가 제한 하는 경우 선택한 장치**합니다. 

[인증 정책에 자세히 알아보려면](https://technet.microsoft.com/windows-server-docs/security/credentials-protection-and-management/authentication-policies-and-authentication-policy-silos)합니다.
