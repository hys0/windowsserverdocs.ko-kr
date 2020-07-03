---
title: ImageGroup
description: 서버에서 이미지 그룹을 제거 하는 ImageGroup에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5b2c9813-5df2-4272-8449-26f3bb16f82b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d11a24152250786e600332c5eea0a6ffebc4848
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933335"
---
# <a name="using-the-remove-imagegroup-command"></a>제거 ImageGroup 명령을 사용 하 여

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 이미지 그룹을 제거합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /remove-ImageGroumediaGroup:<Image group name> [/Server:<Server name>]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
mediaGroup:<Image group name>|제거할 이미지 그룹의 이름을 지정 합니다.|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
## <a name="examples"></a>예
이미지 그룹을 제거 하려면 다음 중 하나를 입력 합니다.
```
wdsutil /remove-ImageGroumediaGroup:ImageGroup1
wdsutil /verbose /remove-ImageGroumediaGroup:My Image Group /Server:MyWDSServer
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [ImageGroup 명령 사용](using-the-add-imagegroup-command.md) 
 [AllImageGroups 명령 사용](using-the-get-allimagegroups-command.md) 
 [ImageGroup 명령 사용](using-the-get-imagegroup-command.md) 
 [하위 명령: ImageGroup](subcommand-set-imagegroup.md)
