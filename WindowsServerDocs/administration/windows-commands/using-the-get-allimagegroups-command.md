---
title: AllImageGroups
description: 서버의 모든 이미지 그룹과 해당 이미지 그룹의 모든 이미지에 대 한 정보를 검색 하는 AllImageGroups에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2ca06533-bcf5-4590-ac8e-263d6c9874f8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5863ecc22ff5b96024cb3ba2bdbcac9f7ae8455
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935179"
---
# <a name="get-allimagegroups"></a>AllImageGroups

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

모든 이미지 그룹에 대 한 정보는 서버와 해당 이미지 그룹의 모든 이미지를 검색합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-AllImageGroups [/Server:<Server name>] [/detailed]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|자세한/|각 이미지에서 이미지 메타 데이터를 반환합니다. 이 매개 변수를 사용 하지 않으면 하는 경우 이미지 이름, 설명 및 각 이미지에 대 한 파일 이름을 반환 하는 기본 동작이입니다.|
## <a name="examples"></a>예
이미지 그룹에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-AllImageGroups
wdsutil /verbose /Get-AllImageGroups /Server:MyWDSServer /detailed
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [ImageGroup 명령 사용](using-the-add-imagegroup-command.md) 
 [ImageGroup 명령 사용](using-the-get-imagegroup-command.md) 
 [ImageGroup 명령 사용](using-the-remove-imagegroup-command.md) 
 [하위 명령: ImageGroup](subcommand-set-imagegroup.md)
