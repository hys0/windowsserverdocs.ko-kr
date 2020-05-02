---
title: certutil
description: Certutil 명령에 대 한 참조 항목-CA (인증 기관) 구성 정보를 덤프 하 고 표시 하 고, 인증서 서비스를 구성 하 고, CA 구성 요소를 백업 및 복원 하 고, 인증서, 키 쌍 및 인증서 체인을 확인 하는 명령줄 프로그램입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c264ccf0-ba1e-412b-9dd3-d77dd9345ad9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3848c5493247e7e2d5e5b57be6d5d6e4015708b4
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716239"
---
# <a name="certutil"></a>certutil

Certutil은 인증서 서비스의 일부로 설치 되는 명령줄 프로그램입니다. Certutil을 사용 하 여 CA (인증 기관) 구성 정보를 덤프 및 표시 하 고, 인증서 서비스를 구성 하 고, CA 구성 요소를 백업 및 복원 하 고, 인증서, 키 쌍 및 인증서 체인을 확인할 수 있습니다.

Certutil이 추가 매개 변수 없이 인증 기관에서 실행 되 면 현재 인증 기관 구성이 표시 됩니다. Certutil이 인증 되지 않은 기관에서 실행 되는 경우 명령은 기본적으로 `certutil [-dump]` 명령을 실행 합니다.

> [!IMPORTANT]
> 이전 버전의 certutil이이 문서에서 설명 하는 옵션을 모두를 제공할 수 있습니다. 또는 `certutil -?` `certutil <parameter> -?`를 실행 하 여 특정 버전의 certutil에서 제공 하는 모든 옵션을 볼 수 있습니다.

## <a name="parameters"></a>매개 변수

### <a name="-dump"></a>-덤프

구성 정보 또는 파일을 덤프 합니다.

```
certutil [options] [-dump]
certutil [options] [-dump] file
```

```
[-f] [-silent] [-split] [-p password] [-t timeout]
```

### <a name="-asn"></a>-asn

ASN 파일의 구문을 분석 합니다.

```
certutil [options] -asn file [type]
```

`[type]`: numeric CRYPT_STRING_ * 디코딩 형식

### <a name="-decodehex"></a>-decodehex

16 진수로 인코딩된 파일을 디코딩합니다.

```
certutil [options] -decodehex infile outfile [type]
```

`[type]`: numeric CRYPT_STRING_ * encoding 형식

```
[-f]
```

### <a name="-decode"></a>-디코딩

B a s e 64로 인코딩된 파일을 디코딩합니다.

```
certutil [options] -decode infile outfile
```

```
[-f]
```

### <a name="-encode"></a>-인코딩

파일을 Base64로 인코딩합니다.

```
certutil [options] -encode infile outfile
```

```
[-f] [-unicodetext]
```

### <a name="-deny"></a>-거부

보류 중인 요청을 거부 합니다.

```
certutil [options] -deny requestID
```

```
[-config Machine\CAName]
```

### <a name="-resubmit"></a>-다시 전송

보류 중인 요청을 다시 제출 합니다.

```
certutil [options] -resubmit requestId
```

```
[-config Machine\CAName]
```

### <a name="-setattributes"></a>-setattributes

보류 중인 인증서 요청에 대 한 특성을 설정 합니다.

```
certutil [options] -setattributes RequestID attributestring
```

위치:

- **requestID** 는 보류 중인 요청에 대 한 숫자 요청 ID입니다.

- **attributestring** 는 요청 특성 이름 및 값 쌍입니다.

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>설명

- 이름 및 값은 콜론으로 구분 해야 하지만 여러 이름, 값 쌍은 줄 바꿈으로 구분 해야 합니다. 예: `CertificateTemplate:User\nEMail:User@Domain.com` 시퀀스는 `\n` 줄 바꿈 구분 기호로 변환 됩니다.

### <a name="-setextension"></a>-setextension

보류 중인 인증서 요청에 대 한 확장을 설정 합니다.

```
certutil [options] -setextension requestID extensionname flags {long | date | string | \@infile}
```

위치:

- **requestID** 는 보류 중인 요청에 대 한 숫자 요청 ID입니다.

- **extensionname** 는 확장에 대 한 ObjectId 문자열입니다.

- **플래그** 는 확장의 우선 순위를 설정 합니다. `0`를 사용 하는 `1` 것이 좋지만,는 확장 `2` 을 위험으로 설정 하 `3` 고 확장을 사용 하지 않도록 설정 하며 둘 다 수행 합니다.

```
[-config Machine\CAName]
```

#### <a name="remarks"></a>설명

- 마지막 매개 변수가 숫자인 경우 **Long**으로 간주 됩니다.

- 마지막 매개 변수를 날짜로 구문 분석할 수 있는 경우 **날짜로**사용 됩니다.

- 마지막 매개 변수가로 `\@`시작 하는 경우 토큰의 나머지 부분은 이진 데이터 또는 ascii 텍스트 hex 덤프를 사용 하는 파일 이름으로 사용 됩니다.

- 마지막 매개 변수가 다른 값 이면 문자열로 간주 됩니다.

### <a name="-revoke"></a>-취소

인증서를 해지 합니다.

```
certutil [options] -revoke serialnumber [reason]
```

위치:

- **일련** 번호는 해지할 인증서 일련 번호의 쉼표로 구분 된 목록입니다.

- **이유** 는 다음과 같은 해지 이유에 대 한 숫자 또는 기호 표현입니다.

  - **0. CRL_REASON_UNSPECIFIED** -지정 되지 않음 (기본값)

  - **1. CRL_REASON_KEY_COMPROMISE** 키 손상

  - **2. CRL_REASON_CA_COMPROMISE** -인증 기관 손상

  - **3. CRL_REASON_AFFILIATION_CHANGED** -정보 변경 됨

  - **4. CRL_REASON_SUPERSEDED** -대체 됨

  - **5. CRL_REASON_CESSATION_OF_OPERATION** -해시 중단 작업

  - **6. CRL_REASON_CERTIFICATE_HOLD** -인증서 보류

  - **8. CRL_REASON_REMOVE_FROM_CRL** -CRL에서 제거

  - **1. 해지** 취소-해지 취소

```
[-config Machine\CAName]
```

### <a name="-isvalid"></a>-isvalid

현재 인증서의 처리를 표시 합니다.

```
certutil [options] -isvalid serialnumber | certhash
```

```
[-config Machine\CAName]
```

### <a name="-getconfig"></a>-getconfig

기본 구성 문자열을 가져옵니다.

```
certutil [options] -getconfig
```

```
[-config Machine\CAName]
```

### <a name="-ping"></a>-ping

Active Directory 인증서 서비스 요청 인터페이스에 연결 하려고 합니다.

```
certutil [options] -ping [maxsecondstowait | camachinelist]
```

위치:

- **camachinelist** 은 쉼표로 구분 된 CA 컴퓨터 이름 목록입니다. 단일 컴퓨터의 경우 종료 쉼표를 사용 합니다. 또한이 옵션은 각 CA 컴퓨터에 대 한 사이트 비용을 표시 합니다.

```
[-config Machine\CAName]
```

### <a name="-cainfo"></a>-cainfo

인증 기관에 대 한 정보를 표시 합니다.

```
certutil [options] -cainfo [infoname [index | errorcode]]
```

위치:

- **infoname** 는 다음 infoname 인수 구문을 기반으로 표시할 CA 속성을 나타냅니다.

  - **파일** -파일 버전
  
  - **제품** 버전
  
  - **exitcount** -끝내기 모듈 수
  
  - **끝내기 `[index]` ** 모듈 설명
  
  - **정책** -정책 모듈 설명
  
  - **이름** -CA 이름
  
  - **sanitizedname** -삭제 CA 이름
  
  - **dsname** -삭제 한 CA 약식 이름 (DS 이름)
  
  - **sharedfolder** -공유 폴더
  
  - **Error1 ErrorCode** -오류 메시지 텍스트
  
  - **Error2 ErrorCode** -오류 메시지 텍스트 및 오류 코드
  
  - **유형** -CA 유형
  
  - **info** -CA 정보
  
  - **부모** -부모 CA
  
  - **certcount** -CA 인증서 수
  
  - **xchgcount** -CA exchange 인증서 수
  
  - **kracount** -KRA 인증서 수
  
  - **kraused** -KRA 인증서 사용 횟수
  
  - **propidmax** -최대 CA PropId
  
  - **certstate `[index]` ** -CA 인증서
  
  - **certversion `[index]` ** -CA 인증서 버전
  
  - **certstatuscode `[index]` ** -CA 인증서 확인 상태
  
  - **crlstate `[index]` ** -CRL
  
  - **krastate `[index]` ** -KRA 인증서
  
  - 상호 **상태 + `[index]` ** -크로스 인증서 전달
  
  - 상호 **상태- `[index]` ** -역방향 상호 인증서
  
  - **인증서 `[index]` ** -CA 인증서
  
  - **certchain `[index]` ** -CA 인증서 체인
  
  - **certcrlchain `[index]` ** -crl을 사용 하는 CA 인증서 체인
  
  - **xchg `[index]` ** -CA exchange 인증서
  
  - **xchgchain `[index]` ** -CA exchange 인증서 체인

  - **xchgcrlchain `[index]` ** -crl을 사용 하는 CA 교환 인증서 체인
  
  - **kra `[index]` ** -kra 인증서
  
  - 크로스-전방 교차 인증서 ** `[index]` **
  
  - 크로스-역방향 인증서 ** `[index]` **
  
  - **Crl `[index]` ** 기반 crl
  
  - **deltacrl `[index]` ** -델타 CRL
  
  - **crlstatus `[index]` ** -CRL 게시 상태
  
  - **deltacrlstatus `[index]` ** -델타 CRL 게시 상태
  
  - **dns** -dns 이름
  
  - **역할** -역할 구분
  
  - **광고** -고급 서버
  
  - **템플릿** -템플릿
  
  - **csp `[index]` ** -OCSP url
  
  - **aia `[index]` ** -aia url
  
  - **cdp `[index]` ** -cdp url
  
  - **localename** -CA 로캘 이름
  
  - 제목 템플릿 **oid** -주제 템플릿 oid
  
  - **&#42;** -모든 속성을 표시 합니다.

