---
title: makecab
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4da95297-c593-427b-9f76-2f389c46cbf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46efbae1d59a85071622df51fc018d0bf73dc504
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840266"
---
# <a name="makecab"></a>makecab

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

캐비닛 (.cab) 파일에 기존 파일을 패키지 합니다.
## <a name="syntax"></a>구문
```
makecab [/v[n]] [/d var=<value> ...] [/l <dir>] <source> [<destination>]
makecab [/v[<n>]] [/d var=<value> ...] /f <directives_file> [...]
```
#### <a name="parameters"></a>매개 변수

|      매개 변수       |                                                                        설명                                                                        |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
|       <source>       |                                                                     파일을 압축 합니다.                                                                     |
|    <destination>     | 압축 된 파일에 파일 이름입니다. 생략 하는 경우 밑줄 (_)로 소스 파일 이름의 마지막 문자와 바뀌고 대상으로 사용 됩니다. |
| /f < directives_file > |                                                   파일을 **makecab** 지시문 (반복 될 수 있습니다).                                                   |
|    /d var =<value>    |                                                          지정 된 값으로 변수를 정의 합니다.                                                           |
|       /l <dir>       |                                               대상을 배치할 위치 (기본값은 현재 디렉터리).                                               |
|       /v[<n>]        |                                                    자세한 정도 수준 디버깅을 설정 (0 = 없음,..., 3 = 전체).                                                     |
|          /?          |                                                           명령 프롬프트에 도움말을 표시합니다.                                                            |

## <a name="remarks"></a>주의
-   Directive_file에 대 한 자세한 내용은 MSDN의 [Microsoft 캐비닛 형식](https://go.microsoft.com/fwlink/?LinkId=226852) 을 참조 하세요.

## <a name="additional-references"></a>추가 참조
-   - [명령줄 구문 키](command-line-syntax-key.md)

