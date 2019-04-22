---
title: certreq
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a04e51f-f395-4bff-b57a-0e9efcadf973
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e48682cee40c00e187ca674bd8019b136a2c3f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818144"
---
# <a name="certreq"></a>certreq



상호 인증 또는 정규 하위 요청에 서명 하 고 새 요청을 수락 하 여 상호 인증 또는 정규화 된 종속 요청을 생성 하는 요청에 대 한 응답을 설치 하는.inf 파일 중에서 만들려는 CA에서 이전 요청에 대 한 응답을 검색 하는 인증 기관 (CA)에서 인증서 요청, 또는 기존 CA 인증서를 요청 하려면 Certreq는 사용할 수 있습니다.

> [!WARNING]
> - 이전 버전의 certreq이이 문서에서 설명 하는 옵션을 모두를 제공할 수 있습니다. 구문 표기법 섹션에 표시 된 명령을 실행 하 여 특정 버전의 certreq 제공 하는 모든 옵션을 볼 수 있습니다.
> - Certreq는 CEP/CES 환경에서 키 증명 템플릿을 기반으로 새 인증서 요청을 만들 수 없습니다.

## <a name="BKMK_Contents"></a>콘텐츠

이 문서의 주요 섹션은 다음과 같습니다.
1.  [동사](#BKMK_Verbs)
2.  [구문 표기법](#BKMK_notation)
3.  [Options](#BKMK_Options)
4.  [형식](#BKMK_Formats)
5.  [추가 certreq 예제](#BKMK_Examples)

## <a name="BKMK_Verbs"></a>동사

다음 테이블 certreq 명령을 사용 하 여 사용할 수 있는 동사에 설명 있습니다.

|스위치|설명|
|------|-----------|
|-제출|CA에 요청을 제출 합니다. 자세한 내용은 참조 [Certreq-제출](#BKMK_Submit)합니다.|
|-검색 *요청 Id*|CA에서 이전 요청에 대 한 응답을 검색합니다. 자세한 내용은 참조 [Certreq-검색](#BKMK_Retrieve)합니다.|
|새 버전|.Inf 파일에서 새 요청을 만듭니다. 자세한 내용은 참조 [Certreq-새](#BKMK_New)합니다.|
|허용|수신 하 고 인증서 요청에 대 한 응답을 설치 합니다. 자세한 내용은 참조 [Certreq-허용](#BKMK_accept)합니다.|
|정책|요청에 대 한 정책을 설정합니다. 자세한 내용은 참조 [Certreq-정책](#BKMK_policy)합니다.|
|) 기호 +|상호 인증 또는 정규화 된 종속 요청을 서명합니다. 자세한 내용은 참조 [Certreq-기호](#BKMK_sign)합니다.|
|-등록|에 대 한 등록 하거나, 인증서를 갱신 합니다. 자세한 내용은 참조 [Certreq-등록](#BKMK_enroll)합니다.|
|-?|Certreq 구문, 옵션 및 설명의 목록을 표시합니다.|
|*\<verb>* -?|지정 된 동사에 대 한 도움말을 표시 합니다.|
|-v -?|Certreq 구문, 옵션 및 설명의 자세한 목록이 표시 됩니다.|

으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_notation"></a>구문 표기법

-   기본 명령줄 구문에 대 한 실행 `certreq -?`
-   Certutil을 사용 하 여 특정 동사와 구문에 대 한 실행 **certreq**  *\<동사 >* **-?**
-   모든 certutil 구문을 텍스트 파일로 보내려면 다음 명령을 실행 합니다.  
    -   `certreq -v -? > certreqhelp.txt`
    -   `notepad certreqhelp.txt`

다음 표에서 명령줄 구문을 나타내는 데 사용 되는 표기법을 설명 합니다.

|Notation|설명|
|--------|-----------|
|대괄호 또는 중괄호 사용 하지 않고 텍스트|표시 된 대로 입력 해야 하는 항목|
|\<꺾쇠 괄호 안의 텍스트 >|자리 표시자 값을 제공 해야|
|[대괄호 안의 텍스트]|선택적 항목입니다.|
|{중괄호 안에 text}|필요한 항목에 대 한 설정 하나를 선택합니다|
|세로 막대 (&#124;)|상호 배타적인 항목에 대 한 구분 기호 하나를 선택합니다|
|줄임표 (...)|반복 될 수 있는 항목|

으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_Submit"></a>Certreq -submit

Certreq.exe 명령줄 프롬프트에서 옵션이 표시 되지 않는 명시적으로 지정 하는 경우 기본 certreq.exe 매개 변수를 이것이 CA에 인증서 요청 제출 하려고 합니다.
```
CertReq [-Submit] [Options] [RequestFileIn [CertFileOut [CertChainFileOut [FullResponseFileOut]]]]
```
사용 하는 경우에 인증서 요청 파일을 지정 해야 – 옵션을 제출 합니다. 이 매개 변수를 생략 하면 적절 한 인증서 요청 파일을 선택할 수 있는 공통 파일 열기 창을 표시 됩니다.

인증서 전송 요청을 작성 하는 시작 점으로 이러한 예제를 사용할 수 있습니다.

간단한 인증서 요청을 제출 하려면 아래 예제에서는 사용 합니다.
```
certreq –submit certRequest.req certnew.cer certnew.pfx
```
SAN 특성을 지정 하 여 인증서를 요청 하려면 Microsoft 기술 자료 문서 931351의 자세한 단계를 참조 하십시오. [보안 LDAP 인증서에 주체 대체 이름을 추가 하는 방법을](https://support.microsoft.com/kb/931351) "Certreq.exe 유틸리티를 사용 하 여 작성 하 고 SAN을 포함 하는 인증서 요청을 전송 하는 방법" 섹션에 있습니다.

으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_Retrieve"></a>Certreq -retrieve

```
certreq -retrieve [Options] RequestId [CertFileOut [CertChainFileOut [FullResponseFileOut]]]
```
-   -Config CAComputerName\CANamea 대화 상자에서 CAComputerName 또는 CAName를 지정 하지 않으면 나타나고 사용할 수 있는 모든 Ca 목록이 표시 됩니다.
-   -config CAComputerName\CAName 대신 -config -를 사용하면 기본 CA를 사용하여 작업이 처리됩니다.
-   Certreq를 사용할 수 있습니다-검색 *RequestID* CA가 발급 실제로 후 인증서를 검색 합니다. *RequestID*PKC 10 진수 수 또는 16 진수 접두사 x는 0으로는 0 x 접두사가 없는 인증서 일련 번호 될 수 있습니다. 적이 있는지 여부는 인증서 요청 된 적 있음은 대기 상태에 관계 없이 해지 또는 만료 된 인증서를 포함 하는 CA에서 발급 된 모든 인증서를 검색 하려면 사용할 수 있습니다.
-   CA의 정책 모듈에서 요청 보류 중 상태 및 반환에 남았을 수는 CA에 요청을 제출 하는 경우는 *RequestID* 표시할 Certreq 호출자에 게 있습니다. 결국은 CA 관리자가 인증서를 발급 되거나 요청을 거부 됩니다.

아래 명령을 20 인증서 id를 검색 하 고 인증서 파일 (.cer)를 만듭니다.
```
certreq -retrieve 20 MyCertificate.cer 

```
으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_New"></a>Certreq -new

```
certreq -new [Options] [PolicyFileIn [RequestFileOut]]
```
INF 파일에 대 한 다양 한 매개 변수 및 옵션을 지정할 수 있으므로, 관리자는 어떤 용도로 사용 해야 하는 기본 템플릿을 정의 하기가 어렵습니다. 따라서이 섹션에서는 특정 요구 사항에 맞는 INF 파일을 만들 수 있도록 하는 모든 옵션을 설명 합니다. 다음 키워드는 INF 파일 구조를 설명 하는 데 사용 됩니다.
1.  A *섹션* 키의 논리적 그룹을 포함 하는 INF 파일에는 영역입니다. 섹션은 항상 INF 파일에서 대괄호 안에 표시 됩니다.
2.  A *키* 등호의 왼쪽에 있는 매개 변수입니다.
3.  A *값* 등호의 오른쪽에 있는 매개 변수입니다.

예를 들어 최소 INF 파일은 다음과 같습니다.
```
[NewRequest] 
; At least one value must be set in this section 
Subject = "CN=W2K8-BO-DC.contoso2.com"
```
다음은 일부 가능한 섹션 INF 파일에 추가할 수 있습니다.

**[NewRequest]**

이 섹션은 새 인증서 요청에 대 한 템플릿으로 사용 되는 INF 파일에 대 한 필수입니다. 이 섹션에는 적어도 하나의 키 값이 필요합니다.

|Key|정의|값|예제|
|---|----------|-----|-------|
|Subject|여러 응용 프로그램 인증서의 주체 정보 사용. 따라서이 키에 대 한 값을 지정 하는 것이 좋습니다. 주체 여기 설정 되지 않은 경우 주체 이름이 주체 대체 이름 인증서 확장의 일부로 포함 되도록 하는 것이 좋습니다.|상대 고유 이름 문자열 값|Subject = "CN=computer1.contoso.com" Subject = "CN = John Smith, CN = Users, DC = Contoso, DC = com"|
|Exportable|이 특성을 TRUE로 설정 하는 경우 인증서와 개인 키를 내보낼 수 있습니다. 높은 수준의 보안을 보장 하려면 개인 키 안 내보낼 수 있습니다. 그러나 경우에 따라 그 필요할 수 개인 키를 여러 컴퓨터 또는 사용자가 동일한 개인 키를 공유 해야 하는 경우에 내보낼 수 있도록 합니다.|true, false|내보낼 수 = TRUE입니다. CNG 키를이 구별할 수 및 일반 텍스트를 내보낼 수 있습니다. CAPI1 키 수는 없습니다.|
|ExportableEncrypted|개인 키를 내보낼 수로 설정 해야 하는지 여부를 지정 합니다.|true, false|ExportableEncrypted = true</br>팁:  일부 공개 키 크기와 알고리즘 모든 해시 알고리즘을 사용 하 여 작동 합니다. Tamehe 지정 CSP도 지정된 된 해시 알고리즘을 지원 해야 합니다. 지원 되는 해시 알고리즘의 목록을 보려면 명령을 실행할 수 있습니다. <code>certutil -oid 1 &#124; findstr pwszCNGAlgid &#124; findstr /v CryptOIDInfo</code>|
|HashAlgorithm|이 요청에 사용할 해시 알고리즘입니다.|Sha256, sha384, sha512, sha1, md5, md4, md2|HashAlgorithm = s h a 1입니다. 사용 하 여 지원 되는 해시 알고리즘의 목록을 보려면: certutil oid 1 &#124; findstr pwszCNGAlgid &#124; findstr /v CryptOIDInfo|
|KeyAlgorithm|공용 및 개인 키 쌍을 생성 하려면 서비스 공급자가 사용할 수 있는 알고리즘입니다.|RSA, DH, DSA, ECDH_P256, ECDH_P521, ECDSA_P256, ECDSA_P384, ECDSA_P521|KeyAlgorithm = RSA|
|KeyContainer|하지 않는 새 키 자료를 생성 된 경우 새 요청에 대해이 매개 변수를 설정 하는 것이 좋습니다. 키 컨테이너는 자동으로 생성 하 고 시스템에 의해 유지. 여기서는 기존 키 자료를 사용 해야 하는 요청에 대 한 기존 키의 키 컨테이너 이름으로이 값을 설정할 수 있습니다. certutil을 사용 하 여 – 컴퓨터 컨텍스트에 대 한 사용 가능한 키 컨테이너 목록을 표시 하는 명령 키입니다. certutil을 사용 하 여 – 키 – 현재 사용자의 컨텍스트에 대 한 사용자 명령입니다.|임의의 문자열 값</br>팁:  에 공백 또는 특수 문자를 잠재적인 INF 구문 분석 문제를 방지 하는 모든 INF 키 값 앞뒤에 큰따옴표를 사용 해야 합니다.|KeyContainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}|
|키 길이|공용 및 개인 키의 길이 정의합니다. 키 길이 인증서의 보안 수준에 영향이 있습니다. 더 긴 키 길이는 일반적으로 더 높은 보안 수준; 제공 그러나 일부 응용 프로그램 키 길이 관련 된 제한이 있을 수 있습니다.|암호화 서비스 공급자에서 지 원하는 모든 유효한 키 길이입니다.|키 길이 = 2048|
|KeySpec|키 서명, Exchange (암호화), 또는 둘 다에 사용 될 수 하는 경우를 결정 합니다.|AT_NONE, AT_SIGNATURE, AT_KEYEXCHANGE|KeySpec AT_KEYEXCHANGE =|
|KeyUsage|어떤 인증서 키에 사용할지를 정의 합니다.|CERT_DIGITAL_SIGNATURE_KEY_USAGE-80 (128)</br>팁:  표시 된 값은 각 비트 정의 대 한 16 진수 (10 진수) 값입니다. 오래 된 구문을 사용할 수도 있습니다: 여러 개의 단일 16 진수 값을 비트 기호 표현 하는 대신 집합입니다. 예를 들어 KeyUsage 0xa0 =.</br>CERT_NON_REPUDIATION_KEY_USAGE-40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE-20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE-10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE-8</br>CERT_KEY_CERT_SIGN_KEY_USAGE-4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE-2</br>CERT_CRL_SIGN_KEY_USAGE-2</br>CERT_ENCIPHER_ONLY_KEY_USAGE-1</br>CERT_DECIPHER_ONLY_KEY_USAGE-8000 (32768)|KeyUsage = "CERT_DIGITAL_SIGNATURE_KEY_USAGE &#124; CERT_KEY_ENCIPHERMENT_KEY_USAGE"</br>팁:  파이프를 사용 하는 여러 값 (&#124;) 구분 기호입니다. INF 구문 분석 문제를 방지 하려면 여러 값을 사용 하는 경우 큰따옴표를 사용 하는 것을 확인 합니다.|
|KeyUsageProperty|개인 키를 사용할 수 있는 특정 용도 식별 하는 값을 검색 합니다.|NCRYPT_ALLOW_DECRYPT_FLAG-1</br>NCRYPT_ALLOW_SIGNING_FLAG-2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG-4</br>NCRYPT_ALLOW_ALL_USAGES-ffffff (16777215)|KeyUsageProperty = "NCRYPT_ALLOW_DECRYPT_FLAG 및 #124; NCRYPT_ALLOW_SIGNING_FLAG "|
|MachineKeySet|이 키는 컴퓨터와 사용자가 아닌 소유 하는 인증서를 만들어야 할 때 중요 합니다. 생성 되는 키 자료의 보안 컨텍스트 보안 주체 (사용자 또는 컴퓨터 계정)가 만든 요청에에서 유지 됩니다. 관리자가 컴퓨터를 대신 하 여 인증서 요청을 만들면 키 자료에 관리자의 보안 컨텍스트가 아닌 컴퓨터의 보안 컨텍스트를 만들어야 합니다. 그렇지 않으면 시스템 관리자의 보안 컨텍스트에서 것은 해당 개인 키를 액세스 하지 못했습니다.|true, false|MachineKeySet = true</br>팁:  기본값은 false입니다.|
|NotBefore|날짜 또는 날짜 및 되기까지의 요청을 실행할 수 없습니다 시간을 지정 합니다. NotBefore는 ValidityPeriod 유닛의와 사용할 수 있습니다.|날짜 또는 날짜 및 시간|NotBefore = "7/24/2012 10:31 AM"</br>팁:  NotBefore 및 NotAfter는 RequestType = 인증서만 합니다. 날짜 구문 분석은 로캘 구분 하려고 합니다. 명확 하 게 됩니다 이름과 모든 로캘에서 작동 해야 하는 월을 사용 합니다.|
|NotAfter|날짜 또는 날짜 및 시간을 요청을 실행할 수 없습니다 지정 합니다. ValidityPeriod 또는 유닛의 NotAfter는 사용할 수 없습니다.|날짜 또는 날짜 및 시간|NotAfter = "2014 년 9 월 23 일 오전 10 시 31"</br>팁:  NotBefore 및 NotAfter는 RequestType = 인증서만 합니다. 날짜 구문 분석은 로캘 구분 하려고 합니다. 명확 하 게 됩니다 이름과 모든 로캘에서 작동 해야 하는 월을 사용 합니다.|
|PrivateKeyArchive|PrivateKeyArchive 설정 키 보관에 대 한 CA를 요청자의 개인 키를 안전 하 게 전송 하는 것에 대 한 요청 형식 CMS (CMC)을 통해 인증서 관리 메시지만 허용 하기 때문에 해당 RequestType "CMC"로 설정 되어 있는 경우에 작동 합니다.|true, false|PrivateKeyArchive = True|
|EncryptionAlgorithm|사용할 암호화 알고리즘입니다.|가능한 옵션에서 운영 체제 버전 및 설치 된 암호화 공급자의 집합에 따라 달라 집니다. 사용 가능한 알고리즘의 목록을 보려면 명령을 <code>certutil -oid 2 &#124; findstr pwszCNGAlgid</code> 지정 된 대칭 암호화 알고리즘 및 길이도 사용 되는 지정 된 CSP 지원 해야 합니다.|EncryptionAlgorithm 3des =|
|EncryptionLength|사용할 암호화 알고리즘의 길이입니다.|지정한 EncryptionAlgorithm에서 허용 된 길이입니다.|EncryptionLength = 128|
|ProviderName|공급자 이름은 CSP의 표시 이름입니다.|사용 하는 CSP의 공급자 이름을 모르는 경우 certutil-csplist 명령줄에서 실행 합니다. 이 명령은 로컬 시스템에서 사용할 수 있는 모든 Csp의 이름이 표시 됩니다.|공급자 이름이 "Microsoft RSA SChannel Cryptographic Provider" =|
|ProviderType|공급자 유형 "RSA 전체"와 같은 특정 알고리즘 기능에 따라 특정 공급자를 선택 하는 데 사용 됩니다.|사용 하는 CSP의 공급자 형식을 모르는 경우 certutil-csplist 명령줄 프롬프트에서 실행 합니다. 이 명령은 로컬 시스템에서 사용할 수 있는 모든 Csp의 공급자 형식을 표시 됩니다.|ProviderType = 1|
|RenewalCert|인증서 요청 생성 된 경우 시스템에 존재 하는 인증서를 갱신 해야 하는 경우에이 키에 대 한 값으로 인증서 해시를 지정 해야 합니다.|인증서 요청을 만들 되는 컴퓨터에서 사용할 수 있는 모든 인증서의 인증서 해시입니다. 인증서 해시를 알 수 없는 경우에 인증서 MMC 스냅인을 사용 하 여을 갱신 해야 하는 인증서를 살펴봅니다. 인증서 속성을 열고 인증서의 "지문" 특성을 확인 합니다. 인증서 갱신에는 PKCS #7 또는 CMC 요청 형식이 필요합니다.|RenewalCert 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D =|
|RequesterName</br>참고: 이렇게 하면 다른 사용자 요청 대신 하 여 등록 요청 합니다. 요청도 등록 에이전트 인증서를 사용 하 여 서명 해야 하거나 CA에서 요청을 거부 합니다. 사용 하 여 등록 에이전트 인증서를 지정 하려면-cert 옵션입니다.|요청자 이름에서 RequestType CMC 또는 PKCS # 7로 설정 된 경우 인증서 요청에 대해 지정할 수 있습니다. 이 키에서 RequestType을 PKCS # 10으로 설정 하는 경우 무시 됩니다. Requestername 요청의 일부로 설정할 수 있습니다. 보류 중인 요청에 Requestername 조작할 수 없습니다.|도메인 \ 사용자|Requestername = "Contoso\BSmith"|
|RequestType|생성 하 고 인증서 요청을 전송 하는 데 사용 되는 표준에 따라 결정 됩니다.|PKCS10-1</br>PKCS7-2</br>CMC-3</br>인증서-4</br>SCEP -- fd00 (64768)</br>팁:  이 옵션에는 자체 서명 또는 자체 발급 된 인증서를 나타냅니다. 요청 하지만 대신 새 인증서를 생성 하지 않습니다 하 고 인증서를 설치 합니다. 자체 서명 된 기본값이입니다. 서명 인증서를 사용 하 여 지정-cert 옵션 없는 자체 서명 된 자체 발급 된 인증서를 만듭니다.|RequestType = CMC|
|SecurityDescriptor</br>팁:  이 기능은 시스템 컨텍스트가 아닌 스마트 카드 키에만 적합 합니다.|보안 개체와 관련 된 보안 정보를 포함 합니다. 가장 보안 개체에 대 한 개체를 만드는 함수 호출에는 개체의 보안 설명자를 지정할 수 있습니다.|문자열 기반 [보안 설명자 정의 언어](https://msdn.microsoft.com/library/aa379567(v=vs.85).aspx)합니다.|SecurityDescriptor "D:P(A;; = GA;; SY) (A; GA;; BA) "|
|AlternateSignatureAlgorithm|지정 하 고 불연속 또는 조합 된 PKCS #10 요청 또는 인증서 서명에 대 한 서명 알고리즘 개체 식별자 (OID) 인지 여부를 나타내는 부울 값을 검색 합니다.|true, false|AlternateSignatureAlgorithm = false</br>팁:  False는 RSA 서명에 대 한 한 Pkcs1 v 1.5를 나타냅니다. True 이면 v2.1 시그니처를 나타냅니다.|
|자동|기본적으로이 옵션에는 사용자에 게 서 스마트 카드 PIN와 같은 대화형 사용자 데스크톱 및 요청 정보를 CSP 액세스할을 수 있습니다. 이 키가 TRUE로 설정, CSP 데스크톱과 상호 작용 해서는 안 하 고 사용자에 게 모든 사용자 인터페이스를 표시 차단 됩니다.|true, false|자동 = true|
|SMIME|이 매개 변수는 TRUE로 설정 하는 경우 개체 식별자 값 1.2.840.113549.1.9.15 확장이 요청에 추가 됩니다. 개체 식별자의 수에 따라 다릅니다은 Outlook 같은 Secure Multipurpose Internet Mail Extensions (S/MIME) 응용 프로그램에서 사용할 수 있는 대칭 암호화 알고리즘에 대 한 참조는 설치 된 운영 체제 버전 및 CSP 기능에 있습니다.|true, false|SMIME = true|
|UseExistingKeySet|이 매개 변수를 사용 하 여 인증서 요청을 만드는 기존 키 쌍을 사용 해야 함을 지정 합니다. 이 키가 TRUE로 설정 하는 경우 RenewalCert 키 또는 KeyContainer 이름에 대 한 값도 지정 해야 합니다. 기존 키의 속성을 변경할 수 없으므로 하지 내보낼 수 있는 키를 설정 해야 합니다. 이 경우 키 자료가 인증서 요청을 빌드할 때 생성 됩니다.|true, false|UseExistingKeySet = true|
|KeyProtection|사용 하기 전에 개인 키를 보호 하는 방법을 나타내는 값을 지정 합니다.|XCN_NCRYPT_UI_NO_PROTCTION_FLAG-0</br>XCN_NCRYPT_UI_PROTECT_KEY_FLAG-1</br>XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG-2|KeyProtection NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG =|
|SuppressDefaults|기본 확장 프로그램 및 특성 요청에 포함 되는지 여부를 나타내는 부울 값을 지정 합니다. 기본값은 해당 Oid (개체 식별자)으로 표현 됩니다.|true, false|SuppressDefaults = true|
|FriendlyName|새 인증서 이름입니다.|텍스트 모드|FriendlyName = "Server1"|
|ValidityPeriodUnits</br>참고: 이 사용 됩니다 요청 형식 때 cert =.|ValidityPeriod 함께 사용 되는 단위 수를 지정 합니다.|숫자|유닛의 = 3|
|ValidityPeriod</br>참고: 이 사용 됩니다 요청 형식 때 cert =.|VValidityPeriod 기간은 영어 (미국) 복수 이어야 합니다.|년, 월, 주, 일, 시간, 분, 초|ValidityPeriod = 년|

으로 돌아가서 [내용](#BKMK_Contents)

**[Extensions]**

이 섹션은 선택 사항입니다.

|OID 확장|정의|값|예제|
|-------------|----------|-----|-------|
|2.5.29.17|||2.5.29.17 = "{text}"|
|_continue_|||_continue_ = "UPN=User@Domain.com&"|
|_continue_|||_계속 진행_ = "전자 메일 =User@Domain.com&"|
|_continue_|||_continue_ = "DNS=host.domain.com&"|
|_continue_|||_continue_ = "DirectoryName=CN=Name,DC=Domain,DC=com&"|
|_continue_|||_continue_ = "URL=http://host.domain.com/default.html&"|
|_continue_|||_continue_ = "IPAddress=10.0.0.1&"|
|_continue_|||_continue_ = "RegisteredId=1.2.3.4.5&"|
|_continue_|||_continue_ = "1.2.3.4.6.1={utf8}String&"|
|_continue_|||_continue_ = "1.2.3.4.6.2={octet}AAECAwQFBgc=&"|
|_continue_|||_continue_ = "1.2.3.4.6.2={octet}{hex}00 01 02 03 04 05 06 07&"|
|_continue_|||_continue_ = "1.2.3.4.6.3={asn}BAgAAQIDBAUGBw==&"|
|_continue_|||_continue_ = "1.2.3.4.6.3={hex}04 08 00 01 02 03 04 05 06 07"|
|2.5.29.37|||2.5.29.37="{text}"|
|_continue_|||_continue_ = "1.3.6.1.5.5.7.|
|_continue_|||_continue_ = "1.3.6.1.5.5.7.3.1"|
|2.5.29.19|||"{text} ca 0pathlength = 3 ="|
|심각|||중요 한 2.5.29.19 =|
|KeySpec|||AT_NONE-0</br>AT_SIGNATURE-2</br>AT_KEYEXCHANGE-1|
|RequestType|||PKCS10-1</br>PKCS7-2</br>CMC-3</br>인증서-4</br>SCEP -- fd00 (64768)|
|KeyUsage|||CERT_DIGITAL_SIGNATURE_KEY_USAGE-80 (128)</br>CERT_NON_REPUDIATION_KEY_USAGE-40 (64)</br>CERT_KEY_ENCIPHERMENT_KEY_USAGE-20 (32)</br>CERT_DATA_ENCIPHERMENT_KEY_USAGE-10 (16)</br>CERT_KEY_AGREEMENT_KEY_USAGE-8</br>CERT_KEY_CERT_SIGN_KEY_USAGE-4</br>CERT_OFFLINE_CRL_SIGN_KEY_USAGE-2</br>CERT_CRL_SIGN_KEY_USAGE-2</br>CERT_ENCIPHER_ONLY_KEY_USAGE-1</br>CERT_DECIPHER_ONLY_KEY_USAGE-8000 (32768)|
|KeyUsageProperty|||NCRYPT_ALLOW_DECRYPT_FLAG-1</br>NCRYPT_ALLOW_SIGNING_FLAG-2</br>NCRYPT_ALLOW_KEY_AGREEMENT_FLAG-4</br>NCRYPT_ALLOW_ALL_USAGES-ffffff (16777215)|
|KeyProtection|||NCRYPT_UI_NO_PROTECTION_FLAG-0</br>NCRYPT_UI_PROTECT_KEY_FLAG-1</br>NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG-2|
|SubjectNameFlags|템플릿||CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME-40000000 (1073741824)</br>CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH-80000000 (2147483648)</br>CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN-10000000 (268435456)</br>CT_FLAG_SUBJECT_REQUIRE_EMAIL-20000000 (536870912)</br>CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME-8</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID-1000000 (16777216)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DNS-8000000 (134217728)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS-400000 (4194304)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL-4000000 (67108864)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_SPN-800000 (8388608)</br>CT_FLAG_SUBJECT_ALT_REQUIRE_UPN-2000000 (33554432)|
|X500NameFlags|||CERT_NAME_STR_NONE-0</br>CERT_OID_NAME_STR-2</br>CERT_X500_NAME_STR-3</br>CERT_NAME_STR_SEMICOLON_FLAG-40000000 (1073741824)</br>CERT_NAME_STR_NO_PLUS_FLAG-20000000 (536870912)</br>CERT_NAME_STR_NO_QUOTING_FLAG-10000000 (268435456)</br>CERT_NAME_STR_CRLF_FLAG-8000000 (134217728)</br>CERT_NAME_STR_COMMA_FLAG-4000000 (67108864)</br>CERT_NAME_STR_REVERSE_FLAG-2000000 (33554432)</br>CERT_NAME_STR_FORWARD_FLAG-1000000 (16777216)</br>CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG-10000 (65536)</br>CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG-20000 (131072)</br>CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG-40000 (262144)</br>CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG-80000 (524288)</br>CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG-100000 (1048576)</br>CERT_NAME_STR_ENABLE_PUNYCODE_FLAG-200000 (2097152)|

으로 돌아가서 [내용](#BKMK_Contents)

> [!NOTE]
> SubjectNameFlags 지정 하는 제목 및 SubjectAltName 확장 필드 certreq 현재 사용자 또는 현재 컴퓨터 속성을 기반으로 자동으로 채워진 INF 파일을 허용 합니다. DNS 이름, UPN 및 등입니다. 리터럴 "템플릿"을 사용 하 여 템플릿 이름 플래그 대신 사용 됩니다 하는 것을 의미 합니다. 따라서 단일 INF 파일을 상황에 맞는 주체 정보를 사용 하 여 요청을 생성 하는 여러 컨텍스트에서 사용할 수 있습니다.
>
> X500NameFlags는 ASN.1 주체 INF 키 값이 변환 될 때 CertStrToName API에 직접 전달 하는 플래그 인코딩된 고유 이름을 지정 합니다.

Certreq를 사용 하 여 기반 인증서를 요청 하려면-새로운 아래 예제에서 단계를 사용 합니다.

> [!WARNING]
> 이 항목의 콘텐츠는 Windows Server 2008 AD CS;에 대 한 기본 설정에 따라 예를 들어, 2048, CSP,으로 Microsoft 소프트웨어 키 저장소 공급자를 선택 하 고 Secure Hash Algorithm 1 (SHA1)를 사용 하 여 키 길이 설정 합니다. 회사의 보안 정책 요구 사항에 대해 이러한 선택 항목을 평가 합니다.

정책 파일 (.inf) 복사 하 고 아래 예제에서는 메모장에서 저장 하 고 RequestConfig.inf로 저장:
```
[NewRequest] 
Subject = "CN=<FQDN of computer you are creating the certificate>" 
Exportable = TRUE 
KeyLength = 2048 
KeySpec = 1 
KeyUsage = 0xf0 
MachineKeySet = TRUE 
[RequestAttributes]
CertificateTemplate="WebServer"
[Extensions] 
OID = 1.3.6.1.5.5.7.3.1 
OID = 1.3.6.1.5.5.7.3.2  

```
인증서를 요청 하는 컴퓨터에서 아래 명령을 입력 합니다.
```
CertReq –New RequestConfig.inf CertRequest.req 

```
다음 예제에서는 [Strings] 섹션 구문 Oid 및 데이터를 해석 하기 어려운 다른 구현 하는 방법을 보여 줍니다. Oid 쉼표로 구분 된 목록을 사용 하 여 EKU 확장을 위한 새로운 {text} 구문 예제:
```
[Version]
Signature="$Windows NT$

[Strings]
szOID_ENHANCED_KEY_USAGE = "2.5.29.37"
szOID_PKIX_KP_SERVER_AUTH = "1.3.6.1.5.5.7.3.1"
szOID_PKIX_KP_CLIENT_AUTH = "1.3.6.1.5.5.7.3.2"

[NewRequest]
Subject = "CN=TestSelfSignedCert"
Requesttype = Cert

[Extensions]
%szOID_ENHANCED_KEY_USAGE%="{text}%szOID_PKIX_KP_SERVER_AUTH%,"
_continue_ = "%szOID_PKIX_KP_CLIENT_AUTH%"
```
으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_accept"></a>Certreq -accept

```
CertReq -accept [Options] [CertChainFileIn | FullResponseFileIn | CertFileIn]
```
– 발급 된 인증서를 사용 하 여 이전에 생성 된 개인 키에 연결 하 고 (있는 경우 일치 하는 요청)의 인증서가 요청 하는 위치는 시스템에서 보류 중인 인증서 요청을 제거 하는 매개 변수를 수락 합니다.

수동으로 인증서를 수락 하는 것에 대 한이 예제를 사용할 수 있습니다.
```
certreq -accept certnew.cer 

```

> [!WARNING]
> -동사 수락,-사용자와 – 컴퓨터 옵션 사용자 또는 컴퓨터 컨텍스트의에 설치 하 고 인증서를 설치 해야 하는지 여부를 나타냅니다. 설치 하 고 공개 키와 일치 하는 두 컨텍스트에서 처리 중인 요청과 없는 경우 이러한 옵션이 필요 하지 않습니다. 처리 중인 요청이 없을 경우 다음 중 하나 지정 해야 합니다.

으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_policy"></a>Certreq -policy

```
certreq -policy [-attrib AttributeString] [-binary] [-cert CertID] [RequestFileIn [PolicyFileIn [RequestFileOut [PKCS10FileOut]]]]
```
-   정규 종속 정의 되었을 경우 CA 인증서에 적용 되는 제약 조건을 정의 하는 구성 파일에는 Policy.inf 라고 합니다.
-   Policy.inf 파일의 예를 찾을 수는 [부록 A의 계획 및 구현 상호 인증 및 정규 종속](https://technet.microsoft.com/library/cc738878(WS.10).aspx) 백서입니다.
-   certreq를 입력 하는 경우-정책 추가 매개 변수 없이 열립니다 대화 상자 창을 선택할 수 있도록는 요청 된 파일 (req, cmc, txt, der로, cer 또는 crt). 요청된 된 파일을 선택 하 고 열기 단추를 클릭 한 후에 INF 파일을 선택 하기 위해 다른 대화 상자 창이 열립니다.

이 예제에서는 빌드 상호 인증서 요청을 사용할 수 있습니다.
```
certreq -policy Certsrv.req Policy.inf newcertsrv.req 

```
으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_sign"></a>Certreq -sign

```
certreq -sign [Options] [RequestFileIn [RequestFileOut]]
```
-   certreq를 입력 하는 경우-기호 추가 매개 변수 없이 열립니다 대화 상자 창 (req, cmc, txt, der로, cer 또는 crt) 요청된 된 파일을 선택할 수 있도록 합니다.
-   정규 종속 요청을 서명 엔터프라이즈 관리자 자격 증명이 필요할 수 있습니다. 이것이 정규 종속에 대 한 서명 인증서를 발급 하는 것이 가장 좋습니다.
-   정규 종속 요청을 서명 하는 데 사용 하는 인증서가 정규 종속 템플릿을 사용 하 여 만들어집니다. Enterprise Admins 요청을 서명 하거나 인증서에 서명 하는 사용자에 대 한 사용자 권한을 부여 해야 합니다.
-   CMC 요청을 서명 하는 경우 정규 종속 연관 된 보증 수준에 따라이 요청을 서명 하는 여러 직원을 할 수 있습니다.
-   부모 CA를 설치 하는 정식된 하위 CA의 오프 라인 상태 이면 받아야 CA 인증서 정식된 하위 CA에 대 한 서버를 오프 라인 부모입니다. 부모 CA 온라인 상태인 경우는 인증서 서비스 설치 마법사 중 정식된 하위 CA에 대 한 CA 인증서를 지정 합니다.

다음 명령 시퀀스의 새 인증서 요청 만들기, 서명 및 앱을 제출 하는 방법을 표시 됩니다.
```
certreq -new policyfile.inf MyRequest.req
certreq -sign MyRequest.req MyRequest_Sign.req
certreq -submit MyRequest_Sign.req MyRequest_cert.cer 

```
으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_enroll"></a>Certreq -enroll

인증서를 등록 하려면
```
certreq –enroll [Options] TemplateName
```
기존 인증서를 갱신 하려면
```
certreq –enroll –cert CertId [Options] Renew [ReuseKeys]
```
만 있는 시간에 유효한 인증서를 갱신할 수 있습니다. 만료 된 인증서를 갱신할 수 없습니다.와 새 인증서로 교체 해야 합니다.

여기의 일련 번호를 사용 하는 인증서를 갱신 합니다. 예:
```
certreq –enroll -machine –cert "61 2d 3c fe 00 00 00 00 00 05" Renew
```
인증서 템플릿에 등록할 경우의 예를 통해 U/i: 정책 서버를 선택 하려면 별표 (*)를 사용 하 여 웹 서버 라는
```
certreq -enroll –machine –policyserver * "WebServer"
```
으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_Options"></a>옵션

|변수|설명|
|-------|-----------|
|-모든|Force ICertRequest::Submit 인코딩 유형을 확인할 수 있습니다.|
|-attrib \<AttributeString>|콜론으로 구분 된 이름 및 값 문자열 쌍을 지정 합니다.</br>\N (예를 들어 Name1:Value1\nName2:Value2) 별도 이름 및 값 문자열 쌍입니다.|
|-이진|형식 대신 base64 인코딩된 이진 파일을 출력합니다.|
|-PolicyServer *\<PolicyServer>*|"ldap: *\<path>*"</br>URI 또는 인증서 등록 정책 웹 서비스를 실행 하는 컴퓨터에 대 한 고유 ID를 삽입 합니다.</br>요청 파일을 이동 하 여 사용 하려는 것을 지정 하려면 삼아 빼기 (-) 기호가  *\<policyserver >* 합니다.|
|-config \<ConfigString>|CAHostName\CAName 구성 문자열에서 지정 된 CA를 사용 하 여 작업을 처리 합니다. Https 연결에 대 한 등록 서버 URI를 지정 합니다. 로컬 컴퓨터에 대 한 CA를 저장, 빼기를 사용 하 여 기호 (-).|
|아닌 익명이|인증서 등록 웹 서비스에 대 한 익명 자격 증명을 사용 합니다.|
|-Kerberos|인증서 등록 웹 서비스에 대 한 Kerberos (도메인) 자격 증명을 사용 합니다.|
|-ClientCertificate *\<ClientCertId>*|바꿀 수 있습니다 합니다  *\<ClientCertID >* 인증서 지문, CN, EKU, 템플릿, 전자 메일, UPN 및 새 이름을 사용 하 여 = 값 구문.|
|-UserName *\<UserName>*|인증서 등록 웹 서비스를 사용합니다. 대체할 수 있습니다  *\<사용자 이름 >* SAM 이름 또는 도메인 \ 사용자입니다. 이 옵션은-p 옵션으로 사용 합니다.|
|-p *\<Password>*|인증서 등록 웹 서비스를 사용합니다. 대체  *\<암호 >* 실제 사용자의 암호를 사용 합니다. 이 옵션은-UserName 옵션으로 사용 합니다.|
|-사용자|구성-사용자 컨텍스트를 새 인증서 요청에 대 한 컨텍스트를 지정 하거나는 인증서를 허용 합니다. INF 또는 서식 파일에 지정 되지 않은 경우 기본 컨텍스트에입니다.|
|-컴퓨터|새 인증서 요청을 구성 하거나 컨텍스트를 지정 된 컴퓨터 컨텍스트에 대 한 인증서를 허용 합니다. 새 요청에 대 한 템플릿 컨텍스트와 MachineKeyset INF 키와 일치 이어야 합니다. 이 옵션을 지정 하지 않으면 템플릿에 컨텍스트를 설정 하지 않는 경우 기본값은 사용자 컨텍스트입니다.|
|-crl|Crl (해지 목록) 출력 CertChainFileOut로 지정 된 base 64 인코딩 PKCS #7 파일 또는 RequestFileOut로 지정 된 base64 인코딩 파일에에서 인증서를 포함 합니다.|
|-rpc|Active Directory 인증서 서비스 (AD CS) 분산 COM. 대신 원격 프로시저 호출 (RPC) 서버 연결을 사용 하도록 지시 합니다.|
|-AdminForceMachine|키 서비스 또는 가장을 사용 하 여 로컬 시스템 컨텍스트에서 요청을 제출 합니다. 이 옵션을 호출 하는 사용자의 로컬 관리자 구성원 되도록 요구 합니다.|
|-RenewOnBehalfOf|서명 인증서에 식별 된 주체를 대신 하 여 갱신을 제출 합니다. 호출할 때이 설정 CR_IN_ROBO [ICertRequest::Submit](https://technet.microsoft.com/subscriptions/aa385040.aspx)|
|-f|기존 파일을 덮어쓰도록 강제 합니다. 캐싱 템플릿 및 정책에도 무시합니다.|
|-q|자동 모드를 사용 합니다. 모든 대화형 프롬프트를 표시 합니다.|
|유니코드|출력에 씁니다 유니코드 표준 출력 리디렉션되거나 Windows PowerShell® 스크립트에서 호출 될 때 도움이 되는 다른 명령에 연결 하는 경우).|
|-UnicodeText|파일에 데이터 blob 인코딩된 base64 텍스트를 작성 하는 경우 유니코드 출력을 보냅니다.|

으로 돌아가서 [내용](#BKMK_Contents)

## <a name="BKMK_Formats"></a>형식

|형식|설명|
|-------|-----------|
|RequestFileIn|Base64로 인코딩된 또는 이진 입력된 파일 이름: PKCS #10 인증서 요청, CMS 인증서 요청, PKCS #7 인증서 갱신 요청, 상호 인증에 X.509 인증서 또는 KeyGen 태그 형식 인증서 요청 합니다.|
|RequestFileOut|Base64 인코딩된 출력 파일 이름|
|CertFileOut|Base64 인코딩된 X-509 파일 이름입니다.|
|PKCS10FileOut|와 함께 사용할는 [Certreq-정책](#BKMK_policy) 동사만 합니다. Base64 인코딩된 PKCS10 출력 파일 이름입니다.|
|CertChainFileOut|Base 64 인코딩 PKCS #7 파일 이름입니다.|
|FullResponseFileOut|Base64 인코딩된 전체 응답 파일 이름입니다.|
|PolicyFileIn|와 함께 사용할는 [Certreq-정책](#BKMK_policy) 동사만 합니다. 요청을 한 정하는 데 사용 되는 확장의 텍스트 표현을 포함 하는 INF 파일입니다.|

## <a name="BKMK_Examples"></a>추가 certreq 예제

다음 문서 certreq 사용의 예를 들어:
-   [사용자 지정 주체 대체 이름으로 인증서를 요청 하는 방법](https://technet.microsoft.com/library/ff625722.aspx)
-   [테스트 랩 가이드: AD CS 2 계층 PKI 계층 배포](https://technet.microsoft.com/library/hh831348.aspx)
-   [부록 3: Certreq.exe 구문](https://technet.microsoft.com/library/cc736326.aspx)
-   [웹 서버 SSL 인증서를 수동으로 만들어야 하는 방법](http://blogs.technet.com/b/pki/archive/2009/08/05/how-to-create-a-web-server-ssl-certificate-manually.aspx)
-   [AMT 프로 비전 Windows Server 2008 CA를 사용 하 여 인증서를 요청](https://social.technet.microsoft.com/wiki/contents/articles/request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)
-   [System Center Operations Manager 에이전트에 대 한 인증서 등록](https://social.technet.microsoft.com/wiki/contents/articles/certificate-enrollment-for-system-center-operations-manager-agent.aspx)
-   [AD CS 단계별 가이드: 2 계층 PKI 계층 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)
-   [타사 인증 기관에 SSL을 통해 LDAP를 사용 하는 방법](https://support.microsoft.com/kb/321051)

으로 돌아가서 [내용](#BKMK_Contents)
