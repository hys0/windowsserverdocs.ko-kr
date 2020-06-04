---
title: msinfo32
description: Msinfo32 명령에 대 한 참조 항목-시스템 정보 도구를 열어 로컬 컴퓨터의 하드웨어, 시스템 구성 요소 및 소프트웨어 환경에 대 한 포괄적인 보기를 표시 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a38f31d7-1766-4103-becc-9d0b87c2826d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6a97902d9988260a840d236e197d7361bcd3882
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354435"
---
# <a name="msinfo32"></a>msinfo32

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

로컬 컴퓨터의 하드웨어, 시스템 구성 요소 및 소프트웨어 환경에 대 한 종합적인 보기를 표시 하려면 시스템 정보 도구를 엽니다.

일부 시스템 정보 범주는 많은 양의 데이터를 포함합니다. 사용할 수는 **start /wait** 명령을 이러한 범주에 대 한 보고 성능을 최적화할 수 있습니다. 자세한 내용은 참조 [시스템 정보](https://technet.microsoft.com/library/cc783305(v=ws.10).aspx)합니다.

## <a name="syntax"></a>구문

```
msinfo32 [/pch] [/nfo <path>] [/report <path>] [/computer <computername>] [/showcategories] [/category <categoryID>] [/categories {+<categoryID>(+<categoryID>)|+all(-<categoryID>)}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| `<path>` | *C:\folder1\file1.xxx*형식으로 열 파일을 지정 합니다. 여기서 *C* 는 드라이브 문자이 고, *Folder1* 는 폴더이 고, *File1* 은 파일 이름이 며, *xxx* 는 파일 이름 확장명입니다.<p>이 파일은 한 **.nfo**, **.xml**, **.txt**, 또는 **.cab** 파일입니다. |
| `<computername>` | 대상 또는 로컬 컴퓨터의 이름을 지정합니다. 이 UNC 이름, IP 주소 또는 전체 컴퓨터 이름 수 있습니다. |
| `<categoryID>` | 범주 항목의 ID를 지정합니다. 사용 하 여 범주 ID를 얻을 수 **/showcategories**합니다. |
| /pch | 시스템 정보 도구에서 시스템 기록 보기를 표시합니다. |
| /nfo | 내보낸된 파일을 저장 한 **.nfo** 파일입니다. *경로* 에 지정 된 파일 이름이 **.nfo** 확장명으로 끝나지 않는 경우 **.nfo** 확장명이 파일 이름에 자동으로 추가 됩니다. |
| /report | *경로* 에 파일을 텍스트 파일로 저장 합니다. 파일 이름은 *경로*에 나타난 대로 정확 하 게 저장 됩니다. 경로에 지정 된 경우를 제외 하 고는 .txt 확장명이 파일에 추가 되지 않습니다. |
| / 컴퓨터 | 지정된 된 원격 컴퓨터에 대 한 시스템 정보 도구를 시작합니다. 원격 컴퓨터에 액세스 하려면 적절 한 사용 권한이 있어야 합니다. |
| /showcategories | 이름 또는 지역화 된 이름을 표시 하지 않고 Id를 표시 하는 사용 가능한 모든 범주와 시스템 정보 도구를 시작 합니다. 소프트웨어 환경 범주도 표시 하는 예를 들어는 **SWEnv** 범주입니다. |
| /category | 지정 된 범주를 선택 하 여 시스템 정보를 시작 합니다. 사용 하 여 **/showcategories** 사용 가능한 범주 Id의 목록을 표시 합니다. |
| /categories | 지정 된 범주 또는 범주를 표시 하 여 시스템 정보를 시작 합니다. 또한 선택한 범주 또는 범주에 대 한 출력을 제한합니다. 사용 하 여 **/showcategories** 사용 가능한 범주 Id의 목록을 표시 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

### <a name="examples"></a>예

사용 가능한 범주 Id를 나열 하려면 다음을 입력 합니다.

```
msinfo32 /showcategories
```

사용 가능한 모든 정보를 시스템 정보 도구를 시작 하려면를 제외 하 고 표시 로드 된 모듈, 형식:

```
msinfo32 /categories +all -loadedmodules
```

시스템 **요약** 정보를 표시 하 고 **시스템 요약** 범주의 정보를 포함 하는 *syssum .nfo*이라는 .nfo 파일을 만들려면 다음을 입력 합니다.

```
msinfo32 /nfo syssum.nfo /categories +systemsummary
```

리소스 충돌 정보를 표시 하 고 리소스 충돌에 대 한 정보를 포함 하는 *충돌 .nfo*이라는 .nfo 파일을 만들려면 다음을 입력 합니다.

```
msinfo32 /nfo conflicts.nfo /categories +componentsproblemdevices+resourcesconflicts+resourcesforcedhardware
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
