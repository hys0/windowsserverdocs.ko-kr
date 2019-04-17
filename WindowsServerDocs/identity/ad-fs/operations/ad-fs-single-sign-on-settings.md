---
ms.assetid: 1a443181-7ded-4912-8e40-5aa447faf00c
title: "광고 FS 2016 설정에서 단일 기호"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 08/17/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e8c24399949efc1b8d0b1782e299593c02374c62
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="ad-fs-single-sign-on-settings"></a>광고 FS 단일 Sign-on 설정

>적용 대상: Windows Server 2016, Windows Server 2012 r 2

Single Sign-on SSO () 사용자를 한 번 인증 하 고 추가 자격 증명 입력 하지 않고도 여러 리소스에 액세스할 수 있습니다.  이 문서에서는 SSO,이 문제를 사용자 지정할 수 있도록 구성 설정에 대 한 기본 ADFS 동작을 설명 합니다.  

## <a name="supported-types-of-single-sign-on"></a>지원 되는 종류의 Single Sign-on

ADFS 여러 가지 유형의 Single Sign-on 경험을 지원합니다.  
  
-   **세션 SSO**  
  
     세션 SSO 쿠키는 사용자가 특정 세션 동안 응용 프로그램 전환 때 추가 메시지를 제거 하는 인증 된 사용자 기록 됩니다. 그러나 특정 세션 종료 되는 경우 사용자가 묻는 자격 증명 다시.  
  
     Adfs가 설정 세션 SSO 쿠키 기본적으로 사용자의 장치를 등록 되지 않은 경우 합니다. 브라우저 세션 종료 및 다시 시작,이 세션 쿠키 삭제 되 고 더 이상 유효 하지 않습니다.  
  
-   **영구 SSO**  
  
     영구 SSO 쿠키 영구 SSO 쿠키는 올바른으로 응용 프로그램에 대 한 간을 전환할 메시지가 더 이상 제거 인증 된 사용자 기록 됩니다. 영구 SSO 및 세션 SSO 간의 차이점은 영구 SSO 서로 다른 여러 세션에서 유지 될 수 있습니다.  
  
     장치를 등록 한 경우 ADFS 영구 SSO 쿠키를 설정 합니다. Adfs은 사용자가 "유지 안 함 로그인 나" 옵션을 선택할 경우 영구 SSO 쿠키를 설정할 수도 있습니다. 영구 SSO 쿠키 유효 하지 않으면 더 이상, 거부 하 고 삭제 될 됩니다.  
  
