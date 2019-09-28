---
title: bitsadmin create
description: '**Bitsadmin 만들기** 에 대 한 Windows 명령 항목-지정 된 표시 이름을 사용 하 여 전송 작업을 만듭니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9f6d641d44c56ea4ff11f48a725367de7dcf472a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381812"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 표시 이름과 함께 전송 작업을 만듭니다. 다운로드 작업은 서버에서 로컬 파일로 데이터를 전송 합니다. 업로드 작업은 로컬 파일의 데이터를 서버로 전송 합니다. 업로드-회신 작업은 로컬 파일에서 서버로 데이터를 전송 하 고 서버에서 회신 파일을 받습니다.

[Bitsadmin resume](bitsadmin-resume.md) 스위치를 사용 하 여 전송 큐에서 작업을 활성화 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /create [type] DisplayName
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|type|-    **/다운로드** 는 서버에서 로컬 파일로 데이터를 전송 합니다.<br />-    **/Upload** 로컬 파일의 데이터를 서버로 전송 합니다.<br />-    **/Upload-Reply** 는 로컬 파일에서 서버로 데이터를 전송 하 고 서버에서 회신 파일을 받습니다.<br />-이 매개 변수의 기본값은 **다운로드/** 명령줄에 지정 되지 않은 경우.|
|DisplayName|새로 만든된 작업에 할당 된 표시 이름입니다.|

**BITS 1.2 및 이전 버전**: /Upload 및/Upload-Reply 형식은 사용할 수 없습니다.

## <a name="BKMK_examples"></a>예와

이라는 다운로드 작업을 만들고 *myDownloadJob*합니다.

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
