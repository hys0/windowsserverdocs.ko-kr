---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: AD FS 2016 Single Sign On 설정
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f3719277c80eae2bf2a4d923146920d17546601d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188733"
---
# <a name="ad-fs-single-sign-on-settings"></a>AD FS Single Sign On 설정

Single Sign-on (SSO)를 사용 하면 한 번 인증 하 고 추가 자격 증명을 묻지 않고 여러 리소스에 액세스할 수 있습니다.  이 문서는이 동작을 사용자 지정할 수 있도록 하는 구성 설정 뿐만 아니라 SSO에 대 한 기본 AD FS 동작을 설명 합니다.  

## <a name="supported-types-of-single-sign-on"></a>Single Sign-on의 지원 되는 형식

AD FS에는 여러 유형의 Single Sign-on 환경 지원합니다.  
  
-   **SSO 세션**  
  
     SSO 세션 쿠키는 사용자가 특정 세션 중 응용 프로그램 전환 추가 메시지를 제거 하는 인증된 된 사용자에 대 한 기록 됩니다. 그러나 특정 세션을 종료 하는 경우는 메시지가 표시 됩니다 자격 증명에 대 한 다시 합니다.  
  
     AD FS는 쿠키를 설정할 세션 SSO 기본적으로 사용자의 장치는 등록 되지 않은 경우. 브라우저 세션 종료 하 고 다시 시작 됩니다, 경우에이 세션 쿠키 삭제 되 고 더 이상 올바르지 않습니다.  
  
-   **영구 SSO**  
  
     영구 SSO 쿠키도 영구 SSO 쿠키의 유효 사용자가 응용 프로그램에 대 한 전환 프롬프트 추가 제거 하는 인증된 된 사용자에 대 한 기록 됩니다. 영구 SSO 및 SSO 세션 간의 차이점은 영구 SSO 다양 한 세션 간에 유지 관리할 수 있습니다.  
  
     장치가 등록 되는 경우 AD FS에서 영구 SSO 쿠키를 설정 합니다. 또한 AD FS는 사용자가 "로그인 유지" 옵션을 선택 하는 경우 영구 SSO 쿠키를 설정 해야 합니다. 영구 SSO 쿠키를 유효 하지 않은 경우 더 이상, 수 거부 하 고 삭제 합니다.  
  
-   **특정 SSO 응용 프로그램**  
  
     OAuth 시나리오에서는 새로 고침 토큰은 특정 응용 프로그램의 범위 내에서 사용자의 SSO 상태를 유지 하기 위해 사용 됩니다.  
  
     AD FS가 장치를 사용 하는 경우 2012R2 AD FS 및 AD FS 2016을 사용 하 여 90 일 동안 최대 기본적으로 7 일을 사용 하는 등록된 된 장치에 대 한 영구 SSO 쿠키 수명에 따라 새로 고침 토큰의 만료 시간 설정이 장치를 등록 하는 경우 14 일 기간 내 AD FS 리소스에 액세스 합니다. 

