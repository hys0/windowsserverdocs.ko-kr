---
title: Sc.exe 쿼리
description: Sc.exe 유틸리티를 사용 하 여 서비스, 드라이버, 서비스 유형 또는 드라이버 유형에 대 한 정보를 얻는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ac365f89-4b20-4de6-a582-b204c5e7d0eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86aabbbc42c965b72f317a3bfaa99acc99c46f3b
ms.sourcegitcommit: 95b60384b0b070263465eaffb27b8e3bb052a4de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2020
ms.locfileid: "82850044"
---
# <a name="scexe-query"></a>Sc.exe 쿼리

키를 가져오고 지정 된 서비스, 드라이버, 형식의 서비스 또는 드라이버의 종류에 대 한 정보를 표시 합니다.

## <a name="syntax"></a>구문

```
sc.exe [<ServerName>] query [<ServiceName>] [type= {driver | service | all}] [type= {own | share | interact | kernel | filesys | rec | adapt}] [state= {active | inactive | all}] [bufsize= <BufferSize>] [ri= <ResumeIndex>] [group= <GroupName>]
```

### <a name="parameters"></a>매개 변수

|       매개 변수        |                                                                                                                          Description                                                                                                                          |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     \<ServerName>      |                       서비스 위치는 원격 서버의 이름을 지정 합니다. 이름은 UNC (범용 명명 규칙) 형식 (예: \\ \\myserver)을 사용 해야 합니다. SC.exe를 로컬로 실행 하려면이 매개 변수를 생략 합니다.                        |
|     \<ServiceName>     |                                      반환 된 서비스 이름을 지정는 **getkeyname** 작업 합니다. 이 **쿼리** 매개 변수는 다른와 함께에서 사용 하지 **쿼리** 매개 변수 (이외의 *ServerName*).                                      |
|     type = {driver      |                                                                                                                            서비스                                                                                                                            |
|       유형 = {소유       |                                                                                                                             공유                                                                                                                             |
|     상태 = {활성     |                                                                                                                           비활성                                                                                                                            |
| bufsize = \<BufferSize> |                     크기 (바이트) 열거 버퍼를 지정합니다. 기본 버퍼 크기는 1024 바이트입니다. 1, 024 바이트를 초과 하는 쿼리에서 결과 표시할 때 열거 버퍼의 크기를 늘려야 합니다.                      |
|   ri = \<ResumeIndex>   | 열거를 시작 하거나 다시 인덱스 번호를 지정 합니다. 기본값은 **0** 입니다. 이 매개 변수를 사용 하 여 함께에서 **bufsize =** 버퍼의 기본 표시할 수 있는 보다 자세한 정보는 쿼리에 의해 반환 될 때 매개 변수입니다. |
|  group = \<GroupName>   |                                                                             서비스 그룹을 열거할 수를 지정 합니다. 기본적으로 모든 그룹이 열거 됩니다 (* * group = * *).                                                                              |
|           /?           |                                                                                                             명령 프롬프트에 도움말을 표시합니다.                                                                                                              |

## <a name="remarks"></a>설명

- 매개 변수 및 값 사이 공백 없이 (즉, **유형 = 자체**, 이 아니라 **유형 = 자체**), 작업이 실패 합니다.
- **쿼리** 서비스에 대 한 다음 정보를 표시 하는 작업: WIN32_EXIT_B, SERVICE_EXIT_B, 검사점 및 WAIT_HINT (뿐만 아니라 상태는 사용할 수 없는), 상태 SERVICE_NAME (서비스의 레지스트리 하위 키 이름)을 입력 합니다.
- **유형 =** 일부 경우에 두 번 매개 변수를 사용할 수 있습니다. 처음 나오는 **유형 =** 매개 변수 서비스, 드라이버 또는 둘 모두를 쿼리할 것인지를 지정 합니다 (**모든**). 두 번째 모양을 **형식 =** 매개 변수에서 형식을 지정 된 **만들기** 더 쿼리의 범위를 좁히기 위해 작업 합니다.
- 면에서 결과 표시할은 **쿼리** 열거 버퍼의 크기를 초과 하는 명령, 다음과 유사한 메시지가 표시 됩니다.  
  ```
  Enum: more data, need 1822 bytes start resume at index 79
  ```  
  나머지를 표시 하려면 **쿼리** 정보를 다시 실행 **쿼리**, 설정 **bufsize =** 바이트 및 설정의 수로 **ri =** 지정 된 인덱스입니다. 예를 들어 나머지 출력은 명령 프롬프트에서 다음을 입력 하 여 표시할 수 있습니다.  
  ```
  sc.exe query bufsize= 1822 ri= 79
  ```

## <a name="examples"></a>예

만 활성화 된 서비스에 대 한 정보를 표시 하려면 다음 명령 중 하나를 입력 합니다.
```
sc.exe query
sc.exe query type= service
```
활성화 된 서비스에 대 한 정보를 표시 하 고 2, 000 바이트의 버퍼 크기를 지정 하려면 다음을 입력 합니다.
```
sc.exe query type= all bufsize= 2000
```
WUAUSERV 서비스에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
sc.exe query wuauserv
```
모든 서비스 (활성 및 비활성)에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
sc.exe query state= all
```
모든 서비스 (활성 및 비활성), 56 줄에서 시작에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
sc.exe query state= all ri= 56
```
대화형 서비스에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
sc.exe query type= service type= interact
```
만 드라이버에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
sc.exe query type= driver
```
드라이버 인터페이스 사양 NDIS (Network) 그룹의 드라이버에 대 한 정보를 표시 하려면 다음을 입력 합니다.
```
sc.exe query type= driver group= ndis
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
