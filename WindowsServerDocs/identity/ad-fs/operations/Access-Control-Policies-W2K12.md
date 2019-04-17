---
ms.assetid: 5728847d-dcef-4694-9080-d63bfb1fe24b
title: "Adfs의 액세스를 제어 정책"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0b4549192bc4dab9edf3b2a10421325144ed0cd2
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="access-control-policies-in-windows-server-2012-r2-and-windows-server-2012-ad-fs"></a>Windows Server 2012 R2 및 Windows Server 2012 광고 FS에서 액세스 제어 정책

>적용 대상: Windows Server 2012 R2 및 Windows Server 2012 

이 문서에서 설명한 정책은 클레임 중 두 종류의 사용  
  
1.  클레임 ADFS Adfs와 웹 응용 프로그램 프록시 검사 하 고 ADFS 또는 WAP에 직접 연결 하는 클라이언트의 IP 주소와 같이 확인할 수 있는 정보에 따라 만듭니다.  
  
2.  클레임 ADFS 탐지도 클라이언트 Adfs에 전달 하는 정보에 따라 만듭니다.  
  
>**중요 한**: Windows 10 도메인 가입 차단 되며 다음과 같은 추가 끝점에 액세스 해야 하는 시나리오에 로그인을 하면 아래에 설명 된 대로 정책

광고 FS 끝점에 Windows 10 도메인 가입 하 고 로그인 필요
- [federation 서비스 이름] / adfs/서비스/신뢰/2005/windowstransport
- [federation 서비스 이름] / adfs/서비스/신뢰 월 13 일 windowstransport
- [federation 서비스 이름] / adfs/서비스/신뢰/2005/usernamemixed
- [federation 서비스 이름] / adfs/서비스/신뢰 월 13 일 usernamemixed 
- [federation 서비스 이름] / adfs/서비스/신뢰/2005/certificatemixed
- [federation 서비스 이름] / adfs/서비스/신뢰 월 13 일 certificatemixed

를 해결 하려면 위의 끝점에 대 한 예외 수 있도록 끝점 클레임에 따라 정책 거부 하는 업데이트입니다.

예를 들어, 규칙 아래의:

`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  

가을 업데이트:

`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "(/adfs/ls/)|(/adfs/services/trust/2005/windowstransport)|(/adfs/services/trust/13/windowstransport)|(/adfs/services/trust/2005/usernamemixed)|(/adfs/services/trust/13/usernamemixed)|(/adfs/services/trust/2005/certificatemixed)|(/adfs/services/trust/13/certificatemixed)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`



> [!NOTE]
>  이 범주에서 클레임 비즈니스 정책 구현할 수만 사용 해야 하 고 네트워크에 대 한 액세스를 보호 하는 보안 정책을 아니라 합니다.  헤더를 보내려면으로 잘못 된 정보에 액세스 하는 방법으로 무단된 클라이언트에 대 한 것 같습니다.  
  
이 문서에서 설명한 정책 항상 사용자 이름 및 암호나 다중 요소 인증와 같은 다른 인증 방법으로 사용 해야 합니다.  
  
## <a name="client-access-policies-scenarios"></a>클라이언트 액세스 정책 시나리오  
  
