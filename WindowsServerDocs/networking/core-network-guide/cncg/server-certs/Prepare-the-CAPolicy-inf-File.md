---
title: CAPolicy.inf 파일 준비
description: CAPolicy.inf 포함 Active Directory 인증 서비스 (광고 CS)를 설치 하거나는 캘리포니아 갱신 때 사용 되는 다양 한 설정 인증서 합니다.
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9618d4abe512b487f4f22ffde85a052c1c52ef22
ms.sourcegitcommit: fb4e2ace2e0a29e0f6b028f1cb945cab6aa6ee2c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
---
# <a name="capolicyinf-syntax"></a>CAPolicy.inf 구문
>   적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

CAPolicy.inf은 구성 파일 확장명, 제한 및 루트 인증서를 및 루트 캘리포니아에서 발급 한 모든 인증서에 적용 되는 기타 구성 설정을 정의입니다. 호스트 서버의 루트 캘리포니아 시작 설정 루틴 하기 전에 CAPolicy.inf 파일을 설치 해야 합니다. 루트 캘리포니아에 대 한 보안 제한 수정 해야 하는, 루트 인증서 갱신 및 갱신 프로세스를 시작 하기 전에 업데이트 CAPolicy.inf 파일 서버에 설치 해야 합니다.

CAPolicy.inf는 다음과 같습니다.

-   만들고 관리자 수동으로 정의

-   루트 하위 캘리포니아 인증서를 생성 하는 동안 이용

-   로그인 하 고 (하지 요청 부여 되 고 캐나다) 인증서를 발급 서명 캘리포니아에 정의 된

CAPolicy.inf 파일을 만든 후에 복사 해야 하는 **% 시스템 루트** 캘리포니아 인증서 갱신 하거나 ADC 설치 하기 전에 서버 폴더 합니다.

CAPolicy.inf 지정 하 고 캘리포니아 특성과 옵션의 다양 한 구성 수 있습니다. 다음 섹션 사용자의 특정 요구에 맞게.inf 파일을 만들 수 있는 모든 옵션에 설명 합니다.

## <a name="capolicyinf-file-structure"></a>CAPolicy.inf 파일 구조

다음 단어.inf 파일 구조 설명 하기 위해 사용 됩니다.

-   _섹션_ – 영역 키 논리 그룹 담당 하는 파일입니다. .Inf 파일의 이름이 섹션 대괄호에서 표시가 표시 됩니다. 많은, 있지만, 일부 섹션 인증서 확장 구성 하는 데 사용 합니다.

-   _키_ – 항목의 이름이 고 등호의 왼쪽에 나타납니다.

-   _값_ 매개 및 등호의 오른쪽에 나타나는입니다.

아래의 예제 **[버전]** 는 섹션을 **서명** 은, 키와 **"\ $ Windows NT \ $"** 값 합니다.

예:

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>버전

.Inf 파일을 식별 합니다. 버전이 경우에 필요 섹션 및 CAPolicy.inf 파일의 시작 부분에 있어야 합니다.

###  <a name="policystatementextension"></a>PolicyStatementExtension

조직에서 정의 된 정책을 나열는 선택적 또는 필수입니다. 여러 개의 정책은 쉼표로 구분 됩니다. 이름이이 정책 있는지 확인 하는 사용자 지정 응용 프로그램 또는 특정 배포의 컨텍스트에서 의미가.

각 정책에 정의 된에 대 한 설정을 해당 특정 정책에 정의 된 섹션 여야 합니다. 각 정책에 대 한 사용자 정의 개체 식별자 (OID)를 제공 해야 하 고 텍스트 표시할 정책 설명 또는 정책 정책에 대 한 URL 포인터 합니다. URL은 HTTP, FTP 또는 LDAP URL 형태의 될 수 있습니다.

설명을 정책 설명에 있는 경우 다음 CAPolicy.inf 다음 세 줄 같습니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

