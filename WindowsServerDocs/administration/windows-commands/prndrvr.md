---
title: prndrvr
description: Prndrvr.vbs 명령에 대 한 참조 항목으로, 프린터 드라이버를 추가, 삭제 및 나열 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 62c63819c175f4b3f3770d90da0bd560443ccb77
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472298"
---
# <a name="prndrvr"></a>prndrvr

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

추가, 삭제 하 고 프린터 드라이버를 나열 합니다. 이 명령은 디렉터리에 있는 Visual Basic 스크립트입니다 `%WINdir%\System32\printing_Admin_Scripts\<language>` . 명령 프롬프트에서이 명령을 사용 하려면 **cscript** 다음에 prndrvr.vbs 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다. 예를 들어 `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr`을 참조하십시오.

매개 변수 없이 사용 **prndrvr.vbs** 명령줄 도움말을 표시 합니다.

## <a name="syntax"></a>구문

```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] [-e <environment>] [-s <Servername>] [-u <Username>] [-w <password>] [-h <path>] [-i <inf file>]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
|--|--|
| 지정하지 않을 경우 | 드라이버를 설치합니다. |
| -d | 드라이버를 삭제합니다. |
| -l | 지정한 서버에 설치 된 모든 프린터 드라이버를 나열 된 **-s** 매개 변수입니다. 서버를 지정 하지 않으면 Windows에서 로컬 컴퓨터에 설치 된 프린터 드라이버를 나열 합니다. |
| -X | 지정한 서버에서 논리 프린터에서 모든 프린터 드라이버와 사용 중이 아닌 추가 프린터 드라이버를 삭제는 **-s** 매개 변수입니다. 목록에서 제거할 서버를 지정 하지 않으면 Windows는 로컬 컴퓨터에서 사용 되지 않는 모든 프린터 드라이버를 삭제 합니다. |
| -m`<model_name>` | 이름을 사용 하 여 드라이버를 설치 하려면 지정 합니다. 드라이버가 지 원하는 프린터 모델에 대 한 자주 라고 합니다. 자세한 내용은 프린터 설명서를 참조 하십시오. |
| `-v {0|1|2|3}` | 설치 하려는 드라이버의 버전을 지정 합니다. 에 대 한 설명을 참조는 **-e**버전은 사용할 수 있는 환경에 대 한 정보에 대 한 매개 변수입니다. 버전을 지정 하지 않으면 드라이버를 설치 하는 컴퓨터에서 실행 되는 Windows 버전에 해당 하는 드라이버 버전이 설치 됩니다. |
| -e `<environment>` | 설치 하려는 드라이버에 대 한 환경을 지정 합니다. 환경을 지정 하지 않으면 드라이버를 설치 하는 컴퓨터의 환경이 사용 됩니다. 지원 되는 환경 매개 변수는 **WINDOWS NT x86**, **Windows X64** 또는 **windows IA64**입니다. |
| -s`<Servername>` | 프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다. |
| -u `<Username>` -w`<password>` | 프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않는 경우 명령이 작동 하려면 이러한 권한이 있는 계정으로 로그온 해야 합니다. |
| -h`<path>` | 드라이버 파일의 경로를 지정합니다. 경로를 지정 하지 않으면 Windows가 설치 된 위치에 대 한 경로가 사용 됩니다. |
| -i`<filename.inf>` | 설치 하려는 드라이버에 대 한 전체 경로 파일 이름을 지정 합니다. 파일 이름을 지정 하지 않으면 스크립트는 Windows 디렉터리의 inf 하위 디렉터리에 있는 수신함 프린터 .inf 파일 중 하나를 사용 합니다.<p>드라이버 경로를 지정 하지 않으면 스크립트는 driver.cab 파일에서 드라이버 파일을 검색 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- 사용자가 제공 하는 정보에 공백이 포함 된 경우 텍스트에 따옴표를 사용 합니다 (예: "컴퓨터 이름").

- **-X** 매개 변수는 기본 드라이버를 사용 하는 경우에도 모든 추가 프린터 드라이버 (다른 버전의 Windows를 실행 하는 클라이언트에서 사용 하도록 설치 된 드라이버)를 삭제 합니다. 팩스 구성 요소가 설치 되어 있는 경우이 옵션은 또한 팩스 드라이버 삭제 합니다. 기본 팩스 드라이버가 없는 경우에 (즉, 있는 경우 큐)를 사용 하 여 삭제 됩니다. 기본 팩스 드라이버는 삭제, 팩스를 다시 사용 하도록 설정 하는 유일한 방법은 하는 경우 팩스 구성 요소를 다시 설치 해야 합니다.

### <a name="examples"></a>예

로컬 printServer1 서버에 있는 모든 드라이버를 나열 하려면 \\ 다음을 입력 합니다.

```
cscript prndrvr -l -s
```

C:\temp 폴더에 저장 된 드라이버에 대 한 c:\temp\Laserprinter1.inf 드라이버 정보 파일을 사용 하 여 레이저 프린터 모델 1 프린터용 버전 3 Windows x64 프린터 드라이버를 추가 하려면 다음을 입력 합니다.

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64 -i c:\temp\Laserprinter1.inf -h c:\temp
```

레이저 프린터 모델 1 용 Windows x64 프린터 드라이버 버전 3을 삭제 하려면 다음을 입력 합니다.

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [인쇄 명령 참조](print-command-reference.md)
