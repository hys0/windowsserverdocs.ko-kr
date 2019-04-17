---
ms.assetid: 96b9f4e6-f01c-4517-8299-017d187d447e
title: "인증 방법을 클레임 보내려면 규칙 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4065a61e042f52298da656899289e718e010f932
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-rule-to-send-an-authentication-method-claim"></a>인증 방법을 클레임 보내려면 규칙 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

사용할 수 있습니다는 **클레임으로 그룹 구성원 보내기** 규칙 템플릿 또는 **들어오는 주장 변환** 규칙 템플릿 인증 방법을 클레임 보낼 수 있습니다. 당사자 Active Directory Federation Services \(AD FS\)에서 인증 하 고 얻을를 사용 하 여 사용자의 로그온 메커니즘 맞는지 확인 하는 인증 방법을 클레임을 사용할 수 있습니다. 인증 방법을 클레임 있는 당사자 스마트 카드 로그온 기반 액세스 수준을 확인 하려는 경우 얻기 위해 입력으로 Windows Server 2012 r 2에서의 Active Directory Federation Services \(AD FS\) 인증 메커니즘 보증 기능을 사용할 수도 있습니다. 예를 들어, 개발자 신뢰 파티 응용 프로그램의 연결 된 사용자에 게 다양 한 수준의 액세스를 지정할 수 있습니다. 액세스 수준은 기준으로 사용자가 여부 사용자 이름 및 암호 자격 증명, 스마트 카드 것이 아니라 사용 하 여 로그온 합니다.  
  
회사의 요구 사항에 따라 다음 절차 중 하나를 사용 합니다.  
  
-   이 규칙을 사용 하 여 만들기는 **클레임으로 그룹 구성원 보내기** 규칙 템플릿 \-이 최종적으로 인증 방법을 결정이 템플릿을에 지정 된 그룹 주장 실행 하는 경우이 규칙 템플릿을 사용할 수 있습니다.  
  
-   이 규칙을 사용 하 여 만들기는 **수신 클레임 변환** 규칙 템플릿 \-기존 인증 방법을 표준 ADFS 인증 방법을 클레임 인식 되지 않는 제품을 사용 하는 새 인증 방법으로 변경 하려는 경우이 규칙 템플릿을 사용할 수 있습니다.  
  


## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>필요로 하 파티 신뢰 Windows Server 2016에 클레임 규칙 템플릿으로 보내기 그룹 구성원을 사용 하 여 만들기 

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임으로 그룹 구성원 보내기** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  클릭 **찾아보기**, 그룹 구성원이이 인증 방법을 클레임 수신를 클릭 한 다음 선택 **확인**합니다.  
  
8.  **보내는 클레임 유형**선택 **인증 방법을** 목록에 있습니다.  
  
9. **클레임 값을 보내는**, 선호 인증 방법에 따라 다음 표에서에 입력 기본값이 식별자 \(URI\) 중 하나를 클릭 **완료**를 차례로 클릭 하 고 **확인** 규칙을 저장 해야 합니다.  
  
|실제 인증 방법|해당 URI|  
|--------------------------------|---------------------|  
|사용자 이름 및 암호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 인증서를 사용 하는 transport Layer Security \(TLS\) 상호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS 사용 하지 않는 X.509\ 기반 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)
  
## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Windows Server 2016에 클레임 공급자 신뢰에 클레임 규칙 템플릿으로 보내기 그룹 구성원을 사용 하 여 만들기 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **클레임 공급자 신뢰**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **편집 클레임 규칙** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임으로 그룹 구성원 보내기** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  클릭 **찾아보기**, 그룹 구성원이이 인증 방법을 클레임 수신를 클릭 한 다음 선택 **확인**합니다.  
  
8.  **보내는 클레임 유형**선택 **인증 방법을** 목록에 있습니다.  
  
9. **클레임 값을 보내는**, 선호 인증 방법에 따라 다음 표에서에 입력 기본값이 식별자 \(URI\) 중 하나를 클릭 **완료**를 차례로 클릭 하 고 **확인** 규칙을 저장 해야 합니다.  
  
|실제 인증 방법|해당 URI|  
|--------------------------------|---------------------|  
|사용자 이름 및 암호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 인증서를 사용 하는 transport Layer Security \(TLS\) 상호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS 사용 하지 않는 X.509\ 기반 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)


## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>들어오는 주장 필요로 하 파티 신뢰 Windows Server 2016에 규칙 템플릿이이 규칙 변환을 사용 하 여 만들기 

