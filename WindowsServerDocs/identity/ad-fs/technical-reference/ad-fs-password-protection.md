---
title: AD FS 암호 공격 보호
description: 이 문서에서는 AD FS 사용자 암호 대입 공격 으로부터 보호 하는 방법 설명
author: billmath
manager: mtillman
ms.reviewer: andandyMSFT
ms.date: 11/15/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5666943138070cfa8cfe62f1ba932c2793daa003
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501597"
---
# <a name="ad-fs-password-attack-protection"></a>AD FS 암호 공격 보호

## <a name="what-is-a-password-attack"></a>암호 공격을 란?

페더레이션된 single sign-on에 대 한 요구 사항은 인터넷을 통해 인증 하는 끝점의 가용성입니다. 인터넷 인증 끝점의 가용성을 통해 사용자가 회사 네트워크에 있지 않은 경우에 응용 프로그램에 액세스할 수 있습니다. 

그러나 따라서 믿지 못할 자 일부 인터넷에서 사용할 수 있는 페더레이션된 끝점을 활용 하 고 암호를 판단 하기 위해 또는 서비스 거부 공격을 만들려면 이러한 끝점을 사용할 수는 있습니다. 더욱 더 보편화 되는 이러한 한 가지 공격 이라고는 **암호 공격**합니다. 

두 가지 유형이 일반적인 암호 공격입니다. 암호 스프레이 공격 및 무차별 암호 대입 공격 암호 강제합니다. 

### <a name="password-spray-attack"></a>암호 스프레이 공격
암호 스프레이 공격에서 믿지 못할 자 이러한 여러 다양 한 계정 및 서비스를 찾을 수 있는 암호로 보호 된 자산에 대 한 액세스를 통해 가장 일반적인 암호를 시도 합니다. 일반적으로 이러한 범위 여러 서로 다른 조직 및 id 공급자입니다. 예를 들어 공격자가 여러 조직에서 사용자의 모든 열거 한 다음 시도 "P@$$w0rd" 및 "Password1" 모든 해당 계정에 대해 일반적으로 사용 가능한 도구 키트를 사용 합니다. 개념에 부여 하려면 공격와 같습니다.


|  대상 사용자   | 대상 암호 |
|----------------|-----------------|
| User1@org1.com |    Password1    |
| User2@org1.com |    Password1    |
| User1@org2.com |    Password1    |
| User2@org2.com |    Password1    |
|       …        |        …        |
| User1@org1.com |    P@$$w0rd     |
| User2@org1.com |    P@$$w0rd     |
| User1@org2.com |    P@$$w0rd     |
| User2@org2.com |    P@$$w0rd     |

개별 사용자 또는 회사의 유리한 지점에서 공격 처럼 보입니다 실패 한 로그인을 격리 하기 때문에 대부분의 검색 기술을 통과 하는이 공격 패턴입니다.

숫자 게임은 공격자가: 몇 가지는 암호를 매우 일반적인 있는지 알고 있습니다.  공격자는 공격을 천 모든 계정에 대 한 몇 가지 성공 받습니다 및 적용 되는 데 충분 합니다. 전자 메일에서 데이터 가져오기, 연락처 정보를 수집 및 피싱 링크를 보낼 또는 방금 암호 스프레이 대상 그룹을 확장 하 고 계정을 사용 합니다. 공격자는 이러한 초기 대상에 훨씬 신경-활용할 수 있는 몇 가지 성공 있는지만 합니다.

하지만 AD FS를 구성 하 고 올바르게 네트워크는 몇 가지 단계를 수행 하 여 AD FS 끝점을 이러한 유형의 공격 으로부터 보호 수 있습니다. 이 문서에서는 이러한 공격 으로부터 보호 하도록 제대로 구성 해야 하는 3 개의 영역을 다룹니다.

### <a name="brute-force-password-attack"></a>무작위 암호 공격 
이 형태의 공격에서 공격자 계정의 대상된 집합에 대 한 암호 시도 횟수를 시도 합니다. 대부분의 경우에서 이러한 계정은 높은 수준의 조직 내에서 액세스할 수 있는 사용자에 대 한 대상이 됩니다. 중요 한 인프라를 관리 하는 조직이 나 관리자 내에서 임원 될 수 있습니다.  

