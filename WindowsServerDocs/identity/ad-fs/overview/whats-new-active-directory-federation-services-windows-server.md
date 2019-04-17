---
ms.assetid: aa892a85-f95a-4bf1-acbb-e3c36ef02b0d
title: Windows Server 2016에 대 한 Active Directory Federation Services 새로운 기능
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 09/08/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: b8dd9174a869110d98ba1e65cbf2c2b6ec000b71
ms.sourcegitcommit: f26d2668f57624a3865ca4ffd36a698eea7b503e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/12/2018
---
# <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Windows Server 2016에 대 한 Active Directory Federation Services 새로운 기능

>Windows Server 2016 적용 됩니다.

## <a name="whats-new-in-active-directory-federation-services-for-windows-server-2016"></a>Windows Server 2016에 대 한 Active Directory Federation Services 새로운 기능   
Adfs의 이전 버전에 대 한 정보를 찾는 경우 다음 문서를 참조 하세요.  
 [Windows Server 2012 또는 2012 r 2에서 ADFS](https://technet.microsoft.com/library/hh831502.aspx) 및 [ADFS 2.0](https://technet.microsoft.com/library/adfs2.aspx)  

 다양 한 Office 365, 클라우드를 포함 하 여 응용 프로그램에서의 단일 로그인 기반 SaaS 응용 프로그램 및 회사 네트워크에서 응용 프로그램 및 active Directory Federation Services 액세스 제어 제공 합니다.  
* IT 조직에 대 한 수에 기호를 제공 하 고 액세스 제어 최신 및 레거시 응용 프로그램에 온-프레미스 하 고, 클라우드의 같은 자격 증명 및 정책에 따라 수 있습니다.    
* 사용자의 경우에 익숙한, 같은 계정 자격 증명을 사용 하 여 원활 하 게 로그인을 제공 됩니다.  
* 개발자에 대 한 사용자 노력 응용 프로그램, 하지 인증 또는 신원을에 집중할 수 있도록 조직 디렉터리에 live id를 인증 하는 편리한 방법을 제공 합니다.  

이 문서 ADFS (AD FS 2016) Windows Server 2016의 새로운 기능에 대해 설명 합니다.  

## <a name="eliminate-passwords-from-the-extranet"></a>암호 엑스트라넷에서 제거  
Phished 누수 하거나 도난당 한 암호를에서 손상 시킬 AD FS 2016 수 있도록 3 대 한 새로운 옵션이 하므로 조직 위험이 네트워크 암호를 않고도 로그인 합니다. 

### <a name="sign-in-with-azure-multi-factor-authentication"></a>Azure 다단계 인증을 사용 하 여 로그인
광고 FS 2016 기반 다단계 인증 ADFS Windows Server 2012 r 2에서의 (MFA) 기능에는 Azure MFA 코드를 사용 하 여 먼저 사용자 이름 및 암호를 입력 하지 않고 로그인 수 있도록 하 여 합니다.

* Azure MFA 주 인증 방법으로,와 사용자의 이름과 Azure 인증자 앱에서 OTP 코드에 대 한 메시지가 나타납니다.  
* Azure MFA 보조 또는 추가 인증 방법으로, 사용자 제공 또는 OTP 기반 Azure MFA 로그인 주 인증 자격 증명 (통합 인증 Windows, 사용자 이름 및 암호, 스마트 카드 또는 사용자 또는 디바이스 인증서 사용)을 선택한 다음 텍스트 음성에 대 한 프롬프트를 표시 합니다.  
* 새로운 기본 제공 Azure MFA 어댑터와 설치 및 구성 Adfs와 MFA Azure에 대 한는 이전 보다 훨씬 더 간단 합니다.
* 조직에서 프레미스 Azure MFA 서버에 대 한 필요 없이 Azure MFA 기능을 수행할 수 있습니다.
* Azure MFA 인트라넷 익스트라넷 또는 모든 액세스를 제어 정책의 일환으로 구성할 수 있습니다.

Azure MFA ADFS 사용에 대 한 자세한 내용은
*  [ADFS 2016 및 Azure MFA 구성](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/configure-ad-fs-and-azure-mfa)  

### <a name="password-less-access-from-compliant-devices"></a>암호 없이 액세스 호환 디바이스에서
광고 FS 2016에 로그인을 할 수 있도록 장치 등록 기능 이전에 빌드 및 액세스 제어 디바이스 호환성 상태를 기반으로 합니다. 사용자가 디바이스 자격 증명을 사용 하 여 로그인 할 수 고 준수가 다시 디바이스 속성을 변경 하 계산 정책이 적용 되는 항상 되도록 할 수 있습니다.  와 같은 이렇게 하면 정책

* 관리 및/또는 호환 되는 장치에서 액세스할 수 있도록  
* 관리 및/또는 호환 되는 장치와 에서만에서 익스트라넷 액세스를 활성화  
* 컴퓨터 관리 되거나 호환 되지 않는 다단계 인증 요구  

Adfs에 프레미스 구성 조건부 액세스 정책을 하이브리드 시나리오에서 제공합니다. Azure AD에 대 한 조건 액세스 클라우드 리소스도 장치를 등록할 때 디바이스 id ADFS 정책을 사용할 수 있습니다.

![새로운 기능](media/whats-new-in-active-directory-federation-services-for-windows-server-2016/ADFS_ITPRO4.png)  

 디바이스 사용에 대 한 자세한 내용은 클라우드에서 조건부 액세스를 기반으로   
 *  [Azure Active Directory 조건부 액세스](https://azure.microsoft.com/en-us/documentation/articles/active-directory-conditional-access/)

디바이스 사용에 대 한 자세한 내용은 기반 Adfs와 조건부 액세스
*  [디바이스에 대 한 계획 기반 Adfs와 조건부 액세스](../../ad-fs/deployment/Plan-Device-based-Conditional-Access-on-Premises.md)  
* [Adfs의 액세스를 제어 정책](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="sign-in-with-windows-hello-for-business"></a>사용 하 여 로그인 비즈니스용 Windows Hello   
Windows 10 디바이스에 Windows Hello 및 비즈니스용 Windows Hello를 교체 하는 사용자의 암호를 소개 강력한 장치 바인딩된 사용자 자격 증명 사용자의 제스처 (PIN, 지문 또는 얼굴 인식 같은 생체 인식 제스처)으로 보호 합니다. 광고 FS 2016 지원 이러한 새로운 이러한 새로운 Windows 10 기능 사용자 인트라넷 또는 암호를 않고도 익스트라넷에서 ADFS 응용 프로그램에 로그인 할 수 있도록 합니다.

사용 하 여 Microsoft Windows Hello 비즈니스를 위한 조직에 대 한 자세한 내용은
*  [비즈니스용 Windows Hello에서 활성화 조직](https://azure.microsoft.com/en-us/documentation/articles/active-directory-azureadjoin-passport-deployment/)

## <a name="secure-access-to-applications"></a>응용 프로그램에 대 한 액세스를 보호 합니다.

### <a name="modern-authentication"></a>최신 인증
광고 FS 2016 최신 Windows 10으로 최신 iOS 및 Android 디바이스 및 앱에 대 한 사용자 환경 개선을 제공 하는 최신 프로토콜을 지원 합니다.  

자세한 내용은 참조 [개발자를 위해 광고 FS 시나리오](../../ad-fs/overview/AD-FS-Scenarios-for-Developers.md)  


### <a name="configure-access-control-policies-without-having-to-know-claim-rules-language"></a>알고를 않고도 액세스 제어 정책을 구성 규칙 언어 주장  
이전에 ADFS 관리자에 ADFS 클레임 규칙 언어를 사용 하 여 정책을 구성 하 구성 하 고 정책을 관리 어렵습니다. 액세스를 제어 정책을 사용 하 여 관리자 사용 하 여 템플릿이 제공된과 같은 일반적인 정책이 적용 하려면
* 인트라넷 액세스만 허용
* 모든 허용 하 고 필요 MFA 익스트라넷에서
* 모든 허용 하 고 특정 그룹에서 MFA 필요

템플릿을은 프로세스 구동 마법사 예외 또는 추가 정책 규칙 추가를 사용 하 여 사용자 지정 하기 하 고 일관 된 정책 적용 하나 또는 여러 응용 프로그램에 적용할 수 있습니다.

자세한 내용은 참조 [adfs에서 액세스 제어 정책입니다.](../../ad-fs/operations/Access-Control-Policies-in-AD-FS.md)  

### <a name="enable-sign-on-with-non-ad-ldap-directories"></a>비 광고 LDAP 디렉터리에 대해 로그인에 사용  
많은 조직에는 Active Directory 및 제 3 자 디렉터리의 조합입니다. 사용자 LDAP v3 호환 디렉터리에 저장 된 인증에 대 한 ADFS 지원 추가 하 여에 ADFS 이제 사용할 수 있습니다.
* 제 3 자 LDAP v3 호환 디렉터리의 사용자
* 사용자의 Active Directory 양방향 신뢰 하지 구성 되어 된 Active Directory 숲
* 사용자가 Active Directory 무게는 가벼우며 디렉터리 서비스 (AD LDS)에서

자세한 내용은 참조 [ADFS 사용자 LDAP 디렉터리에 저장 된 인증을 구성 합니다.](../../ad-fs/operations/Configure-AD-FS-to-authenticate-users-stored-in-LDAP-directories.md)  

## <a name="better-sign-in-experience"></a>더 나은 로그인 환경
### <a name="customize-sign-in-experience-for-ad-fs-applications"></a>로그인 ADFS 응용 프로그램에 대 한 경험을 사용자 지정  
들은 사용자 로부터 각 응용 프로그램에 대 한 로그온 경험을 사용자 지정할 수 특히 여러 개의 다른 회사 또는 브랜드 표현 하는 응용 프로그램에에 로그인을 제공 하는 조직에 대 한 멋진 유용성 향상는 수 있습니다.  

이전에 Windows Server 2012 r 2에서 ADFS 모든 파티 응용 프로그램에 대 한 일반적인 증상 환경을 제공, 응용 프로그램 마다 콘텐츠 기반 텍스트의 하위 집합을 사용자 지정할 수 있습니다. Windows Server 2016 뿐만 아니라는 메시지를 하지만 이미지, 응용 프로그램 마다 로고 및 웹 테마를 지정할 수 있습니다. 또한 새로운 사용자 지정 웹 테마를 받으세요 만들고 수 의존 당 적용 자 합니다.  

자세한 내용은 참조 [ADFS 사용자 지정에 로그인 합니다.](../../ad-fs/operations/AD-FS-user-sign-in-customization.md)  



## <a name="manageability-and-operational-enhancements"></a>효율과 운영 향상 된 기능  
다음 Windows Server 2016에 Active Directory Federation Services를 소개 하는 향상 된 운영 시나리오 설명 합니다.  

### <a name="streamlined-auditing-for-easier-administrative-management"></a>더 쉽게 공공 관리에 대 한 감사 간소화  
광고에 FS Windows Server 2012 R2에 대 한 단일 요청 하 고 로그 기능에 대 한 관련 정보에 대해 생성 하는 수많은 감사 이벤트가 했거나 토큰 발급 활동은 없는 (Adfs의 일부 버전) 또는 여러 개의 감사 이벤트에서 손가락을 펼치고 합니다. Adfs의 기본적으로 감사 이벤트의 세부 정보 표시 특성으로 인해 꺼져 있습니다.  
광고 FS 2016의 릴리스를 통해 감사 되 고 더 간소화 되 고 자세 있습니다.  

자세한 내용은 참조 [Adfs의 Windows Server 2016에 대 한 향상 감사 합니다.](../../ad-fs/technical-reference/auditing-enhancements-to-ad-fs-in-windows-server.md)  

### <a name="improved-interoperability-with-saml-20-for-participation-in-confederations"></a>Confederations에 참여 한 SAML 2.0 상호 운용성을 향상 했습니다.  
광고 FS 2016에 여러 엔터티 포함 된 메타 데이터를 기반 신뢰를 가져오는 대 한 지원을 포함 하 여 SAML 프로토콜 지원을 추가 합니다. 이 통해 ADFS InCommon 연합과 표준 2.0 eGov에 맞는 다른 구현 같은 confederations 참여를 구성할 수 있습니다.  

자세한 내용은 참조 [SAML 2.0 상호 운용성을 향상 했습니다.](../../ad-fs/operations/Improved-interoperability-with-SAML-2.0.md)  

### <a name="simplified-password-management-for-federated-o365-users"></a>연방 O365 사용자를 위한 간단한 암호 관리  
Adfs로 보호 되는 신뢰 파티 신뢰 (응용 프로그램)을 Active Directory Federation Services 만료 클레임 암호를 보내려면 (ADFS)를 구성할 수 있습니다. 이러한 클레임 사용 되는 방식을 응용 프로그램에 따라 다릅니다. 예를 들어, 사용자 당사자로 Office 365, 업데이트 곧-에--만료 암호 연합된 사용자에 게 알리려면 교환 및 Outlook을 구현 되었습니다 했습니다.  

자세한 내용은 참조 [구성 ADFS 암호 만료 클레임 보낼 수 있습니다.](../../ad-fs/operations/Configure-AD-FS-to-Send-Password-Expiry-Claims.md)  

### <a name="moving-from-ad-fs-in-windows-server-2012-r2-to-ad-fs-in-windows-server-2016-is-easier"></a>쉽습니다 ADFS Windows Server 2012 r 2에서에서 Windows Server 2016 Adfs로 이동  
이전 농장에서 구성을 내보내고 가져오는 새로운, 병렬 팜에 이전에 필요한 Adfs의 새 버전으로 마이그레이션하기 합니다.  

이제 Windows Server 2016에 ADFS Windows Server 2012 r 2 Adfs에서 이동 훨씬 더 쉽게 되었습니다. Windows Server 2012 r 2 팜을 새로운 Windows Server 2016 서버 추가 하기만 하면 및 모습과 Windows Server 2012 r 2 농장 처럼 작동 하므로 팜 Windows Server 2012 r 2 팜 동작 수준에서 작동 합니다.  

그런 다음 Windows Server 2016 서버 새 그룹에, 기능을 확인할에서 추가 및 제거 이전 서버 부하 분산 합니다. 모든 농장 노드 Windows Server 2016을 실행 하는 되 면 준비가 2016 팜 동작 수준 업그레이드 하 고 새 기능을 사용 하 여 시작 합니다.  

자세한 내용은 참조 [Windows Server 2016에 Adfs로 업그레이드 합니다.](../../ad-fs/deployment/Upgrading-to-AD-FS-in-Windows-Server-2016.md)  
