---
title: AD FS 암호 공격 보호
description: 이 문서에서는 암호 공격 으로부터 AD FS 사용자를 보호 하는 방법을 설명 합니다.
author: billmath
manager: mtillman
ms.reviewer: andandyMSFT
ms.date: 11/15/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c446ec86d426148836267e29610f86691cf0798a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865460"
---
# <a name="ad-fs-password-attack-protection"></a>AD FS 암호 공격 보호

## <a name="what-is-a-password-attack"></a>암호 공격 이란?

페더레이션된 Single Sign-On에 대 한 요구 사항은 인터넷을 통해 인증할 끝점의 가용성입니다. 인터넷에서 인증 끝점을 사용 하면 사용자가 회사 네트워크에 있지 않은 경우에도 응용 프로그램에 액세스할 수 있습니다. 

그러나이는 일부 잘못 된 행위자가 인터넷에서 사용할 수 있는 페더레이션된 끝점을 활용 하 고 이러한 끝점을 사용 하 여 암호를 시도 및 확인 하거나 서비스 거부 공격을 만들 수 있음을 의미 합니다. 보다 일반적인 공격으로 인 한 공격을 **암호 공격**이라고 합니다. 

일반적인 암호 공격에는 두 가지 유형이 있습니다. 암호 스프레이 공격은 무차별 암호 대입 공격 & 합니다. 

### <a name="password-spray-attack"></a>암호 스프레이 공격
암호 스프레이 공격에서 이러한 잘못 된 행위자는 다양 한 계정 및 서비스에서 가장 일반적인 암호를 사용해 서 찾을 수 있는 모든 암호로 보호 된 자산에 액세스 합니다. 일반적으로 다양 한 조직 및 id 공급자를 포괄 합니다. 예를 들어 공격자는 일반적으로 사용할 수 있는 도구 키트를 사용 하 여 여러 조직에 있는 모든 사용자를 열거 한 다음 "P @ $ $w 0rd" 및 "Password1"를 모든 계정에 대해 시도 합니다. 아이디어를 제공 하기 위해 공격은 다음과 같습니다.


|  대상 사용자   | 대상 암호 |
|----------------|-----------------|
| User1@org1.com |    Password1    |
| User2@org1.com |    Password1    |
| User1@org2.com |    Password1    |
| User2@org2.com |    Password1    |
|       …        |        …        |
| User1@org1.com |    P @ $ $w 0rd     |
| User2@org1.com |    P @ $ $w 0rd     |
| User1@org2.com |    P @ $ $w 0rd     |
| User2@org2.com |    P @ $ $w 0rd     |

이 공격 패턴은 개별 사용자 또는 회사의 유리한 점에서 공격을 격리 된 실패 로그인 처럼 evades 때문에 대부분의 검색 기법을 활용 합니다.

공격자의 경우 숫자 게임입니다. 여기에는 매우 공통적인 몇 가지 암호가 있습니다.  공격자는 모든 천 대의 계정 공격에 대해 몇 가지 성공 하 고이를 효과적으로 사용할 수 있습니다. 계정을 사용 하 여 메일에서 데이터를 가져오고, 연락처 정보를 수집 하 고, 피싱 링크를 보내거나, 암호 스프레이 대상 그룹을 확장 합니다. 공격자는 초기 대상이 무엇 인지에 대해 크게 신경 쓸 수 없습니다.

그러나 AD FS와 네트워크를 올바르게 구성 하는 몇 가지 단계를 수행 하 여 이러한 유형의 공격 으로부터 AD FS 끝점의 보안을 유지할 수 있습니다. 이 문서에서는 이러한 공격 으로부터 보호 하기 위해 올바르게 구성 해야 하는 세 가지 영역에 대해 설명 합니다.

### <a name="brute-force-password-attack"></a>무차별 암호 대입 공격 
이러한 형태의 공격에서 공격자는 대상 계정 집합에 대해 여러 암호를 시도 하려고 시도 합니다. 대부분의 경우 이러한 계정은 조직 내에서 더 높은 수준의 액세스 권한이 있는 사용자를 대상으로 합니다. 이는 조직 내에서 또는 중요 인프라를 관리 하는 관리자 일 수 있습니다.  

