---
title: CAPolicy.inf 파일 준비
description: CAPolicy.inf에서 Active Directory 인증 서비스 (AD CS)를 설치 하거나 CA 인증서를 갱신할 때 사용 되는 다양 한 설정을 포함 합니다.
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 19a87df7c4f165d3b0e6c5add4bc40ff97cc87cb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446464"
---
# <a name="capolicyinf-syntax"></a>CAPolicy.inf 구문
>   적용 대상: Windows Server (반기 채널), Windows Server 2016

CAPolicy.inf 구성 파일 확장, 제한 및 루트 CA 인증서 및 루트 CA에서 발급 된 모든 인증서에 적용 되는 다른 구성 설정을 정의 하는 경우 CAPolicy.inf 파일의 설치 루틴을 루트 CA를 시작 하기 전에 호스트 서버에 설치 되어야 합니다. 루트 CA에 대 한 보안 제한 수정할 경우 루트 인증서를 갱신 및 갱신 프로세스를 시작 하기 전에 업데이트 된 CAPolicy.inf 파일 서버에 설치 해야 합니다.

CAPolicy.inf 다음과 같습니다.

-   작성 및 정의 하는 관리자가 수동으로

-   루트 및 하위 CA 인증서를 만드는 동안 사용

-   서명 CA 서명 하 고 (없습니다 요청 부여 되는 CA) 인증서를 발급 하는 위치 정의

에 복사 해야 CAPolicy.inf 파일을 만든 후 합니다 **%systemroot%** ADCS를 설치 하거나 CA 인증서를 갱신 하기 전에 서버의 폴더입니다.

CAPolicy.inf 지정 하 고 다양 한 CA 특성 및 옵션을 구성할 수 있습니다. 다음 섹션에서는 특정 요구 사항에 맞는.inf 파일을 만들 수에 대 한 모든 옵션을 설명 합니다.

## <a name="capolicyinf-file-structure"></a>CAPolicy.inf 파일 구조

다음 용어는.inf 파일 구조를 설명 하는 데 사용 됩니다.

-   _섹션_ – 키의 논리적 그룹을 포함 하는 파일의 영역입니다. .Inf 파일의 섹션 이름은 대괄호로 표시로 식별 됩니다. 많은 전부는 아니지만, 섹션 확장 인증서를 구성 하는 데 사용 됩니다.

-   _키_ – 항목의 이름이 며 등호의 왼쪽에 나타납니다.

-   _값_ – 매개 변수 및 등호의 오른쪽에 나타납니다.

아래 예에서 **[Version]** 는 섹션이 **서명** 키 및 **"\$Windows NT\$"** 값입니다.

예:

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>버전

.Inf 파일을 식별 합니다. 버전이 유일한 필수 섹션 및 CAPolicy.inf 파일의 시작 부분에 있어야 합니다.

###  <a name="policystatementextension"></a>PolicyStatementExtension

조직에서 정의한 정책을 나열 된 옵션 또는 필수일 및 합니다. 여러 정책은 쉼표로 구분 됩니다. 이름 또는 이러한 정책의 있는지 여부를 확인 하는 사용자 지정 응용 프로그램 관련 하 여 특정 배포의 컨텍스트에서 의미를 갖습니다.

정의 된 각 정책에 대해 해당 특정 정책에 대 한 설정을 정의 하는 섹션 이어야 합니다. 각 정책에 대 한 사용자 정의 개체 식별자 (OID)를 제공 해야 하 고 텍스트 표시 하려는 정책 설명 또는 정책 설명에 대 한 URL 포인터입니다. URL은 HTTP, FTP, 또는 LDAP URL 형식의 수 있습니다.

정책 설명에 설명 텍스트를 포함 하려는 경우에 다음 세 행을 CAPolicy.inf의 같은 형태가 됩니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

