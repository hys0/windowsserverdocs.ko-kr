---
title: getmac
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a749a348-7cd1-4336-9f33-bb42dd0e31e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c770f5da5159e0037af479f90fadb4cd83464c77
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375814"
---
# <a name="getmac"></a>getmac

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

반환 미디어 제어 (MAC) 주소 및 네트워크 프로토콜에 연결 된 각 컴퓨터에 모든 네트워크 카드에 대 한 각 주소 하거나 로컬 또는 네트워크를 통해 목록에 액세스 합니다. 
## <a name="syntax"></a>구문
```
getmac[.exe][/s <computer> [/u <Domain\<User> [/p <Password>]]][/fo {TABLE | list | CSV}][/nh][/v]
```
### <a name="parameters"></a>매개 변수

|             매개 변수              |                                                                                          설명                                                                                          |
|------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /s <computer>            |                                      이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.                                       |
|        /u <Domain> @ no__t-1 @ no__t-2         | 사용자 또는 도메인 \ 사용자가 지정 된 사용자의 계정 권한으로 명령을 실행 합니다. 기본값은 현재 로그온 된 명령을 실행 하는 컴퓨터에서 사용자의 사용 권한. |
|           /p <Password>            |                                                     에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.                                                     |
| /fo {테이블 &#124; 목록&#124; CSV} |                       쿼리 출력에 사용할 형식을 지정 합니다. 유효한 값은 **TABLE**, **list**및 **CSV**입니다. 출력에 대 한 기본 형식은 **테이블**합니다.                        |
|                /nh                 |                                             출력에서 열 머리글을 표시 하지 않습니다. 유효한 경우에는 **/fo** 매개 변수는 설정 **테이블** 또는 **CSV**합니다.                                              |
|                 /v                 |                                                                    출력이 자세한 정보를 표시 하도록 지정 합니다.                                                                     |
|                 /?                 |                                                                                                                                                                                               |

## <a name="remarks"></a>설명
**getmac** 는 네트워크 분석기에 MAC 주소를 입력 하거나 컴퓨터의 각 네트워크 어댑터에서 현재 사용 중인 프로토콜을 알아야 할 때 유용할 수 있습니다.
## <a name="BKMK_Examples"></a>예와
다음 예제에서는 사용 하는 방법을 보여는 **getmac** 명령:
```
getmac /fo table /nh /v
```
```
getmac /s srvmain
```
```
getmac /s srvmain /u maindom\hiropln
```
```
getmac /s srvmain /u maindom\hiropln /p p@ssW23
```
```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo list /v
```
```
getmac /s srvmain /u maindom\hiropln /p p@ssW23 /fo table /nh
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
