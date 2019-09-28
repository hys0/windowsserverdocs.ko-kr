---
title: bitsadmin util 및 setieproxy
description: '**Bitsadmin util 및 setieproxy** 에 대 한 Windows 명령 항목은 서비스 계정을 사용 하 여 파일을 전송할 때 사용할 프록시 설정을 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0e9f31ba-3070-4ffd-a94c-388c8d78f688
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9d485c0e9cb135febdb1bf99cec4de08d7c9321b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380216"
---
# <a name="bitsadmin-util-and-setieproxy"></a>bitsadmin util 및 setieproxy

서비스 계정을 사용 하 여 파일을 전송할 때 사용 하 여 프록시 설정을 지정 합니다.

**Bitsadmin 1.5 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Util /SetIEProxy <Account> <Usage>[/Conn <ConnectionName>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|계정|프록시 설정을 정의 하려는 서비스 계정의 유형을 지정 합니다. 가능한 값은</br>-LOCALSYSTEM</br>-NETWORKSERVICE</br>-LOCALSERVICE|
|사용법|프록시 검색을 사용 하 여 폼을 지정 합니다. 가능한 값은</br>-NO_PROXY-프록시 서버를 사용 하지 않습니다.</br>-자동 검색-프록시 설정을 자동으로 검색 합니다.</br>-MANUAL_PROXY-명시적 프록시 목록을 사용 하 고 바이패스 목록을 사용 합니다. 프록시 목록을 지정 하 고 바이패스 목록 사용 태그 바로 뒤에 키를 누릅니다. 예를 들어, MANUAL_PROXY proxy1 proxy2 NULL입니다.</br>    -프록시 목록은 사용할 프록시 서버를 쉼표로 구분한 목록입니다.</br>    -바이패스 목록은 호스트 이름 또는 IP 주소의 공백으로 구분 된 목록 또는 둘 다를 사용 하 여 전송을 통해 라우팅할 수 없습니다. 동일한 LAN에 있는 모든 서버를 참조 하는 \<local > 수 있습니다. NULL 값 또는 ""는 빈 프록시 무시 목록에 사용할 수 있습니다.</br>-AUTOSCRIPT-스크립트를 실행 하는 경우를 제외 하 고 자동 검색과 동일 합니다. 사용 현황 태그 바로 뒤에 스크립트 URL을 지정 합니다. 예를 들어 AUTOSCRIPT http://server/proxy.js 입니다.</br>-RESET-NO_PROXY와 동일 합니다. 단, 수동 프록시 Url (지정 된 경우) 및 자동 검색을 사용 하 여 검색 된 Url은 제거 합니다.|
|연결 이름|선택 사항- **/Conn** 매개 변수와 함께 사용 하 여 사용할 모뎀 연결을 지정 합니다. **/Conn** 매개 변수를 지정 하지 않으면 BITS는 LAN 연결을 사용 합니다. 바로 뒤에 모뎀 연결 이름 지정은 **/conn** 매개 변수입니다.|

## <a name="remarks"></a>설명

이 스위치를 사용 하는 각 연속 호출은 이전에 지정 된 사용을 대체 하지만 이전에 정의 된 사용의 매개 변수는 대체 하지 않습니다. 예를 들어 별도 호출에서 NO_PROXY, 자동 검색 및 MANUAL_PROXY를 지정 하면 BITS 마지막 제공 된 사용량을 사용 하 여 되지만 이전에 정의 된 사용으로 인해 매개 변수를 유지 합니다.

> [!IMPORTANT]
> 성공적으로 완료 하려면 관리자 권한 명령 프롬프트에서이 명령을 실행 해야 합니다.

## <a name="examples"></a>예

다음 예제에서는 네트워크 서비스 계정에 대 한 프록시 사용을 설정합니다.

```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```

다음은 추가 예제입니다.

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80 ""
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)