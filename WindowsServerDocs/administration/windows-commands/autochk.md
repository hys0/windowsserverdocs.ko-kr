---
title: autochk
description: 컴퓨터를 시작할 때 실행 되 고 Windows Server 이전에 파일 시스템의 논리적 무결성을 확인 하기 시작 하기 전에 실행 되는 **autochk**용 windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30ccdbb6aad6e116988ae9c782e3ff359642453e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851126"
---
# <a name="autochk"></a>autochk

컴퓨터를 시작 하 고 Windows Server&reg; 2008 R2 이전 버전에서 파일 시스템의 논리적 무결성을 확인 하기 시작 하기 전에 실행 됩니다.

**Autochk** 는 NTFS 디스크 에서만 실행 되 고 Windows Server 2008 r 2가 시작 되기 전에 실행 되는 버전의 **Chkdsk** 입니다. **않은** 명령줄에서 직접 실행할 수 없습니다. 대신, **않은** 다음과 같은 상황에서 실행 합니다.

- 부팅 볼륨에서 **Chkdsk** 를 실행 하려고 합니다.

- **Chkdsk** 에서 볼륨을 독점적으로 사용할 수 없으면입니다.

- 볼륨이 더티로 플래그가 지정 되 면입니다.

## <a name="remarks"></a>주의

> [!WARNING]
> **않은** 명령줄 도구는 명령줄에서 직접 실행할 수 없습니다. 대신는 **Chkntfs** 명령줄 도구를 원하는 대로 구성 **않은** 시작 시 실행 되도록 합니다.
> -  사용할 수 있습니다 **Chkntfs** 와 **/x** 동작 하도록 매개 변수 **않은** 특정 볼륨 또는 여러 볼륨에서 실행 합니다.
>
> - 사용 하 여는 **Chkntfs.exe** 와 명령줄 도구는 **/t** 매개 변수를 최대 3 일 (259,200 초)을 0 초에서 않은 지연을 변경 합니다. 그러나 긴 지연 시간이 경과할 때까지 또는 취소에 대 한 키를 누를 때까지 컴퓨터가 시작 되지 않으면 의미 **않은**합니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [손상](chkdsk.md)

- [Chkntfs](chkntfs.md)

- [디스크 및 파일 시스템 문제 해결](https://go.microsoft.com/fwlink/?LinkId=4527)