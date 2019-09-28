---
title: AD FS 문제 해결-감사 이벤트 및 로깅
description: 이 문서에서는 다양 한 AD FS 로그를 사용 하 여 문제를 해결 하는 방법을 설명 합니다.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5985fc022a084e0e36e12ea60f18d1650c8c6b51
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366204"
---
# <a name="ad-fs-troubleshooting---events-and-logging"></a>AD FS 문제 해결-이벤트 및 로깅
AD FS는 문제 해결에 사용할 수 있는 두 가지 기본 로그를 제공 합니다.  구현되지 않은 것은 다음과 같습니다.

- 관리자 로그
- 추적 로그  
 
이러한 각 로그는 아래에 설명 되어 있습니다.

## <a name="admin-log"></a>관리자 로그
관리자 로그는 발생 하는 문제에 대 한 높은 수준의 정보를 제공 하며 기본적으로 사용 하도록 설정 됩니다.

### <a name="to-view-the-admin-log"></a>관리자 로그를 보려면
1.  이벤트 뷰어를 엽니다.
2.  **응용 프로그램 및 서비스 로그**를 확장 합니다.
3.  **AD FS**를 확장 합니다.
4.  **관리자**를 클릭 합니다.

![감사 기능 향상](media/ad-fs-tshoot-logging/event1.PNG)  

## <a name="trace-log"></a>추적 로그
추적 로그에는 자세한 메시지가 기록 되며 문제를 해결할 때 가장 유용한 로그가 됩니다. 시스템 성능에 영향을 줄 수 있는 짧은 시간에 많은 추적 로그 정보가 생성 될 수 있으므로 추적 로그는 기본적으로 사용 하지 않도록 설정 됩니다. 

### <a name="to-enable-and-view-the-trace-log"></a>추적 로그를 사용 하도록 설정 하 고 확인 하려면
1.  이벤트 뷰어를 엽니다.
2.  **응용 프로그램 및 서비스 로그** 를 마우스 오른쪽 단추로 클릭 하 고 보기를 선택한 다음 **분석 및 디버그 로그 표시**를 클릭 합니다.  그러면 왼쪽에 추가 노드가 표시 됩니다.
![향상 된 감사 기능](media/ad-fs-tshoot-logging/event2.PNG)  
3.  AD FS 추적 확장
4.  디버그를 마우스 오른쪽 단추로 클릭 하 고 **로그 사용**을 선택 합니다.
![향상 된 감사 기능](media/ad-fs-tshoot-logging/event3.PNG)  


## <a name="event-auditing-information-for-ad-fs-on-windows-server-2016"></a>Windows Server 2016의 AD FS에 대 한 이벤트 감사 정보  
기본적으로 Windows Server 2016의 AD FS에는 기본 수준의 감사를 사용 하도록 설정 되어 있습니다.  기본 감사 관리자는 단일 요청에 대 한 이벤트 5 개 이하로 표시 됩니다.  이 관찰, 단일 요청을 확인 하기 위해 관리자는 이벤트 수가 크게 감소 되는 표시 됩니다.   PowerShell cmdlt를 사용 하 여 감사 수준을 발생 하거나 낮출 수 있습니다.  

```PowerShell
Set-AdfsProperties -AuditLevel 
```

아래 표에서 사용할 수 있는 감사 수준을 설명합니다.  

|감사 수준|PowerShell 구문|설명|  
|----- | ----- | ----- |
|없음|Set-adfsproperties-AuditLevel None|감사 사용 하지 않도록 설정 하 고 이벤트가 기록 됩니다.|  
|Basic (기본값)|Set-adfsproperties-AuditLevel Basic|단일 요청에 대 한 5 개 이하의 이벤트가 기록 됩니다.|  
|자세히|Set-adfsproperties-AuditLevel Verbose|모든 이벤트가 기록 됩니다.  이 상당한 양의 요청당 정보를 기록 합니다.|  
  
현재 감사 수준을 보려면 PowerShell cmdlt를 사용 하면 됩니다.  Set-adfsproperties.  
  
![감사 기능 향상](media/ad-fs-tshoot-logging/ADFS_Audit_1.PNG)  
  
PowerShell cmdlt를 사용 하 여 감사 수준을 발생 하거나 낮출 수 있습니다.  Set-adfsproperties-AuditLevel을 설정 합니다.  
  
![감사 기능 향상](media/ad-fs-tshoot-logging/ADFS_Audit_2.png)  
  
