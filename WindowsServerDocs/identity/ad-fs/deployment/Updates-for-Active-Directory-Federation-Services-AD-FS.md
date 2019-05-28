---
ms.assetid: ed3206b4-bbfc-4bc7-a43c-981b0544a50d
title: Active Directory Federation Services (AD FS)에 대 한 필수 업데이트
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 3/29/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 071017d05b288a70592af9203fedc72f699d18e0
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191943"
---
# <a name="required-updates-for-active-directory-federation-services-ad-fs-and-web-application-proxy-wap"></a>Active Directory Federation Services (AD FS) 및 웹 응용 프로그램 프록시 (WAP)에 대 한 필수 업데이트


2016 년 10 월부터 Windows Server의 모든 구성 요소에 대 한 모든 업데이트에만 통해 Windows Update (WU) 릴리스됩니다.  자세한 없습니다 핫픽스 또는 개별 다운로드 있습니다.
Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2008 R2 SP1이 적용 됩니다.

이 페이지는 AD FS 및 WAP에서 뿐만 아니라 AD FS 및 WAP에 대 한 권장 핫픽스 업데이트 기록 목록에 대 한 특정 관심 롤업 패키지를 나열 합니다.

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2016"></a>AD FS 및 Windows Server 2016에서에서 WAP에 대 한 업데이트
Windows Server 2016에 대 한 업데이트 Windows Update를 통해 매월 배달 및 누적 됩니다. 아래의 업데이트 패키지는 모든 AD FS 및 WAP 2016 서버에 대 한 것이 좋습니다 하 고 모든 이전에 필요한 업데이트 뿐 아니라 최신 수정 프로그램을 포함 합니다.

