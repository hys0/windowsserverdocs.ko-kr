---
title: autoconv
description: 파일 할당 테이블 (Fat) 및 Fat32 볼륨을 NTFS 파일 시스템으로 변환 하는 **autoconv**의 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 17281e54-0b18-4e84-94ac-24586c82df4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fe0e388a1d4fd79567ef0562197e3181bbbc46f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851116"
---
# <a name="autoconv"></a>autoconv

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

파일 할당 테이블 (Fat) 및 Fat32 볼륨을 NTFS 파일 시스템으로 변환 하 고, 기존 파일 및 디렉터리는 **autochk** 를 실행 한 후에도 그대로 유지 됩니다. NTFS 파일 시스템으로 변환 된 볼륨은 Fat 또는 Fat32로 다시 변환할 수 없습니다.

## <a name="remarks"></a>주의

명령줄에서 **autoconv** 를 실행할 수 없습니다. 이는 **convert.exe**를 통해 설정 되는 경우 시작할 때만 실행 됩니다.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [autochk](autochk.md)

- [convert](convert.md)

- [파일 시스템 작업](https://go.microsoft.com/fwlink/?LinkId=4509)
