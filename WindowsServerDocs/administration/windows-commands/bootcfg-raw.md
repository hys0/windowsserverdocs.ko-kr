---
title: bootcfg raw
description: Windows 명령 항목에 대 한 **원시 bootcfg** -운영 체제 항목에 문자열로 지정 된 운영 체제 로드 옵션을 추가 합니다 **[운영 체제]** Boot.ini 파일의 섹션입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a68c59eb3a7018ba8a7c0c96b594f0ed68d914b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841604"
---
# <a name="bootcfg-raw"></a>bootcfg raw

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

운영 체제 항목에 문자열로 지정 된 운영 체제 로드 옵션을 추가 합니다 **[운영 체제]** Boot.ini 파일의 섹션입니다.

## <a name="syntax"></a>구문
```
bootcfg /raw [/s <computer> [/u <Domain>\<User> /p <Password>]] <OSLoadOptionsString> [/id <OSEntryLineNum>] [/a]
```
## <a name="parameters"></a>매개 변수
|용어|정의|
|----|-------|
|/s <computer>|이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.|
|/u <Domain> \\<User>|지정한 사용자의 계정 권한으로 명령을 실행 <User> 나 <Domain> \\ <User>합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.|
|/p <Password>|에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.|
|<OSLoadOptionsString>|운영 체제 항목에 추가할 운영 체제 로드 옵션을 지정 합니다. 이 로드 옵션은 운영 체제 항목에 연결 된 기존 로드 옵션을 바꿉니다. 유효성을 검사 하지 <OSLoadOptions> 이루어집니다.|
|/id <OSEntryLineNum>|업데이트 하려면 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다.|
|/ a|운영 체제 옵션 추가 되 고 기존 운영 체제 옵션에 추가할 것인지를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
##### <a name="remarks"></a>설명
-   **원시 bootcfg** 기존 운영 체제 항목 옵션을 덮어쓸 운영 체제 항목의 끝에 텍스트를 추가 하는 데 사용 됩니다. 이 텍스트와 같은 유효한 운영 체제 로드 옵션을 포함 해야 **디버그**, **/fastdetect**, **/nodebug**하십시오 **/baudrate**, **/ crashdebug**, 및 **동안**합니다. 다음 명령을 추가 하는 예를 들어, "**/fastdetect 디버그**" 첫 번째는 운영 체제 항목의 끝을 바꾸고 이전 운영 체제 항목 옵션:
    ```
    bootcfg /raw "/debug /fastdetect" /id 1
    ```
## <a name="BKMK_examples"></a>예제
다음 예제에서는 사용 하는 방법을 표시 합니다 **bootcfg 원시 /** 명령:
```
bootcfg /raw "/debug /sos" /id 2
bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 "/crashdebug " /id 2
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