|KB # |설명|출시 날짜
|----- | ----- |-----
|[4489889 (OS 빌드 14393.2879)](https://support.microsoft.com/help/4489889/windows-10-update-kb4489889) | Active Directory Federation Services (AD FS) 신뢰 당사자 트러스트에 AD FS 관리 콘솔에 표시를 중복 시키는 문제를 해결 합니다. 이런 만들거나 볼 때 AD FS 관리 콘솔을 사용 하 여 신뢰 당사자 트러스트 합니다. |2019 년 3 월|
|[4487006 (OS 빌드 14393.2828)](https://support.microsoft.com/help/4487006/windows-10-update-kb4487006) | PowerShell 또는 Active Directory Federation Services (AD FS) 관리 콘솔을 사용 하는 경우 실패 하도록 신뢰 당사자 트러스트를 업데이트 하는 문제를 해결 합니다. 이 문제는 둘 이상의 PassiveRequestorEndpoint를 게시 하는 온라인 메타 데이터 URL을 사용 하는 신뢰 당사자 트러스트를 구성 하는 경우에 발생 합니다. 오류는 "MSIS7615: 신뢰 당사자 트러스트에 지정 된 신뢰할 수 있는 끝점에 대해 고유 해야 해당 신뢰 당사자 트러스트 합니다. "  </br></br>Azure 암호 보호 정책으로 인해 복잡성 외부 암호 변경에 대 한 특정 오류 메시지를 표시 하는 문제를 해결 합니다. |2019년 2월|
|[4462928 (OS 빌드 14393.2580)](https://support.microsoft.com/help/4462928/windows-10-update-kb4462928)|Active Directory Federation Services (ADFS) 엑스트라넷 스마트 잠금 (ESL)와 대체 로그인 ID 간에 상호 운용성 문제를 해결 대체 로그인 ID를 사용 하는 경우 AD FS Powershell cmdlet, Get AdfsAccountActivity 및 재설정 AdfsAccountLockout, 반환 "계정 찾을 수 없음" 오류를 호출 합니다. 집합 AdfsAccountActivity 호출 되 면 기존 항목을 편집 하는 대신 새 항목이 추가 됩니다.|2018년 10월|
|[4343884 (OS 빌드 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)|여기서 Multi-factor Authentication 제대로 작동 하지 않습니다 사용자 지정 문화권 정의 사용 하는 모바일 장치를 사용 하 여 Active Directory Federation Services (AD FS) 문제를 해결 합니다. </br></br>Windows hello for Business에서 새 사용자 등록 (15 초) 상당한 지연이 발생 하는 문제를 해결 합니다. 하드웨어 보안 모듈을 ADFS RA (등록 기관) 인증서를 저장 하는 경우이 문제가 발생 합니다.|2018년 8월|
|[4338822 (OS 빌드 14393.2395)](https://support.microsoft.com/help/4338822/windows-10-update-kb4338822)|만들기 또는 콘솔에서 신뢰 당사자 트러스트를 확인 하는 경우 AD FS 관리 콘솔에서 중복 신뢰 당사자 트러스트를 보여 주는 AD FS에서 문제를 해결 합니다.</br></br>발생 시키는 Windows Hello for Business에서 실패를 ad FS의 문제를 해결 합니다. 문제는 두 개의 클레임 공급자 있을 때 발생 합니다. PIN 등록을 사용 하 여 실패 "400 내부 서버 오류: 가져올 수 없습니다 장치 식별자입니다. "</br></br> 절대로 종료 하지 않는 비활성 연결과 관련 된 WAP 문제를 해결 합니다. 따라서 시스템 리소스 누수 (예: 메모리 누수) 하는 WAP 서비스는 더 이상 반응 형입니다. 사용자가 다른 로그인 옵션을 선택 하는 것을 방지 하는 AD FS 문제를 해결 합니다. 이 사용자가 인증서 기반 인증을 사용 하 여 로그인 하도록 선택 하지만 구성 되지 않은 경우 발생 합니다. 이 경우에 사용자가 인증서 기반 인증을 선택 하 고 다른 로그인 옵션을 선택 해 보십시오. 이 경우 사용자 브라우저를 닫을 때까지 인증서 기반 인증 페이지로 이동 합니다.|2018 년 7 월|
|[4103720 (OS 빌드 14393.2273)](https://support.microsoft.com/help/4103720/windows-10-update-kb4103720)|SAML 신뢰 당사자 PreventTokenReplays을 사용 하는 경우 실패를 IdP에서 시작한 로그인을 발생 시키는 ADFS 사용 하 여 문제를 해결 합니다. </br></br>장치 또는 브라우저 응용 프로그램에서 OAUTH 인증 하는 경우 발생 하는 ADFS 문제를 해결 합니다. 오류를 생성 하 고 앱 또는 로그인 하려면 브라우저를 종료 하려면 사용자를 요구 하는 사용자 암호를 변경 합니다. </br></br>utc + 1 엑스트라넷 스마트 잠금 및 더 높은 (유럽 및 아시아)를 사용 하도록 설정 하면 작동 하지 않는 문제를 해결 합니다. 또한 일반 엑스트라넷 잠금 다음 오류로 인해 실패를 발생 시킵니다. Get-AdfsAccountActivity: DateTime.MaxValue 보다 크거나 DateTime.MinValue UTC로 변환 하는 경우 보다 작은 DateTime 값을 JSON으로 직렬화 할 수 없습니다.</br></br>주소는 ADFS Windows Hello 비즈니스 문제를 새 사용자가 PIN을 프로 비전 할 수 없습니다. 이 없는 MFA 공급자를 구성할 때 발생 합니다.|2018년 5월|
|[4093120 (OS 빌드 14393.2214)](https://support.microsoft.com/help/4093120/windows-10-update-kb4093120)| 처리 되지 않은 새로 고침 토큰 유효성 검사 문제를 해결합니다. 다음 오류가 발생합니다. “Microsoft.IdentityServer.Web.Protocols.OAuth.Exceptions.OAuthInvalidRefreshTokenException: MSIS9312: 잘못 된 OAuth 새로 고침 토큰을 수신 합니다. 새로 고침 토큰을 받은 토큰의 허용된 된 시간 보다 이전입니다. " |2018년 4월|
|[4077525 (OS 빌드 14393.2097)](https://support.microsoft.com/help/4077525/windows-10-update-kb4077525)|HTTP 500 오류는 ADFS 팜에서 Windows 내부 데이터베이스 WID ()를 사용 하 여 두 개 이상의 서버에 있을 때 발생 하는 문제를 해결 합니다. 이 시나리오에서는 일부 사용자를 인증 하도록 웹 응용 프로그램 프록시 (WAP) 서버에서 HTTP 기본 사전 인증 실패 합니다. 오류가 발생 하는 경우에 경고 WAP 이벤트 로그에서 이벤트 ID 13039 Microsoft Windows Web Application Proxy를 볼 수 있습니다. 설명 하는 읽기, "웹 응용 프로그램 프록시는 사용자를 인증 하지 못했습니다. 사전 인증은 ' 리치 클라이언트에 대 한 ADFS'입니다. 지정된 된 사용자가 지정 된 신뢰 당사자에 액세스할 수 있는 권한이 없습니다. 대상 신뢰 당사자 또는 WAP 신뢰 당사자 권한 부여 규칙 수정할 필요는 합니다. "</br></br>AD FS 더 이상 무시할 수 프롬프트 문제를 해결 = 인증 하는 동안 로그인 합니다. 사용 안 함 옵션을 암호 인증이 사용 되지 않습니다 하는 시나리오를 지원 하도록 추가 되었습니다. 자세한 내용은 Windows Server 2016 RTM에서 인증 하는 동안 "prompt = login" 매개 변수를 무시 하는 AD FS를 참조 하세요.</br></br>권한이 부여 된 경우 ad FS 문제를 해결 고객 (및 신뢰 당사자) 인증서 선택 하는 인증 옵션을 연결 하지 못합니다. 프롬프트를 사용 하는 경우 오류가 발생 = Windows 통합 인증 WIA () 사용 하도록 설정 및 요청 WIA를 수행할 수 있는 경우 로그인 합니다.</br></br>AD FS 올바르게 표시 되는 위치 하지 홈 영역 검색 (HRD) 페이지 id 공급자 (IDP) OAuth 그룹에서 신뢰 당사자 (RP)과 연결한 경우 문제를 해결 합니다. 여러 Idp가 RP의 OAuth 그룹에서을 사용 하 여 연결 하지 않는 한 사용자 표시 되지 않습니다 HRD 페이지입니다. 대신 사용자가 인증에 대 한 연결 된 IDP로 직접 이동 합니다.|2018년 2월|
|[4041688 (OS 빌드 14393.1794)](https://support.microsoft.com/kb/4041688)|가끔 잘못 된 캐싱 동작 때문에 잘못 된 Id 공급자에 대 한 AD 기관 요청 misdirects는 문제를 해결 하는이 문제가 해결 합니다. 이 다단계 인증 같은 인증 기능 영향을 줄 수 있습니다. </br></br>혼합된 WS2012R2 및 WS2016 ADFS 팜에 올바른 충실도 (자세한 감사 사용)를 사용 하 여 ADFS 서버 상태 보고서에 AAD Connect Health에 대 한 기능을 추가 합니다.</br></br>여기서 2012 업그레이드 동안 R2 ADFS 팜을 ADFS 2016을 문제 해결, 팜 동작 수준 올리기 하는 powershell cmdlet 실패 제한 시간을 사용 하 여 경우 여러 신뢰 당사자 트러스트 합니다.</br></br>AD FS는 요청을 다른 서버 STS (보안 토큰)를 페더레이션 하는 동안 wct 매개 변수 값을 수정 하 여 인증 실패 하면 문제가 해결 되었습니다.|2017년 10월|
|[4038801 (OS 빌드 14393.1737)](https://support.microsoft.com/kb/4038801)|페더레이션된 LDPs를 사용 하 여 OIDC 로그 아웃에 대 한 추가 지원 합니다. 이렇게 하면 "키오스크 시나리오"를 여러 사용자가 순차적으로 로깅될 수 단일 장치에는 LDP 사용 하 여 페더레이션 있는 합니다.</br></br>여기서 CEP/CES 기반 인증서 문제는 gMSA 계정으로 작동 하지 않습니다는 WinHello를 수정 되었습니다.</br></br>문제를 해결 하 고는 Windows 내부 데이터베이스 WID () Windows Server 2016 ADFS 서버의 IdentityServerPolicy.Scopes 및 IdentityServerPolicy.Clients 테이블 ApplicationGroupId 열과 같은 일부 설정은 동기화에 실패 하는 키를 누릅니다) 외래 키로 인해 제약 조건입니다. 이러한 동기화 실패 하면 다양 한 클레임, 클레임 공급자 및 응용 프로그램 환경을 기본에서 보조 ADFS 서버 간 수 있습니다. 또한 WID 주 역할은 보조 노드로 이동 되 면 응용 프로그램 그룹 더 이상 ADFS 관리 사용자 환경에서에서 관리할 수</br></br>이 업데이트는 다단계 인증 제대로 작동 하지 않습니다 사용자 지정 문화권 정의 사용 하는 모바일 장치를 사용 하 여 문제 해결|2017년 9월|
|[4034661 (OS 빌드 14393.1613)](https://support.microsoft.com/kb/4034661)|호출자 IP 주소 nog ADFS 4.0의 보안 이벤트 로그에서 411 이벤트에 의해 기록 되는 문제를 해결 \ "성공 감사" 및 "실패 감사"를 활성화 한 후에 Windows Server 2016 RS1 ADFS 서버.</br></br>ADFX 서버는 HTTP 프록시를 사용 하도록 구성 된 경우 Azure 다중 요소 인증 (MFA) 사용 하 여 문제를 해결 하는이 문제가 해결 됩니다.</br></br>"위치에서 ADFS 프록시 서버에 만료 되거나 해지 된 인증서를 제시지 않습니다 오류를 반환 하지 사용자에 게 문제가 해결 됩니다."|2017년 8월|
|[4034658 (OS 빌드 14393.1593)](https://support.microsoft.com/kb/4034658)|수정 2016 AD FS 서버 온-프레미스 배포 비즈니스용 Windows Hello에 대 한 인증서 등록 MFA를 지원 하기 위해|2017년 8월|
|[4025334 (OS 빌드 14393.1532)](https://support.microsoft.com/kb/4025334)|PkeyAuth 토큰 처리기 pkeyauth 요청이 잘못 된 데이터를 포함 하는 경우 인증을 실패할 수 있습니다 문제를 해결 합니다. 인증 장치 인증을 수행 하지 않고 계속 해야|2017년 7월|
|[4022723 (OS 빌드 14393.1378)](https://support.microsoft.com/kb/4022723)|[웹 응용 프로그램 프록시] DisableHttpOnlyCookieProtection 구성 속성의 값은 선택 되지 WAP 2016에서 2016 년 2012R2 혼합 배포 </br></br>[웹 응용 프로그램 프록시] EAS 사전 인증 시나리오에서 AD FS에서 사용자 액세스 토큰을 가져올 수 없습니다.</br></br>AD FS 2016 : 로그 아웃 시키는 예외를 WSFED|2017년 6월
|[3213986](https://support.microsoft.com/kb/3213986)|X64 기반 시스템 (KB3213986)에 대 한 Windows Server 2016 용 누적 업데이트| 2017년 1월

## <a name="updates-for-ad-fs-and-wap-in-windows-server-2012-r2"></a>AD FS 및 WAP Windows Server 2012 r 2에서에 대 한 업데이트
Windows Server 2012 R2에서 Active Directory Federation Services (AD FS)에 대 한 출시 된 업데이트 및 핫픽스 롤업 목록은 다음과 같습니다.

|KB # |설명|출시 날짜
|----- | ----- |-----
|[4041685](https://support.microsoft.com/kb/4041685)|여기서 MSISConext 쿠키 요청 헤더에 수 결국 헤더 크기 제한에 오버플로 및 HTTP 상태 코드 400 사용 하 여 인증 하는 오류를 발생 시킬 AD FS 문제 해결 "잘못 된 요청-헤더 너무 깁니다"입니다.</br></br>한 문제를 해결 하 고 있는 ADFS 더 이상 무시할 수 "prompt = login" 인증 하는 동안 키를 누릅니다. "사용 안 함된" 옵션을 복원 시나리오-암호 인증을 사용 하는 위치에 추가 되었습니다.|2017 년 10 월 업데이트 롤업 미리 보기|
|[4019217](https://support.microsoft.com/kb/4019217)|작업 폴더 토큰 broker를 사용 하 여 클라이언트에는 Server 2012 R2 AD FS 서버를 사용 하는 경우 작동 하지 않습니다|2017 년 5 월 미리 보기 업데이트 롤업|
|[4015550](https://support.microsoft.com/kb/4015550)|외부 사용자와 AD FS WAP 임의로 요청 전달 실패를 인증 하지 않는 AD FS를 사용 하 여 문제를 해결 했습니다.|2017 년 4 월 업데이트 롤업|
|[4015547](https://support.microsoft.com/kb/4015547)|외부 사용자와 AD FS WAP 임의로 요청 전달 실패를 인증 하지 않는 AD FS를 사용 하 여 문제를 해결 했습니다.|2017 년 4 월 보안 업데이트|
|[4012216](https://support.microsoft.com/kb/4009970)|MS17 019이 보안 업데이트에서 ADFS Active Directory Federation Services () 취약점을 확인합니다. 취약점으로 인해 공격자는 요청을 보냅니다 특별히 구성 된 AD FS 서버에 공격자가 대상 시스템에 대 한 중요 정보를 읽을 수 있도록 하는 경우 정보 공개가 발생할 수 있습니다.|2017 년 3 월 업데이트 롤업|
|[3179574](https://support.microsoft.com/kb/3179574)|AD FS 엑스트라넷 암호 업데이트를 사용 하 여 문제를 해결 했습니다. |2016 년 8 월 업데이트 롤업
|[3172614](https://support.microsoft.com/kb/3172614)|도입 된 프롬프트 = login [지원](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/overview/ad-fs-faq#BKMK_7), AlwaysRequireAuthentication 설정을 확인 하 고 AD FS 관리 콘솔을 사용 하 여 문제를 해결 합니다. |2016 년 7 월 업데이트 롤업
|[3163306](https://support.microsoft.com/kb/3163306)|Active Directory Federation Services (AD FS) 3.0 Secure Sockets Layer (SSL) 포트 636 또는 연결 문자열에 3269 사용 하도록 구성 된 LDAP Lightweight Directory Access Protocol () 특성 저장소에 연결할 수 없습니다. |2016 년 6 월 업데이트 롤업
|[3148533](https://support.microsoft.com/kb/3148533)|Windows Server 2012 r 2에서 ADFS 프록시를 통해 MFA 대체 (fallback) 인증에 실패 |2016년 5월
|[3134787](https://support.microsoft.com/kb/3134787)|AD FS 로그는 Windows Server 2012 r 2에서의 계정 잠금 시나리오에 대 한 클라이언트 IP 주소를 포함 하지 않습니다. |2016 년 2 월
|[3134222](https://support.microsoft.com/kb/3134222)|MS16-020: 서비스 주소 거부에 Active Directory Federation Services 용 보안 업데이트: 2016 년 2 월 9 일|2016 년 2 월
|[3105881](https://support.microsoft.com/kb/3105881)|AD FS Windows Server 2012 R2 기반 서버에서 장치 인증을 사용 하는 경우 응용 프로그램에 액세스할 수 없습니다.|2015년 10월
|[3092003](https://support.microsoft.com/kb/3092003)|페이지를 반복적으로 로드 하 고 사용자가 Windows Server 2012 R2 AD FS에서 MFA를 사용할 때 인증에 실패|2015년 8월
|[3080778](https://support.microsoft.com/kb/3080778)|MFA 어댑터는 Windows Server 2012 r 2에서 예외를 throw 하는 경우 AD FS OnError를 호출 하지 않습니다.|2015 년 7 월
|[3075610](https://support.microsoft.com/kb/3075610)|트러스트 관계를 추가 하거나 Windows Server 2012 r 2에서 클레임 공급자를 제거한 후 보조 AD FS 서버에서 손실 됩니다.|2015 년 7 월
|[3070080](https://support.microsoft.com/kb/3070080)|비 클레임 인식 신뢰 당사자 트러스트에 대 한 제대로 작동 하지 홈 영역 검색|2015년 6월
|[3052122](https://support.microsoft.com/kb/3052122)|Windows Server 2012 r 2에서 AD FS 토큰에 복합 ID 클레임에 대 한 지원을 추가 하는 업데이트|2015 년 5 월
|[3045711](https://support.microsoft.com/kb/3045711)|MS15-040: Active Directory Federation Services의 취약점으로 인 한 정보 공개|2015 년 4 월
|[3042127](https://support.microsoft.com/kb/3042127)|"HTTP 400-잘못 된 요청" Windows Server 2012 r 2에서 WAP 통해 공유 사서함을 열면 하는 동안 오류가 발생 했습니다.|2015년 3월
|[3042121](https://support.microsoft.com/kb/3042121)|Windows Server 2012 r 2에서 웹 응용 프로그램 프록시 인증 토큰에 대 한 AD FS 토큰 재생 보호|2015년 3월
|[3035025](https://support.microsoft.com/kb/3035025)|사용자는 Windows Server 2012 r 2에서 등록 된 장치를 사용 하 여 필요가 없도록 암호 업데이트에 대 한 핫픽스 기능|2015 년 1 월
|[3033917](https://support.microsoft.com/kb/3033917)|AD FS는 Windows Server 2012 r 2에서 SAML 응답을 처리할 수 없습니다.|2015 년 1 월
|[3025080](https://support.microsoft.com/kb/3025080)|Windows Server 2012 r 2에서 웹 응용 프로그램 프록시를 통해 Office 파일을 저장 하려고 할 때 작업이 실패|2015 년 1 월
|[3025078](https://support.microsoft.com/kb/3025078)|묻는 메시지가 사용자에 대 한 다시는 잘못 된 사용자 이름을 사용 하 여 Windows Server 2012 r 2에 로그온 할 때|2015 년 1 월
|[3020813](https://support.microsoft.com/kb/3020813)|Windows Server 2012 R2 AD FS에서 웹 응용 프로그램을 실행할 때 인증을 위해 묻는|2015 년 1 월
|[3020773](https://support.microsoft.com/kb/3020773)|Windows Server 2012 r 2에서 장치 등록 서비스의 초기 배포 후 시간 초과 오류|2015 년 1 월
|[3018886](https://support.microsoft.com/kb/3018886)|메시지가 표시 되는 사용자 이름 및 암호를 두 번 인트라넷에서 Windows Server 2012 R2 AD FS 서버에 액세스할 때|2015 년 1 월
|[3013769](https://support.microsoft.com/kb/3013769)|Windows Server 2012 R2 업데이트 롤업|2014년 12월
|[3000850](https://support.microsoft.com/kb/3000850)|Windows Server 2012 R2 업데이트 롤업|2014년 11월
|[2975719](https://support.microsoft.com/kb/2975719)|Windows Server 2012 R2 업데이트 롤업|2014 년 8 월
|[2967917](https://support.microsoft.com/kb/2967917)|Windows Server 2012 R2 업데이트 롤업|2014년 7월
|[2962409](https://support.microsoft.com/kb/2962409)|Windows Server 2012 R2 업데이트 롤업|2014년 6월
|[2955164](https://support.microsoft.com/kb/2955164)|Windows Server 2012 R2 업데이트 롤업|2014 년 5 월
|[2919355](https://support.microsoft.com/kb/2919355)|Windows Server 2012 R2 업데이트 롤업|2014년 4월

## <a name="updates-for-ad-fs-in-windows-server-2012-ad-fs-21-and-ad-fs-20"></a>Windows Server 2012 (AD FS 2.1) 및 AD에서 AD FS에 대 한 업데이트 FS 2.0
AD FS 2.0 및 2.1에 대 한 출시 된 업데이트 및 핫픽스 롤업 목록은 다음과 같습니다.

|KB # |설명|출시 날짜|적용 대상:
|----- | ----- |-----|-----
|[3197878](https://support.microsoft.com/kb/3197878)|Windows Server 2012 (이것이 일반적인 3094446 핫픽스 릴리스)에서 프록시를 통해 인증 실패|2016 년 11 월 품질 롤업|AD FS 2.1
|[3197869](https://support.microsoft.com/kb/3197869)|Windows Server 2008 R2 SP1 (이것이 일반적인 3094446 핫픽스 릴리스)에서 프록시를 통해 인증 실패|2016 년 11 월 품질 롤업|AD FS 2.0
|[3094446](https://support.microsoft.com/kb/3094446)|Windows Server 2012 또는 Windows Server 2008 R2 s p 1에서 프록시를 통해 인증 실패|2015년 9월|AD FS 2.0 및 2.1
|[3070078](https://support.microsoft.com/kb/3070078)|AD FS 2.1 암호화 인증서를 Windows Server 2012에 대해 인증할 때 예외를 throw|2015 년 7 월|AD FS 2.1
|[3062577](https://support.microsoft.com/kb/3062577)|MS15-062: Active Directory 페더레이션 서비스의 취약점으로 인 한 권한 상승|2015년 6월|AD FS 2.0 / 2.1
|[3003381](https://support.microsoft.com/kb/3003381)|MS14-077: Active Directory Federation Services의 취약점으로 인 한 정보 공개 문제점: 2015 년 4 월 14 일|2014년 11월|AD FS 2.0 / 2.1
|[2987843](https://support.microsoft.com/kb/2987843)|많은 사용자가 Windows Server 2012에서 웹 응용 프로그램에 로그온 하는 경우 AD FS 페더레이션 서버의 메모리 사용량은 계속 증가|2014년 7월|AD FS 2.1
|[2957619](https://support.microsoft.com/kb/2957619)|위임 된 토큰에 대 한 AD FS를 요청 하는 경우 중지 됩니다. AD FS에서 신뢰 당사자 트러스트|2014 년 5 월|AD FS 2.1
|[2926658](https://support.microsoft.com/kb/2926658)|SQL 권한이 없을 경우 ADFS SQL 팜 배포 실패|2014년 10월|AD FS 2.1
|[2896713](https://support.microsoft.com/kb/2896713) 또는 [2989956](https://support.microsoft.com/kb/2989956)|업데이트는 AD FS 서버에 2843638 보안 업데이트를 설치 하려면 몇 가지 문제를 해결 하려면|2013 년 11 월</br></br>2014 년 9 월|AD FS 2.0 / 2.1
|[2877424](https://support.microsoft.com/kb/2877424)|업데이트를 사용 하면 2.1 팜의 AD FS에서 여러 신뢰 당사자 트러스트에 대 한 인증서가 두 개를 사용 하 여|2013년 10월|AD FS 2.1
|[2873168](https://support.microsoft.com/kb/2873168)|해결 방법: 타사 CSP 및 HSM을 사용 하 고 AD FS 2.0 Windows Server 2008 R2 서비스 팩 1 용 업데이트 롤업 3에서 클레임 공급자 트러스트를 구성한 경우 오류 발생|2013 년 9 월|AD FS 2.0
|[2861090](https://support.microsoft.com/kb/2861090)|Windows Server 2008 R2 s p 1에서 예외를 발생 하는 암호화 인증서의 주체 이름에 쉼표|2013년8월|AD FS 2.0
|[2843639](https://support.microsoft.com/kb/2843639)|[보안] Active Directory Federation Services의 취약점으로 인 한 정보 공개|2013 년 11 월|AD FS 2.1
|[2843638](https://support.microsoft.com/kb/2843638)|MS13-066: Active Directory Federation Services 2.0에 대 한 보안 업데이트 설명: 2013 년 8 월 13 일|2013년8월|AD FS 2.0
|[2827748](https://support.microsoft.com/kb/2827748)|Federationmetadata.xml 파일에 Windows Server 2012에서 Ws-trust 및 Ws-federation 끝점에 대 한 MEX 끝점 정보가 없습니다.|2013년 5월|AD FS 2.1
|[2790338](https://support.microsoft.com/kb/2790338)|Active Directory Federation Services (AD FS)에 대 한 업데이트 롤업 3의 설명 2.0|2013년 3월|AD FS 2.0
