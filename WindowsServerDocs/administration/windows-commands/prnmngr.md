---
title: prnmngr
description: Prnmngr 명령에 대 한 참조 항목으로, 기본 프린터를 설정 하 고 표시 하는 것 외에도 프린터 또는 프린터 연결을 추가, 삭제 및 나열 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39eee1a8-4b41-4c9f-941e-486495135eb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1ccc04e7e040612d9243fe1e3f5ed67b8131ab9d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472218"
---
# <a name="prnmngr"></a>prnmngr

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

추가, 삭제 하 고, 프린터 또는 프린터 연결 설정 및 기본 프린터를 표시 하는 것 외에도 나열 합니다. 이 명령은 디렉터리에 있는 Visual Basic 스크립트입니다 `%WINdir%\System32\printing_Admin_Scripts\<language>` . 명령 프롬프트에서이 명령을 사용 하려면 **cscript** 다음에 prnmngr 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다. 예를 들어 `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr`을 참조하십시오.

## <a name="syntax"></a>구문

```
cscript prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <Servername>] [-p <Printername>] [-m <printermodel>] [-r <portname>] [-u <Username>]
[-w <password>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| 지정하지 않을 경우 | 로컬 프린터 연결을 추가합니다. |
| -d | 프린터 연결을 삭제합니다. |
| -X | **-S** 매개 변수로 지정 된 서버에서 모든 프린터를 삭제 합니다. 서버를 지정 하지 않으면 Windows에서 로컬 컴퓨터의 모든 프린터를 삭제 합니다. |
| -g | 기본 프린터를 표시합니다. |
| -t | 로 지정 된 프린터를 기본 프린터로 설정의 **-p** 매개 변수입니다. |
| -l | 지정한 서버에 설치 된 모든 프린터를 나열 된 **-s** 매개 변수입니다. 서버를 지정 하지 않으면 Windows에서 로컬 컴퓨터에 설치 된 프린터를 나열 합니다. |
| c | 프린터 연결에 매개 변수가 적용 되도록 지정 합니다. 와 함께 사용할 수는 **-** 및 **-x** 매개 변수입니다. |
| -s`<Servername>` | 프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다. |
| -p `<Printername>` | 관리 하려는 프린터의 이름을 지정 합니다. |
| -m`<Modelname>` | 이름을 사용 하 여 드라이버를 설치 하려면 지정 합니다. 드라이버가 지 원하는 프린터 모델에 대 한 자주 라고 합니다. 자세한 내용은 프린터 설명서를 참조 하십시오. |
| -r`<portname>` | 프린터가 연결 되어 있는 포트를 지정 합니다. 포트의 ID를 사용 하 여 병렬 또는 직렬 포트 인 경우 (예를 들어 LPT1: 또는 c o m 1:). TCP/IP 포트 이면 포트를 추가할 때 지정 된 포트 이름을 사용 합니다. |
| -u `<Username>` -w`<password>` | 프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않는 경우 명령이 작동 하려면 이러한 권한이 있는 계정으로 로그온 해야 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예: "컴퓨터 이름").

### <a name="examples"></a>예제

로컬 컴퓨터의 LPT1에 연결 된 colorprinter_2 이라는 프린터를 추가 하 고 컬러 프린터 Driver1 이라는 프린터 드라이버가 필요한 경우 다음을 입력 합니다.

```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```

HRServer 이라는 원격 컴퓨터에서 이름이 colorprinter_2 인 프린터를 삭제 하려면 다음을 입력 합니다.

```
cscript prnmngr -d -s HRServer -p colorprinter_2
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)
