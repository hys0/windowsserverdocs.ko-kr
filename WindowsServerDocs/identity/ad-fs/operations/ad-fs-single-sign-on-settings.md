---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: AD FS 2016 Single Sign On 설정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 311789fdec160faeeeba0ecf26491d1e0cd6105d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407390"
---
# <a name="ad-fs-single-sign-on-settings"></a>Single Sign-on 설정 AD FS

SSO (Single Sign-on)를 사용 하면 사용자가 한 번 인증 하 고 추가 자격 증명을 묻는 메시지가 표시 되지 않고 여러 리소스에 액세스할 수 있습니다.  이 문서에서는이 동작을 사용자 지정할 수 있도록 하는 구성 설정 뿐만 아니라 SSO의 기본 AD FS 동작에 대해 설명 합니다.  

## <a name="supported-types-of-single-sign-on"></a>지원 되는 Single Sign-on 유형

AD FS는 여러 유형의 Single Sign-on 환경을 지원 합니다.  
  
-   **세션 SSO**  
  
     세션 SSO 쿠키는 인증 된 사용자에 대해 기록 되며, 사용자가 특정 세션 중에 응용 프로그램을 전환할 때 추가 프롬프트를 제거 합니다. 그러나 특정 세션이 종료 되 면 사용자에 게 자격 증명을 다시 입력 하 라는 메시지가 표시 됩니다.  
  
     사용자의 장치가 등록 되지 않은 경우 기본적으로 세션 SSO 쿠키를 설정 AD FS 합니다. 브라우저 세션이 종료 되 고 다시 시작 되 면이 세션 쿠키가 삭제 되 고 더 이상 유효 하지 않습니다.  
  
-   **영구 SSO**  
  
     영구 sso 쿠키가 유효한 경우에만 사용자가 응용 프로그램을 전환할 때 추가 프롬프트를 제거 하는 인증 된 사용자에 대해 영구 SSO 쿠키가 작성 됩니다. 영구 SSO와 세션 SSO의 차이점은 영구 SSO가 여러 세션에서 유지 관리 될 수 있다는 것입니다.  
  
     장치가 등록 되는 경우 영구적 SSO 쿠키를 설정 AD FS 합니다. 사용자가 "로그인 유지" 옵션을 선택 하는 경우에도 AD FS에서 영구 SSO 쿠키를 설정 합니다. 영구적 SSO 쿠키가 더 이상 유효 하지 않으면 거부 되 고 삭제 됩니다.  
  
-   **응용 프로그램별 SSO**  
  
     OAuth 시나리오에서 새로 고침 토큰은 특정 응용 프로그램의 범위 내에서 사용자의 SSO 상태를 유지 관리 하는 데 사용 됩니다.  
  
     장치가 등록 되 면 AD FS는 등록 된 장치에 대 한 영구 SSO 쿠키 수명을 기반으로 하는 새로 고침 토큰의 만료 시간을 설정 합니다 .이는 AD FS 2012R2 2의 경우 기본적으로 7 일이 고 장치를 사용 하는 경우 최대 90 일을 사용 하는 경우 AD FS 2016입니다. 14 일 기간 내에 AD FS 리소스에 액세스 합니다. 

