---
title: nslookup
description: DNS (Domain Name System) 인프라를 진단 하는 데 사용할 수 있는 정보를 표시 하는 nslookup 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 41516932-7833-434a-aa92-b4cf0f9a7ef7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 589b8dd5e1244a5aeb27f33b4985f07b776bc7bd
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721156"
---
# <a name="nslookup"></a>nslookup

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

도메인 이름 시스템 (DNS) 인프라를 진단 하는 데 사용할 수 있는 정보를 표시 합니다. 이 도구를 사용 하기 전에 DNS의 작동 원리에 대해 잘 알고 있어야 합니다. Nslookup 명령줄 도구는 TCP/IP 프로토콜을 설치한 경우에만 사용할 수 있습니다.

Nslookup 명령줄 도구에는 대화형 및 비 대화형 모드의 두 가지 모드가 있습니다.

단일 데이터만 조회 해야 하는 경우 비 대화형 모드를 사용 하는 것이 좋습니다. 첫 번째 매개 변수 이름 또는 조회 하려고 하는 컴퓨터의 IP 주소를 입력 합니다. 두 번째 매개 변수 이름 또는 DNS 이름 서버의 IP 주소를 입력 합니다. 두 번째 인수를 생략 하면 **nslookup** 기본 DNS 이름 서버를 사용 합니다.

둘 이상의 데이터 부분을 조회 해야 할 경우에 대화형 모드를 사용할 수 있습니다. 첫 번째 매개 변수 이름 또는 두 번째 매개 변수에 대 한 DNS 이름 서버의 IP 주소를 하이픈 (-)를 입력 합니다. 두 매개 변수를 모두 생략 하면 도구는 기본 DNS 이름 서버를 사용 합니다. 대화형 모드를 사용 하는 동안 다음을 수행할 수 있습니다.

- CTRL + B를 눌러 언제 든 지 대화형 명령을 중단 합니다.

- **Exit를 입력 하**여 종료 합니다.

- 기본 제공 명령을 컴퓨터 이름 앞에 이스케이프 문자 ( \) . 인식할 수 없는 명령에는 컴퓨터 이름으로 해석 됩니다.

## <a name="syntax"></a>구문

