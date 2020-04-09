---
title: bitsadmin setclientcertificatebyname
description: HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 주체 이름을 지정 하는 bitsadmin setclientcertificatebyname에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f308a6d9-d0da-48be-ae41-eced14b3cccb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 08ec6fd8c941234de36f14cd71ffa51c3b428acb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849656"
---
# <a name="bitsadmin-setclientcertificatebyname"></a>bitsadmin setclientcertificatebyname

HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서의 주체 이름을 지정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetClientCertificateByID <Job> <store_location> <store_name> <subject_name>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|Store_location|인증서를 찾는 데 사용할 시스템 저장소의 위치를 식별 합니다. 가능한 값은 다음과 같습니다.</br>1 (CURRENT_USER)</br>2 (LOCAL_MACHINE)</br>3 (CURRENT_SERVICE)</br>4 (서비스)</br>5 (사용자)</br>6 (CURRENT_USER_GROUP_POLICY)</br>7 (LOCAL_MACHINE_GROUP_POLICY)</br>8 (LOCAL_MACHINE_ENTERPRISE)|
|Store_name|인증서 저장소의 이름입니다. 가능한 값은 다음과 같습니다.</br>CA (인증 기관 인증서)</br>내 (개인 인증서)</br>루트 (루트 인증서)</br>SPC (소프트웨어 게시자 인증서)|
|Subject_name|인증서의 이름|

## <a name="examples"></a><a name=BKMK_examples></a>예와

다음 예제에서는 *mycertificate*이라는 작업에 대 한 HTTPS (SSL) 요청에서 클라이언트 인증에 사용할 클라이언트 인증서 *mycertificate* 의 이름을 지정 합니다.
```
C:\>bitsadmin Bitsadmin /SetClientCertificateByName myJob 1 MY myCertificate 
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)