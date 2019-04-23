---
title: bitsadmin util 및 setieproxy
description: Windows 명령 항목에 대 한 **bitsadmin util 및 setieproxy** -서비스 계정을 사용 하 여 파일을 전송할 때 사용할 프록시 설정을 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d4f6ab2e52284895d2e7918364c24bbb69f2b1c9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853514"
---
# <a name="bitsadmin-util-and-setieproxy"></a>bitsadmin util 및 setieproxy

서비스 계정을 사용 하 여 파일을 전송할 때 사용 하 여 프록시 설정을 지정 합니다.

**BITSAdmin 1.5 및 이전 버전**: 지원되지 않습니다.

## <a name="syntax"></a>구문

```
bitsadmin /Util /SetIEProxy <Account> <Usage>[/Conn <ConnectionName>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|계정|프록시 설정을 정의 하려면 서비스 계정의 형식을 지정 합니다. 가능한 값은</br>-LOCALSYSTEM</br>-NETWORKSERVICE</br>-LOCALSERVICE|
|사용법|프록시 검색을 사용 하 여 폼을 지정 합니다. 가능한 값은</br>-NO_PROXY-프록시 서버를 사용 하지 않습니다.</br>자동 감지-프록시 설정 자동 검색 합니다.</br>-MANUAL_PROXY-명시적 프록시 목록을 사용 하 고 바이패스 목록입니다. 프록시 목록을 지정 하 고 바이패스 목록 사용 태그 바로 뒤에 키를 누릅니다. 예를 들어, MANUAL_PROXY proxy1 proxy2 NULL입니다.</br>    -프록시 목록에는 사용할 프록시 서버의 쉼표로 구분 된 목록입니다.</br>    무시 목록-은 공백으로 구분 된 목록 호스트 이름 또는 IP 주소 또는 둘 다에는 전송에 프록시를 통해 라우팅될를 하지. 이 수 \<로컬 > 동일한 LAN에 있는 모든 서버를 가리키도록 합니다. NULL 값 또는 ""는 빈 프록시 무시 목록에 사용할 수 있습니다.</br>-AUTOSCRIPT — 동일 자동 검색을 제외 하 고 스크립트를 실행 합니다. 사용 현황 태그 바로 뒤에 스크립트 URL을 지정 합니다. 예를 들어 AUTOSCRIPT http://server/proxy.js합니다.</br>재설정-NO_PROXY를 제외 하 고 동일 수동 프록시 Url을 지정 하는 경우 제거한 Url 자동 검색을 사용 하 여 검색 합니다.|
|연결 이름|선택적-사용한 합니다 **/conn** 매개 변수를 사용 하 여 모뎀 연결을 지정 합니다. 지정 하지 않으면 경우는 **/conn** 매개 변수, BITS LAN 연결을 사용 합니다. 바로 뒤에 모뎀 연결 이름 지정은 **/conn** 매개 변수입니다.|

## <a name="remarks"></a>설명

이 스위치를 사용 하 여 각 연속 호출 이전에 지정 된 사용 하지만 이전에 정의 된 사용량의 매개 변수가 아니라 대체 합니다. 예를 들어 별도 호출에서 NO_PROXY, 자동 검색 및 MANUAL_PROXY를 지정 하면 BITS 마지막 제공 된 사용량을 사용 하 여 되지만 이전에 정의 된 사용으로 인해 매개 변수를 유지 합니다.

> [!IMPORTANT]
> 성공적으로 완료 하려면 관리자 권한 명령 프롬프트에서이 명령을 실행 해야 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 네트워크 서비스 계정에 대 한 프록시 사용을 설정합니다.

```
C:\>bitsadmin /Util /SetIEProxy localsystem AUTODETECT
```

더 많은 예제는 다음과 같습니다.

```
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1,proxy2,proxy3 NULL
bitsadmin /util /setieproxy localsystem MANUAL_PROXY proxy1:80 ""
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)