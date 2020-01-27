---
ms.assetid: ed3206b4-bbfc-4bc7-a43c-981b0544a50d
title: Active Directory Federation Services에 대 한 필수 업데이트 (AD FS)
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 3/29/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0850145c9281c769c5a2b6532ccb56615abd11b3
ms.sourcegitcommit: ff0db5ca093a31034ccc5e9156f5e9b45b69bae5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/24/2020
ms.locfileid: "76725788"
---
# <a name="required-updates-for-active-directory-federation-services-ad-fs-and-web-application-proxy-wap"></a>Active Directory Federation Services (AD FS) 및 웹 응용 프로그램 프록시 (WAP)에 필요한 업데이트

2016 년 10 월 까지는 Windows Server의 모든 구성 요소에 대 한 모든 업데이트가 WU (Windows 업데이트)를 통해서만 릴리스됩니다.  핫픽스 또는 개별 다운로드가 더 이상 없습니다.
이는 Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2 s p 1에 적용 됩니다.

이 페이지에는 AD FS 및 WAP에 대 한 특정 관심의 롤업 패키지와 AD FS 및 WAP에 권장 되는 핫픽스 업데이트의 기록 목록이 나열 되어 있습니다.

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2016"></a>AD FS 및 Windows Server 2016에서에서 WAP에 대 한 업데이트
Windows Server 2016에 대 한 업데이트는 Windows 업데이트를 통해 매달 배달 되며 누적 됩니다. 아래 나열 된 업데이트 패키지는 모든 AD FS 및 WAP 2016 서버에 권장 되며, 이전에 필요한 모든 업데이트와 최신 수정 프로그램을 포함 합니다.

