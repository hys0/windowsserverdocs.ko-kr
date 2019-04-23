---
title: bootcfg query
description: Windows 명령 항목에 대 한 **bootcfg 쿼리** -쿼리와 표시 [부팅 로더] 및 [운영 체제] 섹션 Boot.ini에서 항목입니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a6886fbdfe541b39e530d2b7f71d4fc40909a2a2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862934"
---
# <a name="bootcfg-query"></a>bootcfg query

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

쿼리하고 [부팅 로더]을 표시 및 [운영 체제] 섹션 Boot.ini에서 항목입니다.

## <a name="syntax"></a>구문
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
## <a name="parameters"></a>매개 변수
|용어|정의|
|----|-------|
|/s <computer>|이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.|
|/u <Domain>\\<User>|지정한 사용자의 계정 권한으로 명령을 실행 <User>나 <Domain> \\ <User>합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.|
|/p <Password>|에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
##### <a name="remarks"></a>설명
-   다음은 샘플입니다 **bootcfg /query** 출력:
    ```
    Boot Loader Settings
    ----------
    timeout: 30
    default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    Boot Entries
    ------
    Boot entry ID:   1
    Friendly Name:   ""
    path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
    OS Load Options: /fastdetect /debug /debugport=com1:
    ```
-   부팅 로더 설정 부분을 **bootcfg 쿼리** 출력 boot.ini [부팅 로더] 섹션에서 각 항목에 표시 됩니다.
-   부팅 항목 부분을 **bootcfg 쿼리** 출력 Boot.ini의 [운영 체제] 섹션에서 각 운영 체제 항목에 대해 다음 세부 정보를 표시 합니다. 부팅 항목 ID, 이름, 경로 및 운영 체제 로드 옵션입니다.
## <a name="BKMK_examples"></a>예제
다음 예제에서는 사용 하는 방법을 표시 합니다 **bootcfg /query** 명령:
```
bootcfg /query
bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
bootcfg /query /u hiropln /p p@ssW23
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
