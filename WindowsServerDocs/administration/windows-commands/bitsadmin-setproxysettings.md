---
title: bitsadmin setproxysettings
description: 지정 된 작업에 대 한 프록시 설정을 설정 하는 bitsadmin setproxysettings 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: be8edb1b-614e-4d0b-a8f8-64b4bde3e64b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a59bbb560b8c89134e81c02f99aaecebdb65ca89
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927583"
---
# <a name="bitsadmin-setproxysettings"></a>bitsadmin setproxysettings

지정된 된 작업에 대 한 프록시 설정을 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setproxysettings <job> <usage> [list] [bypass]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| usage | 다음을 포함 하 여 프록시 사용을 설정 합니다.<ul><li>**미리 구성.** 소유자의 Internet Explorer 기본값을 사용 합니다.</li><li>**NO_PROXY.** 프록시 서버를 사용 하지 마세요.</li><li>**덮어쓸.** 명시적 프록시 목록과 바이패스 목록을 사용 합니다. 프록시 목록 및 프록시 바이패스 정보는 다음과 같아야 합니다.</li><li>**자동 검색.** 에서 자동으로 프록시 설정을 검색 합니다.</li></ul> |
| list | *Usage* 매개 변수가 OVERRIDE로 설정 된 경우 사용 됩니다. 사용할 프록시 서버 목록 (쉼표로 구분)을 포함 해야 합니다. |
| 바이패스 | *Usage* 매개 변수가 OVERRIDE로 설정 된 경우 사용 됩니다. 에는 호스트 이름이 나 IP 주소 또는 둘 다의 공백으로 구분 된 목록이 포함 되어야 합니다 .이 경우 전송은 프록시를 통해 라우팅되지 않습니다. 이 수 `<local>` 동일한 LAN에 있는 모든 서버를 가리키도록 합니다. 빈 프록시 무시 목록에 NULL 값을 사용할 수 있습니다. |

## <a name="examples"></a>예

명명 된 작업에 대 한 다양 한 사용 옵션을 사용 하 여 프록시 설정을 설정 *Mydownloadjob*:

```
bitsadmin /setproxysettings myDownloadJob PRECONFIG
```

```
bitsadmin /setproxysettings myDownloadJob NO_PROXY
```
```
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1:80
```

```
bitsadmin /setproxysettings myDownloadJob OVERRIDE proxy1,proxy2,proxy3 NULL
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
