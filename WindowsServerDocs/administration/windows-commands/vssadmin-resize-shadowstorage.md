---
title: Vssadmin resize shadowstorage
description: Vssadmin resize shadowstorage 명령에 대 한 설명입니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 03/05/2020
ms.localizationpriority: medium
ms.openlocfilehash: 8cd3b5e5629e41702126fb42b815931ff0aea6fa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830026"
---
# <a name="vssadmin-resize-shadowstorage"></a>Vssadmin resize shadowstorage

>적용 대상: Windows 10, Windows 8.1, Windows Server 2016, Windows Server 2012 R2, Windows server 2012, windows Server 2008 R2, Windows Server 2008

섀도 복사본 저장소에 사용할 수 있는 저장소 공간의 최대 크기를 조정 합니다.

**MinDiffAreaFileSize** 레지스트리 값을 사용 하 여 섀도 복사본 저장소에 사용할 수 있는 최소 저장소 공간 크기를 지정할 수 있습니다. 자세한 내용은 [MinDiffAreaFileSize](https://docs.microsoft.com/windows/win32/backup/registry-keys-for-backup-and-restore#mindiffareafilesize)를 참조 하세요.

> [!WARNING]
> 저장소 연결 크기를 조정 하면 섀도 복사본이 사라질 수 있습니다.

## <a name="syntax"></a>구문

```cmd
vssadmin resize shadowstorage /for=<ForVolumeSpec> /on=<OnVolumeSpec> [/maxsize=<MaxSizeSpec>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---|---|
`/for=<ForVolumeSpec>`  | 최대 크기의 저장소 공간 크기를 조정할 볼륨을 지정 합니다.
`/on=<OnVolumeSpec>` | 저장소 볼륨을 지정 합니다.
`[/maxsize=<MaxSizeSpec>]` |  섀도 복사본을 저장 하는 데 사용할 수 있는 공간의 최대 크기를 지정 합니다. /Svmaxsize에 지정 된 값이 없는 경우 사용할 수 있는 저장소 공간의 양에 제한이 없습니다.  <br> <br> MaxSizeSpec 값은 1mb 이상 이어야 하며 KB, MB, GB, TB, PB 또는 EB 단위 중 하나로 표시 되어야 합니다. 단위를 지정 하지 않으면 기본적으로 MaxSizeSpec은 바이트를 사용 합니다.

## <a name="examples"></a>예

```cmd
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=900MB
vssadmin Resize ShadowStorage /For=C: /On=D: /MaxSize=UNBOUNDED
vssadmin Resize ShadowStorage /For=C: /On=C: /MaxSize=20%
```

## <a name="additional-references"></a>추가 참조

* [명령줄 구문 키](https://docs.microsoft.com/windows-server/administration/windows-commands/command-line-syntax-key)
* [List](vssadmin.md)
