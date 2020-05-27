---
title: sfc
description: 모든 보호 된 시스템 파일의 무결성을 검사 하 고 확인 하 고 잘못 된 버전을 올바른 버전으로 대체 하는 sfc에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c58c25da-e028-42a6-9e10-973484a4b953
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: af2167e1e23b0698c17159b1ae6b1970a06219d4
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821265"
---
# <a name="sfc"></a>sfc

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

검사 하 고 모든 보호 된 시스템의 무결성 파일을 올바른 버전으로 잘못 된 버전을 대체를 확인 합니다.


## <a name="syntax"></a>구문
```
sfc [/scannow] [/verifyonly] [/scanfile=<file>] [/verifyfile=<file>] [/offwindir=<offline windows directory> /offbootdir=<offline boot directory>]
```

#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/scannow|모든 보호 된 파일의 무결성을 검사 하 고 가능한 경우 문제를 사용 하 여 파일을 복구 합니다.|
|/verifyonly|모든 보호 된 파일의 무결성을 검사합니다. 복구 작업이 수행 됩니다.|
|/scanfile|지정된 된 파일의 무결성을 검사 하 고 가능한 경우 문제가 감지 되 면 파일을 복구 합니다.|
|\<파일>|지정 된 전체 경로 파일 이름|
|/verifyfile|지정 된 파일의 무결성을 확인 합니다. 복구 작업이 수행 됩니다.|
|/offwindir|오프 라인 복구에 대 한 오프 라인 windows 디렉터리의 위치를 지정합니다.|
|/offbootdir|오프 라인에 대 한 오프 라인 부팅 디렉터리의 위치 지정|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
-   실행 하려면 Administrators 그룹의 구성원으로 로그온 해야 **sfc.exe**합니다.
-   **sfc** 에서 보호 된 파일을 덮어쓴 경우 **systemroot\system32\dllcache** 폴더에서 올바른 버전의 파일을 검색 한 다음 잘못 된 파일을 대체 합니다.
-   Windows Server 2003, Windows Server 2008 및 Windows Server 2008 r 2에서 **sfc** 의 기능 차이가 있습니다.
-   Windows Server 2003의 **sfc** 에 대 한 자세한 내용은 Microsoft 기술 자료 [문서 310747](https://go.microsoft.com/fwlink/?LinkId=227069) 를 참조 하십시오.
-   Windows Server 2008 및 Windows Server 2008 r 2의 **sfc** 에 대 한 자세한 내용은 [시스템 파일 검사기](https://go.microsoft.com/fwlink/?LinkId=227071)를 참조 하세요.

## <a name="examples"></a>예
확인 하는 **kernel32.dll 파일**, 유형:
```
sfc /verifyfile=c:\windows\system32\kernel32.dll
```
설치의 오프 라인 복구 하는 **kernel32.dll** 로 설정 하는 오프 라인 부팅 디렉터리와 파일 **d:** 및로 설정 하는 오프 라인 windows 디렉터리 **d:\windows**, 유형:
```
sfc /scanfile=d:\windows\system32\kernel32.dll /offbootdir=d:\ /offwindir=d:\windows
```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)

