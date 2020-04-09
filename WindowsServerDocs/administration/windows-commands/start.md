---
title: 시작
description: 시작에 대 한 Windows 명령 항목으로, 지정 된 프로그램 또는 명령을 실행 하기 위해 별도의 명령 프롬프트 창을 시작 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0173f9b3-5cd7-4edb-b01e-d02193b4fadc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6ab8fc07923a2396a173803264d54a036983fb71
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834076"
---
# <a name="start"></a>시작

지정 된 프로그램 또는 명령을 실행 하는 별도 명령 프롬프트 창을 시작 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
start [<Title>] [/d <Path>] [/i] [{/min | /max}] [{/separate | /shared}] [{/low | /normal | /high | /realtime | /abovenormal | belownormal}] [/affinity <HexAffinity>] [/wait] [/elevate] [/b] [<Command> [<Parameter>... ] | <Program> [<Parameter>... ]]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|\<제목 >|명령 프롬프트 창 제목 표시줄에 표시할 제목을 지정 합니다.|
|/d \<경로 >|시작 디렉터리를 지정합니다.|
|/i|Cmd.exe 시작 환경을 새 명령 프롬프트 창으로 전달합니다. 경우 **/i** 를 지정 하지 않으면 현재 환경이 사용 됩니다.|
|/min \|/최대|최소화 하기 위해 지정 ( **/min**) 하거나 최대화 ( **/최대 용량**) 새 명령 프롬프트 창입니다.|
|/개별 \|/공유|별도 메모리 공간에서 16 비트 프로그램을 시작 ( **/separate**) 또는 공유 메모리 공간 (**공유 /** ). 이러한 옵션은 64 비트 플랫폼에서 지원 되지 않습니다.|
|/slow \|/hv\| \|/low \| \|/abovenormal|지정 된 우선 순위 클래스에서 애플리케이션을 시작 합니다. 유효한 우선 순위 클래스 값은 **낮은/** , **일반/** , **높은/** , **/realtime**, **/abovenormal**, 및 **/belownormal**합니다.|
|/caffinity \<HexAffinity >|새 애플리케이션 (16 진수 숫자로 표현 되는) 지정 된 프로세서 선호도 마스크를 적용 합니다.|
|/wait|애플리케이션을 시작 하 고 끝날 때까지 대기 합니다.|
|/상승|응용 프로그램을 관리자 권한으로 실행 합니다.|
|/b|새 명령 프롬프트 창을 열지 않고 애플리케이션을 시작 합니다. CTRL + C 처리는 CTRL + C 처리 애플리케이션을 사용 하지 않으면 무시 됩니다. 애플리케이션을 중단 하려면 CTRL + BREAK를 사용 합니다.|
|명령 > \| \<프로그램을 \<>|명령이 나 프로그램 시작을 지정 합니다.|
|매개 변수 > \<...|명령 또는 프로그램에 전달할 매개 변수를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

- 명령으로 파일의 이름을 입력 하 여 파일 연결을 통해 실행 불가능 한 파일을 실행할 수 있습니다.
- 확장명이 나 경로 한정자가 없는 첫 번째 토큰으로 CMD 문자열을 포함 하는 명령을 실행 하면 CMD가 COMSPEC 변수의 값으로 바뀝니다. 이로써 사용자를 받지 **cmd** 현재 디렉터리에서.
- 32 비트 그래픽 사용자 인터페이스 (GUI) 응용 프로그램을 실행 하면 **cmd** 명령 프롬프트를 반환 하기 전에 종료 하도록 응용 프로그램을 기다리지 않습니다. 명령 스크립트에서 애플리케이션을 실행 하는 경우에이 문제가 발생 하지 않습니다.
- 확장을 포함 하지 않는 첫 번째 토큰을 사용 하는 명령을 실행 하면 Cmd.exe를 사용 하 여 PATHEXT 환경 변수의 값을 찾고 어떤 순서로 확장 프로그램을 결정 합니다. PATHEXT 변수에 대 한 기본값은입니다.  
  ```
  .COM;.EXE;.BAT;.CMD;.VBS;.VBE;.JS;.JSE;.WSF;.WSH;.MSC 
  ```  
  구문을 경로 변수와 각 확장 프로그램을 구분 하는 세미콜론으로 동일 하 게 않음을 유의 하십시오.
- 모든 확장에 일치 하는 경우 실행 파일을 검색할 때 **시작** 이름이 디렉터리 이름에 일치 하는 경우를 확인 합니다. 그렇지 않으면 **시작** Explorer.exe 해당 경로에 열립니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

명령 프롬프트에서 Myapp 프로그램을 시작 하 고 현재 명령 프롬프트 창을 사용 하 여 유지 하려면 다음을 입력 합니다.
```
start myapp 
```
보려는 **시작** 별도의 명령줄 도움말 항목 유형 명령 프롬프트 창을 최대화 합니다.
```
start /max start /?
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