|**시나리오**|**설명**| 
| --- | --- | 
|차단 외부 Office 365에 대 한 모든 시나리오 1:|Office 365 액세스 회사 내부 네트워크에 있는 모든 클라이언트에서 사용할 수 있지만 외부 클라이언트의 IP 주소를 기초로 외부 클라이언트의에서 요청을 거부 합니다.|  
|차단 외부 Exchange ActiveSync 제외 하 고 Office 365에 대 한 모든 시나리오 2:|회사 내부 네트워크에 있는 모든 클라이언트 뿐만 아니라 스마트폰 Exchange ActiveSync 사용 하는 등의 모든 클라이언트 외부 디바이스의 office 365 액세스 허용 됩니다. 다른 모든 외부 클라이언트, Outlook을 사용 하는 것과 같은 차단 됩니다.|  
|브라우저 기반 응용 프로그램을 제외 하 고에 Office 365 외부 모든 액세스를 차단 하는 시나리오 3:|외부 사용할 수 없게 Office 365 수동 (브라우저 기반) 등의 응용 프로그램 Outlook Web Access 또는 SharePoint Online 제외 하 고 있습니다.|  
|4 시나리오: 외부에 대 한 모든 Office 365 지정 된 Active Directory 그룹을 제외 하 고 차단|이 시나리오를 테스트 하 고 클라이언트 액세스 정책 배포의 유효성 검사 사용 됩니다. 하나 이상의 Active Directory 그룹의 회원에 대해서만 Office 365에 대 한 액세스 외부를 차단합니다. 그룹의 회원 에게만 외부 액세스를 제공 하기 위해 데도 수 있습니다.|  
  
## <a name="enabling-client-access-policy"></a>클라이언트 액세스 정책 설정  
 Windows Server 2012 r 2에서 adfs에서 액세스 정책 클라이언트를 사용 하려면 파티 신뢰를 사용 하지 않고 Microsoft Office 365 Id 플랫폼 업데이트 해야 합니다. 클레임 규칙에서 구성 하려면 아래의 예제 시나리오 중 하나를 선택는 **Microsoft Office 365 Id 플랫폼** 신뢰 파티 신뢰 가장 조직의 요구 사항을 만족 하는지 합니다.  
  
###  <a name="scenario1"></a>차단 외부 Office 365에 대 한 모든 시나리오 1:  
 이 클라이언트 액세스 정책 시나리오 외부 클라이언트의 IP 주소를 기초로 모든 외부 클라이언트 모든 내부 클라이언트 및 블록에서 액세스할 수 있습니다. 올바른 발급 부여 규칙 선택한 시나리오에 대해 당사자 보안 의존 Office 365에 추가 하려면 다음 절차에 사용할 수 있습니다.  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365"></a>Office 365에 대 한 모든 외부 차단 규칙을 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **광고 FS\Trust 관계**, 클릭 **의존 파티 신뢰**를 마우스 오른쪽 단추로 클릭는 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 한 다음 **편집 클레임 규칙**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자를 선택 하 고 있는 **발급 승인 규칙** 탭을 클릭 한 다음 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**, 클릭 한 다음 **다음**합니다.  
  
5.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**, 예를 들어가이 규칙의 표시 이름을 "원하는 범위를 벗어나는 IP 청구 된 경우 거부" 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을 (대체 위의 "x ms-전달-클라이언트-ip" 유효한 IP 식으로에 대 한 값):  
`c1:[Type == " https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");` </br>
6.  클릭 **완료**합니다. 새 규칙을 기본 하기 전에 발급 승인 규칙 목록에 표시 되는지 확인 **모든 사용자에 액세스 허용** (거부 규칙 우선 앞부분 목록에에서 표시 되지만) 규칙 합니다.  액세스 규칙 허용 기본 없는 경우 다음과 같은 클레임 규칙 언어를 사용 하 여 목록의 끝에 추가할 수 있습니다.  </br>
    
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true"); ` 

7.  새로운 규칙에 저장 하는 **편집 클레임 규칙** 대화 상자를 클릭 **확인**합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급 Auth 규칙](media/Access-Control-Policies-W2K12/clientaccess1.png "ADFS_Client_Access_1")  
  
