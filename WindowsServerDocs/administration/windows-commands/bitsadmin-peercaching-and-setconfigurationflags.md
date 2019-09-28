---
title: bitsadmin 피어 캐싱 및 setconfigurationflags
description: '**Bitsadmin 피어 캐싱 및 setconfigurationflags** 에 대 한 Windows 명령 항목-컴퓨터가 피어에 콘텐츠를 제공할 수 있고 피어에서 콘텐츠를 다운로드할 수 있는지 여부를 결정 하는 구성 플래그를 설정 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a65d54bcaa2bce26eb2b7c98250837ab09c7a423
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381107"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin 피어 캐싱 및 setconfigurationflags



컴퓨터 피어 컴퓨터에 콘텐츠를 사용할 수 및 피어에서 콘텐츠를 다운로드 하는 경우 결정 하는 구성 플래그를 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /PeerCaching /SetConfigurationFlags <Job> <Value>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|값|값이 이진 표현에서 비트에 대 한 다음 해석 가진 부호 없는 정수:</br>-피어에서 작업 데이터를 다운로드할 수 있도록 허용: 최하위 비트를 설정 합니다.</br>-작업의 데이터를 동료에 게 제공할 수 있습니다. 오른쪽에서 두 번째 비트를 설정 합니다.|

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 피어 로부터 다운로드 작업의 데이터를 지정 *myJob*합니다.
```
C:\> Bitsadmin /PeerCaching /SetConfigurationFlags myJob 1
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)