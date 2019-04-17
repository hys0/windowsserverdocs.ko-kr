---
title: "계정 보호를 구성 하는 방법"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: f2effdb7a82a25c810bc041475e760145de492d8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="how-to-configure-protected-accounts"></a>계정 보호를 구성 하는 방법

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

단계-the-해시 (PtH) 공격 공격자 기본 NTLM 해시 사용자의 암호 (또는 다른 자격 증명 파생)를 사용 하 여 원격 서버 또는 서비스 인증할 수 있습니다. Microsoft has previously [published guidance](https://www.microsoft.com/download/details.aspx?id=36036) to mitigate pass-the-hash attacks.  Windows Server 2012 r 2에는 이러한 공격 더 완화 새로운 기능이 있습니다. For more information about other security features that help protect against credential theft, see [Credentials Protection and Management](https://technet.microsoft.com/library/dn408190.aspx). 이 항목에서는 다음과 같은 새로운 기능을 구성 하는 방법을 설명 합니다.  
  
-   [보호 된 사용자](how-to-configure-protected-accounts.md#BKMK_AddtoProtectedUsers)  
  
-   [인증 정책](how-to-configure-protected-accounts.md#BKMK_CreateAuthNPolicies)  
  
-   [인증 정책 사일로](how-to-configure-protected-accounts.md#BKMK_CreateAuthNPolicySilos)  
  
Windows 8.1 및 Windows Server 2012 r 2와 도난당 자격 증명을 방지 하기 위해 다음 항목에 적용 되는에 기본 제공 되는 추가 완화 가지가 있습니다.  
  
-   [원격 데스크톱에 대 한 제한 관리자 모드](http://blogs.technet.com/b/kfalde/archive/20../restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)  
  
-   [LSA 보호](https://technet.microsoft.com/library/dn408187)  
  
## <a name="BKMK_AddtoProtectedUsers"></a>보호 된 사용자  
보호 된 사용자는 새로운 기능이 나 기존 사용자를 추가할 수 있는 새로운 글로벌 보안 그룹입니다. 디바이스가 Windows 8.1 및 Windows Server 2012 r 2 호스트는 자격 증명 도용의 더 잘 보호할 수 있도록이 그룹의 회원 들과 특별 한 작동 합니다. 그룹의 회원 디바이스를 Windows 8.1 또는 Windows Server 2012 r 2 호스트 보호 사용자에 대 한 지원 되지 않는 자격 증명을 하지 캐시지 않습니다. Windows 8.1 이전 Windows 버전을 실행 하는 장치에 로그온 할 경우이 그룹 구성원 추가 보호 하지을 갖습니다.  
  
사용자는 로그인에 대 한 Windows 8.1 디바이스 그룹 구성원 보호 사용자 및 Windows Server 2012 r 2 호스트 수 *더 이상* 사용:  
  
-   자격 증명을 위임 (CredSSP)-기본 일반 자격 증명 캐시 되지 않은 경우에 있는 **위임 기본 자격 증명을 허용** 정책을 사용  
  
-   Windows 요약-자격 증명이 일반 캐시 더 활성화 되 면  
  
-   NTLM-NTOWF 캐시 되지 않으면  
  
-   Kerberos 장기 키-Kerberos 허용 티켓 (TGT)에 로그온 할 때 획득 하 고 자동으로 다시 얻을 수 없음  
  
-   로그인에 오프 라인-확인자 캐시 된 로그온 만들어지지 않습니다  
  
Windows Server 2012 R2 도메인 기능 수준을 경우, 더 이상 그룹의 회원 수 없습니다.  
  
-   NTLM 인증을 사용 하 여 인증  
  
-   Kerberos 미리 인증에서 데이터 표준 DES (암호화) 또는 r c 4 암호 그룹을 사용 하 여  
  
-   무제한 또는 제한 된 위임을 사용 하 여 위임  
  
-   초기 4 시간 수명 이상의 사용자 티켓 (Tgt) 갱신  
  
To add users to the group, you can use [UI tools](https://technet.microsoft.com/library/cc753515.aspx) such as Active Directory Administrative Center (ADAC) or Active Directory Users and Computers, or a command-line tool such as [Dsmod group](https://technet.microsoft.com/library/cc732423.aspx), or the Windows PowerShell[Add-ADGroupMember](https://technet.microsoft.com/library/ee617210.aspx) cmdlet. 계정 서비스, 컴퓨터에 대 한 *하지 않아야* 보호 사용자 그룹의 회원 수 있습니다. 해당 계정에 대 한 멤버십 암호 또는 인증서 항상 호스트에서 사용할 수 없기 때문 없이 로컬 보호를 제공 합니다.  
  
> [!WARNING]  
> 인증 제한을 없는 문제를 해결할 도메인 관리자 그룹 엔터프라이즈 관리자 하나 또는 여러 개의 등의 매우 권한이 있는 그룹의 회원은 사용자가 보호 그룹의 다른 구성원와 같은 제한 될 것을 의미 합니다. 이러한 그룹의 모든 구성원이 보호 사용자 그룹에 추가 되 면 경우 모든 잠기는 해당 계정에 대해 합니다. 영향을 테스트할 철저 하 게 될 때까지 모든 매우 권한이 있는 계정 보호 사용자 그룹에 추가 하지 해야 합니다.  
  
Users 보호 그룹의 회원 Kerberos로 고급 표준 AES (암호화)를 사용 하 여 인증 수 있어야 합니다. 이 방법을 Active Directory에 계정에 대 한 AES 키가 필요 합니다. 기본 제공 관리자 AES 키를 없는 Windows Server 2008 실행 하는 도메인 컨트롤러에서 변경 된 이상 한 암호가 하지 않으면 합니다. 또한 Windows Server의 이전 버전을 실행 하는 도메인 컨트롤러에서 변경 된 암호 있는 계정 잠겨 있습니다. 따라서 이러한 모범 사례에 따라 다음과 같습니다.  
  
-   하지 않는 한 하는 도메인의 테스트 수행 **모든 도메인 컨트롤러 실행 Windows Server 2008 이상**합니다.  
  
-   **비밀 번호 변경** 생성 된 모든 도메인 계정에 대 한 *하기 전에* 도메인 생성 되었습니다. 그렇지 않은 경우 이러한 계정의 인증할 수 없습니다.  
  
-   **비밀 번호 변경** 보호 사용자에 게 계정을 추가 하기 전에 각 사용자 그룹 또는 Windows Server 2008 실행 하는 도메인 컨트롤러에서 최근에 변경 된 이상 암호 되었는지 확인 합니다.  
  
### <a name="BKMK_Prereq"></a>계정 보호를 사용 하 여 요구 사항  
계정 보호 되는 다음과 같은 배포 요구 사항이 있습니다.  
  
-   사용자가 보호에 대 한 클라이언트 측 제한을 제공 하려면 Windows 8.1 또는 Windows Server 2012 r 2 호스트 실행 해야 합니다. 사용자만 로그인 켜 짐는 계정 보호 사용자 그룹 구성원을 가집니다. In this case, the Protected Users group can be created by [transferring the primary domain controller (PDC) emulator role](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) to a domain controller that runs  Windows Server 2012 R2 . 해당 그룹에 복제 되므로 다른 도메인 컨트롤러를 후 이전 버전의 Windows Server를 실행 하는 도메인 컨트롤러에서 PDC 에뮬레이터 역할을 호스트할 수 있습니다.  
  
-   를 제공 하기 위해 보호 된 사용자 NTLM 인증의 사용을 제한 하는 것을 하는 도메인 컨트롤러 측 제한 및 기타 제한 도메인 기능 수준 Windows Server 2012 r 2 있어야 합니다. 수준 기능에 대 한 자세한 내용은 참조 [이해 Active Directory 도메인 서비스 (AD DS) 기능 수준](../../identity/ad-ds/active-directory-functional-levels.md)합니다.  
  
### <a name="BKMK_TrubleshootingEvents"></a>이벤트 보호 사용자에 게 관련 문제 해결  
이 섹션 보호 사용자와 사용자가 보호할 수 있는 어떤 영향을 주나요 문제를 해결 중 티켓 부여 (TGT) 티켓이 만료 또는 위임 변경 관련 된 이벤트 해결을 위해 새 로그에 설명 합니다.  
  
#### <a name="new-logs-for-protected-users"></a>보호 사용자를 위한 새로운 로그  
두 가지 새로운 작업 관리자 로그 보호 사용자와 관련이 이벤트를 해결 하기 위해 사용할 수 있는:-클라이언트 로그 및 사용자 실패 보호-보호 사용자 도메인 컨트롤러 로그인 합니다. 이러한 새 로그 이벤트 뷰어에 위치 하 고 기본적으로 사용할 수 없습니다. 로그를 사용 하도록 설정 하려면 클릭 **응용 프로그램 및 서비스 로그**, 클릭 **Microsoft**, 클릭 **Windows**, 클릭 **인증**, 로그 이름을 클릭 고 클릭 **알림** (또는 로그를 마우스 오른쪽 단추로 클릭)를 클릭 하 고 **로그 사용**합니다.  
  
For more information about events in these logs, see [Authentication Policies and Authentication Policy Silos](https://technet.microsoft.com/library/dn486813.aspx).  
  
#### <a name="troubleshoot-tgt-expiration"></a>TGT 만료 문제 해결  
일반적으로 TGT 수명 및 다음 그룹 정책 편집기 관리 창에 표시 된 대로 도메인 정책에 따라 갱신 도메인 컨트롤러를 설정 합니다.  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
에 대 한 **사용자 보호**, 다음 설정은 하드 코드:  
  
-   최대 수명이 사용자 티켓: 분  
  
-   최대 수명이 사용자 티켓 갱신: 분  
  
#### <a name="troubleshoot-delegation-issues"></a>위임 문제 해결  
이전에 사용 Kerberos 위임 하는 기술이 실패 하는 경우 클라이언트 계정을 체크 경우 **계정은 중요 한 위임 수 없습니다** 설정 합니다. 그러나 계정이 경우 **보호 사용자**의 Active Directory 관리 센터 (ADAC) 구성 된이 설정의 없을 수도 있습니다. 설정 및 그룹 구성원 위임 문제를 해결할 때 결과적으로 확인 합니다.  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
### <a name="BKMK_AuditAuthNattempts"></a>감사 인증 시도  
회원 명시적으로 인증 시도 감사 하 고 **보호 사용자** 그룹 이벤트 감사 로그 보안 수집 하거나, 새로운 작업 관리자 로그에서의 데이터 수집을 계속할 수 있습니다. For more information about these events, see [Authentication Policies and Authentication Policy Silos](https://technet.microsoft.com/library/dn486813.aspx)  
  
### <a name="BKMK_ProvidePUdcProtections"></a>서비스와 컴퓨터에 대 한 DC 측 보호를 제공 합니다.  
서비스 및 컴퓨터에 대 한 계정을의 회원 수 없는 **사용자 보호**합니다. 이 섹션에 설명 있는 도메인 컨트롤러 기반 보호 해당이 계정에 제공 될 수 있습니다.  
  
-   Reject NTLM authentication: Only configurable via [NTLM block policies](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)  
  
-   Kerberos 미리 인증에서 데이터 표준 DES (암호화)를 거부: 컴퓨터 않는 모든 Kerberos과 함께 출시 된 Windows 버전을 r c 4도 지원 되므로 des 구성 된 계정에 대 한 Windows Server 2012 R2 도메인 컨트롤러 DES 허용 하지 않습니다.  
  
-   Kerberos 미리 인증에서 r c 4 거부: 하지 구성할 수 있습니다.  
  
    > [!NOTE]  
    > 수는 있지만 [지원 되는 암호화 형식의 구성을 변경](http://blogs.msdn.com/b/openspecification/archive/20../windows-configurations-for-kerberos-supported-encryption-type.aspx), 대상 환경에서 테스트를 진행 하지 않고 컴퓨터 계정에 대 한 이러한 설정을 변경 하는 것이 좋습니다 되지 않습니다.  
  
-   초기 4 시간 수명 사용자 티켓 (Tgt)를 제한: 사용 인증 정책입니다.  
  
-   거부 위임 위임 무제한 또는 제한 된: 계정을 제한 하려면를 열고 Active Directory 관리 센터 (ADAC)는 **계정을 중요 한 위임 수 없는** 확인란을 선택 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
## <a name="BKMK_CreateAuthNPolicies"></a>인증 정책  
인증 정책 AD ds 인증 정책 개체 포함 된 새 컨테이너 됩니다. 인증 정책을 TGT 수명 계정에 대 한 제한 하거나 다른 클레임 관련 조건 추가 같은 자격 증명 도용의에 노출 줄이는 데 도움이 되는 설정을 지정할 수 있습니다.  
  
Windows Server 2012에서 동적 액세스 제어 중앙 액세스 정책 쉽게 조직에서 파일 서버 구성 하는 방법을 제공 하 라고 한 Active Directory 숲 범위 개체 클래스를 도입 되었습니다. Windows Server 2012 r 2에 인증 정책 (개체 클래스를 AuthNPolicies) 라는 새로운 개체 클래스 인증 구성 클래스 Windows Server 2012 R2 도메인 계정에 적용 사용할 수 있습니다. Active Directory 계정 클래스는 다음과 같습니다.  
  
-   사용자  
  
-   컴퓨터  
  
-   관리 서비스 계정 및 그룹 관리 서비스 계정 (GMSA)  
  
### <a name="quick-kerberos-refresher"></a>Kerberos 소개  
Kerberos 인증 프로토콜 subprotocols 라고도 거래소의 세 종류 이루어져 있습니다.  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbRefresher.gif)  
  
-   인증 서비스 (AS) 교환 (KRB_AS_ *)  
  
-   허용 서비스 (TGS) Exchange (KRB_TGS_ *)  
  
-   (클라이언트/AP) 서버 Exchange (KRB_AP_ *)  
  
AS exchange 위치 클라이언트를 사용 하 여 계정의 암호 또는 개인 키를 요청을 허용 티켓 (TGT) 사전 인증 만들입니다. 사용자 로그인 화면에서 이러한 문제가 발생 하거나 서비스 티켓이 필요한 처음으로 합니다.  
  
TGS exchange 계정의 TGT 서비스 티켓 요청할 수 있는 인증 만드는 데 사용 되는 합니다. 이런 경우 인증 된 연결이 필요 합니다.  
  
AP exchange 응용 프로그램 프로토콜 내 데이터로 일반적으로 발생 하 고 인증 정책 영향을 미치지 않습니다.  
  
For more detailed information, see [How the Kerberos Version 5 Authentication Protocol Works](https://technet.microsoft.com/library/cc772815(v=WS.10.aspx.  
  
### <a name="overview"></a>개요  
계정에 대 한 구성할 수 제한이 적용 하는 방법을 제공 하 고 계정에 대 한 제한 서비스와 컴퓨터에 대 한 제공 하 여 사용자가 보호 보완 하는 인증 정책 합니다. AS exchange 또는 TGS 중 인증 정책이 적용 되어 exchange 합니다.  
  
초기 인증 또는 AS 교환 구성 제한할 수 있습니다.  
  
-   TGT 수명  
  
-   액세스를 제어 조건 사용자 sign-on AS exchange 오고 장치 충족 해야 하는 제한 하려면  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictAS.gif)  
  
구성 티켓 부여 서비스 (TGS) exchange 통해 티켓 요청 서비스를 제한할 수 있습니다.  
  
-   액세스 제어 조건을 충족 해야 합니다 (사용자, 서비스, 컴퓨터) 클라이언트가 또는 TGS exchange 오고 장치  
  
### <a name="BKMK_ReqForAuthnPolicies"></a>인증 정책을 사용 하 여 요구 사항  
  
|정책|요구 사항|  
|-----|--------|  
|사용자 지정 TGT 수명 제공| Windows Server 2012 R2 도메인 기능 수준 계정 도메인|  
|사용자 기호를 제한|-Windows Server 2012 R2 도메인 기능 수준 계정 도메인 동적 액세스 제어 지원<br />Windows 8, Windows 8.1, Windows Server 2012 또는 Windows Server 2012 r 2 장치 동적 액세스 제어 지원|  
|사용자 계정 및 보안 그룹에 따라 서비스 티켓 발급 제한| Windows Server 2012 R2 도메인 수준 리소스 기능 도메인|  
|사용자 클레임 또는 장치 계정, 보안 그룹 또는 클레임 기반 서비스 티켓 발급 제한| Windows Server 2012 R2 도메인 기능 수준 리소스 도메인 동적 액세스 제어 지원|  
  
### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>사용자 계정에 특정 디바이스와 호스트 제한  
관리자 권한이 있는 우선 순위가 높은 계정의 회원 있어야는 **보호 사용자** 그룹입니다. 기본적으로 계정을 설정 하지 않고는의 회원은 **보호 사용자** 그룹입니다. 그룹에 계정을 추가 하기 전에 도메인 컨트롤러 지원 구성 하 고 차단 문제가 없는지 확인 감사 정책을 만듭니다.  
  
#### <a name="configure-domain-controller-support"></a>도메인 컨트롤러 지원을 구성합니다  
Windows Server 2012 R2 도메인 기능 (DFL) 수준에서 사용자의 계정을 도메인 있어야 합니다. Ensure all the domain controllers are  Windows Server 2012 R2 , and then use Active Directory Domains and Trusts to [raise the DFL](https://technet.microsoft.com/library/cc753104.aspx) to  Windows Server 2012 R2 .  
  
**동적 액세스 제어에 대 한 지원을 구성 하려면**  
  
1.  기본 도메인 컨트롤러 정책 클릭 **사용** 수 있도록 **키 메일 센터 (KDC) 클라이언트 클레임, 지원 복합 인증 Kerberos armoring** 컴퓨터 구성에서 | 관리 템플릿 | 시스템 | KDC 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)  
  
2.  아래에서 **옵션**, 드롭다운 목록에서 상자에서 선택 **클레임을 항상 제공**합니다.  
  
    > [!NOTE]  
    > **지원 되는** 구성할 수도 있습니다 있지만 도메인이 Windows Server 2012 r 2 DFL, Dc 항상 필요 하기 때문에 제공 클레임 하면 사용자 클레임 기반 액세스 확인 클레임 비 인식 장치를 사용할 때 발생 하 고 섬에는 클레임 인식 서비스에 연결할 수 있습니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)  
  
    > [!WARNING]  
    > 구성 **무방비 인증 요청이 실패** 운영 체제를 지 원하는 명시적으로 구성 되지 않은 Windows 8으로 시작 또는 Windows 7 이전 운영 체제 등 Kerberos armoring 지원 하지 않는 모든 운영 체제에서 인증 오류가 발생 합니다.  
  
#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>인증 정책에 대 한 사용자 계정 감사 ADAC를 사용 하 여 만들기  
  
1.  관리 센터 Active Directory (ADAC)를 엽니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_OpenADAC.gif)  
  
    > [!NOTE]  
    > 선택한 **인증** 노드 Windows Server 2012 r 2 DFL에가 도메인에 표시 됩니다. 노드 표시 되지 않으면 후 다시 시도 Windows Server 2012 r 2 DFL 아래에 있는 도메인 도메인 관리자 계정을 사용 하 여 합니다.  
  
2.  클릭 **인증 정책**을 차례로 클릭 하 고 **새로** 정책을 새로 만들 수 있습니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)  
  
    인증 정책을 표시 이름이 있어야 하며 기본적으로 적용 됩니다.  
  
3.  감사 전용 정책 만들려면 클릭 **정책 제한 감사**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)  
  
    인증 정책은 Active Directory 계정 종류에 따라 적용 됩니다. 단일 정책을 각 유형에 대 한 설정을 구성 하 여 모든 세 계정 유형 적용할 수 있습니다. 계정 유형이 다음과 같습니다.  
  
    -   사용자  
  
    -   컴퓨터  
  
    -   관리 서비스 계정 및 그룹 관리 서비스 계정  
  
    키 메일 센터 (KDC)를 사용할 수 있는 새 사용자로 스키마를 연장 새 계정 유형은 가까운 파생된 계정 유형을에서 분류 됩니다.  
  
4.  구성 하려면 사용자 계정에 대해 TGT 수명 선택 하십시오는 **사용자 계정에 대 한 허용 티켓 수명 지정** 확인란을 선택 하 고 시간 분 내에 입력 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTLifetime.gif)  
  
    예를 들어 시간이 10 최대 TGT 수명 원하는 입력 **600** 같이 합니다. 없는 TGT 수명 구성 된 경우, 다음 계정이 경우는 **보호 사용자** TGT 수명 그룹화 하 고 갱신 4 시간입니다. 그렇지 않은 경우 TGT 수명과 갱신은 정책에 따라 도메인 기본 설정으로 도메인에 대 한 다음 그룹 정책 편집기 관리 창에 표시 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
5.  장치를 선택 하 여 사용자 계정을 제한 하려면 클릭 **편집** 를 정의할 장치에 필요한 상황입니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)  
  
6.  에 **액세스 제어 조건 편집** 창을 클릭 **조건을 추가**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCondition.png)  
  
##### <a name="add-computer-account-or-group-conditions"></a>컴퓨터 계정을 또는 그룹 조건을 추가합니다  
  
1.  구성 하려면 컴퓨터 계정을 또는 그룹을 드롭다운 목록에서 드롭다운 목록에서 상자를 선택한 후 **각각의 회원** 변경 하 고 **의 모든 구성원이**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompMember.png)  
  
    > [!NOTE]  
    > 이 액세스 제어 디바이스 또는 사용자의 로그인 호스트 조건을 정의 됩니다. 액세스 제어 용어 디바이스 또는 호스트 컴퓨터 계정을 되는 이유는 사용자 **사용자** 옵션만 합니다.  
  
2.  클릭 **항목 추가**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddItems.png)  
  
