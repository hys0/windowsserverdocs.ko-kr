---
title: verifier
description: 드라이버 검증 도구 관리자를 실행 하는 확인 프로그램에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 782173d6-f196-4bc4-a547-76109829453c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7c8ee51a5a085b97093c417a143ee36cffbc979
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931330"
---
# <a name="verifier"></a>verifier

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

드라이버 확인 프로그램 관리자입니다.

## <a name="syntax"></a>구문
```
verifier /standard /driver <name> [<name> ...]
verifier /standard /all
verifier [/flags <flags>] [/faults [<probability> [<tags> [<applications> [<minutes>]]]] /driver <name> [<name>...]
verifier [/flags FLAGS] [/faults [<probability> [<tags> [<applications> [<minutes>]]]] /all
verifier /querysettings
verifier /volatile /flags <flags>
verifier /volatile /adddriver <name> [<name>...]
verifier /volatile /removedriver <name> [<name>...]
verifier /volatile /faults [<probability> [<tags> [<applications>]]
verifier /reset
verifier /query
verifier /log <LogFileName> [/interval <seconds>]
```
#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|\<flags>|비트 조합 하 여 10 진수 또는 16 진수 숫자 여야 합니다.<p>-   **값: 설명**<br />-   **비트 0:** 특수 풀 검사<br />-   **비트 1:** irql 확인 강제 적용<br />-   **비트 2:** 리소스가 부족 한 시뮬레이션<br />-   **비트 3:** 풀 추적<br />-   **비트 4:** I/o 확인<br />-   **비트 5:** 교착 상태 검색<br />-   **비트 6:** 사용 안 함<br />-   **비트 7:** DMA 확인<br />-   **8 비트:** 보안 검사<br />-   **비트 9:** 강제로 보류 중인 i/o 요청<br />-   **10 비트:** IRP 로깅<br />-   **비트 11:** 기타 검사<p>예를 들어 **/flags 27** 은 **/flags 0x1b** 와 동일 합니다.|
|/volatile|시스템 다시 시작 하지 않고 확인 프로그램 설정을 동적으로 변경 하는 데 사용 합니다. 시스템 다시 시작 될 때 모든 새 설정이 손실 됩니다.|
|\<probability>|1에서 10000 오류 주입 확률 지정 사이의 숫자입니다. 예를 들어 100 지정 오류 주입 확률이 1% (100/10000)를 의미 합니다.<p>이 매개 변수를 지정 하지 않으면 기본 확률 6%가 사용 됩니다.|
|\<tags>|공백 문자로 구분 된 오류와 삽입 되는 풀 태그를 지정 합니다. 이 매개 변수를 지정 하지 않으면 모든 풀 할당 오류와 삽입할 수 있습니다.|
|\<applications>|공백 문자로 구분 된 오류와 삽입 되는 애플리케이션의 이미지 파일 이름을 지정 합니다. 이 매개 변수를 지정 하지 않으면 모든 애플리케이션에 리소스 부족 시뮬레이션에 걸릴 수 있습니다.|
|\<minutes>|삽입이 발생 하는 동안 오류는 없음을 분 후에 다시 부팅 한 후 기간의 길이 지정 하는 양수입니다. 이 매개 변수를 지정 하지 않으면 8 분의 기본 길이가 사용 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)