###  <a name="scenario2"></a>차단 외부 Exchange ActiveSync 제외 하 고 Office 365에 대 한 모든 시나리오 2:  
 다음 예제 Outlook 등 내부 클라이언트에서 Exchange Online을 비롯 한 모든 Office 365 응용 프로그램에 액세스할 수 있습니다. 회사 네트워크에서 벗어나 있는 거주 하는 클라이언트에서 액세스 클라이언트 IP 주소 같은 스마트폰 Exchange ActiveSync 클라이언트를 제외 하 고에 표시 된 대로 차단 됩니다.  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-exchange-activesync"></a>Exchange ActiveSync 제외 하 고 Office 365에 대 한 모든 외부 차단 규칙을 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **광고 FS\Trust 관계**, 클릭 **의존 파티 신뢰**를 마우스 오른쪽 단추로 클릭는 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 한 다음 **편집 클레임 규칙**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자를 선택 하 고 있는 **발급 승인 규칙** 탭을 클릭 한 다음 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**, 클릭 한 다음 **다음**합니다.  
  
5.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**를 들어 "원하는 범위를 벗어나는 IP 청구 된 경우 발급 ipoutsiderange 클레임"에 대 한이 규칙에 대 한의 표시 이름을 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을 (대체 위의 "x ms-전달-클라이언트-ip" 유효한 IP 식으로에 대 한 값):  
    
    `c1:[Type == " https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  클릭 **완료**합니다. 새 규칙에 표시 되는지 확인는 **발급 승인 규칙** 목록입니다.  
  
7.  다음는 **클레임 규칙 편집** 대화 상자의 **발급 승인 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
8.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**, 클릭 한 다음 **다음**합니다.  
  
9. 에 **구성 규칙** 페이지의 **클레임 규칙 이름**, 예를 들어가이 규칙의 표시 이름을 "원하는 범위를 벗어나는 IP 고 방법이 아닌 EAS ms 클라이언트 응용 x 클레임 거부" 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을:  
  

    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value != "Microsoft.Exchange.ActiveSync"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  
  
10. 클릭 **완료**합니다. 새 규칙에 표시 되는지 확인는 **발급 승인 규칙** 목록입니다.  
  
11. 다음는 **클레임 규칙 편집** 대화 상자의 **발급 승인 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
12. 에 **규칙 템플릿 선택** 페이지의 **청구 규칙 서식 파일** 선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**을 차례로 클릭 하 고 **다음**합니다.  
  
13. 에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력, 예를 들어 "응용 프로그램이 클레임 있는지 확인" 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을:  
  
    ```  
    NOT EXISTS([Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application"]) => add(Type = "http://custom/xmsapplication", Value = "fail");  
    ```  
  
14. 클릭 **완료**합니다. 새 규칙에 표시 되는지 확인는 **발급 승인 규칙** 목록입니다.  
  
15. 다음는 **클레임 규칙 편집** 대화 상자의 **발급 승인 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
16. 에 **규칙 템플릿 선택** 페이지의 **청구 규칙 서식 파일** 선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**을 차례로 클릭 하 고 **다음**합니다.  
  
17. 에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력, 예를 들어 "거부" ipoutsiderange 참와 응용 프로그램 사용자가 실패 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을:  
  
`c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://custom/xmsapplication", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`</br>  
18. 클릭 **완료**합니다. 새 규칙 이전 규칙 아래 즉시 표시 되는지 확인 및 전에를 허용 액세스 모든 사용자에 게 기본 (거부 규칙 우선 앞부분 목록에에서 표시 되지만) 발급 승인 규칙 목록에서 규칙 합니다.  </br>액세스 규칙 허용 기본 없는 경우 다음과 같은 클레임 규칙 언어를 사용 하 여 목록의 끝에 추가할 수 있습니다.</br></br>      `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`</br></br>
19. 새로운 규칙에 저장 하는 **편집 클레임 규칙** 대화 상자에서 확인을 클릭 합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급 승인 규칙](media/Access-Control-Policies-W2K12/clientaccess2.png )  
  
###  <a name="scenario3"></a>브라우저 기반 응용 프로그램을 제외 하 고에 Office 365 외부 모든 액세스를 차단 하는 시나리오 3:  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-browser-based-applications"></a>브라우저 기반 응용 프로그램을 제외 하 고 Office 365에 외부 모든 액세스를 차단 하는 규칙 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **광고 FS\Trust 관계**, 클릭 **의존 파티 신뢰**를 마우스 오른쪽 단추로 클릭는 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 한 다음 **편집 클레임 규칙**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자를 선택 하 고 있는 **발급 승인 규칙** 탭을 클릭 한 다음 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**, 클릭 한 다음 **다음**합니다.  
  
5.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**를 들어 "원하는 범위를 벗어나는 IP 청구 된 경우 발급 ipoutsiderange 클레임"에 대 한이 규칙에 대 한의 표시 이름을 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을 (대체 위의 "x ms-전달-클라이언트-ip" 유효한 IP 식으로에 대 한 값):  </br>
`c1:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`   
6.  클릭 **완료**합니다. 새 규칙에 표시 되는지 확인는 **발급 승인 규칙** 목록입니다.  
  
7.  다음는 **클레임 규칙 편집** 대화 상자의 **발급 승인 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
8.  에 **규칙 템플릿 선택** 페이지의 **청구 규칙 서식 파일** 선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**을 차례로 클릭 하 고 **다음**합니다.  
  
9. 에 **구성 규칙** 페이지의 **클레임 규칙 이름**, 예를 들어가이 규칙의 표시 이름을 "원하는 범위를 벗어나는 IP 고 끝점/adfs/3!, 않습니다"거부 입력 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을:  
  
 
    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value != "/adfs/ls/"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = " DenyUsersWithClaim");`  
  
10. 클릭 **완료**합니다. 새 규칙을 기본 하기 전에 발급 승인 규칙 목록에 표시 되는지 확인 **모든 사용자에 액세스 허용** (거부 규칙 우선 앞부분 목록에에서 표시 되지만) 규칙 합니다.  </br></br> 액세스 규칙 허용 기본 없는 경우 다음과 같은 클레임 규칙 언어를 사용 하 여 목록의 끝에 추가할 수 있습니다.  
  
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`
  