CA 정책 문을 호스트 하는 URL을 사용 하도록 하려는 경우 다음 다음 세 줄 대신 같습니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
```

이 밖에도 다음 지침을 따릅니다.

-   여러 URL 및 알림 키가 지원 됩니다.

-   동일한 정책 섹션에서 알림 및 URL 키가 지원 됩니다.

-   공백 사용 하 여 Url 또는 공백 사용 하 여 텍스트 따옴표로 묶어야 합니다. 에 대해서는 **URL** 나타나는 섹션에 관계 없이 키입니다.

여러 통지 및 정책 섹션에서 Url의 예는 같습니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

CAPolicy.inf의 루트 CA 인증서에 대 한 CRL 배포 지점 (Cdp)을 지정할 수 있습니다.  CA를 설치한 후 CA에서 발급 한 각 인증서를 포함 하는 CDP Url을 구성할 수 있습니다. 루트 CA 인증서 CAPolicy.inf 파일의이 섹션에서는 지정 된 Url을 보여 줍니다. 

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

이 섹션에 대 한 몇 가지 추가 정보:
-   지원합니다.
    - HTTP 
    - 파일 Url
    - LDAP Url 
    - 여러 Url
   
    >[!IMPORTANT]
    >HTTPS Url을 지원 하지 않습니다.

-   따옴표는 공백을 사용 하 여 Url을 둘러싸야 합니다.

-   Url이 없거나 지정 된 경우 – 즉, 경우 합니다 **[CRLDistributionPoint]** 섹션 파일에 존재 하지만 비어 – 기관 정보 액세스 확장 루트 CA 인증서에서 생략 됩니다. 이 루트 CA 설정할 때 것이 좋습니다. Windows에서 해지 불필요 한 루트 CA 인증서의 CDP 확장 이므로 루트 CA 인증서에 대 한 검사를 수행 하지 않습니다.

-    CA는 클라이언트가 HTTP를 통해 검색 되는 위치는 웹 사이트의 폴더를 나타내는 공유에 예를 들어, UNC 파일을 게시할 수 있습니다.

-   루트 CA 설정 또는 루트 CA 인증서를 갱신 하는 경우에이 절을 사용 합니다. CA는 하위 CA의 CDP 확장을 결정합니다.
   

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

루트 CA 인증서에 대 한 CAPolicy.inf에 기관 정보 액세스 포인트를 지정할 수 있습니다.

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

기관 정보 액세스 섹션에서 몇 가지 추가 참고 사항:

-   Url은 여러 개 지원 됩니다.

-   HTTP, FTP, LDAP 및 파일 Url 지원 됩니다. HTTPS Url은 사용 하는 것이 없습니다.

-   이 섹션에서는 루트 CA 설정 또는 루트 CA 인증서를 갱신 하는 경우에 사용 됩니다. 하위 CA AIA 확장 하위 CA의 인증서를 발급 한 CA에서 결정 됩니다.

-   공백 사용 하 여 Url은 따옴표로 묶어야 합니다.

-   Url이 없거나 지정 된 경우 – 즉, 경우 합니다 **[AuthorityInformationAccess]** 섹션 파일에 존재 하지만 비어 – CRL 배포 지점 확장 루트 CA 인증서에서 생략 됩니다. 마찬가지로 루트 CA 인증서에 대 한 링크에서 참조 하는 보다 높은 인증 기관이 없는 없기 때문에 루트 CA 인증서의 경우 기본 설정이 됩니다.

### <a name="certsrvserver"></a>certsrv_Server

CAPolicy.inf의 다른 선택적 섹션은 [certsrv_server] 되는 CA에 대 한 갱신 키 길이, 갱신 유효 기간 및 인증서 해지 목록 (CRL) 유효 기간을 지정 하는 데 사용 되는 갱신 되거나 설치 합니다. 이 섹션에 있는 키의 하지 않아도 됩니다. 이러한 설정 중 대부분은 대부분의 요구 사항에 대 한 충분 한 CAPolicy.inf 파일에서 생략 될 수 있으며 기본 값을 갖습니다. 또는 이러한 설정 중 대부분은 CA를 설치한 후 변경할 수 있습니다.

예제는 다음과 같이 보입니다.

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

**RenewalKeyLength** 만 갱신에 대 한 키 크기를 설정 합니다. 이 새 키 쌍을 CA 인증서를 갱신 하는 동안 생성 될 때만 사용 됩니다. 초기 CA 인증서에 대 한 키 크기는 CA를 설치할 때 설정 됩니다.

새 키 쌍을 사용 하 여 CA 인증서를 갱신 하는 경우 키 길이 수 있습니다 하거나 증가 또는 감소 시켜야 합니다. 예를 들어, 루트 CA 키 크기는 4096 바이트 또는 그 이상으로 설정 하 고 다음 검색 하는 경우 키 크기가 2048 바이트 지원할 수 있는 네트워크 장치 또는 Java 앱입니다. 크기를 늘리거나 여부를 해당 CA에서 발급 한 모든 인증서를 다시 실행 해야 합니다.

**RenewalValidityPeriod** 하 고 **RenewalValidityPeriodUnits** 이전 루트 CA 인증서를 갱신 하는 경우 새 루트 CA 인증서의 수명을 설정 합니다. 루트 CA에만 적용 됩니다. 해당 상위에서 하위 CA의 인증서 수명 결정 됩니다. RenewalValidityPeriod 다음 값을 가질 수 있습니다. 시간, 일, 주, 월 및 연도입니다.

**수명은** 하 고 **CRLPeriodUnits** 기본 crl 유효 기간을 설정 합니다. **수명은** 다음 값을 가질 수 있습니다. 시간, 일, 주, 월 및 연도입니다.

**CRLDeltaPeriod** 하 고 **CRLDeltaPeriodUnits** 델타 CRL의 유효 기간을 설정 합니다. **CRLDeltaPeriod** 다음 값을 가질 수 있습니다. 시간, 일, 주, 월 및 연도입니다.

이러한 각 설정은 CA를 설치한 후 구성할 수 있습니다.

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

적용 하려면 변경 내용을 Active Directory 인증서 서비스를 다시 시작 해야 합니다.

**된** 엔터프라이즈 CA 설치 중에 적용 됩니다. 이 설정 하거나 True 또는 False (또는 1 또는 0)을 결정 하는 경우 CA는 기본 템플릿 중 하나를 사용 하 여 구성 됩니다.

CA의 기본 설치에서 기본 인증서 템플릿의 일부는 인증 기관 스냅인의 인증서 템플릿 폴더에 추가 됩니다. 이 AD CS 서비스 역할이 설치 된 후 시작 되는 즉시 충분 한 권한이 있는 컴퓨터나 사용자 수 즉시 인증서를 등록할 것을 의미 합니다.

기본 템플릿은 엔터프라이즈 CA에 추가 되 고 하지 못하도록 된 설정을 사용할 수 있도록 CA를 설치한 후에 즉시 모든 인증서를 발급 하지 않을 수도 있습니다. 템플릿이 CA에 구성 된 경우 인증서가 없습니다.을 발급할 수 있습니다.

**AlternateSignatureAlgorithm** PKCS를 지원 하도록 CA 구성\#CA 인증서 및 인증서 요청에 대해 1 V2.1 시그니처 형식입니다. 루트 CA에서 1로 설정 된 경우 CA 인증서는 PKCS\#1 V2.1 시그니처 형식입니다. 하위 CA에 설정 된 경우 하위 CA는 인증서 요청 만들기 PKCS를 포함 하는\#1 V2.1 시그니처 형식입니다.

**ForceUTF8** 기본값 변경의 고유 주체와 발급자의 상대 고유 이름 (Rdn) 인코딩을 u t F-8로 이름을 합니다. 디렉터리 문자열 형식을 RFC, 영향을 받는 정의 된 것과 같은 u t F-8을 지 원하는 이러한 Rdn를만 합니다. 예를 들어 도메인 구성 요소 (DC)에 대 한 RDN을 Country RDN (C) 인쇄할 수 있는 문자열로 인코딩만 지원 하지만 IA5 또는 u t F-8로 인코딩 지원 합니다. ForceUTF8 지시문 따라서 DC RDN에 영향을 하지만 C RDN 영향을 주지 않습니다.

**EnableKeyCounting** CA의 서명 키를 사용할 때마다 카운터를 증가 시킬 CA를 구성 합니다. 하드웨어 보안 모듈 (HSM) 및 키 계산을 지 원하는 연결 된 암호화 서비스 공급자 (CSP) 하는 경우에이 설정을 사용 하지 마십시오. Microsoft 강력한 CSP 아니고는 Microsoft 소프트웨어 키 저장소 공급자 KSP () 지원 키를 계산 합니다.


## <a name="create-the-capolicyinf-file"></a>CAPolicy.inf 파일 만들기

AD CS를 설치 하기 전에 구성한 CAPolicy.inf 파일 특정 설정을 사용 하 여 배포 합니다.

**필수 구성 요소:** Administrators 그룹의 멤버 여야 합니다.

1. AD CS를 Windows PowerShell을 열고 설치 하려는 컴퓨터에서 입력 **메모장 c:\CAPolicy.inf** ENTER 키를 누릅니다.

2. 새로운 파일을 생성할지 묻는 메시지가 표시되면 **예**를 클릭합니다.

3. 다음을 파일의 내용으로 입력합니다.
   ```
   [Version]  
   Signature="$Windows NT$"  
   [PolicyStatementExtension]  
   Policies=InternalPolicy  
   [InternalPolicy]  
   OID=1.2.3.4.1455.67.89.5  
   Notice="Legal Policy Statement"  
   URL=https://pki.corp.contoso.com/pki/cps.txt  
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
4. 클릭 **파일**를 클릭 하 고 **다른 이름으로 저장**합니다.