3.  개체 유형을 변경 하려면 **개체 유형**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjects.gif)  
  
4.  컴퓨터 개체 Active Directory를 선택 하려면 클릭 **컴퓨터**을 차례로 클릭 하 고 **확인**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)  
  
5.  사용자를 제한 하 고 다음을 클릭 하려면 컴퓨터의 이름을 입력 **이름 확인**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)  
  
6.  확인을 클릭 하 고 컴퓨터 계정에 대 한 기타 조건 만듭니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddConditions.png)  
  
7.  완료 되 면 클릭 한 다음 **확인** 컴퓨터 계정에 대 한 조건에 정의 된 해당 표시 됩니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompDone.png)  
  
##### <a name="add-computer-claim-conditions"></a>컴퓨터 클레임 조건을 추가합니다  
  
1.  구성 하려면 컴퓨터 클레임, 드롭다운 청구 선택 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaim.gif)  
  
    클레임은 숲에서 이미 제공 되는 경우 사용할 수만 있습니다.  
  
2.  사용자 계정에 로그인을 하면로 제한 해야, OU의 이름을 입력 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimOUName.gif)  
  
3.  완료 되 면 다음 확인을 클릭 하 고 상자에 정의 된 조건과 표시 됩니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimComplete.gif)  
  
##### <a name="troubleshoot-missing-computer-claims"></a>컴퓨터 클레임 누락 문제 해결  
준비 되 클레임에 사용할 수 없는 경우 것 수만 구성 되어 **컴퓨터** 클래스 합니다.  
  
