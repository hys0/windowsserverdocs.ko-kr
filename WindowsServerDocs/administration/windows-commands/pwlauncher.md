---
title: pwlauncher
description: Windows To Go 시작 옵션 (pwlauncher)을 사용 하거나 사용 하지 않도록 설정 하는 pwlauncher 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29e7434731bc89dff9bddbaedb8a6179f266fa28
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936705"
---
# <a name="pwlauncher"></a>pwlauncher

활성화 하거나 비활성화는 Windows To Go 시작 옵션 (pwlauncher). **pwlauncher** 명령줄 도구를 사용 하면 Windows To Go 작업 영역에 자동으로 부팅 하도록 컴퓨터를 구성할 수 있습니다 (가정 하나가 있는) 펌웨어를 입력 하거나 시작 옵션을 변경 하지 않고도 합니다.

Windows To Go 시작 옵션을 사용 하면 펌웨어가 USB에서 부팅을 지 원하는 한, 사용자가 펌웨어를 입력 하지 않고도 Windows 내에서 USB에서 부팅 하도록 컴퓨터를 구성할 수 있습니다. 항상 USB에서 부팅 하도록 시스템을 사용 하면 처음에 고려해 야 할 수 있습니다. 예를 들어 시스템을 손상 시키는 맬웨어를 포함 하는 USB 디바이스를 실수로 부팅 수 또는 여러 USB 드라이브를 부팅 충돌이 발생 하는 연결 될 수 있습니다. 이러한 이유로 기본 구성에서는 기본적으로 Windows To Go 시작 옵션을 사용할 수 없습니다. 또한 Windows To Go 시작 옵션을 구성 하려면 관리자 권한이 필요 합니다. Pwlauncher 명령줄 도구를 사용 하 여 Windows To Go 시작 옵션을 사용 하도록 설정 하는 경우 또는 **변경 Windows To Go 시작 옵션** 컴퓨터를 시작 하기 전에 컴퓨터에 삽입 하는 모든 USB 디바이스에서 부팅을 시도 하는 응용 프로그램입니다.

## <a name="syntax"></a>구문

```
pwlauncher {/enable | /disable}
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| 같습니다. | Windows To Go 시작 옵션을 사용 하도록 설정 하므로 컴퓨터가 있으면 USB 장치에서 자동으로 부팅 됩니다. |
| /disable | Windows To Go 시작 옵션을 사용 하지 않도록 설정 합니다 .이 경우 펌웨어에서 수동으로 구성 하지 않으면 컴퓨터를 USB 장치에서 부팅할 수 없습니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

USB에서 부팅을 사용 하도록 설정 하려면:

```
pwlauncher /enable
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