- **index** 는 선택적으로 0부터 시작 하는 속성 인덱스입니다.

- **errorcode** 는 숫자 오류 코드입니다.

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cacert"></a>-ca.cert

인증 기관에 대 한 인증서를 검색 합니다.

```
certutil [options] -ca.cert outcacertfile [index]
```

위치:

- **outcacertfile** 는 출력 파일입니다.

- **index** 는 CA 인증서 갱신 인덱스 이며 기본값은 가장 최근 항목입니다.

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-cachain"></a>-ca.chain

인증 기관에 대 한 인증서 체인을 검색 합니다.

```
certutil [options] -ca.chain outcacertchainfile [index]
```

위치:

- **outcacertchainfile** 는 출력 파일입니다.

- **index** 는 CA 인증서 갱신 인덱스 이며 기본값은 가장 최근 항목입니다.

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-getcrl"></a>-getcrl

CRL (인증서 해지 목록)을 가져옵니다.

certutil [옵션]-getcrl 출력 이름 [인덱스] [델타]

위치:

- **index** 는 crl 인덱스 또는 키 인덱스입니다. 기본값은 가장 최근 키의 경우 crl입니다.

- **델타** crl (기본값은 기본 crl)입니다.

```
[-f] [-split] [-config Machine\CAName]
```

### <a name="-crl"></a>-crl

새 Crl (인증서 해지 목록) 또는 델타 Crl을 게시 합니다.

```
certutil [options] -crl [dd:hh | republish] [delta]
```

위치:

- **dd: hh** 는 새 CRL 유효 기간 (일 및 시간)입니다.

- 다시 **게시** 최신 crl을 다시 게시 합니다.

- **델타** crl만 델타 crl을 게시 합니다 (기본값은 기본 및 델타 crl).

```
[-split] [-config Machine\CAName]
```

### <a name="-shutdown"></a>-종료

Active Directory 인증서 서비스를 종료 합니다.

```
certutil [options] -shutdown
```

```
[-config Machine\CAName]
```

### <a name="-installcert"></a>-installcert

인증 기관 인증서를 설치 합니다.

```
certutil [options] -installcert [cacertfile]
```

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-renewcert"></a>-renewcert

인증 기관 인증서를 갱신 합니다.

```
certutil [options] -renewcert [reusekeys] [Machine\ParentCAName]
```

- 을 `-f` 사용 하 여 미해결 갱신 요청을 무시 하 고 새 요청을 생성 합니다.

```
[-f] [-silent] [-config Machine\CAName]
```

### <a name="-schema"></a>-스키마

인증서에 대 한 스키마를 덤프 합니다.

```
certutil [options] -schema [ext | attrib | cRL]
```
위치:

- 이 명령은 기본적으로 요청 및 인증서 테이블로 설정 됩니다.

- **ext** 는 확장 테이블입니다.
  
- **특성은 특성** 테이블입니다.

- **crl은 crl** 테이블입니다.

```
[-split] [-config Machine\CAName]
```

### <a name="-view"></a>-보기

인증서 뷰를 덤프 합니다.

```
certutil [options] -view [queue | log | logfail | revoked | ext | attrib | crl] [csv]
```

위치:

- **큐** 는 특정 요청 큐를 덤프 합니다.

- **로그** 는 발급 되거나 해지 된 인증서와 실패 한 모든 요청을 덤프 합니다.

- **logfail** 은 실패 한 요청을 덤프 합니다.

- **해지 된 인증서를 덤프 합니다** .

- **ext** 는 확장 테이블을 덤프 합니다.
  
- **특성은** 특성 테이블을 덤프 합니다.

- **crl이** crl 테이블을 덤프 합니다.

- **csv** 는 쉼표로 구분 된 값을 사용 하 여 출력을 제공 합니다.

```
[-silent] [-split] [-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

#### <a name="remarks"></a>설명

- 모든 항목에 대해 **StatusCode** 열을 표시 하려면 다음을 입력 합니다.`-out StatusCode`

- 마지막 항목에 대 한 모든 열을 표시 하려면 다음을 입력 합니다.`-restrict RequestId==$`

- 3 개 요청에 대 한 **RequestID** 및 **처리** 를 표시 하려면 다음을 입력 합니다.`-restrict requestID>37,requestID<40 -out requestID,disposition`

- 모든 기본 Crl의 행 id**행 id** 와 **CRL 번호** 를 표시 하려면 다음을 입력 합니다.`-restrict crlminbase=0 -out crlrowID,crlnumber crl`

- 표시 하려면 다음을 입력 합니다.`-v -restrict crlminbase=0,crlnumber=3 -out crlrawcrl crl`

- 전체 CRL 테이블을 표시 하려면 다음을 입력 합니다.`CRL`

- 날짜 `Date[+|-dd:hh]` 제한에 사용 합니다.

- 현재 `now+dd:hh` 시간을 기준으로 하는 날짜에 사용 합니다.

### <a name="-db"></a>-db

원시 데이터베이스를 덤프 합니다.

```
certutil [options] -db
```

```
[-config Machine\CAName] [-restrict RestrictionList] [-out ColumnList]
```

### <a name="-deleterow"></a>-deleterow

서버 데이터베이스에서 행을 삭제 합니다.

```
certutil [options] -deleterow rowID | date [request | cert | ext | attrib | crl]
```

위치:

- **요청** 은 제출 날짜를 기준으로 실패 한 요청 및 보류 중인 요청을 삭제 합니다.

- **인증서** 만료 날짜를 기준으로 만료 되 고 해지 된 인증서를 삭제 합니다.

- **ext** 확장 테이블을 삭제 합니다.
  
- **특성** 은 특성 테이블을 삭제 합니다.

- **crl이** crl 테이블을 삭제 합니다.

```
[-f] [-config Machine\CAName]
```

#### <a name="examples"></a>예

- 2001 년 1 월 22 일에 제출 된 실패 한 요청 및 보류 중인 요청을 삭제 하려면 다음을 입력 합니다.`1/22/2001 request`

- 2001 년 1 월 22 일에 만료 된 모든 인증서를 삭제 하려면 다음을 입력 합니다.`1/22/2001 cert`

- RequestID 37에 대 한 인증서 행, 특성 및 확장을 삭제 하려면 다음을 입력 합니다.`37`

- 2001 년 1 월 22 일에 만료 된 Crl을 삭제 하려면 다음을 입력 합니다.`1/22/2001 crl`

### <a name="-backup"></a>-backup

Active Directory 인증서 서비스를 백업 합니다.

```
certutil [options] -backup backupdirectory [incremental] [keeplog]
```

위치:

- 백업 데이터를 저장할 **디렉터리입니다.**

- **증분** 은 증분 백업만 수행 합니다 (기본값은 전체 백업).

- **keeplog** 는 데이터베이스 로그 파일을 유지 합니다 (기본값은 로그 파일 자르기).

```
[-f] [-config Machine\CAName] [-p Password]
```

### <a name="-backupdb"></a>-backupdb

Active Directory 인증서 서비스 데이터베이스를 백업 합니다.

```
certutil [options] -backupdb backupdirectory [incremental] [keeplog]
```

위치:

- 백업 디렉터리는 백업 된 데이터베이스 파일을 저장 하는 **디렉터리입니다.**

- **증분** 은 증분 백업만 수행 합니다 (기본값은 전체 백업).

- **keeplog** 는 데이터베이스 로그 파일을 유지 합니다 (기본값은 로그 파일 자르기).

```
[-f] [-config Machine\CAName]
```

### <a name="-backupkey"></a>-backupkey

Active Directory 인증서 서비스 인증서와 개인 키를 백업 합니다.

```
certutil [options] -backupkey backupdirectory
```

위치:

- 백업 디렉터리는 백업 된 PFX 파일을 저장 하는 **디렉터리입니다.**

```
[-f] [-config Machine\CAName] [-p password] [-t timeout]
```

### <a name="-restore"></a>-restore

Active Directory 인증서 서비스를 복원 합니다.

```
certutil [options] -restore backupdirectory
```

위치:

- **백업** 디렉터리는 복원할 데이터를 포함 하는 디렉터리입니다.

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-restoredb"></a>-restoredb

Active Directory 인증서 서비스 데이터베이스를 복원 합니다.

```
certutil [options] -restoredb backupdirectory
```

위치:

- **백업** 디렉터리는 복원할 데이터베이스 파일이 들어 있는 디렉터리입니다.

```
[-f] [-config Machine\CAName]
```

### <a name="-restorekey"></a>-restorekey

Active Directory 인증서 서비스 인증서와 개인 키를 복원 합니다.

```
certutil [options] -restorekey backupdirectory | pfxfile
```

위치:

- **백업** 디렉터리는 복원할 PFX 파일을 포함 하는 디렉터리입니다.

```
[-f] [-config Machine\CAName] [-p password]
```

### <a name="-importpfx"></a>-importpfx

인증서 및 개인 키를 가져옵니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

```
certutil [options] -importpfx [certificatestorename] pfxfile [modifiers]
```

위치:

- **certificatestorename** 은 인증서 저장소의 이름입니다.

- **한정자** 는 쉼표로 구분 된 목록으로, 다음 중 하나 이상을 포함할 수 있습니다.

  1. **AT_SIGNATURE** -keyspec을 서명으로 변경 합니다.
  
  2. **AT_KEYEXCHANGE** -keyspec을 키 교환으로 변경 합니다.
  
  3. **Noexport** -개인 키를 내보낼 수 없게 만듭니다.
  
  4. **Nocert** -인증서를 가져오지 않음
  
  5. **Nochain** -인증서 체인을 가져오지 않음
  
  6. **NoRoot** -루트 인증서를 가져오지 않음
  
  7. **보호** -암호를 사용 하 여 키를 보호 합니다.
  
  8. **Noprotect** -암호를 사용 하 여 키를 보호 하지 않음

```
[-f] [-user] [-p password] [-csp provider]
```

#### <a name="remarks"></a>설명

- 기본값은 개인 컴퓨터 저장소입니다.

### <a name="-dynamicfilelist"></a>-dynamicfilelist

동적 파일 목록을 표시 합니다.

```
certutil [options] -dynamicfilelist
```

```
[-config Machine\CAName]
```

### <a name="-databaselocations"></a>-databaselocations

데이터베이스 위치를 표시 합니다.

```
certutil [options] -databaselocations
```

```
[-config Machine\CAName]
```

### <a name="-hashfile"></a>-hashfile

파일에 대 한 암호화 해시를 생성 하 고 표시 합니다.

```
certutil [options] -hashfile infile [hashalgorithm]
```

### <a name="-store"></a>-저장

인증서 저장소를 덤프 합니다.

```
certutil [options] -store [certificatestorename [certID [outputfile]]]
```

위치:

- **certificatestorename** 은 인증서 저장소 이름입니다. 다음은 그 예입니다. 

  - `My, CA (default), Root,`
  
  - `ldap:///CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?one?objectClass=certificationAuthority (View Root Certificates)`
  
  - `ldap:///CN=CAName,CN=Certification Authorities,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Modify Root Certificates)`
  
  - `ldap:///CN=CAName,CN=MachineName,CN=CDP,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?certificateRevocationList?base?objectClass=cRLDistributionPoint (View CRLs)`
  
  - `ldap:///CN=NTAuthCertificates,CN=Public Key Services,CN=Services,CN=Configuration,DC=cpandl,DC=com?cACertificate?base?objectClass=certificationAuthority (Enterprise CA Certificates)`
  
  - `ldap: (AD computer object certificates)`
  
  - `-user ldap: (AD user object certificates)`

