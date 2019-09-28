---
title: bitsadmin getproxybypasslist
description: '**Bitsadmin getproxybypasslist** 에 대 한 Windows 명령 항목-지정 된 작업에 대 한 프록시 무시 목록을 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 50959be3-7014-4bc9-9a7b-68f1ff94a94a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87cc131402707eac40329750e98218ec52083b94
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381420"
---
# <a name="bitsadmin-getproxybypasslist"></a>bitsadmin getproxybypasslist

지정된 된 작업에 대 한 프록시 무시 목록을 검색합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetProxyBypassList <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

바이패스 목록에는 호스트 이름 또는 IP 주소 또는 둘 다 포함 한 프록시를 통과 하지 않을 하 합니다. 이 목록에는 동일한 LAN에 있는 모든 서버를 참조 하는 "\<local >"이 포함 될 수 있습니다. 목록 세미콜론 이나 공백으로 구분 된.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 프록시 무시 목록 검색 *myDownloadJob*합니다.
```
C:\>bitsadmin /GetProxyBypassList myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)