11. 새로운 규칙에 저장 하는 **편집 클레임 규칙** 대화 상자를 클릭 **확인**합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급](media/Access-Control-Policies-W2K12/clientaccess3.png)  
  
###  <a name="scenario4"></a>4 시나리오: 외부에 대 한 모든 Office 365 지정 된 Active Directory 그룹을 제외 하 고 차단  
 이때에는 IP 주소를 기초로 내부 클라이언트에서 액세스할을 수 있습니다. 올바른 발급 승인 규칙을 추가 하려면 다음 단계에 지정 된 Active Directory Group.Use 사람이 제외 하 고, 외부 클라이언트 IP 주소가 회사 네트워크에서 벗어나 있는 상주 하는 클라이언트에서 액세스할 수 있는 **Microsoft Office 365 Id 플랫폼** 신뢰 파티 신뢰 클레임 규칙 마법사를 사용 하 여:  
  
##### <a name="to-create-rules-to-block-all-external-access-to-office-365-except-for-designated-active-directory-groups"></a>지정 된 Active Directory 그룹을 제외 하 고 Office 365에 대 한 모든 외부 차단 규칙을 만들려면  
  
1.  **서버 관리자**, 클릭 **도구**, 클릭 한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **광고 FS\Trust 관계**, 클릭 **의존 파티 신뢰**를 마우스 오른쪽 단추로 클릭는 **Microsoft Office 365 Id 플랫폼** 신뢰 하 고 클릭 한 다음 **편집 클레임 규칙**합니다.  
  
3.  에 **클레임 규칙 편집** 대화 상자를 선택 하 고 있는 **발급 승인 규칙** 탭을 클릭 한 다음 **규칙 추가** 클레임 규칙 마법사를 시작 합니다.  
  
4.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**, 클릭 한 다음 **다음**합니다.  
  