이 유형의 공격으로 인해 DOS 패턴이 발생할 수도 있습니다. 이는 ADFS가 서버 수가 부족 하 여 많은 수의 요청을 처리할 수 없거나 사용자가 계정에서 잠긴 사용자 수준에 있을 수 있는 서비스 수준에 있을 수 있습니다.  

## <a name="securing-ad-fs-against-password-attacks"></a>암호 공격에 대 한 AD FS 보안 

그러나 AD FS와 네트워크를 올바르게 구성 하는 몇 가지 단계를 수행 하 여 AD FS 끝점은 이러한 유형의 공격 으로부터 보호 될 수 있습니다. 이 문서에서는 이러한 공격 으로부터 보호 하기 위해 올바르게 구성 해야 하는 세 가지 영역에 대해 설명 합니다. 


- 수준 1, 기준선: 이는 잘못 된 행위자가 페더레이션된 사용자를 무차별 암호 대입 하 게 만들 수 없도록 AD FS 서버에 구성 해야 하는 기본 설정입니다. 
- 수준 2, 엑스트라넷 보호: 이러한 설정은 엑스트라넷 액세스가 보안 프로토콜, 인증 정책 및 적절 한 응용 프로그램을 사용 하도록 구성 되어 있는지 확인 하기 위해 구성 해야 합니다. 
- 수준 3, 엑스트라넷 액세스에 대 한 암호 없는으로 이동: 이는 공격에 취약 한 암호 대신 보다 안전한 자격 증명을 사용 하 여 페더레이션 리소스에 액세스할 수 있도록 하는 고급 설정 및 지침입니다. 

## <a name="level-1-baseline"></a>수준 1: 기준을

1. ADFS 2016을 구현 하는 경우 [엑스트라넷 스마트 잠금](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md) 엑스트라넷 스마트 잠금은 익숙한 위치를 추적 하 고, 이전에이 위치에서 성공적으로 로그인 한 경우 유효한 사용자가 통과할 수 있도록 합니다. 엑스트라넷 스마트 잠금을 사용 하 여 잘못 된 행위자가 사용자에 게 무작위 공격을 수행할 수 없도록 하 고 동시에 합법적인 사용자의 생산성을 높일 수 있습니다.
    - AD FS 2016를 설정 하지 않은 경우 AD FS 2016로 [업그레이드](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) 하는 것이 좋습니다. AD FS 2012 r 2의 간단한 업그레이드 경로입니다. AD FS 2012 r 2를 사용할 경우 [엑스트라넷 잠금을](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md)구현 합니다. 이 방법의 한 가지 단점은 무차별 암호 대입 패턴의 경우 유효한 사용자가 엑스트라넷 액세스에서 차단 될 수 있다는 것입니다. 서버 2016의 AD FS에는 이러한 단점이 없습니다.

