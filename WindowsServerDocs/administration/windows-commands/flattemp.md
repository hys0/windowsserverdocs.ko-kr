---
title: flattemp
description: 플랫 임시 폴더를 사용 하거나 사용 하지 않도록 설정 하는 flattemp 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 059a0960-1fd9-4382-87fe-a85d5dccdaea
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a30a3f7eb6ec56a499864116debfbb6c09756d34
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2020
ms.locfileid: "83437228"
---
# <a name="flattemp"></a>flattemp

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

하나의 임시 폴더를 사용 하지 않도록 설정 하거나 사용 합니다. 이 명령을 실행 하려면 관리자 자격 증명이 있어야 합니다.

> [!NOTE]
> 이 명령은 원격 데스크톱 세션 호스트 역할 서비스를 설치한 경우에만 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
flattemp {/query | /enable | /disable}
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| / 쿼리 | 현재 설정을 쿼리합니다. |
| 같습니다. | 하나의 임시 폴더를 사용 하도록 설정 합니다. 사용자는 임시 폴더가 사용자의 홈 폴더에 있는 경우를 제외 하 고는 임시 폴더를 공유 합니다. |
| /disable | 하나의 임시 폴더를 사용 하지 않도록 설정 합니다. 각 사용자의 임시 폴더는 별도의 폴더에 상주 합니다 (사용자의 세션 ID에 의해 결정 됨). |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 각 사용자에 게 고유한 임시 폴더가 있는 경우를 사용 `flattemp /enable` 하 여 플랫 임시 폴더를 사용 하도록 설정 합니다.

- 여러 사용자 (일반적으로 가리키는 TEMP 및 TMP 환경 변수)에 대 한 임시 폴더를 만들기 위한 기본 방법은에 하위 폴더를 만들어는 **\Temp** 하위 폴더 이름으로 로그온 Id를 사용 하 여 폴더입니다. 예를 들어, TEMP 환경 변수 C:\Temp를 가리키는 경우 사용자 로그온 Id 4에 할당 된 임시 폴더 C:\Temp\4입니다.

    사용 하 여 **flattemp**, \Temp 폴더에 직접 지정 하 고 하위 폴더를 구성 하지 않도록 합니다. 이 기능은 원격 데스크톱 세션 호스트 server 로컬 드라이브에 있든, 공유 네트워크 드라이브에 있든 간에 사용자 임시 폴더를 홈 폴더에 포함 하려는 경우에 유용 합니다. `flattemp /enable*`각 사용자가 별도의 임시 폴더를 사용 하는 경우에만 명령을 사용 해야 합니다.

- 사용자의 임시 폴더가 네트워크 드라이브에 있으면 앱 오류가 발생할 수 있습니다. 이 공유 네트워크 드라이브는 네트워크에서 일시적으로 사용할 수 없을 때 발생 합니다. 앱의 임시 파일은 액세스할 수 없거나 동기화 되지 않기 때문에 디스크가 중지 된 것 처럼 응답 합니다. 임시 폴더를 네트워크 드라이브로 이동 권장 되지 않습니다. 임시 폴더는 로컬 하드 디스크에 유지 하는 것이 기본값이입니다. 예기치 않은 동작이 나 특정 애플리케이션을 사용 하 여 디스크 손상 오류를 발생 하면 네트워크를 안정화 또는 임시 폴더를 로컬 하드 디스크를 다시 이동 합니다.

- 별도 임시 폴더 세션을 사용 하 여 사용 하지 않도록 설정 하는 경우 **flattemp** 설정이 무시 됩니다. 이 옵션은 원격 데스크톱 서비스 구성 도구에서 설정 됩니다.

### <a name="examples"></a>예

하나의 임시 폴더에 대 한 현재 설정을 표시 하려면 다음을 입력 합니다.

```
flattemp /query
```

하나의 임시 폴더를 사용 하려면 다음을 입력 합니다.

```
flattemp /enable
```

하나의 임시 폴더를 사용 하지 않으려면 다음을 입력 합니다.

```
flattemp /disable
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