5.  에 **구성 규칙** 페이지의 **클레임 규칙 이름**를 들어 "원하는 범위를 벗어나는 IP 청구 된 경우 발표할 ipoutsiderange 클레임입니다."에 대 한이 규칙에 대 한의 표시 이름을 입력 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을 (대체 위의 "x ms-전달-클라이언트-ip" 유효한 IP 식으로에 대 한 값):  
  
      
    `c1:[Type == "https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip", Value =~ "^(?!192\.168\.1\.77|10\.83\.118\.23)"] && c2:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] => issue(Type = "http://custom/ipoutsiderange", Value = "true");`  

6.  클릭 **완료**합니다. 새 규칙에 표시 되는지 확인는 **발급 승인 규칙** 목록입니다.  
  
7.  다음는 **클레임 규칙 편집** 대화 상자의 **발급 승인 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
8.  에 **규칙 템플릿 선택** 페이지의 **청구 규칙 서식 파일** 선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**을 차례로 클릭 하 고 **다음**합니다.  
  
9. 에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력, 예를 들어 "검사 그룹 SID" 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을 (바꾸기 "groupsid"를 사용 하는 광고 그룹의 실제 sid):  
   
    `NOT EXISTS([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-100"]) => add(Type = "http://custom/groupsid", Value = "fail");`  

10. 클릭 **완료**합니다. 새 규칙에 표시 되는지 확인는 **발급 승인 규칙** 목록입니다.  
  
11. 다음는 **클레임 규칙 편집** 대화 상자의 **발급 승인 규칙** 탭을 클릭 **규칙 추가** 클레임 규칙 마법사를 다시 시작 합니다.  
  
12. 에 **규칙 템플릿 선택** 페이지의 **청구 규칙 서식 파일** 선택 **클레임 사용자 지정 규칙을 사용 하 여 보낼**을 차례로 클릭 하 고 **다음**합니다.  
  
13. 에 **구성 규칙** 페이지의 **클레임 규칙 이름**,이 규칙의 표시 이름을 입력, 예를 들어 "거부" ipoutsiderange 참 groupsid와 사용자가 실패 합니다. 아래에서 **사용자 지정 규칙**입력 하거나 붙여 다음 청구 규칙 언어 구문을:  
   
    `c1:[Type == "https://custom/ipoutsiderange", Value == "true"] && c2:[Type == "https://custom/groupsid", Value == "fail"] => issue(Type = "https://schemas.microsoft.com/authorization/claims/deny", Value = "DenyUsersWithClaim");`  

14. 클릭 **완료**합니다. 새 규칙 이전 규칙 아래 즉시 표시 되는지 확인 및 전에를 허용 액세스 모든 사용자에 게 기본 (거부 규칙 우선 앞부분 목록에에서 표시 되지만) 발급 승인 규칙 목록에서 규칙 합니다.  </br></br>액세스 규칙 허용 기본 없는 경우 다음과 같은 클레임 규칙 언어를 사용 하 여 목록의 끝에 추가할 수 있습니다.  
   
    `c:[] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");`  

15. 새로운 규칙에 저장 하는 **편집 클레임 규칙** 대화 상자에서 확인을 클릭 합니다. 결과 목록은 다음과 같습니다.  
  
     ![발급](media/Access-Control-Policies-W2K12/clientaccess4.png)  
  
##  <a name="buildingip"></a>IP 주소 범위 식 빌드  
 현재만 Exchange Online에서는 인증 요청 Adfs에 전달 하는 경우 헤더를 채웁니다으로 설정 되어 있는 HTTP 머리글에서 x ms-전달-클라이언트-ip 클레임이 채워집니다. 클레임 값 다음 중 하나를 수 있습니다.  
  
> [!NOTE]
>  Exchange Online IPV4 및 하지 IPV6 주소 현재 지원합니다.  
  
-   단일 IP 주소: Exchange Online에 직접 연결 하는 클라이언트의 IP 주소  
  
