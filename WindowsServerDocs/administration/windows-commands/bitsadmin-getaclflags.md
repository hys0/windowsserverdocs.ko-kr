---
title: bitsadmin getaclflags
description: '**Bitsadmin getaclflags** 에 대 한 Windows 명령 항목-액세스 제어 목록 전파 플래그를 검색 합니다.'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99266def-7479-4430-a61c-98ec433fa88b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad98cd742161ae06be5cba7acde7b810eaf199d6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381793"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

ACL (액세스 제어 목록) 전파 플래그를 검색 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /GetAclFlags <Job>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|

## <a name="remarks"></a>설명

다음 플래그 값 중 하나 이상을 표시합니다.
-   I/O 파일을 사용 하 여 소유자 정보를 복사 합니다.
-   EXPRESS-G 파일을 사용 하 여 그룹 정보를 복사 합니다.
-   D: 파일을 사용 하 여 DACL 정보를 복사 합니다.
-   삭제 파일을 사용 하 여 SACL 정보를 복사 합니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 명명 된 작업에 대 한 액세스 제어 목록 전파 플래그 *myDownloadJob*합니다.
```
C:\>bitsadmin /getaclflags myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)