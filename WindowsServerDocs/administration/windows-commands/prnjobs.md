---
title: prnjobs
description: 명령줄에서 인쇄 작업을 관리 하는 방법에 알아봅니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ad34199-7a5a-40c1-8053-bccd5929df43
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 03a7f0cf36539272140ea39903bab585b4bc5c72
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889584"
---
# <a name="prnjobs"></a>prnjobs

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

일시 중지, 다시 시작, 취소, 및 인쇄 작업을 나열 합니다.

## <a name="syntax"></a>구문
```
cscript Prnjobs {-z | -m | -x | -l | -?} [-s <ServerName>] 
[-p <printerName>] [-j <JobID>] [-u <UserName>] [-w <Password>]
```

## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|-z|지정 된 인쇄 작업 일시 중지 합니다 **-j** 매개 변수입니다.|
|-M|지정 된 인쇄 작업을 다시 시작 되는 **-j** 매개 변수입니다.|
|-x|지정 된 인쇄 작업을 취소는 **-j** 매개 변수입니다.|
|-l|인쇄 큐에 있는 모든 인쇄 작업을 나열합니다.|
|-s \<ServerName>|프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다.|
|-p \<printerName>|관리 하려는 프린터의 이름을 지정 합니다. 필수.|
|-j \<JobID>|인쇄 작업 취소 하 시겠습니까 (ID 번호)으로 지정 합니다.|
|-u \<UserName> -w <Password>|프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않으면, 작동 하려면 명령에 대 한 이러한 사용 권한이 있는 계정으로 로그온 해야 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   합니다 **prnjobs** 명령입니다는 %WINdir%\System32\printing_Admin_Scripts에 있는 Visual Basic 스크립트\\ <language> 디렉터리입니다. 명령 프롬프트에서이 명령을 사용 하려면 입력 **cscript** 전체 경로 뒤에 prnjobs 파일 또는 디렉터리 적절 한 폴더로 변경 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnjobs
    ```
-   텍스트가 주위에 따옴표를 사용 하 여 사용자가 제공 하는 정보에 공백이 포함 되 면 (예를 들어 `"computer Name"`).

## <a name="BKMK_examples"></a>예제
27 colorprinter 라는 프린터에서 인쇄를 위한 HRServer 라는 원격 컴퓨터에 전송의 작업 ID 사용 하 여 인쇄 작업을 일시 중지 하려면 다음을 입력 합니다.
```
cscript prnjobs -z -s HRServer -p colorprinter -j 27
```
Colorprinter_2 라는 이름의 로컬 프린터 큐에 현재의 모든 인쇄 작업을 나열 하려면 다음을 입력 합니다.
```
cscript prnjobs -l -p colorprinter_2
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[인쇄 명령 참조](print-command-reference.md)