- **인증서** 는 인증서 또는 CRL 일치 토큰입니다. 숫자 CTL 인덱스 (. 0, 1, 등), 숫자 CRL 인덱스 (. 0, 1 등), 숫자 CTL 인덱스 (. 0, 1, 등), 숫자 CTL 인덱스 (.. 0,. 1 등), 공개 키, 서명 또는 확장명 ObjectId, 인증서 주체 일반 이름, 전자 메일 주소, UPN 또는 DNS 이름, 키 컨테이너 이름 또는 CSP 이름, 템플릿 이름 또는 ObjectId, EKU 또는 응용 프로그램 정책 ObjectId 또는 CRL 발급자 일반 이름입니다. 이러한 대부분의 여러 일치 항목이 될 수 있습니다.

- **outputfile** 은 일치 하는 인증서를 저장 하는 데 사용 되는 파일입니다.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-silent] [-split] [-dc DCName]
```

#### <a name="options"></a>옵션

- 옵션 `-user` 은 컴퓨터 저장소 대신 사용자 저장소에 액세스 합니다.

- 옵션 `-enterprise` 은 컴퓨터 엔터프라이즈 저장소에 액세스 합니다.

- 옵션 `-service` 은 컴퓨터 서비스 저장소에 액세스 합니다.

- 옵션 `-grouppolicy` 은 컴퓨터 그룹 정책 저장소에 액세스 합니다.

다음은 그 예입니다. 

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-addstore"></a>-addstore

저장소에 인증서를 추가합니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

```
certutil [options] -addstore certificatestorename infile
```

위치:

- **certificatestorename** 은 인증서 저장소 이름입니다.

- **infile** 은 저장소에 추가 하려는 인증서 또는 CRL 파일입니다.

```
[-f] [-user] [-enterprise] [-grouppolicy] [-dc DCName]
```

### <a name="-delstore"></a>-delstore

저장소에서 인증서를 삭제합니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

```
certutil [options] -delstore certificatestorename certID
```

위치:

- **certificatestorename** 은 인증서 저장소 이름입니다.

- **인증서** 는 인증서 또는 CRL 일치 토큰입니다.

```
[-enterprise] [-user] [-grouppolicy] [-dc DCName]
```

### <a name="-verifystore"></a>-verifystore

저장소에서 인증서를 확인 합니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

```
certutil [options] -verifystore certificatestorename [certID]
```

위치:

- **certificatestorename** 은 인증서 저장소 이름입니다.

- **인증서** 는 인증서 또는 CRL 일치 토큰입니다.

```
[-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-dc DCName] [-t timeout]
```

### <a name="-repairstore"></a>-repairstore

키 연결을 복구 하거나 인증서 속성 또는 키 보안 설명자를 업데이트 합니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

```
certutil [options] -repairstore certificatestorename certIDlist [propertyinffile | SDDLsecuritydescriptor]
```

위치:

- **certificatestorename** 은 인증서 저장소 이름입니다.

- **certIDlist** 은 쉼표로 구분 된 인증서 또는 CRL 일치 토큰 목록입니다. 자세한 내용은이 문서에서 설명 `-store certID` 하는 설명을 참조 하세요.

- **propertyinffile** 은 다음을 비롯 한 외부 속성을 포함 하는 INF 파일입니다.

  ```
  [Properties]
      19 = Empty ; Add archived property, OR:
      19 =       ; Remove archived property

      11 = {text}Friendly Name ; Add friendly name property

      127 = {hex} ; Add custom hexadecimal property
          _continue_ = 00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
          _continue_ = 10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f

      2 = {text} ; Add Key Provider Information property
        _continue_ = Container=Container Name&
        _continue_ = Provider=Microsoft Strong Cryptographic Provider&
        _continue_ = ProviderType=1&
        _continue_ = Flags=0&
        _continue_ = KeySpec=2

      9 = {text} ; Add Enhanced Key Usage property
        _continue_ = 1.3.6.1.5.5.7.3.2,
        _continue_ = 1.3.6.1.5.5.7.3.1,
  ```

```
[-f] [-enterprise] [-user] [-grouppolicy] [-silent] [-split] [-csp provider]
```

### <a name="-viewstore"></a>-뷰 저장소

인증서 저장소를 덤프 합니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

```
certutil [options] -viewstore [certificatestorename [certID [outputfile]]]
```

위치:

- **certificatestorename** 은 인증서 저장소 이름입니다.

- **인증서** 는 인증서 또는 CRL 일치 토큰입니다.

- **outputfile** 은 일치 하는 인증서를 저장 하는 데 사용 되는 파일입니다.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>옵션

- 옵션 `-user` 은 컴퓨터 저장소 대신 사용자 저장소에 액세스 합니다.

- 옵션 `-enterprise` 은 컴퓨터 엔터프라이즈 저장소에 액세스 합니다.

- 옵션 `-service` 은 컴퓨터 서비스 저장소에 액세스 합니다.

- 옵션 `-grouppolicy` 은 컴퓨터 그룹 정책 저장소에 액세스 합니다.

다음은 그 예입니다. 

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-viewdelstore"></a>-viewdelstore

저장소에서 인증서를 삭제합니다.

```
certutil [options] -viewdelstore [certificatestorename [certID [outputfile]]]
```

위치:

- **certificatestorename** 은 인증서 저장소 이름입니다.

- **인증서** 는 인증서 또는 CRL 일치 토큰입니다.

- **outputfile** 은 일치 하는 인증서를 저장 하는 데 사용 되는 파일입니다.

```
[-f] [-user] [-enterprise] [-service] [-grouppolicy] [-dc DCName]
```

#### <a name="options"></a>옵션

- 옵션 `-user` 은 컴퓨터 저장소 대신 사용자 저장소에 액세스 합니다.

- 옵션 `-enterprise` 은 컴퓨터 엔터프라이즈 저장소에 액세스 합니다.

- 옵션 `-service` 은 컴퓨터 서비스 저장소에 액세스 합니다.

- 옵션 `-grouppolicy` 은 컴퓨터 그룹 정책 저장소에 액세스 합니다.

다음은 그 예입니다. 

- `-enterprise NTAuth`

- `-enterprise Root 37`

- `-user My 26e0aaaf000000000004`

- `CA .11`

### <a name="-dspublish"></a>-dspublish

Active Directory에 인증서 또는 CRL (인증서 해지 목록)을 게시 합니다.

```
certutil [options] -dspublish certfile [NTAuthCA | RootCA | SubCA | CrossCA | KRA | User | Machine]
```

```
certutil [options] -dspublish CRLfile [DSCDPContainer [DSCDPCN]]
```

위치:

- **certfile** 은 게시할 인증서 파일의 이름입니다.

- **NTAuthCA** 는 인증서를 DS 엔터프라이즈 저장소에 게시 합니다.

- **Rootca.cer** 는 인증서를 DS의 신뢰할 수 있는 루트 저장소에 게시 합니다.

- **Subca** 는 ca 인증서를 DS ca 개체에 게시 합니다.

- **CrossCA** 는 DS CA 개체에 교차 인증서를 게시 합니다.

- **KRA** 에서 인증서를 DS 키 복구 에이전트 개체에 게시 합니다.

- 사용자가 인증서를 사용자 DS 개체 **에 게시 합니다** .

- **컴퓨터에서** 인증서를 컴퓨터 DS 개체에 게시 합니다.

- **CRLfile** 은 게시할 CRL 파일의 이름입니다.

- **Dscdpcontainer** 는 DS CDP 컨테이너 CN (일반적으로 CA 컴퓨터 이름)입니다.

- **DSCDPCN** 는 일반적으로 삭제 된 CA 약식 이름과 키 인덱스를 기반으로 하는 DS CDP 개체 CN입니다.

- 를 `-f` 사용 하 여 새 DS 개체를 만듭니다.

```
[-f] [-user] [-dc DCName]
```

### <a name="-adtemplate"></a>-adtemplate

Active Directory 템플릿을 표시 합니다.

```
certutil [options] -adtemplate [template]
```

```
[-f] [-user] [-ut] [-mt] [-dc DCName]
```

### <a name="-template"></a>-template

인증서 템플릿을 표시 합니다.

```
certutil [options] -template [template]
```

```
[-f] [-user] [-silent] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-templatecas"></a>-templatecas

