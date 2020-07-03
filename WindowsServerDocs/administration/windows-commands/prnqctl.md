---
title: prnqctl
description: 테스트 페이지를 인쇄 하 고 프린터를 일시 중지 하거나 다시 시작 하는 prnqctl.vbs 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8df9dfa7-984c-4276-bb7d-e7675e7c399e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 7bcc6a36fb2387a82e25afd41be2d22615565bfe
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931155"
---
# <a name="prnqctl"></a>prnqctl

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

테스트 페이지를 인쇄, 일시 중지 하거나 프린터를 다시 시작 및 프린터 큐를 삭제 합니다. 이 명령은 디렉터리에 있는 Visual Basic 스크립트입니다 `%WINdir%\System32\printing_Admin_Scripts\<language>` . 명령 프롬프트에서이 명령을 사용 하려면 **cscript** 다음에 prnqctl.vbs 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다. 예를 들어 `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnqctl`을 참조하십시오.

## <a name="syntax"></a>구문

```
cscript Prnqctl {-z | -m | -e | -x | -?} [-s <Servername>] [-p <Printername>] [-u <Username>] [-w <password>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| -Z | **-P** 매개 변수로 지정 된 프린터에서 인쇄를 일시 중지 합니다. |
| -M | **-P** 매개 변수로 지정 된 프린터에서 인쇄를 다시 시작 합니다. |
| -E | **-P** 매개 변수로 지정 된 프린터에서 테스트 페이지를 인쇄 합니다. |
| -X | **-P** 매개 변수로 지정 된 프린터의 모든 인쇄 작업을 취소 합니다. |
| -s`<Servername>` | 프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다. |
| -p `<Printername>` | 필수 요소. 관리 하려는 프린터의 이름을 지정 합니다. |
| -u `<Username>` -w`<password>` | 프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않는 경우 명령이 작동 하려면 이러한 권한이 있는 계정으로 로그온 해야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예: "컴퓨터 이름").

### <a name="examples"></a>예

Server1 컴퓨터에서 공유 하는 Laserprinter1 프린터에서 테스트 페이지를 인쇄 하려면 \\ 다음을 입력 합니다.

```
cscript prnqctl -e -s Server1 -p Laserprinter1
```

로컬 컴퓨터의 Laserprinter1 프린터에서 인쇄를 일시 중지 하려면 다음을 입력 합니다.

```
cscript prnqctl -z -p Laserprinter1
```

로컬 컴퓨터에서 Laserprinter1 프린터의 모든 인쇄 작업을 취소 하려면 다음을 입력 합니다.

```
cscript prnqctl -x -p Laserprinter1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)
