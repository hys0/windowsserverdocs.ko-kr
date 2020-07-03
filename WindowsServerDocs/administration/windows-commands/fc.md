---
title: fc
description: 두 파일 또는 파일 집합을 비교 하 여 두 파일 또는 파일 집합 간의 차이점을 표시 하는 fc 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 485fc3d8-b7c5-496d-87be-0011112f27d5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6d9e12853d2634f7e7bcbd976b6c301f8e02c0dc
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930483"
---
# <a name="fc"></a>fc

두 개의 파일 또는 파일의 설정와 비교 이들 간의 차이 표시 합니다.

## <a name="syntax"></a>구문

```
fc /a [/c] [/l] [/lb<n>] [/n] [/off[line]] [/t] [/u] [/w] [/<nnnn>] [<drive1>:][<path1>]<filename1> [<drive2>:][<path2>]<filename2>
fc /b [<drive1:>][<path1>]<filename1> [<drive2:>][<path2>]<filename2>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| /a | ASCII 비교의 출력을 줄여서 표시 합니다. 다른 줄을 모두 표시 하는 대신 **fc** 차이의 각 집합에 대 한 첫 번째 및 마지막 줄이 표시 됩니다. |
| /b | 바이트 단위로 이진 모드에서 두 개의 파일을 비교 하 여 불일치를 찾은 후 파일을 다시 동기화를 시도 하지 않습니다. 이 다음과 같은 파일 확장명을 가진 파일을 비교 하기 위한 기본 모드:.exe,.com,.sys,.obj,.lib 또는.bin 합니다. |
| /C | 대/소문자를 무시합니다. |
| /l | 비교는 ASCII 모드, 및의 파일 줄 단위로 불일치가 발견 되 면 파일을 다시 동기화 하려고 합니다. 이 다음 파일 확장명의 파일을 제외 하 고 파일을 비교 하기 위한 기본 모드:.exe,.com,.sys,.obj,.lib 또는.bin 합니다. |
| /lb`<n>` | 내부 버퍼의 줄 수를 *N*으로 설정 합니다. 줄 버퍼의 기본 길이는 100 줄입니다. 파일 비교 하는 100 개 이상의 연속 된 여러 줄에 있으면 **fc** 는 비교를 취소 합니다. |
| /n | ASCII 비교 하는 동안 줄 번호를 표시 합니다. |
| 설정 / 해제 [line] | 오프 라인 특성 집합이 있는 파일을 건너뛰지 않습니다. |
| /t | 방지 **fc** 탭을 공백으로 변환 합니다. 기본 동작은 탭 각각 8 번째 문자 위치에서 중지 공백으로 처리 하는 것입니다. |
| /U | 유니코드 텍스트 파일로 파일을 비교합니다. |
| /w | 비교 시 공백 (즉, 탭과 공백)을 압축합니다. 한 줄에 많은 연속 된 공백이 나 탭 **/w** 단일 공간으로 이러한 문자를 처리 합니다. 와 함께 사용할 경우 **/w**, **fc** 줄의 시작과 끝에 있는 공백을 무시 합니다. |
| /`<nnnn>` | 전에 일치 하지 않습니다 다음 일치 하는 연속 된 줄의 수를 지정 **fc** 가 파일을 다시 동기화 할 수 있습니다. 파일의 일치 하는 줄 수가 *nnnn*보다 작은 경우 **fc** 는 일치 하는 줄을 차이로 표시 합니다. 기본값은 2입니다. |
| `[<drive1>:][<path1>]<filename1>` | 첫 번째 파일의 이름 또는 집합 비교 하는 파일의 위치를 지정 합니다. *filename1* 가 필요 합니다. |
| `[<drive2>:][<path2>]<filename2>` | 두 번째 파일의 이름 또는 집합 비교 하는 파일의 위치를 지정 합니다. *filename2* 가 필요 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 이 명령은 c:\WINDOWS\fc.exe에 의해 implemeted 됩니다. PowerShell 내에서이 명령을 사용할 수 있지만 ' fc '가 형식-사용자 지정의 별칭 이기도 하므로 전체 실행 파일 (fc.exe)의 철자를 확인 해야 합니다.

- ASCII 비교에 **fc** 를 사용 하는 경우 **fc** 는 두 파일 간의 차이점을 다음과 같은 순서로 표시 합니다.

  - 첫 번째 파일의 이름

  - 파일 간에 다른 *filename1* 의 줄

  - 두 파일에서 일치 하는 첫 번째 줄

  - 두 번째 파일의 이름

  - *Filename2* 에서 다른 줄

  - 일치 하는 첫 번째 줄

- **/b** 다음 구문에서 이진 비교를 수행 하는 동안 발견 된 불일치를 표시 합니다.

    `\<XXXXXXXX: YY ZZ>`

    *Xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx* 값은 파일의 시작 부분에서 측정 되는 바이트 쌍의 상대 16 진수 주소를 지정 합니다. 주소는 00000000에서 시작 합니다. *YY* 및 *ZZ* 의 16 진수 값은 각각 *filename1* 및 *filename2*의 불일치 바이트를 나타냅니다.

- *Filename1* 및 *filename2*에서 와일드 카드 문자 (**&#42;** 및 **?**)를 사용할 수 있습니다. *Filename1*에서 와일드 카드를 사용 하는 경우 **fc** 는 지정 된 모든 파일을 *filename2*에서 지정한 파일 또는 파일 집합과 비교 합니다. *Filename2*에서 와일드 카드를 사용 하는 경우 **fc** 는 *filename1*의 해당 값을 사용 합니다.

- ASCII 파일을 비교할 때 **fc** 는 저장소로 내부 버퍼 (100 줄을 저장할 만큼 충분히 큼)를 사용 합니다. 파일이 있는 경우는 버퍼 보다 큰 **fc** 버퍼에 로드할 수 있는 기능을 비교 합니다. **Fc** 는 파일의 로드 된 부분에서 일치 하는 항목을 찾지 못하면 중지 하 고 다음 메시지를 표시 합니다.

    `Resynch failed. Files are too different.`

    사용 가능한 메모리 보다 큰 이진 파일을 비교 하는 경우 **fc** 는 두 파일을 모두 완전히 비교 하 여 메모리의 각 부분을 디스크의 다음 부분으로 겹치게 합니다. 출력은 메모리 용량을 초과 하는 파일에 대 한 동일 하 게 됩니다.

### <a name="examples"></a>예

두 텍스트 파일의 ASCII 비교를 수행 하려면 *rpt* 와 *판매세*를 사용 하 고 결과를 약식 형식으로 표시 하려면 다음을 입력 합니다.

```
fc /a monthly.rpt sales.rpt
```

두 배치 파일에 대 한 이진 비교를 수행 하려면 *profits.bat* 및 *earnings.bat*을 입력 합니다.

```
fc /b profits.bat earnings.bat
```

결과 표시와 비슷합니다.

```
00000002: 72 43
00000004: 65 3A
0000000E: 56 92
000005E8: 00 6E
FC: earnings.bat longer than profits.bat
```

profits.bat 및 earnings.bat 파일이 동일한 경우 **fc** 는 다음과 같은 메시지를 표시 합니다.

```
Comparing files profits.bat and earnings.bat
FC: no differences encountered
```

현재 디렉터리에 있는 모든 .bat 파일 *new.bat*파일을 비교 하려면 다음을 입력 합니다.

```
fc *.bat new.bat
```

C 드라이브에 있는 파일 *new.bat* 와 C 드라이브의 파일 *new.bat* 비교 하려면 다음을 입력 합니다.

```
fc c:new.bat d:*.bat
```

D 드라이브의 루트 디렉터리에 같은 이름의 파일을 C 드라이브의 루트 디렉터리에 각 배치 파일을 비교 하려면 다음을 입력 합니다.

```
fc c:*.bat d:*.bat
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
