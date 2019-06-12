---
title: Get AllServers 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbccb834f9058f2c3cca097cdf998455f2a6892e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440488"
---
# <a name="using-the-get-allservers-command"></a>Get AllServers 명령을 사용 하 여



모든 Windows 배포 서비스 서버에 대 한 정보를 검색합니다.

> [!NOTE]
> 이 명령은 사용자 환경에 여러 Windows 배포 서비스 서버가 있는 경우 또는 연결 된 서버 네트워크 연결이 느린 경우 완료 하는 오랜된 시간을 걸릴 수 있습니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

## <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                                                 설명                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| / 표시: {0} 구성 |                                                                                                                    이미지                                                                                                                    |
|  [/ 자세한]  | 와 함께에서 사용 하는 경우는 **/Show:Images** 또는 **/Show:All**, 모든 이미지 각 이미지의 메타 데이터를 반환 합니다. 하는 경우는 **자세한/** 옵션이 지정 되지 않은, 이미지 이름, 설명 및 파일 이름을 반환 하는 기본 동작입니다. |
| [포리스트 /: {예 |                                                                                                                     No}]                                                                                                                     |

## <a name="BKMK_examples"></a>예제

모든 서버에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-AllServers /Show:Config
```
모든 서버에 대 한 자세한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)