가정 이미 구성 된 컴퓨터의 하지만 대해서만 조직 단위 기반 인증을 제한 하려면를 말한 **컴퓨터** 클래스 합니다.  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictComputers.gif)  
  
디바이스에 제한 사용자 로그인에 사용할 수는 클레임 선택는 **사용자** 확인란을 선택 합니다.  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)  
  
#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>ADAC로 인증 정책 사용 하 여 사용자 계정을 제공합니다  
  
1.  **사용자** 계정, 클릭 **정책**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicy.gif)  
  
2.  선택는 **인증 정책을이 계정에 할당** 확인란을 선택 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)  
  
3.  사용자에 게 적용할 인증 정책을 선택 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicySelect.png)  
  
#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>디바이스 및 호스트 동적 액세스 제어 지원을 구성합니다  
제어 DAC (동적 액세스) 구성 하지 않고 TGT 수명 구성할 수 있습니다. DAC는 AllowedToAuthenticateFrom 및 AllowedToAuthenticateTo 확인에 필요 합니다.  
  
그룹 정책 또는 로컬 그룹 정책 편집기를 사용 하 여 활성화 **Kerberos 클라이언트 클레임, 지원 복합 인증 Kerberos armoring** 컴퓨터 구성에서 | 관리 템플릿 | 시스템 | Kerberos:  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)  
  
