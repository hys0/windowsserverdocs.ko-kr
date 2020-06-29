---
title: pushd
description: Popd 명령에 사용 되는 현재 디렉터리를 저장 한 다음 지정 된 디렉터리로 변경 하는 pushd 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 396bc545-0f41-473e-b0ac-76fbbb74d390
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ca15d4279c65164c385ce3dce57d0420ad5aace3
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472138"
---
# <a name="pushd"></a>pushd

사용 하 여 현재 디렉터리에 저장는 **popd** 명령 및 지정된 된 디렉터리에 다음 변경 합니다.

**Pushd** 명령을 사용할 때마다 단일 디렉터리를 사용할 수 있도록 저장 됩니다. 그러나 **pushd** 명령을 여러 번 사용 하 여 여러 디렉터리를 저장할 수 있습니다. 디렉터리는 가상 스택에 순차적으로 저장 되므로 **pushd** 명령을 한 번 사용 하는 경우 명령을 사용 하는 디렉터리가 스택의 맨 아래에 배치 됩니다. 명령을 다시 사용 하는 경우 첫 번째 디렉터리가 첫 번째 디렉터리 위에 배치 됩니다. **Pushd** 명령을 사용할 때마다 프로세스가 반복 됩니다.

**Popd** 명령을 사용 하면 스택의 맨 위에 있는 디렉터리가 제거 되 고 현재 디렉터리가 해당 디렉터리로 변경 됩니다. 사용 하는 경우는 **popd** 명령을 다시, 스택에서 다음 디렉터리에서 제거 됩니다. 명령 확장을 사용 하는 경우 **popd** 명령은 **pushd** 명령으로 만든 드라이브 문자 assignations을 제거 합니다.

## <a name="syntax"></a>구문

```
pushd [<path>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| `<path>` | 현재 디렉터리에 디렉터리를 지정 합니다. 이 명령은 상대 경로 지원 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 명령 확장을 사용 하는 경우는 **pushd** 명령에는 네트워크 경로 로컬 드라이브 문자 및 경로입니다.

- 네트워크 경로 지정 하는 경우는 **pushd** 명령은 지정 된 네트워크 리소스를 일시적으로 가장 높은 사용 하지 않는 드라이브 문자 (z:부터 시작)를 할당 합니다. 다음 명령은 새로 할당 된 드라이브에 지정된 된 디렉터리에 현재 드라이브 및 디렉터리를 변경합니다. 사용 하는 경우는 **popd** 명령을 명령 확장을 사용 하도록 설정 된 **popd** 명령을 제거 하 여 만든 드라이브 문자 할당 **pushd**합니다.

### <a name="examples"></a>예제

일괄 처리가 실행 된 디렉터리에서 현재 디렉터리를 변경한 다음 다시 변경 하려면 다음을 수행 합니다.

```
@echo off
rem This batch file deletes all .txt files in a specified directory
pushd %1
del *.txt
popd
cls
echo All text files deleted in the %1 directory
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [popd 명령](popd.md)
