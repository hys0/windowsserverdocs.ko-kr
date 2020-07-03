---
title: bitsadmin setpeercachingflags
description: Bitsadmin setpeercachingflags 명령에 대 한 참조 문서-작업의 파일을 캐시 하 고 동료에 게 제공할 수 있는지 여부와 작업에서 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 플래그를 설정 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3340c14bfaaaa4f904ac9cf7918588e45c8bdc57
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927604"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags

피어에서 콘텐츠는 작업의 파일을 캐시 하 고 동료에 게 제공 하 고 작업을 다운로드할 수 하는 경우를 결정 하는 플래그를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setpeercachingflags <job> <value>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| 값 | 다음을 포함 하는 부호 없는 정수입니다.<ul><li>**1.** 작업에서 피어에서 콘텐츠를 다운로드할 수 있습니다.</li><li>**2.** 작업의 파일을 캐시 하 고 동료에 게 제공할 수 있습니다.</li></ul> |

## <a name="examples"></a>예

*Mydownloadjob* 이라는 작업에서 피어의 콘텐츠를 다운로드 하도록 허용 하려면 다음을 수행 합니다.

```
bitsadmin /setpeercachingflags myDownloadJob 1
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
