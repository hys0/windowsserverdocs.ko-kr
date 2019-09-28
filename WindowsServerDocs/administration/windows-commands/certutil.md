---
title: certutil
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c264ccf0-ba1e-412b-9dd3-d77dd9345ad9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45c9946cc53fe3a901c3f6ee53f082a5b3d086c0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379655"
---
# <a name="certutil"></a>certutil

Certutil.exe는 인증서 서비스의 일부로 설치 되는 명령줄 프로그램입니다. Certutil.exe를 사용 하 여를 덤프 및 인증 기관 (CA) 구성 정보를 표시 하 고, 인증서 서비스를 구성 백업 및 CA 구성 요소를 복원 하 고, 인증서, 키 쌍 및 인증서 체인을 확인 합니다.

Certutil 추가 매개 변수 없이 인증 기관에서 실행 되는 현재 인증 기관 구성을 표시 됩니다. 명령이 실행는 certutil 기본적 cerutil-인증 기관에서 실행 될 때 [-덤프](#-dump) 동사입니다.

> [!WARNING]
> 이전 버전의 certutil이이 문서에서 설명 하는 옵션을 모두를 제공할 수 있습니다. Certutil의 특정 버전에 표시 된 명령을 실행 하 여 제공 하는 모든 옵션을 볼 수는 [구문 표기법](#syntax-notations) 섹션입니다.

## <a name="menu"></a>메뉴

이 문서의 주요 섹션이 있습니다.

- [동사의](#verbs)
- [구문 표기법](#syntax-notations)
- [Options](#options)
- [추가 certutil 예제](#additional-certutil-examples)

## <a name="verbs"></a>동사

다음 표에서 certutil 명령을 사용 하 여 사용할 수 있는 동사를 설명 합니다.

|동사|설명|
|-----|-----------|
|[-dump](#-dump)|덤프 구성 정보 또는 파일|
|[-asn](#-asn)|ASN.1 파일을 구문 분석|
|[-decodehex](#-decodehex)|16 진수로 인코딩된 파일 디코딩|
|[-decode](#-decode)|Base64 인코딩된 파일 디코딩|
|[-encode](#-encode)|Base64 파일 인코딩|
|[-deny](#-deny)|보류 중인 인증서 요청을 거부|
|[-resubmit](#-resubmit)|보류 중인 인증서 요청을 다시 제출 하십시오.|
|[-setattributes](#-setattributes)|보류 중인 인증서 요청에 대 한 속성 설정|
|[-setextension](#-setextension)|보류 중인 인증서 요청에 대 한 확장 설정|
|[-revoke](#-revoke)|인증서 해지|
|[-isvalid](#-isvalid)|현재 인증서의 처리를 표시 합니다.|
|[-getconfig](#-getconfig)|기본 구성 문자열 가져오기|
|[-ping](#-ping)|Active Directory 인증서 서비스 요청 인터페이스에 연결 합니다|
|-pingadmin|Active Directory 인증서 서비스 관리 인터페이스를 연결 하기 위해 시도|
|[-CAInfo](#-cainfo)|인증 기관에 대 한 정보를 표시 합니다.|
|[-ca.cert](#-cacert)|인증 기관에 대 한 인증서를 검색 합니다.|
|[-ca.chain](#-cachain)|인증 기관에 대 한 인증서 체인을 검색 합니다.|
|[-GetCRL](#-getcrl)|인증서 해지 목록 (CRL) 가져오기|
|[-CRL](#-crl)|새 인증서 해지 목록 (Crl) [또는 델타 Crl]를 게시 합니다.|
|[-shutdown](#-shutdown)|Active Directory 인증서 서비스를 종료|
|[-installCert](#-installcert)|인증 기관 인증서를 설치 합니다.|
|[-renewCert](#-renewcert)|인증 기관 인증서를 갱신 합니다.|
|[-schema](#-schema)|인증서에 대 한 스키마를 덤프 합니다.|
|[-보기](#-view)|인증서 보기를 덤프 합니다.|
|[-db](#-db)|원시 데이터베이스를 덤프|
|[-deleterow](#-deleterow)|서버 데이터베이스에서 행을 삭제 합니다.|
|[-backup](#-backup)|백업 Active Directory 인증서 서비스|
|[-backupDB](#-backupdb)|Active Directory 인증서 서비스 데이터베이스를 백업 합니다.|
|[-backupKey](#-backupkey)|Active Directory 인증서 서비스 인증서 및 프라이빗 키 백업|
|[-restore](#-restore)|Active Directory 인증서 서비스를 복원 합니다.|
|[-restoreDB](#-restoredb)|Active Directory 인증서 서비스 데이터베이스를 복원 합니다.|
|[-restoreKey](#-restorekey)|Active Directory 인증서 서비스 인증서 및 프라이빗 키 복원|
|[-importPFX](#-importpfx)|인증서 및 프라이빗 가져오기|
|[-dynamicfilelist](#-dynamicfilelist)|동적 파일 목록을 표시 합니다.|
|[-databaselocations](#-databaselocations)|데이터베이스 위치를 표시 합니다.|
|[-hashfile](#-hashfile)|생성 하 고 파일을 통해 암호화 해시를 표시 합니다.|
|[-store](#-store)|인증서 저장소를 덤프 합니다.|
|[-addstore](#-addstore)|저장소에 인증서를 추가 합니다.|
|[-delstore](#-delstore)|저장소에서 인증서를 삭제 합니다.|
|[-verifystore](#-verifystore)|저장소에 인증서를 확인 합니다.|
|[-repairstore](#-repairstore)|키 연결을 복구 하거나 인증서 속성 또는 주요 보안 설명자를 업데이트 합니다.|
|[-viewstore](#-viewstore)|인증서 저장소를 덤프 합니다.|
|[-viewdelstore](#-viewdelstore)|저장소에서 인증서를 삭제 합니다.|
|[-dsPublish](#-dspublish)|인증서 또는 인증서 해지 목록 (CRL) Active Directory에 게시|
|[-ADTemplate](#-adtemplate)|AD 템플릿 표시|
|[-Template](#-template)|인증서 템플릿 표시|
|[-TemplateCAs](#-templatecas)|인증서 템플릿에 대 한 인증 기관 (Ca)를 표시 합니다.|
|[-CATemplates](#-catemplates)|CA에 대 한 서식 파일을 표시 합니다.|
|[-SetCASites](#-setcasites)|Ca에 대 한 사이트 이름 관리|
|[-enrollmentServerURL](#-enrollmentserverurl)|표시, 추가 또는 삭제는 CA와 연결 된 등록 서버 Url|
|[-ADCA](#-adca)|AD Ca 표시|
|[-CA](#-ca)|등록 정책 Ca 표시|
|[-Policy](#-policy)|등록 정책 표시|
|[-PolicyCache](#-policycache)|표시 하거나 등록 정책 캐시 항목 삭제|
|[-CredStore](#-credstore)|표시, 추가 또는 자격 증명 저장소 항목 삭제|
|[-InstallDefaultTemplates](#-installdefaulttemplates)|기본 인증서 템플릿 설치|
|[-URLCache](#-urlcache)|표시 하거나 URL 캐시 항목을 삭제 합니다.|
|[-pulse](#-pulse)|펄스 자동 등록 이벤트|
|[-MachineInfo](#-machineinfo)|Active Directory 컴퓨터 개체에 대 한 정보를 표시 합니다.|
|[-DCInfo](#-dcinfo)|도메인 컨트롤러에 대 한 정보를 표시 합니다.|
|[-EntInfo](#-entinfo)|엔터프라이즈 CA에 대 한 정보를 표시 합니다.|
|[-TCAInfo](#-tcainfo)|CA에 대 한 정보를 표시 합니다.|
|[-SCInfo](#-scinfo)|스마트 카드에 대 한 정보를 표시 합니다.|
|[-SCRoots](#-scroots)|스마트 카드 루트 인증서 관리|
|[-verifykeys](#-verifykeys)|공용 또는 프라이빗 키 집합 확인|
|[-verify](#-verify)|인증서, 인증서 해지 목록 (CRL) 또는 인증서 체인 확인|
|[-verifyCTL](#-verifyctl)|AuthRoot 확인 하거나 인증서 CTL 허용 되지 않습니다.|
|[-sign](#-sign)|인증서 해지 목록 (CRL) 또는 인증서를 다시 서명|
|[-vroot](#-vroot)|웹 가상 루트 및 파일 공유 만들기 또는 삭제|
|[-vocsproot](#-vocsproot)|만들기 또는 웹 가상 루트는 OCSP 웹 프록시에 대 한 삭제|
|[-addEnrollmentServer](#-addenrollmentserver)|등록 서버 응용 프로그램 추가|
|[-deleteEnrollmentServer](#-deleteenrollmentserver)|등록 서버 응용 프로그램 삭제|
|[-addPolicyServer](#-addpolicyserver)|정책 서버 응용 프로그램 추가|
|[-deletePolicyServer](#-deletepolicyserver)|정책 서버 응용 프로그램 삭제|
|[-oid](#-oid)|개체 식별자를 표시 하거나 표시 이름 설정|
|[-error](#-error)|오류 코드와 관련 된 메시지 텍스트를 표시 합니다.|
|[-getreg](#-getreg)|레지스트리 값을 표시 합니다.|
|[-setreg](#-setreg)|레지스트리 값을 설정 합니다.|
|[-delreg](#-delreg)|레지스트리 값 삭제|
|[-ImportKMS](#-importkms)|키를 보관 하 여 서버 데이터베이스에 사용자 키 및 인증서 가져오기|
|[-ImportCert](#-importcert)|데이터베이스에 인증서 파일 가져오기|
|[-GetKey](#-getkey)|보관된 프라이빗 키 복구 blob 검색|
|[-RecoverKey](#-recoverkey)|보관된 프라이빗 키를 복구합니다.|
|[-MergePFX](#-mergepfx)|PFX 파일 병합|
|[-ConvertEPF](#-convertepf)|PFX 파일 EPF 파일로 변환|
|-?|동사 목록을 표시합니다.|
|- *\<verb>* -?|지정 된 동사에 대 한 도움말을 표시 합니다.|
|-? -v|동사의 전체 목록을 표시 하 고|

으로 돌아가서 [메뉴](#menu)

## <a name="syntax-notations"></a>구문 표기법

- 기본 명령줄 구문에 대해를 실행 합니다.`certutil -?`
- 특정 동사에 certutil을 사용 하는 구문에 대해서는 **certutil**  *\<verb >* **-?** 를 실행 합니다.
- 모든 certutil 구문을 텍스트 파일로 보내려면 다음 명령을 실행 합니다.  
  - `certutil -v -? > certutilhelp.txt`
  - `notepad certutilhelp.txt`

다음 표에서 명령줄 구문을 나타내는 데 사용 되는 표기법을 설명 합니다.


|            Notation             |                  설명                  |
|---------------------------------|-----------------------------------------------|
| 대괄호 또는 중괄호가 없는 텍스트 |         표시 된 대로 입력 해야 하는 항목          |
|  \<꺾쇠 괄호 안의 텍스트 >  | 값을 제공 해야 하는 자리 표시자 |
|  [대괄호 안의 텍스트]  |                선택적 항목입니다.                 |
|      {중괄호 안의 텍스트}       |       필수 항목 집합 하나 선택       |
|         세로 막대 (          |                       )                       |
|          줄임표 (...)           |          반복 될 수 있는 항목           |

으로 돌아가서 [메뉴](#menu)

## <a name="-dump"></a>-덤프

CertUtil [Options] [-dump]

CertUtil [옵션] [-덤프] 파일

덤프 구성 정보 또는 파일

[-f] [-자동] [-split] [-p 암호] [-t 제한 시간]

으로 돌아가서 [메뉴](#menu)

## <a name="-asn"></a>-asn

CertUtil [옵션]-asn 파일 [형식]

ASN.1 파일을 구문 분석

형식: 숫자\_문자 및\_ 문자열\* 디코딩 형식

으로 돌아가서 [메뉴](#menu)

## <a name="-decodehex"></a>-decodehex

CertUtil [옵션]-decodehex InFile 출력 이름 [type]

유형: 숫자\_문자 및\_ 문자열\* 인코딩 유형

[-f]

으로 돌아가서 [메뉴](#menu)

## <a name="-decode"></a>-디코딩

CertUtil [Options] -decode InFile OutFile

Base64 인코딩 파일 디코딩

[-f]

으로 돌아가서 [메뉴](#menu)

## <a name="-encode"></a>-인코딩

CertUtil [옵션]-InFile 출력 인코딩

Base64로 파일 인코딩

[-f] [-UnicodeText]

으로 돌아가서 [메뉴](#menu)

## <a name="-deny"></a>-거부

CertUtil [옵션]-RequestId 거부

보류 중인 요청 거부

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-resubmit"></a>-다시 전송

CertUtil [Options] -resubmit RequestId

보류 중인 요청 다시 제출

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-setattributes"></a>-setattributes

CertUtil [옵션]-setattributes RequestId AttributeString

보류 중인 요청에 대 한 특성 설정

RequestId--보류 중인 요청의 숫자 요청 Id

AttributeString--특성 이름 및 값 쌍 요청

- 이름 및 값으로 구분 됩니다.
- 여러 개의 이름 값 쌍은 줄 바꿈 구분 됩니다.
- 예: "CertificateTemplate:User\nEMail:User@Domain.com"
- 각 "\n" 시퀀스를 줄 바꿈 구분 기호로 변환 됩니다.

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-setextension"></a>-setextension

CertUtil [옵션]-setextension RequestId ExtensionName Flags {Long | 날짜 | 문자열 | \@InFile}

보류 중인 요청에 대 한 확장 설정

RequestId--보류 중인 요청의 숫자 요청 Id

ExtensionName--확장의 ObjectId 문자열

플래그--0이 권장 됩니다.  1은 확장을 중요 하 고, 비활성화할 경우 2, 3 모두를 수행 합니다.

마지막 매개 변수는 숫자, Long으로 수행 됩니다.

날짜로 분석, 날짜로 수행 됩니다.

'\@'로 시작 하는 경우 토큰의 나머지 부분은 이진 데이터 또는 ascii 텍스트 hex 덤프를 포함 하는 파일 이름입니다.

다른 항목을 문자열로 가져옵니다.

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-revoke"></a>-취소

CertUtil [Options] -revoke SerialNumber [Reason]

인증서 해지

SerialNumber 해지할 인증서 일련 번호의 쉼표로 구분 된 목록입니다.

이유: 숫자 또는 기호화 된 해지 이유

- 0: CRL_REASON_UNSPECIFIED: 지정 되지 않음 (기본값)
- 1: CRL_REASON_KEY_COMPROMISE: 키 손상
- 2: CRL_REASON_CA_COMPROMISE: CA 손상
- 3: CRL_REASON_AFFILIATION_CHANGED: 정보가 변경됨
- 4: CRL_REASON_SUPERSEDED: 대체됨
- 5: CRL_REASON_CESSATION_OF_OPERATION: 작업 해시 중단
- 6: CRL_REASON_CERTIFICATE_HOLD: 인증서 보유
- 20cm(8 CRL_REASON_REMOVE_FROM_CRL: CRL에서 제거
- -1: 해지 해지

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-isvalid"></a>-isvalid

CertUtil [옵션]-isvalid 일련 문으로

현재 인증서 처리 표시

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-getconfig"></a>-getconfig

CertUtil [Options] -getconfig

기본 구성 문자열 가져오기

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-ping"></a>-ping

CertUtil [옵션]-ping [MaxSecondsToWait | CAMachineList

Ping Active Directory 인증서 서비스 요청 인터페이스

CAMachineList-쉼표로 구분 된 CA 컴퓨터 이름 목록

1. 단일 컴퓨터에 대 한 종결 쉼표를 사용 합니다.
2. 각 CA 컴퓨터에 대 한 사이트 비용을 표시 합니다.

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-cainfo"></a>-CAInfo

CertUtil [옵션]-CAInfo [InfoName [Index | ErrorCode]]

CA 정보 표시

InfoName-표시할 CA 속성을 나타냅니다 (아래 참조). 모든 속성\*에 대해 ""를 사용 합니다.

인덱스--선택적 0부터 시작 하는 속성 인덱스

ErrorCode-숫자 오류 코드

[-f] [-split] [-config Machine\CAName]

InfoName 인수 구문:

- 파일과 파일 버전
- 제품은 제품 버전
- exitcount: 끝내기 모듈 수
- 종료 [Index]: 끝내기 모듈 설명
- policy 정책 모듈 설명
- 이름의 CA 이름
- sanitizedname: 삭제 한 CA 이름
- dsname 삭제 한 CA 약식 이름 (DS 이름)
- sharedfolder: 공유 폴더
- error1 ErrorCode: 오류 메시지 텍스트
- error2 ErrorCode: 오류 메시지 텍스트 및 오류 코드
- 형식: CA 유형
- 나타납니다 CA 정보
- 부모 부모 CA
- certcount: CA 인증서 수
- xchgcount: CA exchange 인증서 수
- kracount: KRA 인증서 수
- kraused: KRA 인증서 사용 횟수
- propidmax: 최대 CA PropId
- certstate [Index]: CA 인증서
- certversion [Index]: CA 인증서 버전
- certstatuscode [Index]: CA 인증서 확인 상태
- crlstate [Index]: CRL
- krastate [Index]: KRA 인증서
- 사이 주 + [인덱스]: 크로스 인증서 전달
- 간 상태-[Index]: 역방향 상호 인증서
- cert [Index]: CA 인증서
- certchain [Index]: CA 인증서 체인
- certcrlchain [Index]: Crl을 사용 하는 CA 인증서 체인
- xchg [Index]: CA exchange 인증서
- xchgchain [Index]: CA 교환 인증서 체인
- xchgcrlchain [Index]: Crl을 사용한 CA 교환 인증서 체인
- kra [인덱스]: KRA 인증서
- cross + [Index]: 크로스 인증서 전달
- 교차 [인덱스]: 역방향 상호 인증서
- CRL [인덱스]: 기본 CRL
- deltacrl [Index]: 델타 CRL
- crlstatus [Index]: CRL 게시 상태
- deltacrlstatus [Index]: 델타 CRL 게시 상태
- dns DNS 이름
- 역할 역할 구분
- 통한 Advanced Server
- 모음 템플릿
- csp [인덱스]: OCSP Url
- aia [Index]: AIA Url
- cdp [Index]: CDP Url
- localename CA 로캘 이름
- 주제 템플릿 oid: 주제 템플릿 Oid

으로 돌아가서 [메뉴](#menu)

## <a name="-cacert"></a>-ca.cert

CertUtil [옵션]-OutCACertFile [인덱스]

CA의 인증서 검색

OutCACertFile: 출력 파일

인덱싱할 CA 인증서 갱신 인덱스 (기본값은 가장 최근)

[-f] [-split] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-cachain"></a>-ca.chain

CertUtil [옵션]-OutCACertChainFile [인덱스]

CA의 인증서 체인 검색

OutCACertChainFile: 출력 파일

인덱싱할 CA 인증서 갱신 인덱스 (기본값은 가장 최근)

[-f] [-split] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-getcrl"></a>-GetCRL

CertUtil [Options] -GetCRL OutFile [Index] [delta]

CRL 가져오기

인덱싱할 CRL 인덱스 또는 키 인덱스 (최신 키의 경우 CRL로 기본값)

델타: 델타 CRL (기본값은 기본 CRL)

[-f] [-split] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-crl"></a>-CRL

CertUtil [Options] -CRL [dd:hh | republish] [delta]

새 Crl 게시 [또는 델타 Crl만]

dd: hh--새 CRL 유효 기간 (일 및 시간)

다시 게시-최신 Crl 다시 게시

델타--델타 Crl만 (기본값은 기본 및 델타 Crl)

[-split] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-shutdown"></a>-종료

CertUtil [Options] -shutdown

Active Directory 인증서 서비스를 종료

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-installcert"></a>-installCert

CertUtil [옵션]-installCert [CACertFile]

인증 기관 인증서 설치

[-f] [-자동] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-renewcert"></a>-renewCert

CertUtil [Options] -renewCert [ReuseKeys] [Machine\ParentCAName]

인증 기관 인증서 갱신

-F를 사용 하 여 미해결 갱신 요청을 무시 하 고 새 요청을 생성 합니다.

[-f] [-자동] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-schema"></a>-스키마

CertUtil [Options] -schema [Ext | Attrib | CRL]

인증서 스키마 덤프

요청 및 인증서 테이블로 기본값 설정

확장 확장 테이블

특성과 특성 테이블

CRL: CRL 테이블

[-split] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-view"></a>-보기

CertUtil [옵션]-보기 [큐 | 로그 | LogFail | 해지 됨 | Ext | 특성 | CRL] [csv]

인증서 보기 덤프

큐: 요청 큐

로그 발급 되거나 해지 된 인증서 및 실패 한 요청

LogFail: 실패한 요청

됨 해지 된 인증서

확장 확장 테이블

특성과 특성 테이블

CRL: CRL 테이블

csv: 쉼표로 구분 된 값으로 출력

모든 항목에 대해 StatusCode 열을 표시 하려면:-out StatusCode

마지막 항목에 대 한 모든 열을 표시 하려면:-restrict "RequestId = = $"

세 개의 요청에 대 한 requestid 및 처리를 표시 하려면:-restrict "requestid >\<= 37, requestid 40"-out "requestid, 처리"

모든 기본 Crl의 행 Id 및 CRL 번호를 표시 하려면:-restrict "CRLMinBase = 0"-out "CRLRowId, CRLNumber" CRL

기본 CRL 번호 3:-v-restrict "CRLMinBase = 0, CRLNumber = 3" CRLRawCRL "CRL을 표시 하려면

전체 CRL 테이블을 표시 하려면 다음을 수행 합니다. CRL

날짜 제한의 경우 "Date [+ |-dd: hh]"를 사용 합니다.

현재 시간을 기준으로 하는 날짜에는 "now + dd: hh"를 사용 합니다.

[-자동] [-split] [-config Machine\CAName] [-RestrictionList 제한] [-out ColumnList]

으로 돌아가서 [메뉴](#menu)

## <a name="-db"></a>-db

CertUtil [Options] -db

원시 데이터베이스 덤프

[-config Machine\CAName] [-RestrictionList 제한] [-out ColumnList]

으로 돌아가서 [메뉴](#menu)

## <a name="-deleterow"></a>-deleterow

CertUtil [옵션]-deleterow RowId | 날짜 [요청 | 인증서 | Ext | 특성 | CRL

서버 데이터베이스 행 삭제

요구 실패 한 요청 및 보류 중인 요청 (제출 날짜)

인증서: 만료 및 해지 된 인증서 (만료 날짜)

확장 확장 테이블

특성과 특성 테이블

CRL: CRL 테이블 (만료 날짜)

2001 년 1 월 22 일에 제출 된 실패 및 보류 중인 요청을 삭제 하려면: 1/22/2001 요청

2001 년 1 월 22 일에 만료 된 모든 인증서를 삭제 하려면: 1/22/2001 인증서

RequestId 37에 대 한 인증서 행, 특성 및 확장을 삭제 하려면 다음을 수행 합니다. 37

2001 년 1 월 22 일에 만료 된 Crl을 삭제 하려면: 1/22/2001 CRL

[-f] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-backup"></a>-백업

CertUtil [옵션]-백업 백업 백업 [증분] [KeepLog]

백업 Active Directory 인증서 서비스

백업 디렉터리: 백업 데이터를 저장할 디렉터리

증분: 증분 백업만 수행 (기본값은 전체 백업)

KeepLog: 데이터베이스 로그 파일 보존 (기본값은 로그 파일 자르기)

[-f] [-config Machine\CAName] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-backupdb"></a>-backupDB

CertUtil [옵션]-backupDB 백업 [증분] [KeepLog]

인증서 서비스 데이터베이스 백업 Active Directory

백업 디렉터리: 백업 데이터베이스 파일을 저장 하는 디렉터리

증분: 증분 백업만 수행 (기본값은 전체 백업)

KeepLog: 데이터베이스 로그 파일 보존 (기본값은 로그 파일 자르기)

[-f] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-backupkey"></a>-backupKey

CertUtil [Options] -backupKey BackupDirectory

인증서 서비스 인증서 및 개인 키 Active Directory 백업

백업 디렉터리: 백업 PFX 파일을 저장할 디렉터리

[-f] [-config Machine\CAName] [-p 암호] [-t 제한 시간]

으로 돌아가서 [메뉴](#menu)

## <a name="-restore"></a>-복원

CertUtil [Options] -restore BackupDirectory

Active Directory 인증서 서비스를 복원 합니다.

백업 디렉터리: 복원할 데이터를 포함 하는 디렉터리

[-f] [-config Machine\CAName] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-restoredb"></a>-restoreDB

CertUtil [Options] -restoreDB BackupDirectory

Active Directory 인증서 서비스 데이터베이스 복원

백업 디렉터리: 복원할 데이터베이스 파일을 포함 하는 디렉터리

[-f] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-restorekey"></a>-restoreKey

CertUtil [옵션]-restoreKey 백업 | 복원할

Active Directory 인증서 서비스 인증서 및 개인 키 복원

백업 디렉터리: 복원할 PFX 파일을 포함 하는 디렉터리

복원할 복원할 PFX 파일

[-f] [-config Machine\CAName] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-importpfx"></a>-importPFX

CertUtil [옵션]-importPFX [CertificateStoreName] 복원할 [Modifiers]

인증서 및 프라이빗 가져오기

CertificateStoreName: 인증서 저장소 이름입니다.  참조 [-저장](#-store)합니다.

복원할 가져올 PFX 파일

수정자 쉼표로 구분 된 다음 중 하나 이상의 목록입니다.

1. AT_SIGNATURE: KeySpec를 Signature로 변경 합니다.
2. AT_KEYEXCHANGE: KeySpec를 키 교환으로 변경
3. NoExport: 개인 키를 내보낼 수 없는 것으로 설정
4. NoCert: 인증서를 가져오지 않음
5. NoChain: 인증서 체인을 가져오지 않음
6. NoRoot: 루트 인증서를 가져오지 않음
7. 보호 암호를 사용 하 여 키 보호
8. NoProtect: 키를 암호로 보호 하지 않음

기본값은 개인 컴퓨터 저장소입니다.

[-f] [-user] [-p 암호] [-csp 공급자]

으로 돌아가서 [메뉴](#menu)

## <a name="-dynamicfilelist"></a>-dynamicfilelist

CertUtil [Options] -dynamicfilelist

동적 파일 목록 표시

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-databaselocations"></a>-databaselocations

CertUtil [Options] -databaselocations

데이터베이스 위치를 표시 합니다.

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-hashfile"></a>-hashfile

CertUtil [옵션]-hashfile InFile [HashAlgorithm]

파일에 대 한 암호화 해시 생성 및 표시

으로 돌아가서 [메뉴](#menu)

## <a name="-store"></a>-저장

CertUtil [Options] -store [CertificateStoreName [CertId [OutputFile]]]

인증서 저장소 덤프

CertificateStoreName: 인증서 저장소 이름입니다. 예를 들면 다음과 같습니다.

- "My", "CA" (기본값), "Root"
- "ldap: / / / CN 인증 기관, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 하나? objectClass certificationAuthority =" (루트 인증서 보기)
- "ldap: / / / CN CAName, CN = 인증 기관, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 기본? objectClass certificationAuthority =" (수정 루트 인증서)
- "ldap: / / / CN CAName, CN = MachineName, CN = CDP, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? certificateRevocationList? 기본? objectClass cRLDistributionPoint =" (Crl 보기)
- "ldap: / / / CN NTAuthCertificates, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 기본? objectClass certificationAuthority =" (엔터프라이즈 CA 인증서)
- ldap (AD 컴퓨터 개체 인증서)
- -사용자 ldap: (AD 사용자 개체 인증서)

CertId: 인증서 또는 CRL 일치 토큰입니다.  이 일련 번호, s h A 1 인증서, CRL, CTL 또는 공개 키 해시 숫자 cert 인덱스 수 (0, 1 및 등) CRL의 숫자 인덱스 (. 0, 순서 대로.1, 및 등), CTL의 숫자 인덱스 (... 0, .. 1, 등), 공개 키, 서명 또는 확장 ObjectId, 인증서 주체 일반 이름, 전자 메일 주소, UPN 또는 DNS 이름, 키 컨테이너 이름 또는 CSP 이름, 템플릿 이름 또는 ObjectId, EKU 또는 응용 프로그램 정책 ObjectId 또는 CRL 발급자 일반 이름입니다. 이러한 대부분의 여러 일치 항목이 될 수 있습니다.

OutputFile: 일치 하는 인증서를 저장할 파일

-User를 사용 하 여 컴퓨터 저장소 대신 사용자 저장소에 액세스 합니다.

-을 사용 하 여 컴퓨터 엔터프라이즈 저장소에 액세스 하는 기업입니다.

-을 사용 하 여 컴퓨터 서비스 저장소에 액세스 하는 서비스입니다.

-그룹 정책을 사용 하 여 컴퓨터 그룹 정책 저장소에 액세스 합니다.

예를 들면 다음과 같습니다.

- -엔터프라이즈 NTAuth
- -엔터프라이즈 루트 37
- -사용자 내 26e0aaaf000000000004
- CA. 11

[-f] [-enterprise] [-user] [-GroupPolicy] [-자동] [-split] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-addstore"></a>-addstore

CertUtil [옵션]-addstore CertificateStoreName InFile

저장소에 인증서 추가

CertificateStoreName: 인증서 저장소 이름입니다.  참조 [-저장](#-store)합니다.

InFile 저장소에 추가할 인증서 또는 CRL 파일입니다.

[-f] [-enterprise] [-user] [-GroupPolicy] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-delstore"></a>-delstore

CertUtil [Options] -delstore CertificateStoreName CertId

저장소에서 인증서 삭제

CertificateStoreName: 인증서 저장소 이름입니다.  참조 [-저장](#-store)합니다.

CertId: 인증서 또는 CRL 일치 토큰입니다.  참조 [-저장](#-store)합니다.

[-enterprise] [-user] [-GroupPolicy] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-verifystore"></a>-verifystore

CertUtil [Options] -verifystore CertificateStoreName [CertId]

저장소에서 인증서 확인

CertificateStoreName: 인증서 저장소 이름입니다.  참조 [-저장](#-store)합니다.

CertId: 인증서 또는 CRL 일치 토큰입니다.  참조 [-저장](#-store)합니다.

[-enterprise] [-user] [-GroupPolicy] [-자동] [-split] [-dc DCName] [-t 제한 시간]

으로 돌아가서 [메뉴](#menu)

## <a name="-repairstore"></a>-repairstore

CertUtil [Options] -repairstore CertificateStoreName CertIdList [PropertyInfFile | SDDLSecurityDescriptor]

키 연결 복구 또는 인증서 속성 또는 키 보안 설명자 업데이트

CertificateStoreName: 인증서 저장소 이름입니다.  참조 [-저장](#-store)합니다.

인증서 또는 CRL 일치 토큰 CertIdList: 쉼표로 구분 된 목록입니다. 참조 [-저장](#-store) 인증서 설명 합니다.

외부 속성을 포함 한 PropertyInfFile-INF 파일:

```
[Properties]
     19 = Empty ; Add archived property, OR:
     19 =       ; Remove archived property

     11 = "{text}Friendly Name" ; Add friendly name property

     127 = "{hex}" ; Add custom hexadecimal property
         _continue_ = "00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f"
         _continue_ = "10 11 12 13 14 15 16 17 18 19 1a 1b 1c 1d 1e 1f"

     2 = "{text}" ; Add Key Provider Information property
       _continue_ = "Container=Container Name&"
       _continue_ = "Provider=Microsoft Strong Cryptographic Provider&"
       _continue_ = "ProviderType=1&"
       _continue_ = "Flags=0&"
       _continue_ = "KeySpec=2"

     9 = "{text}" ; Add Enhanced Key Usage property
       _continue_ = "1.3.6.1.5.5.7.3.2,"
       _continue_ = "1.3.6.1.5.5.7.3.1,"
```

[-f] [-enterprise] [-user] [-GroupPolicy] [-자동] [-split] [-csp 공급자]

으로 돌아가서 [메뉴](#menu)

## <a name="-viewstore"></a>-뷰 저장소

CertUtil [옵션]-viewstore [CertificateStoreName [인증서 [OutputFile]]]

인증서 저장소 덤프

CertificateStoreName: 인증서 저장소 이름입니다. 예를 들면 다음과 같습니다.

- "My", "CA" (기본값), "Root"
- "ldap: / / / CN 인증 기관, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 하나? objectClass certificationAuthority =" (루트 인증서 보기)
- "ldap: / / / CN CAName, CN = 인증 기관, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 기본? objectClass certificationAuthority =" (수정 루트 인증서)
- "ldap: / / / CN CAName, CN = MachineName, CN = CDP, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? certificateRevocationList? 기본? objectClass cRLDistributionPoint =" (Crl 보기)
- "ldap: / / / CN NTAuthCertificates, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 기본? objectClass certificationAuthority =" (엔터프라이즈 CA 인증서)
- ldap (AD 컴퓨터 개체 인증서)
- -사용자 ldap: (AD 사용자 개체 인증서)

CertId: 인증서 또는 CRL 일치 토큰입니다. 이 일련 번호, s h A 1 인증서, CRL, CTL 또는 공개 키 해시 숫자 cert 인덱스 수 (0, 1 및 등) CRL의 숫자 인덱스 (. 0, 순서 대로.1, 및 등), CTL의 숫자 인덱스 (... 0, .. 1, 등), 공개 키, 서명 또는 확장 ObjectId, 인증서 주체 일반 이름, 전자 메일 주소, UPN 또는 DNS 이름, 키 컨테이너 이름 또는 CSP 이름, 템플릿 이름 또는 ObjectId, EKU 또는 응용 프로그램 정책 ObjectId 또는 CRL 발급자 일반 이름입니다. 이러한 대부분의 여러 일치 항목이 될 수 있습니다.

OutputFile: 일치 하는 인증서를 저장할 파일

-User를 사용 하 여 컴퓨터 저장소 대신 사용자 저장소에 액세스 합니다.

-을 사용 하 여 컴퓨터 엔터프라이즈 저장소에 액세스 하는 기업입니다.

-을 사용 하 여 컴퓨터 서비스 저장소에 액세스 하는 서비스입니다.

-그룹 정책을 사용 하 여 컴퓨터 그룹 정책 저장소에 액세스 합니다.

예를 들면 다음과 같습니다.

1. -엔터프라이즈 NTAuth
2. -엔터프라이즈 루트 37
3. -사용자 내 26e0aaaf000000000004
4. CA. 11

[-f] [-enterprise] [-user] [-GroupPolicy] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-viewdelstore"></a>-viewdelstore

CertUtil [옵션]-viewdelstore [CertificateStoreName [인증서 [OutputFile]]]

저장소에서 인증서 삭제

CertificateStoreName: 인증서 저장소 이름입니다. 예를 들면 다음과 같습니다.

- "My", "CA" (기본값), "Root"
- "ldap: / / / CN 인증 기관, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 하나? objectClass certificationAuthority =" (루트 인증서 보기)
- "ldap: / / / CN CAName, CN = 인증 기관, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 기본? objectClass certificationAuthority =" (수정 루트 인증서)
- "ldap: / / / CN CAName, CN = MachineName, CN = CDP, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? certificateRevocationList? 기본? objectClass cRLDistributionPoint =" (Crl 보기)
- "ldap: / / / CN NTAuthCertificates, CN = Public Key Services, CN = Services, CN = Configuration, DC = cpandl, DC = com =? cACertificate? 기본? objectClass certificationAuthority =" (엔터프라이즈 CA 인증서)
- ldap (AD 컴퓨터 개체 인증서)
- -사용자 ldap: (AD 사용자 개체 인증서)

CertId: 인증서 또는 CRL 일치 토큰입니다. 이 일련 번호, s h A 1 인증서, CRL, CTL 또는 공개 키 해시 숫자 cert 인덱스 수 (0, 1 및 등) CRL의 숫자 인덱스 (. 0, 순서 대로.1, 및 등), CTL의 숫자 인덱스 (... 0, .. 1, 등), 공개 키, 서명 또는 확장 ObjectId, 인증서 주체 일반 이름, 전자 메일 주소, UPN 또는 DNS 이름, 키 컨테이너 이름 또는 CSP 이름, 템플릿 이름 또는 ObjectId, EKU 또는 응용 프로그램 정책 ObjectId 또는 CRL 발급자 일반 이름입니다. 이러한 대부분의 여러 일치 항목이 될 수 있습니다.

OutputFile: 일치 하는 인증서를 저장할 파일

-User를 사용 하 여 컴퓨터 저장소 대신 사용자 저장소에 액세스 합니다.

-을 사용 하 여 컴퓨터 엔터프라이즈 저장소에 액세스 하는 기업입니다.

-을 사용 하 여 컴퓨터 서비스 저장소에 액세스 하는 서비스입니다.

-그룹 정책을 사용 하 여 컴퓨터 그룹 정책 저장소에 액세스 합니다.

예를 들면 다음과 같습니다.

1. -엔터프라이즈 NTAuth
2. -엔터프라이즈 루트 37
3. -사용자 내 26e0aaaf000000000004
4. CA. 11

[-f] [-enterprise] [-user] [-GroupPolicy] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-dspublish"></a>-dsPublish

CertUtil [옵션]-dsPublish CertFile [NTAuthCA | Rootca.cer | 하위 Ca | CrossCA | KRA | 사용자 | 컴퓨터

CertUtil [옵션]-dsPublish CRLFile [DSCDPContainer [DSCDPCN]]

Active Directory에 인증서 또는 CRL 게시

CertFile: 게시할 인증서 파일

NTAuthCA: DS 엔터프라이즈 저장소에 인증서 게시

RootCA: DS의 신뢰할 수 있는 루트 저장소에 인증서 게시

SubCA DS CA 개체에 CA 인증서 게시

CrossCA: DS CA 개체에 교차 인증서 게시

KRA DS 키 복구 에이전트 개체에 인증서 게시

사용자: 사용자 DS 개체에 인증서 게시

컴퓨터: 컴퓨터 DS 개체에 인증서 게시

CRLFile 게시할 CRL 파일

DSCDPContainer: DS CDP 컨테이너 CN (일반적으로 CA 컴퓨터 이름)

DSCDPCN: 일반적으로 삭제 된 CA 짧은 이름 및 키 인덱스를 기반으로 하는 DS CDP 개체 CN

-F를 사용 하 여 DS 개체를 만듭니다.

[-f] [-user] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-adtemplate"></a>-ADTemplate

CertUtil [옵션]-ADTemplate [템플릿]

AD 템플릿 표시

[-f] [-user] [-전체] [-mt] [-dc DCName]

## <a name="-template"></a>템플릿

CertUtil [옵션]-템플릿 [템플릿]

등록 정책 템플릿 표시

[-f] [-user] [-자동] [-PolicyServer URLOrId] [-익명] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName 사용자 이름] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-templatecas"></a>-TemplateCAs

CertUtil [Options] -TemplateCAs Template

템플릿에 대 한 Ca 표시

[-f] [-user] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-catemplates"></a>-CATemplates

CertUtil [옵션]-CATemplates [템플릿]

CA에 대 한 서식 파일을 표시 합니다.

[-f] [-user] [-ut] [-mt] [-config Machine\CAName] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-setcasites"></a>-SetCASites

CertUtil [Options] -SetCASites [set] [SiteName]

CertUtil [옵션]-SetCASites 확인 [SiteName]

CertUtil [Options] -SetCASites delete

CA 사이트 이름 설정, 확인 또는 삭제

- -Config 옵션을 사용 하 여 단일 CA 대상 (기본값인 모든 Ca)
- *SiteName* 단일 CA를 대상으로 하는 경우에 허용 됩니다
- -F를 사용 하 여 지정 된 유효성 검사 오류를 무시 하려면 *사이트 이름*
- 모든 CA 사이트 이름을 삭제 하려면-f를 사용 합니다.

[-f] [-config Machine\CAName] [-dc DCName]

> [!NOTE]
> Active Directory 도메인 서비스 (AD DS) 사이트 인식에 대 한 Ca를 구성에 대 한 자세한 내용은 참조 하십시오. [AD CS 및 PKI 클라이언트에 대 한 AD DS 사이트 인지도](https://social.technet.microsoft.com/wiki/contents/articles/14106.ad-ds-site-awareness-for-ad-cs-and-pki-clients.aspx)합니다.

으로 돌아가서 [메뉴](#menu)

## <a name="-enrollmentserverurl"></a>-enrollmentServerURL

CertUtil [옵션]-enrollmentServerURL [URL AuthenticationType [우선 순위] [한정자]]

CertUtil [Options] -enrollmentServerURL URL delete

표시, 추가 또는 삭제는 CA와 연결 된 등록 서버 Url

AuthenticationType: URL을 추가 하는 동안 다음 클라이언트 인증 방법 중 하나를 지정 합니다.

1. Kerberos Kerberos SSL 자격 증명을 사용 하 여
2. 이름 SSL 자격 증명에 명명 된 계정 사용
3. ClientCertificate X.509 인증서 SSL 자격 증명 사용
4. Anonymous: 익명 SSL 자격 증명을 사용 하 여

삭제: CA와 연결 된 지정 된 URL을 삭제 합니다.

우선 순위: URL을 추가할 때 지정 되지 않은 경우 기본값은 ' 1 '입니다.

한정자-쉼표로 구분 된 다음 중 하나 이상의 목록입니다.

1. AllowRenewalsOnly: 이 URL을 통해이 CA에 갱신 요청을 제출할 수 있습니다.
2. AllowKeyBasedRenewal: AD에 연결 된 계정이 없는 인증서를 사용할 수 있습니다. 이는 ClientCertificate 및 AllowRenewalsOnly 모드에만 적용 됩니다.

[-config Machine\CAName] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-adca"></a>-ADCA

CertUtil [Options] -ADCA [CAName]

AD Ca 표시

[-f] [-split] [-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-ca"></a>-CA

CertUtil [옵션]-CA [CAName | TemplateName

등록 정책 Ca 표시

[-f] [-user] [-자동] [-split] [-PolicyServer URLOrId] [-익명] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName 사용자 이름] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-policy"></a>정책

등록 정책 표시

[-f] [-user] [-자동] [-split] [-PolicyServer URLOrId] [-익명] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName 사용자 이름] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-policycache"></a>-PolicyCache

CertUtil [Options] -PolicyCache [delete]

표시 하거나 등록 정책 캐시 항목 삭제

삭제: 정책 서버 캐시 항목 삭제

-f: 모든 캐시 항목을 삭제 하려면-f를 사용 합니다.

[-f] [-user] [-PolicyServer URLOrId]

으로 돌아가서 [메뉴](#menu)

## <a name="-credstore"></a>-CredStore

CertUtil [Options] -CredStore [URL]

CertUtil [옵션]-CredStore URL 추가

CertUtil [옵션]-CredStore URL 삭제

표시, 추가 또는 자격 증명 저장소 항목 삭제

URL: 대상 URL입니다.  모든 \* 항목을 일치 시키는 데 사용 합니다. \* https://machine\ 를 사용 하 여 URL 접두사를 일치 시킵니다.

추가: 자격 증명 저장소 항목을 추가 합니다. 또한 SSL 자격 증명을 지정 해야 합니다.

삭제: 자격 증명 저장소 항목 삭제

-f:-f를 사용 하 여 항목을 덮어쓰거나 여러 항목을 삭제 합니다.

[-f] [-user] [-자동] [-익명] [-Kerberos] [-ClientCertificate ClientCertId] [-UserName 사용자 이름] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-installdefaulttemplates"></a>-InstallDefaultTemplates

CertUtil [Options] -InstallDefaultTemplates

기본 인증서 템플릿 설치

[-dc DCName]

으로 돌아가서 [메뉴](#menu)

## <a name="-urlcache"></a>-URLCache

CertUtil [옵션]-URLCache [URL | CRL | \* [삭제]]

표시 하거나 URL 캐시 항목을 삭제 합니다.

URL: 캐시 된 URL

CRL: 모든 캐시 된 CRL Url에 대해서만 작동 합니다.

\*: 모든 캐시 된 Url에 대해 작동 합니다.

삭제: 현재 사용자의 로컬 캐시에서 관련 Url을 삭제 합니다.

-F를 사용 하 여 특정 URL을 강제로 페치하고 캐시를 업데이트 합니다.

[-f] [-split]

으로 돌아가서 [메뉴](#menu)

## <a name="-pulse"></a>-펄스

CertUtil [Options] -pulse

펄스 자동 등록 이벤트

[-user]

으로 돌아가서 [메뉴](#menu)

## <a name="-machineinfo"></a>-MachineInfo

CertUtil [Options] -MachineInfo DomainName\MachineName$

컴퓨터 개체 정보 Active Directory 표시

으로 돌아가서 [메뉴](#menu)

## <a name="-dcinfo"></a>-DCInfo

CertUtil [Options] -DCInfo [Domain] [Verify | DeleteBad | DeleteAll]

도메인 컨트롤러 정보 표시

기본값은 확인 하지 않고 DC 인증서를 표시 하는 것입니다.

[-f] [-user] [-urlfetch] [-dc DCName] [-t 제한 시간]

> [!TIP]
> Active Directory Domain Services (AD DS) **도메인을 지정 하 고 도메인** 컨트롤러 ( **-dc**)를 지정 하는 기능은 Windows Server 2012에 추가 되었습니다. 명령을 성공적으로 실행 하려면의 구성원 인 계정을 사용 해야 **Domain Admins** 또는 **Enterprise Admins**합니다. 이 명령의 동작 수정 작업은 다음과 같습니다.</br>> 1.  도메인을 지정 하지 않으면 특정 도메인 컨트롤러를 지정 하지 않은 경우이 옵션의 기본 도메인 컨트롤러에서 처리 하는 도메인 컨트롤러의 목록을 반환 합니다.</br>> 2.  도메인을 지정 하지 않으면, 도메인 컨트롤러는 지정 하는 경우 지정된 된 도메인 컨트롤러에는 인증서의 보고서가 생성 됩니다.</br>> 3.  도메인을 지정 하는 경우 도메인 컨트롤러를 지정 하지 않으면 보고서 목록에서 각 도메인 컨트롤러에 대 한 인증서와 함께 도메인 컨트롤러 목록이 생성 됩니다.</br>> 4.  도메인 및 도메인 컨트롤러를 지정 하는 경우 대상된 도메인 컨트롤러에서 도메인 컨트롤러 목록이 생성 됩니다. 목록에서 각 도메인 컨트롤러에 대 한 인증서에 대 한 보고서도 생성 됩니다.

예를 들어 CPANDL-d c 1 이라는 도메인 컨트롤러와 CPANDL 라는 도메인이 가정 합니다. 다음 명령을 실행 하 여 CPANDL-DC1: certutil-dc CPANDL-dc1-dcinfo CPANDL에서 도메인 컨트롤러 및 해당 인증서 목록을 검색할 수 있습니다.

으로 돌아가서 [메뉴](#menu)

## <a name="-entinfo"></a>-EntInfo

CertUtil [Options] -EntInfo DomainName\MachineName$

[-f] [-user]

으로 돌아가서 [메뉴](#menu)

## <a name="-tcainfo"></a>-TCAInfo

CertUtil [옵션]-TCAInfo [DomainDN |-]

CA 정보 표시

[-f] [-enterprise] [-user] [-urlfetch] [-dc DCName] [-t 제한 시간]

으로 돌아가서 [메뉴](#menu)

## <a name="-scinfo"></a>-SCInfo

CertUtil [Options] -SCInfo [ReaderName [CRYPT_DELETEKEYSET]]

스마트 카드 정보 표시

CRYPT_DELETEKEYSET: 스마트 카드에서 모든 키 삭제

[-자동] [-split] [-urlfetch] [-t 제한 시간]

으로 돌아가서 [메뉴](#menu)

## <a name="-scroots"></a>-SCRoots

CertUtil [옵션]-SCRoots 업데이트 [+] [InputRootFile] [ReaderName]

CertUtil [옵션]-SCRoots save \@OutputRootFile [ReaderName]

CertUtil [옵션]-SCRoots 뷰 [InputRootFile | 판독기 이름

CertUtil [옵션]-SCRoots 삭제 [ReaderName]

스마트 카드 루트 인증서 관리

[-f] [-split] [-p 암호]

으로 돌아가서 [메뉴](#menu)

## <a name="-verifykeys"></a>-verifykeys

CertUtil [Options] -verifykeys [KeyContainerName CACertFile]

공개/개인 키 집합 확인

Cspparameters.keycontainername: 확인할 키의 키 컨테이너 이름입니다. 컴퓨터 키 기본값으로 지정 됩니다.  -을 사용 하 여 사용자에 게 사용자 키입니다.

CACertFile: 서명 또는 암호화 인증서 파일

인수를 지정 하지 않으면 각 서명 CA 인증서가 개인 키에 대해 확인 됩니다.

만 로컬 CA 또는 로컬 키에 대해이 작업을 수행할 수 있습니다.

[-f] [-user] [-자동] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-verify"></a>-확인

CertUtil [옵션]-CertFile 확인 [ApplicationPolicyList |-[IssuancePolicyList]]

CertUtil [옵션]-CertFile 확인 [CACertFile [CrossedCACertFile]]

CertUtil [옵션]-verify CRLFile CACertFile [IssuedCertFile]

CertUtil [옵션]-verify CRLFile CACertFile [DeltaCRLFile]

인증서, CRL 또는 체인 확인

CertFile 확인할 인증서

ApplicationPolicyList: 필요한 응용 프로그램 정책 Objectid의 선택적 쉼표로 구분 된 목록입니다.

IssuancePolicyList: 필요한 발급 정책 Objectid의 선택적 쉼표로 구분 된 목록입니다.

CACertFile: 확인할 발급 CA 인증서 (선택 사항)

CrossedCACertFile: CertFile에의 한 선택적 인증서 교차 인증

CRLFile 확인할 CRL

IssuedCertFile: CRLFile에서 적용 되는 선택적 발급 된 인증서

DeltaCRLFile: 선택적 델타 CRL

ApplicationPolicyList를 지정 하는 경우 체인 건물이 지정 된 응용 프로그램 정책에 대해 유효한 체인으로 제한 됩니다.

IssuancePolicyList 지정 된 경우 체인이 체인 지정된 발급 정책에 대 한 유효한 제한 됩니다.

CACertFile 지정 된 경우 CACertFile 필드 CertFile 또는 CRLFile에 대해 확인 됩니다.

CACertFile를 지정 하지 않으면 CertFile는 만들고 전체 체인을 확인 사용 됩니다.

CACertFile와 CrossedCACertFile 둘 모두를 지정 하는 경우 필드 CACertFile와 CrossedCACertFile CertFile에 대해 확인 됩니다.

IssuedCertFile를 지정 하는 경우 IssuedCertFile 필드 CRLFile에 대해 확인 됩니다.

DeltaCRLFile를 지정 하는 경우 DeltaCRLFile 필드 CRLFile에 대해 확인 됩니다.

[-f] [-enterprise] [-user] [-자동] [-split] [-urlfetch] [-t 제한 시간]

으로 돌아가서 [메뉴](#menu)

## <a name="-verifyctl"></a>-verifyCTL

CertUtil [옵션]-verifyCTL CTLObject [CertDir] [CertFile]

AuthRoot 확인 하거나 인증서 CTL 허용 되지 않습니다.

CTLObject 확인할 CTL을 식별 합니다.

- AuthRootWU: URL 캐시에서 AuthRoot CAB와 일치 하는 인증서를 읽습니다. -F를 사용 하 여 대신 Windows Update에서 다운로드 합니다.
- DisallowedWU: 허용 되지 않는 인증서 CAB 읽고 URL 캐시에서 인증서 저장소 파일을 사용할 수 없습니다.  -F를 사용 하 여 대신 Windows Update에서 다운로드 합니다.
- AuthRoot: 읽기 레지스트리 AuthRoot CTL을 캐시 합니다.  캐시 된 AuthRoot 및 허용 되지 않는 인증서 Ctl-f 및 레지스트리 업데이트를 강제로 이미 신뢰할 수 없는 CertFile 사용 합니다.
- 허용 안 함: 레지스트리 읽기 캐시 인증서 CTL 허용 되지 않습니다. -f AuthRoot와 마찬가지로 동일한 동작을 포함 합니다.
- CTLFileName: file 또는 http: CTL 또는 CAB 경로

CertDir: CTL 항목과 일치 하는 인증서를 포함 하는 폴더입니다. Http: 폴더 경로 경로 구분 기호로 끝나야 합니다. 여러 위치 AuthRoot 또는 허용 안 함 폴더를 지정 하지 않으면, 일치 하는 인증서에 대 한 검색 됩니다: 로컬 인증서 저장소, crypt32.dll 리소스, 로컬 URL 캐시 합니다. -F를 사용 하 여 필요한 경우 Windows Update에서 다운로드 합니다. 그렇지 않은 경우 기본값은 같은 폴더 또는 웹 사이트는 CTLObject으로입니다.

확인 하는 인증서를 포함 하는 CertFile: 파일입니다. 인증서는 CTL 항목에 대해를 검색 하 고 표시 하는 결과 일치 합니다. 대부분을의 기본 출력을 표시 하지 않습니다.

[-f] [-user] [-split]

으로 돌아가서 [메뉴](#menu)

## <a name="-sign"></a>-기호

CertUtil [옵션]-InFileList 서명 | 일련의 CRL OutFileList [SerialNumberList + dd: hh] [+ |-SerialNumberList |-수정 | \@ExtensionFile]

CertUtil [Options] -sign InFileList|SerialNumber|CRL OutFileList [#HashAlgorithm] [+AlternateSignatureAlgorithm | -AlternateSignatureAlgorithm]

CRL 또는 인증서 다시 서명

InFileList: 수정 하 고 다시 서명할 인증서 또는 CRL 파일의 쉼표로 구분 된 목록입니다.

SerialNumber 만들 인증서의 일련 번호입니다. 유효 기간 및 기타 옵션 없어야 합니다.

CRL: 빈 CRL을 만듭니다. 유효 기간 및 기타 옵션 없어야 합니다.

수정 된 인증서 또는 CRL 출력 파일의 OutFileList: 쉼표로 구분 된 목록입니다. 파일 수가 InFileList 일치 해야 합니다.

StartDate + dd:hh: 새 유효 기간: 더하기; 선택적 날짜 선택적 일과 시간 유효 기간. 둘 다 지정 하는 경우에 더하기 기호 (+) 구분 기호를 사용 합니다. "지금 [+ dd:hh]"는 현재 시간에서 시작 하려면 사용 합니다. 사용 하 여 "never" (대 한 Crl에만 해당)에 만료 날짜가 없습니다.

SerialNumberList: 추가 하거나 제거할 쉼표로 구분 된 일련 번호 목록입니다.

수정: 제거할 쉼표로 구분 된 확장 ObjectId 목록

\@ExtensionFile: 업데이트 하거나 제거할 확장을 포함 하는 INF 파일:

```
[Extensions]
     2.5.29.31 = ; Remove CRL Distribution Points extension
     2.5.29.15 = "{hex}" ; Update Key Usage extension
     _continue_="03 02 01 86"
```

HashAlgorithm # 기호 뒤에 오는 해시 알고리즘의 이름입니다.

AlternateSignatureAlgorithm: 대체 서명 알고리즘 지정자

빼기 기호를 사용할 경우 일련 번호와 확장이 제거 됩니다. 더하기 기호 하면 일련 번호는 CRL에 추가할 수 있습니다. CRL에서 항목을 제거할 때 목록 일련 번호 및 Objectid를 모두 포함할 수 있습니다. AlternateSignatureAlgorithm 앞에 빼기 기호 사용 되는 레거시 서명 형식을 하면 됩니다. AlternateSignatureAlgorithm 앞에 더하기 기호 하면 alternature 서명 형식을 사용할 수 있습니다. AlternateSignatureAlgorithm 지정 하지 않으면 인증서 또는 CRL에 서명 형식이 사용 됩니다.

[-nullsign] [-f] [-자동] [-Cert 인증서]

으로 돌아가서 [메뉴](#menu)

## <a name="-vroot"></a>-vroot

CertUtil [Options] -vroot [delete]

웹 가상 루트 및 파일 공유 만들기/삭제

으로 돌아가서 [메뉴](#menu)

## <a name="-vocsproot"></a>-vocsproot

CertUtil [Options] -vocsproot [delete]

OCSP 웹 프록시에 대 한 웹 가상 루트 만들기/삭제

으로 돌아가서 [메뉴](#menu)

## <a name="-addenrollmentserver"></a>-addEnrollmentServer

CertUtil [옵션]-addEnrollmentServer Kerberos | 사용자 이름 | ClientCertificate [AllowRenewalsOnly] [AllowKeyBasedRenewal]

등록 서버 응용 프로그램 추가

지정 된 CA에 대해 필요한 경우 등록 서버 응용 프로그램 및 응용 프로그램 풀을 추가 합니다. 이 명령은 이진 또는 패키지를 설치 하지 않습니다. 클라이언트 인증서 등록 서버에 연결 된 다음 인증 방법 중 하나입니다.

- Kerberos Kerberos SSL 자격 증명을 사용 하 여
- 이름 SSL 자격 증명에 명명 된 계정 사용
- ClientCertificate X.509 인증서 SSL 자격 증명 사용
- AllowRenewalsOnly: 이 URL을 통해이 CA에 갱신 요청을 제출할 수 있습니다.
- AllowKeyBasedRenewal-AD에 연결 된 계정이 없는 인증서를 사용할 수 있습니다. ClientCertificate 및 AllowRenewalsOnly 모드에만 적용 됩니다.

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-deleteenrollmentserver"></a>-deleteEnrollmentServer

CertUtil [옵션]-deleteEnrollmentServer Kerberos | 사용자 이름 | ClientCertificate

등록 서버 응용 프로그램 삭제

지정 된 CA에 대해 필요한 경우 등록 서버 응용 프로그램 및 응용 프로그램 풀을 삭제 합니다. 이 명령은 이진 또는 패키지를 제거 하지 않습니다. 클라이언트 인증서 등록 서버에 연결 된 다음 인증 방법 중 하나입니다.

1. Kerberos Kerberos SSL 자격 증명을 사용 하 여
2. 이름 SSL 자격 증명에 명명 된 계정 사용
3. ClientCertificate X.509 인증서 SSL 자격 증명 사용

[-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-addpolicyserver"></a>-addPolicyServer

CertUtil [옵션]-addPolicyServer Kerberos | 사용자 이름 | ClientCertificate [KeyBasedRenewal]

정책 서버 응용 프로그램 추가

필요한 경우 정책 서버 응용 프로그램 및 응용 프로그램 풀을 추가 합니다. 이 명령은 이진 또는 패키지를 설치 하지 않습니다. 클라이언트 인증서 정책 서버에 연결 된 다음 인증 방법 중 하나입니다.

- Kerberos Kerberos SSL 자격 증명을 사용 하 여
- 이름 SSL 자격 증명에 명명 된 계정 사용
- ClientCertificate X.509 인증서 SSL 자격 증명 사용
- KeyBasedRenewal: KeyBasedRenewal 템플릿이 포함 된 정책만 클라이언트에 반환 됩니다. 이 플래그는 사용자 이름 및 ClientCertificate 인증에만 적용 됩니다.

으로 돌아가서 [메뉴](#menu)

## <a name="-deletepolicyserver"></a>-deletePolicyServer

CertUtil [옵션]-deletePolicyServer Kerberos | 사용자 이름 | ClientCertificate [KeyBasedRenewal]

정책 서버 응용 프로그램 삭제

필요한 경우 정책 서버 응용 프로그램 및 응용 프로그램 풀을 삭제 합니다. 이 명령은 이진 또는 패키지를 제거 하지 않습니다. 클라이언트 인증서 정책 서버에 연결 된 다음 인증 방법 중 하나입니다.

1. Kerberos Kerberos SSL 자격 증명을 사용 하 여
2. 이름 SSL 자격 증명에 명명 된 계정 사용
3. ClientCertificate X.509 인증서 SSL 자격 증명 사용
4. KeyBasedRenewal: KeyBasedRenewal 정책 서버

으로 돌아가서 [메뉴](#menu)

## <a name="-oid"></a>-oid

CertUtil [옵션]-oid ObjectId [DisplayName | delete [LanguageId [Type]]]

CertUtil [Options] -oid GroupId

CertUtil [Options] -oid AlgId | AlgorithmName [GroupId]

ObjectId 표시 또는 표시 이름 설정

- ObjectId-ObjectId를 표시 하거나 표시 이름 추가
- 그룹 Id-GroupId 10 진수를 열거 하는 Objectid
- ObjectId 조회에 대 한 16 진수 AlgId AlgId-
- ObjectId 조회에 대 한 AlgorithmName-알고리즘 이름
- DS에 저장할 수 DisplayName-표시 이름
- 표시 이름을 삭제합니다-삭제
- LanguageId--Language Id (기본값: 1033)
- 유형--만들 DS 개체 유형: 1 (기본값), 2 (발급 정책), 3 (응용 프로그램 정책)
- -F를 사용 하 여 DS 개체를 만듭니다.

[-f]

으로 돌아가서 [메뉴](#menu)

## <a name="-error"></a>-오류

CertUtil [옵션]-오류 ErrorCode

오류 코드 메시지 텍스트 표시

으로 돌아가서 [메뉴](#menu)

## <a name="-getreg"></a>-getreg

CertUtil [Options] -getreg [{ca|restore|policy|exit|template|enroll|chain|PolicyServers}\[ProgId\]][RegistryValueName]

레지스트리 값 표시

발급 CA의 레지스트리 키 사용

복원 CA의 복원 레지스트리 키 사용

policy 정책 모듈의 레지스트리 키 사용

끝낸 첫 번째 끝내기 모듈의 레지스트리 키 사용

할당량 템플릿 레지스트리 키 사용 (사용자 템플릿에-user 사용)

등록 등록 레지스트리 키 사용 (사용자 컨텍스트에-user 사용)

미 체인 구성 레지스트리 키 사용

PolicyServers: 정책 서버 레지스트리 키 사용

ProgId: 정책 또는 끝내기 모듈의 ProgId 사용 (레지스트리 하위 키 이름)

RegistryValueName: 레지스트리 값 이름 (접두사 일치에\*"name" 사용)

값: 새 숫자, 문자열 또는 날짜 레지스트리 값 또는 파일 이름입니다. 숫자 값으로 시작 하는 경우 "+" 또는 "-", 새 값에 지정 된 비트 설정 되거나 기존 레지스트리 값에서 선택을 취소 합니다.

문자열 값으로 시작 하는 경우 "+" 또는 "-", 및 기존 값은 REG_MULTI_SZ 값, 문자열에 추가 하거나 기존 레지스트리 값에서 제거 합니다. REG_MULTI_SZ 값의 생성을 강제로 문자열 값의 끝에 "\n"을 추가 합니다.

값이 "\@"로 시작 하는 경우 나머지 값은 이진 값의 16 진수 텍스트 표현을 포함 하는 파일의 이름입니다. 올바른 파일을 참조 하지 않는 하는 경우 대신 구문 분석 [Date]와 [+ |-] [dd:hh]-더하기 또는 빼기 선택적 일과 시간에는 선택적 날짜입니다. 둘 다 지정 하는 경우 더하기 기호 (+) 또는 빼기 기호 (-) 구분 기호를 사용 합니다. 현재 시간을 기준으로 날짜에 대 한 "현재 날짜 + dd:hh"를 사용 합니다.

"Chain\ChainCacheResyncFiletime \@now"를 사용 하 여 캐시 된 crl을 효과적으로 플러시합니다.

[-f] [-user] [-GroupPolicy] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-setreg"></a>-setreg

CertUtil [Options] -setreg [{ca|restore|policy|exit|template|enroll|chain|PolicyServers}\[ProgId\]]RegistryValueName Value

레지스트리 값 설정

발급 CA의 레지스트리 키 사용

복원 CA의 복원 레지스트리 키 사용

policy 정책 모듈의 레지스트리 키 사용

끝낸 첫 번째 끝내기 모듈의 레지스트리 키 사용

할당량 템플릿 레지스트리 키 사용 (사용자 템플릿에-user 사용)

등록 등록 레지스트리 키 사용 (사용자 컨텍스트에-user 사용)

미 체인 구성 레지스트리 키 사용

PolicyServers: 정책 서버 레지스트리 키 사용

ProgId: 정책 또는 끝내기 모듈의 ProgId 사용 (레지스트리 하위 키 이름)

RegistryValueName: 레지스트리 값 이름 (접두사 일치에\*"name" 사용)

값: 새 숫자, 문자열 또는 날짜 레지스트리 값 또는 파일 이름입니다. 숫자 값으로 시작 하는 경우 "+" 또는 "-", 새 값에 지정 된 비트 설정 되거나 기존 레지스트리 값에서 선택을 취소 합니다.

문자열 값으로 시작 하는 경우 "+" 또는 "-", 및 기존 값은 REG_MULTI_SZ 값, 문자열에 추가 하거나 기존 레지스트리 값에서 제거 합니다. REG_MULTI_SZ 값의 생성을 강제로 문자열 값의 끝에 "\n"을 추가 합니다.

값이 "\@"로 시작 하는 경우 나머지 값은 이진 값의 16 진수 텍스트 표현을 포함 하는 파일의 이름입니다. 올바른 파일을 참조 하지 않는 하는 경우 대신 구문 분석 [Date]와 [+ |-] [dd:hh]-더하기 또는 빼기 선택적 일과 시간에는 선택적 날짜입니다. 둘 다 지정 하는 경우 더하기 기호 (+) 또는 빼기 기호 (-) 구분 기호를 사용 합니다. 현재 시간을 기준으로 날짜에 대 한 "현재 날짜 + dd:hh"를 사용 합니다.

"Chain\ChainCacheResyncFiletime \@now"를 사용 하 여 캐시 된 crl을 효과적으로 플러시합니다.

[-f] [-user] [-GroupPolicy] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-delreg"></a>-delreg

CertUtil [Options] -delreg [{ca|restore|policy|exit|template|enroll|chain|PolicyServers}\[ProgId\]][RegistryValueName]

레지스트리 값 삭제

발급 CA의 레지스트리 키 사용

복원 CA의 복원 레지스트리 키 사용

policy 정책 모듈의 레지스트리 키 사용

끝낸 첫 번째 끝내기 모듈의 레지스트리 키 사용

할당량 템플릿 레지스트리 키 사용 (사용자 템플릿에-user 사용)

등록 등록 레지스트리 키 사용 (사용자 컨텍스트에-user 사용)

미 체인 구성 레지스트리 키 사용

PolicyServers: 정책 서버 레지스트리 키 사용

ProgId: 정책 또는 끝내기 모듈의 ProgId 사용 (레지스트리 하위 키 이름)

RegistryValueName: 레지스트리 값 이름 (접두사 일치에\*"name" 사용)

값: 새 숫자, 문자열 또는 날짜 레지스트리 값 또는 파일 이름입니다. 숫자 값으로 시작 하는 경우 "+" 또는 "-", 새 값에 지정 된 비트 설정 되거나 기존 레지스트리 값에서 선택을 취소 합니다.

문자열 값으로 시작 하는 경우 "+" 또는 "-", 및 기존 값은 REG_MULTI_SZ 값, 문자열에 추가 하거나 기존 레지스트리 값에서 제거 합니다. REG_MULTI_SZ 값의 생성을 강제로 문자열 값의 끝에 "\n"을 추가 합니다.

값이 "\@"로 시작 하는 경우 나머지 값은 이진 값의 16 진수 텍스트 표현을 포함 하는 파일의 이름입니다. 올바른 파일을 참조 하지 않는 하는 경우 대신 구문 분석 [Date]와 [+ |-] [dd:hh]-더하기 또는 빼기 선택적 일과 시간에는 선택적 날짜입니다. 둘 다 지정 하는 경우 더하기 기호 (+) 또는 빼기 기호 (-) 구분 기호를 사용 합니다. 현재 시간을 기준으로 날짜에 대 한 "현재 날짜 + dd:hh"를 사용 합니다.

"Chain\ChainCacheResyncFiletime \@now"를 사용 하 여 캐시 된 crl을 효과적으로 플러시합니다.

[-f] [-user] [-GroupPolicy] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-importkms"></a>-ImportKMS

CertUtil [Options] -ImportKMS UserKeyAndCertFile [CertId]

키 보관을 위해 사용자 키 및 인증서를 서버 데이터베이스로 가져오기

UserKeyAndCertFile--보관할 사용자 개인 키 및 인증서를 포함 하는 데이터 파일입니다.  이 다음 중 하나일 수 있습니다.

- Exchange Server KMS (키 관리) 내보내기 파일
- PFX 파일

CertId: KMS 내보내기 파일 암호 해독 인증서 일치 토큰입니다.  참조 [-저장](#-store)합니다.

-F를 사용 하 여 CA에서 발급 되지 않으며 인증서를 가져옵니다.

[-f] [-자동] [-split] [-config Machine\CAName] [-p 암호] [-symkeyalg SymmetricKeyAlgorithm [, KeyLength]]

으로 돌아가서 [메뉴](#menu)

## <a name="-importcert"></a>-ImportCert

CertUtil [옵션]-ImportCert Certfile [ExistingRow]

데이터베이스에 인증서 파일 가져오기

동일한 키에 대해 보류 중인 요청 대신 ExistingRow를 사용 하 여 인증서를 가져옵니다.

-F를 사용 하 여 CA에서 발급 되지 않으며 인증서를 가져옵니다.

외래 인증서 가져오기를 지원 하도록 CA를 구성 해야 할 수도 있습니다. certutil-setreg ca\KRAFlags + KRAF_ENABLEFOREIGN

[-f] [-config Machine\CAName]

으로 돌아가서 [메뉴](#menu)

## <a name="-getkey"></a>-GetKey

CertUtil [옵션]-GetKey SearchToken [RecoveryBlobOutFile]

CertUtil [옵션]-GetKey SearchToken 스크립트 OutputScriptFile

CertUtil [옵션]-GetKey SearchToken 검색 | OutputFileBaseName 복구

보관 된 개인 키 복구 blob 검색, 복구 스크립트 생성 또는 보관 된 키 복구

스크립트: 키를 검색 및 복구 하는 스크립트를 생성 합니다 (일치 하는 복구 후보가 여러 개 있는 경우 또는 출력 파일이 지정 되지 않은 경우 기본 동작).

검색: 하나 이상의 키 복구 Blob (정확히 하나의 일치 하는 복구 후보가 발견 되는 경우 기본 동작 및 출력 파일이 지정 된 경우)을 검색 합니다.

복구: 한 번에 개인 키 검색 및 복구 (키 복구 에이전트 인증서 및 개인 키 필요)

토큰 복구할 키와 인증서를 선택 하는 데 사용 됩니다.

다음 중 하나일 수 있습니다.

1. 인증서 일반 이름
2. 인증서 일련 번호
3. 인증서의 sha-1 해시 (지문)
4. 인증서 KeyId sha-1 해시 (주체 키 식별자)
5. 요청자 이름 (도메인 \ 사용자)
6. UPN (사용자\@도메인)

RecoveryBlobOutFile 파일: 인증서 체인 및 연결 된 개인 키를 포함 하는 출력 파일은 하나 이상의 키 복구 에이전트 인증서로 암호화 됩니다.

OutputScriptFile: 프라이빗 키를 검색하고 복구하기 위한 배치 스크립트가 포함된 출력 파일입니다.

OutputFileBaseName: 출력 파일 기본 이름입니다. 검색에 대 한 모든 확장 잘리고는 인증서 문자열 및.rec 확장 각 키 복구 blob에 대 한 추가 됩니다.  각 파일에는 인증서 체인과 연결된 프라이빗 키가 들어 있으며, 여전히 하나 이상의 키 복구 에이전트 인증서로 암호화되어 있습니다. 복구에 대 한 모든 확장 잘리고.p12 확장명이 추가 됩니다.  PFX 파일로 저장되는 복구된 인증서 체인 및 관련 프라이빗 키가 포함되어 있습니다.

[-f] [-UnicodeText] [-silent] [-config Machine\CAName] [-p Password] [-ProtectTo SAMNameAndSIDList] [-csp Provider]

으로 돌아가서 [메뉴](#menu)

## <a name="-recoverkey"></a>-RecoverKey

CertUtil [옵션]-RecoverKey RecoveryBlobInFile [PFXOutFile [RecipientIndex]]

보관 된 개인 키 복구

[-f] [-user] [-자동] [-split] [-p 암호] [-ProtectTo SAMNameAndSIDList] [-csp 공급자] [-t 제한 시간]

으로 돌아가서 [메뉴](#menu)

## <a name="-mergepfx"></a>-MergePFX

CertUtil [옵션]-MergePFX PFXInFileList PFXOutFile [ExtendedProperties]

PFXInFileList: 쉼표로 구분 된 PFX 입력 파일 목록

PFXOutFile: PFX 출력 파일

ExtendedProperties 확장 속성 포함

명령줄에 지정 된 암호가 쉼표로 구분 된 암호 목록입니다.  둘 이상의 암호를 지정 하면 출력 파일에 대 한 마지막 암호가 사용 됩니다.  암호를 하나만 제공 하거나 마지막 암호가 "\*" 이면 사용자에 게 출력 파일 암호를 입력 하 라는 메시지가 표시 됩니다.

[-f] [-user] [-split] [-p Password] [-ProtectTo SAMNameAndSIDList] [-csp Provider]

으로 돌아가서 [메뉴](#menu)

## <a name="-convertepf"></a>-ConvertEPF

CertUtil [옵션]-ConvertEPF PFXInFileList EPFOutFile [cast | cast-] [V3CACertId] [, 솔트]

PFX 파일에 대 한 PFX 파일 변환

PFXInFileList: 쉼표로 구분 된 PFX 입력 파일 목록

EPF EPF 출력 파일

캐스팅이 CAST 64 암호화 사용

cast-: CAST 64 암호화 사용 (내보내기)

V3CACertId: V3 CA 인증서 일치 토큰입니다.  참조 [-저장](#-store) 인증서 설명 합니다.

솔트 EPF 출력 파일 솔트 문자열

명령줄에 지정 된 암호가 쉼표로 구분 된 암호 목록입니다. 둘 이상의 암호를 지정 하면 출력 파일에 대 한 마지막 암호가 사용 됩니다.  암호를 하나만 제공 하거나 마지막 암호가 "\*" 이면 사용자에 게 출력 파일 암호를 입력 하 라는 메시지가 표시 됩니다.

[-f] [-자동] [-split] [-dc DCName] [-p 암호] [-csp 공급자]

으로 돌아가서 [메뉴](#menu)

## <a name="options"></a>변수

이 섹션의 명령을 사용 하 여 지정할 수 있는 옵션을 정의 합니다.

|변수|설명|
|-------|-----------|
|-nullsign|데이터의 해시를 사용 하 여 서명으로|
|-f|무조건 덮어쓰기|
|-엔터프라이즈|로컬 컴퓨터 엔터프라이즈 레지스트리 인증서 저장소를 사용 하 여|
|-사용자|HKEY_CURRENT_USER 키 또는 인증서 저장소를 사용 하 여|
|-그룹 정책|사용 하 여 그룹 정책 인증서 저장소|
|-ut|사용자 템플릿 표시|
|-mt|컴퓨터 템플릿 표시|
|유니코드|유니코드에서 리디렉션된 출력 쓰기|
|-UnicodeText|유니코드로 출력 파일을 기록 합니다.|
|-gmt|GMT로 표시 시간|
|-초|시간을 초와 밀리초로 표시|
|-자동|자동 플래그를 사용 하 여 암호화 컨텍스트를 가져오려고 합니다.|
|-분할|포함 된 ASN.1 요소를 분할 하 고 파일에 저장|
|-v|작업 세부 정보 표시|
|-privatekey|암호 및 프라이빗 데이터 표시|
|-핀 고정|스마트 카드 PIN|
|-urlfetch|검색 하 고 인증서 AIA 및 CDP Crl 확인|
|-config Machine\CAName|CA 및 컴퓨터 이름 문자열|
|-PolicyServer URLOrId|정책 서버 URL 또는 id입니다. 선택할 U / I,-PolicyServer를 사용 합니다. 모든 정책 서버에 대해-PolicyServer를 사용 합니다.\*|
|아닌 익명이|익명 SSL 자격 증명을 사용 하 여|
|-Kerberos|Kerberos SSL 자격 증명을 사용 하 여|
|-ClientCertificate ClientCertId|SSL 되는 X.509 인증서 자격 증명을 사용 합니다. 선택할 U / I, clientCertificate 사용 합니다.|
|-UserName 사용자 이름|SSL 자격 증명에 대 한 명명 된 계정을 사용 합니다. 선택할 U / I,-UserName을 사용 합니다.|
|-인증서 인증서|서명 인증서|
|-dc DCName|특정 도메인 컨트롤러를 대상으로|
|-RestrictionList 제한|쉼표로 구분 된 제한 목록입니다. 각 제한 열 이름, 관계형 연산자 및 상수 정수, 문자열 또는 날짜 구성 됩니다. 한 열 이름 수 앞에 더하기 또는 빼기 기호 정렬 순서를 나타냅니다. 예를 들면 다음과 같습니다.</br>"RequestId 47 ="</br>"+ RequesterName > = a, RequesterName < b"</br>"-RequesterName > 도메인, 처리 = 21"|
|-ColumnList 아웃|쉼표로 구분 된 열 목록|
|-p 암호|암호|
|-ProtectTo SAMNameAndSIDList|쉼표로 구분 된 이름/SID 목록 SAM|
|-csp 공급자|공급자|
|-t 제한 시간|URL 인출 제한 시간 (밀리초)|
|-symkeyalg SymmetricKeyAlgorithm [, 키 길이]|선택적인 키 길이가 있는 대칭 키 알고리즘의 이름입니다. 예를 들면 다음과 같습니다. AES, 128 또는 3DES|

으로 돌아가서 [메뉴](#menu)

## <a name="additional-certutil-examples"></a>추가 certutil 예제

이 명령을 사용 하는 방법의 몇 가지 예를 참조 하십시오.

1. [명령줄에서 Active Directory 인증서 서비스 (AD CS)를 관리 하기 위한 Certutil 예제](https://social.technet.microsoft.com/wiki/contents/articles/3063.certutil-examples-for-managing-active-directory-certificate-services-ad-cs-from-the-command-line.aspx)
2. [인증서 관리를 위한 Certutil 작업](https://technet.microsoft.com/library/cc772898.aspx)
3. [CertUtil 명령줄 도구를 사용 하 여 이진 요청 내보내기 연습](https://social.technet.microsoft.com/wiki/contents/articles/7573.active-directory-certificate-services-pki-key-archival-and-management.aspx)
4. [루트 CA 인증서 갱신](https://social.technet.microsoft.com/wiki/contents/articles/2016.root-ca-certificate-renewal.aspx)
5. [Certutil.exe](https://msdn.microsoft.com/subscriptions/cc773087.aspx)

으로 돌아가서 [메뉴](#menu)