이러한 유형의 공격 DOS 패턴에도 발생할 수 있습니다. 이 ADFS 큰 # 서버의 부족 하 여 #로 인해 요청을 처리할 수 없는 서비스 수준 수 없거나 계정 사용자가 잠긴 사용자 수준에서 일 수 있습니다.  

## <a name="securing-ad-fs-against-password-attacks"></a>AD FS 암호 대입 공격 으로부터 보호 

하지만 AD FS를 구성 하 고 올바르게 네트워크는 몇 가지 단계를 수행 하 여 AD FS 끝점을 이러한 유형의 공격 으로부터 보호 수 있습니다. 이 문서에서는 이러한 공격 으로부터 보호 하도록 제대로 구성 해야 하는 3 개의 영역을 다룹니다. 


- 수준 1, 기준: 이들은 믿지 못할 자 무차별 공격 페더레이션 사용자 수 없다는 것을 확인 하려면 AD FS 서버에서 구성 해야 하는 기본 설정입니다. 
- 엑스트라넷 보호 되는 수준 2: 이러한 설정은 엑스트라넷 액세스 보안 프로토콜, 인증 정책 및 적절 한 응용 프로그램을 사용 하도록 구성 되었는지 확인 하도록 구성 되어야 합니다. 
- 엑스트라넷 액세스에 대 한 수준 3 암호 없이 이동: 이러한 고급 더 안전한 자격 증명 보다는 공격 가능성이 있는 암호를 사용 하 여 연결된 된 리소스에 대 한 액세스를 사용 하도록 설정 및 지침입니다. 

## <a name="level-1-baseline"></a>수준 1: 기준

1. ADFS 2016을 구현 하는 경우 [엑스트라넷 잠금](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md) 엑스트라넷 잠금 익숙한 위치를 추적 하 고 유효한 사용자는 이전에 로그인 했습니다. 해당 위치에서 하는 경우를 통해 야 합니다. 엑스트라넷 잠금을 사용 하 여 확실히 믿지 못할 자 (brute force) 할 수는 사용자를 공격 하 고 동시에는 합법적인 사용자 생산성을 높일 수 있습니다.
    - AD FS 2016에 있지 않다면 좋습니다 [업그레이드](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) ad FS 2016 합니다. AD FS 2012 r 2에서에서 간단한 업그레이드 경로 것입니다. AD FS 2012 r 2를 사용 하는 경우 구현 [엑스트라넷 잠금](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md)합니다. 하나이 방식의 단점은 (brute force) 패턴의 경우 엑스트라넷 액세스에 유효한 사용자는 차단 될 수 있습니다. 서버 2016에서 AD FS에는 이러한 단점이 없습니다.