> [!NOTE]
>  -   회사 네트워크에 대 한 클라이언트의 IP 주소 조직의 아웃 바운드 프록시 또는 게이트웨이 외부 인터페이스 IP 주소가 표시 됩니다.  
> -   VPN 또는 Microsoft DirectAccess (DA) 하 여 회사 네트워크에 연결 하는 클라이언트 기업 클라이언트 내부 또는 외부 클라이언트 VPN 또는 da. 구성에 따라으로 표시 될 수 있습니다.  
  
-   하나 이상의 IP 주소: 연결 클라이언트의 IP 주소를 확인할 수 없는 경우 Exchange Online을 x-전달 기능에 대 한 머리글, HTTP 기반 요청에 포함 될 수 있는 많은 클라이언트, 부하 분산와 프록시 시장에서 지원 되는 사용할 수 없는 헤더 값에 따라 값 설정 됩니다.  
  
> [!NOTE]
>  1.  클라이언트 IP 주소와 요청을 전달 각 프록시의 주소가 표시 여러 IP 주소가 쉼표로 구분 됩니다.  
> 2.  Exchange Online 인프라와 관련 된 IP 주소 목록에 없는 됩니다.  
  
### <a name="regular-expressions"></a>일반 표현  
 IP 주소와 일치 해야 할 때 수행 비교 문자를 생성 하는 데 필요한 됩니다. 다음 일련의 단계를 우리는 예 다음 주소 범위 (공용 IP 범위 내에 맞게 이러한 예 변경 하는 주)에 맞게 식 생성 하는 방법에 대 한 제공 합니다.  
  
-   192.168.1.1 – 192.168.1.25  
  