인증서 템플릿에 대 한 Ca (인증 기관)를 표시 합니다.

```
certutil [options] -templatecas template
```

```
[-f] [-user] [-dc DCName]
```

### <a name="-catemplates"></a>-catemplates

인증 기관에 대 한 템플릿을 표시 합니다.

```
certutil [options] -catemplates [template]
```

```
[-f] [-user] [-ut] [-mt] [-config Machine\CAName] [-dc DCName]
```

### <a name="-setcasites"></a>-setcasites

인증 기관 사이트 이름 설정, 확인 및 삭제를 포함 하 여 사이트 이름을 관리 합니다.

```
certutil [options] -setcasites [set] [sitename]
certutil [options] -setcasites verify [sitename]
certutil [options] -setcasites delete
```

위치:

- **sitename** 은 단일 인증 기관을 대상으로 하는 경우에만 허용 됩니다.

```
[-f] [-config Machine\CAName] [-dc DCName]
```

#### <a name="remarks"></a>설명

- 옵션 `-config` 은 단일 인증 기관 (기본값은 모든 ca)을 대상으로 합니다.

- 옵션 `-f` 은 지정 된 **sitename** 의 유효성 검사 오류를 재정의 하거나 모든 CA sitenames을 삭제 하는 데 사용할 수 있습니다.

