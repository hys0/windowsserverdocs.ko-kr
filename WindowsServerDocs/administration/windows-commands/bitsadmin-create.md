---
title: bitsadmin create
description: '**Bitsadmin create**에 대 한 Windows 명령 항목으로, 지정 된 표시 이름으로 전송 작업을 만듭니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9a8c53af-900b-4c24-9265-5b8b08213fac
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4a922d9f15aff0a9bd064a7e987920adf3a9107d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850816"
---
# <a name="bitsadmin-create"></a>bitsadmin create

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정 된 표시 이름과 함께 전송 작업을 만듭니다. 다운로드 작업은 서버에서 로컬 파일로 데이터를 전송 합니다. 업로드 작업은 로컬 파일의 데이터를 서버로 전송 합니다. 업로드-회신 작업은 로컬 파일에서 서버로 데이터를 전송 하 고 서버에서 회신 파일을 받습니다.

[Bitsadmin resume](bitsadmin-resume.md) 스위치를 사용 하 여 전송 큐에서 작업을 활성화 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /create [type] displayname
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| ------- | -------- |
| 형식 | -  **/다운로드** 는 서버에서 로컬 파일로 데이터를 전송 합니다.<p>-  **/Upload** 는 로컬 파일에서 서버로 데이터를 전송 합니다.<p>-  **/Upload-Reply** 는 로컬 파일에서 서버로 데이터를 전송 하 고 서버에서 회신 파일을 받습니다.<p>이 매개 변수는 명령줄에 지정 되지 않은 경우 기본적으로 **/Download** 로 설정 됩니다. 또한 **/Upload** 및 **/UPLOAD-REPLY** 형식은 BITS 1.2 이전 버전에서는 사용할 수 없습니다. |
| displayname | 새로 만든된 작업에 할당 된 표시 이름입니다. |

## <a name="examples"></a><a name=BKMK_examples></a>예와

이라는 다운로드 작업을 만들고 *myDownloadJob*합니다.

```
C:\>bitsadmin /create myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