캘리포니아 정책 호스팅할 URL을 사용할 경우 다음 다음 세 줄 대신 같습니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=http://pki.wingtiptoys.com/policies/legalpolicy.asp
```

또한:

-   여러 URL 및 알림 키가 지원 됩니다.

-   동일한 정책 섹션의 공지 및 URL 키가 지원 됩니다.

-   공간을 사용 하 여 텍스트 또는 공백이 Url 둘러싸여 있어야 인용 됩니다. 이 문제가 잘 일어납니다에 대 한는 **URL** 나타나는 섹션에 관계 없이 키.

여러 알림 및 Url 정책 섹션에서의 예로 같습니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=http://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

CAPolicy.inf에서에서 루트 인증서를에 대 한 배포 Cdp CRL 지점 ()를 지정할 수 있습니다. 캘리포니아는 설치 된 후는 캘리포니아 발급 된 인증서 각에 포함 된 CDP Url 구성할 수 있습니다. CAPolicy.inf 파일의이 섹션에 지정 된 Url 루트 캘리포니아 인증서 자체에 포함 됩니다.

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

이 섹션에 대 한 몇 가지 추가 정보.

-   여러 Url 지원 됩니다.

-   HTTP, FTP 및 LDAP Url 지원 됩니다. HTTPS Url 지원 되지 않습니다.

-   이 섹션 루트 캘리포니아를 설정 하거나 루트 인증서 갱신 하는 경우에 사용 됩니다. 캘리포니아 CDP 확장 하위 하위 인증서 문제는 캘리포니아 따라 결정 됩니다.

-   Url 공백 사용 하 여 인용 둘러싸여 있어야 합니다.

-   Url이 없거나 지정 된 경우 – 즉, 하는 경우는 **[CRLDistributionPoint]** CRL 배포 지점 확장 캘리포니아 루트 인증서의 생략 섹션 파일에 있지만 비어입니다. 캘리포니아 루트를 설정할 때 좋습니다. Windows 해지 CDP 확장 루트 인증서를에 불필요 한 이므로 루트 캘리포니아 인증서의 확인을 수행 하지 않습니다.

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

루트 인증서에 대 한 CAPolicy.inf 기관 정보가 액세스 지점 수가 가장 지정할 수 있습니다.

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

섹션 기관 정보에 대 한 몇 가지 추가 노트에 액세스합니다.

-   여러 Url 지원 됩니다.

-   HTTP, FTP, LDAP 파일 Url 지원 됩니다. HTTPS Url 지원 되지 않습니다.

-   이 섹션 루트 캐나다를 설정 하거나 루트 인증서 갱신 하는 경우에 사용 됩니다. 캘리포니아 AIA 확장 하위 하위 캘리포니아 인증서를 발급 한 캘리포니아 따라 결정 됩니다.

-   Url 공백 사용 하 여 인용 둘러싸여 있어야 합니다.

-   Url이 없거나 지정 된 경우 – 즉, 하는 경우는 **[AuthorityInformationAccess]** CRL 배포 지점 확장 캘리포니아 루트 인증서의 생략 섹션 파일에 있지만 비어입니다. 다시 루트 인증서에 대 한 링크가에서 참조 되 해야 하는 캘리포니아 보다 더 기관이 그대로 루트 인증서를의 경우 기본 설정 됩니다.

### <a name="certsrvserver"></a>certsrv_Server

다른 옵션 CAPolicy.inf 섹션은 [certsrv_server] 있는 캐나다에 대 한 갱신 키 길이, 갱신 유효 기간 및 해지 CRL (목록) 인증서 유효 기간의 지정 하는 데 사용 되는 갱신 되거나 설치 되지 합니다. 이 섹션의 키 하지 않아도 됩니다. 이러한 설정 중 상당수는 CAPolicy.inf 파일에서 간단 하 게 생략 수 있는 대부분 요구 사항에 대 한 충분 한 기본값이 합니다. 또는 이러한 설정 중 상당수는 캘리포니아 설치 된 후 변경할 수 있습니다.

예를 들어는 다음과 같습니다.

```
[certsrv_server]
RenewalKeyLength=2048
RenewalValidityPeriod=Years
RenewalValidityPeriodUnits=5
CRLPeriod=Days
CRLPeriodUnits=2
CRLDeltaPeriod=Hours
CRLDeltaPeriodUnits=4
ClockSkewMinutes=20
LoadDefaultTemplates=True
AlternateSignatureAlgorithm=0
ForceUTF8=0
EnableKeyCounting=0
```

**RenewalKeyLength** 만 갱신에 대 한 주요 크기를 설정 합니다. 새 주요 페어링 하는 동안 캘리포니아 인증서 갱신 생성 되 면만 사용 됩니다. 설치 되 고 캐나다 초기 캘리포니아 인증서에 대 한 주요 크기 설정 됩니다.

경우 새로운 키 쌍 된 인증서를을 갱신, 키 길이 수 늘렸으며 하거나 줄여 합니다. 예를 들어 루트 4096 바이트 이상, 캘리포니아 주요 크기를 설정 하 고 다음 발견 하는 경우 있는 Java 않는 앱 이나 네트워크 디바이스의 2048 바이트 주요 크기 지원할 수 있습니다. 크기 늘리거나 수 있는지 여부를 해당 캘리포니아 하 여 모든 인증서 다시 실행 해야 있습니다.

**RenewalValidityPeriod** 및 **RenewalValidityPeriodUnits** 이전 캘리포니아 루트 인증서 갱신 새 캘리포니아 루트 인증서의 수명을 설정 합니다. 캘리포니아 루트에만 적용 됩니다. 하위 캐나다의 인증서 수명 해당 상사에 의해 결정 됩니다. RenewalValidityPeriod 다음 값을 할 수 있습니다: 시간, 일, 주, 개월 및 년 합니다.

**수명은** 및 **CRLPeriodUnits** 기본 CRL에 대 한 유효 기간을 설정 합니다. **수명은** 다음 값은: 시간, 일, 주, 개월 및 년 합니다.

**CRLDeltaPeriod** 및 **CRLDeltaPeriodUnits** CRL 델타 유효 기간의 설정 합니다. **CRLDeltaPeriod** 다음 값은: 시간, 일, 주, 개월 및 년 합니다.

캘리포니아는 설치 된 후 이러한 설정을 구성할 수 있습니다.

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

적용 하려면 모든 변경에 대 한 Active Directory 인증서 서비스 다시 시작 해야 합니다.

**LoadDefaultTemplates** 엔터프라이즈 캘리포니아 설치 하는 동안에 적용 됩니다. 참 중 하나는이 설정을 또는 False 또는 1 하거나 (0), 명시 기본 템플릿을 사용 하 여는 캘리포니아 구성 됩니다.

캐나다의 기본 설치 기본 인증서 템플릿의 하위 집합 인증 기관 스냅인 인증서 템플릿 폴더에 추가 됩니다. 이 광고 CS 서비스 역할을 설치한 후에 시작 되는 즉시 사용자 또는 컴퓨터 권한이 있는 즉시 등록할 수 인증서 의미 합니다.

기본 템플릿을 엔터프라이즈 캘리포니아에 추가 되지 않도록 하려면 LoadDefaultTemplates 설정을 사용할 수 있도록 한 캘리포니아 설치가 완료 된 후 직후 인증서 실행 하지 않을 수도 있습니다. 경우에 캘리포니아 구성 템플릿이 인증서를 실행할 수 있습니다.

**AlternateSignatureAlgorithm** 인증서 및 인증서 요청 PKCS\ #1 v 2.1 서명 형식을 지원 하기 위해 캘리포니아 구성 합니다. 1 루트로 설정 하면 캘리포니아 캘리포니아 인증서 PKCS\ #1 v 2.1 서명 형식을 포함 됩니다. 하위 수준에서 설정 된 경우 캐나다, 하위 캘리포니아 만들어집니다 인증서 요청 하는 PKCS\ #1 v 2.1 서명 형식을 포함 되어 있습니다.

**ForceUTF8** 기본 변경 상대 고유 이름의 (Rdn)의 제목 및 발행인이 인코딩 고유 F-8 이름입니다. 디렉터리 문자열 유형 RFC에 의해 영향을 받는으로 정의 된 해당 등 F-8 지원 해당 Rdn를만 합니다. 예를 들어 있는 Country RDN (C)를 인쇄 가능한 문자열로 인코딩 지원 IA5 또는 F-8 인코딩 RDN 도메인 구성 요소 (DC)에 대 한 지원 합니다. ForceUTF8 지시문 따라서 DC RDN에 영향을 하지만 C RDN 영향을 주지 않습니다.

**EnableKeyCounting** 캐나다의 서명 키를 사용할 때마다 카운터 증가 캘리포니아 구성 합니다. 하드웨어 보안 HSM (모듈)와 관련된 암호화 CSP (서비스 공급자) 주요 계산 지 있는 경우이 설정을 사용 하지 마십시오. Microsoft는 강력한 CSP 지도 Microsoft 소프트웨어 키 저장소 공급자 KSP () 지원 주요 수를 계산.


## <a name="create-the-capolicyinf-file"></a>CAPolicy.inf 파일 만들기

AD CS 설치 하기 전에 파일을 구성 하기 CAPolicy.inf 특정 설정을 사용 하 여 배포 합니다.

**필수 조건:** 관리자가 그룹의 회원 여야 합니다.

1.  광고 CS 열기 Windows PowerShell 설치 하려는 컴퓨터에서 입력 **메모장 c:.inf** ENTER 키를 누릅니다.

2.  새 파일을 메시지가 표시 되 면 클릭 **예**합니다.

3.  파일의 내용으로 다음을 입력 합니다.
   ```
   [Version]  
    Signature="$Windows NT$"  
    [PolicyStatementExtension]  
    Policies=InternalPolicy  
    [InternalPolicy]  
    OID=1.2.3.4.1455.67.89.5  
    Notice="Legal Policy Statement"  
    URL=http://pki.corp.contoso.com/pki/cps.txt  
    [Certsrv_Server]  
    RenewalKeyLength=2048  
    RenewalValidityPeriod=Years  
    RenewalValidityPeriodUnits=5  
    CRLPeriod=weeks  
    CRLPeriodUnits=1  
    LoadDefaultTemplates=0  
    AlternateSignatureAlgorithm=1  
    [CRLDistributionPoint]  
    [AuthorityInformationAccess]
   ```
1.  클릭 **파일**을 차례로 클릭 하 고 **다른 이름으로 저장**합니다.

2.  % 시스템 루트 % 폴더로 이동 합니다.

3.  다음 있는지 확인 합니다.

    -   **파일 이름** 로 설정 되어 **CAPolicy.inf**

    -   **파일 형식** 로 설정 되어 **모든 파일**

    -   **인코딩** 는 **ANSI**

4.  클릭 **저장**합니다.

5.  파일은 덮어쓰기를 하 라는 메시지가 나타나면 클릭 **예**합니다.

    ![CAPolicy.inf 파일에 대 한 다른 이름으로 저장 위치](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

    >   [!CAUTION]  
    >   Inf 확장명을 가진 CAPolicy.inf 저장 해야 합니다. 특히 입력 하지 않으면 **.inf** 끝에 설명 된 대로 옵션 선택와 파일 이름을 파일 텍스트 파일로 저장 및 캘리포니아 설치 하는 동안 사용 되지 것입니다.

6.  메모장을 닫습니다.

>   [!IMPORTANT]  
>   CAPolicy.inf 볼 수 있습니다 URL 지정 하는 줄 http://pki.corp.contoso.com/pki/cps.txt합니다. CAPolicy.inf의 내부 정책 섹션 인증서 약관 (CPS)의 위치를 지정 되는 어떻게 예를 들어만 표시 됩니다. 이 가이드에서는 하지 인증서 약관 (CPS) 만드는 나와 있습니다.
