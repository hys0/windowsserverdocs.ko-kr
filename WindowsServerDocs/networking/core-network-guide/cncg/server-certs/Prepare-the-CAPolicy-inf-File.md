---
title: CAPolicy.inf 파일 준비
description: Capolicy.inf에는 Active Directory 인증 서비스 (AD CS)를 설치 하거나 CA 인증서를 갱신할 때 사용 되는 다양 한 설정이 포함 되어 있습니다.
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 810f6f8ba9e33f1f26f49f542ad6d23819deb463
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406286"
---
# <a name="capolicyinf-syntax"></a>Capolicy.inf 구문
>   적용 대상: Windows Server(반기 채널), Windows Server 2016

Capolicy.inf는 루트 ca 인증서 및 루트 CA에서 발급 한 모든 인증서에 적용 되는 확장, 제약 조건 및 기타 구성 설정을 정의 하는 구성 파일입니다. 루트 CA에 대 한 설치 루틴이 시작 되기 전에 Capolicy.inf 파일이 호스트 서버에 설치 되어 있어야 합니다. 루트 CA에 대 한 보안 제한을 수정 해야 하는 경우 갱신 프로세스를 시작 하기 전에 루트 인증서를 갱신 하 고 업데이트 된 Capolicy.inf 파일을 서버에 설치 해야 합니다.

Capolicy.inf는 다음과 같습니다.

-   관리자가 수동으로 만들고 정의

-   루트 및 하위 CA 인증서를 만드는 동안 사용 됩니다.

-   인증서를 서명 하 고 발급 하는 서명 CA (요청이 부여 된 CA 아님)에 정의 되어 있습니다.

Capolicy.inf 파일을 만든 후에는 ADCS를 설치 하거나 CA 인증서를 갱신 하기 전에 서버의 **% systemroot%** 폴더에 복사 해야 합니다.

Capolicy.inf를 사용 하면 다양 한 CA 특성 및 옵션을 지정 하 고 구성할 수 있습니다. 다음 섹션에서는 특정 요구 사항에 맞게 조정 된 .inf 파일을 만들기 위한 모든 옵션에 대해 설명 합니다.

## <a name="capolicyinf-file-structure"></a>Capolicy.inf 파일 구조

다음 용어는 .inf 파일 구조를 설명 하는 데 사용 됩니다.

-   _섹션_ -논리적 키 그룹을 포함 하는 파일의 영역입니다. .Inf 파일의 섹션 이름은 대괄호로 묶여 표시 됩니다. 일부 섹션은 인증서 확장을 구성 하는 데 사용 됩니다.

-   _Key_ – 항목의 이름이 며 등호의 왼쪽에 표시 됩니다.

-   _Value_ – 매개 변수 이며 등호 오른쪽에 나타납니다.

아래 예제에서 **[Version]** 은 섹션입니다. **Signature** 는 키이 고 **"\$windows NT @ no__t-4"** 는 값입니다.

예:

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>버전

파일을 .inf 파일로 식별 합니다. 버전은 필수 섹션 이며 Capolicy.inf 파일의 시작 부분에 있어야 합니다.

###  <a name="policystatementextension"></a>PolicyStatementExtension

조직에서 정의한 정책과 선택적 또는 필수 인지 여부를 나열 합니다. 여러 정책은 쉼표로 구분 됩니다. 이름은 특정 배포의 컨텍스트에서 의미가 있거나 이러한 정책의 존재 여부를 확인 하는 사용자 지정 응용 프로그램과 관련이 있습니다.

정의 된 각 정책에 대해 해당 특정 정책에 대 한 설정을 정의 하는 섹션이 있어야 합니다. 각 정책에 대해 사용자 정의 OID (개체 식별자) 및 정책 문으로 표시 하려는 텍스트 또는 정책 문에 대 한 URL 포인터를 제공 해야 합니다. URL은 HTTP, FTP 또는 LDAP URL 형식으로 지정할 수 있습니다.

정책 문에 설명 텍스트를 포함 하려는 경우 Capolicy.inf의 다음 세 줄은 다음과 같습니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

