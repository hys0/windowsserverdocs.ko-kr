---
title: bitsadmin setaclflag
description: '**Bitsadmin setaclflag** 의 Windows 명령 항목-액세스 제어 목록 전파 플래그를 설정 합니다.'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fbdb12c29af7b4db8b25846d43ee1c93b2454ff2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380761"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

작업에 대 한 ACL (액세스 제어 목록) 전파 플래그를 설정 합니다. 플래그는 다운로드 하는 파일을 사용 하 여 소유자 및 ACL 정보를 유지 관리 하려는 경우를 의미 합니다. 예를 들어 파일을 사용 하 여 소유자와 그룹을 유지 하려면 **플래그** 를 `OG` 설정 합니다.

## <a name="syntax"></a>구문

```
bitsadmin /SetAclFlags <Job> <Flags>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|작업|작업의 표시 이름 또는 GUID|
|플래그|다음 플래그 값 중 하나 이상 지정 합니다.</br>-O: 파일 소유자 정보를 복사 합니다.</br>-G: 파일 그룹 정보를 복사 합니다.</br>-D: 복사할 파일을 사용 하 여 DACL 정보입니다.</br>-S: 복사 SACL 파일을 사용 하 여 정보입니다.|

## <a name="remarks"></a>설명

SetAclFlags 스위치는 작업이 Windows (SMB) 공유에서 데이터를 다운로드 하는 경우 소유자 및 액세스 제어 목록 정보를 유지 관리 하는 데 사용 됩니다.

## <a name="BKMK_examples"></a>예와

다음 예제에서는 액세스 제어 목록 전파 플래그 이라는 작업에 대 한 *myDownloadJob* 다운로드 한 파일 소유자 및 그룹 정보를 유지 관리 합니다.
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)