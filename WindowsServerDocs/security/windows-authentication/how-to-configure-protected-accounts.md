---
title: 보호된 계정을 구성하는 방법
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
ms.openlocfilehash: 28296b588c87bddb0364b9c3e10ad443870dc52f
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266830"
---
# <a name="how-to-configure-protected-accounts"></a>보호된 계정을 구성하는 방법

>적용 대상: Windows Server (반기 채널), Windows Server 2016

PtH(Pass-the-hash) 공격을 통해 공격자는 사용자 암호(또는 다른 자격 증명 파생물)의 기본 NTLM 해시를 사용하여 원격 서버 또는 서비스에서 인증을 받을 수 있습니다. Microsoft는 이전에 PtH(Pass-the-hash) 공격을 완화할 수 있는 [지침을 게시](https://www.microsoft.com/download/details.aspx?id=36036) 했습니다.  Windows Server 2012 r 2에는 이러한 공격을 추가로 위험을 완화 하려면 새로운 기능이 있습니다. 자격 증명 도난을 방지하는 데 도움이 되는 다른 보안 기능에 대한 자세한 내용은 [자격 증명 보호 및 관리](https://technet.microsoft.com/library/dn408190.aspx)를 참조하세요. 이 항목에서는 다음과 같은 새로운 기능을 구성하는 방법에 대해 설명합니다.  
  
-   [보호 된 사용자](#protected-users)  
  
-   [인증 정책](#authentication-policies)  
  
-   [인증 정책 사일로](#authentication-policy-silos)  
  
Windows 8.1 및 Windows Server 2012 R2에는 자격 증명 도난을 방지하는 데 도움이 되는 추가 완화 기능이 기본 제공되며, 이러한 기능은 다음 항목에서 다룹니다.  
  
-   [원격 데스크톱에 대 한 제한 된 관리자 모드](http://blogs.technet.com/b/kfalde/archive/20../restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)  
  
-   [LSA 보호](https://technet.microsoft.com/library/dn408187)  
  
## <a name="protected-users"></a>보호된 사용자  
보호된 사용자는 새 사용자 또는 기존 사용자를 추가할 수 있는 새로운 글로벌 보안 그룹입니다. Windows 8.1 장치 및 Windows Server 2012 R2 호스트는 자격 증명 도난 방지 보호를 제공 하는이 그룹의 멤버와 특수 한 동작이 있습니다. 그룹의 멤버에 대 한 Windows 8.1 장치 또는 Windows Server 2012 R2 호스트에 보호 된 사용자에 대 한 지원 되지 않는 자격 증명을 캐시 있을 하지 않습니다. 이 그룹의 구성원 Windows 8.1 이전 버전의 Windows 실행 하는 장치에 로그온 한 경우 추가 보호 없이 보유 합니다.  
  
사용자는 로그온 Windows 8.1 장치에 그룹 보호 된 사용자의 구성원 및 Windows Server 2012 R2 호스트 수 *더 이상* 사용:  
  
-   기본 자격 증명 위임(CredSSP) - 일반 텍스트 자격 증명이 캐시되지 않으며, 이는 **기본 자격 증명 위임 허용** 정책을 사용하는 경우에도 마찬가지입니다.  
  
-   Windows 다이제스트 - 일반 텍스트 자격 증명이 캐시되지 않으며, 이는 일반 텍스트 자격 증명을 사용하도록 설정한 경우에도 마찬가지입니다.  
  
-   NTLM - NTOWF가 캐시되지 않습니다.  
  
-   Kerberos 장기 키 - Kerberos TGT(Ticket-Granting Ticket)를 로그온 시 얻을 수 있으며, 자동으로 다시 얻을 수 없습니다.  
  
-   오프라인 로그온 - 캐시된 로그온 검증 도구가 생성되지 않습니다.  
  
도메인 기능 수준이 Windows Server 2012 r 2 인 경우 그룹의 구성원은 더 이상 수: 없습니다  
  
-   NTLM 인증을 사용한 인증  
  
-   Kerberos 사전 인증에 DES(데이터 암호화 표준) 또는 RC4 암호 그룹 사용  
  
-   제한 없는 위임 또는 제한된 위임을 사용한 위임  
  
-   초기 4시간의 수명이 지난 후 사용자 티켓(TGT) 갱신  
  
그룹에 사용자를 추가 하려면 사용할 수 있습니다 [UI 도구](https://technet.microsoft.com/library/cc753515.aspx) Active Directory 관리 센터 ADAC () 또는 Active Directory 사용자 및 컴퓨터와 같은 명령줄 도구 등 [Dsmod 그룹](https://technet.microsoft.com/library/cc732423.aspx), 나는 Windows PowerShell [Add-adgroupmember](https://technet.microsoft.com/library/ee617210.aspx) cmdlet. 서비스 및 컴퓨터 계정은 보호된 사용자 그룹의 구성원이 *될 수 없습니다*. 암호 또는 인증서를 호스트에서 항상 사용할 수 있으므로, 이러한 계정의 구성원 자격에는 로컬 보호 기능이 제공되지 않습니다.  
  
> [!WARNING]  
> 인증 제한은 피할 수 있는 방법이 없습니다. 즉, Enterprise Admins 그룹 또는 Domain Admins 그룹과 같은 매우 강력한 권한의 그룹 구성원에게도 보호된 사용자 그룹의 다른 구성원과 동일한 제한이 적용됩니다. 이러한 그룹의 모든 구성원이 보호된 사용자 그룹에 추가된 경우 해당 계정이 모두 잠길 수 있습니다. 따라서 잠재적 영향을 철저히 테스트할 때까지 매우 강력한 권한의 계정을 보호된 사용자 그룹에 추가해서는 안 됩니다.  
  
보호된 사용자 그룹의 구성원은 AES(고급 암호화 표준)와 함께 Kerberos를 사용하여 인증할 수 있어야 합니다. 이 방법에는 Active Directory의 계정에 대한 AES 키가 필요합니다. 기본 제공 관리자 없는 AES 키 암호가 변경 된 Windows Server 2008을 실행 하는 도메인 컨트롤러에 이상이 아닌 경우. 또한 이전 버전의 Windows Server를 실행하는 도메인 컨트롤러에서 암호가 변경된 계정은 모두 잠깁니다. 따라서 다음 모범 사례를 따라야 합니다.  
  
-   하지 않는 한 도메인에서 테스트 하지 않는 **모든 도메인 컨트롤러 Windows Server 2008 이상을 실행**합니다.  
  
-   도메인이 생성되기 **이전**에 만들어진 모든 도메인 계정의 *암호를 변경*하세요. 그러지 않으면 이러한 계정을 인증할 수 없습니다.  
  
-   **암호 변경** 보호 된 사용자 계정을 추가 하기 전에 각 사용자에 대 한 그룹 또는 Windows Server 2008을 실행 하는 도메인 컨트롤러에 최근에 변경 된 이상 암호 되었는지 확인 합니다.  
  
### <a name="requirements-for-using-protected-accounts"></a>보호된 계정 사용을 위한 요구 사항  
보호된 계정에는 다음과 같은 배포 요구 사항이 있습니다.  
  
-   호스트는 보호 된 사용자에 대 한 클라이언트 쪽 제한을 제공 하려면 Windows 8.1 또는 Windows Server 2012 r 2를 실행 해야 합니다. 사용자는 보호된 사용자 그룹의 구성원 계정으로만 로그온해야 합니다. 보호 된 사용자 그룹을 만들 수 있습니다이 경우 [주 도메인 컨트롤러 (PDC) 에뮬레이터 역할을 전송](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) Windows Server 2012 r 2를 실행 하는 도메인 컨트롤러에 있습니다. 해당 그룹 개체를 다른 도메인 컨트롤러에 복제한 후 이전 버전의 Windows Server를 실행하는 도메인 컨트롤러에서 PDC 에뮬레이터 역할을 호스트할 수 있습니다.  
  
-   NTLM 인증 사용을 제한 하는 것을 하는 보호 된 사용자에 대 한 도메인 컨트롤러 쪽 제한 및 기타 제약을 제공 하려면 도메인 기능 수준이 Windows Server 2012 r 2 이어야 합니다. 기능 수준에 대한 자세한 내용은 [AD DS(Active Directory 도메인 서비스) 기능 수준 이해](../../identity/ad-ds/active-directory-functional-levels.md)를 참조하세요.  
  
### <a name="troubleshoot-events-related-to-protected-users"></a>보호된 사용자와 관련된 이벤트 문제 해결  
이 섹션에서는 보호된 사용자와 관련된 이벤트 문제를 해결하는 데 도움이 되는 새로운 로그 및 보호된 사용자가 TGT(Ticket-Granting Ticket) 만료 또는 위임 문제를 해결하기 위한 변경 사항에 미치는 영향에 대해 알아봅니다.  
  
#### <a name="new-logs-for-protected-users"></a>보호된 사용자에 대한 새로운 로그  
보호된 사용자와 관련된 이벤트 문제를 해결하는 데 도움이 되는 두 가지 새로운 작업 관리 로그인 보호 된 사용자-클라이언트 로그와 보호 된 사용자 실패-도메인 컨트롤러 로그 합니다. 이러한 새 로그는 이벤트 뷰어에 있으며 기본적으로 사용되지 않습니다. 로그를 사용하려면 **응용 프로그램 및 서비스 로그**, **Microsoft**, **Windows**, **인증**을 차례로 클릭하고 로그 이름을 클릭한 다음 **작업** 을 클릭(또는 로그를 마우스 오른쪽 단추로 클릭)하고 **로그 사용**을 클릭합니다.  
  
이러한 로그의 이벤트에 대한 자세한 내용은 [인증 정책 및 인증 정책 사일로](https://technet.microsoft.com/library/dn486813.aspx)를 참조하세요.  
  
#### <a name="troubleshoot-tgt-expiration"></a>TGT 만료 문제 해결  
일반적으로 도메인 컨트롤러는 다음 그룹 정책 관리 편집기 창에 표시된 대로 도메인 정책을 기반으로 TGT 수명 및 갱신을 설정합니다.  
  
![도메인 컨트롤러는 TGT 수명 및 갱신이 도메인 정책을 기반으로 설정 하는 방법을 보여 주는 그룹 정책 관리 편집기 창의 스크린샷](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
**보호된 사용자**에 대해 다음 설정이 하드 코드됩니다.  
  
-   사용자 티켓 최대 수명: 240분  
  
-   사용자 티켓 갱신 최대 수명: 240분  
  
#### <a name="troubleshoot-delegation-issues"></a>위임 문제 해결  
이전에는 Kerberos 위임을 사용하는 기술이 실패한 경우 클라이언트 계정을 검사하여 **계정이 민감하여 위임할 수 없음** 이 설정되어 있는지 확인했습니다. 그러나 계정이 **보호된 사용자**의 구성원인 경우 ADAC(Active Directory 관리 센터)에 이 설정이 구성되어 있지 않을 수 있습니다. 따라서 위임 문제를 해결할 때 설정 및 그룹 구성원 자격을 확인해야 합니다.  
  
![확인 하는 위치를 보여주는 스크린샷 * * 계정이 민감하여 위임할 수 없음 * * UI 요소](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
### <a name="audit-authentication-attempts"></a>인증 시도 감사  
**보호된 사용자** 그룹의 구성원에 대한 인증 시도를 명시적으로 감사하기 위해 보안 로그 감사 이벤트를 계속 명시적으로 수집하거나 새로운 작업 관리 로그에서 데이터를 수집할 수 있습니다. 이러한 이벤트에 대한 자세한 내용은 [인증 정책 및 인증 정책 사일로](https://technet.microsoft.com/library/dn486813.aspx)를 참조하세요.  
  
### <a name="provide-dc-side-protections-for-services-and-computers"></a>서비스 및 컴퓨터에 대한 DC 쪽 보호 제공  
서비스 및 컴퓨터 계정은 **보호된 사용자**의 구성원일 수 없습니다. 이 섹션에서는 이러한 계정에 제공할 수 있는 도메인 컨트롤러 기반 보호에 대해 설명합니다.  
  
-   NTLM 인증 거부: 통해 구성할 수 있는 유일한 [NTLM 차단 정책](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)합니다.  
  
-   Kerberos 사전 인증에서 DES(데이터 암호화 표준) 거부:  Kerberos와 함께 릴리스된 Windows의 모든 버전에서는 RC4도 지원 때문에 des 구성 되지 않으면 Windows Server 2012 R2 도메인 컨트롤러 컴퓨터 계정에 대해 DES를 허용 하지 않습니다.  
  
-   Kerberos 사전 인증에서 RC4 거부: 구성할 수 없습니다.  
  
    > [!NOTE]  
    > [지원되는 암호화 형식의 구성을 변경](http://blogs.msdn.com/b/openspecification/archive/20../windows-configurations-for-kerberos-supported-encryption-type.aspx)할 수 있지만 대상 환경에서 테스트하지 않은 상태에서는 컴퓨터 계정에 대해 이러한 설정을 변경하지 않는 것이 좋습니다.  
  
-   초기 4시간으로 사용자 티켓(TGT) 수명 제한: 인증 정책을 사용합니다.  
  
-   제한 없는 위임 또는 제한된 위임의 통한 위임 거부: 계정을 제한하려면 ADAC(Active Directory 관리 센터)를 열고 **계정이 민감하여 위임할 수 없음** 확인란을 선택합니다.  
  
    ![계정을 제한 하려면 위치를 보여 주는 스크린샷](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
## <a name="authentication-policies"></a>인증 정책  
인증 정책은 인증 정책 개체를 포함하는 AD DS의 새 컨테이너입니다. 인증 정책에서는 계정에 대한 TGT 수명을 제한하거나 다른 클레임 관련 조건을 추가하는 등 자격 증명 도난에 대한 노출 완화에 도움이 되는 설정을 지정할 수 있습니다.  
  
Windows Server 2012 동적 액세스 제어에는 조직 전체에서 파일 서버를 구성 하는 간편한 방법을 제공 하는 중앙 액세스 정책 이라는 Active Directory 포리스트 범위의 개체 클래스를 도입 했습니다. Windows Server 2012 r 2에서는 인증 정책 (objectClass Msds-authnpolicies) 이라는 새 개체 클래스를 Windows Server 2012 R2 도메인의 계정 클래스에 인증 구성을 적용할 사용할 수 있습니다. Active Directory 계정 클래스는 다음과 같습니다.  
  
-   사용자  
  
-   Computer  
  
-   관리 서비스 계정 및 GMSA(그룹 관리 서비스 계정)  
  
### <a name="quick-kerberos-refresher"></a>빠른 Kerberos 리프레셔  
Kerberos 인증 프로토콜은 하위 프로토콜이라고도 하는 세 가지 유형의 교환 기능으로 구성됩니다.  
  
![세 가지 유형의 Kerberos 인증 프로토콜 교환, 하위 프로토콜 라고도 보여 주는 스크린샷](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbRefresher.gif)  
  
-   AS(인증 서비스) 교환(KRB_AS_*)  
  
-   TGS(Ticket-Granting Service) 교환(KRB_TGS_*)  
  
-   클라이언트/서버(AP) 교환(KRB_AP_ *)  
  
AS 교환 위치 클라이언트가 사용 하는 계정의 암호 또는 개인 키를 허용 티켓 (TGT)을 요청 하는 사전 인증자를 만드는 경우 이 교환은 사용자 로그온 시 또는 서비스 티켓이 처음 필요할 때 발생합니다.  
  
TGS 교환에서는 계정의 TGT 서비스 티켓을 요청 하는 인증자를 만드는 데 사용 되는 위치입니다. 이 교환은 인증된 연결이 필요할 때 발생합니다.  
  
AP 교환은 응용 프로그램 프로토콜 내부의 데이터처럼 일반적으로 발생하며 인증 정책의 영향을 받지 않습니다.  
  
자세한 내용은 [Kerberos 버전 5 인증 프로토콜의 작동 방식](https://technet.microsoft.com/library/cc772815(v=WS.10.aspx))을 참조하세요.  
  
### <a name="overview"></a>개요  
인증 정책은 계정에 구성 가능한 제한을 적용할 수 있는 방법을 제공하고 서비스 및 컴퓨터 계정에 대한 제한을 제공하여 보호된 사용자를 보완합니다. 인증 정책은 AS 교환 또는 TGS 교환 중에 적용됩니다.  
  
다음을 구성하여 초기 인증 또는 AS 교환을 제한할 수 있습니다.  
  
-   TGT 수명  
  
-   사용자 로그온을 제한하는 액세스 제어 조건(AS 교환을 보내는 장치에서 이 조건을 충족해야 함)  
  
![사용자 지정 도메인을 제한 하는 TGT 수명 및 액세스 제어 조건을 구성 하 여 초기 인증을 제한 하는 방법을 보여 주는 스크린샷](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictAS.gif)  
  
다음을 구성하여 TGS(Ticket-Granting Service) 교환을 통한 서비스 티켓 요청을 제한할 수 있습니다.  
  
-   TGS 교환을 보내는 장치 또는 클라이언트(사용자, 서비스, 컴퓨터)에서 충족해야 하는 액세스 제어 조건  
  
### <a name="requirements-for-using-authentication-policies"></a>인증 정책 사용을 위한 요구 사항  
  
|정책|요구 사항|  
|-----|--------|  
|사용자 지정 TGT 수명 제공| Windows Server 2012 R2 도메인 기능 수준 계정 도메인|  
|사용자 로그온 제한|-동적 액세스 제어 지원 Windows Server 2012 R2 도메인 기능 수준 계정 도메인<br />Windows 8, Windows 8.1, Windows Server 2012 또는 Windows Server 2012 R2 장치 동적 액세스 제어를 사용 하 여 지원|  
|사용자 계정 및 보안 그룹을 기반으로 하는 서비스 티켓 발급 제한| Windows Server 2012 R2 도메인 기능 수준 리소스 도메인|  
|사용자 클레임이나 장치 계정, 보안 그룹 또는 클레임을 기반으로 하는 서비스 티켓 발급 제한| 동적 액세스 제어를 사용한 Windows Server 2012 R2 도메인 기능 수준 리소스 도메인 지원|  
  
### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>특정 장치 및 호스트로 사용자 계정 제한  
관리자 권한이 있는 중요한 계정은 **보호된 사용자** 그룹의 구성원이어야 합니다. 기본적으로 **보호된 사용자** 그룹의 구성원인 계정은 없습니다. 그룹에 계정을 추가하기 전에 도메인 컨트롤러 지원을 구성하고 감사 정책을 만들어 차단 문제가 발생하지 않도록 해야 합니다.  
  
#### <a name="configure-domain-controller-support"></a>도메인 컨트롤러 지원 구성  
사용자의 계정 도메인 (DFL) Windows Server 2012 R2 도메인 기능 수준에 있어야 합니다. 모든 도메인 컨트롤러가 Windows Server 2012 r 2를 하 고 Active Directory 도메인 및 트러스트를 사용 하 여 확인 [dfl](https://technet.microsoft.com/library/cc753104.aspx) Windows Server 2012 r 2로 합니다.  
  
**동적 Access Control에 대 한 지원을 구성 하려면**  
  
1.  기본 도메인 컨트롤러 정책에서 **사용**을 클릭하여 컴퓨터 구성 | 관리 템플릿 | 시스템 | KDC에서 **클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 KDC(키 배포 센터) 클라이언트 지원**을 사용하도록 설정합니다.  
  
    ![기본 도메인 컨트롤러 정책에서 * * 사용 * *을 사용 하도록 설정 하려면 * * 클레임, 복합 인증 및 Kerberos 아머 링에 대 한 키 배포 센터 (KDC) 클라이언트 지원 * * 컴퓨터 구성에서 | 관리 템플릿 | 시스템 | KDC](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)  
  
2.  **옵션**아래의 드롭다운 목록에서 **항상 클레임 제공**을 선택합니다.  
  
    > [!NOTE]  
    > **지원** 구성할 수도 있습니다 하지만 도메인에서 Windows Server 2012 R2 DFL, Dc를 항상 필요 없으므로 제공 클레임 사용자 클레임 기반 액세스 확인이 비 클레임 인식 장치를 사용할 때 발생 하 고 클레임 인식 서비스에 연결할 호스트를 허용 합니다.  
  
    ![아래에서 * * 옵션 * *, 드롭다운 목록 상자에서 선택 * * 항상 클레임 제공](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)  
  
    > [!WARNING]  
    > 구성 **아머 링 되지 않은 인증 요청 실패** Windows 7 및 이전 운영 체제와 같은 Kerberos 아머 링을 지원 하지 않는 모든 운영 체제 또는 Windows 8을 지원 하도록 명시적으로 구성 하지 않은로 시작 하는 운영 체제에서 인증 오류가 발생 합니다.  
  
#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>ADAC를 사용하여 인증 정책에 대한 사용자 계정 감사 만들기  
  
1.  ADAC(Active Directory 관리 센터)를 엽니다.  
  
    ![Active Directory 관리 센터를 보여 주는 스크린샷](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_OpenADAC.gif)  
  
    > [!NOTE]  
    > 선택한 **인증** 노드 Windows Server 2012 R2 DFL에 있는 도메인에 대 한 표시 됩니다. 노드가 표시 되지 않는 경우 다시 시도 Windows Server 2012 R2 DFL에 있는 도메인에서 도메인 관리자 계정을 사용 하 여 합니다.  
  
2.  **인증 정책**을 클릭한 다음 **새로 만들기**를 클릭하여 새 정책을 만듭니다.  
  
    ![Authentication Policies](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)  
  
    인증 정책은 표시 이름이 있어야 하며 기본적으로 적용됩니다.  
  
3.  감사 전용 정책을 만들려면 **감사 정책 제한만**을 클릭합니다.  
  
    ![감사 정책 제한만](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)  
  
    인증 정책은 Active Directory 계정 유형에 따라 적용됩니다. 각 유형에 대한 설정을 구성하여 세 가지 계정 유형 모두에 단일 정책을 적용할 수 있습니다. 계정 유형은 다음과 같습니다.  
  
    -   사용자  
  
    -   Computer  
  
    -   관리 서비스 계정 및 그룹 관리 서비스 계정  
  
    KDC(키 배포 센터)에서 사용할 수 있는 새 보안 주체로 스키마를 확장한 경우 가장 가까운 파생된 계정 유형에서 새 계정 유형이 분류됩니다.  
  
4.  사용자 계정에 대한 TGT 수명을 구성하려면 **사용자 계정에 대한 허용 티켓 수명을 지정하세요.** 확인란을 선택하고 시간(분)을 입력합니다.  
  
    ![사용자 계정에 대 한 허용 티켓 수명을 지정합니다](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTLifetime.gif)  
  
    예를 들어 최대 TGT 수명을 10시간으로 지정하려면 그림과 같이 **600** 을 입력합니다. TGT 수명을 구성하지 않으면 계정이 **Protected Users** 그룹의 구성원인 경우 TGT 수명 및 갱신이 4시간으로 설정됩니다. 그렇지 않으면 기본 설정을 사용하는 도메인에 대한 다음 그룹 정책 관리 편집기 창에 표시된 것처럼 TGT 수명 및 갱신이 도메인 정책을 기반으로 설정됩니다.  
  
    ![기본 설정 사용 하 여 도메인에 대 한 그룹 정책 관리 편집기 창](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
5.  사용자 계정의 장치 선택을 제한하려면 **편집**을 클릭하여 장치에 필요한 조건을 정의합니다.  
  
    ![사용자 계정의 장치 선택을 제한 하려면 * * 편집 * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)  
  
6.  **액세스 제어 조건 편집** 창에서 **조건 추가**를 클릭합니다.  
  
    ![액세스 제어 조건 편집](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCondition.png)  
  
##### <a name="add-computer-account-or-group-conditions"></a>컴퓨터 계정 또는 그룹 조건 추가  
  
1.  컴퓨터 계정 또는 그룹을 구성하려면 드롭다운 목록에서 **각 그룹의 구성원** 드롭다운 목록 상자를 선택하고 **모든 그룹의 구성원**으로 변경합니다.  
  
    ![컴퓨터 계정 또는 그룹을 구성 합니다.](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompMember.png)  
  
    > [!NOTE]  
    > 이 액세스 제어는 사용자가 로그온하는 장치 또는 호스트의 조건을 정의합니다. 액세스 제어 용어에서 장치 또는 호스트의 컴퓨터 계정은 사용자를 의미하기 때문에 옵션이 **사용자**뿐입니다.  
  
2.  **항목 추가**를 클릭합니다.  
  
    ![항목 추가](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddItems.png)  
  
3.  개체 유형을 변경하려면 **개체 유형**을 클릭합니다.  
  
    ![개체 유형](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjects.gif)  
  
4.  Active Directory에서 컴퓨터 개체를 선택하려면 **컴퓨터**를 클릭한 다음 **확인**을 클릭합니다.  
  
    ![컴퓨터](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)  
  
5.  사용자를 제한할 컴퓨터의 이름을 입력하고 **이름 확인**을 클릭합니다.  
  
    ![이름 확인을 클릭 합니다.](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)  
  
6.  확인을 클릭하고 컴퓨터 계정에 대한 다른 모든 조건을 만듭니다.  
  
    ![확인을 클릭 하 고 컴퓨터 계정에 대 한 다른 모든 조건을 만듭니다](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddConditions.png)  
  
7.  작업을 마친 경우 **확인** 을 클릭하면 해당 컴퓨터 계정에 대해 정의된 조건이 표시됩니다.  
  
    ![마치면 클릭 * * 확인 * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompDone.png)  
  
##### <a name="add-computer-claim-conditions"></a>컴퓨터 클레임 조건 추가  
  
1.  컴퓨터 클레임을 구성하려면 그룹 드롭다운에서 클레임을 선택합니다.  
  
    ![컴퓨터 클레임을 구성 하려면 그룹 드롭다운에서 클레임을 선택](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaim.gif)  
  
    포리스트에 이미 프로비전된 경우에만 클레임을 사용할 수 있습니다.  
  
2.  사용자 계정의 로그온을 제한하려는 OU의 이름을 입력합니다.  
  
    ![사용자 계정의 로그온을 제한하려는 OU의 이름을 입력합니다.](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimOUName.gif)  
  
3.  작업을 마친 경우 확인을 클릭하면 상자에 정의된 조건이 표시됩니다.  
  
    ![클릭을 확인 했으면](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimComplete.gif)  
  
##### <a name="troubleshoot-missing-computer-claims"></a>누락된 컴퓨터 클레임 문제 해결  
클레임이 프로비전되어 있지만 사용할 수 없는 경우 **컴퓨터** 클래스에 대해서만 구성되었기 때문일 수 있습니다.  
  
조직 구성 단위 (OU)에 따라 인증을 제한 하려는 경우 이미 구성 된 컴퓨터의 하지만 가정해에 대해서만 **컴퓨터** 클래스입니다.  
  
![컴퓨터의 조직 구성 단위 (OU) 기반 인증을 제한 하는 방법을 보여 주는 스크린샷](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictComputers.gif)  
  
사용자 로그온을 장치로 제한하는 데 사용할 수 있는 클레임에 대해 **사용자** 확인란을 선택합니다.  
  
![Select를 확인 하 여 장치에 대 한 로그온 사용자를 제한 하는 방법을 보여 주는 스크린 샷 * * 사용자 * * 확인란 합니다.  ](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)  
  
#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>ADAC를 사용하여 인증 정책과 함께 사용자 계정 프로비전  
  
1.  **사용자** 계정에서 **정책**을 클릭합니다.  
  
    ![* * 사용자 * * 계정에 클릭 * * 정책 * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicy.gif)  
  
2.  **이 계정에 인증 정책을 할당합니다.** 확인란을 선택합니다.  
  
    ![선택 된 * *이 계정 * * 확인란에 인증 정책을 할당](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)  
  
3.  그런 다음 사용자에게 적용할 인증 정책을 선택합니다.  
  
    ![사용자에 게 적용할 인증 정책을 선택 합니다.](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicySelect.png)  
  
#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>장치 및 호스트에서 동적 액세스 제어 지원 구성  
DAC(동적 액세스 제어)를 구성하지 않고 TGT 수명을 구성할 수 있습니다. DAC는 AllowedToAuthenticateFrom 및 AllowedToAuthenticateTo를 확인하는 데에만 필요합니다.  
  
그룹 정책 또는 로컬 그룹 정책 편집기를 사용하여 컴퓨터 구성 | 관리 템플릿 | 시스템 | Kerberos에서 **클레임, 복합 인증 및 Kerberos 아머링(armoring)에 대한 Kerberos 클라이언트 지원**을 사용하도록 설정합니다.  
  
![사용 하도록 설정 하려면 그룹 정책 또는 로컬 그룹 정책 편집기를 사용 하는 방법을 보여 주는 스크린 샷 * * 클레임, 복합 인증 및 Kerberos 아머 링에 대 한 Kerberos 클라이언트 지원 * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)  
  
### <a name="troubleshoot-authentication-policies"></a>인증 정책 문제 해결  
  
#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>인증 정책이 직접 할당된 계정 확인  
인증 정책의 계정 섹션에 정책을 직접 적용한 계정이 표시됩니다.  
  
![정책을 직접 적용 하는 계정을 보여주는 인증 정책의 계정 섹션의 스크린 샷](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AccountsAssigned.gif)  
  
#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>인증 정책 실패-도메인 컨트롤러 관리 로그를 사용 하 여  
새 **인증 정책 실패-도메인 컨트롤러** 관리 로그에서 **응용 프로그램 및 서비스 로그** > **Microsoft** > **Windows** > **인증** 쉽게 인증 정책으로 인 한 오류를 검색 하기 위해 만들었습니다. 이 로그는 기본적으로 사용되지 않습니다. 사용하려면 로그 이름을 마우스 오른쪽 단추로 클릭한 다음 **로그 사용**을 클릭합니다. 새 이벤트는 기존 Kerberos TGT 및 서비스 티켓 감사 이벤트와 내용이 매우 유사합니다. 이러한 이벤트에 대한 자세한 내용은 [인증 정책 및 인증 정책 사일로](https://technet.microsoft.com/library/dn486813.aspx)를 참조하세요.  
  
### <a name="manage-authentication-policies-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 인증 정책 관리  
다음 명령은 **TestAuthenticationPolicy**라는 인증 정책을 만듭니다. **UserAllowedToAuthenticateFrom** 매개 변수는 사용자가 someFile.txt 파일의 SDDL 문자열로 인증할 수 있는 장치를 지정합니다.  
  
```  
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl  
```  
  
다음 명령은 **Filter** 매개 변수에 지정된 필터와 일치하는 모든 인증 정책을 가져옵니다.  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com  
  
```  
  
다음 명령은 지정된 인증 정책의 **UserTGTLifetimeMins** 속성 및 설명을 수정합니다.  
  
```  
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45  
```  
  
다음 명령은 **Identity** 매개 변수에 지정된 인증 정책을 제거합니다.  
  
```  
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1  
```  
  
다음 명령은 **Get-ADAuthenticationPolicy** cmdlet에서 **Filter** 매개 변수를 사용하여 적용되지 않은 모든 인증 정책을 가져옵니다. 결과 집합은 **Remove-ADAuthenticationPolicy** cmdlet으로 파이프됩니다.  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy  
```  
  
## <a name="authentication-policy-silos"></a>인증 정책 사일로  
인증 정책 사일로는 사용자, 컴퓨터 및 서비스 계정에 대한 AD DS의 새 컨테이너(objectClass AuthNPolicySilos)로서, 중요한 계정을 보호하도록 도와줍니다. 모든 조직에서는 Enterprise Admins, Domain Admins 및 Schema Admins 그룹의 구성원(이러한 계정은 공격자가 포리스트의 모든 항목에 액세스하는 데 악용될 수 있기 때문)을 보호해야 하지만 다른 계정도 보호해야 할 수 있습니다.  
  
일부 조직에서는 조직에 고유한 계정을 만들고 그룹 정책 설정을 적용하여 로컬 및 원격 대화형 로그온 및 관리 권한을 제한하는 방식으로 작업을 격리합니다. 인증 정책 사일로는 사용자, 컴퓨터 및 관리 서비스 계정 간의 관계를 정의하는 방법을 만들어 이러한 작업을 보완합니다. 계정은 하나의 사일로에만 속할 수 있습니다. 각 유형의 계정에 대한 인증 정책을 구성하여 다음을 제어할 수 있습니다.  
  
1.  갱신할 수 없는 TGT 수명  
  
2.  TGT 반환에 대한 액세스 제어 조건(참고: Kerberos 아머링(armoring)이 필요하므로 시스템에 적용할 수 없음)  
  
3.  서비스 티켓 반환에 대한 액세스 제어 조건  
  
또한 인증 정책 사일로의 계정에는 파일 서버와 같은 클레임 인식 리소스가 액세스를 제어하는 데 사용할 수 있는 사일로 클레임이 있습니다.  
  
새 보안 설명자를 구성하여 다음을 기반으로 서비스 티켓 발급을 제어할 수 있습니다.  
  
-   사용자, 사용자의 보안 그룹 및/또는 사용자의 클레임  
  
-   장치, 장치의 보안 그룹 및/또는 장치의 클레임  
  
리소스의 Dc로이 정보를 가져오는 동적 액세스 제어가 필요 합니다.  
  
-   사용자 클레임:  
  
    -   동적 Access Control을 지원하는 Windows 8 이상의 클라이언트  
  
    -   동적 액세스 제어 및 클레임을 지원하는 계정 도메인  
  
-   장치 및/또는 장치 보안 그룹:  
  
    -   동적 Access Control을 지원하는 Windows 8 이상의 클라이언트  
  
    -   복합 인증에 대해 구성된 리소스  
  
-   장치 클레임:  
  
    -   동적 Access Control을 지원하는 Windows 8 이상의 클라이언트  
  
    -   동적 액세스 제어 및 클레임을 지원하는 장치 도메인  
  
    -   복합 인증에 대해 구성된 리소스  
  
개별 계정 대신 인증 정책 사일로의 모든 구성원에 인증 정책을 적용하거나, 사일로 내의 여러 계정 유형에 별도의 인증 정책을 적용할 수 있습니다. 예를 들어 매우 강력한 권한의 사용자 계정에 하나의 인증 정책을 적용하고, 서비스 계정에 다른 정책을 적용할 수 있습니다. 인증 정책 사일로를 만들려면 먼저 인증 정책을 하나 이상 만들어야 합니다.  
  
> [!NOTE]  
> 인증 정책 사일로의 구성원에 인증 정책을 적용하거나, 사일로에 독립적으로 인증 정책을 적용하여 특정 계정 범위를 제한할 수 있습니다. 예를 들어 단일 계정 또는 소수의 계정을 보호하려는 경우 이러한 계정을 사일로에 추가하지 않고 해당 계정에 대한 정책을 설정할 수 있습니다.  
  
Active Directory 관리 센터 또는 Windows PowerShell을 사용 하 여 인증 정책 사일로 만들 수 있습니다. 기본적으로 인증 정책 사일로 사일로 정책만 감사 하므로,이 값은 지정 하는 것은 **WhatIf** Windows PowerShell cmdlet의 매개 변수입니다. 이 경우에는 정책 사일로 제한이 적용되지 않지만, 제한이 적용되는 경우 오류 발생 여부를 나타내기 위해 감사가 생성됩니다.  
  
#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Active Directory 관리 센터를 사용하여 인증 정책 사일로를 만들려면  
  
1.  **Active Directory 관리 센터**를 열고 **인증**을 클릭한 다음 **인증 정책 사일로**를 마우스 오른쪽 단추로 클릭하고 **새로 만들기**, **인증 정책 사일로**를 차례로 클릭합니다.  
  
    ![열기 * * Active Directory 관리 센터 * *을 클릭 * * 인증 * *을 마우스 오른쪽 단추로 클릭 * * 인증 정책 사일로 * *을 클릭 * * 새 * *을 클릭 한 다음 * * 인증 정책 사일로 * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)  
  
2.  **표시 이름**에 사일로의 이름을 입력합니다. **허용된 계정**에서 **추가**를 클릭하고 계정의 이름을 입력한 다음 **확인**을 클릭합니다. 사용자, 컴퓨터 또는 서비스 계정을 지정할 수 있습니다. 그런 다음 모든 보안 주체에 단일 정책을 사용할지 또는 각 유형의 보안 주체에 별도의 정책을 사용할지 지정하고 정책의 이름을 지정합니다.  
  
    ![* * 표시 이름 * *에 사일로의 이름을 입력 합니다. * * 허용 계정 * *을 클릭 * * 추가 * * 고 계정의 이름을 입력 하 고 클릭 * * 확인 * *](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)  
  
### <a name="manage-authentication-policy-silos-by-using-windows-powershell"></a>Windows PowerShell을 사용하여 인증 정책 사일로 관리  
다음 명령은 인증 정책 사일로 개체를 만들고 적용합니다.  
  
```  
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce  
```  
  
다음 명령은 **Filter** 매개 변수에 지정된 필터와 일치하는 모든 인증 정책 사일로를 가져옵니다. 그런 다음 출력을 **Format-Table** cmdlet으로 전달하여 정책의 이름과 각 정책에 대한 **Enforce** 값을 표시합니다.  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize  
  
Name  Enforce  
--  ----  
silo     True  
silos   False  
  
```  
  
다음 명령은 **Get-ADAuthenticationPolicySilo** cmdlet에서 **Filter** 매개 변수를 사용하여 적용되지 않은 모든 인증 정책 사일로를 가져오고 필터 결과를 **Remove-ADAuthenticationPolicySilo** cmdlet으로 파이프합니다.  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo  
```  
  
다음 명령은 *User01* 이라는 사용자 계정에 *Silo*라는 인증 정책 사일로에 대한 액세스 권한을 부여합니다.  
  
```  
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01  
```  
  
다음 명령은 *User01* 이라는 사용자 계정에 대해 *Silo*라는 인증 정책 사일로에 대한 액세스 권한을 거부합니다. **Confirm** 매개 변수가 **$False**로 설정되어 있으므로 확인 메시지는 나타나지 않습니다.  
  
```  
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False  
```  
  
다음 예제에서는 먼저 **Get-ADComputer** cmdlet을 사용하여 **Filter** 매개 변수에 지정된 필터와 일치하는 모든 컴퓨터 계정을 가져옵니다. 이 명령의 출력을 **Set-ADAccountAuthenticatinPolicySilo**로 전달하여 해당 계정에 *Silo*라는 인증 정책 사일로 및 *AuthenticationPolicy02*라는 인증 정책을 할당합니다.  
  
```  
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02  
```  
  