CA 정책 설명을 호스트 하는 데 URL을 사용 하는 경우 다음 세 줄은 다음과 같이 표시 됩니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
```

이 밖에도 다음 지침을 따릅니다.

-   여러 URL 및 알림 키가 지원 됩니다.

-   동일한 정책 섹션의 알림 및 URL 키가 지원 됩니다.

-   공백이 있는 Url 또는 공백이 있는 Url은 따옴표로 묶어야 합니다. 이는 URL 키가 표시 되는 섹션에 관계 없이 **URL** 키에 적용 됩니다.

정책 섹션에서 여러 알림 및 Url의 예는 다음과 같습니다.

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

Capolicy.inf에서 루트 CA 인증서에 대 한 Cdp (CRL 배포 지점의)를 지정할 수 있습니다.  CA를 설치한 후 CA에서 발급 된 각 인증서에 포함 하는 CDP Url을 구성할 수 있습니다. 루트 CA 인증서는 Capolicy.inf 파일의이 섹션에 지정 된 Url을 표시 합니다. 

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

이 섹션에 대 한 몇 가지 추가 정보:
-   지원함
    - HTTP 
    - 파일 Url
    - LDAP Url 
    - 여러 Url
   
    >[!IMPORTANT]
    >는 HTTPS Url을 지원 하지 않습니다.

-   따옴표는 Url을 공백으로 묶어야 합니다.

-   Url을 지정 하지 않으면 (즉, **[CRLDistributionPoint]** 섹션이 파일에 있지만 비어 있는 경우) 루트 CA 인증서에서 권한 정보 액세스 확장이 생략 됩니다. 이는 일반적으로 루트 CA를 설정할 때 좋습니다. Windows에서는 루트 CA 인증서에 대 한 해지 검사를 수행 하지 않으므로, CDP 확장은 루트 CA 인증서에 불필요 합니다.

-    예를 들어 CA는 클라이언트가 HTTP를 통해 검색 하는 웹 사이트의 폴더를 나타내는 공유에 파일 UNC에 게시할 수 있습니다.

-   루트 CA를 설정 하거나 루트 CA 인증서를 갱신 하는 경우에만이 섹션을 사용 합니다. CA는 하위 CA CDP 확장을 결정 합니다.
   

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

루트 CA 인증서에 대해 Capolicy.inf의 기관 정보 액세스 요소를 지정할 수 있습니다.

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

권한 정보 액세스 섹션에 대 한 몇 가지 추가 참고 사항:

-   여러 Url이 지원 됩니다.

-   HTTP, FTP, LDAP 및 파일 Url이 지원 됩니다. HTTPS Url은 지원 되지 않습니다.

-   이 섹션은 루트 CA를 설정 하거나 루트 CA 인증서를 갱신 하는 경우에만 사용 됩니다. 하위 ca AIA 확장은 하위 CA의 인증서를 발급 한 CA에 의해 결정 됩니다.

-   공백이 있는 Url은 따옴표로 묶어야 합니다.

-   Url이 지정 되지 않은 경우 즉, **[AuthorityInformationAccess]** 섹션이 파일에 있지만 비어 있는 경우 루트 CA 인증서에서 CRL 배포 지점 확장이 생략 됩니다. 이는 루트 ca 인증서에 대 한 링크에서 참조 해야 하는 루트 CA 보다 높은 권한이 없기 때문에 루트 CA 인증서의 경우이 설정이 기본 설정입니다.

### <a name="certsrv_server"></a>certsrv_Server

Capolicy.inf의 또 다른 선택적 섹션은 [certsrv_server]입니다 .이 섹션은 갱신 키 길이, 갱신 유효 기간 및 갱신 되거나 설치 되는 CA에 대 한 CRL (인증서 해지 목록) 유효 기간을 지정 하는 데 사용 됩니다. 이 섹션에는 어떤 키도 필요 하지 않습니다. 이러한 설정 중 상당수는 대부분의 요구에 충분 한 기본값을 가지 며, Capolicy.inf 파일 에서만 생략 하면 됩니다. 또는 CA가 설치 된 후 이러한 설정 중 대부분을 변경할 수 있습니다.

예를 들면 다음과 같습니다.

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

**RenewalKeyLength** 는 갱신에 대해서만 키 크기를 설정 합니다. CA 인증서를 갱신 하는 동안 새 키 쌍이 생성 되는 경우에만 사용 됩니다. 초기 CA 인증서의 키 크기는 CA가 설치 될 때 설정 됩니다.

새 키 쌍을 사용 하 여 CA 인증서를 갱신 하는 경우 키 길이를 늘리거나 줄일 수 있습니다. 예를 들어 루트 CA 키 크기를 4096 바이트 이상으로 설정한 후에는 2048 바이트의 키 크기만 지원할 수 있는 Java 앱 또는 네트워크 장치가 있음을 알 수 있습니다. 크기를 늘리거나 줄일 경우 해당 CA에서 발급 한 모든 인증서를 다시 발급 해야 합니다.

**RenewalValidityPeriod** 및 **RenewalValidityPeriodUnits** 는 이전 루트 ca 인증서를 갱신할 때 새 루트 ca 인증서의 수명을 설정 합니다. 루트 CA에만 적용 됩니다. 하위 CA의 인증서 수명은 상위 CA의 용도에 따라 결정 됩니다. RenewalValidityPeriod에는 다음 값을 사용할 수 있습니다. 시간, 일, 주, 월, 년

**CRLPeriod** 및 **CRLPERIODUNITS** 는 기본 CRL의 유효 기간을 설정 합니다. **CRLPeriod** 에는 다음 값을 사용할 수 있습니다. 시간, 일, 주, 월, 년

**CRLDeltaPeriod** 및 **CRLDELTAPERIODUNITS** 는 델타 CRL의 유효 기간을 설정 합니다. **CRLDeltaPeriod** 에는 다음 값을 사용할 수 있습니다. 시간, 일, 주, 월, 년

이러한 각 설정은 CA가 설치 된 후에 구성할 수 있습니다.

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

변경 내용을 적용 하려면 Active Directory 인증서 서비스를 다시 시작 해야 합니다.

**Loaddefaulttemplates** 는 엔터프라이즈 CA를 설치 하는 동안에만 적용 됩니다. 이 설정은 True 또는 False (또는 1 또는 0)로, CA가 기본 템플릿 중 하나를 사용 하 여 구성 되었는지 여부를 나타냅니다.

기본 CA 설치에서 기본 인증서 템플릿의 하위 집합이 인증 기관 스냅인의 인증서 템플릿 폴더에 추가 됩니다. 즉, 역할이 설치 된 후 AD CS 서비스가 시작 되는 즉시, 충분 한 권한이 있는 사용자 또는 컴퓨터에서 즉시 인증서를 등록할 수 있습니다.

CA가 설치 된 후 즉시 인증서를 발급 하지 않을 수 있으므로 LoadDefaultTemplates 설정을 사용 하 여 기본 템플릿이 엔터프라이즈 CA에 추가 되지 않도록 할 수 있습니다. CA에 구성 된 템플릿이 없는 경우 인증서를 발급할 수 있습니다.

**AlternateSignatureAlgorithm** ca 인증서 및 인증서 요청 모두에\#대해 PKCS 1 v 2.1 서명 형식을 지원 하도록 ca를 구성 합니다. 루트 CA에서 1로 설정 된 경우 CA 인증서에 PKCS\#1 v 2.1 서명 형식이 포함 됩니다. 하위 CA에 설정 된 경우 하위 CA는 PKCS\#1 v 2.1 서명 형식을 포함 하는 인증서 요청을 만듭니다.

**ForceUTF8** 는 Subject 및 Issuer 고유 이름에 있는 RDNs (상대 고유 이름)의 기본 인코딩을 u t f-8로 변경 합니다. RFC에 의해 디렉터리 문자열 형식으로 정의 된 것과 같이 u t f-8을 지 원하는 RDNs 영향을 받습니다. 예를 들어 DC (도메인 구성 요소)에 대 한 RDN은 인코딩을 IA5 또는 u t f-8로 지원 하는 반면, Country RDN (C)은 인쇄 가능한 문자열로의 인코딩만 지원 합니다. 따라서 ForceUTF8 지시문은 DC RDN에 영향을 주지만 C RDN에는 영향을 주지 않습니다.

**Enablekeycounting** 은 ca의 서명 키를 사용할 때마다 카운터를 증가 시 키는 ca를 구성 합니다. 키 계산을 지 원하는 HSM (하드웨어 보안 모듈) 및 연결 된 CSP (암호화 서비스 공급자)가 없는 경우에는이 설정을 사용 하지 마십시오. Microsoft 강력한 CSP 나 Microsoft 소프트웨어 KSP (키 저장소 공급자)는 키 계산을 지원 하지 않습니다.


## <a name="create-the-capolicyinf-file"></a>Capolicy.inf 파일 만들기

AD CS를 설치 하기 전에 구성한 CAPolicy.inf 파일 특정 설정을 사용 하 여 배포 합니다.

**인지** 관리자 그룹의 멤버 여야 합니다.

1. AD CS를 설치 하려는 컴퓨터에서 Windows PowerShell을 열고 **notepad c:\CAPolicy.inf** 를 입력 한 다음 enter 키를 누릅니다.

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
4. **파일**을 클릭 한 다음 다른 **이름으로 저장**을 클릭 합니다.

5. % Systemroot% 폴더로 이동 합니다.

6. 다음을 확인합니다.

   -   **파일 이름**이 **CAPolicy.inf**로 설정됨

   -   **파일 형식**이 **모든 파일**로 설정됨

   -   **인코딩**이 **ANSI**임

7. **저장**을 클릭합니다.

8. 파일을 덮어쓸지 묻는 메시지가 나타나면 **예**를 클릭합니다.

   ![Capolicy.inf 파일의 위치를 저장 합니다.](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

   > [!CAUTION]
   >   CAPolicy.inf를 inf 확장명으로 저장하도록 합니다. 파일 이름 끝에 **.inf**를 특별히 입력하지 않고 설명된 대로 옵션을 선택하지 않는다면 파일이 텍스트 파일로 저장되고 CA 설치 중에 사용되지 않습니다.

9. 메모장을 닫습니다.

> [!IMPORTANT]
>   Capolicy.inf에서 URL https://pki.corp.contoso.com/pki/cps.txt 을 지정 하는 줄이 표시 되는 것을 볼 수 있습니다. CAPolicy.inf의 내부 정책 섹션은 CPS(인증서 사용 약관)의 위치를 지정하는 방법을 보여주는 예시로 제공되었습니다. 이 가이드에서는 CPS (certificate statement)를 만들도록 지시 하지 않습니다.
