---
title: bitsadmin util 및 getieproxy
description: '**Bitsadmin util 및 getieproxy** 에 대 한 Windows 명령 항목-지정 된 서비스 계정에 대 한 프록시 사용을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6936e088ddcf467b5a8f931bc8217ba9da4662c2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380275"
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
|연결 이름|사용할 모뎀 연결을 지정 하기 위해 **/Conn** 매개 변수와 함께 사용 되는 옵션입니다. **/Conn** 매개 변수를 지정 하지 않으면 BITS는 LAN 연결을 사용 합니다. 바로 뒤에 모뎀 연결 이름 지정은 **/conn** 매개 변수입니다.|

## <a name="remarks"></a>설명

이 스위치는 서비스 계정에 대해 지정한 프록시 사용 뿐만 아니라 각 프록시 사용에 대 한 값을 표시 합니다. 서비스 계정에 대 한 프록시 사용을 설정 하는 방법에 대 한 자세한 내용은 [bitsadmin util 및 setieproxy](bitsadmin-util-and-setieproxy.md) 스위치를 참조 하세요.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 네트워크 서비스 계정에 대 한 프록시 사용을 표시합니다.

```
C:\>bitsadmin /Util /GetIEProxy NETWORKSERVICE
```

## <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)
