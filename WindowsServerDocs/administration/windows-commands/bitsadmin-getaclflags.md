---
title: bitsadmin getaclflags
description: Windows 명령 항목에 대 한 **bitsadmin getaclflags** -액세스 제어 목록 전파 플래그를 검색 합니다.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 185445a97168344f910abc0e644718296de2c712
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861454"
---
# <a name="bitsadmin-getaclflags"></a>bitsadmin getaclflags

액세스 제어 목록 (ACL) 전파 플래그를 검색합니다.

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
-   /O: 파일 소유자 정보를 복사 합니다.
-   G: 파일 그룹 정보를 복사 합니다.
-   D: 파일과 함께 DACL 정보를 복사 합니다.
-   S: 파일을 사용 하 여 SACL 정보를 복사 합니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 명명 된 작업에 대 한 액세스 제어 목록 전파 플래그 *myDownloadJob*합니다.
```
C:\>bitsadmin /getaclflags myDownloadJob
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)