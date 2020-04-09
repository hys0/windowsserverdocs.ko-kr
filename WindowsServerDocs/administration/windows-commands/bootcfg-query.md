---
title: bootcfg query
description: Boot.ini의 부팅 로더 및 운영 체제 섹션 항목을 쿼리하고 표시 하는 bootcfg 쿼리에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a4cacfd1-10a6-4a11-b0c5-f8abde72bfc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ac80c802b1d30dcf7221f94f761233c6b6fc6b6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848526"
---
# <a name="bootcfg-query"></a>bootcfg query

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

를 쿼리하고 Boot.ini의 [부팅 로더] 및 [운영 체제] 섹션 항목을 표시 합니다.

## <a name="syntax"></a>구문
```
bootcfg /query [/s <computer> [/u <Domain>\<User> /p <Password>]]
```
### <a name="parameters"></a>매개 변수

|        용어         |                                                                                             정의                                                                                              |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>    |                                         이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                          |
| /u <Domain>\\<User> | <User>또는 <Domain>\\<User>에 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
|    /p <Password>    |                                                        에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                        |
|         /?          |                                                                                명령 프롬프트에 도움말을 표시합니다.                                                                                 |

##### <a name="remarks"></a>주의
- 다음은 **bootcfg/query** 출력의 샘플입니다.
  ```
  Boot Loader Settings
  ----------
  timeout: 30
  default: multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  Boot Entries
  ------
  Boot entry ID:   1
  Friendly Name:   
  path:            multi(0)disk(0)rdisk(0)partition(1)\WINDOWS
  OS Load Options: /fastdetect /debug /debugport=com1:
  ```
- **Bootcfg 쿼리** 출력의 부팅 로더 설정 부분에는 boot.ini의 [부팅 로더] 섹션에 각 항목이 표시 됩니다.
- **Bootcfg 쿼리** 출력의 부팅 항목 부분에는 Boot.ini: 부팅 항목 ID, 이름, 경로 및 OS 로드 옵션의 [운영 체제] 섹션에 각 운영 체제 항목에 대 한 다음과 같은 세부 정보가 표시 됩니다.
  ## <a name="examples"></a><a name=BKMK_examples></a>예와
  다음 예에서는 **bootcfg/query** 명령을 사용 하는 방법을 보여 줍니다.
  ```
  bootcfg /query
  bootcfg /query /s srvmain /u maindom\hiropln /p p@ssW23
  bootcfg /query /u hiropln /p p@ssW23
  ```
  ## <a name="additional-references"></a>추가 참조
  - [명령줄 구문 키](command-line-syntax-key.md)
