---
title: bootcfg default
description: '**Bootcfg 기본값** 에 대 한 Windows 명령 항목-기본값으로 지정할 운영 체제 항목을 지정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e21824d7-8278-41d7-a2c5-ce09803d513a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e69868739a9c338b711984ba0f03452f307b430b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380018"
---
# <a name="bootcfg-default"></a>bootcfg default

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

기본적으로 지정 하려면 운영 체제 항목을 지정 합니다.

## <a name="syntax"></a>구문
```
bootcfg /default [/s <computer> [/u <Domain>\<User> /p <Password>]] [/id <OSEntryLineNum>]
```
## <a name="parameters"></a>매개 변수

|      매개 변수       |                                                                                             설명                                                                                              |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /s <computer>     |                                          이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                          |
| /u <Domain> @ no__t-1 @ no__t-2  | @No__t-0 또는 <Domain> @ no__t @ no__t-3로 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
|    /p <Password>     |                                                        에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                         |
| /id <OSEntryLineNum> | 기본값으로 지정할 Boot.ini 파일의 [운영 체제] 섹션에 운영 체제 항목 줄 번호를 지정 합니다. [운영 체제] 섹션 헤더 후 첫 번째 줄은 1입니다.  |
|          /?          |                                                                                 명령 프롬프트에 도움말을 표시합니다.                                                                                 |

## <a name="BKMK_examples"></a>예와
다음 예에서는 **bootcfg/default**명령을 사용 하는 방법을 보여 줍니다.
```
bootcfg /default /id 2
bootcfg /default /s srvmain /u maindom\hiropln /p p@ssW23 /id 2
```
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
