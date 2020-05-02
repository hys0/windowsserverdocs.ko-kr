---
title: bitsadmin setaclflag
description: Bitsadmin setaclflag 명령에 대 한 참조 항목으로, ACL (액세스 제어 목록) 전파 플래그를 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1852bd267fe22825d55f7522a81179e9290e2a00
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716984"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

작업에 대 한 ACL (액세스 제어 목록) 전파 플래그를 설정 합니다. 플래그는 다운로드 하는 파일을 사용 하 여 소유자 및 ACL 정보를 유지 관리 하려는 경우를 의미 합니다. 예를 들어 파일을 사용 하 여 소유자와 그룹을 유지 하려면 **flags** 매개 변수를 `og`로 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setaclflag <job> <flags>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| flags | 다음을 포함 하 여 하나 이상의 값을 지정 합니다.<ul><li>**o** -파일을 사용 하 여 소유자 정보를 복사 합니다.</li><li>**g** -파일을 사용 하 여 그룹 정보를 복사 합니다.</li><li>**d** -파일을 사용 하 여 DACL (임의 액세스 제어 목록) 정보를 복사 합니다.</li><li>**s** -파일이 포함 된 SACL (시스템 액세스 제어 목록) 정보를 복사 합니다.</li></ul> |

## <a name="examples"></a>예

이름이 *Mydownloadjob*인 작업에 대 한 액세스 제어 목록 전파 플래그를 설정 하려면 다운로드 한 파일을 사용 하 여 소유자 및 그룹 정보를 유지 관리 합니다.

```
bitsadmin /setaclflags myDownloadJob og
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
