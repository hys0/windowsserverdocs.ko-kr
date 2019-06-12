---
title: AD FS 문제 해결-이벤트 감사 및 로깅
description: 이 문서에서는 문제를 해결 하는 다양 한 AD FS 로그를 사용 하는 방법 설명
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1acc00ca376c48f7fb34214cef3a92961d355ae4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444019"
---
# <a name="ad-fs-troubleshooting---events-and-logging"></a>AD FS 문제 해결-이벤트 및 로깅
AD FS 문제 해결에 사용할 수 있는 두 개의 기본 로그를 제공 합니다.  구현되지 않은 것은 다음과 같습니다.

- 관리자 로그
- 추적 로그  
 
이러한 로그의 각 아래 설명 되어 있습니다.

## <a name="admin-log"></a>관리자 로그
관리 로그 발생 하 고 기본적으로 사용 하도록 설정할지 여부를 지정 하는 문제에 높은 수준의 정보를 제공 합니다.

### <a name="to-view-the-admin-log"></a>관리자 로그를 보려면
1.  이벤트 뷰어를 엽니다.
2.  확장 **응용 프로그램 및 서비스 로그**합니다.
3.  확장 **AD FS**합니다.
4.  클릭할 **관리자**합니다.

![감사 기능 향상](media/ad-fs-tshoot-logging/event1.PNG)  

## <a name="trace-log"></a>추적 로그
추적 로그 위치 이며 자세한 메시지 로그는 문제를 해결할 때 가장 유용한 로그 됩니다. 많은 추적 로그 정보는 짧은 기간 동안 시스템 성능에 영향을 줄 수에서 생성 될 수 있으므로 추적 로그는 기본적으로 비활성화 됩니다. 

### <a name="to-enable-and-view-the-trace-log"></a>설정 및 추적 로그를 확인 하려면
1.  이벤트 뷰어를 엽니다.
2.  마우스 오른쪽 단추로 클릭 **응용 프로그램 및 서비스 로그** 뷰를 선택 하 고 클릭 **분석 및 디버그 로그 표시**합니다.  추가 노드는 왼쪽에 표시 됩니다.
![감사 기능 향상](media/ad-fs-tshoot-logging/event2.PNG)  
3.  AD FS 추적 확장
4.  선택한 디버그를 마우스 오른쪽 단추로 클릭 **로그 사용**합니다.
![감사 기능 향상](media/ad-fs-tshoot-logging/event3.PNG)  


## <a name="event-auditing-information-for-ad-fs-on-windows-server-2016"></a>Windows Server 2016에서 AD FS에 대 한 이벤트 감사 정보  
기본적으로 Windows Server 2016에서 AD FS 감사 사용의 기본 수준을 있습니다.  기본 감사 관리자는 단일 요청에 대 한 이벤트 5 개 이하로 표시 됩니다.  이 관찰, 단일 요청을 확인 하기 위해 관리자는 이벤트 수가 크게 감소 되는 표시 됩니다.   감사 수준 수 거 나 낮추는 PowerShell cmdlt을 사용 하 여:  

```PowerShell
Set-AdfsProperties -AuditLevel 
```

아래 표에서 사용할 수 있는 감사 수준을 설명합니다.  

|감사 수준|PowerShell 구문|설명|  
|----- | ----- | ----- |
|없음|Set-adfsproperties-AuditLevel 없음|감사 사용 하지 않도록 설정 하 고 이벤트가 기록 됩니다.|  
|Basic (기본값)|Set-adfsproperties-AuditLevel Basic|단일 요청에 대 한 5 개 이하의 이벤트가 기록 됩니다.|  
|자세히|Set-adfsproperties-AuditLevel 세부 정보 표시|모든 이벤트가 기록 됩니다.  이 상당한 양의 요청당 정보를 기록 합니다.|  
  
현재 감사 수준을 보려면 PowerShell cmdlt을 사용할 수 있습니다.  Get-AdfsProperties.  
  
![감사 기능 향상](media/ad-fs-tshoot-logging/ADFS_Audit_1.PNG)  
  
감사 수준 수 거 나 낮추는 PowerShell cmdlt을 사용 하 여:  Set-AdfsProperties -AuditLevel.  
  
![감사 기능 향상](media/ad-fs-tshoot-logging/ADFS_Audit_2.png)  
  
## <a name="types-of-events"></a>이벤트 유형  
AD FS 이벤트는 다양 한 유형의 AD FS에서 처리 된 요청 수에 따라 다양 한 유형의 수 있습니다. 각 유형의 이벤트에 연결 된 특정 데이터가 있습니다.  이벤트의 유형 시스템 요청 (구성 정보를 가져오는 중을 비롯 한 서버 호출)와 로그인 요청 (즉, 토큰 요청) 간의 구분할 수 있습니다.    

아래 표에서 기본 유형의 이벤트를 설명합니다.  
  
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
보안 감사는 AD FS 서비스 계정 암호 업데이트, 요청/응답 로깅, 요청 contect 헤더 및 장치 등록 결과 사용 하 여 문제를 추적할 경우에 따라 지원할 수 있습니다.  AD FS 서비스 계정에 대 한 감사는 기본적으로 비활성화 됩니다.