5. % Systemroot % 폴더로 이동 합니다.

6. 다음을 확인합니다.

   -   **파일 이름**이 **CAPolicy.inf**로 설정됨

   -   **파일 형식**이 **모든 파일**로 설정됨

   -   **인코딩**이 **ANSI**임

7. **저장**을 클릭합니다.

8. 파일을 덮어쓸지 묻는 메시지가 나타나면 **예**를 클릭합니다.

   ![CAPolicy.inf 파일에 대 한 이름으로 저장 위치](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

   > [!CAUTION]
   >   CAPolicy.inf를 inf 확장명으로 저장하도록 합니다. 파일 이름 끝에 **.inf**를 특별히 입력하지 않고 설명된 대로 옵션을 선택하지 않는다면 파일이 텍스트 파일로 저장되고 CA 설치 중에 사용되지 않습니다.

9. 메모장을 닫습니다.

> [!IMPORTANT]
>   CAPolicy.inf에서 보면 URL을 지정 하는 줄 https://pki.corp.contoso.com/pki/cps.txt합니다. CAPolicy.inf의 내부 정책 섹션은 CPS(인증서 사용 약관)의 위치를 지정하는 방법을 보여주는 예시로 제공되었습니다. 이 가이드에서는 하지 지시를 받았습니다는 인증서 cps ()를 만듭니다.