|50 # |설명|출시 날짜
|----- | ----- |-----
|[CVE-2019-1126](https://portal.msrc.microsoft.com/security-guidance/advisory/CVE-2019-1126) | 이 보안 업데이트는 공격자가 엑스트라넷 잠금 정책을 우회 하는 데 사용할 수 있는 Active Directory Federation Services (AD FS)의 취약성을 해결 합니다. |2019 年 7 月|
|[4489889 (OS 빌드 14393.2879)](https://support.microsoft.com/help/4489889/windows-10-update-kb4489889) | Active Directory Federation Services (AD FS)에서 중복 된 신뢰 당사자 트러스트를 AD FS 관리 콘솔에 표시 하는 문제를 해결 합니다. 이는 AD FS 관리 콘솔을 사용 하 여 신뢰 당사자 트러스트를 만들거나 볼 때 발생 합니다.</br></br> 2016 AD FS에서 엑스트라넷 스마트 잠금 (ESL)을 사용 하는 동안 발생 하는 높은 Active Directory Federation Services (ADFS) 웹 응용 프로그램 프록시 (WAP) 대기 시간 문제 (10, 000ms 이상)를 해결 합니다. 이 보안 업데이트는 [CVE-2018-16794](https://nvd.nist.gov/vuln/detail/CVE-2018-16794)에 설명 된 취약성을 해결 합니다. |2019 年 3 月|
|[4487006 (OS 빌드 14393.2828)](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) | PowerShell 또는 AD FS (Active Directory Federation Services) 관리 콘솔을 사용 하는 경우 신뢰 당사자 트러스트에 대 한 업데이트가 실패 하는 문제를 해결 합니다. 이 문제는 둘 이상의 PassiveRequestorEndpoint을 게시 하는 온라인 메타 데이터 URL을 사용 하도록 신뢰 당사자 트러스트를 구성 하는 경우에 발생 합니다. "MSIS7615: 신뢰 당사자 트러스트에 지정 된 신뢰할 수 있는 끝점은 신뢰 당사자 트러스트에 대해 고유 해야 합니다." 라는 오류입니다.  </br></br>Azure 암호 보호 정책으로 인해 외부 복잡성 암호 변경에 대 한 특정 오류 메시지를 표시 하는 문제를 해결 합니다. |2019년 2월|
|[4462928 (OS 빌드 14393.2580)](https://support.microsoft.com/help/4462928/windows-10-update-kb4462928)|Active Directory Federation Services (ADFS) 엑스트라넷 스마트 잠금 (ESL)과 대체 로그인 ID 간의 상호 운용 문제를 해결 합니다. 대체 로그인 ID를 사용 하도록 설정 하면 AD FS Powershell cmdlet AdfsAccountActivity 및 AdfsAccountLockout를 호출 하 여 "계정을 찾을 수 없음" 오류가 반환 됩니다. AdfsAccountActivity가 호출 되 면 기존 항목을 편집 하는 대신 새 항목이 추가 됩니다.|2018년 10월|
|[4343884 (OS 빌드 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)|사용자 지정 문화권 정의를 사용 하는 모바일 장치에서 Multi-Factor Authentication 제대로 작동 하지 않는 Active Directory Federation Services (AD FS) 문제를 해결 합니다. </br></br>새 사용자 등록에서 상당한 지연 (15 초)이 발생 하는 비즈니스용 Windows Hello의 문제를 해결 합니다. 이 문제는 RA (ADFS 등록 기관) 인증서를 저장 하는 데 하드웨어 보안 모듈을 사용 하는 경우에 발생 합니다.|2018년 8월|
|[4338822 (OS 빌드 14393.2395)](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822)|콘솔에서 신뢰 당사자 트러스트를 만들거나 볼 때 AD FS 관리 콘솔에서 중복 신뢰 당사자 트러스트를 표시 하는 AD FS 문제를 해결 합니다.</br></br>에서는 비즈니스용 Windows Hello가 실패 하 게 하는 ADFS의 문제를 해결 합니다. 두 클레임 공급자가 있는 경우이 문제가 발생 합니다. PIN 등록은 "400 내부 서버 오류: 장치 식별자를 가져올 수 없습니다."와 함께 실패 합니다.</br></br> 종료 되지 않는 비활성 연결과 관련 된 WAP 문제를 해결 합니다. 이로 인해 시스템 리소스 누수 (예: 메모리 누수) 및 더 이상 응답 하지 않는 WAP 서비스가 발생 합니다. 사용자가 다른 로그인 옵션을 선택할 수 없도록 하는 AD FS 문제를 해결 합니다. 이는 사용자가 인증서 기반 인증을 사용 하 여 로그인 하도록 선택 했지만 구성 되지 않은 경우에 발생 합니다. 사용자가 인증서 기반 인증을 선택한 다음 다른 로그인 옵션을 선택 하는 경우에도이 오류가 발생 합니다. 이런 경우 사용자는 브라우저를 닫을 때까지 인증서 기반 인증 페이지로 리디렉션됩니다.|2018 年 7 月|
|[4103720 (OS 빌드 14393.2273)](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)|PreventTokenReplays를 사용 하는 경우 SAML 신뢰 당사자에 대 한 IdP 시작 로그인이 실패 하 게 하는 ADFS와 관련 된 문제를 해결 합니다. </br></br>OAUTH가 장치 또는 브라우저 응용 프로그램에서 인증 될 때 발생 하는 ADFS 문제를 해결 합니다. 사용자 암호 변경으로 인해 오류가 발생 하 고 사용자가 응용 프로그램 또는 브라우저를 종료 하 여 로그인 해야 합니다. </br></br>UTC + 1 이상 (유럽 및 아시아)에서 엑스트라넷 스마트 잠금을 사용 하도록 설정 하지 못한 문제를 해결 합니다. 또한 다음과 같은 오류와 함께 일반적인 엑스트라넷 잠금이 실패 합니다. AdfsAccountActivity: UTC로 변환 될 때 Int32.maxvalue 보다 크거나 datetime. MinValue 보다 작은 DateTime 값을 JSON으로 직렬화 할 수 없습니다.</br></br>새 사용자가 자신의 PIN을 프로 비전 할 수 없는 ADFS Windows Hello for business 문제를 해결 합니다. 이는 MFA 공급자가 구성 되지 않은 경우에 발생 합니다.|2018년 5월|
|[4093120 (OS 빌드 14393.2214)](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)| 처리 되지 않은 새로 고침 토큰 유효성 검사 문제를 해결 합니다. 다음 오류를 생성 합니다. "IdentityServer. OAuthInvalidRefreshTokenException: MSIS9312: 잘못 된 OAuth 새로 고침 토큰을 받았습니다. 토큰에 허용 된 시간 보다 빨리 새로 고침 토큰이 수신 되었습니다. " |2018년 4월|
|[4077525 (OS 빌드 14393.2097)](https://support.microsoft.com/help/4077525/windows-10-update-kb4077525)|ADFS 팜에 WID (Windows 내부 데이터베이스)를 사용 하는 서버가 두 대 이상 있을 때 HTTP 500 오류가 발생 하는 문제를 해결 합니다. 이 시나리오에서는 WAP (웹 응용 프로그램 프록시) 서버에서 HTTP 기본 사전 인증이 일부 사용자를 인증 하지 못합니다. 오류가 발생 하면 WAP 이벤트 로그에 Microsoft Windows 웹 응용 프로그램 프록시 경고 이벤트 ID 13039이 표시 될 수도 있습니다. 설명은 "웹 응용 프로그램 프록시가 사용자를 인증 하지 못했습니다. 사전 인증은 ' 리치 클라이언트의 ADFS '입니다. 지정 된 사용자에 게 지정 된 신뢰 당사자에 액세스할 수 있는 권한이 없습니다. 대상 신뢰 당사자 또는 WAP 신뢰 당사자의 권한 부여 규칙을 수정 해야 합니다. "</br></br>인증 하는 동안 AD FS에서 더 이상 prompt = login을 무시 하지 않을 수 있는 문제를 해결 합니다. 암호 인증을 사용 하지 않는 시나리오를 지원 하기 위해 사용 하지 않도록 설정 된 옵션이 추가 되었습니다. 자세한 내용은 Windows Server 2016 RTM에서 인증 하는 동안 "prompt = login" 매개 변수를 무시 AD FS를 참조 하세요.</br></br>인증 옵션으로 인증서를 선택 하는 권한 있는 고객 (신뢰 당사자)이 연결 되지 않는 AD FS의 문제를 해결 합니다. WIA (Windows 통합 인증)를 사용 하도록 설정 하 고 요청에서 WIA를 수행할 수 있는 경우 prompt = login을 사용 하면 오류가 발생 합니다.</br></br>IDP (id 공급자)가 OAuth 그룹의 RP (신뢰 당사자)와 연결 된 경우 HRD (홈 영역 검색) 페이지를 잘못 표시 하는 문제 AD FS를 해결 합니다. 여러 IDPs가 OAuth 그룹의 RP와 연결 되어 있지 않으면 사용자에 게 HRD 페이지가 표시 되지 않습니다. 대신, 사용자는 인증을 위해 연결 된 IDP로 직접 이동 합니다.|2018년 2월|
|[4041688 (OS 빌드 14393.1794)](https://support.microsoft.com/kb/4041688)|이 픽스는 잘못 된 캐싱 동작으로 인해 AD 기관 요청을 잘못 된 Id 공급자로 잘못 지시 하는 문제를 해결 합니다. 이는 Multi-factor Authentication과 같은 인증 기능에 영향을 미칠 수 있습니다. </br></br>Mixed WS2012R2 및 WS2016 ADFS 팜에서 자세한 감사를 사용 하 여 ADFS 서버 상태를 정확 하 게 보고 하는 AAD Connect Health에 대 한 기능이 추가 되었습니다.</br></br>2012 R2 ADFS 팜을 ADFS 2016로 업그레이드 하는 동안 팜 동작 수준을 올리는 powershell cmdlet이 여러 신뢰 당사자 트러스트를 사용 하는 경우 시간 초과로 인해 실패 하는 문제가 해결 되었습니다.</br></br>요청을 다른 STS (보안 토큰 서버)에 페더레이션 하는 동안 wct 매개 변수 값을 수정 하 여 인증 오류가 발생 하는 AD FS 문제를 해결 했습니다.|2017년 10월|
|[4038801 (OS 빌드 14393.1737)](https://support.microsoft.com/kb/4038801)|페더레이션된 LDPs를 사용 하 여 OIDC 로그 아웃에 대 한 지원이 추가 되었습니다. 이렇게 하면 여러 사용자가 LDP와 페더레이션 하는 단일 장치에 순차적으로 로그인 할 수 있는 "키오스크 시나리오"가 허용 됩니다.</br></br>CEP/CES 기반 인증서가 gMSA 계정에서 작동 하지 않는 WinHello 문제를 수정 했습니다.</br></br>외래 키로 인해 Windows Server 2016 ADFS 서버의 WID (Windows 내부 데이터베이스)에서 IdentityServerPolicy 및 IdentityServerPolicy 테이블의 ApplicationGroupId 열과 같은 일부 설정을 동기화 하지 못하는 문제를 해결 합니다. check. 이러한 동기화 오류로 인해 주 서버와 보조 ADFS 서버 간에 다른 클레임, 클레임 공급자 및 응용 프로그램 환경을 만들 수 있습니다. 또한 WID 주 역할을 보조 노드로 이동 하는 경우에는 ADFS 관리 UX에서 응용 프로그램 그룹을 더 이상 관리할 수 없습니다.</br></br>이 업데이트는 사용자 지정 문화권 정의를 사용 하는 모바일 장치에서 Multi-factor Authentication이 제대로 작동 하지 않는 문제를 해결 합니다.|2017년 9월|
|[4034661 (OS 빌드 14393.1613)](https://support.microsoft.com/kb/4034661)|"성공 감사" 및 "실패 감사"를 사용 하도록 설정한 후에도 ad 4.0 \ Windows Server 2016 RS1 ADFS 서버의 보안 이벤트 로그에 있는 411 이벤트에서 호출자 IP 주소를 nog 하는 문제를 해결 합니다.</br></br>이 픽스는 ADFX 서버가 HTTP 프록시를 사용 하도록 구성 된 경우 Azure MFA (Multi-factor Authentication)와 관련 된 문제를 해결 합니다.</br></br>"만료 되거나 해지 된 인증서를 ADFS 프록시 서버에 표시 하는 문제를 해결 했지만 사용자에 게 오류를 반환 하지 않습니다."|2017년 8월|
|[4034658 (OS 빌드 14393.1593)](https://support.microsoft.com/kb/4034658)|프레미스 배포에 대 한 비즈니스용 Windows Hello에 대 한 MFA 인증서 등록을 지원 하기 위해 2016 AD FS 서버에 대 한 수정|2017년 8월|
|[4025334 (OS 빌드 14393.1532)](https://support.microsoft.com/kb/4025334)|PkeyAuth 요청이 잘못 된 데이터를 포함 하는 경우 PkeyAuth 토큰 처리기가 인증에 실패할 수 있는 문제를 해결 했습니다. 장치 인증을 수행 하지 않고 인증을 계속 진행 해야 합니다.|2017년 7월|
|[4022723 (OS 빌드 14393.1378)](https://support.microsoft.com/kb/4022723)|[웹 응용 프로그램 프록시] DisableHttpOnlyCookieProtection 구성 속성의 값은 2012R2/2016 혼합 배포에서 WAP 2016에 의해 선택 되지 않습니다. </br></br>[웹 응용 프로그램 프록시] EAS 사전 인증 시나리오에서 AD FS에서 사용자 액세스 토큰을 가져올 수 없습니다.</br></br>AD FS 2016: WSFED 로그 아웃으로 인해 예외가 발생 합니다.|2017년 6월
|[3213986](https://support.microsoft.com/kb/3213986)|KB3213986 (x64 기반 시스템용 Windows Server 2016 누적 업데이트)| 2017년 1월

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2012-r2"></a>AD FS 및 WAP Windows Server 2012 r 2에서에 대 한 업데이트
다음은 Windows Server 2012 r 2에서 Active Directory Federation Services (AD FS) 용으로 릴리스된 핫픽스와 업데이트 롤업을 나열 합니다.

|50 # |설명|출시 날짜
|----- | ----- |-----
|[4507448](https://support.microsoft.com/help/4507448/windows-8-1-update-kb4507448)| 이 보안 업데이트는 공격자가 엑스트라넷 잠금 정책을 우회 하는 데 사용할 수 있는 Active Directory Federation Services (AD FS)의 취약성을 해결 합니다. |2019 年 7 月
|[4041685](https://support.microsoft.com/kb/4041685)|요청 헤더의 MSISConext 쿠키가 결국 헤더 크기 제한을 오버플로 하 고 HTTP 상태 코드 400 "잘못 된 요청-헤더 너무 깁니다."로 인해 실패 하는 경우 발생 하는 문제를 AD FS 해결 했습니다.</br></br>ADFS가 인증 중에 "prompt = login"을 더 이상 무시할 수 없는 문제를 해결 했습니다. 암호 없는 인증을 사용 하는 경우 복원 시나리오에 "사용 안 함" 옵션이 추가 되었습니다.|10 월 2017 업데이트 롤업 미리 보기
|[4019217](https://support.microsoft.com/kb/4019217)|Server 2012 R2 AD FS Server를 사용 하는 경우 token broker를 사용 하는 클라우드 폴더 클라이언트가 작동 하지 않음|2017 년 5 월 미리 보기 업데이트 롤업
|[4015550](https://support.microsoft.com/kb/4015550)|요청을 전달 하는 데 임의로 실패 하는 외부 사용자 및 AD FS WAP를 인증 하지 AD FS 문제 해결|4 월 2017 업데이트 롤업
|[4015547](https://support.microsoft.com/kb/4015547)|요청을 전달 하는 데 임의로 실패 하는 외부 사용자 및 AD FS WAP를 인증 하지 AD FS 문제 해결|4 월 2017 보안 업데이트
|[4012216](https://support.microsoft.com/kb/4009970)|MS17-019이 보안 업데이트는 ADFS (Active Directory Federation Services)의 취약성을 해결 합니다. 공격자가 특수 하 게 작성 된 요청을 AD FS 서버에 전송 하 여 대상 시스템에 대 한 중요 한 정보를 읽을 수 있도록 하는 경우 취약점으로 인해 정보가 공개 될 수 있습니다.|3 월 2017 업데이트 롤업
|[3179574](https://support.microsoft.com/kb/3179574)|AD FS 엑스트라넷 암호 업데이트와 관련 된 문제가 해결 되었습니다. |8 월 2016 업데이트 롤업
|[3172614](https://support.microsoft.com/kb/3172614)|소개 된 프롬프트 = 로그인 [지원](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/ad-fs-faq#BKMK_7), AD FS management Console 및 AlwaysRequireAuthentication 설정 문제 해결 |7 월 2016 업데이트 롤업
|[3163306](https://support.microsoft.com/kb/3163306)|Active Directory Federation Services (AD FS) 3.0는 연결 문자열에서 SSL(Secure Sockets Layer) (SSL) 포트 636 또는 3269을 사용 하도록 구성 된 LDAP (Lightweight Directory Access Protocol) 특성 저장소에 연결할 수 없습니다. |6 월 2016 업데이트 롤업
|[3148533](https://support.microsoft.com/kb/3148533)|Windows Server 2012 r 2에서 ADFS 프록시를 통해 MFA 대체 (fallback) 인증에 실패 |2016년 5월
|[3134787](https://support.microsoft.com/kb/3134787)|AD FS 로그는 Windows Server 2012 r 2에서의 계정 잠금 시나리오에 대 한 클라이언트 IP 주소를 포함 하지 않습니다. |2016년 2월
|[3134222](https://support.microsoft.com/kb/3134222)|서비스 주소 거부에 Active Directory Federation Services 용 보안 업데이트 MS16-020:: 2016 년 2 월 9 일|2016년 2월
|[3105881](https://support.microsoft.com/kb/3105881)|AD FS Windows Server 2012 R2 기반 서버에서 디바이스 인증을 사용 하는 경우 애플리케이션에 액세스할 수 없습니다.|2015 년 10 월
|[3092003](https://support.microsoft.com/kb/3092003)|페이지를 반복적으로 로드 하 고 사용자가 Windows Server 2012 R2 AD FS에서 MFA를 사용할 때 인증에 실패|2015년 8월
|[3080778](https://support.microsoft.com/kb/3080778)|MFA 어댑터는 Windows Server 2012 r 2에서 예외를 throw 하는 경우 AD FS OnError를 호출 하지 않습니다.|2015 년 7 월
|[3075610](https://support.microsoft.com/kb/3075610)|트러스트 관계를 추가 하거나 Windows Server 2012 r 2에서 클레임 공급자를 제거한 후 보조 AD FS 서버에서 손실 됩니다.|2015 년 7 월
|[3070080](https://support.microsoft.com/kb/3070080)|비 클레임 인식 신뢰 당사자 트러스트에 대 한 제대로 작동 하지 홈 영역 검색|2015 년 6 월
|[3052122](https://support.microsoft.com/kb/3052122)|Windows Server 2012 r 2에서 AD FS 토큰에 복합 ID 클레임에 대 한 지원을 추가 하는 업데이트|2015 년 5 월
|[3045711](https://support.microsoft.com/kb/3045711)|MS15-040: Active Directory 페더레이션 서비스의 취약점으로 정보 공개|2015 년 4 월
|[3042127](https://support.microsoft.com/kb/3042127)|"HTTP 400-잘못 된 요청" Windows Server 2012 r 2에서 WAP 통해 공유 사서함을 열면 하는 동안 오류가 발생 했습니다.|2015 년 3 월
|[3042121](https://support.microsoft.com/kb/3042121)|Windows Server 2012 r 2에서 웹 애플리케이션 프록시 인증 토큰에 대 한 AD FS 토큰 재생 보호|2015 년 3 월
|[3035025](https://support.microsoft.com/kb/3035025)|사용자는 Windows Server 2012 r 2에서 등록 된 디바이스를 사용 하 여 필요가 없도록 암호 업데이트에 대 한 핫픽스 기능|2015 년 1 월
|[3033917](https://support.microsoft.com/kb/3033917)|AD FS는 Windows Server 2012 r 2에서 SAML 응답을 처리할 수 없습니다.|2015 년 1 월
|[3025080](https://support.microsoft.com/kb/3025080)|Windows Server 2012 r 2에서 웹 애플리케이션 프록시를 통해 Office 파일을 저장 하려고 할 때 작업이 실패|2015 년 1 월
|[3025078](https://support.microsoft.com/kb/3025078)|묻는 메시지가 사용자에 대 한 다시는 잘못 된 사용자 이름을 사용 하 여 Windows Server 2012 r 2에 로그온 할 때|2015 년 1 월
|[3020813](https://support.microsoft.com/kb/3020813)|Windows Server 2012 R2 AD FS에서 웹 애플리케이션을 실행할 때 인증을 위해 묻는|2015 년 1 월
|[3020773](https://support.microsoft.com/kb/3020773)|Windows Server 2012 r 2에서 디바이스 등록 서비스의 초기 배포 후 시간 초과 오류|2015 년 1 월
|[3018886](https://support.microsoft.com/kb/3018886)|메시지가 표시 되는 사용자 이름 및 암호를 두 번 인트라넷에서 Windows Server 2012 R2 AD FS 서버에 액세스할 때|2015 년 1 월
|[3013769](https://support.microsoft.com/kb/3013769)|Windows Server 2012 R2 업데이트 롤업|2014 년 12 월
|[3000850](https://support.microsoft.com/kb/3000850)|Windows Server 2012 R2 업데이트 롤업|2014 年 11 月
|[2975719](https://support.microsoft.com/kb/2975719)|Windows Server 2012 R2 업데이트 롤업|2014 년 8 월
|[2967917](https://support.microsoft.com/kb/2967917)|Windows Server 2012 R2 업데이트 롤업|2014 년 7 월
|[2962409](https://support.microsoft.com/kb/2962409)|Windows Server 2012 R2 업데이트 롤업|2014 년 6 월
|[2955164](https://support.microsoft.com/kb/2955164)|Windows Server 2012 R2 업데이트 롤업|2014 년 5 월
|[2919355](https://support.microsoft.com/kb/2919355)|Windows Server 2012 R2 업데이트 롤업|2014년 4월

## <a name="updates-for-ad-fs-in-windows-server-2012-ad-fs-21-and-ad-fs-20"></a>Windows Server 2012 (AD FS 2.1) 및 AD FS 2.0의 AD FS에 대 한 업데이트
다음은 AD FS 2.0 및 2.1에 대해 출시 된 핫픽스와 업데이트 롤업을 나열 합니다.

|50 # |설명|출시 날짜|적용 대상:
|----- | ----- |-----|-----
|[3197878](https://support.microsoft.com/kb/3197878)|Windows Server 2012에서 프록시를 통한 인증 실패 (핫픽스 3094446의 일반 릴리스)|11 월 2016 품질 롤업|AD FS 2.1
|[3197869](https://support.microsoft.com/kb/3197869)|Windows Server 2008 R2 s p 1에서 프록시를 통한 인증 실패 (핫픽스 3094446의 일반 릴리스)|11 월 2016 품질 롤업|AD FS 2.0
|[3094446](https://support.microsoft.com/kb/3094446)|Windows Server 2012 또는 Windows Server 2008 R2 s p 1에서 프록시를 통해 인증 실패|2015 년 9 월|AD FS 2.0 및 2.1
|[3070078](https://support.microsoft.com/kb/3070078)|2\.1 AD FS Windows Server 2012에서 암호화 인증서에 대해 인증할 때 예외를 throw 합니다.|2015 년 7 월|AD FS 2.1
|[3062577](https://support.microsoft.com/kb/3062577)|MS15-062: Active Directory 페더레이션 서비스의 취약점으로 권한 상승 문제점|2015 년 6 월|AD FS 2.0 / 2.1
|[3003381](https://support.microsoft.com/kb/3003381)|M s 14-077: Active Directory 페더레이션 서비스의 취약점으로 정보 공개: 2015 년 4 월 14 일|2014 年 11 月|AD FS 2.0 / 2.1
|[2987843](https://support.microsoft.com/kb/2987843)|많은 사용자가 Windows Server 2012에서 웹 애플리케이션에 로그온 하는 경우 AD FS 페더레이션 서버의 메모리 사용량은 계속 증가|2014 년 7 월|AD FS 2.1
|[2957619](https://support.microsoft.com/kb/2957619)|위임 된 토큰에 대 한 AD FS를 요청 하는 경우 중지 됩니다. AD FS에서 신뢰 당사자 트러스트|2014 년 5 월|AD FS 2.1
|[2926658](https://support.microsoft.com/kb/2926658)|SQL 권한이 없을 경우 ADFS SQL 팜 배포 실패|2014년 10월|AD FS 2.1
|[2896713](https://support.microsoft.com/kb/2896713) 또는 [2989956](https://support.microsoft.com/kb/2989956)|업데이트는 AD FS 서버에 2843638 보안 업데이트를 설치 하려면 몇 가지 문제를 해결 하려면|2013 년 11 월</br></br>2014 년 9 월|AD FS 2.0 / 2.1
|[2877424](https://support.microsoft.com/kb/2877424)|업데이트를 사용 하면 2.1 팜의 AD FS에서 여러 신뢰 당사자 트러스트에 대 한 인증서가 두 개를 사용 하 여|2013년 10월|AD FS 2.1
|[2873168](https://support.microsoft.com/kb/2873168)|FIX: 타사 CSP 및 HSM을 사용 하 고 다음 Windows Server 2008 R2 서비스 팩 1에서 AD FS 2.0에 대 한 업데이트 롤업 3에서 클레임 공급자 트러스트를 구성할 때 오류가 발생 한다|2013 년 9 월|AD FS 2.0
|[2861090](https://support.microsoft.com/kb/2861090)|Windows Server 2008 R2 s p 1에서 예외를 발생 하는 암호화 인증서의 주체 이름에 쉼표|2013년8월|AD FS 2.0
|[2843639](https://support.microsoft.com/kb/2843639)|[보안] Active Directory Federation Services의 취약점으로 인 한 정보 공개|2013 년 11 월|AD FS 2.1
|[2843638](https://support.microsoft.com/kb/2843638)|MS13-066: 2008 Active Directory Federation Services 2.0에 대 한 보안 업데이트: 2013 년 8 월 13 일|2013년8월|AD FS 2.0
|[2827748](https://support.microsoft.com/kb/2827748)|Federationmetadata.xml 파일에 Windows Server 2012에서 Ws-trust 및 Ws-federation 엔드포인트에 대 한 MEX 엔드포인트 정보가 없습니다.|2013년 5월|AD FS 2.1
|[2790338](https://support.microsoft.com/kb/2790338)|Active Directory Federation Services (AD FS)에 대 한 업데이트 롤업 3의 설명 2.0|2013년 3월|AD FS 2.0