## <a name="types-of-events"></a>이벤트 유형  
AD FS 이벤트는 AD FS에서 처리 하는 다양 한 유형의 요청을 기준으로 다양 한 형식일 수 있습니다. 각 이벤트 유형에는 관련 된 특정 데이터가 있습니다.  이벤트 유형은 로그인 요청 (즉, 토큰 요청)과 시스템 요청 (구성 정보 페치를 포함 하 여 서버 호출) 간에 구분할 수 있습니다.    

다음 표에서는 기본적인 이벤트 유형을 설명 합니다.  
  
|이벤트 유형|이벤트 ID|설명| 
|----- | ----- | ----- | 
|새 자격 증명 유효성 검사 성공|1202|여기서 새 자격 증명의 유효성을 검사 성공적으로 페더레이션 서비스는 요청입니다. Saml-p, Ws-federation, Ws-trust, 여기에 포함 됩니다 (SSO를 생성 하려면 첫 번째 구간) 및 OAuth 권한 부여 끝점입니다.|  
|새 자격 증명 유효성 검사 오류|1203|새 자격 증명 유효성 검사는 페더레이션 서비스에는 실패 한 요청입니다. Ws-trust, 이때 Ws-fed, Saml-p (SSO를 생성 하려면 첫 번째 구간) 및 OAuth 권한 부여 끝점입니다.|  
|응용 프로그램 토큰 성공|1200|보안 토큰을 페더레이션 서비스에서 성공적으로 실행 되는 요청입니다. Ws-federation, SAML-P이 이벤트는 SSO 아티팩트가 요청이 처리 될 때 기록 됩니다. (예: SSO 쿠키).|  
|응용 프로그램 토큰 실패|1201|페더레이션 서비스에서 보안 토큰 발급 실패 하는 위치는 요청입니다. Ws-federation, SAML-P SSO 아티팩트가 요청이 처리 된이 기록 됩니다. (예: SSO 쿠키).|  
|암호 변경 요청 성공|1204|페더레이션 서비스에서 암호 변경 요청에는 트랜잭션이 처리 되었습니다.|  
|암호 변경 요청 오류|1205|페더레이션 서비스에서 처리할 수 있는 암호 변경 요청 트랜잭션이 실패 했습니다.| 
|로그 아웃 성공|1206|로그 아웃 요청이 성공적으로 실행에 대해 설명 합니다.|  
|로그 아웃 실패|1207|실패 한 로그 아웃 요청에 설명 합니다.|  

## <a name="security-auditing"></a>보안 감사
AD FS 서비스 계정의 보안 감사는 때때로 암호 업데이트, 요청/응답 로깅, 요청 하는 요청/응답 로깅, 장치 등록 결과 요청을 추적 하는 데 도움이 될 수 있습니다.  AD FS 서비스 계정의 감사는 기본적으로 사용 하지 않도록 설정 되어 있습니다.

### <a name="to-enable-security-auditing"></a>보안 감사를 사용 하도록 설정 하려면
1. 시작을 클릭 하 고 **프로그램**, **관리 도구**를 차례로 가리킨 다음 **로컬 보안 정책**을 클릭 합니다.
2. **보안 설정\로컬 정책\사용자 권한 관리** 폴더로 이동한 다음 **보안 감사 생성**을 두 번 클릭합니다.
3. **로컬 보안 설정** 탭에서 AD FS 서비스 계정이 나열 되어 있는지 확인 합니다. 없는 경우 사용자 또는 그룹 추가를 클릭 하 여 목록에 추가 하 고 확인을 클릭 합니다.
4. 상승 된 권한으로 명령 프롬프트를 열고 다음 명령을 실행 하 여 "응용 프로그램 생성"/실패 감사를 사용 하도록 설정 합니다./subcategory: enable/success: enable
5. **로컬 보안 정책을**닫고 AD FS 관리 스냅인을 엽니다.
 
AD FS 관리 스냅인을 열려면 시작을 클릭 하 고 프로그램, 관리 도구를 차례로 가리킨 다음 AD FS 관리를 클릭 합니다.
 
6. 작업 창에서 편집 페더레이션 서비스 속성을 클릭 합니다.
7. 페더레이션 서비스 속성 대화 상자에서 이벤트 탭을 클릭 합니다.
8. **성공 감사** 및 **실패 감사** 확인란을 선택 합니다.
9. 확인을 클릭합니다.

![감사 기능 향상](media/ad-fs-tshoot-logging/event4.PNG)  
 
