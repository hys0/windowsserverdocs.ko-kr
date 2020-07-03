---
title: ServerFiles 업데이트
description: 서버%Windir%\System32\RemInst 폴더에 저장 된 최신 파일을 사용 하 여 REMINST 공유 폴더의 파일을 업데이트 하는 업데이트 ServerFiles에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79b9332d5962c7e3c50ea3d7c71f33111a0e74b8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930134"
---
# <a name="update-serverfiles"></a>ServerFiles 업데이트

서버%Windir%\System32\RemInst 폴더에 저장 된 최신 파일을 사용 하 여 REMINST 공유 폴더의 파일을 업데이트 합니다. Windows 배포 서비스 설치의 유효성을 검사 하려면 각 서버를 업그레이드 한 후에이 명령을 한 번 실행 하거나, 설치를 Service Pack Windows 배포 서비스 파일을 업데이트 해야 합니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Update-ServerFiles [/Server:<Server name>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[/ 서버:\<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|

## <a name="examples"></a>예

파일을 업데이트 하려면 다음 중 하나를 입력 합니다.
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)