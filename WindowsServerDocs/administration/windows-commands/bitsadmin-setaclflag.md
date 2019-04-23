---
title: bitsadmin setaclflag
description: Windows 명령 항목에 대 한 **bitsadmin setaclflag** -액세스 제어 목록 전파 플래그를 설정 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 89d825a4bc4512022fed98a3188537d3977fa3c3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867404"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

액세스 제어 작업에 대 한 목록 (ACL) 전파 플래그를 설정합니다. 플래그 다운로드할 파일의 소유자 및 ACL 정보를 유지 하려는 것을 나타냅니다. 예를 들어, 소유자 및 그룹 파일을 유지 하려면 설정 **플래그** 하려면 `OG`합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetAclFlags <Job> <Flags>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|Flags|다음 플래그 값 중 하나 이상 지정 합니다.</br>-   O: 파일 소유자 정보를 복사 합니다.</br>-   G: 파일 그룹 정보를 복사 합니다.</br>-   D: 파일과 함께 DACL 정보를 복사 합니다.</br>-S: 복사 SACL 파일을 사용 하 여 정보입니다.|

## <a name="remarks"></a>설명

SetAclFlags 스위치는 작업은 Windows (SMB) 공유에서 데이터를 다운로드 하는 경우 소유자 및 액세스 제어 목록 정보를 유지 하기 위해 사용 됩니다.

## <a name="BKMK_examples"></a>예제

다음 예제에서는 액세스 제어 목록 전파 플래그 이라는 작업에 대 한 *myDownloadJob* 다운로드 한 파일 소유자 및 그룹 정보를 유지 관리 합니다.
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)