2. 모니터링 및 블록 의심 스러운 IP 주소 
    - Azure AD Premium에 있는 경우 ADFS를 사용 하 여 Connect Health를 구현 합니다 [위험한 IP 보고서](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-adfs#risky-ip-report-public-preview) 제공 하는 알림입니다.

        a. 라이선스 모든 사용자에 대 한 아니며 고객이 쉽게 수 있는 25 라이선스/ADFS/WAP 서버가 필요 합니다.

        b. IP의 큰 횟수 실패 한 로그인을 생성 하는 이제 조사할 수 있습니다.

        c. ADFS 서버에서 감사를 사용 하도록 해야 합니다.

3.  의심 스러운 IP를 차단 합니다.  이 잠재적 DOS 공격을 차단합니다.

    a. 2016 년에 있는 경우 사용 합니다 [ *엑스트라넷 금지 된 IP 주소* ](../../ad-fs/operations/configure-ad-fs-banned-ip.md) #3 (또는 수동 분석) 플래그가 지정 된 ip의 모든 요청을 차단 하는 기능.

    b. AD FS 2012 r 2에서 낮은 경우 Exchange Online에서 직접 및 필요에 따라 방화벽에서 IP 주소를 차단 합니다.

4. 사용 하 여 Azure AD Premium에 있으면 [Azure AD 암호 보호](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-on-premises) Azure ad에서 추측할 수 있는 암호를 방지 하기 위해  

    a. 추측할 수 있는 암호를 설정한 경우 있습니다 수 해독 방금 1-3 시도 사용 하 여 note 합니다. 이 기능은 가져오기 설정에서 방지 합니다. 

    b. 거의 미리 보기 상태에서 새 암호의 20 ~ 50% 설정에서 차단 가져옵니다. 즉, 해당 %의 사용자는 쉽게 추측 된 암호가에 취약 합니다.

## <a name="level-2-protect-your-extranet"></a>수준 2: 엑스트라넷 보호

5. 엑스트라넷에서 액세스 하는 클라이언트에 대 한 최신 인증으로 이동 합니다. 메일 클라이언트는이 중요 한 부분입니다. 

    a. 모바일 장치에 대 한 Outlook Mobile을 사용 해야 합니다. 새 iOS 네이티브 메일 앱에는 최신 인증도 지원합니다. 

    b. Outlook 2013 (최신 CU 패치) 또는 Outlook 2016을 사용 해야 합니다.

6. 모든 엑스트라넷 액세스에 대 한 MFA를 사용 합니다. 이렇게 하면 모든 엑스트라넷 액세스에 대 한 보호를 추가 합니다.

   a.  사용 하 여 Azure AD premium에 있으면 [Azure AD 조건부 액세스 정책](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) 이것을 제어 합니다.  AD FS에서 규칙을 구현 하는 보다 좋습니다.  즉, 최신 클라이언트 앱을 더 자주 강제로 적용 됩니다.  이때 Azure AD에서 새로 고침 토큰을 사용 하 여 새 액세스 토큰 (일반적으로 매시간)을 요청 하는 경우.  

   b.  Azure AD premium이 없는 경우 인터넷을 허용 하는 AD FS에서 추가 앱 액세스를 따라 구현 일 수 있습니다 Azure MFA도 AD FS 2016에서 MFA를 수행을 [전역 MFA 정책](../../ad-fs/operations/configure-authentication-policies.md#to-configure-multi-factor-authentication-globally) 모든 엑스트라넷 액세스에 대 한 합니다.

## <a name="level-3-move-to-password-less-for-extranet-access"></a>수준 3: 암호는 엑스트라넷 액세스에 대 한 작은 이동

7. Window 10으로 이동 하 고 사용 하 여 [Hello For Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification)합니다.

8. 다른 장치에 대 한 AD FS 2016에서 작업 하는 경우 사용할 수 있습니다 [Azure MFA OTP](../../ad-fs/operations/configure-ad-fs-and-azure-mfa.md) 첫 번째 요소 및 두 번째 단계로 암호입니다. 

9. 모바일 장치를 MDM 관리 장치에만 허용 하는 경우 사용할 수 있습니다 [인증서](../../ad-fs/operations/configure-user-certificate-authentication.md) 사용자를 로그인 합니다. 

## <a name="urgent-handling"></a>긴급 처리

AD FS 환경을 활성 공격을 받고 있는 경우 다음 단계를 가능한 한 빨리 구현 해야 합니다.

 - ADFS에 U/P 끝점을 사용 하지 않도록 설정 하 고 모든 사용자가 이용 하거나 네트워크 내에서 VPN에 필요 합니다. 이렇게 하려면 단계가 있을 **수준 2 #1a** 완료 합니다. 그렇지 않으면 모든 내부 Outlook 요청이 계속 라우팅됩니다 EXO 프록시 인증을 통해 클라우드를 통해
 - Exchange 프로토콜 (POP, IMAP, SMTP, EWS, 등)에 대 한 기본 인증을 비활성화할 수 있습니다 공격 EXO 통해만 경우, 인증 정책을 사용 하 여, 이러한 프로토콜 및 인증 방법에서 사용 중인 대부분의 이러한 공격입니다. 또한 EXO 및 사서함별 프로토콜 사용의 클라이언트 액세스 규칙이 평가 사후 인증 되며 공격을 완화 하는 데 도움이 되지 않습니다. 
 - 선택적으로 수준 3 #1-3를 사용 하 여 엑스트라넷 액세스를 제공 합니다.

## <a name="next-steps"></a>다음 단계

- [AD FS server 2016으로 업그레이드](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) 
- [AD FS 2016에서에서 엑스트라넷 잠금](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [조건부 액세스 정책 구성](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Azure AD 암호 보호](https://docs.microsoft.com/azure/active-directory/authentication/howto-password-ban-bad-on-premises)
