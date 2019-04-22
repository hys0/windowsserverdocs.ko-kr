---
title: 업데이트 ServerFiles 명령
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ec96e2ba9aea14ed9a203dabbb697187736b33a8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817444"
---
# <a name="the-update-serverfiles-command"></a>업데이트 ServerFiles 명령



서버의 %Windir%\System32\RemInst 폴더에 저장 되는 최신 파일을 사용 하 여 REMINST 공유 폴더의 파일을 업데이트 합니다. Windows 배포 서비스 설치의 유효성을 보장 하려면 Windows 배포 서비스 파일에 각 server 업그레이드, 서비스 팩 설치 또는 업데이트 후이 명령을 실행 해야 있습니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Update-ServerFiles [/Server:<Server name>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/ 서버:\<서버 이름 >]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|

## <a name="BKMK_examples"></a>예제

파일을 업데이트 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)