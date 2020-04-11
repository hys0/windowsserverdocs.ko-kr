---
title: bitsadmin setclientcertificatebyid
description: HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 식별자를 지정 하는 **bitsadmin setclientcertificatebyid**에 대 한 Windows 명령 항목
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 376bb850664a5ed569488634029cb7384856f158
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123043"
---
# <a name="bitsadmin-setclientcertificatebyid"></a>bitsadmin setclientcertificatebyid

HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 식별자를 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /setclientcertificatebyid <job> <store_location> <store_name> <hexadecimal_cert_id>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| -------------- | -------------- |
| 제출 | 작업의 표시 이름 또는 GUID입니다. |
| store_location | 다음을 포함 하 여 인증서를 조회 하는 데 사용할 시스템 저장소의 위치를 식별 합니다.<ul><li>CURRENT_USER</li><li>LOCAL_MACHINE</li><li>CURRENT_SERVICE</li><li>서비스</li><li>사용자</li><li>CURRENT_USER_GROUP_POLICY</li><li>LOCAL_MACHINE_GROUP_POLICY</li><li>LOCAL_MACHINE_ENTERPRISE.</li></ul> |
| store_name | 인증서 저장소의 이름으로 다음을 포함 합니다.<ul><li>CA (인증 기관 인증서)</li><li>내 (개인 인증서)</li><li>루트 (루트 인증서)</li><li>SPC (소프트웨어 게시자 인증서).</li></ul> |
| hexadecimal_cert_id | 인증서의 해시를 나타내는 16 진수입니다. |

## <a name="examples"></a>예

다음 예제에서는 명명 된 작업에 대 한 HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 식별자를 지정 *Mydownloadjob*합니다.

```
C:\>bitsadmin /setclientcertificatebyid myDownloadJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)