### <a name="BKMK_TroubleshootAuthnPolicies"></a>인증 정책 문제 해결  
  
#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>인증 정책이 할당 직접 계정 확인  
인증 정책을의 계정 섹션 직접 정책이 적용 되는 계정을 표시 됩니다.  
  
![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AccountsAssigned.gif)  
  
#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>인증 정책 실패-관리 로그 도메인 컨트롤러를 사용 하 여  
새 **인증 정책 실패 도메인 컨트롤러** 아래 관리 로그 **응용 프로그램 및 서비스 로그** > **Microsoft** > **Windows** > **인증** 인증 정책으로 인해 오류 검색 쉽게 만들었습니다. 로그는 기본적으로 사용할 수 없습니다. 을 사용 하려면 로그 이름을 마우스 오른쪽 단추로 클릭 한 **로그 사용**합니다. 새 이벤트는 기존 Kerberos TGT 및 서비스 티켓 이벤트 감사 콘텐츠 매우 유사 합니다. For more information about these events, see [Authentication Policies and Authentication Policy Silos](https://technet.microsoft.com/library/dn486813.aspx).  
  
### <a name="BKMK_ManageAuthnPoliciesUsingPSH"></a>Windows PowerShell를 사용 하 여 인증 정책을 관리합니다  
이 명령은 이라는 인증 정책을 **TestAuthenticationPolicy**합니다. **UserAllowedToAuthenticateFrom** 매개 변수 someFile.txt 다음 파일은 SDDL 문자열 하 여 사용자가 인증할 수 있는 디바이스를 지정 합니다.  
  
```  
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl  
```  
  
이 명령을 가져옵니다 필터 일치 하는 모든 인증 정책 하는 **필터** 매개 변수를 지정 합니다.  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com  
  
```  
  
설명 수정 및 **UserTGTLifetimeMins** 지정 된 인증 정책의 속성 합니다.  
  
```  
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45  
```  
  
이 명령을 인증 정책을 제거 하는 **신원을** 매개 변수를 지정 합니다.  
  
```  
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1  
```  
  
이 명령을 사용 하 여는 **Get ADAuthenticationPolicy** 와 cmdlet는 **필터** 매개 변수를 적용 되는 모든 인증 정책입니다. 결과 집합에 파이프라인을 통해 전달 되 고 **제거 ADAuthenticationPolicy** cmdlet 합니다.  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy  
```  
  
## <a name="BKMK_CreateAuthNPolicySilos"></a>인증 정책 사일로  
인증 정책 사일로 AD DS 사용자, 컴퓨터 및 계정 서비스에 대 한 새 컨테이너 (개체 클래스를 AuthNPolicySilos)입니다. 우선 순위가 높은 계정을 보호 데 도움이 됩니다. 해당 계정 숲에서 아무 것도 액세스할 수 공격자가 사용 될 수 있으므로 엔터프라이즈 관리, 도메인 관리자 및 스키마 관리자 그룹의 회원 보호 하기 위해 필요한 모든 조직이 하는 동안 다른 계정 보호를 할 수도 있습니다.  
  
일부 조직에 고유 계정을 만들어 및 지역 및 원격 대화형 로그온 및 관리자 권한이 제한 하려면 그룹 정책 설정을 적용 하 여 작업을 분리 합니다. 인증 정책 사일로이 작업을 만들어 사용자, 컴퓨터와 관리 서비스 계정 간의 관계 정의 하는 방법을 보충 합니다. 계정을 하나 기지만 속할 수 있습니다. 제어 하려면 각 유형의 계정에 대 한 정책을 인증 구성할 수 있습니다.  
  
1.  비 갱신 TGT 수명  
  
2.  제어 조건 TGT 환불에 대 한 액세스 (참고: 필요 하기 때문에 Kerberos armoring 시스템에 적용 수 없는)  
  
3.  서비스 티켓 환불에 대 한 액세스를 제어 조건  
  
또한 인증 정책 기지에서 계정 액세스를 제어할 수 파일 서버 등 클레임 인식 리소스 사용할 수 있는 기지 클레임은 합니다.  
  
에 따라 서비스 티켓 발급를 제어 하는 새로운 보안 설명자 구성할 수 있습니다.  
  
-   사용자, 사용자의 보안 그룹 또는 사용자의 클레임  
  
-   장치, 디바이스의 보안 그룹 및/또는 디바이스의 클레임  
  
이 정보는 리소스 Dc에 동적 액세스 제어가 필요 합니다.  
  
-   사용자 클레임:  
  
    -   Windows 8 및 이후 클라이언트 동적 액세스 제어 지원  
  
    -   도메인 계정 동적 액세스 제어 및 청구 지원  
  
-   디바이스 및/또는 장치 보안 그룹 다음과 같습니다.  
  
    -   Windows 8 및 이후 클라이언트 동적 액세스 제어 지원  
  
    -   복합 인증에 대해 구성 리소스  
  
-   장치 클레임:  
  
    -   Windows 8 및 이후 클라이언트 동적 액세스 제어 지원  
  
    -   장치 도메인 동적 액세스 제어 및 청구 지원  
  
    -   복합 인증에 대해 구성 리소스  
  
인증 정책을 개별 계정에는 인증 정책 기지 대신의 모든 구성원이에 적용할 수 또는 별도 인증 정책 다른 유형의 계정 기지 내에 적용할 수 있습니다. 예를 들어, 매우 권한이 있는 사용자 계정에 하나의 인증 정책이 적용 될 수 및 정책이 다른가요 서비스 계정에 적용 될 수 있습니다. 하나 이상의 인증 정책은 인증 정책 기지를 만들기 전에 만들어야 합니다.  
  
> [!NOTE]  
> 인증 정책을 인증 정책 기지의 회원에 적용할 수 또는 특정 계정 범위를 제한 하려면 사일로 독립적으로 적용 될 수 있습니다. 예를 들어,를 보호 하기 위해 단일 계정이 나 소수의 계정 정책 설정할 수 있습니다 해당 계정에 기지에 계정을 추가 하지 않고 합니다.  
  
인증 정책 기지 Windows PowerShell 또는 Active Directory 관리 센터를 사용 하 여 만들 수 있습니다. 기본적으로 인증 정책 기지만 감사 기지 정책으로 지정 하 고 **WhatIf** Windows PowerShell cmdlet에 매개 합니다. 이 경우 정책 기지 제한이 적용 되지 않습니다 있지만 감사 오류가 발생 제한 사항이 적용 되는 경우 여부를 나타내는 생성 됩니다.  
  
#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>인증 정책 기지 Active Directory 관리 센터를 사용 하 여 만들기  
  
1.  열기 **Active Directory 관리 센터**, 클릭 **인증**를 마우스 오른쪽 단추로 클릭 **인증 정책 사일로**, 클릭 **새로**를 차례로 클릭 하 고 **인증 정책 기지**합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)  
  