>[!NOTE]
>위의 지침은 AD FS 독립 실행형 멤버 서버에 있는 경우에만 사용 됩니다.  AD FS 로컬 보안 정책 대신 도메인 컨트롤러에서 실행 되는 경우 **그룹 정책 관리/포리스트/도메인/도메인 컨트롤러**에 있는 **기본 도메인 컨트롤러 정책을** 사용 합니다.  편집을 클릭 하 고 **Computer Configuration\Policies\Windows 설정 \ 로컬 정책 \ 정책 \ Rights Management** 로 이동 합니다.

## <a name="windows-communication-foundation-and-windows-identity-foundation-messages"></a>Windows Communication Foundation 및 Windows Identity Foundation 메시지
추적 로깅 외에도 문제를 해결 하기 위해 WCF (Windows Communication Foundation) 및 WIF (Windows Identity Foundation) 메시지를 확인 해야 하는 경우가 있습니다. AD FS 서버에서 **IdentityServer** 파일을 수정 하 여이 작업을 수행할 수 있습니다. 

이 파일은 **<% system root% > \Windows\ADFS** 에 있으며 XML 형식입니다. 파일의 관련 부분이 다음과 같이 표시 됩니다. 
```
<!-- To enable WIF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="Microsoft.IdentityModel" switchValue="Off"> … </source>

<!-- To enable WCF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="System.ServiceModel" switchValue="Off" > … </source>
```


이러한 변경 내용을 적용 한 후에 구성을 저장 하 고 AD FS 서비스를 다시 시작 합니다. 적절 한 스위치를 설정 하 여 이러한 추적을 사용 하도록 설정 하면 Windows 이벤트 뷰어의 AD FS 추적 로그에 표시 됩니다.

## <a name="correlating-events"></a>이벤트 상관 관계
문제를 해결 하는 가장 어려운 작업 중 하나는 많은 오류 또는 디버그 이벤트를 생성 하는 액세스 문제입니다.

이를 지원 하기 위해 AD FS는 관리자와 디버그 로그 둘 다에서 이벤트 뷰어에 기록 되는 모든 이벤트의 상관 관계를 유지 하며,이는 활동 ID 라는 고유 GUID (Globally Unique Identifier)를 사용 하 여 특정 요청에 해당 합니다. 이 ID는 토큰 발급 요청이 처음에 웹 응용 프로그램 (수동 요청자 프로필을 사용 하는 응용 프로그램의 경우) 또는 클레임 공급자로 직접 전송 된 요청 (WS-TRUST를 사용 하는 응용 프로그램의 경우)으로 표시 될 때 생성 됩니다. 

![activityid](media/ad-fs-tshoot-logging/activityid1.png)

이 활동 ID는 요청의 전체 기간에 대해 동일 하 게 유지 되 고 해당 요청에 대 한 이벤트 뷰어에 기록 된 모든 이벤트의 일부로 기록 됩니다. 즉,
 - 이 작업 ID를 사용 하 여 이벤트 뷰어를 필터링 하거나 검색 하면 토큰 요청에 해당 하는 모든 관련 이벤트를 추적 하는 데 도움이 됩니다.
 - 동일한 활동 ID가 여러 컴퓨터에 기록 되므로, 사용자 요청에 대 한 문제를 해결 하는 데는 FSP (페더레이션 서버 프록시)와 같은 여러 컴퓨터를 사용할 수 있습니다.
 - 작업 ID는 AD FS 요청이 실패 하는 경우 사용자의 브라우저에도 표시 되므로 사용자가이 ID를 지원 센터 또는 IT 지원에 전달할 수 있습니다.

![activityid](media/ad-fs-tshoot-logging/activityid2.png)

문제 해결 프로세스를 지원 하기 위해 AD FS는 AD FS 서버에서 토큰 발급 프로세스가 실패할 때마다 호출자 ID 이벤트를 로깅합니다. 이 이벤트는 다음 클레임 유형 중 하나의 클레임 유형 및 값을 포함 합니다 .이 정보는 토큰 요청의 일부로 페더레이션 서비스 전달 된 것으로 가정 합니다.
- http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountnameh
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upnh
- http://schemas.microsoft.com/ws/2008/06/identity/claims/upn
- http://schemas.xmlsoap.org/claims/UPN
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddressh
- http://schemas.microsoft.com/ws/2008/06/identity/claims/emailaddress 
- http://schemas.xmlsoap.org/claims/EmailAddress
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name
- http://schemas.microsoft.com/ws/2008/06/identity/claims/name
- http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier 

또한 호출자 ID 이벤트는 해당 작업 id를 사용 하 여 특정 요청에 대 한 이벤트 로그를 필터링 하거나 검색할 수 있도록 하는 작업 ID를 기록 합니다.




## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)
