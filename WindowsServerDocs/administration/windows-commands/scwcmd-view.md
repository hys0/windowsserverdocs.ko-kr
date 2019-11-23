---
title: Scwcmd 뷰
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7995959a-d93e-4865-a6a0-2ab18c2bb47f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a69db16696f42950af97b62ba6f28c4083954137
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371191"
---
# <a name="scwcmd-view"></a>Scwcmd: 보기

> 적용 대상: Windows Server 2012 R2, Windows Server 2012

지정 된.xsl 변환을 사용 하 여.xml 파일을 렌더링 합니다. 이 명령은 서로 다른 뷰를 사용 하 여 구성 마법사 SCW (보안).xml 파일을 표시 하는 데 유용할 수 있습니다.

## <a name="syntax"></a>구문

```
scwcmd view /x:<Xmlfile.xml> [/s:<Xslfile.xsl>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/x:\<Xmlfile >|.Xml 파일을 볼 수를 지정 합니다. 이 매개 변수를 지정 합니다.|
|/s:\<Xslfile >|렌더링 과정의 일부로.xml 파일에 적용할.xsl 변환을 지정 합니다. 이 매개 변수는 선택 사항 SCW.xml 파일입니다. 경우는 **보기** 명령은 SCW.xml 파일을 렌더링 하는 데 사용 됩니다, 지정한.xml 파일에 대 한 올바른 기본 변환을 로드를 자동으로 시도 합니다. .Xsl 변환을 지정 된 경우 변환은.xml 파일이.xsl 변환와 같은 디렉터리에 있다는 가정 아래 작성 되어야 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Scwcmd.exe은 Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 컴퓨터에서 사용할 수만 있습니다.

## <a name="BKMK_Examples"></a>예와

Policyfile.xml Policyview.xsl 변환을 사용 하 여를 보려면 다음을 입력 합니다.
```
scwcmd view /x:C:\policies\Policyfile.xml /s:C:\viewers\Policyview.xsl
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)