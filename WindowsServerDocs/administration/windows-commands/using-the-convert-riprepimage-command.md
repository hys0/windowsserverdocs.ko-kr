---
title: 변환-RiprepImage
description: 기존 RIPrep (원격 설치 준비) 이미지를 Windows 이미지 (.wim) 형식으로 변환 하는 RiprepImage에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d0e360a23874ada4659819395db16de7527208b4
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934106"
---
# <a name="convert-riprepimage"></a>변환-RiprepImage

기존 원격 설치 준비 (RIPrep) 이미지를 Windows 이미지 (.wim) 형식으로 변환 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Convert-RIPrepImage /FilePath:<File path and name>
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/InPlace]
         [/Overwrite:{Yes | No | Append}]
```

### <a name="parameters"></a>매개 변수

|            매개 변수            |                                                                                                                                                                                                                                                                                                               설명                                                                                                                                                                                                                                                                                                                |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Null\<File path and name> |                                                                                                                                                                                                       RIPrep 이미지에 해당 하는.sif 파일의 전체 경로 파일 이름을 지정 합니다. 이 일반적으로 Riprep.sif 호출 파일과 RIPrep 이미지를 포함 하는 폴더의 \Templates 하위 폴더에서 찾을 수 있습니다.                                                                                                                                                                                                       |
|        / DestinationImage        | 다음 옵션을 사용 하 여 대상 이미지에 대 한 설정을 지정 합니다.</br>-/FilePath:\<File path and name> -새 파일에 대 한 전체 파일 경로 설정 합니다. 예를 들어: **C:\Temp\convert.wim**</br>-[/Name:\<Name>]-이미지의 표시 이름을 설정 합니다. 표시 이름을 지정 하지 않으면 원본 이미지의 표시 이름이 사용 됩니다.</br>-[/ 설명: \<Description>]-이미지의 설명을 설정 합니다.</br>-[/InPlace]-변환이 발생할 기본 동작인 원본 이미지의 사본을 아닌 원래 RIPrep 이미지에는 지정 해야 합니다.</br>-[/Overwrite: {예 |

## <a name="examples"></a>예

지정된 된 RIPrep.sif 이미지 RIPREP.wim을 변환 하려면 다음을 입력 합니다.
```
WDSUTIL /Convert-RiPrepImage /FilePath:R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif /DestinationImage
/FilePath:C:\Temp\RIPREP.wim
```
지정 된 이름 및 설명을 지정한 RIPrep.sif 이미지 RIPREP.wim 변환할 파일이 이미 있으면 새 파일로 덮어쓰기를 입력 합니다.
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif
/DestinationImage /FilePath:\\Server\Share\RIPREP.wim
/Name:WindowsXP image /Description:Converted RIPREP image of WindowsXP
/Overwrite:Append
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)