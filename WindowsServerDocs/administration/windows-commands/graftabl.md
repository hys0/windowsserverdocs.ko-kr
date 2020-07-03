---
title: graftabl
description: Windows 운영 체제에서 그래픽 모드로 확장 문자 집합을 표시할 수 있도록 하는 graftabl 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9259833856ec5c6de402b0db0a4de4636a66f508
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85924598"
---
# <a name="graftabl"></a>graftabl

Windows 운영 체제에서 그래픽 모드로 확장 문자 집합을 표시할 수 있도록 합니다. 매개 변수 없이 사용 하는 경우 **graftabl** 는 이전 및 현재 코드 페이지를 표시 합니다.

## <a name="syntax"></a>구문

```
graftabl <codepage>
graftabl /status
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<codepage>` | 그래픽 모드에서 확장 문자의 모양을 정의 하는 코드 페이지를 지정 합니다. 유효한 코드 페이지 id 번호는 다음과 같습니다.<ul><li>**437** -미국</li><li>**850** -다국어 (라틴어 I)</li><li>**852** -슬라브어 (라틴어 II)</li><li>**855** -키릴 자모 (러시아어)</li><li>**857** -터키어</li><li>**860** -포르투갈어</li><li>**861** -아이슬란드어</li><li>**863** -캐나다-프랑스어</li><li>**865** -북유럽어</li><li>**866** -러시아어</li><li>**869** -현대 그리스어</li></ul> |
| /status | 이 명령에 사용 되는 현재 코드 페이지를 표시 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **Graftabl** 명령은 지정한 코드 페이지의 확장 된 문자 모니터 표시에만 영향을 줍니다. 실제 콘솔 입력 코드 페이지는 변경 되지 않습니다. 콘솔 입력 코드 페이지를 변경 하려면 [모드](mode.md) 또는 [chcp](chcp.md) 명령을 사용 합니다.

- 각 종료 코드와 간단한 설명입니다.

    | 종료 코드 | Description |
    | --------- | ----------- |
    | 0 | 문자 집합을 로드 했습니다. 이전 코드 페이지가 로드 되지 않았습니다. |
    | 1 | 잘못 된 매개 변수가 지정 되었습니다. 아무 조치도 취하지 않았습니다. |
    | 2 | 파일 오류가 발생 했습니다. |

- 일괄 처리 프로그램에서 ERRORLEVEL 환경 변수를 사용 하 여 **graftabl**에서 반환 하는 종료 코드를 처리할 수 있습니다.

### <a name="examples"></a>예

**Graftabl**에서 사용 하는 현재 코드 페이지를 보려면 다음을 입력 합니다.

```
graftabl /status
```

코드 페이지 437 (미국)에 대 한 그래픽 문자 집합을 메모리에 로드 하려면 다음을 입력 합니다.

```
graftabl 437
```

코드 페이지 850 (다국어)의 그래픽 문자 집합을 메모리로 로드 하려면 다음을 입력 합니다.

```
graftabl 850
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [freedisk 명령](freedisk.md)

- [모드 명령](mode.md)

- [chcp 명령](chcp.md)
