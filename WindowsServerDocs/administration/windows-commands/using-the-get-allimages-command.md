---
title: AllImages
description: 서버에 있는 모든 이미지에 대 한 정보를 검색 하는 AllImages에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 19de3720-4315-415a-8dc6-486caa0b2100
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9834552ebe6395f13333e81fbc2996a8ff49f39c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935173"
---
# <a name="get-allimages"></a>AllImages

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 모든 이미지에 대 한 정보를 검색합니다.

## <a name="syntax"></a>구문
```
wdsutil /Get-AllImages [/Server:<Server name>] /Show:{Boot | Install | LegacyRis | All} [/detailed]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.|
|/ Show: {부팅 & #124; 설치 및 #124; LegacyRis & #124; 모든}|-   **부팅** 은 부팅 이미지만 반환 합니다.<br />-   **설치** 는 설치 이미지와 해당 이미지를 포함 하는 이미지 그룹에 대 한 정보를 반환 합니다.<br />-   **LegacyRis** 은 RIS (원격 설치 서비스) 이미지만 반환 합니다.<br />-   **모든** 부팅 이미지 정보, 설치 이미지 정보 (이미지 그룹에 대 한 정보 포함) 및 RIS 이미지 정보를 반환 합니다.|
|자세한/|각 이미지에서 모든 이미지 메타 데이터 반환 되어야 함을 나타냅니다. 이 옵션을 사용 하지 않는 경우 기본 동작은 반환할 이미지 이름, 설명 및 파일 이름입니다.|
## <a name="examples"></a>예
이미지에 대 한 정보를 보려면 다음 중 하나를 입력 합니다.
```
wdsutil /Get-AllImages /Show:Install
wdsutil /verbose /Get-AllImages /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [추가 이미지 명령을](using-the-add-image-command.md) 
 사용 하 여 [복사 이미지 명령을](using-the-copy-image-command.md) 
 사용 하 여 [내보내기 이미지 명령 사용](using-the-export-image-command.md) 
 [제거 이미지 명령을](using-the-remove-image-command.md) 
 사용 하 여 [Replace 이미지 명령을](using-the-replace-image-command.md) 
 사용 하 여 [하위 명령: 설정 이미지](subcommand-set-image.md)
