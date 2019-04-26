---
title: pwlauncher
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0917bb7b-408a-40f7-a1c5-20e94c10d38b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1aa2e22f74323bb6cabfc644ca67e17a7fcbd3fc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851024"
---
# <a name="pwlauncher"></a>pwlauncher



활성화 하거나 비활성화는 Windows To Go 시작 옵션 (pwlauncher). **pwlauncher** 명령줄 도구를 사용 하면 Windows To Go 작업 영역에 자동으로 부팅 하도록 컴퓨터를 구성할 수 있습니다 (가정 하나가 있는) 펌웨어를 입력 하거나 시작 옵션을 변경 하지 않고도 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Pwlauncher {/enable | /disable}
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|같습니다.|컴퓨터가 있는 경우 USB 장치에서 자동으로 부팅 됩니다 있도록 Windows To Go 시작 옵션을 사용 하도록 설정|
|/disable|Windows To Go 시작 옵션을 사용 하지 않습니다를 펌웨어에 수동으로 구성 하지 않으면 USB 장치에서 컴퓨터를 부팅할 수 없습니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Windows To Go를 사용 하려는 사용자에 대 한 가장 큰 장애물은 USB에서 부팅 하도록 컴퓨터를 가져오는 중입니다. 일반적으로 펌웨어를 입력 하 고 컴퓨터를 제대로 구성 될 때까지 다른 구성 옵션을 시도 하면 됩니다. 이 대부분의 사용자에 대 한 간단한 작업이 아니며은 펌웨어를 잘못 사용 하는 경우 사용할 수 없는 시스템을 렌더링할 수 있는 옵션을 포함 하기 때문에 매우 위험 합니다. 이 문제, Windows 8and 완화 하기 위해 나중에 운영 체제 포함 "Windows To Go 시작 옵션 이라고 하는 기능? windows에서 USB에서 부팅 하도록 컴퓨터를 구성할 수 있도록 하는-적 펌웨어를 입력을 하지 않고 USB에서 부팅 펌웨어를 원하는 만큼 합니다. 항상 USB에서 부팅 하도록 시스템을 사용 하면 처음에 고려해 야 할 수 있습니다. 예를 들어 시스템을 손상 시키는 맬웨어를 포함 하는 USB 장치를 실수로 부팅 수 또는 여러 USB 드라이브를 부팅 충돌이 발생 하는 연결 될 수 있습니다. 따라서 기본 구성에는 Windows To Go 시작 옵션 기본적으로 사용 하지 않도록 설정 합니다. 또한 Windows To Go 시작 옵션을 구성 하려면 관리자 권한이 필요 합니다. Pwlauncher 명령줄 도구를 사용 하 여 Windows To Go 시작 옵션을 사용 하도록 설정 하는 경우 또는 **변경 Windows To Go 시작 옵션** 컴퓨터를 시작 하기 전에 컴퓨터에 삽입 하는 모든 USB 장치에서 부팅을 시도 하는 응용 프로그램입니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 사용 하는 방법을 보여 줍니다.는 **pwlauncher** 명령을 USB에서 부팅을 사용 하도록 설정 합니다.
```
Pwlauncher /enable
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)