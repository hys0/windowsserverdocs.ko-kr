---
title: ntfrsutl
description: Ntfrsutl 명령에 대 한 참조 항목으로, NT 파일 복제 서비스 (NTFRS)의 내부 테이블, 스레드 및 메모리 정보를 덤프 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f931d916888a372d66a1cc06cb7543067b9b9d3b
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472769"
---
# <a name="ntfrsutl"></a>ntfrsutl

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로컬 및 원격 서버 모두에서 NT 파일 복제 서비스 (NTFRS)에 대 한 내부 테이블, 스레드 및 메모리 정보를 덤프 합니다. SCM (서비스 제어 관리자)의 NTFRS에 대 한 복구 설정은 컴퓨터에서 중요 한 로그 이벤트를 찾고 유지 하는 데 중요할 수 있습니다. 이 도구는 이러한 설정을 검토 하는 편리한 방법을 제공 합니다.

## <a name="syntax"></a>구문

```
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]
ntfrsutl[memory|threads|stage][<computer>]
ntfrsutl ds[<computer>]
ntfrsutl [sets][<computer>]
ntfrsutl [version][<computer>]
ntfrsutl poll[/quickly[=[<n>]]][/slowly[=[<n>]]][/now][<computer>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| idtable | ID 테이블을 지정 합니다. |
| 구성 테이블 | FRS 구성 테이블을 지정 합니다. |
| 인 로그 | 인바운드 로그를 지정 합니다. |
| 아웃 로그 | 아웃 바운드 로그를 지정 합니다. |
| `<computer>` | 컴퓨터를 지정합니다. |
| 메모리 | 메모리 사용량을 지정 합니다. |
| 스레드 | 메모리 사용량을 지정 합니다. |
| stage(단계) | 메모리 사용량을 지정 합니다. |
| ds | DS의 NTFRS 서비스의 뷰를 나열합니다. |
| 설정 | 활성 복제본 집합을 지정 합니다. |
| 버전 | API 및 NTFRS 서비스 버전을 지정합니다. |
| 설문 조사 | 현재 폴링 간격을 지정합니다.<ul><li>`/quickly`-안정적인 구성을 검색할 때까지 빠르게 폴링합니다.</li><li>`/quickly=`-기본 시간 (분) 마다 빠르게 폴링합니다.</li><li>`/quickly=<n>`- *N* 분 마다 빠르게 폴링합니다.</li><li>`/slowly`-안정적인 구성을 검색할 때까지 느리게 폴링합니다.</li><li>`/slowly=`-기본 시간 (분) 마다 천천히 폴링합니다.</li><li>`/slowly=<n>`- *N* 분 마다 천천히 폴링합니다.</li><li>`/now`-지금 폴링합니다.</li></ul>|
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예제

파일 복제에 대 한 폴링 간격을 확인 하려면 다음을 입력 합니다.

```
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1
```

현재 NTFRS API (응용 프로그램 인터페이스) 버전을 확인 하려면 다음을 입력 합니다.

```
C:\Program Files\SupportTools>ntfrsutl version
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
