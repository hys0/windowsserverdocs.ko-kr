---
title: manage-bde keypackage
description: 드라이브의 키 패키지를 생성 하는 manage-bde keypackage command에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c631ef10-2a2f-4541-8578-292f2d4e9e80
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4bdbd9bb46b75e7dc87cae1cd6e9b3a101ff91ff
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928565"
---
# <a name="manage-bde-keypackage"></a>manage-bde keypackage

드라이브에 대 한 키 패키지를 생성합니다. 키 패키지를 손상 된 드라이브를 복구 하려면 복구 도구와 함께에서 사용할 수 있습니다.

## <a name="syntax"></a>구문

```
manage-bde -keypackage [<drive>] [-ID <keyprotectoryID>] [-path <pathtoexternalkeydirectory>] [-computername <name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<drive>` | 드라이브 문자를 뒤에 콜론을 나타냅니다. |
| -ID | 이 ID 값으로 지정 된 식별자와 함께 키 보호기를 사용 하 여 키 패키지를 만듭니다. **팁:** 키 패키지를 만들려는 드라이브 문자와 함께 **manage-bde – protectors – get** 명령을 사용 하 여 ID 값으로 사용할 사용 가능한 guid 목록을 가져옵니다. |
| -경로 | 만든 키 패키지를 저장할 위치를 지정 합니다. |
| -computername | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

GUID로 식별 되는 키 보호기를 기준으로 C 드라이브에 대 한 키 패키지를 만들고 키 패키지를 F:\Folder에 저장 하려면 다음을 입력 합니다.

```
manage-bde -keypackage C: -id {84E151C1...7A62067A512} -path f:\Folder
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde 명령](manage-bde.md)
