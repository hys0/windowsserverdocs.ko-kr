---
title: takeown
description: 파일의 소유자가 되기 때문에 파일에 액세스 하는 방법에 대해 알아봅니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0683cd65-a6db-4cab-962b-45a0ff61f43c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af6952b8c4c14a717f7904ee0b77bf6ec9f5030e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80833447"
---
# <a name="takeown"></a>takeown

관리자를 파일 소유자로 만들어 이전에는 거부된 파일에 대한 관리자의 액세스 권한을 복구할 수 있도록 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
takeown [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <File name> [/a] [/r [/d {Y|N}]]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/s \<컴퓨터 >|이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다. 이 매개 변수는 모든 파일 및 명령에 지정 된 폴더에 적용 됩니다.|
|/u [\<도메인 >\]<User name>|지정된 된 사용자 계정 권한으로 스크립트를 실행합니다. 기본값은 시스템 사용 권한.|
|/p [\<암호 >]|에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.|
|/f \<파일 이름 >|파일 이름이 나 디렉터리 이름 지정 패턴입니다. 패턴을 지정할 때 와일드 카드 문자 *를 사용할 수 있습니다. 또한 *ShareName*\*파일 이름 * 구문을 사용할 수 있습니다.|
|/a|현재 사용자 대신 관리자 그룹에 소유권을 제공합니다.|
|/r|지정 된 디렉터리와 하위 디렉터리의 모든 파일에 대 한 재귀 작업을 수행합니다.|
|/d {Y \| N}|현재 사용자 지정된 된 디렉터리에 "폴더 보기" 권한이 없는 대신 지정 된 기본값을 사용 하는 경우 표시 되는 확인 프롬프트를 표시 하지 않습니다. 에 대 한 유효한 값은 **/d** 옵션은 다음과 같습니다.</br>-Y: 디렉터리의 소유권을 수행 합니다.</br>-N: 컴퓨터의 디렉터리를 건너뜁니다.</br>와 함께에서이 옵션을 사용 해야는 **/r** 옵션입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   이 명령은 배치 파일에서 일반적으로 사용 됩니다.
-   하는 경우는 **/a** 매개 변수를 지정 하지 않으면, 컴퓨터에 현재 로그온 사용자에 게 파일 소유권이 부여 됩니다.
-   혼합된 패턴을 사용 하 여 ( **?** 및 **&#42;** )는 **takeown** 명령에서 지원 되지 않습니다.
-   사용 하 여 잠금을 삭제 한 후 **takeown**, Windows 탐색기를 사용 해야 할 수 있습니다 또는 **cacls** 직접 전체 사용 권한을 부여 하는 파일 및 디렉터리 삭제 하기 전에 명령입니다. 에 대 한 자세한 내용은 **cacls**, 이 항목의 끝에 "추가 참조"를 참조 하십시오.

## <a name="examples"></a><a name="BKMK_examples"></a>예와

소유권을 갖도록 Lostfile 라는 파일을 입력 합니다.
```
takeown /f lostfile
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)