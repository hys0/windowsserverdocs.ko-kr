---
ms.assetid: ed3206b4-bbfc-4bc7-a43c-981b0544a50d
title: "필요한 업데이트에 대 한 Active Directory Federation Services ADFS)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 434bf65c9f5ec977318b5efcdeebd19a5f1ed475
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="required-updates-for-active-directory-federation-services-ad-fs-and-web-application-proxy-wap"></a>필수 업데이트 (ADFS) Active Directory Federation Services와 웹 응용 프로그램 프록시 WAP)

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 s p 1

2016 년 10 월 Windows Server의 모든 구성 요소에 대 한 모든 업데이트가을 통해 Windows 업데이트 (WU) 해제 됩니다.  추가 핫픽스 없는 또는 개별 다운로드 가지가 있습니다.
Windows Server 2016, Windows Server 2012 R2, Windows Server 2012와 Windows Server 2008 R2 s p 1에 해당 합니다.

이 페이지의 관심 롤업 패키지 ADFS WAP를 제공할 뿐만 아니라 역사적인 ADFS 및 WAP 권장 핫픽스 업데이트 목록에 대 한 나열 됩니다.

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2016"></a>ADFS 및 WAP Windows server 2016 용 업데이트
Windows Server 2016 용 업데이트에는 월별 Windows 업데이트를 통해 제공 되며 누적 수 있습니다. 아래에 나열 된 업데이트 패키지 모든 ADFS 및 WAP 2016 서버에 대 한 권장와 최신 수정 사항이 적용 뿐만 아니라 이전에 필요한 모든 업데이트가 포함 됩니다.

