---
title: bootcfg raw
description: '**Bootcfg raw** 의 Windows 명령 항목-boot.ini 파일의 **[운영 체제]** 섹션에서 운영 체제 항목에 문자열로 지정 된 운영 체제 로드 옵션을 추가 합니다.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fb5c052f85f54656c54a9e534f867d287407d2d4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379901"
---
# <a name="bootcfg-raw"></a>bootcfg raw

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Boot.ini 파일의 **[운영 체제]** 섹션에서 운영 체제 항목에 문자열로 지정 된 운영 체제 로드 옵션을 추가 합니다.

## <a name="syntax"></a>구문
```
bootcfg /raw [/s <computer> [/u <Domain>\<User> /p <Password>]] <OSLoadOptionsString> [/id <OSEntryLineNum>] [/a]
```
## <a name="parameters"></a>매개 변수

|         용어          |                                                                                                            정의                                                                                                             |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     /s <computer>     |                                                        이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                                         |
| /u <Domain> \\<User>  |               <User> 또는 <Domain>\\<User>에 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한.                |
|     /p <Password>     |                                                                       에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                                       |
| <OSLoadOptionsString> | 운영 체제 항목에 추가할 운영 체제 로드 옵션을 지정 합니다. 이러한 로드 옵션은 운영 체제 항목과 관련 된 모든 기존 로드 옵션을 대체 합니다. <OSLoadOptions>의 유효성 검사가 수행 되지 않습니다. |
| /id <OSEntryLineNum>  |                       업데이트할 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다.                       |
|          / a           |                                                       추가 되는 운영 체제 옵션을 기존 운영 체제 옵션에 추가 하도록 지정 합니다.                                                        |
|          /?           |                                                                                               명령 프롬프트에 도움말을 표시합니다.                                                                                                |

##### <a name="remarks"></a>설명
- **bootcfg raw** 는 운영 체제 항목의 끝에 텍스트를 추가 하 여 기존 운영 체제 항목 옵션을 덮어쓰는 데 사용 됩니다. 이 텍스트에는 **/debug**, **/fastdetect**, **/nodebug**, **/srrl**, **/crashdebug**및 **/sos**와 같은 올바른 OS 로드 옵션이 포함 되어야 합니다. 예를 들어 다음 명령은 첫 번째 운영 체제 항목의 끝에 " **/debug/fastdetect**"를 추가 하 여 이전 운영 체제 항목 옵션을 대체 합니다.
  ```
  bootcfg /raw "/debug /fastdetect" /id 1
  ```
  ## <a name="BKMK_examples"></a>예와
  다음 예에서는 **bootcfg/raw** 명령을 사용 하는 방법을 보여 줍니다.
  ```
  bootcfg /raw "/debug /sos" /id 2
  bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 "/crashdebug " /id 2
  ```
  #### <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