2.  **표시 이름**, 기지 이름을 입력 합니다. **허용 계정**, 클릭 **추가**를 입력 하는 계정 이름을 클릭 한 다음 **확인**합니다. 사용자가, 컴퓨터 또는 서비스 계정 지정할 수 있습니다. 모든 사용자 또는 사용자를 유형과 정책이 나 방침의 이름에 대 한 별도 정책에 대 한 단일 정책을 사용 여부를 지정 합니다.  
  
    ![계정 보호](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)  
  
### <a name="BKMK_ManageAuthnSilosUsingPSH"></a>Windows PowerShell를 사용 하 여 인증 정책 사일로 관리  
이 명령을 인증 정책 기지 개체 만들고 적용 됩니다.  
  
```  
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce  
```  
  
이 명령을 정책 사일로 필터도 지정 된와 일치 하는 모든 인증을 가져옵니다는 **필터** 매개 합니다. 출력 전달 됩니다는 **표 서식** cmdlet 정책과 값을의 이름을 표시 하려면 **적용** 각 정책에 합니다.  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize  
  
Name  Enforce  
--  ----  
silo     True  
silos   False  
  
```  
  
이 명령을 사용 하 여는 **Get ADAuthenticationPolicySilo** 와 cmdlet는 **필터** 매개 결과를 얻으려면 모든 적용 되는 인증 정책 사일로 및 파이프 필터의는 **제거 ADAuthenticationPolicySilo** cmdlet 합니다.  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo  
```  
  
이 명령을 라는 인증 정책 기지에 대 한 액세스 권한을 부여 *기지* 사용자 계정 이름을 *User01*합니다.  
  
```  
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01  
```  
  
이 명령을 라는 인증 정책 기지에 대 한 액세스를 해지 *기지* 사용자 계정 이름을 *User01*합니다. 때문에 **확인** 매개 **$False**, 확인 메시지가 나타나지 않습니다.  
  
```  
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False  
```  
  
이 이때 먼저 사용 하 여는 **Get ADComputer** 필터 일치 하는 모든 컴퓨터 계정을 cmdlet 하는 **필터** 매개 변수를 지정 합니다. 이 명령 출력으로 전달 됩니다 **설정 ADAccountAuthenticatinPolicySilo** 인증 정책 기지 할당 하 라는 *기지* 및 이라는 인증 정책을 *AuthenticationPolicy02* 에 있습니다.  
  
```  
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02  
```  
  