1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **파티 신뢰 의존**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **클레임 발급 정책 편집**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  에 **클레임 발급 정책 편집** 대화 상자의 **발급 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **수신 클레임 변환** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**, **인증 방법을** 목록에 있습니다.  
  
8.  **보내는 클레임 유형**선택 **인증 방법을** 목록에 있습니다.  
  
9. 선택 **수신 클레임 값을 바꿉니다 다른 보내는 클레임**, 다음을 수행 하 고 다음과 같습니다.  
  
    1.  **클레임 값을 수신**입력 URI 값 원래 사용 했던 URI 실제 인증 방법에 따라 다음 중 하나를 클릭 **완료**, 클릭 한 다음 **확인** 규칙을 저장 해야 합니다.  
  
    2.  **클레임 값을 보내는**, 새 기본 설정된 인증 방법 선택 항목에 따라 달라 집니다 다음 표에서에 입력 기본값 URI 중 하나를 클릭 **완료**을 차례로 클릭 하 고 **확인** 규칙을 저장 해야 합니다.  
  
|실제 인증 방법|해당 URI|  
|--------------------------------|---------------------|  
|사용자 이름 및 암호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 인증서를 사용 하 여 상호 인증 TLS|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS 사용 하지 않는 X.509\ 기반 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)
  
> [!NOTE]  
> 테이블에 값 뿐만 아니라 다른 URI 값을 사용할 수 있습니다. URI 값 이온 표시 되는 위의 표 당사자 기본적으로 허용 Uri 반영 합니다.  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>들어오는 주장 Windows Server 2016에 클레임 공급자 신뢰에 규칙 템플릿이이 규칙 변환을 사용 하 여 만들기 
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 **ADFS**, 클릭 **클레임 공급자 신뢰**합니다. 
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  에 **편집 클레임 규칙** 대화 상자의 **수용 변환 규칙** 클릭 **규칙 추가** 규칙 마법사를 시작 합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **수신 클레임 변환** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**, **인증 방법을** 목록에 있습니다.  
  
8.  **보내는 클레임 유형**선택 **인증 방법을** 목록에 있습니다.  
  
9. 선택 **수신 클레임 값을 바꿉니다 다른 보내는 클레임**, 다음을 수행 하 고 다음과 같습니다.  
  
    1.  **클레임 값을 수신**입력 URI 값 원래 사용 했던 URI 실제 인증 방법에 따라 다음 중 하나를 클릭 **완료**, 클릭 한 다음 **확인** 규칙을 저장 해야 합니다.  
  
    2.  **클레임 값을 보내는**, 새 기본 설정된 인증 방법 선택 항목에 따라 달라 집니다 다음 표에서에 입력 기본값 URI 중 하나를 클릭 **완료**을 차례로 클릭 하 고 **확인** 규칙을 저장 해야 합니다.  
  
|실제 인증 방법|해당 URI|  
|--------------------------------|---------------------|  
|사용자 이름 및 암호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 인증서를 사용 하 여 상호 인증 TLS|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS 사용 하지 않는 X.509\ 기반 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)























## <a name="to-create-this-rule-by-using-the-send-group-membership-as-claims-rule-template-in-windows-server-2012-r2"></a>이 규칙 Windows Server 2012 r 2에서 클레임 규칙 템플릿으로 보내기 그룹 구성원을 사용 하 여 만들기  
  
1.  서버 관리자 클릭 **도구**를 선택한 다음 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래에서 **광고 FS\\Trust 관계**, 클릭 **클레임 공급자 신뢰** 또는 **의존 파티 신뢰**, 클릭 한 다음이 규칙 만들려는 목록에 특정 신뢰 하 고 합니다.  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  
  
4.  에 **클레임 규칙 편집** 대화 상자에서 하나 다음 탭, 보안 편집 하는 및 규칙을 설정에 따라를 만들려면이 규칙을 선택한 다음 **규칙 추가** 해당 규칙 집합와 연결 된 규칙 마법사를 시작 합니다.  
  
    -   **승인 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 승인 규칙**  
  
    -   **위임 인증 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
    
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **클레임으로 그룹 구성원 보내기** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)
  
6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  클릭 **찾아보기**, 그룹 구성원이이 인증 방법을 클레임 수신를 클릭 한 다음 선택 **확인**합니다.  
  
8.  **보내는 클레임 유형**선택 **인증 방법을** 목록에 있습니다.  
  