2. 의심 스러운 IP 주소를 차단 하 & 모니터링 
    - Azure AD Premium 있는 경우 ADFS에 대 한 Connect Health를 구현 하 고 제공 되는 [위험한 IP 보고서](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-adfs#risky-ip-report-public-preview) 알림을 사용 합니다.

        a. 라이선스는 모든 사용자에 게 적합 하지 않으며 25 개의 라이선스/s s o/WAP 서버가 필요 하며,이는 고객에 게 쉬울 수 있습니다.

        b. 이제 많은 수의 실패 한 로그인을 생성 하는 IP를 조사할 수 있습니다.

        c. 그러면 ADFS 서버에서 감사를 사용 하도록 설정 해야 합니다.

3.  의심 스러운 IP를 차단 합니다.  DOS 공격을 차단할 수 있습니다.

    a. 2016의 경우 [*엑스트라넷 금지 된 ip 주소*](../../ad-fs/operations/configure-ad-fs-banned-ip.md) 기능을 사용 하 여 #3 (또는 수동 분석)에 의해 플래그가 지정 된 ip의 모든 요청을 차단 합니다.

    b. AD FS 2012 R2 이하로 설정 된 경우 Exchange Online에서 직접 또는 방화벽에서 IP 주소를 차단 합니다.

4. Azure AD Premium 있는 경우 [AZURE Ad 암호 보호](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-on-premises) 를 사용 하 여 azure ad에 추측할 암호가 표시 되지 않도록 방지 합니다.  

    a. 추측할 암호를 사용 하는 경우 1-3 시도 만으로 암호를 해독할 수 있습니다. 이 기능은 이러한 기능을 설정 하는 것을 방지 합니다. 

    b. 미리 보기 통계에서 새로운 암호의 거의 20-50%가 설정 되지 않도록 차단 됩니다. 이는 사용자의%가 쉽게 추측할 수 있는 암호에 취약 함을 의미 합니다.

## <a name="level-2-protect-your-extranet"></a>수준 2: 엑스트라넷 보호

5. 엑스트라넷에서 액세스 하는 모든 클라이언트에 대 한 최신 인증으로 이동 합니다. 메일 클라이언트는이에 대 한 중요 한 부분입니다. 

    a. 모바일 장치에는 Outlook Mobile을 사용 해야 합니다. 새 iOS 네이티브 메일 앱은 최신 인증도 지원 합니다. 

    b. Outlook 2013 (최신 CU 패치 포함) 또는 Outlook 2016을 사용 해야 합니다.

6. 모든 엑스트라넷 액세스에 대해 MFA를 사용 하도록 설정 합니다. 이를 통해 모든 엑스트라넷 액세스에 대 한 보호를 추가할 수 있습니다.

   a.  Azure AD premium을 사용 하는 경우 [AZURE Ad 조건부 액세스 정책을](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) 사용 하 여이를 제어 합니다.  이는 AD FS에서 규칙을 구현 하는 것 보다 좋습니다.  최신 클라이언트 앱은 더 자주 적용 되기 때문입니다.  이는 Azure AD에서 새로 고침 토큰을 사용 하 여 새 액세스 토큰 (일반적으로 1 시간 마다)을 요청할 때 발생 합니다.  

   b.  Azure AD premium이 없거나 인터넷 기반 액세스를 허용 하는 AD FS에 대 한 추가 앱이 있는 경우 MFA를 구현 하 고 (AD FS 2016의 Azure MFA와 함께) 모든 엑스트라넷 액세스에 대 한 [전역 mfa 정책을](../../ad-fs/operations/configure-authentication-policies.md#to-configure-multi-factor-authentication-globally) 수행할 수 있습니다.

## <a name="level-3-move-to-password-less-for-extranet-access"></a>수준 3: 엑스트라넷 액세스에 대 한 암호 보다 작은 값으로 이동

7. 창 10으로 이동 하 고 비즈니스용 [Hello](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)를 사용 합니다.

8. 다른 장치의 경우 2016 AD FS 경우 [AZURE MFA OTP](../../ad-fs/operations/configure-ad-fs-and-azure-mfa.md) 를 첫 번째 요소와 암호 (두 번째 단계)로 사용할 수 있습니다. 

9. 모바일 장치의 경우 MDM 관리 장치만 허용 하는 경우 [인증서](../../ad-fs/operations/configure-user-certificate-authentication.md) 를 사용 하 여 사용자를 로그인 할 수 있습니다. 

## <a name="urgent-handling"></a>긴급 처리

AD FS 환경이 활성 공격을 받고 있는 경우 다음 단계를 가장 이른 시간에 구현 해야 합니다.

 - ADFS에서 U/P 끝점을 사용 하지 않도록 설정 하 고 모든 사용자가 VPN에 액세스 하거나 네트워크 내부에 있어야 합니다. 이렇게 하려면 단계 **수준 2 #1a** 완료 해야 합니다. 그렇지 않으면 모든 내부 Outlook 요청은 EXO 프록시 인증을 통해 클라우드를 통해 계속 라우팅됩니다.
 - EXO를 통해서만 공격을 받는 경우 인증 정책을 사용 하 여 Exchange 프로토콜 (POP, IMAP, SMTP, EWS 등)에 대 한 기본 인증을 사용 하지 않도록 설정할 수 있습니다. 이러한 프로토콜과 인증 방법은 대부분의 공격에서 사용 됩니다. 또한 EXO 및 사서함별 프로토콜 사용의 클라이언트 액세스 규칙은 인증 후 평가 되며 공격의 완화에 도움이 되지 않습니다. 
 - 수준 3 #1-3을 사용 하 여 엑스트라넷 액세스를 선택적으로 제공 합니다.

## <a name="next-steps"></a>다음 단계

- [AD FS server 2016로 업그레이드](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) 
- [AD FS 2016의 엑스트라넷 스마트 잠금](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [조건부 액세스 정책 구성](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Azure AD 암호 보호](https://docs.microsoft.com/azure/active-directory/authentication/howto-password-ban-bad-on-premises)
