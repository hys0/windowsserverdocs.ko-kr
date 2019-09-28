---
title: driverquery
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d44a1be300b7178bc2271187344c2fc4ab8815e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377646"
---
# <a name="driverquery"></a>driverquery



관리자가 설치 된 장치 드라이버 및 해당 속성의 목록을 표시 합니다. 매개 변수 없이 사용 하는 경우 **driverquery** 로컬 컴퓨터에서 실행 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
driverquery [/s <System> [/u [<Domain>\]<Username> [/p <Password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

## <a name="parameters"></a>매개 변수

|         매개 변수         |                                                                                                                                         설명                                                                                                                                          |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s \<System >        |                                                                                      이름 또는 원격 컴퓨터의 IP 주소를 지정합니다. 백슬래시를 사용 하지 마십시오. 기본값은 로컬 컴퓨터입니다.                                                                                       |
| /u [\<Domain > \] @ no__t-2 | *사용자* 또는 *도메인*\*user @ no__t-3에 지정 된 대로 사용자 계정의 자격 증명을 사용 하 여 명령을 실행 합니다. 기본적으로 \* @ no__t-1/s @ no__t-2 @ no__t-3은 명령을 실행 하는 컴퓨터에 현재 로그온 한 사용자의 자격 증명을 사용 합니다. **/u** 않으면 사용할 수 없습니다 **/s** 지정 됩니다. |
|      /p \<암호 >       |                                                                           에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다. **/p** 않으면 사용할 수 없습니다 **/u** 지정 됩니다.                                                                            |
|        /fo {테이블         |                                                                                                                                             list                                                                                                                                             |
|            /nh            |                                                                                      표시 된 드라이버 정보에서 머리글 행을 생략합니다. 유효 하지 않은 경우에는 **/fo** 매개 변수는 설정 **목록**합니다.                                                                                      |
|            /v             |                                                                                                               자세한 정보 출력을 표시합니다. **/v** 서명 된 드라이버에 적합 하지 않습니다.                                                                                                               |
|            /si            |                                                                                                                          서명 된 드라이버에 대 한 정보를 제공합니다.                                                                                                                          |
|            /?             |                                                                                                                             명령 프롬프트에 도움말을 표시합니다.                                                                                                                             |

## <a name="BKMK_examples"></a>예와

가 로컬 컴퓨터에 설치 된 장치 드라이버의 목록을 표시 하려면 다음을 입력 합니다.
```
driverquery 
```
쉼표로 구분 된 값 (CSV) 형식으로 출력을 표시 하려면 다음을 입력 합니다.
```
driverquery /fo csv 
```
출력에 머리글 행을 숨기려면 다음을 입력 합니다.
```
driverquery /nh 
```
사용 하는 **driverquery** 라는 원격 서버에 명령을 **server1** 현재 자격 증명을 사용 하 여 로컬 컴퓨터에를 입력 합니다.
```
driverquery /s server1
```
사용 하는 **driverquery** 라는 원격 서버에 명령을 **server1** 에 대 한 자격 증명을 사용 하 여 **user1** 도메인에 **maindom**, 유형:
```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)