9. **클레임 값을 보내는**, 선호 인증 방법에 따라 다음 표에서에 입력 기본값이 식별자 \(URI\) 중 하나를 클릭 **완료**를 차례로 클릭 하 고 **확인** 규칙을 저장 해야 합니다.  
  
|실제 인증 방법|해당 URI|  
|--------------------------------|---------------------|  
|사용자 이름 및 암호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 인증서를 사용 하는 transport Layer Security \(TLS\) 상호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS 사용 하지 않는 X.509\ 기반 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth1.PNG)
 
> [!NOTE]  
> 테이블에 값 뿐만 아니라 다른 URI 값을 사용할 수 있습니다. 위의 표에 표시 되는 URI 값 당사자 기본적으로 허용 Uri 반영 합니다.  
  
## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>이 규칙 사용 하 여 만들기 변환 들어오는 클레임 규칙 서식 Windows Server 2012 r 2  
   
  
  
1.  서버 관리자 클릭 **도구**을 차례로 클릭 하 고 **AD FS 관리**합니다.  
  
2.  콘솔 트리에서 아래에서 **광고 FS\\Trust 관계**, 클릭 **클레임 공급자 신뢰** 또는 **의존 파티 신뢰**, 클릭 한 다음이 규칙 만들려는 목록에 특정 신뢰 하 고 합니다.  
  
3.  선택한 신뢰 Right\ 클릭 하 고 다음 클릭 **편집 클레임 규칙**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
 
4.  에 **클레임 규칙 편집** 대화 상자를 선택 하 고 편집 하는 어떤 규칙을 설정 하 고 신뢰에 따라 달라 집니다는 다음과 같은 탭 만들려는이 규칙을 클릭 한 다음 **규칙 추가** 해당 규칙 집합와 연결 된 규칙 마법사를 시작 합니다.  
  
    -   **승인 변환 규칙**  
  
    -   **발급 변환 규칙**  
  
    -   **발급 승인 규칙**  
  
    -   **위임 인증 규칙**  
![규칙 만들기](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  에 **규칙 템플릿 선택** 페이지의 **클레임 규칙 서식**선택 **수신 클레임 변환** 목록에서 **다음**합니다.  
![규칙 만들기](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)    
  
6.  에 **구성 규칙** 페이지에서 클레임 규칙 이름을 입력 합니다.  
  
7.  **수신 클레임 유형**, **인증 방법을** 목록에 있습니다.  
  
8.  **보내는 클레임 유형**선택 **인증 방법을** 목록에 있습니다.  
  
9. 선택 **수신 클레임 값을 바꿉니다 다른 보내는 클레임**, 다음을 수행 하 고 다음과 같습니다.  
  
    1.  **클레임 값을 수신**입력 URI 값 원래 사용 했던 URI 실제 인증 방법에 따라 다음 중 하나를 클릭 **완료**, 클릭 한 다음 **확인** 규칙을 저장 해야 합니다.  
  
    2.  **클레임 값을 보내는**, 새 기본 설정된 인증 방법 선택 항목에 따라 달라 집니다 다음 표에서에 입력 기본값 URI 중 하나를 클릭 **완료**을 차례로 클릭 하 고 **확인** 규칙을 저장 해야 합니다.  
  
|실제 인증 방법|해당 URI|  
|--------------------------------|---------------------|  
|사용자 이름 및 암호 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password|  
|Windows 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows|  
|X.509 인증서를 사용 하 여 상호 인증 TLS|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient|  
|TLS 사용 하지 않는 X.509\ 기반 인증|https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509|  
![규칙 만들기](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth3.PNG)
  
> [!NOTE]  
> 테이블에 값 뿐만 아니라 다른 URI 값을 사용할 수 있습니다. URI 값 이온 표시 되는 위의 표 당사자 기본적으로 허용 Uri 반영 합니다.  

## <a name="additional-references"></a>추가 참조 
[클레임은 규칙 구성](Configure-Claim-Rules.md)  
 
[검사: 신뢰 파티 보안에 대 한 청구 규칙 만들기](https://technet.microsoft.com/library/ee913578.aspx)  

[청구 공급자에 대 한 청구 규칙 만들기 신뢰 검사:](https://technet.microsoft.com/library/ee913564.aspx)  
  
[승인 클레임 규칙을 사용 하는 경우](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[클레임 역할](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[클레임은 규칙의 역할](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
