---
title: gpupdate
description: 그룹 정책 설정을 업데이트 하는 gpupdate 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2fd4e567-2ce1-4637-b611-c2f0895e5708
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a2047d6beb515350a534343ca484bc2deeb50daa
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818743"
---
# <a name="gpupdate"></a>gpupdate

그룹 정책 설정을 업데이트합니다.

## <a name="syntax"></a>구문

```
gpupdate [/target:{computer | user}] [/force] [/wait:<VALUE>] [/logoff] [/boot] [/sync] [/?]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| /target:`{computer|user}` | 사용자 또는 컴퓨터 정책 설정만 업데이트 되도록 지정 합니다. 기본적으로 사용자 및 컴퓨터 정책 설정이 모두 업데이트 됩니다. |
| /force | 모든 정책 설정을 다시 적용합니다. 기본적으로 변경 된 정책 설정만 적용 됩니다. |
| /wait`<VALUE>` | 정책 처리 명령 프롬프트를 반환 하기 전에 완료 될 때까지 기다리는 시간 (초) 수를 설정 합니다. 시간 제한이 초과 되 면 명령 프롬프트 표시 되지만 정책 처리가 계속 됩니다. 기본값은 600초입니다. 값 **0** 기다려야 하지 함을 의미 합니다. 값 **-1** 무기한 대기를 의미 합니다.<p>스크립트에서이 명령을 사용 하 여 제한 시간을 지정 하 여 실행할 수 있습니다 **gpupdate** 하 고 완료 될 때 종속 되지 않는 명령으로 계속 **gpupdate**합니다. 수 있도록 지정 된 시간 제한이 없는이 명령을 사용할 수는 또는 **gpupdate** 의존 하는 다른 명령을 실행 하기 전에 실행을 완료 합니다. |
| /logoff | 그룹 정책 설정을 업데이트 한 후 로그 오프를 하면 됩니다. 이 명령은 백그라운드 업데이트 주기에서 정책을 처리 하지 않는 경우에 처리 정책을 사용자가 로그온 하는 그룹 정책 클라이언트 쪽 확장에 필요 합니다. 사용자 대상 소프트웨어 설치 및 폴더 리디렉션을 예로 들 수 있습니다. 로그 오프를 요청 하는 확장이 없는 경우이 옵션은 효과가 없습니다. |
| /boot | 그룹 정책 설정을 적용 한 후 컴퓨터를 다시 시작을 하면 됩니다. 이 명령은 백그라운드 업데이트 주기에서 정책을 처리 하지만 컴퓨터를 시작할 때 정책을 처리 하는 그룹 정책 클라이언트 쪽 확장에 필요 합니다. 예로 소프트웨어 설치 컴퓨터를 대상으로 합니다. 다시 시작을 요청 하는 확장이 없는 경우이 옵션은 효과가 없습니다. |
| /sync | 동기적으로 완료 되도록 다음 전경 정책 애플리케이션이 있습니다. 포그라운드는 컴퓨터 부팅 및 사용자 로그온 시 적용 됩니다. 사용자, 컴퓨터 또는 모두를 사용 하 여이 지정할 수는 **/대상** 매개 변수입니다. **/force** 및 **/wait** 지정 하면 매개 변수가 무시 됩니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

변경 여부와 관계 없이 모든 그룹 정책 설정의 백그라운드 업데이트를 적용 하려면 다음을 입력 합니다.

```
gpupdate /force
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)