### <a name="to-enable-security-auditing"></a>보안 감사를 사용 하도록 설정 하려면
1. 시작을 클릭 **프로그램**, 가리킨 **관리 도구**를 클릭 하 고 **로컬 보안 정책**합니다.
2. **보안 설정\로컬 정책\사용자 권한 관리** 폴더로 이동한 다음 **보안 감사 생성**을 두 번 클릭합니다.
3. 에 **로컬 보안 설정** 탭에서 AD FS 서비스 계정이 나열 되어 있는지 확인 합니다. 제공 되지 사용자 또는 그룹 추가 클릭 하 고 목록에 추가 및 확인을 클릭 합니다.
4. 상승 된 권한으로 명령 프롬프트를 열고 사용 감사 auditpol.exe /set /subcategory 다음 명령을 실행: "Application Generated" /failure: enable /success:enable
5. 닫기 **로컬 보안 정책**, AD FS 관리 스냅인을 엽니다.
 
AD FS 관리 스냅인을 열려면 시작을 클릭 하 고 프로그램, 관리 도구를 가리키고 AD FS 관리를 차례로 클릭 합니다.
 
6. 작업 창에서 페더레이션 서비스 속성 편집 클릭
7. 페더레이션 서비스 속성 대화 상자에서 [이벤트] 탭을 클릭 합니다.
8. 선택 된 **성공 감사** 하 고 **실패 감사** 확인란 합니다.
9. 확인을 클릭합니다.

![감사 기능 향상](media/ad-fs-tshoot-logging/event4.PNG)  
 
>[!NOTE]
>위의 지침에 따라 독립 실행형 구성원 서버에서 AD FS가 하는 경우에 사용 됩니다.  AD FS는 로컬 보안 정책, 대신 도메인 컨트롤러에서 실행 중인 경우 사용 합니다 **기본 도메인 컨트롤러 정책** 에 있는 **그룹 정책 관리/포리스트/도메인/도메인 컨트롤러**합니다.  편집을 클릭 하 고 이동할 **컴퓨터 구성 \ 정책 \ Settings\Local Policies\User Rights Management**

## <a name="windows-communication-foundation-and-windows-identity-foundation-messages"></a>Windows Communication Foundation 및 Windows Identity Foundation 메시지
경우에 따라 로깅 추적 하는 것 외에도 문제를 해결 하기 위해 Windows Communication Foundation (WCF) 및 Windows Identity Foundation (WIF) 메시지를 보려면 해야 할 수 있습니다. 수정 하 여 이렇게 합니다 **Microsoft.IdentityServer.ServiceHost.Exe.Config** AD FS 서버에서 파일입니다. 

이 파일에 위치한 **< % 시스템 루트 % > \Windows\ADFS** 이며 XML 형식입니다. 이와 관련 된 부분 파일은 다음과 같습니다. 
```
<!-- To enable WIF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="Microsoft.IdentityModel" switchValue="Off"> … </source>

<!-- To enable WCF tracing, change the switchValue below to desired trace level - Verbose, Information, Warning, Error, Critical -->

<source name="System.ServiceModel" switchValue="Off" > … </source>
```


이러한 변경 내용을 적용 하 여 구성을 저장 후 AD FS 서비스를 다시 시작 합니다. 적절 한 스위치를 설정 하 여 이러한 추적을 사용 하도록 설정한 후 Windows 이벤트 뷰어에서 AD FS 추적 로그에 나타납니다.

## <a name="correlating-events"></a>이벤트 상관 관계 설정
문제를 해결 하려면 가장 어려운 일 중 하나는 많은 오류를 생성 하거나 이벤트를 디버그 하는 액세스 문제입니다.

AD FS이를 돕기 위해 관리자와는 고유 식별자 GUID (Globally Unique) 활동 id를 사용 하 여 특정 요청에 해당 하는 디버그 로그를 이벤트 뷰어에 기록 되는 모든 이벤트를 상호 연결 이 ID는 토큰 발급 요청 (WS-트러스트를 사용 하 여 응용 프로그램)에 대 한 클레임 공급자에 게 직접 전송 된 요청 (수동 요청자 프로필을 사용 하 여 응용 프로그램)에 대 한 웹 응용 프로그램에 처음 표시 되 면 생성 됩니다. 

![activityid](media/ad-fs-tshoot-logging/activityid1.png)

이 작업 ID는 요청의 전체 기간 동안 동일 하 게 유지 하 고 모든 이벤트의 일부로 기록 된 이벤트 뷰어는 요청에 대 한 기록 됩니다. 즉,
 - 필터링 또는 ID 토큰 요청에 해당 하는 모든 관련된 이벤트의 추적을 유지 하는 데 도움이 됩니다이 작업을 사용 하 여 이벤트 뷰어를 검색 하는
 - 동일한 동작 ID는 페더레이션 서버 프록시 (FSP)와 같은 여러 컴퓨터에서 사용자 요청을 해결 하는 여러 컴퓨터에서 로깅됩니다.
 - 작업 ID도 나타납니다 사용자의 브라우저에서 어떤 방식으로든에서 AD FS 요청에 실패 하면 되므로 사용자가 IT 지원 또는 기술 지원팀에이 ID를 전달할 수 있도록 합니다.

![activityid](media/ad-fs-tshoot-logging/activityid2.png)

문제 해결 프로세스를 지원 하기 위해 AD FS는 또한 토큰 발급 프로세스를 AD FS 서버에서 실패할 때마다 호출자 ID 이벤트를 기록 합니다. 이 이벤트는 클레임의 형식 및 값이이 정보는 토큰 요청의 일부분으로 페더레이션 서비스에 전달 된 가정 하 고 다음 클레임 형식 중 하나에 포함 되어 있습니다.
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

호출자 ID 이벤트는 또한 해당 작업 ID를 사용 하 여 특정 요청에 대 한 이벤트 로그를 검색 하거나 필터링 할 수 있도록 작업 ID를 기록 합니다.




## <a name="next-steps"></a>다음 단계

- [AD FS 문제 해결](ad-fs-tshoot-overview.md)
