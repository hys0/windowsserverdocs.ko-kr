---
title: certreq
description: Certreq 명령에 대 한 참조 항목으로, CA (인증 기관)에서 인증서를 요청 하 고, CA에서 이전 요청에 대 한 응답을 검색 하 고, .inf 파일에서 새 요청을 생성 하 고, 요청에 대 한 응답을 수락 및 설치 하 고, 기존 CA 인증서 또는 요청에서 상호 인증 또는 정규 종속 요청을 생성 하 고, 상호 인증 또는 정규화 된 종속 요청
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7a04e51f-f395-4bff-b57a-0e9efcadf973
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 14fc717ad49a676387206692af32842f212c4296
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719644"
---
# <a name="certreq"></a>certreq

Certreq 명령을 사용 하 여 CA (인증 기관)에서 인증서를 요청할 수 있습니다. CA에서 이전 요청에 대 한 응답을 검색 하려면 .inf 파일에서 새 요청을 만들고, 요청에 대 한 응답을 수락 및 설치 하 고, 기존 CA 인증서 또는 요청에서 교차 인증 또는 정규화 된 종속 요청을 생성 하 고, 상호 인증 또는 정규 종속 요청을 서명 합니다.

> [!IMPORTANT]
> 이전 버전의 certreq 명령은 여기에 설명 된 일부 옵션을 제공 하지 않을 수 있습니다. Certreq의 특정 버전에 따라 지원 되는 옵션을 확인 하려면 명령줄 도움말 옵션인를 `certreq -v -?`실행 합니다.
>
> Certreq 명령은 CEP/CES 환경에서 키 증명 템플릿을 기반으로 새 인증서 요청을 만드는 것을 지원 하지 않습니다.

> [!WARNING]
> 이 항목의 내용은 Windows Server에 대 한 기본 설정을 기반으로 합니다. 예를 들어 키 길이를 2048로 설정 하 고, CSP로 Microsoft 소프트웨어 키 저장소 공급자를 선택 하 고, SHA(Secure Hash Algorithm) 1 (SHA1)를 사용 합니다. 회사의 보안 정책에 대 한 요구 사항에 따라 이러한 선택 항목을 평가 합니다.

## <a name="syntax"></a>구문

