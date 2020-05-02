---
title: bitsadmin setclientcertificatebyid
description: HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 식별자를 지정 하는 bitsadmin setclientcertificatebyid 명령에 대 한 참조 항목
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8585a7a1-7472-437b-b04a-a11925782a3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 24f5d0b9cda9fecc70611d8eaa21b0c8976c4c7c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719338"
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
| 작업(job) | 작업의 표시 이름 또는 GUID입니다. |
| store_location | 다음을 포함 하 여 인증서를 조회 하는 데 사용할 시스템 저장소의 위치를 식별 합니다.<ul><li>CURRENT_USER</li><li>LOCAL_MACHINE</li><li>CURRENT_SERVICE</li><li>서비스</li><li>사용자</li><li>CURRENT_USER_GROUP_POLICY</li><li>LOCAL_MACHINE_GROUP_POLICY</li><li>LOCAL_MACHINE_ENTERPRISE.</li></ul> |
| store_name | 인증서 저장소의 이름으로 다음을 포함 합니다.<ul><li>CA (인증 기관 인증서)</li><li>내 (개인 인증서)</li><li>루트 (루트 인증서)</li><li>SPC (소프트웨어 게시자 인증서).</li></ul> |
| hexadecimal_cert_id | 인증서의 해시를 나타내는 16 진수입니다. |

## <a name="examples"></a>예

: *Mydownloadjob*이라는 작업에 대 한 HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 식별자를 지정 합니다.

```
bitsadmin /setclientcertificatebyid myDownloadJob BG_CERT_STORE_LOCATION_CURRENT_USER MY A106B52356D3FBCD1853A41B619358BD
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
