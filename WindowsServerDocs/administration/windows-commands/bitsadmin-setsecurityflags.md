---
title: bitsadmin setsecurityflags
description: BITS에서 인증서 해지 목록을 확인 하 고 특정 인증서 오류를 무시 하 고 서버가 HTTP 요청을 리디렉션할 때 사용할 정책을 정의 하는 bitsadmin setsecurityflags 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f6030316396e64c9884d6df9b56d5489ec2c6318
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927506"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags

BITS에서 인증서 해지 목록을 확인 하 고, 특정 인증서 오류를 무시 하 고, 서버가 HTTP 요청을 리디렉션할 때 사용할 정책을 정의 하도록 HTTP에 대 한 보안 플래그를 설정 합니다. 값은 부호 없는 정수입니다.

## <a name="syntax"></a>구문

```
bitsadmin /setsecurityflags <job> <value>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| 값 | 다음과 같은 알림 플래그 중 하나 이상을 포함할 수 있습니다.<ul><li>CRL 확인을 사용 하려면 최하위 비트를 설정 합니다.</li><li>서버 인증서의 잘못 된 일반 이름을 무시 하려면 오른쪽에서 두 번째 비트를 설정 합니다.</li><li>서버 인증서에서 잘못 된 날짜를 무시 하려면 오른쪽에서 3 비트를 설정 합니다.</li><li>서버 인증서에서 잘못 된 인증 기관을 무시 하려면 오른쪽에서 4 번째 비트를 설정 합니다.</li><li>서버 인증서의 잘못 된 사용을 무시 하려면 오른쪽에서 5 번째 비트를 설정 합니다.</li><li>다음을 포함 하 여 지정 된 리디렉션 정책을 구현 하기 위해 오른쪽에서 11 비트까지 9를 설정 합니다.<ul><li>**0, 0, 0입니다.** 리디렉션은 자동으로 허용 됩니다.</li><li>**0, 0, 1입니다.** 리디렉션이 발생 하면 **IBackgroundCopyFile** 인터페이스의 원격 이름이 업데이트 됩니다.</li><li>**0, 1, 0입니다.** 리디렉션이 발생 하면 BITS에서 작업에 실패 합니다.</li></ul></li><li>HTTPS에서 HTTP로의 리디렉션을 허용 하려면 오른쪽에서 12 비트를 설정 합니다.</li></ul> |

## <a name="examples"></a>예

보안 플래그를 설정 하 여 이름이 *Mydownloadjob*인 작업에 대 한 CRL 확인을 사용 하도록 설정 합니다.

```
bitsadmin /setsecurityflags myDownloadJob 0x0001
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
