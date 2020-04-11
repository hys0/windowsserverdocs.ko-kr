---
title: bitsadmin setclientcertificatebyname
description: HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 주체 이름을 지정 하는 **bitsadmin setclientcertificatebyname**에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f2308bb5331f1555965b278a64bb7ab95e03779b
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123052"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname

HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 주체 이름을 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setclientcertificatebyname <job> <store_location> <store_name> <subject_name>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| store_location | 인증서를 찾는 데 사용할 시스템 저장소의 위치를 식별 합니다. 가능한 값은 다음과 같습니다.<ul><li>1 (CURRENT_USER)</li><li>2 (LOCAL_MACHINE)</li><li>3 (CURRENT_SERVICE)</li><li>4 (서비스)</li><li>5 (사용자)</li><li>6 (CURRENT_USER_GROUP_POLICY)</li><li>7 (LOCAL_MACHINE_GROUP_POLICY)</li><li>8 (LOCAL_MACHINE_ENTERPRISE)</li></ul> |
| store_name | 인증서 저장소의 이름입니다. 가능한 값은 다음과 같습니다.<ul><li>CA (인증 기관 인증서)</li><li>내 (개인 인증서)</li><li>루트 (루트 인증서)</li><li>SPC (소프트웨어 게시자 인증서)</li></ul> |
| subject_name | 인증서의 이름입니다. |

## <a name="examples"></a>예

다음 예제에서는 *Mydownloadjob*이라는 작업에 대 한 HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서 *mycertificate* 의 이름을 지정 합니다.

```
C:\>bitsadmin /setclientcertificatebyname myDownloadJob 1 MY myCertificate
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)