> [!NOTE]
> Active Directory Domain Services (AD DS) 사이트 인식에 대해 Ca를 구성 하는 방법에 대 한 자세한 내용은 [AD CS 및 PKI 클라이언트에 대 한 사이트 인식 AD DS](https://social.technet.microsoft.com/wiki/contents/articles/14106.ad-ds-site-awareness-for-ad-cs-and-pki-clients.aspx)을 참조 하십시오.

### <a name="-enrollmentserverurl"></a>-enrollmentserverURL

CA와 연결 된 등록 서버 Url을 표시, 추가 또는 삭제 합니다.

```
certutil [options] -enrollmentServerURL [URL authenticationtype [priority] [modifiers]]
certutil [options] -enrollmentserverURL URL delete
```

위치:

- **authenticationtype** 은 URL을 추가 하는 동안 다음 클라이언트 인증 방법 중 하나를 지정 합니다.

  1. **kerberos** -kerberos SSL 자격 증명을 사용 합니다.

  2. **사용자 이름** -SSL 자격 증명에 명명 된 계정을 사용 합니다.

  3. **clientcertificate**:-X.509 인증서 SSL 자격 증명을 사용 합니다.

  4. **익명** -익명 SSL 자격 증명을 사용 합니다.

- **DELETE** CA와 연결 된 지정 된 URL을 삭제 합니다.

- URL을 추가할 `1` 때 지정 되지 않은 경우 **우선 순위** 는로 설정 됩니다.

- **한정자** 는 쉼표로 구분 된 목록으로, 다음 중 하나 이상을 포함 합니다.

1. **allowrenewalsonly** -이 URL을 통해이 CA에 갱신 요청을 제출할 수 있습니다.

2. **allowkeybasedrenewal** -AD에 연결 된 계정이 없는 인증서를 사용할 수 있습니다. 이는 clientcertificate 및 allowrenewalsonly 모드에만 적용 됩니다.

```
[-config Machine\CAName] [-dc DCName]
```

### <a name="-adca"></a>-adca

Active Directory 인증 기관을 표시 합니다.

```
certutil [options] -adca [CAName]
```

```
[-f] [-split] [-dc DCName]
```

### <a name="-ca"></a>-ca

등록 정책 인증 기관을 표시 합니다.

```
certutil [options] -CA [CAName | templatename]
```

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policy"></a>-정책

등록 정책을 표시 합니다.

```
[-f] [-user] [-silent] [-split] [-policyserver URLorID] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-policycache"></a>-policycache

등록 정책 캐시 항목을 표시 하거나 삭제 합니다.

```
certutil [options] -policycache [delete]
```

위치:

- **delete** 는 정책 서버 캐시 항목을 삭제 합니다.

- **-f** 모든 캐시 항목을 삭제 합니다.

```
[-f] [-user] [-policyserver URLorID]
```

### <a name="-credstore"></a>-credstore

자격 증명 저장소 항목을 표시, 추가 또는 삭제 합니다.

```
certutil [options] -credstore [URL]
certutil [options] -credstore URL add
certutil [options] -credstore URL delete
```

위치:

- **Url** 은 대상 url입니다. 를 사용 `*` 하 여 모든 항목을 검색 하거나 `https://machine*` URL 접두사와 일치 시킬 수도 있습니다.

- **추가** 는 자격 증명 저장소 항목을 추가 합니다. 이 옵션을 사용 하려면 SSL 자격 증명도 사용 해야 합니다.

- **delete** 는 자격 증명 저장소 항목을 삭제 합니다.

- **-f** 단일 항목을 덮어쓰거나 여러 항목을 삭제 합니다.

```
[-f] [-user] [-silent] [-anonymous] [-kerberos] [-clientcertificate clientcertID] [-username username] [-p password]
```

### <a name="-installdefaulttemplates"></a>-installdefaulttemplates

기본 인증서 템플릿을 설치 합니다.

```
certutil [options] -installdefaulttemplates
```

```
[-dc DCName]
```

### <a name="-urlcache"></a>-URLcache

URL 캐시 항목을 표시 하거나 삭제 합니다.

```
certutil [options] -URLcache [URL | CRL | * [delete]]
```

위치:

- **Url** 은 캐시 된 url입니다.

- **Crl** 은 모든 캐시 된 crl url 에서만 실행 됩니다.

- **&#42;** 는 모든 캐시 된 url에 대해 작동 합니다.

- **delete** 는 현재 사용자의 로컬 캐시에서 관련 url을 삭제 합니다.

- **-f** 특정 URL을 페치 하 고 캐시를 업데이트 합니다.

```
[-f] [-split]
```

### <a name="-pulse"></a>-펄스

자동 등록 이벤트를 펄스 합니다.

```
certutil [options] -pulse
```

```
[-user]
```

### <a name="-machineinfo"></a>-machineinfo

Active Directory 컴퓨터 개체에 대 한 정보를 표시 합니다.

```
certutil [options] -machineinfo domainname\machinename$
```

### <a name="-dcinfo"></a>-DCInfo

도메인 컨트롤러에 대 한 정보를 표시 합니다. 기본은 확인 하지 않고 DC 인증서를 표시 합니다.

```
certutil [options] -DCInfo [domain] [verify | deletebad | deleteall]
```

```
[-f] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

> [!TIP]
> Active Directory Domain Services (AD DS) **도메인을 지정 하 고 도메인** 컨트롤러 (**-dc**)를 지정 하는 기능은 Windows Server 2012에 추가 되었습니다. 명령을 성공적으로 실행 하려면의 구성원 인 계정을 사용 해야 **Domain Admins** 또는 **Enterprise Admins**합니다. 이 명령의 동작 수정 작업은 다음과 같습니다.<ol><li>1. 도메인을 지정 하지 않은 경우 특정 도메인 컨트롤러를 지정 하지 않으면이 옵션은 기본 도메인 컨트롤러에서 처리할 도메인 컨트롤러의 목록을 반환 합니다.</li><li>2. 도메인을 지정 하지 않은 경우 도메인 컨트롤러가 지정 된 경우 지정 된 도메인 컨트롤러의 인증서에 대 한 보고서가 생성 됩니다.</li><li>3. 도메인이 지정 되었지만 도메인 컨트롤러가 지정 되지 않은 경우 목록에서 각 도메인 컨트롤러에 대 한 인증서에 대 한 보고서와 함께 도메인 컨트롤러 목록이 생성 됩니다.</li><li>4. 도메인 컨트롤러와 도메인 컨트롤러가 지정 된 경우 대상 도메인 컨트롤러에서 도메인 컨트롤러 목록이 생성 됩니다. 목록에서 각 도메인 컨트롤러에 대 한 인증서에 대 한 보고서도 생성 됩니다.</li></ol>
>
>예를 들어 CPANDL-d c 1 이라는 도메인 컨트롤러와 CPANDL 라는 도메인이 가정 합니다. 다음 명령을 실행 하 여 CPANDL-DC1에서 도메인 컨트롤러 및 해당 인증서의 목록을 검색할 수 있습니다.`certutil -dc cpandl-dc1 -DCInfo cpandl`

### <a name="-entinfo"></a>-entinfo

엔터프라이즈 인증 기관에 대 한 정보를 표시 합니다.

```
certutil [options] -entinfo domainname\machinename$
```

```
[-f] [-user]
```

### <a name="-tcainfo"></a>-tcainfo

인증 기관에 대 한 정보를 표시 합니다.

```
certutil [options] -tcainfo [domainDN | -]
```

```
[-f] [-enterprise] [-user] [-urlfetch] [-dc DCName] [-t timeout]
```

### <a name="-scinfo"></a>-scinfo

스마트 카드에 대 한 정보를 표시 합니다.

```
certutil [options] -scinfo [readername [CRYPT_DELETEKEYSET]]
```

위치:

- **CRYPT_DELETEKEYSET** 스마트 카드의 모든 키를 삭제 합니다.

```
[-silent] [-split] [-urlfetch] [-t timeout]
```

### <a name="-scroots"></a>-scroots

스마트 카드 루트 인증서를 관리 합니다.

```
certutil [options] -scroots update [+][inputrootfile] [readername]
certutil [options] -scroots save \@in\\outputrootfile [readername]
certutil [options] -scroots view [inputrootfile | readername]
certutil [options] -scroots delete [readername]
```

```
[-f] [-split] [-p Password]
```

### <a name="-verifykeys"></a>-verifykeys

공개 또는 개인 키 집합을 확인 합니다.

```
certutil [options] -verifykeys [keycontainername cacertfile]
```

위치:

- **cspparameters.keycontainername** 는 확인할 키의 키 컨테이너 이름입니다. 이 옵션은 기본적으로 컴퓨터 키로 설정 됩니다. 사용자 키로 전환 하려면를 사용 `-user`합니다.

- **cacertfile** 는 인증서 파일을 서명 하거나 암호화 합니다.

```
[-f] [-user] [-silent] [-config Machine\CAName]
```

#### <a name="remarks"></a>설명

- 인수를 지정 하지 않으면 각 서명 CA 인증서는 개인 키에 대해 확인 됩니다.

- 만 로컬 CA 또는 로컬 키에 대해이 작업을 수행할 수 있습니다.

### <a name="-verify"></a>-확인

인증서, CRL (인증서 해지 목록) 또는 인증서 체인을 확인 합니다.

```
certutil [options] -verify certfile [applicationpolicylist | - [issuancepolicylist]]
certutil [options] -verify certfile [cacertfile [crossedcacertfile]]
certutil [options] -verify CRLfile cacertfile [issuedcertfile]
certutil [options] -verify CRLfile cacertfile [deltaCRLfile]
```

위치:

- **certfile** 은 확인할 인증서의 이름입니다.

- **applicationpolicylist** 는 필수 응용 프로그램 정책 objectid의 쉼표로 구분 된 선택적 목록입니다.

- **issuancepolicylist** 는 필수 발급 정책 objectid의 쉼표로 구분 된 선택적 목록입니다.

- **cacertfile** 은 확인할 발급 CA 인증서 (선택 사항)입니다.

- **crossedcacertfile** 는 **certfile**에 의해 교차 인증 되는 선택적인 인증서입니다.

- **CRLfile** 는 **cacertfile**를 확인 하는 데 사용 되는 CRL 파일입니다.

- **issuedcertfile** 는 CRLfile에서 적용 되는 선택적 발급 된 인증서입니다.

- **deltaCRLfile** 는 선택적 델타 CRL 파일입니다.

```
[-f] [-enterprise] [-user] [-silent] [-split] [-urlfetch] [-t timeout]
```

#### <a name="remarks"></a>설명

- **Applicationpolicylist** 를 사용 하면 체인 건물이 지정 된 응용 프로그램 정책에 대해 유효한 체인 으로만 제한 됩니다.

- **Issuancepolicylist** 를 사용 하면 체인 건물이 지정 된 발급 정책에 대해 유효한 체인 으로만 제한 됩니다.

- **Cacertfile** 를 사용 하 여 파일에서 **certfile** 또는 **CRLfile**에 대 한 필드를 확인 합니다.

- **Issuedcertfile** 를 사용 하 여 파일에서 **CRLfile**에 대 한 필드를 확인 합니다.

- DeltaCRLfile를 사용 하 여 **certfile**에 대해 파일의 필드를 확인 합니다.

- **Cacertfile** 를 지정 하지 않으면 전체 체인이 빌드되고 **certfile**에 대해 확인 됩니다.

- **Cacertfile** 및 **crossedcacertfile** 를 모두 지정 하는 경우 두 파일의 필드는 **certfile**에 대해 확인 됩니다.

### <a name="-verifyctl"></a>-verifyCTL

AuthRoot 또는 허용 되지 않는 인증서 CTL을 확인 합니다.

```
certutil [options] -verifyCTL CTLobject [certdir] [certfile]
```

위치:

- **CTLobject** 는 다음을 포함 하 여 확인할 CTL을 식별 합니다.

  - **AuthRootWU** -URL 캐시에서 AuthRoot CAB 및 일치 하는 인증서를 읽습니다. 대신 `-f` 를 사용 하 여 Windows 업데이트에서 다운로드할 수 있습니다.

  - **Disallowedwu** -URL 캐시에서 허용 되지 않는 인증서 CAB 및 허용 되지 않는 인증서 저장소 파일을 읽습니다. 대신 `-f` 를 사용 하 여 Windows 업데이트에서 다운로드할 수 있습니다.

  - **AuthRoot** -레지스트리 캐시 된 AuthRoot CTL을 읽습니다. `-f` 및 신뢰할 수 없는 **certfile** 을 사용 하 여 레지스트리 캐시 된 AuthRoot를 강제로 실행 하 고 허용 되지 않는 인증서 ctl을 업데이트 합니다.

  - **허용 안 함** -레지스트리 캐시 된 허용 되지 않는 인증서 CTL을 읽습니다. `-f` 및 신뢰할 수 없는 **certfile** 을 사용 하 여 레지스트리 캐시 된 AuthRoot를 강제로 실행 하 고 허용 되지 않는 인증서 ctl을 업데이트 합니다.

- **CTLfilename** 는 CTL 또는 CAB 파일에 대 한 파일 또는 http 경로를 지정 합니다.

- **certdir** CTL 항목과 일치 하는 인증서를 포함 하는 폴더를 지정 합니다. 기본값은 **CTLobject**와 동일한 폴더 또는 웹 사이트입니다. Http 폴더 경로를 사용 하려면 끝에 경로 구분 기호가 필요 합니다. **AuthRoot** 또는 **허용**안 함을 지정 하지 않으면 로컬 인증서 저장소, CRYPT32.DLL 리소스 및 로컬 URL 캐시를 포함 하 여 일치 하는 인증서에 대해 여러 위치가 검색 됩니다. 필요 `-f` 에 따라 Windows 업데이트에서 다운로드 하는 데 사용 합니다.

- **certfile** 은 확인할 인증서를 지정 합니다. 인증서는 CTL 항목과 일치 하 여 결과를 표시 합니다. 이 옵션은 대부분의 기본 출력을 표시 하지 않습니다.

```
[-f] [-user] [-split]
```

### <a name="-sign"></a>-기호

인증서 해지 목록 (CRL) 또는 인증서를 다시 서명 합니다.

```
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [startdate+dd:hh] [+serialnumberlist | -serialnumberlist | -objectIDlist | \@extensionfile]
certutil [options] -sign infilelist | serialnumber | CRL outfilelist [#hashalgorithm] [+alternatesignaturealgorithm | -alternatesignaturealgorithm]
```

위치:

- **infilelist** 는 수정 하 고 다시 서명할 인증서 또는 CRL 파일의 쉼표로 구분 된 목록입니다.

- **일련** 번호는 만들 인증서의 일련 번호입니다. 유효 기간 및 기타 옵션을 사용할 수 없습니다.

- **Crl** 이 빈 crl을 만듭니다. 유효 기간 및 기타 옵션을 사용할 수 없습니다.

- **outfilelist** 는 수정 된 인증서 또는 CRL 출력 파일의 쉼표로 구분 된 목록입니다. 파일 수는 infilelist와 일치 해야 합니다.

- 가 중 **+ dd: hh** 는 인증서 또는 CRL 파일의 새 유효 기간 (다음을 포함)입니다.

  - 선택적 날짜 더하기

  - 선택적 요일 및 시간 유효 기간
  
  둘 다 지정 하는 경우에는 더하기 기호 (+) 구분 기호를 사용 해야 합니다. 현재 `now[+dd:hh]` 시간에서를 시작 하는 데 사용 합니다. 만료 `never` 날짜를 사용 하지 않으려면를 사용 합니다 (crl에만 해당).

- **serialnumberlist** 은 추가 하거나 제거할 파일의 쉼표로 구분 된 일련 번호 목록입니다.

- **수정** 은 제거할 파일의 쉼표로 구분 된 확장 ObjectId 목록입니다.

- extensionfile은 업데이트 하거나 제거할 확장을 포함 하는 INF 파일입니다. ** \@** 다음은 그 예입니다. 

  ```
  [Extensions]
      2.5.29.31 = ; Remove CRL Distribution Points extension
      2.5.29.15 = {hex} ; Update Key Usage extension
      _continue_=03 02 01 86
  ```

- **hashalgorithm** 는 해시 알고리즘의 이름입니다. 이는 `#` 부호 앞에 오는 텍스트 여야 합니다.

- **alternatesignaturealgorithm** 는 대체 서명 알고리즘 지정자입니다.

```
[-nullsign] [-f] [-silent] [-cert certID]
```

#### <a name="remarks"></a>설명

- 빼기 기호 (-)를 사용 하면 일련 번호 및 확장이 제거 됩니다.

- 더하기 기호 (+)를 사용 하면 CRL에 일련 번호가 추가 됩니다.

- 목록을 사용 하 여 CRL의 일련 번호와 Objectid을 동시에 제거할 수 있습니다.

- **Alternatesignaturealgorithm** 앞에 빼기 기호를 사용 하면 레거시 서명 형식을 사용할 수 있습니다. 더하기 기호를 사용 하면 대체 서명 형식을 사용할 수 있습니다. **Alternatesignaturealgorithm**를 지정 하지 않으면 인증서 또는 CRL의 서명 형식이 사용 됩니다.

### <a name="-vroot"></a>-vroot

웹 가상 루트 및 파일 공유를 만들거나 삭제 합니다.

```
certutil [options] -vroot [delete]
```

### <a name="-vocsproot"></a>-vocsproot

OCSP 웹 프록시에 대 한 웹 가상 루트를 만들거나 삭제 합니다.

```
certutil [options] -vocsproot [delete]
```

### <a name="-addenrollmentserver"></a>-addenrollmentserver

지정 된 인증 기관에 대해 필요한 경우 등록 서버 응용 프로그램 및 응용 프로그램 풀을 추가 합니다. 이 명령은 이진 또는 패키지를 설치 하지 않습니다.

```
certutil [options] -addenrollmentserver kerberos | username | clientcertificate [allowrenewalsonly] [allowkeybasedrenewal]
```

위치:

- **addenrollmentserver** 를 사용 하려면 다음을 포함 하 여 인증서 등록 서버에 대 한 클라이언트 연결에 대 한 인증 방법을 사용 해야 합니다.

  - **kerberos는 KERBEROS** SSL 자격 증명을 사용 합니다.
  
  - **사용자 이름은** SSL 자격 증명에 명명 된 계정을 사용 합니다.

  - **clientcertificate** 는 X.509 인증서 SSL 자격 증명을 사용 합니다.

- **allowrenewalsonly** 은 URL을 통해 인증 기관에 대 한 갱신 요청 제출만 허용 합니다.

- **allowkeybasedrenewal** 는 Active Directory에서 연결 된 계정이 없는 인증서를 사용할 수 있도록 허용 합니다. 이는 **clientcertificate** 및 **allowrenewalsonly** 모드에서 사용 될 때 적용 됩니다.

```
[-config Machine\CAName]
```

### <a name="-deleteenrollmentserver"></a>-deleteenrollmentserver

지정 된 인증 기관에 대해 필요한 경우 등록 서버 응용 프로그램 및 응용 프로그램 풀을 삭제 합니다. 이 명령은 이진 또는 패키지를 설치 하지 않습니다.

```
certutil [options] -deleteenrollmentserver kerberos | username | clientcertificate
```

위치:

- **deleteenrollmentserver** 를 사용 하려면 다음을 포함 하 여 인증서 등록 서버에 대 한 클라이언트 연결에 대 한 인증 방법을 사용 해야 합니다.

  - **kerberos는 KERBEROS** SSL 자격 증명을 사용 합니다.
  
  - **사용자 이름은** SSL 자격 증명에 명명 된 계정을 사용 합니다.

  - **clientcertificate** 는 X.509 인증서 SSL 자격 증명을 사용 합니다.

```
[-config Machine\CAName]
```

### <a name="-addpolicyserver"></a>-addpolicyserver

필요한 경우 정책 서버 응용 프로그램 및 응용 프로그램 풀을 추가 합니다. 이 명령은 이진 또는 패키지를 설치 하지 않습니다.

```
certutil [options] -addpolicyserver kerberos | username | clientcertificate [keybasedrenewal]
```

위치:

- **addpolicyserver** 를 사용 하려면 다음을 포함 하 여 인증서 정책 서버에 대 한 클라이언트 연결에 대 한 인증 방법을 사용 해야 합니다.

  - **kerberos는 KERBEROS** SSL 자격 증명을 사용 합니다.
  
  - **사용자 이름은** SSL 자격 증명에 명명 된 계정을 사용 합니다.

  - **clientcertificate** 는 X.509 인증서 SSL 자격 증명을 사용 합니다.

- **keybasedrenewal** 를 사용 하면 keybasedrenewal 템플릿을 포함 하는 클라이언트에 반환 되는 정책의 사용을 허용 합니다. 이 옵션은 **사용자 이름** 및 **clientcertificate** 인증에만 적용 됩니다.

### <a name="-deletepolicyserver"></a>-deletepolicyserver

필요한 경우 정책 서버 응용 프로그램 및 응용 프로그램 풀을 삭제 합니다. 이 명령은 이진 또는 패키지를 제거 하지 않습니다.

certutil [옵션]-deletePolicyServer kerberos | 사용자 이름 | clientcertificate [keybasedrenewal]

위치:

- **deletepolicyserver** 를 사용 하려면 다음을 포함 하 여 인증서 정책 서버에 대 한 클라이언트 연결에 대 한 인증 방법을 사용 해야 합니다.

  - **kerberos는 KERBEROS** SSL 자격 증명을 사용 합니다.
  
  - **사용자 이름은** SSL 자격 증명에 명명 된 계정을 사용 합니다.

  - **clientcertificate** 는 X.509 인증서 SSL 자격 증명을 사용 합니다.

- **keybasedrenewal** 는 keybasedrenewal 정책 서버를 사용할 수 있습니다.

### <a name="-oid"></a>-oid

개체 식별자를 표시 하거나 표시 이름을 설정 합니다.

```
certutil [options] -oid objectID [displayname | delete [languageID [type]]]
certutil [options] -oid groupID
certutil [options] -oid agID | algorithmname [groupID]
```

위치:

- **objectID** 표시 이름을 추가 하는 또는를 표시 합니다.

- **groupid** 는 objectid가 열거 하는 groupid 번호 (10 진수)입니다.

- **algID** 는 objectID가 조회 하는 16 진수 ID입니다.

- **algorithmname** 는 objectID가 조회 하는 알고리즘 이름입니다.

- **DISPLAYNAME** DS에 저장할 이름을 표시 합니다.

- **delete** 표시 이름을 삭제 합니다.

- **LanguageId** 는 언어 ID 값 (기본값: 1033)입니다.

- **Type** 은 다음을 비롯 하 여 만들 DS 개체의 유형입니다.

  - `1`-Template (기본값)
  
  - `2`-발급 정책

  - `3`-응용 프로그램 정책

- `-f`DS 개체를 만듭니다.

### <a name="-error"></a>-오류

오류 코드와 관련 된 메시지 텍스트를 표시 합니다.

```
certutil [options] -error errorcode
```

### <a name="-getreg"></a>-getreg

레지스트리 값을 표시 합니다.

```
certutil [options] -getreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

위치:

- **ca** 는 인증 기관의 레지스트리 키를 사용 합니다.

- **복원은** 인증 기관의 복원 레지스트리 키를 사용 합니다.

- **정책은** 정책 모듈의 레지스트리 키를 사용 합니다.

- **종료** 는 첫 번째 끝내기 모듈의 레지스트리 키를 사용 합니다.

- **template에서** 템플릿 레지스트리 키를 사용 합니다 `-user` (사용자 템플릿에 사용).

- **등록은** 등록 레지스트리 키 (사용자 컨텍스트에 `-user` 사용)를 사용 합니다.

- **체인** 구성 레지스트리 키를 사용 합니다.

- **policyservers** 는 Policy servers 레지스트리 키를 사용 합니다.

- **progid** 는 정책 또는 끝내기 모듈의 progID (레지스트리 하위 키 이름)를 사용 합니다.

- **registryvaluename** 는 레지스트리 값 이름 (접두사 일치 `Name*` 에 사용)을 사용 합니다.

- **value** 는 새로운 숫자, 문자열 또는 날짜 레지스트리 값 또는 파일 이름을 사용 합니다. 숫자 값이 또는 `+` `-`로 시작 하는 경우 새 값에 지정 된 비트가 기존 레지스트리 값에서 설정 되거나 지워집니다.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>설명

- 문자열 값이 또는 `+` `-`로 시작 하 고 기존 값이 `REG_MULTI_SZ` 값 이면 기존 레지스트리 값에서 문자열이 추가 되거나 제거 됩니다. `REG_MULTI_SZ` 값을 강제로 생성 하려면 문자열 값의 `\n` 끝에를 추가 합니다.

- 값이로 `\@`시작 하는 경우 나머지 값은 이진 값의 16 진수 텍스트 표현을 포함 하는 파일의 이름입니다. 유효한 파일을 참조 하지 않는 경우에는 선택적 날짜를 포함 하 `[Date][+|-][dd:hh]` 는 선택적 날짜를 포함 하는 대신 선택적 날짜와 시간을 추가 하 여 구문 분석 합니다. 둘 다 지정 하는 경우 더하기 기호 (+) 또는 빼기 기호 (-) 구분 기호를 사용 합니다. 현재 `now+dd:hh` 시간을 기준으로 하는 날짜에 사용 합니다.

- 를 `chain\chaincacheresyncfiletime \@now` 사용 하 여 캐시 된 crl을 효과적으로 플러시합니다.

### <a name="-setreg"></a>-setreg

레지스트리 값을 설정 합니다.

```
certutil [options] -setreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]]registryvaluename value
```

위치:

- **ca** 는 인증 기관의 레지스트리 키를 사용 합니다.

- **복원은** 인증 기관의 복원 레지스트리 키를 사용 합니다.

- **정책은** 정책 모듈의 레지스트리 키를 사용 합니다.

- **종료** 는 첫 번째 끝내기 모듈의 레지스트리 키를 사용 합니다.

- **template에서** 템플릿 레지스트리 키를 사용 합니다 `-user` (사용자 템플릿에 사용).

- **등록은** 등록 레지스트리 키 (사용자 컨텍스트에 `-user` 사용)를 사용 합니다.

- **체인** 구성 레지스트리 키를 사용 합니다.

- **policyservers** 는 Policy servers 레지스트리 키를 사용 합니다.

- **progid** 는 정책 또는 끝내기 모듈의 progID (레지스트리 하위 키 이름)를 사용 합니다.

- **registryvaluename** 는 레지스트리 값 이름 (접두사 일치 `Name*` 에 사용)을 사용 합니다.

- **value** 는 새로운 숫자, 문자열 또는 날짜 레지스트리 값 또는 파일 이름을 사용 합니다. 숫자 값이 또는 `+` `-`로 시작 하는 경우 새 값에 지정 된 비트가 기존 레지스트리 값에서 설정 되거나 지워집니다.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>설명

- 문자열 값이 또는 `+` `-`로 시작 하 고 기존 값이 `REG_MULTI_SZ` 값 이면 기존 레지스트리 값에서 문자열이 추가 되거나 제거 됩니다. `REG_MULTI_SZ` 값을 강제로 생성 하려면 문자열 값의 `\n` 끝에를 추가 합니다.

- 값이로 `\@`시작 하는 경우 나머지 값은 이진 값의 16 진수 텍스트 표현을 포함 하는 파일의 이름입니다. 유효한 파일을 참조 하지 않는 경우에는 선택적 날짜를 포함 하 `[Date][+|-][dd:hh]` 는 선택적 날짜를 포함 하는 대신 선택적 날짜와 시간을 추가 하 여 구문 분석 합니다. 둘 다 지정 하는 경우 더하기 기호 (+) 또는 빼기 기호 (-) 구분 기호를 사용 합니다. 현재 `now+dd:hh` 시간을 기준으로 하는 날짜에 사용 합니다.

- 를 `chain\chaincacheresyncfiletime \@now` 사용 하 여 캐시 된 crl을 효과적으로 플러시합니다.

### <a name="-delreg"></a>-delreg

레지스트리 값을 삭제 합니다.

```
certutil [options] -delreg [{ca | restore | policy | exit | template | enroll |chain | policyservers}\[progID\]][registryvaluename]
```

위치:

- **ca** 는 인증 기관의 레지스트리 키를 사용 합니다.

- **복원은** 인증 기관의 복원 레지스트리 키를 사용 합니다.

- **정책은** 정책 모듈의 레지스트리 키를 사용 합니다.

- **종료** 는 첫 번째 끝내기 모듈의 레지스트리 키를 사용 합니다.

- **template에서** 템플릿 레지스트리 키를 사용 합니다 `-user` (사용자 템플릿에 사용).

- **등록은** 등록 레지스트리 키 (사용자 컨텍스트에 `-user` 사용)를 사용 합니다.

- **체인** 구성 레지스트리 키를 사용 합니다.

- **policyservers** 는 Policy servers 레지스트리 키를 사용 합니다.

- **progid** 는 정책 또는 끝내기 모듈의 progID (레지스트리 하위 키 이름)를 사용 합니다.

- **registryvaluename** 는 레지스트리 값 이름 (접두사 일치 `Name*` 에 사용)을 사용 합니다.

- **value** 는 새로운 숫자, 문자열 또는 날짜 레지스트리 값 또는 파일 이름을 사용 합니다. 숫자 값이 또는 `+` `-`로 시작 하는 경우 새 값에 지정 된 비트가 기존 레지스트리 값에서 설정 되거나 지워집니다.

```
[-f] [-user] [-grouppolicy] [-config Machine\CAName]
```

#### <a name="remarks"></a>설명

- 문자열 값이 또는 `+` `-`로 시작 하 고 기존 값이 `REG_MULTI_SZ` 값 이면 기존 레지스트리 값에서 문자열이 추가 되거나 제거 됩니다. `REG_MULTI_SZ` 값을 강제로 생성 하려면 문자열 값의 `\n` 끝에를 추가 합니다.

- 값이로 `\@`시작 하는 경우 나머지 값은 이진 값의 16 진수 텍스트 표현을 포함 하는 파일의 이름입니다. 유효한 파일을 참조 하지 않는 경우에는 선택적 날짜를 포함 하 `[Date][+|-][dd:hh]` 는 선택적 날짜를 포함 하는 대신 선택적 날짜와 시간을 추가 하 여 구문 분석 합니다. 둘 다 지정 하는 경우 더하기 기호 (+) 또는 빼기 기호 (-) 구분 기호를 사용 합니다. 현재 `now+dd:hh` 시간을 기준으로 하는 날짜에 사용 합니다.

- 를 `chain\chaincacheresyncfiletime \@now` 사용 하 여 캐시 된 crl을 효과적으로 플러시합니다.

### <a name="-importkms"></a>-importKMS

키 보관을 위해 사용자 키와 인증서를 서버 데이터베이스로 가져옵니다.

```
certutil [options] -importKMS userkeyandcertfile [certID]
```

위치:

- **userkeyandcertfile** 은 보관할 사용자 개인 키와 인증서를 포함 하는 데이터 파일입니다. 이 파일은 다음과 같을 수 있습니다.

  - Exchange 키 관리 서버 (KMS) 내보내기 파일입니다.

  - PFX 파일.

- 인증서는 KMS 내보내기 파일 암호 해독 인증서 일치 토큰입니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

- `-f`인증 기관에서 발급 하지 않은 인증서를 가져옵니다.

```
[-f] [-silent] [-split] [-config Machine\CAName] [-p password] [-symkeyalg symmetrickeyalgorithm[,keylength]]
```

### <a name="-importcert"></a>-importcert

인증서 파일을 데이터베이스로 가져옵니다.

```
certutil [options] -importcert certfile [existingrow]
```

위치:

- **가져오려면** 는 동일한 키에 대해 보류 중인 요청 대신 인증서를 가져옵니다.

- `-f`인증 기관에서 발급 하지 않은 인증서를 가져옵니다.

```
[-f] [-config Machine\CAName]
```

#### <a name="remarks"></a>설명

외래 인증서를 지원 하도록 인증 기관을 구성 해야 할 수도 있습니다. 이렇게 하려면을 입력 `import - certutil -setreg ca\KRAFlags +KRAF_ENABLEFOREIGN`합니다.

### <a name="-getkey"></a>-getkey

보관 된 개인 키 복구 blob을 검색 하거나, 복구 스크립트를 생성 하거나, 보관 된 키를 복구 합니다.

```
certutil [options] -getkey searchtoken [recoverybloboutfile]
certutil [options] -getkey searchtoken script outputscriptfile
certutil [options] -getkey searchtoken retrieve | recover outputfilebasename
```

위치:

- **스크립트** 는 키를 검색 및 복구 하는 스크립트를 생성 합니다 (일치 하는 복구 후보가 여러 개 있는 경우 또는 출력 파일이 지정 되지 않은 경우 기본 동작).

- **검색** 은 하나 이상의 키 복구 blob (정확히 하나의 일치 하는 복구 후보가 발견 되는 경우 기본 동작 및 출력 파일이 지정 된 경우)을 검색 합니다. 이 옵션을 사용 하면 확장을 자르고 각 키 복구 blob에 대 한 인증서 관련 문자열과. rec 확장을 추가 합니다.  각 파일에서 인증서 체인 및 하나 이상의 키 복구 에이전트 인증서에 암호화 되어 연결된 된 프라이빗 키를 포함 합니다.

- **복구** 는 한 번에 개인 키를 검색 하 고 복구 합니다. 키 복구 에이전트 인증서 및 개인 키가 필요 합니다. 이 옵션을 사용 하면 모든 확장이 잘리고. p12 확장명이 사용 됩니다.  각 파일에는 PFX 파일로 저장 된 복구 된 인증서 체인 및 연결 된 개인 키가 포함 되어 있습니다.

- **토큰** 은 다음을 비롯 하 여 복구할 키와 인증서를 선택 합니다.

  - 1. 인증서 일반 이름
  
  - 2. 인증서 일련 번호
  
  - 3. 인증서의 sha-1 해시 (지문)
  
  - 4. 인증서 KeyId sha-1 해시 (주체 키 식별자)
  
  - 5. 요청자 이름 (도메인 \ 사용자)
  
  - 6. UPN (사용자\@도메인)

- **하나가** 파일은 하나 이상의 키 복구 에이전트 인증서로 암호화 된 인증서 체인 및 연결 된 개인 키를 사용 하 여 파일을 출력 합니다.

- **outputscriptfile** 는 일괄 처리 스크립트를 사용 하 여 개인 키를 검색 하 고 복구 하는 파일을 출력 합니다.

- **outputfilebasename** 는 파일 기본 이름을 출력 합니다.

```
[-f] [-unicodetext] [-silent] [-config Machine\CAName] [-p password] [-protectto SAMnameandSIDlist] [-csp provider]
```

### <a name="-recoverkey"></a>-recoverkey

보관 된 개인 키를 복구 합니다.

```
certutil [options] -recoverkey recoveryblobinfile [PFXoutfile [recipientindex]]
```

```
[-f] [-user] [-silent] [-split] [-p password] [-protectto SAMnameandSIDlist] [-csp provider] [-t timeout]
```

### <a name="-mergepfx"></a>-mergePFX

PFX 파일을 병합 합니다.

```
certutil [options] -mergePFX PFXinfilelist PFXoutfile [extendedproperties]
```

위치:

- **PFXinfilelist** 은 쉼표로 구분 된 PFX 입력 파일 목록입니다.

- **PFXoutfile** 는 PFX 출력 파일의 이름입니다.

- **extendedproperties** 는 확장 속성을 포함 합니다.

```
[-f] [-user] [-split] [-p password] [-protectto SAMnameAndSIDlist] [-csp provider]
```

#### <a name="remarks"></a>설명

- 명령줄에 지정 된 암호는 쉼표로 구분 된 암호 목록 이어야 합니다.

- 둘 이상의 암호를 지정 하면 출력 파일에 대 한 마지막 암호가 사용 됩니다. 암호를 하나만 제공 하거나 마지막 암호 `*`를 입력 한 경우에는 사용자에 게 출력 파일 암호를 입력 하 라는 메시지가 표시 됩니다.

### <a name="-convertepf"></a>-convertEPF

PFX 파일을 EPF 파일로 변환 합니다.

```
certutil [options] -convertEPF PFXinfilelist PFXoutfile [cast | cast-] [V3CAcertID][,salt]
```

위치:


- **PFXinfilelist** 은 쉼표로 구분 된 PFX 입력 파일 목록입니다.

- **PFXoutfile** 는 PFX 출력 파일의 이름입니다.

- **Epf** 는 epf 출력 파일의 이름입니다.

- **cast** 는 cast 64 암호화를 사용 합니다.

- **cast-** 캐스트 64 암호화 (내보내기)를 사용 합니다.

- **V3CAcertID** 은 V3 CA 인증서 일치 토큰입니다. 자세한 내용은이 문서의 `-store` 매개 변수를 참조 하세요.

- **솔트** 는 EPF 출력 파일 솔트 문자열입니다.

```
[-f] [-silent] [-split] [-dc DCName] [-p password] [-csp provider]
```

#### <a name="remarks"></a>설명

- 명령줄에 지정 된 암호는 쉼표로 구분 된 암호 목록 이어야 합니다.

- 둘 이상의 암호를 지정 하면 출력 파일에 대 한 마지막 암호가 사용 됩니다. 암호를 하나만 제공 하거나 마지막 암호 `*`를 입력 한 경우에는 사용자에 게 출력 파일 암호를 입력 하 라는 메시지가 표시 됩니다.

### <a name="-"></a>-?

매개 변수 목록을 표시 합니다.

``` 
certutil -?
certutil <name_of_parameter> -?
certutil -? -v
```

위치:

- **-?** 매개 변수의 전체 목록을 표시 합니다.

- **-`<name_of_parameter>` -?** 지정 된 매개 변수에 대 한 도움말 콘텐츠를 표시 합니다.

- **-?-v** 매개 변수 및 옵션의 전체 목록을 표시 합니다.

## <a name="options"></a>옵션

이 섹션에서는 명령에 따라 지정할 수 있는 모든 옵션을 정의 합니다. 각 매개 변수에는 사용할 수 있는 옵션에 대 한 정보가 포함 됩니다.

| 옵션 | 설명 |
| ------- | ----------- |
| -nullsign | 데이터의 해시를 서명으로 사용 합니다. |
| -f | 강제로 덮어쓰기. |
| -enterprise | 로컬 컴퓨터 엔터프라이즈 레지스트리 인증서 저장소를 사용 합니다. |
| -사용자 | HKEY_CURRENT_USER 키 또는 인증서 저장소를 사용 합니다. |
| -그룹 정책 | 그룹 정책 인증서 저장소를 사용 합니다. |
| -ut | 사용자 템플릿을 표시 합니다. |
| -mt | 컴퓨터 템플릿을 표시 합니다. |
| 유니코드 | 유니코드로 리디렉션된 출력을 씁니다. |
| -UnicodeText | 유니코드로 출력 파일을 씁니다. |
| -gmt | GMT를 사용 하 여 시간을 표시 합니다. |
| -초 | 초와 밀리초를 사용 하 여 시간을 표시 합니다. |
| -자동 | 플래그를 `silent` 사용 하 여 묘지 컨텍스트를 가져옵니다. |
| -분할 | 포함 된 ASN 요소를 분할 하 고 파일에 저장 합니다. |
| -v | 자세한 정보 (자세한 정보)를 제공 합니다. |
| -privatekey | 암호 및 개인 키 데이터를 표시 합니다. |
| -핀 고정 | 스마트 카드 PIN. |
| -urlfetch | AIA 인증서 및 CDP Crl을 검색 하 고 확인 합니다. |
| -config Machine\CAName | 인증 기관 및 컴퓨터 이름 문자열입니다. |
| -policyserver URLorID | 정책 서버 URL 또는 ID입니다. U/I 선택의 경우를 `-policyserver`사용 합니다. 모든 정책 서버에 대해 다음을 사용 합니다.`-policyserver *`|
| -익명 | 익명 SSL 자격 증명을 사용 합니다. |
| -kerberos | Kerberos SSL 자격 증명을 사용 합니다. |
| -clientcertificate clientcertID | SSL 되는 X.509 인증서 자격 증명을 사용 합니다. U/I 선택의 경우를 `-clientcertificate`사용 합니다. |
| -username 사용자 이름 | SSL 자격 증명에 대 한 명명 된 계정을 사용 합니다. U/I 선택의 경우를 `-username`사용 합니다. |
| -cert 인증서 | 서명 인증서입니다. |
| -dc DCName | 특정 도메인 컨트롤러를 대상으로 지정 합니다. |
| -restrictionlist 제한 | 쉼표로 구분 된 제한 목록입니다. 각 제한 열 이름, 관계형 연산자 및 상수 정수, 문자열 또는 날짜 구성 됩니다. 한 열 이름 수 앞에 더하기 또는 빼기 기호 정렬 순서를 나타냅니다. 예: `requestID = 47`, `+requestername >= a, requestername`또는`-requestername > DOMAIN, Disposition = 21` |
| -out columnlist | 쉼표로 구분 된 열 목록입니다. |
| -p 암호 | 암호 |
| -protectto SAMnameandSIDlist | 쉼표로 구분 된 SAM 이름/s i d 목록입니다. |
| -csp 공급자 | 공급자 |
| -t 제한 시간 | URL 페치 제한 시간 (밀리초)입니다. |
| -symkeyalg symmetrickeyalgorithm [, keylength] | 키 길이가 선택적인 대칭 키 알고리즘의 이름입니다. 예: `AES,128` 또는`3DES` |

### <a name="additional-references"></a>추가 참조

이 명령을 사용 하는 방법에 대 한 몇 가지 예제는를 참조 하십시오.

- [명령줄에서 Active Directory 인증서 서비스 (AD CS)를 관리 하기 위한 Certutil 예제](https://social.technet.microsoft.com/wiki/contents/articles/3063.certutil-examples-for-managing-active-directory-certificate-services-ad-cs-from-the-command-line.aspx)

- [인증서 관리를 위한 Certutil 작업](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc772898(v=ws.10))

- [Certutil 명령줄 도구를 사용 하 여 이진 요청 내보내기 연습](https://social.technet.microsoft.com/wiki/contents/articles/7573.active-directory-certificate-services-pki-key-archival-and-management.aspx)

- [루트 CA 인증서 갱신](https://social.technet.microsoft.com/wiki/contents/articles/2016.root-ca-certificate-renewal.aspx)

- [certutil 명령](certutil.md)
