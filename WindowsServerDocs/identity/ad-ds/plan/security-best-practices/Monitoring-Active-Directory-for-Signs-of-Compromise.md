---
ms.assetid: a7ef2fba-b05c-4be2-93b2-b9456244c3ad
title: "침입 Active Directory를 모니터링합니다."
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 096f2fa58b9aae53a06bf26c2107eb4cee3aa5d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="monitoring-active-directory-for-signs-of-compromise"></a>침입 Active Directory를 모니터링합니다.

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*법률 5 번호: 터널 경계는 보안 가격 합니다.* - [10 Immutable Laws of Security Administration](https://technet.microsoft.com/library/cc722488.aspx)  
  
시스템 모니터링 단색 이벤트 로그 모든 보안 Active Directory 설계의 중요 한 부분입니다. 컴퓨터 보안 손상 많은 발견 될 수 있습니다 초기 이벤트는 희생자 모니터링 및 경고 적절 한 이벤트 로그 위임 하는 경우 합니다. 독립 보고서이 결론을 지원 오래 했습니다. 예를 들어 있는 [2009 Verizon 데이터 위반 보고서](http://www.verizonbusiness.com/resources/security/reports/2009_databreach_rp.pdf) 상태:  
  
"이벤트를 모니터링 하 고 로그 분석 분명 ineffectiveness 계속 약간는 enigma 수 있습니다. 검색에 대 한 기회가입니다. 수 사관 했음을 알아차렸을 희생자 66%가 증명 이들과 되었던 자녀가 더 정확한 후 분석 이러한 리소스에는 위반 검색 로그에서 사용할 수 있는 충분 한 정보는. "  
  
이 부족 이벤트 로그 활성 모니터링 많은 회사의 보안 defense 계획 일관 된 결점 유지 됩니다. [2012 Verizon 데이터 위반 보고서](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf) 발견 침해 85% 촬영 발견 하는 몇 주도 희생자 84% 이벤트 로그에서 위반의 증거를 했습니다.  
  
## <a name="windows-audit-policy"></a>Windows 감사 정책  
Microsoft 공식 엔터프라이즈 지원 블로그에 대 한 링크는 다음과 같습니다. 이러한 블로그 콘텐츠 조언을, 지침 및 추천을 제공 하는 감사에 대 한 Active Directory infrastructure의 보안을 강화 하는 데 도움이 됩니다 및 감사 정책 디자인할 때 소중한 리소스는 제공 합니다.  
  
-   [마술은 전 세계 개체 액세스 감사](http://blogs.technet.com/b/askds/archive/2011/03/10/global-object-access-auditing-is-magic.aspx) -고급 감사 정책 구성에 추가 된 Windows 7 및 Windows Server 2008 R2 수 있는 데이터의 종류 하려는 쉽게 감사 하 고 있지 스크립트 및 auditpol.exe 기간이 설정 라는 제어 메커니즘을 설명 합니다.  
  
-   [Windows 2008 변경 감사 소개](http://blogs.technet.com/b/askds/archive/2007/10/19/introducing-auditing-changes-in-windows-2008.aspx) -Windows Server 2008에서 감사 변경한을 소개 합니다.  
  
-   [감사 힌트 Vista와 2008 냉각](http://blogs.technet.com/b/askds/archive/2007/11/16/cool-auditing-tricks-in-vista-and-2008.aspx) -문제를 해결 하거나 사용자 환경에서 발생 하는 내용을 보는에 사용할 수 있는 Windows Server 2008 및 Windows Vista의 감사 흥미로운 기능에 설명 합니다.  
  
-   [Windows Server 2008 및 Windows Vista에 대 한 분석을 한곳에서 구입할](http://blogs.technet.com/b/askds/archive/2008/03/27/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista.aspx) -기능 및 Windows Server 2008 및 Windows Vista에 포함 된 정보의 감사 수록 포함 되어 있습니다.  
  
다음 링크 Windows Server 2008에 감사 광고 DS에 대 한 정보와 Windows Windows 8 및 Windows Server 2012에서 감사 향상 된 기능에 대 한 정보를 제공 합니다.  
  
-   [보안 감사의 새로운](https://technet.microsoft.com/library/hh849638.aspx) -개요 새 보안 기능 Windows 8 및 Windows Server 2012에 감사를 제공 합니다.  
  
-   [광고 DS 감사 단계별 가이드](https://technet.microsoft.com/library/a9c25483-89e2-4202-881c-ea8e02b4b2a5.aspx) -Windows Server 2008 새로운 Active Directory 도메인 서비스 (AD DS) 감사 기능에 설명 합니다. 또한이 새로운 기능을 구현 하는 절차를 제공 합니다.  
  
### <a name="windows-audit-categories"></a>Windows 감사 범주  
이전 Windows Vista 및 Windows Server 2008, Windows는 9 개의 이벤트 로그 감사 정책 범주 있었습니다.  
  
-   계정 로그온 이벤트  
  
-   계정 관리  
  
-   디렉터리 서비스 액세스  
  
-   로그온 이벤트  
  
-   개체 액세스  
  
-   정책 변경  
  
-   사용 권한  
  
-   프로세스 추적  
  
-   시스템 이벤트  
  
이러한 9 번체 감사 범주 감사 정책으로 구성 됩니다. 성공, 실패 하거나 성공 및 오류에 대 한 각 감사 정책 범주를 사용할 수 이벤트 합니다. 다음 섹션에 설명 포함 됩니다.  
  
#### <a name="audit-policy-category-descriptions"></a>정책 범주 설명 감사 합니다.  
감사 정책 범주 이벤트 로그 메시지 종류를 사용 하도록 설정 합니다.  
  
##### <a name="audit-account-logon-events"></a>감사 계정 로그온 이벤트  
보안 사용자 (예를 들어, 사용자를 컴퓨터 또는 서비스 계정)에 로그인 하거나 계정을 확인 하 다른 컴퓨터를 사용 하는 컴퓨터에서 로그 오프는 각 인스턴스를 보고 합니다. 계정 로그온 이벤트 도메인 컨트롤러에 보안 주 도메인 계정 인증 때 생성 됩니다. 인증 로컬 컴퓨터에서 로컬 사용자의 로컬 보안 로그에 기록 로그온 이벤트를 생성 합니다. 계정 로그 오프 이벤트가 기록 됩니다.  
  
이 범주 "노이즈가" 많은 Windows 계정에 로그인 하는 데 지속적으로 때문에 및 생성 지역 및 원격 컴퓨터에서 비즈니스 일반 과정에서 합니다. 여전히, 모든 보안 계획 성공 및이 감사 범주의 오류를 포함 해야 합니다.  
  
##### <a name="audit-account-management"></a>감사 계정 관리  
이 감사 설정 관리 사용자 및 그룹 추적을 결정 합니다. 예를 들어, 사용자 및 그룹을 추적 때 사용자 또는 컴퓨터 계정, 보안 그룹 메일 그룹을 만든, 변경 또는 삭제 됨, 사용자 또는 컴퓨터 계정의 이름을 바꿀, 비활성화 되어 있거나 사용할 수 있습니다. 또는 때 사용자 또는 컴퓨터 암호를 변경 합니다. 이벤트를 추가 하거나 다른 그룹에서 제거 하는 사용자 또는 그룹에 대 한 생성할 수 있습니다.  
  
##### <a name="audit-directory-service-access"></a>디렉터리 서비스 액세스 감사  

이 정책 설정을 있는지 확인 Active Directory 개체로 보안 주 액세스 감사 하는 고유한 지정된 시스템 액세스 제어 목록 (SACL) 합니다. 일반적으로이 범주 에서만 도메인 컨트롤러에서 사용 해야 합니다. 이 설정을 생성 많이 "노이즈."를 사용 하는 경우  
  
##### <a name="audit-logon-events"></a>감사 로그온 이벤트  
로컬 보안 사용자가 로컬 컴퓨터에서 인증 하는 경우 로그온 이벤트 생성 됩니다. 로그온 이벤트 기록 로컬 컴퓨터에 발생 하는 도메인 로그온 합니다. 계정 로그 오프 이벤트 생성 되지 않습니다. 로그온 이벤트의 "," 많은 생성 활성화 되어 있지만 모든 보안 감사 요금제에 기본적으로 사용할 수 됩니다.  
  
##### <a name="audit-object-access"></a>감사 개체 액세스  
개체 액세스 활성화 감사 이후 정의 된 개체 예, 열린, 읽기, 이름이 바뀐, 삭제 됨, 또는 닫힘) (에 액세스할 때 이벤트 생성할 수 있습니다. 주 감사 범주를 활성화 한 후 관리자는 개체 사용 감사는 정의 개별적으로 해야 합니다. 많은 Windows 시스템 개체를 사용 하도록 설정 감사 관리자가 정의 된 하기 전에 이벤트를 얻기 위해 일반적으로 예정이 범주를 사용 하므로 함께 제공 됩니다.  
  
이 범주는 매우 "시끄러운" 및 각 개체 액세스에 대해 5-10 이벤트가 생성 됩니다. 유용한 정보를 얻을 개체 감사 새 관리자에 대 한 어려울 수 있습니다. 필요한 경우에 사용 해야 합니다.  
  
##### <a name="auditing-policy-change"></a>감사 정책 변경  
이 정책 설정을 사용자 권한 할당 정책, Windows 방화벽 정책, 보안 정책이 또는 감사 정책에 대 한 변경 변경에 대 한 모든 내용의 감사를 결정 합니다. 이 범주 모든 컴퓨터에서 사용 해야 합니다. 거의 노이즈를 생성합니다.  
  
##### <a name="audit-privilege-use"></a>감사 권한 사용  

사용자 권한과 Windows (예를 들어, 로그온 일괄 작업 및 운영 체제의 일부로 Act)의 사용에는 여러 가지가 있습니다. 이 정책 설정을 보안 사용자의 각각 인스턴스 사용자 권한을 나 권한을 행사에 감사를 결정 합니다. 하지만 "노이즈가" 많은이 범주 결과 사용 하면 높은 권한을 사용 하 여 사용자 계정 보안을 추적 하는 데 도움이 될 수 있습니다.  
  
##### <a name="audit-process-tracking"></a>감사 프로세스 추적  
이 정책 설정을 자세한 프로세스 프로그램 정품 인증, 프로세스 종료 핸들 중복 및 간접 개체 액세스 같은 이벤트에 대 한 정보를 추적 감사 여부를 결정 합니다. 자녀가 사용 하 여 프로그램과 악의적인 사용자가 추적 하는 데 유용 합니다.  
  
감사 프로세스 추적 사용 하면 일반적으로 설정 되 많은 수의 이벤트를 생성 **감사 안**합니다. 그러나이 설정은 프로세스를 시작에 대 한 자세한 로그를 문제 대응 하는 동안 큰 도움이 및 된 시간 제공할 수 있습니다. 도메인 컨트롤러 및 기타 단일 역할 infrastructure 서버에 대 한이 범주 항상 안전 하 게 설정 수 있습니다. 단일 역할 서버 업무 정상적 중 교통 추적 많은 프로세스를 생성 하지 않습니다. 따라서 이벤트를 캡처하 무단으로 발생 하는 경우 사용할 수 있습니다.  
  
##### <a name="system-events-audit"></a>시스템 이벤트 감사  

시스템 이벤트는 일반 다양 범주 거의 컴퓨터, 해당 시스템 보안 또는 보안 로그 영향을 미칠 수 있는 다양 한 이벤트를 등록 하는 중입니다. 컴퓨터를 종료 및 다시 시작, 정전, 시스템 시간 변경 내용, 인증 패키지 초기화, 감사 로그 개 간지 사이, 가장 문제 및 다양 한 다른 일반적인 이벤트에 대 한 이벤트를 포함합니다. 일반적으로이 감사 범주를 사용 하면 "노이즈가" 많은 생성 하지만 사용 하지 않으면 것이 좋습니다 하기 어렵습니다 매우 유용 충분 한 이벤트를 생성 합니다.  
  
#### <a name="advanced-audit-policies"></a>고급 감사 정책  
Windows Vista 및 Windows Server 2008 부터는 Microsoft 이벤트 로그 범주 선택할 수 만들어 주 감사 각 범주 아래 하위 범주 방식으로 향상 되었습니다. 하위 범주 감사 주요 범주를 사용 하 여 그렇지 않은 경우 수 보다 훨씬 더 자세한 되도록 허용 합니다. 하위 범주를 사용 하 여 특정 주 범주의 부분만 사용 하도록 설정 하 고 사용 되지 않지만 열어야 생성 이벤트 건너뛸 수 있습니다. 성공, 실패 하거나 성공 및 오류에 대 한 각 감사 정책을 하위 범주를 사용할 수 이벤트 합니다.  
  
모든 사용 가능한 감사 하위 범주를 표시 하려면 그룹 정책 개체에 감사 정책 고급 컨테이너 검토 하거나 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008, Windows 8, Windows 7 또는 Windows Vista를 실행 하는 컴퓨터에서 명령 프롬프트에서 다음 명령을 입력 합니다.  
  
**auditpol /list /subcategory: \ ***  
  
Windows Server 2012, Windows Server 2008 R2 또는 Windows 2008 실행 하는 컴퓨터의 현재 구성 된 감사 하위 범주 목록을 가져오려면 다음을 입력 합니다.  
  
**auditpol /get /category: \ ***  
  
다음 스크린샷 감사 정책 나열 auditpol.exe의 예를 나타냅니다.  
  
![광고를 모니터링합니다.](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_5.gif)  
  
> [!NOTE]  
> Auditpol.exe는 반면 그룹 정책 설정 된 모든 감사 정책 상태를 항상 정확 하 게 보고 하지 않습니다. 참조 [2008 R2 및 Windows 7의 실제 감사 정책 가져오는](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) 에 대 한 자세한 내용은 합니다.  
  
각 기본 범주 여러 하위 범주에 있습니다. 다음은 범주의 하위 범주와 그 기능에 대 한 설명을의 목록입니다.  
  
### <a name="auditing-subcategories-descriptions"></a>하위 범주 설명을 감사합니다.  
감사 정책 하위 범주 이벤트 로그 메시지 종류를 설정합니다.  
  
#### <a name="account-logon"></a>계정 로그온  
  
##### <a name="credential-validation"></a>자격 증명 유효성 검사  
이 범주의 자격 증명을 위해 사용자 계정 로그온 요청을 제출 유효성 검사 결과 보고 합니다. 이러한 이벤트 자격 증명을 신뢰할 수 있는 컴퓨터에 발생 합니다. 도메인 계정에 대 한 로컬 계정, 로컬 컴퓨터가 신뢰할 수 있는 반면 도메인 컨트롤러를 신뢰할 수 있습니다.  
  
도메인 환경에서 대부분 계정 로그온 이벤트의 도메인 계정에 대 한 권한 있는 도메인 컨트롤러의 보안 로그에 기록 됩니다. 그러나 이러한 이벤트 로컬 계정을 사용 하 여 로그온 할 때 조직에서 다른 컴퓨터에 발생할 수 있습니다.  
  
##### <a name="kerberos-service-ticket-operations"></a>Kerberos 서비스 티켓 작업  
이 범주의 Kerberos 티켓 요청 프로세스 도메인 계정에 대 한 권한이 있는 도메인 컨트롤러에서 생성 된 이벤트를 보고 합니다.  
  
##### <a name="kerberos-authentication-service"></a>Kerberos 인증 서비스  
이 범주의 Kerberos 인증 서비스에서 생성 되는 이벤트를 보고 합니다. 이러한 이벤트 자격 증명을 신뢰할 수 있는 컴퓨터에 발생 합니다.  
  
##### <a name="other-account-logon-events"></a>다른 계정 로그온 이벤트  
이 범주의 하는 유효성 검사 자격 증명 또는 Kerberos 티켓 사용자 계정 로그온 요청을 제출 자격에 대 한 응답으로 발생 하는 이벤트를 보고 합니다. 이러한 이벤트 자격 증명을 신뢰할 수 있는 컴퓨터에 발생 합니다. 도메인 계정에 대 한 로컬 계정, 로컬 컴퓨터가 신뢰할 수 있는 반면 도메인 컨트롤러를 신뢰할 수 있습니다.  
  
도메인 환경에서 대부분 계정 로그온 이벤트 도메인 계정에 대 한 권한 있는 도메인 컨트롤러의 보안 로그에 기록 됩니다. 그러나 이러한 이벤트 로컬 계정을 사용 하 여 로그온 할 때 조직에서 다른 컴퓨터에 발생할 수 있습니다. 예는 다음과 같은 포함 될 수 있습니다.  
  
-   원격 데스크톱 서비스 세션 연결 끊기  
  
-   원격 데스크톱 서비스 세션 새  
  
-   잠금 및 잠금 해제 워크스테이션  
  
-   화면 보호기를 호출  
  
-   화면 보호기 해제  
  
-   재생 공격, Kerberos 요청 동일한 정보를 두 번 수신 되는 kerberos 검색  
  
-   사용자 또는 컴퓨터 계정 부여 무선 네트워크에 대 한 액세스  
  
-   유선된 802.1에 대 한 액세스 하는 컴퓨터 또는 사용자 계정에 게 부여 네트워크 x  
  
#### <a name="account-management"></a>계정 관리  
  
##### <a name="user-account-management"></a>사용자 계정 관리  
이 범주의 각 사용자 계정 관리 등 사용자 계정을 만든, 변경 또는 삭제 됨, 이벤트를 보고 사용자 계정 이름이 비활성화 되어 있거나 사용할 수 있습니다. 또는 암호를 설정 하거나 변경 합니다. 이 감사 정책 설정을 사용 하는 경우 관리자 트랙 이벤트 사용자 계정의 악성, 사고, 및 공인 만들기를 수 있습니다.  
  
##### <a name="computer-account-management"></a>컴퓨터 계정 관리  
이 범주의 보고 각 이벤트 컴퓨터 계정 관리 때 계정을 만든 변경, 삭제, 이름이, 비활성화 되어 있거나 사용 하도록 설정 합니다.  
  
##### <a name="security-group-management"></a>보안 그룹 관리  
이 범주의 보안 그룹 관리 구성원에 추가 하거나 제거 보안 그룹에서 또는 그룹 보안 만든, 변경 또는 삭제 등의 각 이벤트를 보고 합니다. 이 감사 정책 설정을 사용 하는 경우 관리자가 그룹 계정 보안 악성, 사고, 및 공인 작성을 감지 하 트랙 이벤트 수 있습니다.  
  
##### <a name="distribution-group-management"></a>메일 그룹 관리  
이 범주의 각 메일 그룹 관리 메일 그룹을 만든, 변경 또는 삭제 또는 구성원에 추가 하거나 메일 그룹에서 제거 같은 이벤트를 보고 합니다. 이 감사 정책 설정을 사용 하는 경우 관리자가 그룹 계정 악성, 사고, 및 공인 작성을 감지 하 트랙 이벤트 수 있습니다.  
  
##### <a name="application-group-management"></a>응용 프로그램 그룹 관리  
이 범주의 각 응용 프로그램 그룹 관리 이벤트 구성원에 추가 하거나 응용 프로그램 그룹에서 제거 또는 응용 프로그램 그룹 만든, 변경 또는 삭제 등의 컴퓨터에 보고 합니다. 이 감사 정책 설정을 사용 하는 경우 관리자 트랙 이벤트 응용 프로그램 그룹 계정 악성, 사고, 및 공인 작성을 수 있습니다.  
  
##### <a name="other-account-management-events"></a>다른 계정 관리 이벤트  
이 범주의 다른 계정 관리 이벤트를 보고합니다.  
  
#### <a name="detailed-process-tracking"></a>자세한 프로세스 추적  
  
##### <a name="process-creation"></a>프로세스 만들기  
이 범주의 프로세스의 생성 및 사용자 또는 만든 프로그램의 이름을 보고 합니다.  
  
##### <a name="process-termination"></a>프로세스 종료  
이 범주의 종료 되는 프로세스를 보고 합니다.  
  
##### <a name="dpapi-activity"></a>하는 DPAPI 활동  
이 범주의 보고 암호화 또는 데이터 보호 응용 프로그램 프로그래밍 인터페이스는 DPAPI ()를 호출 하는 암호를 해독 합니다. 저장 된 암호 등 비밀 정보 및 중요 한 정보를 보호 하는 DPAPI 사용 됩니다.  
  
##### <a name="rpc-events"></a>RPC 이벤트  
이 범주의 보고서 원격 프로시저 호출 (RPC) 연결 이벤트 합니다.  
  
#### <a name="directory-service-access"></a>디렉터리 서비스 액세스  
  
##### <a name="directory-service-access"></a>디렉터리 서비스 액세스  
이 범주의 AD DS 개체 액세스 하는 경우에 보고 합니다. 구성 된 Sacl 유일한 개체 인해 SACL 항목을 일치 하는 방식에서 액세스할 때 되도록 생성 하 고만 이벤트 감사 합니다. 이러한 이벤트는 이전 버전의 Windows Server에서 디렉터리 서비스 액세스 이벤트 유사 합니다. 이 범주의 도메인 컨트롤러에만 적용 됩니다.  
  
##### <a name="directory-service-changes"></a>디렉터리 서비스를 변경  
이 범주의 변경 개체 AD DS에 보고합니다. 만들 보고 되는 변경 내용 형식을, 수정, 이동 및 개체 수행 하는 작업 취소 합니다. 디렉터리 서비스 변경 감사, 경우에 따라 변경 된 개체 변경된 속성의 이전 버전과 새 값 나타냅니다. Sacl 개체 인해 SACL 항목을 일치 하는 방식에서 액세스할 때 되도록 생성 하 고만 이벤트 감사 합니다. 일부 개체와 속성 개체 클래스 스키마를에 설정으로 인해 생성 이벤트 감사 발생 하지 않습니다. 이 범주의 도메인 컨트롤러에만 적용 됩니다.  
  
##### <a name="directory-service-replication"></a>디렉터리 서비스 복제  
두 명의 도메인 컨트롤러 간 복제 시작 되 고 종료 될 때이 하위 범주를 보고 합니다.  
  
##### <a name="detailed-directory-service-replication"></a>자세한 디렉터리 서비스 복제  
이 범주의 도메인 컨트롤러 간에 복제 정보에 대 한 자세한 정보를 알려줍니다. 이러한 이벤트에서 볼륨 높은 될 수 있습니다.  
  
#### <a name="logonlogoff"></a>로그온/로그 오프  
  
##### <a name="logon"></a>로그온  
사용자가 시스템에 로그온 할 때이 하위 범주를 보고 합니다. 이러한 이벤트는 액세스 컴퓨터에 발생합니다. 대화형 로그온에 대 한 이러한 이벤트 세대에에 로그인 하는 컴퓨터에 발생 합니다. 네트워크 로그온 액세스 공유를 위해 수행,이 이벤트 액세스 리소스를 호스트 하는 컴퓨터에서 생성 합니다. 이 설정으로 구성 된 **감사 안**, 것이 어렵게 만들거나는 사용자가 액세스 하거나 조직 컴퓨터에 액세스 하려고 확인할 수 있습니다.  
  
##### <a name="network-policy-server"></a>네트워크 정책 서버  
이 범주의 RADIUS (IAS) 및 액세스 보호 (NAP 네트워크) 사용자 액세스 요청에서 생성 된 이벤트를 보고 합니다. 이러한 요청 될 수 있는 **부여**, **거부**, **취소**, **격리**, **잠금**, 및 **잠금 해제**합니다. 이 설정을 감사 중간 또는 높은 양의 NPS 및 IAS 서버에 기록 될 수 있습니다.  
  
##### <a name="ipsec-main-mode"></a>주 IPsec 모드  
이 범주의 주 모드 협상 인터넷 키 (IKE 교환) 및 인터넷 프로토콜 인증 (AuthIP)의 결과 보고합니다.  
  
##### <a name="ipsec-extended-mode"></a>IPsec 모드의 확장  
이 범주의 모드 확장 협상 AuthIP 결과 보고합니다.  
  
##### <a name="other-logonlogoff-events"></a>다른 로그온/로그 오프 이벤트  
이 범주의 다른 로그온 및 원격 데스크톱 서비스의 연결이 끊어지기 세션과 다시 연결 되 면 RunAs을 사용 하 여 다른 계정으로 프로세스를 실행 하 고 잠금 및 워크스테이션 잠금 해제 등 로그 오프 관련 이벤트에 보고 합니다.  
  
##### <a name="logoff"></a>로그 오프  
이 하위 범주 사용자가 시스템 로그에 보고 합니다. 이러한 이벤트는 액세스 컴퓨터에 발생합니다. 대화형 로그온에 대 한 이러한 이벤트 세대에에 로그인 하는 컴퓨터에 발생 합니다. 네트워크 로그온 액세스 공유를 위해 수행,이 이벤트 액세스 리소스를 호스트 하는 컴퓨터에서 생성 합니다. 이 설정으로 구성 된 **감사 안**, 것이 어렵게 만들거나는 사용자가 액세스 하거나 조직 컴퓨터에 액세스 하려고 확인할 수 있습니다.  
  
##### <a name="account-lockout"></a>계정 잠금  
이 범주의 너무 많은 로그온 시도가 실패 결과 사용자의 계정을 잠기면 보고 합니다.  
  
##### <a name="ipsec-quick-mode"></a>빠른 IPsec 모드  
이 범주의 빠른 모드 협상 IKE 프로토콜 및 AuthIP 결과 보고합니다.  
  
##### <a name="special-logon"></a>특별 한 로그온  
이 범주의 보고 특별 한 로그온을 사용 합니다. 특별 한 로그온이에 해당 하는 관리자 권한이 있는 프로세스 상위 상승 하는 데 사용 될 로그온 합니다.  
  
#### <a name="policy-change"></a>정책 변경  
  
##### <a name="audit-policy-change"></a>감사 정책 변경  
이 범주의 보고 감사 정책이 SACL 변경 사항을 포함 하 여 변경 합니다.  
  
##### <a name="authentication-policy-change"></a>인증 정책 변경  
이 범주의 보고 인증 정책이 변경 합니다.  
  
##### <a name="authorization-policy-change"></a>승인 정책 변경  
이 범주의 보고 인증 정책이 (DACL) 사용 권한 변경 사항을 포함 하 여 변경 합니다.  
  
##### <a name="mpssvc-rule-level-policy-change"></a>MPSSVC 규칙 수준 정책 변경  
이 범주의 보고 정책 규칙 Microsoft 보호 서비스 (MPSSVC.exe) 사용 하 여 변경 합니다. Windows 방화벽에서이 서비스 사용 됩니다.  
  
##### <a name="filtering-platform-policy-change"></a>필터링 플랫폼 정책 변경  
이 범주의 추가 및 시작 필터를 포함 하 여 WFP에서 개체의 제거를 보고 합니다. 이러한 이벤트에서 볼륨 높은 될 수 있습니다.  
  
##### <a name="other-policy-change-events"></a>다른 정책 변경 이벤트  
이 범주의 다른 종류의 보안 정책 변경 신뢰할 수 있는 TPM (플랫폼 모듈) 또는 암호화 공급자의 구성 등 보고합니다.  
  
#### <a name="privilege-use"></a>사용 권한  
  
##### <a name="sensitive-privilege-use"></a>중요 한 권한 사용  
이 범주의 때 사용자 계정 보고 또는 서비스 사용 민감한 권한 합니다. 중요 한 권한 포함 다음 사용자 권한을: 운영 체제의 일부로 파일과 디렉터리가 백업, 토큰 개체, 프로그램, 컴퓨터 및 사용자 계정이 위임 신뢰할 수 있는, 보안 감사 생성, 인증 후 클라이언트 가장, 로드 하 고 디바이스 드라이버를 언로드하, 감사 관리 하 고 보안 로그, 펌웨어 환경을 값을 수정할 파일을 만들고 프로세스 수준을 토큰 바꾸기 파일과 디렉터리가, 복원 하 고 파일 또는 기타 개체의 소유권을 합니다. 이 범주의 감사 이벤트 양의 만들어집니다.  
  
##### <a name="nonsensitive-privilege-use"></a>Nonsensitive 권한 사용  
이 범주의 때 사용자 계정 보고 또는 서비스 사용 nonsensitive 권한 합니다. Nonsensitive 권한 포함 다음 사용자 권한을: 신뢰할 수 있는 발신자로 자격 증명 관리자에 액세스, 네트워크에서이 컴퓨터에 액세스, 워크스테이션 도메인에 추가, 메모리 할당량 프로세스에 대 한 조정, 로컬 로그온 허용, 원격 데스크톱 서비스를 통해 로그온 허용, 통과 확인을 건너뛸, 시스템 시간을 변경할 페이지 파일을 만들, 만들기 글로벌 개체, 영구 공유 개체 만들기, 기호 링크 만들기 네트워크에서이 컴퓨터가 액세스 거부, 일괄 작업으로 로그온 거부, 로그온 서비스 거부, 로컬 로그온 거부, 원격 데스크톱 서비스를 통해 로그온 거부, 강제 종료 원격 시스템에서 프로세스 작업 집합을 늘릴, 일정 우선 순위를 높일, 메모리의 페이지를 잠그는, 일괄 작업으로 로그온, 서비스 로그인, 수정 개체 레이블 볼륨 유지 관리 작업을 단일 프로세스 프로필을 프로필 시스템 성능을 수행할 도킹 스테이션의 컴퓨터를 제거, 시스템, 종료 및 디렉터리 서비스의 데이터를 동기화 합니다. 이 범주의 감사 매우 높은 볼륨의 이벤트 만들어집니다.  
  
##### <a name="other-privilege-use-events"></a>다른 권한 사용 하 여 이벤트  
이 보안 정책 설정 현재 사용 되지 않습니다.  
  
#### <a name="object-access"></a>개체 액세스  
  
##### <a name="file-system"></a>시스템 파일  
시스템 개체 파일에 액세스할 때이 하위 범주를 보고 합니다. Sacl와만 파일 시스템 개체 인해 SACL 항목을 일치 하는 방식 액세스할 때 되도록 생성 하 고만 이벤트 감사 합니다. 자체적으로이 정책 설정을 발생 하지 않습니다 이벤트에 대 한 감사 합니다. 지정 된 시스템 액세스 제어 목록 SACL (), 파일 시스템 개체 액세스 하는 사용자의 이벤트 감사 것인지 결정 효과적으로 하는 데 감사를 사용 합니다.  
  
개체 액세스 감사 설정을 하도록 구성 된 경우 **성공**, 감사 항목이 만들어집니다 때마다 사용자가 지정 된 SACL 개체 성공적으로 액세스할 합니다. 이 정책 설정을 하도록 구성 된 경우 **오류**, 감사 항목이 하면 지정 된 SACL 개체에 액세스 하지 못하는 사용자 때마다 생성 됩니다.  
  
##### <a name="registry"></a>레지스트리  
레지스트리 개체 액세스할 때이 하위 범주를 보고 합니다. Sacl으로 레지스트리 개체 인해 SACL 항목을 일치 하는 방식 액세스할 때 되도록 생성 하 고만 이벤트 감사 합니다. 자체적으로이 정책 설정을 발생 하지 않습니다 이벤트에 대 한 감사 합니다.  
  
##### <a name="kernel-object"></a>커널 개체  
프로세스와 뮤텍스 같은 커널 개체 액세스할 때이 하위 범주를 보고 합니다. Sacl으로 커널 개체 인해 SACL 항목을 일치 하는 방식 액세스할 때 되도록 생성 하 고만 이벤트 감사 합니다. 일반적으로 커널 개체 AuditBaseObjects 또는 AuditBaseDirectories 감사 옵션을 사용 하는 경우에 Sacl 제공 됩니다.  
  
##### <a name="sam"></a>삼로  
로컬 보안 계정을 관리자 (삼로) 인증 데이터베이스 개체 액세스할 때이 하위 범주를 보고 합니다.  
  
##### <a name="certification-services"></a>인증 서비스  
인증 서비스 작업을 수행할 때이 하위 범주를 보고 합니다.  
  
##### <a name="application-generated"></a>응용 프로그램 생성  
이 범주의 응용 프로그램 (Api) 응용 프로그램 프로그래밍 인터페이스 감사 Windows를 사용 하 여 이벤트 감사 생성 하려고 하면 보고 합니다.  
  
##### <a name="handle-manipulation"></a>핸들 조작  
이 범주의 개체 핸들을 열기 또는 닫기 때 보고 합니다. Sacl 개체 이러한 이벤트를 생성 하 고 시도한 핸들 작업 SACL 항목을 일치 하는 경우에 하면 됩니다. 핸들 이벤트는만 개체 유형에 생성 조작 해당 개체 액세스 하위 범주 (예를 들어, 파일 시스템 또는 레지스트리)를 사용 하도록 설정 합니다.  
  
##### <a name="file-share"></a>파일 공유  
파일 공유 액세스할 때이 하위 범주를 보고 합니다. 자체적으로이 정책 설정을 발생 하지 않습니다 이벤트에 대 한 감사 합니다. 지정 된 시스템 액세스 제어 목록 SACL (), 파일 공유 개체를 액세스 하는 사용자의 이벤트 감사 것인지 결정 효과적으로 하는 데 감사를 사용 합니다.  
  
##### <a name="filtering-platform-packet-drop"></a>필터링 플랫폼 패킷 놓기  
이 하위 범주에서 필터링 WFP (Windows 플랫폼) 패킷을 때 보고 합니다. 이러한 이벤트에서 볼륨 높은 될 수 있습니다.  
  
##### <a name="filtering-platform-connection"></a>필터링 플랫폼 연결  
이 범주의 연결 허용 또는 WFP에 의해 차단 되 면 보고 합니다. 이러한 이벤트에서 볼륨 높은 될 수 있습니다.  
  
##### <a name="other-object-access-events"></a>다른 개체 액세스 이벤트  
이 범주의 작업 스케줄러 작업 및 COM + 개체와 같은 다른 개체 액세스 관련 이벤트를 보고 합니다.  
  
#### <a name="system"></a>시스템  
  
##### <a name="security-state-change"></a>보안 상태 변경  
이 범주의 변경 보안 하위 시스템 시작 하 고 중지 하는 때와 같은 시스템의 보안 상태에 보고 합니다.  
  
##### <a name="security-system-extension"></a>보안 시스템 확장  
이 범주의 인증 패키지 같은 확장 코드 로드 되는 보안 하위 시스템에서 보고 됩니다.  
  
##### <a name="system-integrity"></a>시스템 무결성  
이 범주의 보안 하위 시스템의 무결성을 위반 하는 경우에 보고합니다.  
  
IPsec 드라이버  
  
이 범주의 인터넷 프로토콜 보안 드라이버의 활동에 보고합니다.  
  
##### <a name="other-system-events"></a>기타 시스템 이벤트  
이 범주의 기타 시스템 이벤트에 보고합니다.  
  
하위 범주 설명에 대 한 자세한 내용은 참조는 [Microsoft 보안 준수 관리자 도구](https://technet.microsoft.com/library/cc677002.aspx)합니다.  
  
각 조직 이전 덮여 범주와 하위 범주를 검토 하 고 환경에 가장 잘 맞는 하는 기능을 사용 하도록 설정 해야 합니다. 변경 내용은 정책을 감사할 생산 환경에서 배포 하기 전에 항상 테스트 합니다.  
  
### <a name="configuring-windows-audit-policy"></a>구성 Windows 감사 정책  
Windows 정책 감사 그룹 정책, auditpol.exe, Api를 또는 레지스트리 편집을 사용 하 여 설정할 수 있습니다. 대부분의 회사에 대 한 감사 정책 구성 하는 권장된 방법은 그룹 정책 또는 auditpol.exe입니다. 시스템의 감사 정책 설정 하는 관리자 수준 계정 사용 권한이 나 위임된 적절 한 권한이 필요 합니다.  
  
> [!NOTE]  
> **관리 하 고 보안 감사 로그** 보안 사용자에 권한을 부여 해야 합니다 (관리자가 기본적으로 함) 개체 액세스 옵션을 파일, Active Directory 개체 레지스트리 키 등 개별 리소스에 감사를 수정할 수 있도록 합니다.  
  
#### <a name="setting-windows-audit-policy-by-using-group-policy"></a>그룹 정책을 사용 하 여 Windows 감사 정책 설정  
그룹 정책을 사용 하 여 감사 정책을 설정 하려면 아래에 있는 적절 한 감사 범주를 구성할 **컴퓨터 구성 보안 설정을 감사 정책** (예를 들어 로컬 그룹 정책 편집기에서 (gpedit.msc)에 대 한 다음 스크린샷 참조). 각 감사 정책 범주에 사용할 수 **성공**, **오류**, 또는 **성공** 및 오류 이벤트 합니다.  
  
![광고를 모니터링합니다.](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_6.gif)  
  
로컬 그룹 정책 또는 Active Directory를 사용 하 여 고급 감사 정책 설정할 수 있습니다. 감사 정책을 고급 설정 하려면 아래에 있는 적절 한 하위 범주를 구성 **컴퓨터 구성 보안 Settings\Advanced 감사 정책** (예를 들어 로컬 그룹 정책 편집기에서 (gpedit.msc)에 대 한 다음 스크린샷 참조). 각 감사 정책을 하위 범주를 사용할 수 **성공**, **오류**, 또는 **성공** 및 **오류** 이벤트 합니다.  
  
![광고를 모니터링합니다.](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_7.gif)  
  
#### <a name="setting-windows-audit-policy-using-auditpolexe"></a>Auditpol.exe를 사용 하 여 Windows 감사 정책 설정  
Windows Server 2008 및 Windows Vista에 (Windows 감사 정책 설정)를 Auditpol.exe 도입 되었습니다. 처음에 auditpol.exe 감사 정책을 고급 설정 하는 데 사용 될 수 있지만 그룹 정책을 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008, Windows 8 및 Windows 7에서 사용할 수 있습니다.  
  
Auditpol.exe 명령줄 유틸리티입니다. 구문을 다음과 같습니다.  
  
**auditpol /set / < 범주 | 하위 범주 >:<audit category> / < 성공 | 오류: > / < 사용 하도록 설정 | 사용 안 함 >**  
  
Auditpol.exe 구문 예:  
  
**auditpol /subcategory 설정 /: "사용자 계정 관리" /success:enable /failure:enable**  
  
**auditpol /subcategory 설정 /: "로그온" /success:enable /failure:enable**  
  
**auditpol /subcategory 설정 /: "IPSEC 주 모드" /failure:enable**  
  
> [!NOTE]  
> Auditpol.exe 감사 정책 고급 로컬 설정합니다. 로컬 정책 충돌 Active Directory 또는 로컬 그룹 정책, 그룹 정책 설정을 auditpol.exe 설정을 통해 일반적으로 우선 합니다. 여러 하나 또는 여러 개의 로컬 정책 충돌 존재 (즉, 대체) 정책을 하나만 우선 합니다. 감사 정책 병합 하지 됩니다.  
  
#### <a name="scripting-auditpol"></a>스크립팅 Auditpol  
Microsoft는 제공는 [스크립트 샘플](https://support.microsoft.com/kb/921469) 스크립트 각 auditpol.exe 명령에서 수동으로 입력 하는 대신 사용 하 여 감사 정책을 고급 설정 하려면 관리자입니다.  
  
**참고** auditpol.exe는 반면 그룹 정책 항상 정확 하 게 설정 된 모든 감사 정책 상태를 보고 하지는 않습니다. 참조 [Windows 7 및 Windows 2008 r 2의 실제 감사 정책 가져오는](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) 에 대 한 자세한 내용은 합니다.  
  
#### <a name="other-auditpol-commands"></a>다른 Auditpol 명령  
Auditpol.exe 저장 하 고 로컬 감사 정책 복원 하 고 다른 감사 관련 된 명령 볼 사용할 수 있습니다. 다음은 다른 **auditpol** 명령을 합니다.  
  
**auditpol 지우기/** -선택을 취소 하 고 로컬 감사 정책 초기화를 사용  
  
**auditpol 차례로/파일:<filename> ** -현재 로컬 감사 정책 이진 파일 백업에 사용  
  
**auditpol /restore /file:<filename> ** -로컬 감사 정책에 이전에 저장 된 감사 정책 파일을 가져오려면 사용  
  
**auditpol / < 가져오거나 설정 > /option:<CrashOnAuditFail> / < 사용/사용 안 함 >** -하면 즉시 중지 시스템이 감사 정책 설정을 사용 하는 경우 (중지와: C0000244 메시지 {실패 감사}) 보안 감사 어떤 이유로 기록 될 수 없는 경우입니다. 일반적으로, 이벤트 보안 감사 로그 꽉 보안 로그 지정 된 보존 방법이 때 로그인에 실패 **이벤트 덮어쓰지 않음** 또는 **매일 이벤트 덮어씁니다**합니다. 일반적으로 보안 로그 로깅는 더 높은 보증 해야 하는 환경으로 활성화만 됩니다. 를 사용 하도록 설정 관리자 보안 로그 크기 시청 밀접 하 고 필요에 따라 로그 회전 해야 합니다. 또한 설정할 수 있습니다 그룹 정책을 사용 하 여 보안 옵션을 수정 하 여 **감사: 시스템 보안 감사 로그에 없는 경우 즉시 종료** (기본 = 사용 안 함).  
  
**Auditpol / < 가져오거나 설정 > /option:<AuditBaseObjects> / < 사용/사용 안 함 >** -이 감사 정책 설정을 글로벌 시스템 개체의 액세스를 감사 여부를 결정 합니다. 이 정책이 옵션을 사용 하면 시스템 개체 등 뮤텍스에, 이벤트, 세마포와 DOS 디바이스를 기본 시스템 액세스 제어 목록 (SACL) 만들 수 있습니다. 대부분의 관리자는 전 세계 시스템 개체 너무 "번거롭고" 되도록 감사 것이 좋습니다 한 시작 되는 악성 해킹과 의심 되는 경우 합니다. 명명된 개체만 SACL 제공 됩니다. 감사 개체 access 감사 정책 (또는 커널 개체 감사 하위 범주) 함께 사용 하면 이러한 시스템에 대 한 액세스 감사 됩니다. 이 보안 설정을 구성할 때 변경 하지 사항을 적용 Windows를 다시 시작 해야 합니다. 이 정책 설정할 수도 있습니다 그룹 정책을 사용 하 여 보안 옵션 감사 액세스 글로벌 시스템 개체 수정 하 여 (기본 = 사용 안 함).  
  
**auditpol / < 가져오거나 설정 > /option:<AuditBaseDirectories> / < 사용/사용 안 함 >** -이 감사 정책 설정을 지정 명명된 커널 개체 (뮤텍스 세마포 등)을 만들 때 Sacl 제공 될 합니다. AuditBaseDirectories는 AuditBaseObjects 개체 다른 개체를 포함할 수 없는 영향을 동안 컨테이너 개체를 영향을 줍니다.  
  
**Auditpol / < 가져오거나 설정 > /option:<FullPrivilegeAuditing> / < 사용/사용 안 함 >** -  
  
클라이언트 한 경우 이벤트를 생성 되는지를 사용자 보안 토큰에 할당 되어 더 이러한 권한은이 감사 정책 설정을 지정: AssignPrimaryTokenPrivilege, AuditPrivilege, BackupPrivilege, CreateTokenPrivilege, DebugPrivilege, EnableDelegationPrivilege, ImpersonatePrivilege, LoadDriverPrivilege, RestorePrivilege, SecurityPrivilege, SystemEnvironmentPrivilege, TakeOwnershipPrivilege, 및 TcbPrivilege 합니다. 이 옵션을 사용할 수 없는 경우 (기본 = 사용 안 함)를 BackupPrivilege 및 RestorePrivilege 권한을 기록 되지 않습니다. 이 옵션을 사용 하면 작업을 백업 하는 동안 (초 이벤트 수백 때때로) 보안 로그를 매우 번거롭고 만들 수 있습니다. 이 정책 설정할 수도 있습니다 그룹 정책을 사용 하 여 보안 옵션을 수정 하 여 **감사: 사용 백업 및 복원 권한 감사**합니다.  
  
> [!NOTE]  
> 여기에 제공 된 일부 정보는 Microsoft에서 찍은 [감사 옵션 종류](https://msdn.microsoft.com/library/dd973862(prot.20).aspx) Microsoft SCM 도구입니다.  
  
### <a name="enforcing-traditional-auditing-or-advanced-auditing"></a>기존 감사 또는 고급 감사 적용  
Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 및 Windows Vista에서 관리자 9 일반적인 범주를 사용 하도록 설정 하거나 하위 범주를 사용 하도록 선택할 수 있습니다. 각 Windows 시스템 변경 해야 하는 이진 선택은 합니다. 주요 범주를 사용할 수 또는 둘 다에서 subcategoriesit 수 없습니다.  
  
레거시 일반적인 범주 정책 덮어쓰지 감사 정책 하위 범주를 방지 하려면 설정 해야는 **힘 감사 정책 범주의 설정 (Windows Vista 이상) 감사 정책 범주 설정을 재정의 하려면** 정책 설정을 아래에 있는 **컴퓨터 구성 보안 로컬 보안 옵션**합니다.  
  
하위 범주 사용 하도록 설정 되어 9 주요 범주 대신 구성 하는 것이 좋습니다. 이 설정 해야 하 그룹 정책 설정을 (감사 범주 재정의 하려면 하위 범주를 허용)를 함께 감사 정책을 원하는 다른 하위 범주를 구성 합니다.  
  
하위 범주 감사 그룹 정책을 명령줄 프로그램, auditpol.exe를 포함 한 몇 가지 방법을 사용 하 여 구성할 수 있습니다.  
  
감사 Windows에 대 한 자세한 내용은 다음 문서를 참조 하세요.  
  
-   [Windows에서 7 및 Windows Server 2008 R2 감사 고급 보안](https://social.technet.microsoft.com/wiki/contents/articles/advanced-security-auditing-in-windows-7-and-windows-server-2008-r2.aspx)  
  
-   [감사 및 Windows server 2008 준수](https://technet.microsoft.com/magazine/2008.03.auditing.aspx)  
  
-   [그룹 정책을 사용 하 여 세부 보안 감사 Windows Vista 및 Windows Server 2008 기반 컴퓨터에서 도메인 Windows Server 2008, Windows Server 2003 도메인 또는 Windows 2000 도메인에 대 한 설정을 구성 하는 방법](https://support.microsoft.com/kb/921469)  
  
-   [고급 보안 감사 정책 Step-by-Step 가이드](https://technet.microsoft.com/library/dd408940(WS.10).aspx)  
  


