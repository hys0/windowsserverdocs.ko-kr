---
title: netsh
description: 로컬 또는 원격으로, 현재 실행 중인 컴퓨터의 네트워크 구성을 표시 하거나 수정할 수 있는 명령줄 스크립팅 유틸리티인 netsh 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 96fc069d-53c0-4d0a-9f7f-f9f3d49a02bd carmonmills
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c538dd10f86d252390a4e862e7b97204d1c945c9
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721106"
---
# <a name="netsh"></a>netsh

> 적용 대상: Windows Server(반기 채널), Windows Server 2016

네트워크 셸 명령줄 스크립팅 유틸리티를 사용 하 여 로컬 또는 원격으로, 현재 실행 중인 컴퓨터의 네트워크 구성을 표시 하거나 수정할 수 있습니다. 명령 프롬프트 또는 Windows PowerShell에서이 유틸리티를 시작할 수 있습니다.

## <a name="syntax"></a>구문

```
netsh [-a <Aliasfile>][-c <Context>][-r <Remotecomputer>][-u [<domainname>\<username>][-p <Password> | [{<NetshCommand> | -f <scriptfile>}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| -a`<Aliasfile>` | Aliasfile를 실행 한 후 netsh 프롬프트로 반환 되 고 하나 이상의 netsh 명령이 포함 된 텍스트 파일의 이름을 지정 합니다. |
| -c`<Context>` | 지정 된 netsh 컨텍스트 및 입력할 netsh 컨텍스트를 netsh로 지정 합니다. |
| -r`<Remotecomputer>` | 구성할 원격 컴퓨터를 지정 합니다.<p>**중요:** 이 매개 변수를 사용 하는 경우 원격 컴퓨터에서 원격 레지스트리 서비스가 실행 되 고 있는지 확인 해야 합니다. 실행 되 고 있지 않으면 Windows에 "네트워크 경로를 찾을 수 없음" 오류 메시지가 표시 됩니다. |
| -u`<domainname>\<username>` | 사용자 계정으로 netsh 명령을 실행 하는 동안 사용할 도메인 및 사용자 계정 이름을 지정 합니다. 도메인을 생략 하면 기본적으로 로컬 도메인이 사용 됩니다. |
| -p `<Password>` | 매개 변수로 지정 된 사용자 계정의 암호를 지정 합니다 `-u <username>` . |
| `<NetshCommand>` | 실행할 netsh 명령을 지정 합니다. |
| -f`<scriptfile>` | 지정 된 스크립트 파일을 실행 한 후 netsh 명령을 종료 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

#### <a name="remarks"></a>설명

- **-R** 을 지정 하 고 다른 명령을 지정 하면 netsh는 원격 컴퓨터에서 명령을 실행 한 다음 Cmd.exe 명령 프롬프트로 돌아갑니다. 다른 명령 없이 **-r** 을 지정 하면 netsh가 원격 모드에서 열립니다. 이 프로세스는 Netsh 명령 프롬프트에서 **set machine**을 사용하는 것과 비슷합니다. **-R**을 사용 하는 경우 netsh의 현재 인스턴스에 대해서만 대상 컴퓨터를 설정 합니다. netsh를 종료하고 다시 입력하면 대상 컴퓨터가 로컬 컴퓨터로 다시 설정됩니다. WINS에 저장된 컴퓨터 이름, UNC 이름, DNS 서버에서 확인할 인터넷 이름 또는 IP 주소를 지정하여 원격 컴퓨터에서 netsh 명령을 실행할 수 있습니다.

- 문자열 값이 문자 사이에 공백을 포함 하는 경우 문자열 값을 큰따옴표로 묶어야 합니다. 예를 들어 `-r "contoso remote device"`

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
