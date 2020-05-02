---
title: 사용 안 함-서버
description: Windows 배포 서비스 서버에 대 한 모든 서비스를 비활성화 하는 disable Server에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b69fcfe0-b744-4794-bc75-2c9218c0ba66
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5df5c7e2f18cdda2aeeea22c209881077c681f03
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720969"
---
# <a name="disable-server"></a>사용 안 함-서버

Windows 배포 서비스 서버에 대 한 모든 서비스를 사용 하지 않도록 설정 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Disable-Server [/Server:<Server name>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/Server:\<서버 이름>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|

## <a name="examples"></a>예

서버를 비활성화 하려면 다음 중 하나를 실행 합니다.
```
WDSUTIL /Disable-Server
WDSUTIL /Verbose /Disable-Server /Server:MyWDSServer
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