```
certreq [-submit] [options] [requestfilein [certfileout [certchainfileout [fullresponsefileOut]]]]
certreq -retrieve [options] requestid [certfileout [certchainfileout [fullresponsefileOut]]]
certreq -new [options] [policyfilein [requestfileout]]
certreq -accept [options] [certchainfilein | fullresponsefilein | certfilein]
certreq -sign [options] [requestfilein [requestfileout]]
certreq –enroll [options] templatename
certreq –enroll –cert certId [options] renew [reusekeys]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------- | ----------- |
| -제출 | 인증 기관에 요청을 제출 합니다. |
| -검색`<requestid>` | 인증 기관에서 이전 요청에 대 한 응답을 검색 합니다. |
| -신규 | .Inf 파일에서 새 요청을 만듭니다. |
| -수락 | 수신 하 고 인증서 요청에 대 한 응답을 설치 합니다. |
| -정책 | 요청에 대 한 정책을 설정합니다. |
| -기호 | 상호 인증 또는 정규화 된 종속 요청을 서명합니다. |
| -등록 | 에 대 한 등록 하거나, 인증서를 갱신 합니다. |
| -? | Certreq 구문, 옵션 및 설명의 목록을 표시합니다. |
| `<parameter>` -? | 지정 된 매개 변수에 대 한 도움말을 표시 합니다. |
| -v -? | Certreq 구문, 옵션 및 설명의 자세한 목록이 표시 됩니다. |

## <a name="examples"></a>예

### <a name="certreq--submit"></a>certreq-제출

단순 인증서 요청을 제출 하려면:

```
certreq –submit certrequest.req certnew.cer certnew.pfx
```

#### <a name="remarks"></a>설명

- 이 매개 변수는 기본 certreq 매개 변수입니다. 명령줄 프롬프트에서 옵션을 지정 하지 않으면 certreq는 인증 기관에 인증서 요청을 제출 하려고 합니다. **– Submit** 옵션을 사용할 때 인증서 요청 파일을 지정 해야 합니다. 이 매개 변수를 생략 하면 적절 한 인증서 요청 파일을 선택할 수 있는 공용 **파일 열기** 창이 표시 됩니다.

- SAN 특성을 지정 하 여 인증서를 요청 하려면 Microsoft 기술 자료 문서 931351 [보안 LDAP 인증서에 주체 대체 이름을 추가 하는 방법](https://support.microsoft.com/kb/931351) *certreq 유틸리티를 사용 하 여 인증서 요청을 만들고 제출* 하는 방법 섹션을 참조 하세요.

### <a name="certreq--retrieve"></a>certreq-검색

인증서 ID 20을 검색 하 고 이름이 *Mycertificate*인 인증서 파일 (.cer)을 만들려면 다음을 수행 합니다.

```
certreq -retrieve 20 MyCertificate.cer
```

#### <a name="remarks"></a>설명

- Certreq-인증 기관에서 인증서를 발급 한 후이를 *검색 하 여* 인증서를 검색 합니다. *Requestid* pkc는 0x 접두사가 있는 10 진수 또는 16 진수 일 수 있으며, 0x 접두사가 없는 인증서 일련 번호 일 수 있습니다. 인증서 요청이 보류 중 상태 인지 여부에 관계 없이 해지 되었거나 만료 된 인증서를 비롯 하 여 인증 기관에서 발급 한 모든 인증서를 검색 하는 데 사용할 수도 있습니다.

- 인증 기관에 요청을 제출 하는 경우 인증 기관의 정책 모듈은 요청을 보류 중 상태로 유지 하 고 certreq 호출자에 게 요청 *id* 를 반환 하 여 표시할 수 있습니다. 결국 인증 기관의 관리자가 인증서를 발급 하거나 요청을 거부 합니다.

### <a name="certreq--new"></a>certreq-신규

새 요청을 만들려면 다음을 수행 합니다.

```
[newrequest]
; At least one value must be set in this section
subject = CN=W2K8-BO-DC.contoso2.com
```

다음은 일부 가능한 섹션 INF 파일에 추가할 수 있습니다.

#### <a name="newrequest"></a>[newrequest]

INF 파일의이 영역은 새 인증서 요청 템플릿에 필수 이며 값이 포함 된 매개 변수를 하나 이상 포함 해야 합니다.

| 키<sup>1</sup> | 설명 | 값<sup>2</sup> | 예제 |
| --- | ---------- | ----- | ------- |
| 제목 | 여러 앱은 인증서의 주체 정보를 사용 합니다. 이 키의 값을 지정 하는 것이 좋습니다. 여기에서 주체를 설정 하지 않은 경우 주체 대체 이름 인증서 확장의 일부로 주체 이름을 포함 하는 것이 좋습니다. | 상대 고유 이름 문자열 값 | Subject = CN = computer1 Subject = CN = John Smith, CN = Users, DC = Contoso, DC = com |
| Exportable | TRUE로 설정 되 면 인증서를 사용 하 여 개인 키를 내보낼 수 있습니다. 높은 수준의 보안을 유지 하기 위해 개인 키를 내보낼 수 없습니다. 그러나 경우에 따라 여러 컴퓨터 또는 사용자가 동일한 개인 키를 공유 해야 하는 경우 필요할 수 있습니다. | `true | false` | `Exportable = TRUE`. CNG 키를이 구별할 수 및 일반 텍스트를 내보낼 수 있습니다. CAPI1 키를 사용할 수 없습니다. |
| ExportableEncrypted | 프라이빗 키를 내보낼 수로 설정 해야 하는지 여부를 지정 합니다. | `true | false` | `ExportableEncrypted = true`<p>**팁:** 모든 공개 키 크기 및 알고리즘이 모든 해시 알고리즘에서 작동 하는 것은 아닙니다. 지정 된 CSP도 지정 된 해시 알고리즘을 지원 해야 합니다. 지원 되는 해시 알고리즘의 목록을 보려면 명령을 실행할 수 있습니다.`certutil -oid 1 | findstr pwszCNGAlgid | findstr /v CryptOIDInfo` |
| HashAlgorithm | 이 요청에 사용할 해시 알고리즘입니다. | `Sha256, sha384, sha512, sha1, md5, md4, md2` | `HashAlgorithm = sha1`. 지원 되는 해시 알고리즘의 목록을 보려면 certutil-oid 1을 사용 합니다. | findstr pwszCNGAlgid | findstr/v CryptOIDInfo|
| KeyAlgorithm| 퍼블릭 및 프라이빗 키 쌍을 생성 하려면 서비스 공급자가 사용할 수 있는 알고리즘입니다.| `RSA, DH, DSA, ECDH_P256, ECDH_P521, ECDSA_P256, ECDSA_P384, ECDSA_P521` | `KeyAlgorithm = RSA` |
| KeyContainer | 새 키 자료가 생성 되는 새 요청에 대해서는이 매개 변수를 설정 하지 않는 것이 좋습니다. 키 컨테이너는 자동으로 생성 하 고 시스템에 의해 유지.<p>여기서는 기존 키 자료를 사용 해야 하는 요청에 대 한 기존 키의 키 컨테이너 이름으로이 값을 설정할 수 있습니다. `certutil –key` 명령을 사용 하 여 컴퓨터 컨텍스트에 사용할 수 있는 키 컨테이너 목록을 표시 합니다. 현재 사용자 `certutil –key –user` 의 컨텍스트에 대해 명령을 사용 합니다.| 임의의 문자열 값<p>**팁:** 잠재적 INF 구문 분석 문제를 방지 하려면 공백이 나 특수 문자를 포함 하는 모든 INF 키 값 주위에 큰따옴표를 사용 합니다. | `KeyContainer = {C347BD28-7F69-4090-AA16-BC58CF4D749C}` |
| 키 길이 | 퍼블릭 및 프라이빗 키의 길이 정의합니다. 키 길이 인증서의 보안 수준에 영향이 있습니다. 더 긴 키 길이는 일반적으로 더 높은 보안 수준; 제공 그러나 일부 애플리케이션 키 길이 관련 된 제한이 있을 수 있습니다. | 암호화 서비스 공급자에서 지 원하는 모든 유효한 키 길이입니다. | `KeyLength = 2048` |
| KeySpec | 키 서명, Exchange (암호화), 또는 둘 다에 사용 될 수 하는 경우를 결정 합니다. | `AT_NONE, AT_SIGNATURE, AT_KEYEXCHANGE` | `KeySpec = AT_KEYEXCHANGE` |
| KeyUsage | 어떤 인증서 키에 사용할지를 정의 합니다. | <ul><li>`CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)`</li><li>`CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)`</li><li>`CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)`</li><li>`CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)`</li><li>`CERT_KEY_AGREEMENT_KEY_USAGE -- 8`</li><li>`CERT_KEY_CERT_SIGN_KEY_USAGE -- 4`</li><li>`CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_ENCIPHER_ONLY_KEY_USAGE -- 1`</li><li>`CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)`</li></ul> | `KeyUsage = CERT_DIGITAL_SIGNATURE_KEY_USAGE | CERT_KEY_ENCIPHERMENT_KEY_USAGE`<p>**팁:** 여러 값이 파이프를 사용 합니다.|) 기호 구분 기호를 구분 합니다. INF 구문 분석 문제를 방지 하려면 여러 값을 사용 하는 경우 큰따옴표를 사용 하는 것을 확인 합니다. 표시 되는 값은 각 비트 정의에 대 한 16 진수 (10 진수) 값입니다. 오래 된 구문을 사용할 수도 있습니다: 여러 개의 단일 16 진수 값을 비트 기호 표현 하는 대신 집합입니다. `KeyUsage = 0xa0`)을 입력합니다. |
| KeyUsageProperty | 프라이빗 키를 사용할 수 있는 특정 용도 식별 하는 값을 검색 합니다. | <ul><li>`NCRYPT_ALLOW_DECRYPT_FLAG -- 1`</li><li>`NCRYPT_ALLOW_SIGNING_FLAG -- 2`</li><li>`NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4`</li><li>`NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)`</li></ul> | `KeyUsageProperty = NCRYPT_ALLOW_DECRYPT_FLAG | NCRYPT_ALLOW_SIGNING_FLAG` |
| MachineKeySet | 이 키는 컴퓨터와 사용자가 아닌 소유 하는 인증서를 만들어야 할 때 중요 합니다. 생성 되는 키 자료의 보안 컨텍스트 보안 주체 (사용자 또는 컴퓨터 계정)가 만든 요청에에서 유지 됩니다. 관리자가 컴퓨터를 대신 하 여 인증서 요청을 만들 때 키 자료는 관리자의 보안 컨텍스트가 아니라 컴퓨터의 보안 컨텍스트에서 만들어야 합니다. 그렇지 않으면 관리자의 보안 컨텍스트에 있기 때문에 컴퓨터가 개인 키에 액세스할 수 없습니다. | `true | false`. 기본값은 false입니다. | `MachineKeySet = true` |
| NotBefore | 날짜 또는 날짜 및 되기까지의 요청을 실행할 수 없습니다 시간을 지정 합니다. `NotBefore`및 `ValidityPeriod` `ValidityPeriodUnits`와 함께 사용할 수 있습니다. | 날짜 또는 날짜 및 시간 | `NotBefore = 7/24/2012 10:31 AM`<p>**팁:** `NotBefore` 및 `NotAfter` 는 R`equestType=cert` 전용입니다. 날짜 구문 분석에서 로캘을 구분 하려고 합니다. 월 이름을 사용 하는 경우 모든 로캘에서 명확 하 게 사용할 수 있습니다. |
| NotAfter | 날짜 또는 날짜 및 시간을 요청을 실행할 수 없습니다 지정 합니다. `NotAfter`또는 `ValidityPeriod` `ValidityPeriodUnits`와 함께 사용할 수 없습니다. | 날짜 또는 날짜 및 시간 | `NotAfter = 9/23/2014 10:31 AM`<p>**팁:** `NotBefore` 및 `NotAfter` 는에 `RequestType=cert` 만 해당 됩니다. 날짜 구문 분석에서 로캘을 구분 하려고 합니다. 월 이름을 사용 하는 경우 모든 로캘에서 명확 하 게 사용할 수 있습니다. |
| PrivateKeyArchive | PrivateKeyArchive 설정은 해당 RequestType이 CMC로 설정 된 경우에만 작동 합니다. 예를 들어 CMC (인증서 관리 메시지) 요청 형식을 사용 하면 키 보관을 위해 요청자의 개인 키를 CA에 안전 하 게 전송할 수 있습니다. | `true | false` | `PrivateKeyArchive = true` |
| EncryptionAlgorithm | 사용할 암호화 알고리즘입니다. | 가능한 옵션은 운영 체제 버전 및 설치 된 암호화 공급자 집합에 따라 달라 집니다. 사용 가능한 알고리즘 목록을 보려면 명령을 실행 합니다 `certutil -oid 2 | findstr pwszCNGAlgid`. 사용 된 지정 된 CSP는 지정 된 대칭 암호화 알고리즘과 길이만 지원 해야 합니다. | `EncryptionAlgorithm = 3des` |
| EncryptionLength | 사용할 암호화 알고리즘의 길이입니다. | 지정한 EncryptionAlgorithm에서 허용 된 길이입니다. | `EncryptionLength = 128` |
| ProviderName | 공급자 이름은 CSP의 표시 이름입니다. | 사용 중인 CSP의 공급자 이름을 모르는 경우 명령줄에서를 실행 `certutil –csplist` 합니다. 이 명령은 로컬 시스템에서 사용할 수 있는 모든 Csp의 이름이 표시 됩니다. | `ProviderName = Microsoft RSA SChannel Cryptographic Provider` |
| ProviderType | 공급자 유형은 RSA Full과 같은 특정 알고리즘 기능에 따라 특정 공급자를 선택 하는 데 사용 됩니다. | 사용 중인 CSP의 공급자 유형을 알 수 없는 경우 명령줄 프롬프트에서를 실행 `certutil –csplist` 합니다. 이 명령은 로컬 시스템에서 사용할 수 있는 모든 Csp의 공급자 형식을 표시 됩니다. | `ProviderType = 1` |
| RenewalCert | 인증서 요청 생성 된 경우 시스템에 존재 하는 인증서를 갱신 해야 하는 경우에이 키에 대 한 값으로 인증서 해시를 지정 해야 합니다. | 인증서 요청을 만들 되는 컴퓨터에서 사용할 수 있는 모든 인증서의 인증서 해시입니다. 인증서 해시를 알 수 없는 경우에 인증서 MMC 스냅인을 사용 하 여을 갱신 해야 하는 인증서를 살펴봅니다. 인증서 속성을 열고 인증서의 `Thumbprint` 특성을 확인 합니다. 인증서를 `PKCS#7` 갱신 하려면 또는 `CMC` 요청 형식이 필요 합니다. | `RenewalCert = 4EDF274BD2919C6E9EC6A522F0F3B153E9B1582D` |
| RequesterName | 다른 사용자 요청을 대신 하 여 등록 요청을 만듭니다. 또한 등록 에이전트 인증서를 사용 하 여 요청을 서명 해야 합니다. 그렇지 않으면 CA에서 요청을 거부 합니다. `-cert` 옵션을 사용 하 여 등록 에이전트 인증서를 지정 합니다. `RequestType` 이 또는 `PKCS#7` `CMC`로 설정 된 경우 인증서 요청에 대해 요청자 이름을 지정할 수 있습니다. `RequestType` 가로 `PKCS#10`설정 된 경우에는이 키가 무시 됩니다. 는 `Requestername` 요청의 일부로만 설정할 수 있습니다. 보류 중인 요청에서 `Requestername` 을 조작할 수 없습니다. | `Domain\User` | `Requestername = Contoso\BSmith` |
| RequestType | 생성 하 고 인증서 요청을 전송 하는 데 사용 되는 표준에 따라 결정 됩니다. | <ul><li>`PKCS10 -- 1`</li><li>`PKCS7 -- 2`</li><li>`CMC -- 3`</li><li>`Cert -- 4`</li><li>`SCEP -- fd00 (64768)`</li></ul>**팁:** 이 옵션은 자체 서명 된 인증서 또는 자체 발급 된 인증서를 나타냅니다. 요청을 생성 하지 않고 새 인증서를 생성 한 다음 인증서를 설치 합니다. 자체 서명 됨이 기본값입니다. -Cert 옵션을 사용 하 여 서명 인증서를 지정 하 여 자체 서명 되지 않은 자체 발급 인증서를 만듭니다. | `RequestType = CMC` |
| SecurityDescriptor | 보안 개체와 연결 된 보안 정보를 포함 합니다. 대부분의 보안 개체에 대해 개체를 만드는 함수 호출에서 개체의 보안 설명자를 지정할 수 있습니다. [보안 설명자 정의 언어](https://msdn.microsoft.com/library/aa379567(v=vs.85).aspx)를 기반으로 하는 문자열입니다.<p>**팁:** 이는 컴퓨터 컨텍스트 비 스마트 카드 키와 관련 된 것입니다. | `SecurityDescriptor = D:P(A;;GA;;;SY)(A;;GA;;;BA)` |
| AlternateSignatureAlgorithm | 지정 하 고 불연속 또는 조합 된 PKCS #10 요청 또는 인증서 서명에 대 한 서명 알고리즘 개체 식별자 (OID) 인지 여부를 나타내는 부울 값을 검색 합니다. | `true | false` | `AlternateSignatureAlgorithm = false`<p>RSA 시그니처의 경우는를 `false` 나타내며 `Pkcs1 v1.5`,는 `true` `v2.1` 서명을 나타냅니다. |
| 자동 | 기본적으로이 옵션에는 사용자에 게 서 스마트 카드 PIN와 같은 대화형 사용자 데스크톱 및 요청 정보를 CSP 액세스할을 수 있습니다. 이 키가 TRUE로 설정, CSP 데스크톱과 상호 작용 해서는 안 하 고 사용자에 게 모든 사용자 인터페이스를 표시 차단 됩니다. | `true | false` | `Silent = true` |
| SMIME | 이 매개 변수는 TRUE로 설정 하는 경우 개체 식별자 값 1.2.840.113549.1.9.15 확장이 요청에 추가 됩니다. 개체 식별자의 수에 따라 다릅니다은 Outlook 같은 Secure Multipurpose Internet Mail Extensions (S/MIME) 애플리케이션에서 사용할 수 있는 대칭 암호화 알고리즘에 대 한 참조는 설치 된 운영 체제 버전 및 CSP 기능에 있습니다. | `true | false` | `SMIME = true` |
| UseExistingKeySet | 이 매개 변수를 사용 하 여 인증서 요청을 만드는 기존 키 쌍을 사용 해야 함을 지정 합니다. 이 키가 TRUE로 설정 하는 경우 RenewalCert 키 또는 KeyContainer 이름에 대 한 값도 지정 해야 합니다. 기존 키의 속성을 변경할 수 없으므로 하지 내보낼 수 있는 키를 설정 해야 합니다. 이 경우 키 자료가 인증서 요청을 빌드할 때 생성 됩니다. | `true | false` | `UseExistingKeySet = true` |
| KeyProtection | 사용 하기 전에 프라이빗 키를 보호 하는 방법을 나타내는 값을 지정 합니다. | <ul><li>`XCN_NCRYPT_UI_NO_PROTCTION_FLAG -- 0`</li><li>`XCN_NCRYPT_UI_PROTECT_KEY_FLAG -- 1`</li><li>`XCN_NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2`</li></ul> | `KeyProtection = NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG` |
| SuppressDefaults | 기본 확장 프로그램 및 특성 요청에 포함 되는지 여부를 나타내는 부울 값을 지정 합니다. 기본값은 해당 Oid (개체 식별자)으로 표현 됩니다. | `true | false` | `SuppressDefaults = true` |
| FriendlyName | 새 인증서 이름입니다. | Text | `FriendlyName = Server1` |
| ValidityPeriodUnits | ValidityPeriod 함께 사용 되는 단위 수를 지정 합니다. 참고:이는이 사용 되는 `request type=cert`경우에만 사용 됩니다. | 숫자 | `ValidityPeriodUnits = 3` |
| ValidityPeriod | ValidityPeriod는 미국 영어 복수형 기간 이어야 합니다. 참고: 요청 유형 = cert 인 경우에만 사용 됩니다. | `Years |  Months | Weeks | Days | Hours | Minutes | Seconds` | `ValidityPeriod = Years` |

<sup>1</sup> 등호 (=)의 왼쪽에 있는 매개 변수입니다.

<sup>2</sup> 등호 (=) 오른쪽에 있는 매개 변수

#### <a name="extensions"></a>확장할

이 섹션은 선택 사항입니다.

| OID 확장 | 정의 | 예제 |
| ------------- | ---------- | ----- | ------- |
| 2.5.29.17 | | 2.5.29.17 = {text} |
| *continue* | | `continue = UPN=User@Domain.com&` |
| *continue* | | `continue = EMail=User@Domain.com&` |
| *continue* | | `continue = DNS=host.domain.com&` |
| *continue* | | `continue = DirectoryName=CN=Name,DC=Domain,DC=com&` |
| *continue* | | `continue = URL=<http://host.domain.com/default.html&>` |
| *continue* | | `continue = IPAddress=10.0.0.1&` |
| *continue* | | `continue = RegisteredId=1.2.3.4.5&` |
| *continue* | | `continue = 1.2.3.4.6.1={utf8}String&` |
| *continue* | | `continue = 1.2.3.4.6.2={octet}AAECAwQFBgc=&` |
| *continue* | | `continue = 1.2.3.4.6.2={octet}{hex}00 01 02 03 04 05 06 07&` |
| *continue* | | `continue = 1.2.3.4.6.3={asn}BAgAAQIDBAUGBw==&` |
| *continue* | | `continue = 1.2.3.4.6.3={hex}04 08 00 01 02 03 04 05 06 07` |
| 2.5.29.37 | | `2.5.29.37={text}` |
| *continue* | | `continue = 1.3.6.1.5.5.7` |
| *continue* | | `continue = 1.3.6.1.5.5.7.3.1` |
| 2.5.29.19 | | `{text}ca=0pathlength=3` |
| 위험 | | `Critical=2.5.29.19` |
| KeySpec | | <ul><li>`AT_NONE -- 0`</li><li>`AT_SIGNATURE -- 2`</li><li>`AT_KEYEXCHANGE -- 1`</ul></li> |
| RequestType | | <ul><li>`PKCS10 -- 1`</li><li>`PKCS7 -- 2`</li><li>`CMC -- 3`</li><li>`Cert -- 4`</li><li>`SCEP -- fd00 (64768)`</li></ul> |
| KeyUsage | | <ul><li>`CERT_DIGITAL_SIGNATURE_KEY_USAGE -- 80 (128)`</li><li>`CERT_NON_REPUDIATION_KEY_USAGE -- 40 (64)`</li><li>`CERT_KEY_ENCIPHERMENT_KEY_USAGE -- 20 (32)`</li><li>`CERT_DATA_ENCIPHERMENT_KEY_USAGE -- 10 (16)`</li><li>`CERT_KEY_AGREEMENT_KEY_USAGE -- 8`</li><li>`CERT_KEY_CERT_SIGN_KEY_USAGE -- 4`</li><li>`CERT_OFFLINE_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_CRL_SIGN_KEY_USAGE -- 2`</li><li>`CERT_ENCIPHER_ONLY_KEY_USAGE -- 1`</li><li>`CERT_DECIPHER_ONLY_KEY_USAGE -- 8000 (32768)`</li></ul> |
| KeyUsageProperty | | <ul><li>`NCRYPT_ALLOW_DECRYPT_FLAG -- 1`</li><li>`NCRYPT_ALLOW_SIGNING_FLAG -- 2`</li><li>`NCRYPT_ALLOW_KEY_AGREEMENT_FLAG -- 4`</li><li>`NCRYPT_ALLOW_ALL_USAGES -- ffffff (16777215)`</li></ul> |
| KeyProtection | | <ul><li>`NCRYPT_UI_NO_PROTECTION_FLAG -- 0`</li><li>`NCRYPT_UI_PROTECT_KEY_FLAG -- 1`</li><li>`NCRYPT_UI_FORCE_HIGH_PROTECTION_FLAG -- 2`</li></ul> |
| SubjectNameFlags | template | <ul><li>`CT_FLAG_SUBJECT_REQUIRE_COMMON_NAME -- 40000000 (1073741824)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_DIRECTORY_PATH -- 80000000 (2147483648)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_DNS_AS_CN -- 10000000 (268435456)`</li><li>`CT_FLAG_SUBJECT_REQUIRE_EMAIL -- 20000000 (536870912)`</li><li>`CT_FLAG_OLD_CERT_SUPPLIES_SUBJECT_AND_ALT_NAME -- 8`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DIRECTORY_GUID -- 1000000 (16777216)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DNS -- 8000000 (134217728)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_DOMAIN_DNS -- 400000 (4194304)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_EMAIL -- 4000000 (67108864)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_SPN -- 800000 (8388608)`</li><li>`CT_FLAG_SUBJECT_ALT_REQUIRE_UPN -- 2000000 (33554432)`</li></ul> |
| X500NameFlags | | <ul><li>`CERT_NAME_STR_NONE -- 0`</li><li>`CERT_OID_NAME_STR -- 2`</li><li>`CERT_X500_NAME_STR -- 3`</li><li>`CERT_NAME_STR_SEMICOLON_FLAG -- 40000000 (1073741824)`</li><li>`CERT_NAME_STR_NO_PLUS_FLAG -- 20000000 (536870912)`</li><li>`CERT_NAME_STR_NO_QUOTING_FLAG -- 10000000 (268435456)`</li><li>`CERT_NAME_STR_CRLF_FLAG -- 8000000 (134217728)`</li><li>`CERT_NAME_STR_COMMA_FLAG -- 4000000 (67108864)`</li><li>`CERT_NAME_STR_REVERSE_FLAG -- 2000000 (33554432)`</li><li>`CERT_NAME_STR_FORWARD_FLAG -- 1000000 (16777216)`</li><li>`CERT_NAME_STR_DISABLE_IE4_UTF8_FLAG -- 10000 (65536)`</li><li>`CERT_NAME_STR_ENABLE_T61_UNICODE_FLAG -- 20000 (131072)`</li><li>`CERT_NAME_STR_ENABLE_UTF8_UNICODE_FLAG -- 40000 (262144)`</li><li>`CERT_NAME_STR_FORCE_UTF8_DIR_STR_FLAG -- 80000 (524288)`</li><li>`CERT_NAME_STR_DISABLE_UTF8_DIR_STR_FLAG -- 100000 (1048576)`</li><li>`CERT_NAME_STR_ENABLE_PUNYCODE_FLAG -- 200000 (2097152)`</li></ul> |

> [!NOTE]
> `SubjectNameFlags`INF 파일에서 현재 사용자 또는 현재 컴퓨터 속성 (예: DNS 이름, UPN 등)을 기반으로 certreq에서 자동으로 채울 **Subject** 및 **SubjectAltName** 확장 필드를 지정할 수 있습니다. 리터럴 템플릿을 사용 하면 템플릿 이름 플래그가 대신 사용 됩니다. 따라서 단일 INF 파일을 상황에 맞는 주체 정보를 사용 하 여 요청을 생성 하는 여러 컨텍스트에서 사용할 수 있습니다.
>
> `X500NameFlags`값이 a s n. 1로 `CertStrToName` 인코딩된 고유 이름으로 변환 될 때 API에 직접 전달할 플래그를 지정 합니다. **Name** `Subject INF keys`

#### <a name="example"></a>예제

메모장에서 정책 파일 (.inf)을 만든 다음 *requestconfig .inf*로 저장 합니다.

```
[NewRequest]
Subject = CN=<FQDN of computer you are creating the certificate>
Exportable = TRUE
KeyLength = 2048
KeySpec = 1
KeyUsage = 0xf0
MachineKeySet = TRUE
[RequestAttributes]
CertificateTemplate=WebServer
[Extensions]
OID = 1.3.6.1.5.5.7.3.1
OID = 1.3.6.1.5.5.7.3.2
```

인증서를 요청 하는 컴퓨터에서 다음을 수행 합니다.

```
certreq –new requestconfig.inf certrequest.req
```

Oid에 대해 [Strings] 섹션 구문을 사용 하 고 데이터를 해석 하기 어려운 경우 Oid 쉼표로 구분 된 목록을 사용 하 여 EKU 확장을 위한 새로운 {text} 구문 예제:

```
[Version]
Signature=$Windows NT$

[Strings]
szOID_ENHANCED_KEY_USAGE = 2.5.29.37
szOID_PKIX_KP_SERVER_AUTH = 1.3.6.1.5.5.7.3.1
szOID_PKIX_KP_CLIENT_AUTH = 1.3.6.1.5.5.7.3.2

[NewRequest]
Subject = CN=TestSelfSignedCert
Requesttype = Cert

[Extensions]
%szOID_ENHANCED_KEY_USAGE%={text}%szOID_PKIX_KP_SERVER_AUTH%,
_continue_ = %szOID_PKIX_KP_CLIENT_AUTH%
```

### <a name="certreq--accept"></a>certreq-수락

매개 `–accept` 변수는 이전에 생성 된 개인 키를 발급 된 인증서와 연결 하 고 인증서가 요청 된 시스템에서 보류 중인 인증서 요청을 제거 합니다 (일치 하는 요청이 있는 경우).

인증서를 수동으로 수락 하려면:

```
certreq -accept certnew.cer
```

> [!WARNING]
> `-user` 및 `–machine` 옵션과 `-accept` 함께 매개 변수를 사용 하면 설치 하는 인증서 **가 사용자** 또는 **컴퓨터** 컨텍스트에 설치 되어야 하는지 여부가 표시 됩니다. 설치 중인 공개 키와 일치 하는 컨텍스트에 처리 중인 요청이 있는 경우 이러한 옵션은 필요 하지 않습니다. 처리 중인 요청이 없을 경우 다음 중 하나 지정 해야 합니다.

### <a name="certreq--policy"></a>certreq-정책

정책 .inf 파일은 정규화 된 종속가 정의 된 경우 CA 인증에 적용 되는 제약 조건을 정의 하는 구성 파일입니다.

인증서 간 요청을 빌드하려면 다음을 수행 합니다.

```
certreq -policy certsrv.req policy.inf newcertsrv.req
```

추가 `certreq -policy` 매개 변수 없이를 사용 하면 대화 상자 창이 열리며,이를 통해 요청 된 파일 (. 요청, cmc, .txt,. x x x 또는 .crt)를 선택할 수 있습니다. 요청 된 파일을 선택 하 고 **열기**를 클릭 한 후에는 정책 .inf 파일을 선택할 수 있는 다른 대화 상자 창이 열립니다.

#### <a name="examples"></a>예

[Capolicy.inf 구문](https://docs.microsoft.com/windows-server/networking/core-network-guide/cncg/server-certs/prepare-the-capolicy-inf-file)에서 정책 .inf 파일의 예를 찾습니다.

### <a name="certreq--sign"></a>certreq-서명

새 인증서 요청을 만들고, 서명 하 고, 전송 하려면 다음을 수행 합니다.

```
certreq -new policyfile.inf myrequest.req
certreq -sign myrequest.req myrequest.req
certreq -submit myrequest_sign.req myrequest_cert.cer
```

#### <a name="remarks"></a>설명

- 추가 `certreq -sign` 매개 변수 없이를 사용 하면 요청 된 파일 (요청, cmc, txt, der, cer 또는 crt)을 선택할 수 있는 대화 상자 창이 열립니다.

- 정규 종속 요청을 서명 하려면 **엔터프라이즈 관리자** 자격 증명이 필요할 수 있습니다. 이것이 정규 종속에 대 한 서명 인증서를 발급 하는 것이 가장 좋습니다.

- 정규화 된 종속 요청에 서명 하는 데 사용 되는 인증서는 정규화 된 종속 템플릿을 사용 합니다. 엔터프라이즈 관리자는 요청에 서명 하거나 인증서에 서명 하는 개인에 게 사용자 권한을 부여 해야 합니다.

- 사용자가 CMC 요청에 서명 해야 할 수도 있습니다. 이는 정규 종속과 관련 된 보증 수준에 따라 달라 집니다.

- 부모 CA를 설치 하는 정식된 하위 CA의 오프 라인 상태 이면 받아야 CA 인증서 정식된 하위 CA에 대 한 서버를 오프 라인 부모입니다. 부모 CA가 온라인 상태인 경우 **인증서 서비스 설치** 마법사를 실행 하는 동안 정규화 된 하위 ca에 대 한 ca 인증서를 지정 합니다.

### <a name="certreq--enroll"></a>certreq-등록

이 주석을 사용 하 여 인증서를 등록 하거나 갱신할 수 있습니다.

#### <a name="examples"></a>예

웹 서버 템플릿을 사용 하 고 U/I를 사용 하 여 정책 서버를 선택 하 여 인증서를 *등록 합니다.*

```
certreq -enroll –machine –policyserver * WebServer
```

일련 번호를 사용 하 여 인증서를 갱신 하려면:

```
certreq –enroll -machine –cert 61 2d 3c fe 00 00 00 00 00 05 renew
```

유효한 인증서만 갱신할 수 있습니다. 만료 된 인증서는 갱신할 수 없으며 새 인증서로 바꾸어야 합니다.

## <a name="options"></a>옵션

| 옵션 | 설명 |
| ------- | ----------- |
| -모든 | `Force ICertRequest::Submit`인코딩 유형을 결정 합니다.|
| -attrib`<attributestring>` | 콜론으로 구분 된 **이름** 및 **값** 문자열 쌍을 지정 합니다.<p>을 사용 하 **Value** 여 `\n` **이름** 및 값 문자열 쌍을 구분 합니다 (예: Name1: value1\nName2: value2). |
| -이진 | 형식 대신 base64 인코딩된 이진 파일을 출력합니다. |
| -policyserver`<policyserver>` | ldap`<path>`<br>인증서 등록 정책 웹 서비스를 실행 하는 컴퓨터에 대 한 URI 또는 고유 ID를 삽입 합니다.<p>요청 파일을 이동 하 여 사용 하려는 지정 하려면 삼아 빼기 (-) 기호에 대 한 `<policyserver>`합니다. |
| -config`<ConfigString>` | 구성 문자열에 지정 된 CA를 사용 하 여 작업을 처리 합니다. 여기서는 **Cahostname\caname**입니다. Https:\\\ 연결의 경우 등록 서버 URI를 지정 합니다. 로컬 컴퓨터에 대 한 CA를 저장, 빼기를 사용 하 여 기호 (-). |
| -익명 | 인증서 등록 웹 서비스에 익명 자격 증명을 사용 합니다. |
| -kerberos | 인증서 등록 웹 서비스에 Kerberos (도메인) 자격 증명을 사용 합니다. |
| -clientcertificate`<ClientCertId>` | 을 인증서 지문, `<ClientCertId>` CN, EKU, template, EMAIL, UPN 또는 새 `name=value` 구문으로 바꿀 수 있습니다. |
| -username`<username>` | 인증서 등록 웹 서비스와 함께 사용 됩니다. SAM 이름 또는 `<username>` **도메인 \ 사용자** 값으로 대체할 수 있습니다. 이 옵션은 `-p` 옵션과 함께 사용할 수 있습니다. |
| -p `<password>` | 인증서 등록 웹 서비스와 함께 사용 됩니다. 대체 `<password>` 실제 사용자의 암호를 사용 합니다. 이 옵션은 `-username` 옵션과 함께 사용할 수 있습니다. |
| -사용자 | 새 인증서 `-user` 요청에 대 한 컨텍스트를 구성 하거나 인증서 동의의 컨텍스트를 지정 합니다. INF 또는 서식 파일에 지정 되지 않은 경우 기본 컨텍스트에입니다. |
| -컴퓨터 | 새 인증서 요청을 구성 하거나 컨텍스트를 지정 된 컴퓨터 컨텍스트에 대 한 인증서를 허용 합니다. 새 요청에 대 한 템플릿 컨텍스트와 MachineKeyset INF 키와 일치 이어야 합니다. 이 옵션을 지정 하지 않으면 템플릿에 컨텍스트를 설정 하지 않는 경우 기본값은 사용자 컨텍스트입니다. |
| -crl | 출력의 Crl (인증서 해지 목록)을에 지정 된 b a s e 64로 인코딩된 PKCS `certchainfileout` #7 파일 또는에 지정 된 b a s `requestfileout`e 64로 인코딩된 파일에 포함 합니다. |
| -rpc | Active Directory 인증서 서비스 (AD CS) 분산 COM. 대신 원격 프로시저 호출 (RPC) 서버 연결을 사용 하도록 지시 합니다. |
| -adminforcemachine | 키 서비스 또는 가장을 사용 하 여 로컬 시스템 컨텍스트에서 요청을 제출 합니다. 이 옵션을 호출 하는 사용자의 로컬 관리자 구성원 되도록 요구 합니다. |
| -renewonbehalfof | 서명 인증서에 식별 된 주체를 대신 하 여 갱신을 제출 합니다. 이 집합은 [ICertRequest:: Submit 메서드를](https://docs.microsoft.com/windows/win32/api/certcli/nf-certcli-icertrequest-submit) 호출할 때 CR_IN_ROBO 설정 됩니다. |
| -f | 기존 파일을 덮어쓰도록 강제 합니다. 캐싱 템플릿 및 정책에도 무시합니다. |
| -Q | 자동 모드를 사용 합니다. 모든 대화형 프롬프트를 표시 합니다. |
| -유니코드 | 표준 출력이 리디렉션되는 경우 또는 Windows PowerShell 스크립트에서 호출 되는 경우 도움이 되는 다른 명령으로 파이프 될 때 유니코드 출력을 씁니다. |
| -unicodetext | 파일에 데이터 blob 인코딩된 base64 텍스트를 작성 하는 경우 유니코드 출력을 보냅니다. |

## <a name="formats"></a>형식

| 형식 | 설명 |
| ------- | ----------- |
| requestfilein | Base64 인코딩 또는 이진 입력된 파일 이름: PKCS #10 인증서 요청, CMS 인증서 요청, PKCS #7 인증서 갱신 요청, 상호 인증에 X.509 인증서 또는 KeyGen 태그 형식 인증서 요청 합니다. |
| requestfileout | B a s e 64로 인코딩된 출력 파일 이름입니다. |
| certfileout | Base64 인코딩된 X-509 파일 이름입니다. |
| PKCS10fileout | `certreq -policy` 매개 변수와 함께 사용 합니다. Base64 인코딩된 PKCS10 출력 파일 이름입니다. |
| requestfileout | Base 64 인코딩 PKCS #7 파일 이름입니다. |
| fullresponsefileout | Base64 인코딩된 전체 응답 파일 이름입니다. |
| policyfilein | `certreq -policy` 매개 변수와 함께 사용 합니다. 요청을 한 정하는 데 사용 되는 확장의 텍스트 표현을 포함 하는 INF 파일입니다. |

## <a name="additional-resources"></a>추가 리소스

다음 문서 certreq 사용의 예를 들어:

- [보안 LDAP 인증서에 주체 대체 이름을 추가 하는 방법](https://support.microsoft.com/help/931351/how-to-add-a-subject-alternative-name-to-a-secure-ldap-certificate)

- [Test Lab Guide: Deploying an AD CS Two-Tier PKI Hierarchy](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831348(v=ws.11))

- [부록 3: Certreq.exe 구문](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc736326(v=ws.10))

- [웹 서버 SSL 인증서를 수동으로 만드는 방법](https://techcommunity.microsoft.com/t5/core-infrastructure-and-security/how-to-create-a-web-server-ssl-certificate-manually/ba-p/1128529)

- [AMT 프로 비전 Windows Server 2008 CA를 사용 하 여 인증서 요청](https://social.technet.microsoft.com/wiki/contents/articles/548.request-an-amt-provisioning-certificate-using-a-windows-server-2008-ca.aspx)

- [System Center Operations Manager 에이전트에 대 한 인증서 등록](https://social.technet.microsoft.com/wiki/contents/articles/2017.certificate-enrollment-for-system-center-operations-manager-agent.aspx)

- [AD CS 단계별 가이드: 2 계층 PKI 계층 배포](https://social.technet.microsoft.com/wiki/contents/articles/15037.ad-cs-step-by-step-guide-two-tier-pki-hierarchy-deployment.aspx)

- [타사 인증 기관에 SSL을 통해 LDAP를 사용 하는 방법](https://support.microsoft.com/help/321051/how-to-enable-ldap-over-ssl-with-a-third-party-certification-authority)