장치가 등록 되지 않은 사용자가 "로그인 유지" 옵션을 선택 하지만 새로 고침 토큰의 만료 시간에는 "로그인 유지"의 영구 SSO 쿠키 수명을 용량이 됩니다 하는 경우 최대 7 일을 사용 하 여 기본적으로 1 일입니다. 그렇지 않은 경우 새로 고침 토큰 수명 equals 세션 SSO 쿠키 수명은 기본적으로 8 시간  
  
 위에서 설명 했 듯이 영구 SSO가 비활성화 되어 있지 않으면 등록 된 장치 사용자에 게 영구 SSO를 얻으려면 항상 됩니다. 장치 등록된 취소, 영구 SSO "로그인 상태 유지"를 사용 하 여 얻을 수 있습니다 (KMSI) 기능입니다. 
 
 Windows Server 2012 R2에 대 한 PSSO "로그인 유지" 시나리오의 경우 사용 하도록 설정 하려면이 패키지를 설치할 [핫픽스](https://support.microsoft.com/en-us/kb/2958298/) 이기도 부분을의 [Windows RT 8.1, Windows 8.1 및 Windows Server 2012 용 2014 년 8 월 업데이트 롤업 R2](https://support.microsoft.com/en-us/kb/2975719)합니다.   

태스크 | PowerShell | 설명
------------ | ------------- | -------------
영구 SSO 사용/사용 안 함 | ```` Set-AdfsProperties –EnablePersistentSso <Boolean> ````| 영구 SSO는 기본적으로 사용 됩니다. 비활성화 된 경우 PSSO 쿠키가 없는 기록 됩니다.
"사용/사용 안 함"로그인 유지" | ```` Set-AdfsProperties –EnableKmsi <Boolean> ```` | "로그인 유지" 기능은 기본적으로 해제 됩니다. 최종 사용자 AD FS 로그인 페이지에 "로그인 유지" 선택할을 표시를 사용 하는 경우



## <a name="ad-fs-2016---single-sign-on-and-authenticated-devices"></a>AD FS 2016-Single Sign-on 및 인증 된 장치
등록된 된 장치 최대 90 일로 증가는 authenticvation 14 일 이내 (장치 사용량 창)에서 요청자에 게 인증 하는 경우 AD FS 2016을 PSSO를 변경 합니다.
를 처음으로 자격 증명을 입력 한 후 기본적으로 등록 된 장치를 사용 하 여 만료 된 Single sign On 최대 90 일 동안 장치가 14 일 마다 한 번 이상 AD FS 리소스에 액세스를 사용 하 여 제공 합니다.  자격 증명을 입력 한 후 15 일을 대기 하는 경우 사용자에 게는 다시 자격 증명에 대 한 메시지가 있습니다.  

영구 SSO는 기본적으로 사용 됩니다. PSSO 쿠키가 없는 비활성화 된 경우 기록 됩니다. |  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
장치 사용 창 (기본적으로 14 일)은 AD FS 속성에 의해 관리 됩니다 **DeviceUsageWindowInDays**합니다.

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
최대 single Sign On 기간 (기본적으로 90 일)은 AD FS 속성에 의해 관리 됩니다 **PersistentSsoLifetimeMins**합니다.

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>인증 되지 않은 장치에 대 한 로그인 유지 
등록 되지 않은 장치에 대 한 단일 로그온 한 기간으로 결정 됩니다는 **유지 Me 서명에서 kmsi (로그인 유지)** 기능을 설정 합니다.  KMSI는 기본적으로 비활성화 되 고 KmsiEnabled AD FS 속성을 True로 설정 하 여 사용할 수 있습니다.

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

KMSI를 사용 하지 않도록 설정, 사용 하 여 기본 단일 로그온 기간은 8 시간입니다.  SsoLifetime 속성을 사용 하 여 구성할 수 있습니다.  속성의 기본값은 480 분 단위로 측정 됩니다.  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

KMSI 활성화를 사용 하 여 기본 single sign-on이 기간은 24 시간입니다.  KmsiLifetimeMins 속성을 사용 하 여 구성할 수 있습니다.  속성의 기본값은 1440 분 단위로 측정 됩니다.

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>Multi-factor authentication (MFA) 동작  
것에 비교적 오랜 기간 single에서 하면서 AD FS를 묻는 추가 인증 (다단계 인증)에 유의 해야 경우 이전 로그온 된 기본 자격 증명 및 없습니다 MFA를 기반으로 하지만 현재 로그온 MFA를 요구 합니다.  SSO 구성에 관계 없이입니다. AD FS 인증 요청을 받는 경우, 먼저 여부 컨텍스트가 있는 SSO (예: 쿠키)을 확인 한 다음 MFA가 필요한 경우 (처럼 요청이 들어오는에서 외부) SSO 컨텍스트에 MFA를 포함 하는지 여부를 평가 됩니다.  그렇지 않은 경우 MFA 라는 메시지가 표시 됩니다.  


  
## <a name="psso-revocation"></a>PSSO 해지  
 보안을 보호 하려면 AD FS에서 다음 조건이 충족 되 면 이전에 발급 된 모든 영구 SSO 쿠키를 거부 합니다. 사용자가 AD FS를 사용 하 여 다시 인증 하기 위해 자격 증명을 제공 해야 합니다. 
  
-   사용자가 암호 변경  
  
-   AD FS에서 영구 SSO 설정은 사용 불가능  
  
-   장치를 분실 하거나 도난당 한 경우에서 관리자가 사용할 수 있습니다.  
  
-   AD FS 사용자 등록된 되지만 해당 사용자에 대해 발급 하는 영구 SSO 쿠키를 수신 하거나 장치가 더 이상 등록 되어 있지 않습니다.  
  
-   AD FS 등록된 된 사용자에 대 한 영구 SSO 쿠키를 받지만 사용자 다시 등록 합니다.  
  
-   "로그인 유지" 하지만 "로그인 유지"의 결과로 발생 하는 영구 SSO 쿠키를 수신 하는 AD FS 설정을 AD FS에서 사용 불가능  
  
-   AD FS는 등록 된 사용자에 대해 발급 하는 영구 SSO 쿠키를 받지만 인증 중 장치 인증서가 없거나 변경  
  
-   AD FS 관리자는 영구 SSO에 대 한 마감 시간을 설정 했습니다. 이 구성 되 면 AD FS에서이 시간 전에 발급 된 모든 영구 SSO 쿠키를 거부  
  
 차단 시간을 설정 하려면 다음 PowerShell cmdlet을 실행 합니다.  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>SharePoint Online에 액세스 하려면 Office 365 사용자에 대 한 PSSO를 사용 하도록 설정  
 PSSO가 설정 되 고 AD FS에서 구성 되 면 사용자가 인증 한 후 AD FS 영구 쿠키를 작성 합니다. 영구 쿠키가 여전히 유효한 경우, 사용자는 다음에 사용자 하지 않아도 다시 인증 자격 증명을 제공 합니다. Office 365에 대 한 추가 인증 프롬프트를 방지할 수도 있습니다 및 다음 두 가지를 구성 하 여 SharePoint Online 사용자가 Microsoft Azure AD 및 SharePoint Online 트리거 지 속성에 대 한 AD FS에서 규칙을 클레임 합니다.  PSSO Office 365 사용자가 SharePoint online 액세스를 사용 하도록 설정 하려면이 패키지를 설치할 [핫픽스](https://support.microsoft.com/en-us/kb/2958298/) 이기도 부분을의 [Windows RT 8.1, Windows 8.1 및 Windows Server 2012 R2용2014년8월업데이트롤업](https://support.microsoft.com/en-us/kb/2975719).  
  
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
  
요약:
<table>
  <tr>
    <th colspan="1">Single sign On 환경</th>
    <th colspan="3">ADFS 2012 R2 <br> 장치 등록</th>
        <th colspan="1"></th>
    <th colspan="3">ADFS 2016 <br> 장치 등록</th>
  </tr>

  <tr align="center">
    <th></th>
    <th>아니요</th>
    <th>KMSI 있지만 없음</th>
    <th>예</th>
    <th></th>
    <th>아니요</th>
    <th>KMSI 있지만 없음</th>
    <th>예</th>
  </tr>
 <tr align="center">
    <td>SSO = > 새로 고침 토큰 설정 = ></td>
    <td>8 시간</td>
    <td>해당 사항 없음</td>
    <td>해당 사항 없음</td>
    <th></th>
    <td>8 시간</td>
    <td>해당 사항 없음</td>
    <td>해당 사항 없음</td>
  </tr>

 <tr align="center">
    <td>PSSO=>set Refresh Token=></td>
    <td>해당 사항 없음</td>
    <td>24 시간</td>
    <td>7 일</td>
    <th></th>
    <td>해당 사항 없음</td>
    <td>24 시간</td>
    <td>최대 14 일 창 사용 하 여 90 일</td>
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

**등록 된 장치가 있습니까?** PSSO 얻게 / 영구 SSO <br>
**장치를 등록 하지?** SSO를 얻으려면 <br>
**KMSI 있지만 장치를 등록 하지?** PSSO 얻게 / 영구 SSO <p>
IF:
 - [KMSI 기능 [및] x] 관리자가 사용 하도록 설정
 - [x] 사용자가 forms 로그인 페이지에서 KMSI 확인란을 클릭합니다.
 
**Good 알아야 합니다.** <br>
권한이 없는 사용자를 페더레이션 합니다 **LastPasswordChangeTimestamp** 특성이 동기화 세션 쿠키 및 새로 고침 토큰을 발급 한를 **12 시간의 최대 기간 값**합니다.<br>
Azure AD는 이전 자격 증명 (예: 변경 된 암호)와 관련 된 토큰을 해지할 시기를 확인할 수 없으므로 발생 합니다. 따라서 Azure AD 사용자와 연결 된 토큰이 여전히 양호한 상태에에서는 있는지 자주 확인 해야 합니다.
