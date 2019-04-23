---
title: autochk
description: Windows 명령 항목에 대 한 **않은** -컴퓨터를 시작할 때 실행 되 고 이전 Windows Server를 시작 하는 파일 시스템의 논리적 무결성을 확인 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 023bd81b93106a091fb9f26d97cf7eda75f0f633
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888464"
---
# <a name="autochk"></a>autochk



컴퓨터를 시작할 때 실행 하 고 파일 시스템의 논리적 무결성을 확인 하기 전에 Windows Server® 2008 R2.

**Autochk.exe** 버전이 **Chkdsk** NTFS 디스크에만 및 Windows Server 2008 R2 시작 하기 전에 실행 되는 합니다. **않은** 명령줄에서 직접 실행할 수 없습니다. 대신, **않은** 다음과 같은 상황에서 실행 합니다.
-   실행 하려고 하면 **Chkdsk** 부팅 볼륨에
-   경우 **Chkdsk** 볼륨의 단독 사용을 얻을 수 없으므로
-   변경 된 볼륨으로 플래그가 지정 되어 있는 경우

## <a name="remarks"></a>설명

> -   [!WARNING]
>     **않은** 명령줄 도구는 명령줄에서 직접 실행할 수 없습니다. 대신는 **Chkntfs** 명령줄 도구를 원하는 대로 구성 **않은** 시작 시 실행 되도록 합니다.
-   사용할 수 있습니다 **Chkntfs** 와 **/x** 동작 하도록 매개 변수 **않은** 특정 볼륨 또는 여러 볼륨에서 실행 합니다.
-   사용 하 여는 **Chkntfs.exe** 와 명령줄 도구는 **/t** 매개 변수를 최대 3 일 (259,200 초)을 0 초에서 않은 지연을 변경 합니다. 그러나 긴 지연 시간이 경과할 때까지 또는 취소에 대 한 키를 누를 때까지 컴퓨터가 시작 되지 않으면 의미 **않은**합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)

[Chkdsk](chkdsk.md)

[Chkntfs](chkntfs.md)

[디스크 및 파일 시스템 문제 해결](https://go.microsoft.com/fwlink/?LinkId=4527)