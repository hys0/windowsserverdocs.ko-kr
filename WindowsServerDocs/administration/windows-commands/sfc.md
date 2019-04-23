---
title: sfc
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1db0ab81c9469c88ddb64a367a9dc98a1fd9b70c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832394"
---
# <a name="sfc"></a>sfc

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

검사 하 고 모든 보호 된 시스템의 무결성 파일을 올바른 버전으로 잘못 된 버전을 대체를 확인 합니다.
이 명령을 사용 하는 방법의 예제를 참조 하세요 [예제](#BKMK_examples)합니다.

## <a name="syntax"></a>구문
```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/scannow|모든 보호 된 파일의 무결성을 검사 하 고 가능한 경우 문제를 사용 하 여 파일을 복구 합니다.|
|/verifyonly|모든 보호 된 파일의 무결성을 검사합니다. 복구 작업이 수행 됩니다.|
|/scanfile|지정된 된 파일의 무결성을 검사 하 고 가능한 경우 문제가 감지 되 면 파일을 복구 합니다.|
|\<file>|지정 된 전체 경로 파일 이름|
|/verifyfile|지정된 된 파일의 무결성을 확인합니다. 복구 작업이 수행 됩니다.|
|/offwindir|오프 라인 복구에 대 한 오프 라인 windows 디렉터리의 위치를 지정합니다.|
|/offbootdir|오프 라인에 대 한 오프 라인 부팅 디렉터리의 위치 지정|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   실행 하려면 Administrators 그룹의 구성원으로 로그온 해야 **sfc.exe**합니다.
-   하는 경우 **sfc** 보호 된 파일을 덮어를 올바른 버전에서 파일의 검색은 검색 된 **systemroot\system32\dllcache** 폴더를 잘못 된 파일을 다음으로 바꿉니다.
-   간의 기능 차이가 **sfc** Windows Server 2003, Windows Server 2008 및 Windows Server 2008 R2에서:
-   에 대 한 자세한 내용은 **sfc** Windows Server 2003에서 참조 [310747](https://go.microsoft.com/fwlink/?LinkId=227069) Microsoft 기술 자료에서 합니다.
-   에 대 한 자세한 내용은 **sfc** Windows Server 2008 및 Windows Server 2008 R2에서는 참조 [System File Checker](https://go.microsoft.com/fwlink/?LinkId=227071)합니다.

## <a name="BKMK_examples"></a>예제
확인 하는 **kernel32.dll 파일**, 유형:
```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```
설치의 오프 라인 복구 하는 **kernel32.dll** 로 설정 하는 오프 라인 부팅 디렉터리와 파일 **d:** 및로 설정 하는 오프 라인 windows 디렉터리 **d:\windows**, 유형:
```
sfc /scanfile=d:\windows\system32\kernel32.dll /offbootdir=d:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)

