---
title: bootcfg query
description: '**Bootcfg 쿼리** -쿼리 및 boot.ini의 [부팅 로더] 및 [운영 체제] 섹션 항목을 표시 하는 Windows 명령 항목입니다.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ae82357cfe178343872448c2ebd46c49a797b5a9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379907"
---
# <a name="bootcfg-query"></a>bootcfg query

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

를 쿼리하고 Boot.ini의 [부팅 로더] 및 [운영 체제] 섹션 항목을 표시 합니다.

## <a name="syntax"></a>구문
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
## <a name="parameters"></a>매개 변수

|        용어         |                                                                                             정의                                                                                              |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>    |                                         이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                          |
| /u <Domain>\\<User> | <User>또는 <Domain>\\<User>에 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
|    /p <Password>    |                                                        에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                        |
|         /?          |                                                                                명령 프롬프트에 도움말을 표시합니다.                                                                                 |

##### <a name="remarks"></a>설명
- 다음은 **bootcfg/query** 출력의 샘플입니다.
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
- **Bootcfg 쿼리** 출력의 부팅 로더 설정 부분에는 boot.ini의 [부팅 로더] 섹션에 각 항목이 표시 됩니다.
- **Bootcfg 쿼리** 출력의 부팅 항목 부분에는 Boot.ini: 부팅 항목 ID, 이름, 경로 및 OS 로드 옵션의 [운영 체제] 섹션에 각 운영 체제 항목에 대 한 다음과 같은 세부 정보가 표시 됩니다.
  ## <a name="BKMK_examples"></a>예와
  다음 예에서는 **bootcfg/query** 명령을 사용 하는 방법을 보여 줍니다.
  ```
  bootcfg /query
  bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
  bootcfg /query /u hiropln /p p@ssW23
  ```
  #### <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
