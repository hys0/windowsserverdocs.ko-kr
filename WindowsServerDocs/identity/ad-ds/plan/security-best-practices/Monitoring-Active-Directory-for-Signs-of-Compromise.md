---
ms.assetid: a7ef2fba-b05c-4be2-93b2-b9456244c3ad
title: 손상 징후에 대한 Active Directory 모니터링
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 40d0d06f8d6d25c2c1dbf4662d3296a996d22055
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882944"
---
# <a name="monitoring-active-directory-for-signs-of-compromise"></a>손상 징후에 대한 Active Directory 모니터링

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*법률 숫자 5: 영원한 보안의 경우* - [10 immutable Laws of Security 관리](https://technet.microsoft.com/library/cc722488.aspx)  
  
시스템을 모니터링 하는 견고한 이벤트 로그에는 모든 보안 Active Directory 디자인의 중요 한 부분입니다. 많은 컴퓨터 보안 손상은 검색할 수 없습니다 초기 이벤트는 교착 상태가 발생 된 적절 한 이벤트 로그 모니터링 및 경고를 실행 하는 경우. 독립적인 보고서이 결론 지원 되는 시간입니다. 예를 들어는 [2009 Verizon 데이터 위반 보고서](http://www.verizonbusiness.com/resources/security/reports/2009_databreach_rp.pdf) 상태:  
  
"이벤트 모니터링 및 로그 분석의 명백한 ineffectiveness 계속 다소는 enigma 수 있습니다. 검색에 대 한 영업 기회는 있습니다. 수 사관 나와 피해자의 66%에 해당 로그를 검색할 보안 결점은 있었던 같은 리소스를 분석에 더 노력 내에서 사용할 수 있는 충분 한 증거가 있음을. "  
  
이 처럼 사용 가능한 이벤트 로그를 모니터링 합니다. 대부분의 회사 보안 방어 계획 일관성 있는 약점 유지 됩니다. [2012 Verizon 데이터 노출 보고서](http://www.verizonbusiness.com/resources/reports/rp_data-breach-investigations-report-2012_en_xg.pdf) 발견 느끼지 몇 주를 침해의 85%를 진행 하는 경우에 교착 상태가 발생의 84%의 이벤트 로그에 위반의 증거를 했습니다.  
  
## <a name="windows-audit-policy"></a>Windows 감사 정책

Microsoft 공식 기업 지원 블로그에 대 한 링크는 다음과 같습니다. 조언, 지침 및 권장 되는 감사에 대 한 Active Directory 인프라의 보안 강화에 도움이 되 고 감사 정책을 설계할 때 중요 한 리소스는 이러한 블로그 콘텐츠를 제공 합니다.  
  
* [Magic은 전역 개체 액세스 감사](http://blogs.technet.com/b/askds/archive/2011/03/10/global-object-access-auditing-is-magic.aspx) -고급 감사 정책 구성에 추가 된 Windows 7 및 Windows Server 2008 R2 수 있게 해 주는 어떤 유형의 데이터가 하려는 쉽게 감사 하 고 스크립트 및 auditpol.exe 하지 기간이 설정 이라고 하는 제어 메커니즘에 설명 합니다.  
* [Windows 2008에서 변경 된 감사 소개](http://blogs.technet.com/b/askds/archive/2007/10/19/introducing-auditing-changes-in-windows-2008.aspx) -Windows Server 2008에서 감사 변경 사항을 소개 합니다.  
* [Vista 및 2008에 대 한 감사 트릭 냉각](http://blogs.technet.com/b/askds/archive/2007/11/16/cool-auditing-tricks-in-vista-and-2008.aspx) -문제 해결 하거나 사용자 환경에서 일어나는 표시에 사용할 수 있는 Windows Server 2008 및 Windows Vista의 흥미로운 감사 기능에 설명 합니다.  
* [Windows Server 2008 및 Windows Vista의 감사에 대 한 원스톱 상점](http://blogs.technet.com/b/askds/archive/2008/03/27/one-stop-shop-for-auditing-in-windows-server-2008-and-windows-vista.aspx) -컴파일 감사 기능 및 Windows Server 2008 및 Windows Vista에 포함 된 정보를 포함 합니다.  
  
다음 링크는 Windows Server 2008에서 감사 향상 된 Windows 8 및 Windows Server 2012에서 감사 하는 Windows에 대 한 정보 및 AD DS에 대 한 정보를 제공 합니다.  
  
* [보안 감사의 새로운 기능 이란](https://technet.microsoft.com/library/hh849638.aspx) -새로운 보안 감사 Windows 8 및 Windows Server 2012의 기능에 대해 간략하게 설명 합니다.  
* [AD DS 감사 단계별 가이드](https://technet.microsoft.com/library/a9c25483-89e2-4202-881c-ea8e02b4b2a5.aspx) -Windows Server 2008의 새로운 Active Directory 도메인 서비스 (AD DS) 감사 기능에 설명 합니다. 이 새로운 기능을 구현 하는 절차를 제공 합니다.  
  
### <a name="windows-audit-categories"></a>Windows 감사 범주

Windows Vista 및 Windows Server 2008 이전의 Windows는 이벤트 로그 감사 정책 범주를 9 개 밖에 있었습니다.  
  
* 계정 로그온 이벤트  
* 계정 관리  
* 디렉터리 서비스 액세스  
* 로그온 이벤트  
* 개체 액세스  
* 정책 변경  
* 권한 사용  
* 프로세스 추적  
* 시스템 이벤트  
  
이러한 9 개의 일반적인 감사 범주에는 감사 정책을 구성합니다. 성공, 실패 또는 성공 및 실패에 대 한 각 감사 정책 범주를 사용할 수 있는 이벤트입니다. 해당 설명을 보려면 다음 섹션에 포함 됩니다.  
  
#### <a name="audit-policy-category-descriptions"></a>감사 정책 범주 설명  
감사 정책 범주는 다음과 같은 이벤트 로그 메시지 유형을 사용 하도록 설정 합니다.  
  
##### <a name="audit-account-logon-events"></a>계정 로그온 이벤트 감사  
다른 컴퓨터 계정을 확인 하는 데 사용 되는 한 컴퓨터에서 로그 오프 하거나 로그온 하는 보안 주체 (예: 사용자, 컴퓨터 또는 서비스 계정)의 각 인스턴스를 보고 합니다. 계정 로그온 이벤트는 한 도메인 보안 주체 계정을 도메인 컨트롤러에서 인증 될 때 생성 됩니다. 로컬 컴퓨터에서 로컬 사용자의 인증의 로컬 보안 로그에 기록 된 로그온 이벤트를 생성 합니다. 계정을 로그 오프 이벤트가 기록 됩니다.  
  
이 범주는 많은 생성 "노이즈" Windows 로그온 계정에 끊임없이 되 고 로컬 및 원격 컴퓨터에서 비즈니스의 일반적인 과정입니다. 그러나 모든 보안 계획 성공 및 실패 감사 범주에 속하는이 포함 되어야 합니다.  
  
##### <a name="audit-account-management"></a>계정 관리 감사  
이 감사 설정은 사용자 및 그룹의 관리를 추적할지 여부를 결정 합니다. 예를 들어, 사용자 및 그룹 추적 해야 사용자 또는 컴퓨터 계정, 보안 그룹 또는 메일 그룹을 생성, 변경 또는 삭제 하는 경우 사용자 또는 컴퓨터 계정 이름이 바뀌었거나, 비활성화 되었거나, 그렇지 않으면 또는 사용자 또는 컴퓨터 암호가 변경 될 때입니다. 사용자 또는 그룹에 추가 또는 다른 그룹에서 제거 된 이벤트를 생성할 수 있습니다.  
  
##### <a name="audit-directory-service-access"></a>디렉터리 서비스 액세스 감사  

이 정책 설정은 있는지 여부를 Active Directory 개체에 대 한 보안 주체 액세스를 감사 하는 자체 지정한 시스템 액세스 제어 목록 (SACL)을 결정 합니다. 일반적으로이 범주에 도메인 컨트롤러에만 설정 해야 합니다. 이 설정을 사용 하면 "노이즈". 많이 생성  
  
##### <a name="audit-logon-events"></a>로그온 이벤트 감사  
로컬 보안 주체는 로컬 컴퓨터에서 인증 하는 경우 로그온 이벤트가 생성 됩니다. 로그온 이벤트는 로컬 컴퓨터에서 발생 하는 도메인 로그온을 기록 합니다. 계정 로그 오프 이벤트 생성 되지 않습니다. 로그온 이벤트를 사용 하면 다양 한 "노이즈"를 생성 하지만 모든 보안 감사 계획에서 기본적으로 활성화 되어야 합니다.  
  
##### <a name="audit-object-access"></a>개체 액세스 감사  
개체 액세스 감사 사용 된 후 정의 된 개체 (예, Opened, 읽기, 이름이 바뀐, 삭제 됨 또는 닫힘)에 액세스할 때 이벤트를 생성할 수 있습니다. 주 감사 범주를 활성화 한 후 관리자는 설정한 감사 개체 정의 개별적으로 해야 합니다. 많은 Windows 시스템 개체 전에 관리자가 정의 된 이벤트를 생성 하려면 일반적으로 예정이 범주를 사용 하도록 설정 되므로 사용을 감사 하는 함께 제공 됩니다.  
  
이 범주는 매우 "시끄러운" 이며 각 개체 액세스에 대 한 5-10 개의 이벤트를 생성 합니다. 유용한 정보를 얻을 수 개체 감사 새 관리자를 위한 어려울 수 있습니다. 필요할 때만 설정 해야 합니다.  
  
##### <a name="auditing-policy-change"></a>정책 변경 감사  
이 정책 설정은 사용자 권한 할당 정책, Windows 방화벽 정책, 신뢰할 수 있는 정책 또는 감사 정책의 변경에 대 한 변경의 모든 이벤트를 감사할지 여부를 결정 합니다. 이 범주는 모든 컴퓨터에서 사용할 수 있어야 합니다. 거의 노이즈를 생성합니다.  
  
##### <a name="audit-privilege-use"></a>권한 사용 감사  

사용자 권한 및 사용 권한 (예를 들어 일괄 처리 작업 및 운영 체제의 일부로 작동으로 로그온) Windows에서 여러 가지가 있습니다. 이 정책 설정은 사용자 권한이 나 권한을 검토 하 여 각 인스턴스의 보안 주체를 감사 여부를 결정 합니다. 이 범주 결과 "노이즈" 하지만 많은 보안 주체 계정 상승 된 권한을 사용 하 여 추적에 유용 합니다.  
  
##### <a name="audit-process-tracking"></a>프로세스 추적 감사  
이 정책 설정은 감사 프로그램 활성화, 프로세스 종료, 핸들 복제 및 간접 개체 액세스와 같은 이벤트에 대 한 정보를 추적 하는 자세한 프로세스를 결정 합니다. 악의적인 사용자와 사용할 프로그램을 추적 하기 위한 것이 유용 합니다.  
  
프로세스 추적 감사를 사용 하면 일반적으로 설정 되어 많은 수의 이벤트를 생성 **감사 안**합니다. 그러나이 설정 된 시간과 시작 되는 프로세스의 자세한 로그에서 문제는 대응 하는 동안 매우 유익 하 게 제공할 수 있습니다. 도메인 컨트롤러와 다른 단일 역할 인프라 서버에 대 한이 범주에는 항상 안전 하 게 설정할 수 있습니다. 단일 역할 서버에서 트래픽을 업무는 일반적인 과정 추적 많은 프로세스를 생성 하지 않습니다. 따라서 이벤트를 캡처하기 위해 권한이 없는 경우에 사용할 수 있습니다.  
  
##### <a name="system-events-audit"></a>시스템 이벤트 감사  

시스템 이벤트는 일반 포괄적인 범주 거의 컴퓨터, 해당 시스템 보안 또는 보안 로그에 영향을 주는 다양 한 이벤트를 등록 하는 중입니다. 컴퓨터를 종료 하 고 다시 시작, 정전, 시스템 시간 변경 내용, 인증 패키지 초기화, 감사 로그 개 간지 사이, 가장 문제 및 다른 일반 이벤트의 호스트에 대 한 이벤트 포함 됩니다. 일반적으로이 감사 범주를 사용 하면 "노이즈" 많은 생성 하지만 적 설정 하지 않으면 권장 하기 어렵다는 것 충분 한 매우 유용한 이벤트를 생성 합니다.  
  
#### <a name="advanced-audit-policies"></a>고급 감사 정책

Windows Vista 및 Windows Server 2008 부터는 Microsoft 각 주 감사 범주 아래의 하위 범주를 만들어 이벤트 로그 범주 선택 항목을 가능 하는 방법을 향상 되었습니다. 하위 범주를 주요 범주를 사용 하 여 그렇지 않으면 했다는 것 보다 훨씬 더 세밀 하 게 감사를 허용 합니다. 하위 범주를 사용 하 여 특정 주 범주의 일부만 사용 하도록 설정 하 고는 사용 되지 않은 없는 생성 이벤트를 건너뛸 수 있습니다. 성공, 실패 또는 성공 및 실패 이벤트에 대한 감사 정책 하위 범주를 각각 설정할 수 있습니다.  
  
모든 사용할 수 있는 감사 하위 범주를 나열 하려면 그룹 정책 개체에서 고급 감사 정책 컨테이너를 검토 하거나 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008, Windows 8, Windows 7 또는 Windows Vista를 실행 하는 컴퓨터에서 명령 프롬프트에서 다음을 입력 합니다.  
  
`auditpol /list /subcategory:\*`
  
Windows Server 2012, Windows Server 2008 R2 또는 Windows 2008을 실행 하는 컴퓨터에 현재 구성 된 감사 하위 범주의 목록을 가져오려면 다음을 입력 합니다.  
  
`auditpol /get /category:\*`
  
다음 스크린 샷에서 현재 감사 정책을 나열 auditpol.exe의 예를 보여줍니다.  
  
![AD 모니터링](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_5.gif)  
  
> [!NOTE]  
> Auditpol.exe 없지만 그룹 정책 설정 된 모든 감사 정책 상태를 항상 정확 하 게 보고 하지 않습니다. 참조 [Windows 7 및 2008 r 2에서 실제 감사 정책 가져오기](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) 대 한 자세한 내용은 합니다.  
  
각 기본 범주에는 여러 하위 범주에 있습니다. 다음은 범주, 해당 하위 범주 및 해당 기능에 대 한 설명을의 목록입니다.  
  
### <a name="auditing-subcategories-descriptions"></a>감사 하위 범주 설명  
감사 정책 하위 범주는 다음 이벤트 로그 메시지 유형을 사용 합니다.  
  
#### <a name="account-logon"></a>계정 로그온  
  
##### <a name="credential-validation"></a>자격 증명 유효성 검사  
이 하위 범주에 대 한 사용자 계정 로그온 요청을 제출 하는 자격 증명 유효성 검사 테스트의 결과 보고 합니다. 자격 증명에 대 한 권한이 있는 컴퓨터에서 이러한 이벤트가 발생 합니다. 반면 로컬 계정의 경우 로컬 컴퓨터는 신뢰할 수 있는 도메인 계정에 대 한 도메인 컨트롤러가 신뢰할 수입니다.  
  
도메인 환경에서 대부분의 경우 계정 로그온 이벤트는 도메인 계정에 대 한 권한이 있는 도메인 컨트롤러의 보안 로그에 기록 됩니다. 그러나 이러한 이벤트는 로컬 계정을 사용 하 여 로그온 할 때 조직에서 다른 컴퓨터에서 발생할 수 있습니다.  
  
##### <a name="kerberos-service-ticket-operations"></a>Kerberos 서비스 티켓 작업  
이 하위 도메인 계정에 대 한 권한이 있는 도메인 컨트롤러에서 Kerberos 티켓 요청 프로세스에 의해 생성 된 이벤트를 보고 합니다.  
  
##### <a name="kerberos-authentication-service"></a>Kerberos 인증 서비스  
이 하위 Kerberos 인증 서비스에 의해 생성 된 이벤트를 보고 합니다. 자격 증명에 대 한 권한이 있는 컴퓨터에서 이러한 이벤트가 발생 합니다.  
  
##### <a name="other-account-logon-events"></a>기타 계정 로그온 이벤트  
이 하위 자격 증명 사용자 계정 로그온 요청을 위해 제출 하는 자격 증명 유효성 검사 또는 Kerberos 티켓에 대 한 응답으로 발생 하는 이벤트를 보고 합니다. 자격 증명에 대 한 권한이 있는 컴퓨터에서 이러한 이벤트가 발생 합니다. 반면 로컬 계정의 경우 로컬 컴퓨터는 신뢰할 수 있는 도메인 계정에 대 한 도메인 컨트롤러가 신뢰할 수입니다.  
  
도메인 환경에서 대부분 계정 로그온 이벤트는 도메인 계정에 대 한 권한이 있는 도메인 컨트롤러의 보안 로그에 기록 됩니다. 그러나 이러한 이벤트는 로컬 계정을 사용 하 여 로그온 할 때 조직에서 다른 컴퓨터에서 발생할 수 있습니다. 예제는 다음과 같습니다.  
  
* 원격 데스크톱 서비스 세션 연결 끊기  
* 새 원격 데스크톱 서비스 세션  
* 잠금 및 워크스테이션 잠금 해제  
* 화면 보호기를 호출합니다.  
* 화면 보호기를 해제합니다.  
* Kerberos 검색 재생 공격을 동일한 정보 함께 Kerberos 요청을 두 번 수신는  
* 사용자 또는 컴퓨터 계정에 부여 된 무선 네트워크에 대 한 액세스  
* 액세스 유선 802.1 x 네트워크 사용자 또는 컴퓨터 계정에 부여  
  
#### <a name="account-management"></a>계정 관리  
  
##### <a name="user-account-management"></a>사용자 계정 관리  
이 하위 보고서의 각 이벤트의 사용자 계정 생성, 변경 또는 삭제와 같은 사용자 계정 관리 사용자 계정 이름이 바뀌었거나, 비활성화 되었거나, 그렇지 않으면 또는 암호를 설정 하거나 변경할 수 있습니다. 이 감사 정책 설정을 사용 하는 경우 관리자에 추적 이벤트를 악의적이 고, 실수로 인 한 권한 있는 사용자 계정 만들 수 있습니다.  
  
##### <a name="computer-account-management"></a>컴퓨터 계정 관리  
이 하위 때 컴퓨터 계정을 생성, 변경, 삭제, 변경, 비활성화 되거나 활성화 같은 컴퓨터 계정 관리의 각 이벤트를 보고 합니다.  
  
##### <a name="security-group-management"></a>보안 그룹 관리  
이 하위 멤버를 추가 또는 보안 그룹에서 제거할 때 또는 보안 그룹을 생성, 변경 또는 삭제와 같은 보안 그룹 관리의 각 이벤트를 보고 합니다. 이 감사 정책 설정을 사용 하는 경우 관리자에 추적 이벤트를 악의적이 고, 실수로 인 한 권한 있는 보안 그룹 계정 만들 수 있습니다.  
  
##### <a name="distribution-group-management"></a>메일 그룹 관리  
이 하위 멤버를 추가 또는 메일 그룹에서 제거할 때 또는 메일 그룹을 생성, 변경 또는 삭제 등의 메일 그룹 관리의 각 이벤트를 보고 합니다. 이 감사 정책 설정을 사용 하는 경우 관리자는 악의적이 고, 실수로 인 한 권한 있는 그룹 계정 생성을 검색 이벤트 추적 수 있습니다.  
  
##### <a name="application-group-management"></a>응용 프로그램 그룹 관리  
이 하위 멤버를 추가 또는 응용 프로그램 그룹에서 제거할 때 또는 응용 프로그램 그룹 생성, 변경 또는 삭제와 같은 컴퓨터에서 응용 프로그램 그룹 관리의 각 이벤트를 보고 합니다. 이 감사 정책 설정을 사용 하는 경우 관리자는 추적 이벤트를 응용 프로그램 그룹 계정의 악의적이 고, 실수로 인 한 권한 있는 생성 수 있습니다.  
  
##### <a name="other-account-management-events"></a>다른 계정 관리 이벤트  
이 하위 다른 계정 관리 이벤트를 보고합니다.  
  
#### <a name="detailed-process-tracking"></a>상세한 프로세스 추적  
  
##### <a name="process-creation"></a>프로세스 만들기  
이 하위 프로세스를 만들고 프로그램을 만든 사용자의 이름을 보고 합니다.  
  
##### <a name="process-termination"></a>프로세스 종료  
이 하위 프로세스가 종료 될 때 보고 합니다.  
  
##### <a name="dpapi-activity"></a>DPAPI 활동  
이 하위 암호화 하거나 암호 해독 데이터 보호 응용 프로그래밍 인터페이스 (DPAPI)로 호출을 보고 합니다. DPAPI는 저장 된 암호와 같은 기밀 정보 및 키 정보를 보호 하는 데 사용 됩니다.  
  
##### <a name="rpc-events"></a>RPC 이벤트  
이 하위 보고서 원격 프로시저 호출 (RPC) 연결 이벤트입니다.  
  
#### <a name="directory-service-access"></a>디렉터리 서비스 액세스  
  
##### <a name="directory-service-access"></a>디렉터리 서비스 액세스  
이 하위 범주에는 AD DS 개체에 액세스할 때 보고 합니다. 구성 된 Sacl 유일한 개체는 되며, 생성 된 유일한 SACL 항목을 일치 하는 방식으로 액세스할 때 감사 이벤트를 발생 합니다. 이러한 이벤트는 이전 버전의 Windows Server의 디렉터리 서비스 액세스 이벤트와 유사 합니다. 이 하위 도메인 컨트롤러에만 적용 됩니다.  
  
##### <a name="directory-service-changes"></a>디렉터리 서비스 변경  
이 하위 AD DS에서 개체의 변경 내용을 보고 합니다. 보고 되는 변경 유형에 만들기, 수정, 이동 및 개체에 대해 수행 되는 작업이 삭제 취소 디렉터리 서비스 변경 감사, 적절 한 경우 변경 된 개체의 변경 된 속성의 이전 및 새 값을 나타냅니다. Sacl 인 개체만 되며, 생성 된 유일한 SACL 항목의 일치 하는 방식으로 액세스할 때 감사 이벤트를 발생 합니다. 일부 개체 및 속성 스키마의 개체 클래스에 대 한 설정으로 인해 생성 되는 감사 이벤트를 발생 하지 않습니다. 이 하위 도메인 컨트롤러에만 적용 됩니다.  
  
##### <a name="directory-service-replication"></a>디렉터리 서비스 복제  
이 하위 두 도메인 컨트롤러 간의 복제가 시작 되 고 종료 하는 경우를 보고 합니다.  
  
##### <a name="detailed-directory-service-replication"></a>세부 디렉터리 서비스 복제  
이 하위 도메인 컨트롤러 간에 복제 하는 정보에 대 한 자세한 정보를 보고 합니다. 이러한 이벤트는 볼륨에서 매우 커질 수 있습니다.  
  
#### <a name="logonlogoff"></a>로그온/로그 오프  
  
##### <a name="logon"></a>로그온  
이 하위 시스템에 로그온 하는 사용자가 시도 보고 합니다. 액세스 되는 컴퓨터에서 이러한 이벤트가 발생 합니다. 대화형 로그온에 대 한 이러한 이벤트의 생성에 로그온 하는 컴퓨터에서 발생 합니다. 공유에 액세스 하는 네트워크 로그온 완료 되 면 하는 경우 이러한 이벤트 액세스 되는 리소스를 호스팅하는 컴퓨터를 생성 합니다. 이 설정은 하도록 구성 된 경우 **감사 안**, 은 사용자에 액세스 또는 조직의 컴퓨터에 액세스 하려고 했습니다. 확인할 어렵거나 합니다.  
  
##### <a name="network-policy-server"></a>네트워크 정책 서버  
이 하위 RADIUS (IAS) 및 네트워크 액세스 보호 (NAP) 사용자 액세스 요청에 의해 생성 된 이벤트를 보고 합니다. 이러한 요청 수 **부여**, **거부**, **취소**, **격리**, **잠금**, 및 **잠금 해제**합니다. 이 설정은 감사 NPS 및 IAS 서버에 있는 레코드가 중간 또는 높은 볼륨에서 발생 합니다.  
  
##### <a name="ipsec-main-mode"></a>IPsec 주 모드  
이 하위 주 모드 협상 하는 동안 인터넷 키 교환 (IKE) 프로토콜 및 인증 된 인터넷 프로토콜 (AuthIP)의 결과 보고합니다.  
  
##### <a name="ipsec-extended-mode"></a>IPsec 확장 모드  
이 하위 확장 모드 협상 AuthIP의 결과 보고합니다.  
  
##### <a name="other-logonlogoff-events"></a>다른 로그온/로그 오프 이벤트  
이 하위 다른 로그온 및 원격 데스크톱 서비스 세션 연결을 끊고 다시 연결 되 면 실행을 사용 하 여 다른 계정으로 프로세스를 실행 하 고 잠금 및 워크스테이션을 잠금 해제와 같은 로그 오프 관련 이벤트를 보고 합니다.  
  
##### <a name="logoff"></a>로그 오프  
이 하위 시스템 사용자가 로그를 보고 합니다. 액세스 되는 컴퓨터에서 이러한 이벤트가 발생 합니다. 대화형 로그온에 대 한 이러한 이벤트의 생성에 로그온 하는 컴퓨터에서 발생 합니다. 공유에 액세스 하는 네트워크 로그온 완료 되 면 하는 경우 이러한 이벤트 액세스 되는 리소스를 호스팅하는 컴퓨터를 생성 합니다. 이 설정은 하도록 구성 된 경우 **감사 안**, 은 사용자에 액세스 또는 조직의 컴퓨터에 액세스 하려고 했습니다. 확인할 어렵거나 합니다.  
  
##### <a name="account-lockout"></a>계정 잠금  
이 하위 범주에는 너무 많은 실패 한 로그온 시도 결과로 사용자의 계정이 잠겨 때 보고 합니다.  
  
##### <a name="ipsec-quick-mode"></a>IPsec 빠른 모드  
이 하위 빠른 모드 협상 IKE 프로토콜 및 AuthIP의 결과 보고합니다.  
  
##### <a name="special-logon"></a>특별 한 로그온  
이 하위 특별 한 로그온 사용 될 때 보고 합니다. 특별 한 로그온은 관리자가 그와 동등한 권한이 않았으며 프로세스를 더 높은 수준으로 권한을 상승에 사용할 수 있는 로그온입니다.  
  
#### <a name="policy-change"></a>정책 변경  
  
##### <a name="audit-policy-change"></a>정책 변경 감사  
이 하위 SACL 변경 내용을 포함 하는 감사 정책에 대 한 변경 내용을 보고 합니다.  
  
##### <a name="authentication-policy-change"></a>인증 정책 변경  
이 하위 인증 정책에 대 한 변경 내용을 보고합니다.  
  
##### <a name="authorization-policy-change"></a>권한 부여 정책 변경  
이 하위 범주에는 사용 권한 (DACL) 변경 내용을 포함 하 여 권한 부여 정책 변경을 보고 합니다.  
  
##### <a name="mpssvc-rule-level-policy-change"></a>MPSSVC 규칙 수준 정책 변경  
이 하위 Microsoft 보호 서비스 (MPSSVC.exe)에서 사용 하는 정책 규칙의 변경 내용을 보고 합니다. 이 서비스는 Windows 방화벽에 의해 사용 됩니다.  
  
##### <a name="filtering-platform-policy-change"></a>필터링 플랫폼 정책 변경  
이 하위 추가 및 제거의 WFP, 시작 필터를 포함 하 여 개체를 보고 합니다. 이러한 이벤트는 볼륨에서 매우 커질 수 있습니다.  
  
##### <a name="other-policy-change-events"></a>기타 정책 변경 이벤트  
이 하위 다른 형식의 암호화 공급자는 신뢰할 수 있는 플랫폼 모듈 (TPM)의 구성과 같은 보안 정책 변경 내용 보고합니다.  
  
#### <a name="privilege-use"></a>권한 사용  
  
##### <a name="sensitive-privilege-use"></a>중요 한 권한 사용  
이 하위 때 보고 합니다. 사용자 계정 또는 서비스에는 중요 한 권한을 사용 하 여 합니다. 다음 사용자 권한이 포함 하는 중요 한 권한: 운영 체제의 일부로 작동, 파일 및 디렉터리를 백업, 토큰 개체 만들기, 프로그램을 디버깅, 컴퓨터 및 사용자 계정을 위임용으로 신뢰할 수, 보안 감사 생성, 인증 후 클라이언트 가장, 로드 및 언로드 장치 드라이버, 감사 관리 및 보안 로그 사용, 펌웨어 환경 값 수정, 프로세스 수준 토큰 바꾸기 파일 및 디렉터리를 복원 하 고 파일 또는 다른 개체의 소유권을 합니다. 이 하위 감사 이벤트의 대용량을 만들어집니다.  
  
##### <a name="nonsensitive-privilege-use"></a>Nonsensitive 권한 사용  
이 하위 때 보고 합니다. 사용자 계정 또는 서비스 nonsensitive 권한을 사용 합니다. Nonsensitive 권한 다음 사용자 권한이 포함: 신뢰할 수 있는 호출자로 자격 증명 관리자에 액세스, 네트워크에서이 컴퓨터 액세스, 도메인에 워크스테이션 추가, 프로세스에 대 한 메모리 할당량 조정, 로컬 로그온 허용, 원격 데스크톱 서비스를 통한 로그온 허용, 트래버스 검사 무시, 시스템 시간 변경, 페이지 파일 만들기, 전역 개체 만들기, 영구 공유 개체 만들기, 기호화 된 링크를 만들 네트워크에서이 컴퓨터 액세스 거부, 일괄 작업으로 로그온 거부, 서비스로 로그온 거부, 로컬 로그온 거부, 원격 데스크톱 서비스를 통한 로그온 거부, 원격 시스템에서 강제 종료, 프로세스 작업 집합 향상, 예약 우선 순위 증가, 메모리의 페이지 잠금, 일괄 처리 작업으로 로그온, 서비스로 로그온, 개체 레이블 수정 볼륨 유지 관리 작업, 단일 프로세스 프로필, 시스템 성능 프로필을 수행, 도킹 스테이션에서 컴퓨터를 제거, 시스템, 종료 및 디렉터리 서비스 데이터를 동기화 합니다. 이 하위 감사 매우 많은 양의 이벤트 만들어집니다.  
  
##### <a name="other-privilege-use-events"></a>기타 권한 사용 이벤트  
이 보안 정책 설정은 현재 사용 되지 않습니다.  
  
#### <a name="object-access"></a>개체 액세스  
  
##### <a name="file-system"></a>파일 시스템  
이 하위 파일 시스템 개체에 액세스할 때 보고 합니다. Sacl 있는 파일 시스템 개체만 되며, 생성 된 유일한 SACL 항목의 일치 하는 방식으로 액세스할 때 감사 이벤트를 발생 합니다. 자체적으로이 정책 설정은 발생 하지 않습니다 모든 이벤트의 감사 합니다. 파일 시스템 개체에 지정 된 시스템 액세스 제어 목록 (SACL)를 액세스 하는 사용자의 이벤트 감사 것인지를 결정 효과적으로 수행 되려면 감사를 사용 합니다.  
  
개체 액세스 감사를 설정 하도록 구성 된 경우 **성공**, 감사 항목이 생성 됩니다 될 때마다 사용자 지정 된 SACL 포함 된 개체를 액세스 하는 성공적으로 합니다. 이 정책 설정을 하도록 구성 된 경우 **실패**, 감사 항목에는 사용자 지정 된 SACL이 있는 개체에 액세스 하지 못하는 때마다 생성 됩니다.  
  
##### <a name="registry"></a>레지스트리  
이 하위 레지스트리 개체에 액세스 하는 경우를 보고 합니다. Sacl 레지스트리 개체만 되며, 생성 된 유일한 SACL 항목의 일치 하는 방식으로 액세스할 때 감사 이벤트를 발생 합니다. 자체적으로이 정책 설정은 발생 하지 않습니다 모든 이벤트의 감사 합니다.  
  
##### <a name="kernel-object"></a>커널 개체  
이 하위 프로세스와 뮤텍스 같은 커널 개체에 액세스 하는 경우를 보고 합니다. Sacl 커널 개체만 되며, 생성 된 유일한 SACL 항목의 일치 하는 방식으로 액세스할 때 감사 이벤트를 발생 합니다. 일반적으로 커널 개체 AuditBaseObjects 또는 AuditBaseDirectories 감사 옵션을 사용 하는 경우에 Sacl 제공 됩니다.  
  
##### <a name="sam"></a>SAM  
이 하위 범주에는 로컬 보안 계정 관리자 (SAM) 인증 데이터베이스 개체에 액세스할 때 보고 합니다.  
  
##### <a name="certification-services"></a>인증 서비스  
이 하위 인증 서비스 작업을 수행할 때 보고 합니다.  
  
##### <a name="application-generated"></a>생성 된 응용 프로그램  
이 하위 응용 프로그램은 Windows 응용 프로그래밍 인터페이스 (Api)를 감사를 사용 하 여 감사 이벤트를 생성 하려고 할 때 보고 합니다.  
  
##### <a name="handle-manipulation"></a>조작 처리  
이 하위 개체에 대 한 핸들 열리거나 닫힐 때 보고 합니다. Sacl 사용 하 여 개체에만 생성 되며 작업을 시도한 핸들 SACL 항목을 일치 하는 경우에 이러한 이벤트를 발생 합니다. 핸들 조작 이벤트는 해당 개체 액세스 하위 범주 (예, 파일 시스템 또는 레지스트리)에 설정 되는 개체 유형에 생성 됩니다.  
  
##### <a name="file-share"></a>파일 공유  
이 하위 파일 공유에 액세스할 때 보고 합니다. 자체적으로이 정책 설정은 발생 하지 않습니다 모든 이벤트의 감사 합니다. 이벤트에 지정 된 시스템 액세스 제어 목록 (SACL) 파일 공유 개체를 액세스 하는 사용자의 감사 것인지를 결정 효과적으로 수행 되려면 감사를 사용 합니다.  
  
##### <a name="filtering-platform-packet-drop"></a>필터링 플랫폼 패킷 삭제  
이 하위 하 여 Windows WFP (필터링 플랫폼) 패킷을 때 보고 합니다. 이러한 이벤트는 볼륨에서 매우 커질 수 있습니다.  
  
##### <a name="filtering-platform-connection"></a>플랫폼 연결 필터링  
이 하위 연결이 허용 되거나 WFP에 의해 차단 하는 경우를 보고 합니다. 이러한 이벤트는 볼륨에서 높은 수 있습니다.  
  
##### <a name="other-object-access-events"></a>다른 개체 액세스 이벤트  
이 하위 작업 스케줄러 작업 및 COM + 개체와 같은 다른 개체 액세스 관련 이벤트를 보고합니다.  
  
#### <a name="system"></a>시스템  
  
##### <a name="security-state-change"></a>보안 상태 변경  
이 하위 보안 하위 시스템의 시작 및 중지 시기 등 시스템의 보안 상태에서 변경을 보고 합니다.  
  
##### <a name="security-system-extension"></a>보안 시스템 확장  
이 하위 보안 하위 시스템에 의해 인증 패키지와 같은 확장 프로그램 코드의 로드를 보고합니다.  
  
##### <a name="system-integrity"></a>시스템 무결성  
이 하위 보안 하위 시스템의 무결성 위반을 보고합니다.  
  
IPsec 드라이버  
  
이 하위 인터넷 프로토콜 보안 (IPsec) 드라이버의 활동을 보고합니다.  
  
##### <a name="other-system-events"></a>기타 시스템 이벤트  
이 하위 기타 시스템 이벤트를 보고 합니다.  
  
하위 범주 설명에 대 한 자세한 내용은 참조는 [도구 Microsoft Security Compliance Manager](https://technet.microsoft.com/library/cc677002.aspx)합니다.  
  
각 조직은 이전 대상된 범주 및 하위 범주를 검토 하 고 자신의 환경에 가장 적합 하는 것을 사용 하도록 설정 해야 합니다. 변경 내용은 감사 정책으로는 프로덕션 환경에 배포 하기 전에 항상 테스트 해야 합니다.  
  
## <a name="configuring-windows-audit-policy"></a>Windows 감사 정책 구성

Windows 감사 정책은 그룹 정책, auditpol.exe, Api 또는 레지스트리 편집을 사용 하 여 설정할 수 있습니다. 대부분의 회사에 대 한 감사 정책을 구성 하는 데 권장 되는 방법에는 그룹 정책 또는 auditpol.exe입니다. 시스템의 감사 정책 설정 관리자 수준 계정 사용 권한 또는 위임된 된 적절 한 사용 권한이 필요 합니다.  
  
> [!NOTE]  
> **관리 감사 및 보안 로그** 보안 주체에 권한을 부여 해야 (관리자는 기본적으로 함)에 개체 액세스 감사 옵션의 파일, Active Directory 개체 및 레지스트리 키와 같은 개별 리소스를 수정할 수 있도록 합니다.  
  
### <a name="setting-windows-audit-policy-by-using-group-policy"></a>Windows 그룹 정책을 사용 하 여 감사 정책 설정

그룹 정책을 사용 하 여 감사 정책을 설정 하려면 아래에 있는 적절 한 감사 범주로 구성 **컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ 감사 정책** (예제에서 로컬 그룹 정책 편집기 (gpedit.msc)를 보려면 다음 스크린샷 참조). 각 감사 정책 범주에 대해 사용할 수 있는 **성공**, **실패**, 또는 **성공** 및 오류 이벤트입니다.  
  
![AD 모니터링](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_6.gif)  
  
Active Directory 또는 로컬 그룹 정책을 사용 하 여 고급 감사 정책은 설정할 수 있습니다. 고급 감사 정책을 설정 하려면 적절 한 하위 범주 아래에 있는 구성 **컴퓨터 구성 설정 \ 보안 설정 \ 고급 감사 정책** (예제에서 로컬 그룹 정책 편집기 (gpedit.msc)를 보려면 다음 스크린샷 참조). 각 감사 정책 하위 범주에 대해 사용할 수 있는 **성공**, **실패**, 또는 **성공** 및 **실패** 이벤트입니다.  
  
![AD 모니터링](media/Monitoring-Active-Directory-for-Signs-of-Compromise/SAD_7.gif)  
  
### <a name="setting-windows-audit-policy-using-auditpolexe"></a>Auditpol.exe를 사용 하 여 Windows 감사 정책 설정

Auditpol.exe (설정에 대 한 Windows 감사 정책)는 Windows Server 2008 및 Windows Vista에서 도입 되었습니다. 처음에 auditpol.exe 고급 감사 정책 설정에 사용할 수 있지만 그룹 정책 Windows Server 2012, Windows Server 2008 R2 또는 Windows Server 2008, Windows 8 및 Windows 7에서 사용할 수 있습니다.  
  
Auditpol.exe 명령줄 유틸리티입니다. 구문은 다음과 같습니다.  
  
`auditpol /set /<Category|Subcategory>:<audit category> /<success|failure:> /<enable|disable>`
  
Auditpol.exe 구문 예제:  
  
`auditpol /set /subcategory:"user account management" /success:enable /failure:enable`
  
`auditpol /set /subcategory:"logon" /success:enable /failure:enable`
  
`auditpol /set /subcategory:"IPSEC Main Mode" /failure:enable`
  
> [!NOTE]  
> Auditpol.exe 로컬로 고급 감사 정책을 설정합니다. 로컬 정책 Active Directory 또는 로컬 그룹 정책 충돌, 그룹 정책 설정을 일반적으로 auditpol.exe 설정 보다 우선 적용 합니다. 여러 그룹 또는 로컬 정책 충돌이 있는 경우 하나의 정책만 우선 적용 (교체)입니다. 감사 정책을 병합 되지 않습니다.  
  
#### <a name="scripting-auditpol"></a>Auditpol 스크립팅

Microsoft에서 제공 된 [샘플 스크립트](https://support.microsoft.com/kb/921469) 각 auditpol.exe 명령에 직접 입력 하지 않고 스크립트를 사용 하 여 고급 감사 정책 설정 하려는 관리자에 대 한 합니다.  
  
**참고** auditpol.exe 없지만 그룹 정책 항상 정확 하 게 설정 된 모든 감사 정책 상태를 보고 하지는 않습니다. 참조 [Windows 7 및 Windows 2008 r 2에서 실제 감사 정책 가져오기](http://blogs.technet.com/b/askds/archive/2011/03/11/getting-the-effective-audit-policy-in-windows-7-and-2008-r2.aspx) 대 한 자세한 내용은 합니다.  
  
#### <a name="other-auditpol-commands"></a>다른 Auditpol 명령

저장 하 고는 로컬 감사 정책을 복원 하 고 다른 감사 관련된 명령을 볼 Auditpol.exe는 사용할 수 있습니다. 다음은 다른 **auditpol** 명령입니다.  
  
`auditpol /clear` -선택을 취소 하 고 로컬 감사 정책을 다시 설정 하는 데 사용  
  
`auditpol /backup /file:<filename>` -이진 파일에는 현재 로컬 감사 정책을를 백업 하는 데 사용  
  
`auditpol /restore /file:<filename>` -로컬 감사 정책에는 이전에 저장 된 감사 정책 파일을 가져오는 데 사용 합니다.  
  
`auditpol /<get/set> /option:<CrashOnAuditFail> /<enable/disable>` -이 감사 정책 설정을 사용 하면 시스템을 즉시 중지 (STOP을 사용 하 여: C0000244 {감사 실패} 메시지) 보안 감사 하는 경우를 로그할 수 없는 어떤 이유로 든 합니다. 보안 감사 로그가 꽉 차고 보안 로그에 대해 지정 된 보존 메서드는 로그에 이벤트 실패 하는 일반적으로 **이벤트 덮어쓰지 않음** 또는 **이벤트 덮어쓰기**합니다. 일반적으로 로그온 하는 보안 로그를 더 높은 보증 해야 하는 환경에 의해 활성화만 됩니다. 설정 된 경우 관리자가 보안 로그 크기를 시청 고 필요에 따라 로그 회전 밀접 하 게 해야 합니다. 또한 설정할 수 있습니다 그룹 정책 보안 옵션을 수정 하 여 **감사 합니다. 보안 감사를 로그할 수 없는 경우 즉시 시스템 종료** (기본값 = 사용 안 함).  
  
`auditpol /<get/set> /option:<AuditBaseObjects> /<enable/disable>` -이 감사 정책 설정을 글로벌 시스템 개체에 대 한 액세스를 감사 여부를 결정 합니다. 이 정책 옵션을 사용 하면 뮤텍스, 이벤트, 세마포 및 기본 시스템 액세스 제어 목록 (SACL)를 사용 하 여 만들어집니다 DOS 장치 등의 시스템 개체입니다. 대부분의 관리자가 너무 "심하거"를 글로벌 시스템 개체를 감사 하 고 악의적인 해킹 의심 되 면만 로드할 수 있습니다. 명명 된 개체만 SACL이 제공 됩니다. 감사 개체 액세스 감사 정책 (또는 커널 개체 감사 하위 범주)도 사용 하는 경우 이러한 시스템 개체에 대 한 액세스 감사 됩니다. 이 보안 설정을 구성할 때 변경 내용이 적용 되지 않습니다 Windows를 다시 시작 해야 합니다. 이 정책을 설정할 수 있으며 그룹 정책을 사용 하 여 글로벌 시스템 개체에 대 한 액세스 감사 보안 옵션을 수정 하 여 (기본값 = 사용 안 함).  
  
`auditpol /<get/set> /option:<AuditBaseDirectories> /<enable/disable>` -이 감사 정책 설정을 생성 될 때 Sacl이 제공 될 명명 된 커널 개체 (예: 뮤텍스 및 세마포에) 지정 합니다. AuditBaseDirectories는 AuditBaseObjects 다른 개체를 포함할 수 없는 개체를 적용 하는 동안 컨테이너 개체를 영향을 줍니다.  
  
`auditpol /<get/set> /option:<FullPrivilegeAuditing> /<enable/disable>` -이 감사 정책 설정은 클라이언트가 생성 한 경우 이벤트 여부 사용자 보안 토큰에 할당 된 이러한 권한을 더를 지정 합니다. AssignPrimaryTokenPrivilege, AuditPrivilege, BackupPrivilege, CreateTokenPrivilege, DebugPrivilege, EnableDelegationPrivilege, ImpersonatePrivilege, LoadDriverPrivilege, RestorePrivilege, SecurityPrivilege, SystemEnvironmentPrivilege, TakeOwnershipPrivilege, 및 TcbPrivilege 합니다. 이 옵션을 사용 하지 않는 경우 (기본값 = 사용 안 함), BackupPrivilege 및 RestorePrivilege 권한을 기록 되지 않습니다. 이 옵션을 사용 하면 백업 작업 중에서 보안 로그 매우 시끄러운 (때로는 수백 개의 이벤트를 두 번째로) 가능 합니다. 이 정책을 설정할 수도 있습니다 그룹 정책 보안 옵션을 수정 하 여 **감사 합니다. 백업 및 복원 권한 사용 감사**합니다.  
  
> [!NOTE]  
> 여기에 제공 된 일부 정보는 Microsoft에서 가져왔으면 [감사 옵션 종류](https://msdn.microsoft.com/library/dd973862(prot.20).aspx) 및 Microsoft SCM 도구입니다.  
  
## <a name="enforcing-traditional-auditing-or-advanced-auditing"></a>기존 감사 또는 고급 감사를 적용합니다.

Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows 8, Windows 7 및 Windows Vista, 관리자에는 9 개의 일반 범주를 사용 하거나 하위 범주를 사용 하도록 선택할 수 있습니다. 각 Windows 시스템에서 수행 해야 하는 이진 선택 이며 주요 범주를 사용할 수 있으며 또는 subcategoriesit 둘 다를 수 없습니다.  
  
레거시 기존 범주 정책을에서 감사 정책 하위 범주를 덮어쓰지 않도록 하려면 활성화 해야는 **Force 감사 정책 하위 범주 설정 (Windows Vista 이상) 감사 정책 범주 설정 보다 우선 하** 아래에 있는 정책 설정을 **컴퓨터 구성 설정 \ 보안 설정 \ 로컬 정책 \ 보안 옵션**합니다.  
  
하위 범주 설정 되 고 9 가지 주요 범주는 대신 구성 하는 것이 좋습니다. 이 설정 해야 하는 그룹 정책 설정을 (하위 범주 감사 범주를 재정의할 수 있도록) 함께 지 원하는 감사 정책을 서로 다른 하위 범주를 구성 합니다.  
  
그룹 정책 및 명령줄 프로그램, auditpol.exe 등 몇 가지 메서드를 사용 하 여 감사 하위 범주를 구성할 수 있습니다.  
  
## <a name="next-steps"></a>다음 단계
  
* [에서 고급 보안 감사 Windows 7 및 Windows Server 2008 R2](https://social.technet.microsoft.com/wiki/contents/articles/advanced-security-auditing-in-windows-7-and-windows-server-2008-r2.aspx)  
  
* [감사 및 Windows Server 2008의에서 규정 준수](https://technet.microsoft.com/magazine/2008.03.auditing.aspx)  
  
* [그룹 정책을 사용 하 여 세부 보안 감사 Windows Vista 및 Windows Server 2008 기반 컴퓨터에서 Windows Server 2008 도메인, Windows Server 2003 도메인 또는 Windows 2000 도메인에 대 한 설정을 구성 하는 방법](https://support.microsoft.com/kb/921469)  
  
* [고급 보안 감사 정책 단계별 가이드](https://technet.microsoft.com/library/dd408940(WS.10).aspx)  
