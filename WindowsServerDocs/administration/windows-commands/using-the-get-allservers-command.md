---
title: get AllServers
description: 모든 Windows 배포 서비스 서버에 대 한 정보를 검색 하는 get AllServers에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe2e3c69-8f2e-457d-af55-d249ebf70f53
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b400d5a2be69e8e89a05b233cc2e8f29bec848f6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831216"
---
# <a name="get-allservers"></a>get AllServers

모든 Windows 배포 서비스 서버에 대 한 정보를 검색합니다.

> [!NOTE]
> 이 명령은 사용자 환경에 여러 Windows 배포 서비스 서버가 있는 경우 또는 연결 된 서버 네트워크 연결이 느린 경우 완료 하는 오랜된 시간을 걸릴 수 있습니다.

## <a name="syntax"></a>구문

```
WDSUTIL [Options] /Get-AllServers /Show:{Config | Images | All} [/Detailed] [/Forest:{Yes | No}]
```

### <a name="parameters"></a>매개 변수

|   매개 변수   |                                                                                                                 설명                                                                                                                  |
|---------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /Show: {Config |                                                                                                                    이미지                                                                                                                    |
|  [/ 자세한]  | 와 함께에서 사용 하는 경우는 **/Show:Images** 또는 **/Show:All**, 모든 이미지 각 이미지의 메타 데이터를 반환 합니다. 하는 경우는 **자세한/** 옵션이 지정 되지 않은, 이미지 이름, 설명 및 파일 이름을 반환 하는 기본 동작입니다. |
| [포리스트/: {예 |                                                                                                                     아니요}]                                                                                                                     |

## <a name="examples"></a><a name=BKMK_examples></a>예와

모든 서버에 대 한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Get-AllServers /Show:Config
```
모든 서버에 대 한 자세한 정보를 보려면 다음을 입력 합니다.
```
WDSUTIL /Verbose /Get-AllServers /Show:All /Detailed /Forest:Yes
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)