|KB # |설명|릴리스 날짜
|----- | ----- |-----
|[4041688 (OS Build 14393.1794)](https://support.microsoft.com/kb/4041688)|This fix addresses an issue that intermittently misdirects AD Authority requests to the wrong Identity Provider because of incorrect caching behavior. This can effect authentication features like Multi Factor Authentication. </br></br>Added the ability for AAD Connect Health to report ADFS server health with correct fidelity (using verbose auditing) on mixed WS2012R2 and WS2016 ADFS farms.</br></br>Fixed a problem where during upgrade of 2012 R2 ADFS farm to ADFS 2016, the powershell cmdlet to raise the farm behavior level fails with a timeout when there are many relying party trusts.</br></br>Addressed an issue where AD FS causes authentication failures by modifying the wct parameter value while federating the requests to other Security Token Server (STS).|October 2017|
|[4038801 (OS Build 14393.1737)](https://support.microsoft.com/kb/4038801)|Support added for OIDC logout using federated LDPs. This will allow "Kiosk Scenarios" where multiple users might be serially logged into a single device where there is federation with an LDP.</br></br>Fixed a WinHello issue where CEP/CES based certificates don't work with gMSA accounts.</br></br>Fixes a problem where the Windows Internal Database (WID) on Windows Server 2016 ADFS servers fails to sync some settings, such as the ApplicationGroupId columns from IdentityServerPolicy.Scopes and IdentityServerPolicy.Clients tables)  due to a foreign key constraint. Such sync failures can cause different claim, claim provider and application experiences between primary to secondary ADFS servers. Also, if the WID primary role is moved to a secondary node, application groups will no longer be manageable in the ADFS management UX.</br></br>This update fixes an issues where Multi Factor Authentication does not work correctly with Mobile devices that use custom culture definitions|September 2017|
|[4034661 (OS Build 14393.1613)](https://support.microsoft.com/kb/4034661)|Fixes a problem where the caller IP address is nog logged by 411 events in the Security Event log of ADFS 4.0 \ Windows Server 2016 RS1 ADFS servers even after enabling “success audits” and “failure audits”.</br></br>This fix addresses an issue with Azure Multi Factor Authentication (MFA) when an ADFX server is configured to use an HTTP Proxy.</br></br>"Addressed an issue where presenting an expired or revoked certificate to the ADFS Proxy server does not return an error to the user."|August 2017|
|[4034658 (OS Build 14393.1593)](https://support.microsoft.com/kb/4034658)|Fix for 2016 AD FS server in order to support MFA certificate enrollment for Windows Hello For Business for on prem deployments|August 2017| 
|[4025334 (OS Build 14393.1532)](https://support.microsoft.com/kb/4025334)|Addressed an issue where the PkeyAuth token handler could fail an authentication if the pkeyauth request contains incorrect data. The authentication should still continue without performing device authentication|July 2017|
|[4022723 (OS Build 14393.1378)](https://support.microsoft.com/kb/4022723)|[Web Application Proxy] Value of DisableHttpOnlyCookieProtection configuration property is not picked up by WAP 2016 in 2012R2/2016 mixed deployment </br></br>[Web Application Proxy] Unable to obtain user access token from AD FS in EAS Pre-auth scenarios.</br></br>AD FS 2016 : WSFED sign-out leads to an exception|2017 년 6 월 
|[3213986](https://support.microsoft.com/kb/3213986)|Windows Server 2016 용 누적 업데이트 x64 기반 시스템용 (KB3213986)| 2017 년 1 월

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2012-r2"></a>Adfs와 WAP Windows Server 2012 r 2에서에 대 한 업데이트
다음 목록에 대 한 Active Directory Federation Services (ADFS) Windows Server 2012 r 2에 출시 된 핫픽스 및 업데이트 롤업에입니다.

|KB # |설명|릴리스 날짜
|----- | ----- |-----
|[4041685](https://support.microsoft.com/kb/4041685)|Addressed an AD FS issue where MSISConext cookies in request headers can eventually overflow the headers size limit and cause failure to authenticate with HTTP status code 400 “Bad Request - Header Too Long".</br></br>Fixed a problem where ADFS can no longer ignore "prompt=login" during authentication. A "Disabled" option was added to restore scenarios where non-password authentication is used.|October 2017 Preview of Update Rollup|
|[4019217](https://support.microsoft.com/kb/4019217)|Work Folders clients using token broker do not work when using a Server 2012 R2 AD FS Server|May 2017 Preview Update Rollup| 
|[4015550](https://support.microsoft.com/kb/4015550)|Fixed an issue with AD FS not authenticating External users and AD FS WAP randomly failing to forward request|April 2017 Update Rollup| 
|[4015547](https://support.microsoft.com/kb/4015547)|Fixed an issue with AD FS not authenticating External users and AD FS WAP randomly failing to forward request|April 2017 Security Update| 
|[4012216](https://support.microsoft.com/kb/4009970)|MS17-019 This security update resolves a vulnerability in Active Directory Federation Services (ADFS). The vulnerability could allow information disclosure if an attacker sends a specially crafted request to an AD FS server, allowing the attacker to read sensitive information about the target system.|March 2017 Update Rollup| 
|[3179574](https://support.microsoft.com/kb/3179574)|ADFS 엑스트라넷 암호 업데이트와 함께 문제를 해결 했습니다. |2016 년 8 월 업데이트 롤업
|[3172614](https://support.microsoft.com/kb/3172614)|도입 된 프롬프트 로그인 = [지원](https://technet.microsoft.com/en-us/windows-server-docs/identity/ad-fs/overview/ad-fs-faq#BKMK_7), ADFS 관리 콘솔 및 AlwaysRequireAuthentication 설정을 사용 하 여 문제를 해결 했습니다. |2016 년 7 월 업데이트 롤업
|[3163306](https://support.microsoft.com/kb/3163306)|Active Directory Federation Services (ADFS) 3.0 636 또는 연결 문자열의 3269 소켓 SSL (Secure Layer) 포트를 사용 하도록 구성 된 경량 Directory 액세스 LDAP 특성 저장소에 연결할 수 없습니다. |2016 년 6 월 업데이트 롤업
|[3148533](https://support.microsoft.com/kb/3148533)|ADFS 프록시 Windows Server 2012 r 2에서를 통해 MFA 대체 인증이 실패 |2016 년 5 월
|[3134787](https://support.microsoft.com/kb/3134787)|ADFS 로그 계정 잠금 시나리오 Windows Server 2012 r 2에서에 대 한 클라이언트 IP 주소를 포함 하지 |2016 년 2 월
|[3134222](https://support.microsoft.com/kb/3134222)|MS16-020: 보안 업데이트에 대 한 Active Directory Federation Services 서비스 거부가 주소를: 2016 년 2 월 9 일|2016 년 2 월
|[3105881](https://support.microsoft.com/kb/3105881)|Windows Server 2012 R2 기반 ADFS 서버에서 디바이스 인증을 사용 하는 경우 응용 프로그램에 액세스할 수 없는|2015 년 10 월
|[3092003](https://support.microsoft.com/kb/3092003)|반복적으로 페이지 로드 하 고 사용자에 게 MFA를 사용 하 여 Windows Server 2012 r 2 adfs에서 인증이 실패|2015 년 8 월
|[3080778](https://support.microsoft.com/kb/3080778)|Adfs가 OnError 호출 하지 않으면 MFA 어댑터는 예외 Windows Server 2012 r 2의 경우|2015 년 7 월
|[3075610](https://support.microsoft.com/kb/3075610)|보안 관계는 보조 ADFS 서버의 잃어버린 추가 또는 Windows Server 2012 r 2에서 클레임 공급자를 제거|2015 년 7 월
|[3070080](https://support.microsoft.com/kb/3070080)|비 클레임 인식 의존 파티 신뢰 하는 것에 대 한 제대로 작동 하지 않는 홈 영역 검색|2015 년 6 월
|[3052122](https://support.microsoft.com/kb/3052122)|업데이트는 Windows Server 2012 r 2에서 ADFS 토큰 복합 ID 청구에 대 한 지원이 추가|2015 년 5 월
|[3045711](https://support.microsoft.com/kb/3045711)|MS15 040: Active Directory Federation Services 클라우드의 취약성 정보 공개|2015 년 4 월
|[3042127](https://support.microsoft.com/kb/3042127)|"400-잘못 요청 HTTP" Windows Server 2012 r 2에서를 통해 WAP 공유 사서함 열 때 오류|2015 년 3 월
|[3042121](https://support.microsoft.com/kb/3042121)|웹 응용 프로그램 프록시 인증 토큰 Windows Server 2012 r 2에서에 대 한 AD FS 토큰 재생 보호|2015 년 3 월
|[3035025](https://support.microsoft.com/kb/3035025)|Windows Server 2012 r 2의 등록 된 디바이스를 사용 하 여 사용자에 게 필요는 없습니다 되도록 핫픽스 암호 업데이트에 대 한 기능|2015 년 1 월
|[3033917](https://support.microsoft.com/kb/3033917)|Adfs는 SAML 응답 Windows Server 2012 r 2에서를 처리할 수 없습니다.|2015 년 1 월
|[3025080](https://support.microsoft.com/kb/3025080)|Windows Server 2012 r 2에서를 통해 웹 응용 프로그램 프록시 Office 파일을 저장 하려고 할 때 작업이 실패|2015 년 1 월
|[3025078](https://support.microsoft.com/kb/3025078)|묻는 사용자 이름에 대해 다시 Windows Server 2012 r 2에 로그온 할 때 잘못 된 사용자 이름을 사용 하는 경우|2015 년 1 월
|[3020813](https://support.microsoft.com/kb/3020813)|메시지가 표시 되 인증을 위해 Windows Server 2012 r 2 adfs에서 웹 응용 프로그램을 실행 하는 경우|2015 년 1 월
|[3020773](https://support.microsoft.com/kb/3020773)|Windows Server 2012 r 2에 장치를 등록 서비스의 초기 배포 후 시간 초과 오류|2015 년 1 월
|[3018886](https://support.microsoft.com/kb/3018886)|메시지가 표시 되는 사용자 이름 및 암호를 두 번 인트라넷에서 Windows Server 2012 r 2 ADFS 서버에 액세스할 때|2015 년 1 월
|[3013769](https://support.microsoft.com/kb/3013769)|Windows Server 2012 R2 업데이트 롤 접속|2014 년 12 월
|[3000850](https://support.microsoft.com/kb/3000850)|Windows Server 2012 R2 업데이트 롤 접속|2014 년 11 월
|[2975719](https://support.microsoft.com/kb/2975719)|Windows Server 2012 R2 업데이트 롤 접속|2014 년 8 월
|[2967917](https://support.microsoft.com/kb/2967917)|Windows Server 2012 R2 업데이트 롤 접속|2014 년 7 월
|[2962409](https://support.microsoft.com/kb/2962409)|Windows Server 2012 R2 업데이트 롤 접속|2014 년 6 월
|[2955164](https://support.microsoft.com/kb/2955164)|Windows Server 2012 R2 업데이트 롤 접속|2014 년 5 월
|[2919355](https://support.microsoft.com/kb/2919355)|Windows Server 2012 R2 업데이트 롤 접속|2014 년 4 월

## <a name="updates-for-ad-fs-in-windows-server-2012-ad-fs-21-and-ad-fs-20"></a>Windows Server 2012 (ADFS 2.1) 및 AD Adfs에 대 한 업데이트 FS 2.0
다음 2.0 및 2.1 adfs 출시 된 핫픽스 및 업데이트 롤업에의 목록이입니다.

|KB # |설명|릴리스 날짜|적용 대상:
|----- | ----- |-----|-----
|[3197878](https://support.microsoft.com/kb/3197878)|(핫픽스 3094446 일반 릴리스는) Windows Server 2012에서 실패 하는 프록시 인증|2016 년 11 월 품질 롤업|ADFS 2.1
|[3197869](https://support.microsoft.com/kb/3197869)|Windows Server 2008 R2 SP1 (핫픽스 3094446 일반 릴리스는)에 실패 하는 프록시 인증|2016 년 11 월 품질 롤업|ADFS 2.0
|[3094446](https://support.microsoft.com/kb/3094446)|Windows Server 2008 R2 SP1 또는 Windows Server 2012에서 실패 하는 프록시 인증|2015 년 9 월|ADFS 2.0 및 2.1
|[3070078](https://support.microsoft.com/kb/3070078)|ADFS 2.1는 예외 인증 Windows Server 2012에 대 한 암호화 인증서 하는 경우|2015 년 7 월|ADFS 2.1
|[3062577](https://support.microsoft.com/kb/3062577)|MS15 062: Active Directory federation services 클라우드의 취약성 권한이 상승|2015 년 6 월|ADFS 2.0 2.1 /
|[3003381](https://support.microsoft.com/kb/3003381)|MS14 077: Active Directory Federation Services 클라우드의 취약성 정보 공개: 2015 년 4 월 14 일|2014 년 11 월|ADFS 2.0 2.1 /
|[2987843](https://support.microsoft.com/kb/2987843)|Windows Server 2012에서 웹 응용 프로그램 많은 사용자가 로그인 ADFS federation 서버의 메모리 사용량 계속 증가 함|2014 년 7 월|ADFS 2.1
|[2957619](https://support.microsoft.com/kb/2957619)|Adfs의 신뢰 파티 신뢰를 ADFS 위임된 토큰에 대 한 요청이 있을 때 중지|2014 년 5 월|ADFS 2.1
|[2926658](https://support.microsoft.com/kb/2926658)|ADFS SQL 농장 배포 실패 SQL 권한 없는 경우|2014 년 10 월|ADFS 2.1
|[2896713](https://support.microsoft.com/kb/2896713) or [2989956](https://support.microsoft.com/kb/2989956)|업데이트를 사용할 수 있는 몇 가지 문제는 ADFS 서버에 2843638 보안 업데이트를 설치한 후 문제를 해결 하려면|2013 년 11 월</br></br>2014 년 9 월|ADFS 2.0 2.1 /
|[2877424](https://support.microsoft.com/kb/2877424)|업데이트를 통해 여러 Relying 파티 신뢰 ADFS 2.1 팜에 대 한 하나의 인증서를 사용 하 여|2013 년 10 월|ADFS 2.1
|[2873168](https://support.microsoft.com/kb/2873168)|제 3 자 CSP 및 HSM 사용 하 고 다음 Windows Server 2008 R2 서비스 팩 1 ADFS 2.0에 대 한 업데이트 롤업 3에서 클레임 공급자 신뢰를 구성할 때 수정: 오류가 발생|2013 년 9 월|ADFS 2.0
|[2861090](https://support.microsoft.com/kb/2861090)|Windows Server 2008 R2 s p 1에서 예외도 인해 쉼표 한 암호화 인증서의 제목 이름에|2013 년 8 월|ADFS 2.0
|[2843639](https://support.microsoft.com/kb/2843639)|[보안] Active Directory Federation Services의 취약성 정보 공개|2013 년 11 월|ADFS 2.1
|[2843638](https://support.microsoft.com/kb/2843638)|MS13-066: 대 한 Active Directory Federation Services 2.0에 대 한 보안 업데이트: 2013 년 8 월 13|2013 년 8 월|ADFS 2.0
|[2827748](https://support.microsoft.com/kb/2827748)|Federationmetadata.xml 파일에 Ws-trust 및 WS Federation 끝점 Windows Server 2012에 대 한 MEX endpoint 정보가 없습니다.|5 월 2013|ADFS 2.1
|[2790338](https://support.microsoft.com/kb/2790338)|(ADFS) Active Directory Federation Services에 대 한 업데이트 롤업 3 설명 2.0|2013 년 3 월|ADFS 2.0




