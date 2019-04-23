---
title: Convert RiprepImage 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf5fffdedbc25ad97e9e96a84d3ff1bbdaf87b2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835054"
---
# <a name="using-the-convert-riprepimage-command"></a>Convert RiprepImage 명령을 사용 하 여



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

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/ FilePath:\<파일 경로 및 이름 >|RIPrep 이미지에 해당 하는.sif 파일의 전체 경로 파일 이름을 지정 합니다. 이 일반적으로 Riprep.sif 호출 파일과 RIPrep 이미지를 포함 하는 폴더의 \Templates 하위 폴더에서 찾을 수 있습니다.|
|/ DestinationImage|다음 옵션을 사용 하 여 대상 이미지에 대 한 설정을 지정 합니다.</br>-/FilePath:\<파일 경로 및 이름 >-새 파일에 대 한 전체 파일 경로 설정 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. **C:\Temp\convert.wim**</br>-[/Name:\<이름 >]-이미지의 표시 이름을 가져오거나 설정 합니다. 표시 이름이 없는 지정 하는 경우 원본 이미지의 표시 이름을 사용 됩니다.</br>-   [/Description: \<설명 >]-이미지의 설명을 설정 합니다.</br>-[/InPlace]-변환이 발생할 기본 동작인 원본 이미지의 사본을 아닌 원래 RIPrep 이미지에는 지정 해야 합니다.</br>-[/Overwrite: {예 | 아니오 | 추가}]-파일에 지정 되었는지 여부를 결정 합니다 **/DestinationImage** 옵션 덮어써야 하면 해당 이름 가진 기존 파일 /FilePath에 이미 있습니다. **예** 기존 파일을 덮어씁니다. **더** (기본값) 이면 오류가 동일한 이름 가진 다른 파일이 이미 있는 경우 발생 합니다. **추가** 기존.wim 파일 내에서 새 이미지로 생성 되는 이미지를 연결 합니다.|

## <a name="BKMK_examples"></a>예제

지정된 된 RIPrep.sif 이미지 RIPREP.wim을 변환 하려면 다음을 입력 합니다.
```
WDSUTIL /Convert-RiPrepImage /FilePath:"R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif" /DestinationImage
/FilePath:"C:\Temp\RIPREP.wim"
```
지정 된 이름 및 설명을 지정한 RIPrep.sif 이미지 RIPREP.wim 변환할 파일이 이미 있으면 새 파일로 덮어쓰기를 입력 합니다.
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:"\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif"
/DestinationImage /FilePath:"\\Server\Share\RIPREP.wim"
/Name:"WindowsXP image" /Description:"Converted RIPREP image of WindowsXP"
/Overwrite:Append
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)