-   **특정 SSO 응용 프로그램**  
  
     OAuth 시나리오에서 새로 고침 토큰 특정 응용 프로그램의 범위 내에서 사용자의 SSO 상태를 유지 하는 데 사용 됩니다.  
  
     디바이스에 등록 한 경우 Adfs의 새로 고침 토큰은 7 일 있는 등록 된 디바이스에 대 한 지속적인 SSO 쿠키 수명 기본적으로 기반 만료 시간을 설정 합니다. 새로 고침 토큰의 만료 시간 "유지 로그인 나"에 대 한 지속적인 SSO 쿠키 수명 용량이 됩니다 "유지 안 함 로그인 나" 옵션을 선택 하는 경우는 7 일 최대 기본적으로 1 일 합니다. 그렇지 않으면 토큰 수명 같음 세션 SSO 쿠키 수명은 기본적으로 8 시간 새로 고침  
  
 위에서 언급 한 대로 영구 SSO 비활성화 되어 있지 않으면 등록 된 디바이스에서 사용자가 영구 SSO 얻게 항상 됩니다. 없다고 등록 된 디바이스에 대 한 지속적인 SSO "유지 로그인 알림"을 사용 하 여 얻을 수 있습니다 (KMSI) 기능이 있습니다. 
 
 Windows Server 2012 r 2에 대 한 PSSO "유지 안 함 로그인 나" 시나리오에 대 한 사용 하도록 설정 하려면이 설치 [핫픽스](https://support.microsoft.com/en-us/kb/2958298/) 이기도의 일부로의 [Windows RT 8.1, Windows 8.1, 및 Windows Server 2012 r 2 용 업데이트 롤업 2014 년 8 월](https://support.microsoft.com/en-us/kb/2975719)합니다.   
 
  
## <a name="single-sign-on-and-authenticated-devices"></a>Single Sign-on 및 인증 된 디바이스  
후 자격 증명에 처음으로 제공 하 기본적으로 등록 된 디바이스와 사용자가 다운로드 single Sign-on 최대 90 일 동안 제공 자녀가 디바이스를 사용 하 여 14 일에 한 번 이상 ADFS 리소스에 액세스할 수 있습니다.  자녀가 자격 증명을 입력 한 후 15 일 동안 대기한 후, 경우 사용자는 다시 자격 증명에 나타납니다.  

영구 SSO 기본적으로 활성화 됩니다. 비활성화 되어 있으면 없이 PSSO 쿠키를 작성할 수는 있습니다. |  

``` powershell
Set-AdfsProperties –EnablePersistentSso <Boolean\>
```     
  
장치 사용 창 (기본적으로 14 일)에 ADFS 속성에서 적용 **DeviceUsageWindowInDays**합니다.

``` powershell
Set-AdfsProperties -DeviceUsageWindowInDays
```   
ADFS 속성에서 최대 single Sign-on 기간 (기본적으로 90 일)에 적용 **PersistentSsoLifetimeMins**합니다.

``` powershell
Set-AdfsProperties -PersistentSsoLifetimeMins
```    

## <a name="keep-me-signed-in-for-unauthenticated-devices"></a>인증 되지 않은 디바이스에 대 한 로그인 상태 유지 
비 등록 된 디바이스에 대 한 단일 로그온 기간에 따라 결정 됩니다는 **나 기록에 (KMSI) 유지** 기능을 설정 합니다.  KMSI는 기본적으로 비활성화 되 고 KmsiEnabled ADFS 속성을 설정 하 여 사용할 수 있습니다.

``` powershell
Set-AdfsProperties -EnableKmsi $true  
```    

사용 하지 않도록 설정 KMSI와 기본 단일 로그온 기간은 8 시간 합니다.  사용 하 여 SsoLifetime 속성 구성할 수 있습니다.  기본값은 480 하므로 분 속성 측정 됩니다.  

``` powershell
Set-AdfsProperties –SsoLifetime <Int32\> 
```   

사용 KMSI와 기본 단일 로그온 기간 24 시간입니다.  사용 하 여 KmsiLifetimeMins 속성 구성할 수 있습니다.  기본값은 1440 하므로 분 속성 측정 됩니다.

``` powershell
Set-AdfsProperties –KmsiLifetimeMins <Int32\> 
```   

## <a name="multi-factor-authentication-mfa-behavior"></a>다중 요소 인증 (MFA) 동작  
사항에 유의 하세요 때에서 이전 로그인을 주 자격 증명 하 고 있지 MFA 기반 하지만에 로그인을 하면 현재 MFA 요구에 단일 로그인 상대적으로 오랜 기간 ADFS (다중 요소 인증) 추가 인증에 대 한 물어봅니다 제공 하는 동안을 고려해 야 합니다.  SSO 구성에 관계 없이입니다. ADFS, 인증 요청을 받는 경우 먼저 (예: 쿠키) SSO 컨텍스트가 되는지 여부를 결정 다음 MFA 해야 하는 경우 (등 요청은에서 들어오는 외부) SSO 컨텍스트가 포함 MFA 여부 평가 됩니다.  그렇지 않으면 MFA 라는 메시지가 표시 됩니다.  


  
## <a name="psso-revocation"></a>PSSO 해지  
 보안을 보호 하기 위해 Adfs은 다음 조건을 충족 하는 경우 이전에 발행 된 영구 SSO 쿠키를 거부 합니다. 자격 증명을 다시 ADFS 인증 하기 위해 제공 하기 위해 사용자가 필요 합니다. 
  
-   암호 변경  
  
-   Adfs의 영구 SSO 설정은 사용 안 함  
  
-   장치를 분실 하거나 도난당 한 경우에는 관리자가 사용할 수 있습니다.  
  
-   ADFS 등록된 된 사용자는 사용자에 대해 발급 영구 SSO 쿠키를 받거나 디바이스가 더 이상 등록 되지 않습니다.  
  
-   ADFS 등록된 사용자에 대 한 지속적인 SSO 쿠키 받지만 사용자 다시 등록  
  
-   ADFS 수신 "유지 안 함 로그인 나" 하지만 "로그인 나 보관"으로 인해 발생 하는 지속적인 SSO 쿠키 Adfs에서 설정을 사용 안 함  
  
-   ADFS 등록된 사용자에 대해 발급 된 영구 SSO 쿠키 받지만 인증 하는 동안 장치 인증서가 손실 되거나 변경  
  
-   광고 FS 관리자 영구 sso 마감 시간을 설정 했습니다. Adfs이이 시간 전에 발급 한 모든 영구 SSO 쿠키는 거부이 구성 된 경우  
  
 구분 시간을 설정 하려면 다음 PowerShell cmdlet을 실행 합니다.  
  

``` powershell
Set-AdfsProperties -PersistentSsoCutoffTime <DateTime>
```
  
## <a name="enable-psso-for-office-365-users-to-access-sharepoint-online"></a>Office 365 액세스 하는 사용자 SharePoint Online PSSO 사용 하도록 설정  
 PSSO 사용 및 adfs에서 구성 되어 되 면 사용자가 인증 후 ADFS 영구 쿠키를 작성 합니다. 영구 쿠키는 올바른 여전히 하는 경우, 사용자가 다음에 사용자 하지 않아도 자격 증명을 다시 제공 합니다. Office 365에 대 한 추가 인증 프롬프트를 방지할 수 있습니다 하 고 다음과 같은 두 가지 구성 하 여 사용자에 게 SharePoint Online ADFS 트리거 지 속성 Microsoft Azure AD 및 SharePoint Online에서 규칙을 요구 합니다.  이 설치 하려면 필요한 PSSO Office 365 사용자가 온라인 SharePoint 액세스할 수 있도록 [핫픽스](https://support.microsoft.com/en-us/kb/2958298/) 입니다의 일부로의 [Windows RT 8.1, Windows 8.1, 및 Windows Server 2012 r 2 용 업데이트 롤업 2014 년 8 월](https://support.microsoft.com/en-us/kb/2975719)합니다.  
  
 InsideCorporateNetwork 클레임 통과 하는 발급 변환 규칙  
  
```  
@RuleTemplate = "PassThroughClaims"  
@RuleName = "Pass through claim - InsideCorporateNetwork"  
c:[Type == "https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork"]  
=> issue(claim = c);   
A custom Issuance Transform rule to pass through the persistent SSO claim  
@RuleName = "Pass Through Claim - Psso"  
c:[Type == "https://schemas.microsoft.com/2014/03/psso"]  
=> issue(claim = c);  
  
```
  
  
    


