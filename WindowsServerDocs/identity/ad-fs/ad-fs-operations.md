---
ms.assetid: eefcc989-8763-45ee-8a64-3a97b4397160
title: AD FS 작업
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2db9cd83ed08673835a38e443e90c5eb092f43ac
ms.sourcegitcommit: b649047f161cb605df084f18b573f796a584753b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2020
ms.locfileid: "76162484"
---
# <a name="ad-fs-operations"></a>AD FS 작업



이 문서에는 AD FS에 대 한 모든 설명서 작업 목록이 포함 되어 있습니다. 

## <a name="service-configuration"></a>서비스 구성
- [AD FS 및 WAP 2016에서 SSL 인증서 업데이트](../ad-fs/operations/Manage-SSL-Certificates-AD-FS-WAP-2016.md)
- [AD FS 신속 복원 도구](../ad-fs/operations/AD-FS-Rapid-Restore-Tool.md)
- [AD FS에서 인증서 인증에 대 한 대체 호스트 이름 바인딩을 구성 합니다.](../ad-fs/operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)
- [특성 저장소 추가](../ad-fs/operations/Add-an-Attribute-Store.md)
- [AD FS 2019를 사용 하 여 HTTP 보안 응답 헤더 사용자 지정](../ad-fs/operations/customize-http-security-headers-ad-fs.md)
- [관리자가 아닌 사용자에게 AD FS Powershell Commandlet 액세스 위임](../ad-fs/operations/delegate-ad-fs-pshell-access.md)
- [SQL 및 주소 대기 시간 미세 조정](../ad-fs/operations/adfs-sql-latency.md)
- [AlwaysOn 가용성 그룹](../ad-fs/operations/ad-fs-always-on.md) 


## <a name="authentication-configuration"></a>인증 구성
### <a name="strong-authentication-mfa--password-less"></a>MFA (강력한 인증) & 암호 없음
- [AD FS (2019 이상)에서 기본으로 외부 인증 공급자 구성](../ad-fs/operations/Additional-Authentication-Methods-AD-FS.md)
- [AD FS (2016 이상) 및 Azure MFA 구성](../ad-fs/operations/Configure-AD-FS-2016-and-Azure-MFA.md)
- [AD FS에 대 한 추가 인증 방법 구성](../ad-fs/operations/Configure-Additional-Authentication-Methods-for-AD-FS.md)

### <a name="lockout-protection"></a>잠금 방지
- [AD FS 엑스트라넷 소프트 잠금 보호 구성](../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md)
- [AD FS 엑스트라넷 스마트 잠금 보호 구성](../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [AD FS 엑스트라넷 금지된 IP 구성](../ad-fs/operations/Configure-AD-FS-Banned-IP.md)

### <a name="policy-configuration"></a>정책 구성
- [인증 정책 구성](../ad-fs/operations/Configure-Authentication-Policies.md)
- [대체 로그인 ID 구성](../ad-fs/operations/Configuring-Alternate-Login-ID.md)
- [AD FS 정책과 함께 작동 하도록 Azure AD 프롬프트 로그인 동작 구성](../ad-fs/operations/AD-FS-Prompt-Login.md)

### <a name="kerberos--certificate-authentication"></a>Kerberos & 인증서 인증
- [AD FS에서 kerberos 복합 인증 & AD DS 클레임 사용](../ad-fs/operations/AD-FS-Compound-Authentication-and-AD-DS-claims.md)
- [사용자 인증서 인증을 위한 AD FS 구성](../ad-fs/operations/Configure-User-Certificate-Authentication.md)
- [AD FS에서 인증서 인증에 대 한 대체 호스트 이름 바인딩을 구성 합니다.](../ad-fs/operations/AD-FS-support-for-alternate-hostname-binding-for-certificate-authentication.md)


### <a name="device"></a>장치
- [AD FS의 디바이스 인증 컨트롤](../ad-fs/operations/device-authentication-controls-in-AD-FS.md) 


## <a name="authorization-configuration"></a>권한 부여 구성
- [AD FS에서 Access Control 정책 구성](../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)
- [온-프레미스 디바이스 기반 조건부 액세스 구성](../ad-fs/operations/Configure-Device-based-Conditional-Access-on-Premises.md)

## <a name="rpt--cpt-configuration"></a>RPT & CPT 구성
- [LDAP 디렉터리에 저장된 사용자를 인증하도록 AD FS 구성](../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)
- [클레임 규칙 구성](../ad-fs/operations/Configure-Claim-Rules.md) 
- [클레임 공급자 트러스트 만들기](../ad-fs/operations/Create-a-Claims-Provider-Trust.md) 
- [비 클레임 인식 신뢰 당사자 트러스트 만들기](../ad-fs/operations/Create-a-Non-Claims-Aware-Relying-Party-Trust.md)
- [신뢰 당사자 트러스트 만들기](../ad-fs/operations/Create-a-Relying-Party-Trust.md)
- [집계 된 페더레이션 공급자와 작동 하도록 AD FS 구성 (예: InCommon)](../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)

## <a name="sign-in-experience-configuration"></a>로그인 환경 구성
- [AD FS 2016 Single Sign On 설정 구성](../ad-fs/operations/AD-FS-2016-Single-Sign-On-Settings.md)
- [페이지를 매긴 로그인 AD FS 구성](../ad-fs/operations/AD-FS-paginated-sign-in.md)
- [사용자 로그인 사용자 지정 AD FS 구성](../ad-fs/operations/AD-FS-user-sign-in-customization.md)
- [암호 만료 클레임을 보내도록 AD FS 구성](../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)
- [WIA를 지원하지 않는 디바이스에 대한 인트라넷 폼 기반 인증 구성](../ad-fs/operations/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA.md)

## <a name="other"></a>기타
- [회사 애플리케이션 전반에 SSO 및 연속된 두 번째 단계 인증을 위한 모든 디바이스의 작업 공간 연결](../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [중요 애플리케이션에 추가 Multi-Factor Authentication을 사용하여 위험 관리](../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
- [조건부 액세스 제어를 사용하여 위험 관리](../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)
- [AD FS 실습 환경 설정](../ad-fs/operations/Set-up-an-AD-FS-lab-environment.md)
- [연습 가이드: 중요 한 응용 프로그램에 대 한 추가 Multi-Factor Authentication로 위험 관리](../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)
- [연습 가이드: 조건부 Access Control를 사용 하 여 위험 관리](../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Conditional-Access-Control.md)
- [연습: Windows 장치를 사용 하 여 Workplace Join](../ad-fs/operations/Walkthrough--Workplace-Join-with-a-Windows-Device.md)
- [연습: iOS 장치를 사용 하 여 Workplace Join](../ad-fs/operations/Walkthrough--Workplace-Join-with-an-iOS-Device.md)

  


