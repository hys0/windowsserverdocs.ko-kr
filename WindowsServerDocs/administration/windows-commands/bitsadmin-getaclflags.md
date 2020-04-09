---
title: bitsadmin getaclflags
description: ACL (액세스 제어 목록) 전파 플래그를 검색 하는 **bitsadmin getaclflags**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d53018e2fa5c659c8cf4b0ec985beda848a8c1af
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850796"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

자식 개체에 의해 항목이 상속 되는지 여부를 반영 하 여 ACL (액세스 제어 목록) 전파 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /getaclflags <job>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |

## <a name="remarks"></a>주의

다음 플래그 값 중 하나 이상을 표시합니다.

- **o** -파일을 사용 하 여 소유자 정보를 복사 합니다.

- **g** -파일을 사용 하 여 그룹 정보를 복사 합니다.

- **d** -파일을 사용 하 여 DACL (임의 액세스 제어 목록) 정보를 복사 합니다.

- **s** -파일이 포함 된 SACL (시스템 액세스 제어 목록) 정보를 복사 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 명명 된 작업에 대 한 액세스 제어 목록 전파 플래그 *myDownloadJob*합니다.

```
C:\>bitsadmin /getaclflags myDownloadJob
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)