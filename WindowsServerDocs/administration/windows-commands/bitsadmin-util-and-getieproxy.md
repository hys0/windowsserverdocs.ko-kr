---
title: bitsadmin util 및 getieproxy
description: Windows 명령 항목에 대 한 **bitsadmin util 및 getieproxy** -지정한 서비스 계정에 대 한 프록시 사용을 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d50c7e3-f4eb-4ca5-9f0c-4ed396087db6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: de4f86340b1163c4d8e3286d9c86c9df794a21c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876874"
---
# <a name="bitsadmin-util-and-getieproxy"></a>bitsadmin util 및 getieproxy

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정한 서비스 계정에 대 한 프록시 사용을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /Util /GetIEProxy <Account> [/Conn <ConnectionName>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|계정|서비스 계정을 검색 하려면 프록시 설정을 지정 합니다. 가능한 값은<br /><br />-LOCALSYSTEM<br />-NETWORKSERVICE<br />-LOCALSERVICE|
|연결 이름|옵션을 사용 합니다 **/conn** 모뎀 연결이 사용 하도록 지정 하려면 매개 변수입니다. 지정 하지 않으면 경우는 **/conn** 매개 변수, BITS LAN 연결을 사용 합니다. 바로 뒤에 모뎀 연결 이름 지정은 **/conn** 매개 변수입니다.|

## <a name="remarks"></a>설명

이 스위치는 각 프록시 사용에 대 한 값을 표시 뿐 아니라 프록시 사용에 대해 지정한 서비스 계정입니다. 서비스 계정에 대 한 프록시 사용 설정에 대 한 내용은 참조는 [bitsadmin util 및 setieproxy](bitsadmin-util-and-setieproxy.md) 전환 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 네트워크 서비스 계정에 대 한 프록시 사용을 표시합니다.

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