-   10.0.0.1 – 10.0.0.14  
  
 먼저은 단일 IP 주소와 일치 하는 기본 패턴은 다음과 같습니다: \b###\\.###\\.###\\.###\b  
  
 를 확장 우리 수 일치 OR 식으로 두 가지 IP 주소 다음과 같은: \b###\\.###\\.###\\.###\b 및 #124;\b###\\.###\\.###\\.###\b  
  
 두 개의 주소 (192.168.1.1 10.0.0.1 등)와 일치 하도록 예로 들 수 있으므로,: \b192\\.168\\.1\\.1\b 및 #124;\b10\\.0\\.0\\.1\b  
  
 이 주소의 수에 관계 없이 입력할 수 있는 방법을 제공 합니다. 허용 예를 들어 192.168.1.1 – 192.168.1.25, 해야 할 다양 한 주소 나타나는 일치 하는 수행 해야 문자별으로 문자: \b192\\.168\\.1\\ 합니다. ([1-9] & #124; 1 [0-9] & #124, 2 [0 5]) \b  
  
 다음 note 하세요.  
  
-   IP 주소가 문자열 및 숫자가 아니라으로 간주 됩니다.  
  
-   규칙 다음과 같은 분할 됩니다. \b192\\.168\\.1\\ 합니다.  
  
-   192.168.1로 시작을 하는 가치를 찾습니다.  
  
-   다음 문자 최종 소수점 주소의 부분에 필요한 범위를 찾습니다.  
  
    -   1-9로 끝나는 ([1-9] 일치 주소  
  
    -   & #124; 1 [0-9] 10-19로 끝나는 주소를 찾습니다.  
  
    -   & 20 25로 끝나는 #124;2[0-5]) 일치 주소  
  
-   Note 다른 부분 IP 주소와 일치 하는 시작 하지 않도록는 괄호 올바르게 위치 해야 합니다.  
  
-   일치 하는 192 블록으로 10 블록에 대 한 유사 식 작성할 수 있습니다: \b10\\.0\\.0\\ 합니다. ([1-9] & #124; 1 [0 4]) \b  
  
-   결합 하, 다음 식 일치 해야 "192.168.1.1~25" 및 "10.0.0.1~14"에 대 한 모든 주소 및: \b192\\.168\\.1\\ 합니다. ([1-9] & #124; 1 [0-9] & #124, 2 [0 5]) \b & #124;\b10\\.0\\.0\\ 합니다. ([1-9] & #124; 1 [0 4]) \b  
  
### <a name="testing-the-expression"></a>식 테스트  
 Regex 확인 도구를 사용 하는 것이 좋습니다 하므로 Regex 식 매우 하기가 될 수 있습니다. "온라인 regex 식"에 대해 인터넷 검색을 수행 하면 샘플 데이터에 대 한 식 사용해 볼 수 있는 몇 가지 좋은 온라인 유틸리티를 찾을 수 있습니다.  
  
 식 테스트 때와 일치 하는 데 발생할 수 있는 문제를 이해 하는 것이 중요 합니다. Exchange online 시스템 쉼표로 많은 IP 주소를 보낼 수 있습니다. 위의 표현이 작동 합니다. 그러나는 regex 식 테스트 하는이 대해 생각 하는 것이 중요 합니다. 예를 들어, 위 예제 확인 입력 다음 샘플을 사용할 수 하나.  
  
 192.168.1.1, 192.168.1.2, 192.169.1.1. 192.168.12.1, 192.168.1.10, 192.168.1.25, 192.168.1.26, 192.168.1.30, 1192.168.1.20  
  
 10.0.0.1, 10.0.0.5, 10.0.0.10, 10.0.1.0, 10.0.1.1, 110.0.0.1, 10.0.0.14, 10.0.0.15, 10.0.0.10, 10,0.0.1  
  
## <a name="claim-types"></a>클레임 유형  
 Windows Server 2012 r 2에서 ADFS 다음 청구 형식을 사용 하 여 요청 상황에 맞는 정보를 제공 합니다.  
  
### <a name="x-ms-forwarded-client-ip"></a>X MS-전달-클라이언트-IP  
 클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-forwarded-client-ip`  
  
 이 ADFS 클레임 요청 (예: Outlook 클라이언트) 사용자의 IP 주소를 구축 방향을 얻기 위한에서 "좋은 시도를"를 나타냅니다. 이 청구 요청을 전달 하는 모든 프록시의 주소를 포함 하 여 여러 개의 IP 주소를 포함 될 수 있습니다.  이 클레임 HTTP에서 채워집니다. 클레임 값 다음 중 하나 될 수 있습니다.  
  
-   하나 IP 주소-Exchange Online에 직접 연결 하는 클라이언트의 IP 주소  
  
> [!NOTE]
>  회사 네트워크에 대 한 클라이언트의 IP 주소 조직의 아웃 바운드 프록시 또는 게이트웨이 외부 인터페이스 IP 주소가 표시 됩니다.  
  
-   하나 이상의 IP 주소  
  
    -   Exchange Online을 확인할 수 없는 연결 클라이언트의 IP 주소 HTTP 기반에 포함 될 수 있는 비 표준 헤더 요청 하 고 여러 클라이언트, 부하 분산와 프록시 시장에 지 원하는 x-전달 기능에 대 한 헤더 값에 따라 값이 설정 합니다.  
  
    -   클라이언트 IP 주소와 요청 전달 하는 각 프록시의 주소가 표시 여러 IP 주소가 쉼표로 구분 됩니다.  
  
> [!NOTE]
>  Exchange Online 인프라와 관련 된 IP 주소 목록에 표시 되지 않습니다.  
  
> [!WARNING]
>  Exchange Online IPV4 주소;만 현재 지원 IPV6 주소를 지원 하지 않습니다.  
  
### <a name="x-ms-client-application"></a>MS 클라이언트 응용 X  
 클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application`  
  
 이 ADFS 클레임 느슨하게 사용 중인 응용 프로그램에 해당 하는 최종 클라이언트를 사용 하는 프로토콜을 나타냅니다.  현재 있는 HTTP 머리글에서이 클레임 채워집니다만 Exchange Online을 인증 요청 Adfs에 전달 하는 경우 헤더를 채웁니다 하 여 설정 합니다. 응용 프로그램에 따라 다음 중 하나를 값이이 청구 됩니다.  
  
-   Exchange Activesync 사용 하는 디바이스의 경우 값 Microsoft.Exchange.ActiveSync입니다.  
  
-   Microsoft Outlook 클라이언트를 사용 하 여 다음 값 발생할 수 있습니다.  
  
    -   Microsoft.Exchange.Autodiscover  
  
    -   Microsoft.Exchange.OfflineAddressBook  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
    -   Microsoft.Exchange.RPCMicrosoft.Exchange.WebServices  
  
-   이 헤더에 대 한 기타 가능한 값은 다음과 같습니다.  
  
    -   Microsoft.Exchange.Powershell  
  
    -   Microsoft.Exchange.SMTP  
  
    -   Microsoft.Exchange.Pop  
  
    -   Microsoft.Exchange.Imap  
  
### <a name="x-ms-client-user-agent"></a>X-MS-클라이언트-사용자 에이전트  
 클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-user-agent`  
  
 이 ADFS 클레임 장치 종류 서비스에 액세스할 때 사용 하는 클라이언트를 표시 하는 문자열을 제공 합니다. 고객이 특정 장치 (예: 특정 유형의 스마트폰)에 액세스 하지 못하도록 하려는 경우 사용할 수 있습니다.  포함 (하지만에 제한 되지는 않습니다)이이 클레임에 대 한 값 예제 아래 값 합니다.  
  
 아래은 해당 x-ms-클라이언트 응용 프로그램은 "Microsoft.Exchange.ActiveSync" 클라이언트에 대 한 포함 될 수 ms 사용자 에이전트 x 값 가지  
  
-   소용돌이/1.0  
  
-   Apple-iPad1C1/812.1  
  
-   Apple-iPhone3C1/811.2  
  
-   Apple-iPhone/704.11  
  
-   Moto-DROID2/4.5.1  
  
-   SAMSUNGSPHD700/100.202  
  
-   Android/0.3  
  
 이 값은 비어 가능한 이기도 합니다.  
  
### <a name="x-ms-proxy"></a>X MS 프록시  
 클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-proxy`  
  
 이 ADFS 클레임 요청이 프록시 웹 응용 프로그램을 통해 전달 된 것을 나타냅니다.  이 청구는 인증 요청 백 엔드 Federation 서비스를 전달 하는 경우 헤더를 채웁니다 웹 응용 프로그램 프록시 채워집니다. ADFS 다음 변환 클레임 합니다.  
  
 클레임 값 요청 전달 하는 웹 응용 프로그램 프록시 DNS 이름입니다.  
  
### <a name="insidecorporatenetwork"></a>InsideCorporateNetwork  
 클레임은 유형: `https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`  
  
 위의 x-ms-프록시 유사 클레임 유형,이 클레임 유형 요청 웹 응용 프로그램 프록시 통과 된 있는지 여부를 나타냅니다. 프록시 x ms-, 달리 insidecorporatenetwork 진정한 나타내는 회사의 네트워크 안에 federation 서비스에서 직접 요청와 함께 부울 값을입니다.  
  
### <a name="x-ms-endpoint-absolute-path-active-vs-passive"></a>X-MS-끝점-절대 경로 (활성와 수동)  
 클레임은 유형: `https://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path`  
  
 이와 같은 클레임 (웹 브라우저 기반) 클라이언트가 "수동"와 "활성" (풍부한) 클라이언트의 요청을 확인 하는 데 사용할 수 있습니다. 이 통해 외부 Outlook 웹 액세스, SharePoint Online 또는 Office 365 포털 풍부한 클라이언트 Microsoft Outlook 등의 요청 차단 된 동안 허용 등의 응용 프로그램 브라우저 기반 요청 합니다.  
  
 클레임 값 요청을 받은 ADFS 서비스의 이름입니다.  
  
## <a name="see-also"></a>참조 하십시오  
 [AD FS 작업](../../ad-fs/AD-FS-2016-Operations.md)