```
nslookup [exit | finger | help | ls | lserver | root | server | set | view] [options]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| [nslookup 종료](nslookup-exit-command.md) | Nslookup 명령줄 도구를 종료 합니다. |
| [nslookup 손가락](nslookup-finger-command.md) | 현재 컴퓨터에서 손가락 서버와 연결합니다. |
| [nslookup help](nslookup-help.md) | 하위 명령에 대 한 간단한 요약을 표시 합니다. |
| [nslookup ls](nslookup-ls.md) | DNS 도메인에 대 한 정보를 나열합니다. |
| [nslookup lserver](nslookup-lserver.md) | 지정 된 DNS 도메인의 기본 서버를 변경합니다. |
| [nslookup root](nslookup-root.md) | DNS 도메인 네임 스페이스의 루트에 대 한 서버에 기본 서버를 변경합니다. |
| [nslookup server](nslookup-server.md) | 지정 된 DNS 도메인의 기본 서버를 변경합니다. |
| [nslookup set](nslookup-set.md) | 구성 설정에 영향을 주는 변경 방법을 조회 함수입니다. |
| [nslookup set all](nslookup-set-all.md) | 구성 설정의 현재 값을 인쇄합니다. |
| [nslookup set class](nslookup-set-class.md) | 쿼리 클래스를 변경 합니다. 클래스는 프로토콜 그룹 정보를 지정합니다. |
| [nslookup set d2](nslookup-set-d2.md) | 철저 한 디버깅 모드를 설정 하거나 해제 합니다. 모든 패킷이 모든 필드를 표시 합니다. |
| [nslookup set debug](nslookup-set-debug.md) | 디버깅 모드를 설정 하거나 해제 합니다. |
| [nslookup set domain](nslookup-set-domain.md) | 지정 된 이름과 기본 DNS 도메인 이름을 변경 합니다. |
| [nslookup set port](nslookup-set-port.md) | 지정 된 값으로 기본 TCP/UDP DNS 이름 서버 포트를 변경 합니다. |
| [nslookup set querytype](nslookup-set-querytype.md) | 쿼리에 대 한 리소스 레코드 종류를 변경합니다. |
| [nslookup set recurse](nslookup-set-recurse.md) | 정보가 없는 경우 다른 서버를 쿼리하도록 DNS 이름 서버에 지시 합니다. |
| [nslookup set retry](nslookup-set-retry.md) | 재시도 횟수를 설정합니다. |
| [nslookup set root](nslookup-set-root.md) | 쿼리에 사용 되는 루트 서버 이름을 변경 합니다. |
| [nslookup set search](nslookup-set-search.md) | 응답을 받을 때까지 요청에 DNS 도메인 검색 목록에 DNS 도메인 이름을 추가 합니다. 집합과 조회 요청 하나 이상의 기간을 포함 하는 경우에 적용 됩니다 있지만 뒤에 마침표 종료 하지 마십시오. |
| [nslookup set srchlist](nslookup-set-srchlist.md) | 기본 DNS 도메인 이름 및 검색 목록을 변경합니다. |
| [nslookup set timeout](nslookup-set-timeout.md) | 초기 요청에 회신을 기다릴 시간 (초) 수를 변경 합니다. |
| [nslookup set type](nslookup-set-type.md) | 쿼리에 대 한 리소스 레코드 종류를 변경합니다. |
| [nslookup set vc](nslookup-set-vc.md) | 가상 회로 보낼 때 서버에 요청을 사용 하지 않는 또는 사용 하도록 지정 합니다. |
| [nslookup view](nslookup-view.md) | 정렬 하 고는 이전 출력 나열 **ls** 하위 명령 또는 명령입니다. |

### <a name="remarks"></a>설명

- *Computertofind* 가 IP 주소이 고 쿼리가 **A** 또는 **PTR** 리소스 레코드 종류에 대 한 것 이면 컴퓨터 이름이 반환 됩니다.

- *Computertofind* 가 이름이 고 마침표가 없으면 기본 DNS 도메인 이름이 이름에 추가 됩니다. 이 동작은 다음의 상태에 따라 **설정** 하위 명령: **도메인**, **srchlist**, **defname**, 및 **검색**합니다.

- *Computertofind*대신 하이픈 (-)을 입력 하면 명령 프롬프트가 **nslookup** 대화형 모드로 변경 됩니다.

- 조회 요청이 실패 하는 경우 명령줄 도구는 다음과 같은 오류 메시지를 제공 합니다.

  | 오류 메시지 | Description |
  | ------------- | ----------- |
  | 시간 초과 됨 |특정 시간이 지난 후 서버에서 요청에 응답 하지 않았습니다. [Nslookup set timeout](nslookup-set-timeout.md) 명령을 사용 하 여 시간 제한 기간을 설정할 수 있습니다. [Nslookup 설정 다시 시도](nslookup-set-retry.md) 명령을 사용 하 여 다시 시도 횟수를 설정할 수 있습니다. |
  | 서버에서 응답 없음 | DNS 이름 서버는 서버 컴퓨터에서 실행 됩니다. |
  | 레코드 없음 | 컴퓨터 이름이 유효한 경우에도 DNS 이름 서버에는 컴퓨터에 대 한 현재 쿼리 유형의 리소스 레코드가 없습니다. 쿼리 형식은 [nslookup set querytype](nslookup-set-querytype.md) 명령을 사용 하 여 지정 합니다. |
  | 존재 하지 않는 도메인 | 컴퓨터 또는 DNS 도메인 이름이 없습니다. |
  | 연결이 거부 되었거나 네트워크에 연결할 수 없습니다. | DNS 이름 서버 또는 손가락 서버에 연결할 수 없습니다. 이 오류는 일반적으로 **ls** 및 **핑거** 요청에서 발생 합니다. |
  | 서버 오류 | DNS 이름 서버 데이터베이스의 내부 불일치를 발견 하 고 유효한 응답을 반환할 수 없습니다. |
  | 함 | DNS 이름 서버 요청을 거부 했습니다. |
  | 서식 오류 | DNS 이름 서버 요청 패킷의 형식이 없음을 발견 합니다. 에 오류가 있다는 의미일 수 있습니다 **nslookup**합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