장치가 등록 되어 있지 않지만 사용자가 "로그인 유지" 옵션을 선택 하면 새로 고침 토큰의 만료 시간이 "로그인 유지"에 대 한 영구 SSO 쿠키 수명 (기본적으로 최대 7 일)이 됩니다. 그렇지 않은 경우 새로 고침 토큰 수명은 세션 SSO 쿠키 수명과 같으며 기본값은 8 시간입니다.  
  
 위에서 설명한 대로, 영구 SSO를 사용 하지 않는 한 등록 된 장치의 사용자는 항상 영구 SSO를 가져옵니다. 등록 되지 않은 장치의 경우 "로그인 유지" (KMSI) 기능을 사용 하도록 설정 하 여 영구 SSO를 구현할 수 있습니다. 
 
 Windows Server 2012 r 2의 경우 "로그인 유지" 시나리오에 대해 PSSO를 사용 하도록 설정 하려면 [WINDOWS RT 8.1, Windows 8.1 및 Windows Server 2012 r 2 용 8 월 2014 업데이트 롤업](https://support.microsoft.com/en-us/kb/2975719)의 일부인이 [핫픽스](https://support.microsoft.com/en-us/kb/2958298/) 를 설치 해야 합니다.   

태스크 | PowerShell | 설명
------------ | ------------- | -------------
영구 SSO 사용/사용 안 함 | ```` Set-AdfsProperties –EnablePersistentSso <Boolean> ````| 영구 SSO는 기본적으로 사용 하도록 설정 되어 있습니다. 사용 하지 않도록 설정 된 경우 PSSO 쿠키가 작성 되지 않습니다.
"로그인 유지/사용 안 함" | ```` Set-AdfsProperties –EnableKmsi <Boolean> ```` | "로그인 유지" 기능은 기본적으로 사용 하지 않도록 설정 되어 있습니다. 사용 하도록 설정 된 경우 최종 사용자에 게 AD FS 로그인 페이지에 "로그인 유지" 선택이 표시 됩니다.



## <a name="ad-fs-2016---single-sign-on-and-authenticated-devices"></a>AD FS 2016-Single Sign-on 및 인증 된 장치
AD FS 2016은 요청 자가 등록 된 장치에서 최대 90 일로 늘어나고 14 일 내에 인증을 요청 하는 경우 (장치 사용 기간) PSSO를 변경 합니다.
처음으로 자격 증명을 제공한 후에 등록 된 장치를 사용 하는 사용자는 최대 90 일 동안 single Sign-on을 받습니다 .이 경우 장치를 사용 하 여 14 일 마다 한 번 이상 AD FS 리소스에 액세스할 수 있습니다.  자격 증명을 제공한 후 15 일 동안 기다리면 사용자에 게 자격 증명을 묻는 메시지가 다시 표시 됩니다.  

영구 SSO는 기본적으로 사용 하도록 설정 되어 있습니다. 사용 하지 않도록 설정 된 경우 PSSO 쿠키가 작성 되지 않습니다. |  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
장치 사용 기간 (기본적으로 14 일)은 AD FS 속성 **DeviceUsageWindowInDays**에 의해 제어 됩니다.

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
최대 single Sign-on 기간 (기본적으로 90 일)은 AD FS 속성 **PersistentSsoLifetimeMins**에 의해 제어 됩니다.

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>인증 되지 않은 장치에 대해 로그인 상태 유지 
등록 되지 않은 장치의 경우 **로그인 유지 (KMSI)** 기능 설정에 따라 Single Sign-On 기간이 결정 됩니다.  KMSI는 기본적으로 사용 하지 않도록 설정 되어 있으며, AD FS 속성 KmsiEnabled를 True로 설정 하 여 사용 하도록 설정할 수 있습니다.

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

KMSI를 사용 하지 않도록 설정 하면 기본 Single Sign-On 기간은 8 시간입니다.  SsoLifetime 속성을 사용 하 여 구성할 수 있습니다.  속성은 분 단위로 측정 되므로 기본값은 480입니다.  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

KMSI를 사용 하는 경우 기본 Single Sign-On 기간은 24 시간입니다.  KmsiLifetimeMins 속성을 사용 하 여 구성할 수 있습니다.  속성은 분 단위로 측정 되므로 기본값은 1440입니다.

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>MFA (multi-factor authentication) 동작  
비교적 긴 single AD FS sign-on을 제공 하는 동안 이전 로그온이 MFA가 아닌 기본 자격 증명을 기반으로 하 고 현재 로그온 한 경우 추가 인증 (multi-factor authentication)을 요청 하는 것을 확인 하는 것이 중요 합니다. MFA 필요  이는 SSO 구성에 관계 없이입니다. AD FS 인증 요청을 받을 때는 먼저 SSO 컨텍스트 (예: 쿠키)가 있는지 여부를 확인 한 다음 MFA가 필요한 경우 (예: 요청이 외부에서 들어오는 경우) SSO 컨텍스트가 MFA를 포함 하는지 여부를 평가 합니다.  그렇지 않으면 MFA에 메시지가 표시 됩니다.  


  
## <a name="psso-revocation"></a>PSSO 해지  
 보안을 보호 하기 위해 AD FS는 다음 조건이 충족 될 때 이전에 발급 된 영구 SSO 쿠키를 거부 합니다. 이렇게 하려면 사용자가 다시 AD FS으로 인증 하려면 자격 증명을 제공 해야 합니다. 
  
- 사용자가 암호 변경  
  
- 영구 SSO 설정은 AD FS에서 사용 되지 않습니다.  
  
- 장치를 분실 하거나 도난당 한 경우 관리자가 사용 하지 않도록 설정 됨  
  
- AD FS는 등록 된 사용자에 대해 발급 된 영구 SSO 쿠키를 받지만 사용자 또는 장치가 더 이상 등록 되지 않았습니다.  
  
- AD FS는 등록 된 사용자에 대 한 영구 SSO 쿠키를 받지만 사용자가 다시 등록 되었습니다.  
  
- AD FS는 "로그인 유지"의 결과로 발급 된 영구 SSO 쿠키를 수신 하지만, "로그인 유지" 설정은에서 사용할 수 없습니다 AD FS  
  
- AD FS는 등록 된 사용자에 대해 발급 되었지만 인증 중에 장치 인증서가 없거나 변경 된 영구 SSO 쿠키를 수신 합니다.  
  
- AD FS 관리자가 영구 SSO에 대 한 구분 시간을 설정 했습니다. 이를 구성 하는 경우이 시간 이전에 실행 된 영구 SSO 쿠키를 거부 AD FS 합니다.  
  
  구분 시간을 설정 하려면 다음 PowerShell cmdlet을 실행 합니다.  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>Office 365 사용자가 SharePoint Online에 액세스할 수 있도록 PSSO 사용  
 PSSO를 사용 하도록 설정 하 고 AD FS에서 구성한 후에는 사용자가 인증 된 후 영구 쿠키를 작성 AD FS. 다음에 사용자가 들어올 때 영구 쿠키가 여전히 유효한 경우 사용자는 다시 인증을 위해 자격 증명을 제공할 필요가 없습니다. AD FS에서 다음 두 클레임 규칙을 구성 하 여 Microsoft Azure AD 및 SharePoint Online에서 지 속성을 트리거하는 방법으로 Office 365 및 SharePoint Online 사용자에 대 한 추가 인증 프롬프트를 방지할 수도 있습니다.  Office 365 사용자가 SharePoint online에 액세스할 수 있도록 PSSO를 사용 하도록 설정 하려면이 [핫픽스](https://support.microsoft.com/en-us/kb/2958298/) 를 설치 해야 합니다 .이 핫픽스는 [windows RT 8.1, Windows 8.1 및 windows Server 2012 r 2 용 8 월 2014 업데이트 롤업](https://support.microsoft.com/en-us/kb/2975719)의 일부 이기도 합니다.  
  
 InsideCorporateNetwork 클레임을 통과 하는 발급 변환 규칙  
  
```  
@RuleTemplate = "PassThroughClaims"  
@RuleName = "Pass through claim - InsideCorporateNetwork"  
c:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork"]  
=> issue(claim = c);   
A custom Issuance Transform rule to pass through the persistent SSO claim  
@RuleName = "Pass Through Claim - Psso"  
c:[Type == "http://schemas.microsoft.com/2014/03/psso"]  
=> issue(claim = c);  
  
```
  
요약 하면 다음과 같습니다.
<table>
  <tr>
    <th colspan="1">단일 SignOn 환경</th>
    <th colspan="3">ADFS 2012 R2 <br> 장치가 등록 되나요?</th>
        <th colspan="1"></th>
    <th colspan="3">ADFS 2016 <br> 장치가 등록 되나요?</th>
  </tr>

  <tr align="center">
    <th></th>
    <th>아니요</th>
    <th>아니요, KMSI</th>
    <th>예</th>
    <th></th>
    <th>아니요</th>
    <th>아니요, KMSI</th>
    <th>예</th>
  </tr>
 <tr align="center">
    <td>SSO =&gt;새로 고침 토큰 설정 =&gt;</td>
    <td>8 시간</td>
    <td>해당 사항 없음</td>
    <td>해당 사항 없음</td>
    <th></th>
    <td>8 시간</td>
    <td>해당 사항 없음</td>
    <td>해당 사항 없음</td>
  </tr>

 <tr align="center">
    <td>Pss\=&gt;set Refresh Token =&gt;</td>
    <td>해당 사항 없음</td>
    <td>24 시간</td>
    <td>7 일</td>
    <th></th>
    <td>해당 사항 없음</td>
    <td>24 시간</td>
    <td>최대 90 일 동안 14 일 기간</td>
  </tr>

 <tr align="center">
    <td>토큰 수명</td>
    <td>1 시간</td>
    <td>1 시간</td>
    <td>1 시간</td>
    <th></th>
    <td>1 시간</td>
    <td>1 시간</td>
    <td>1 시간</td>
  </tr>
</table>

**등록 된 장치 인가요?** PSSO/Persistent SSO를 가져옵니다. <br>
**장치를 등록 하지 않나요?** SSO를 가져옵니다. <br>
**장치를 등록 하지 않았지만 KMSI?** PSSO/Persistent SSO를 가져옵니다. <p>
때
 - [x] 관리자가 KMSI 기능 [및]을 사용 하도록 설정 했습니다.
 - [x] 사용자가 양식 로그인 페이지에서 KMSI 확인란을 클릭 합니다.
 
**잘 알고 있어야 합니다.** <br>
**Lastpasswordchangetimestamp** 특성이 동기화 되지 않은 페더레이션된 사용자에 게는 **최대 기간 값이 12 시간인**발급 된 세션 쿠키 및 새로 고침 토큰이 발급 됩니다.<br>
이는 Azure AD가 이전 자격 증명과 관련 된 토큰 (예: 변경 된 암호)을 해지할 시점을 결정할 수 없기 때문에 발생 합니다. 따라서 Azure AD는 사용자 및 연결 된 토큰이 여전히 적절 한 상태에 있는지 확인 하기 위해 더 자주 확인 해야 합니다.
