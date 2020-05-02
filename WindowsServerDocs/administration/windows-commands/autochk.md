---
title: autochk
description: 컴퓨터를 시작할 때 그리고 Windows Server가 파일 시스템의 논리적 무결성을 확인 하기 시작 하기 전에 실행 되는 autochk 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a767e8f6cebee9c946f53e0403198384b7c0b790
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718787"
---
# <a name="autochk"></a>autochk

컴퓨터를 시작 하 고 Windows Server 이전 버전에서 파일 시스템의 논리적 무결성을 확인 하기 시작 하기 전에 실행 됩니다.

**Sc.exe** 는 NTFS 디스크 에서만 실행 되 고 Windows Server가 시작 되기 전에 실행 되는 **chkdsk** 버전입니다. **autochk** 는 명령줄에서 직접 실행할 수 없습니다. 대신, **autochk** 는 다음과 같은 경우에 실행 됩니다.

- 부팅 볼륨에서 **chkdsk** 를 실행 하려고 합니다.

- **Chkdsk** 에서 볼륨을 독점적으로 사용할 수 없으면입니다.

- 볼륨이 더티로 플래그가 지정 되 면입니다.

## <a name="remarks"></a>설명

> [!WARNING]
> **Autochk** 명령줄 도구는 명령줄에서 직접 실행할 수 없습니다. 대신, **chkntfs** 명령줄 도구를 사용 하 여 시작 시 **autochk** 를 실행 하는 방법을 구성 합니다.
>
> - **Chkntfs** 를 **/x** 매개 변수와 함께 사용 하 여 특정 볼륨 또는 여러 볼륨에서 **autochk** 가 실행 되지 않도록 할 수 있습니다.
>
> - **Chkntfs** 명령줄 도구를 **/t** 매개 변수와 함께 사용 하 여 autochk 지연 시간을 0 초에서 최대 3 일 (259200 초)으로 변경할 수 있습니다. 그러나 긴 지연은 시간이 경과할 때까지 또는 키를 눌러 **autochk**를 취소할 때까지 컴퓨터가 시작 되지 않는다는 것을 의미 합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [chkdsk 명령](chkdsk.md)

- [chkntfs 명령](chkntfs.md)
