---
ms.assetid: fb95c8ee-a418-4520-a12a-7754ae947c3c
title: Fsutil reparsepoint
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 940131a02a5cd3a6122022cf9b0dff3281d1dabf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847944"
---
# <a name="fsutil-reparsepoint"></a>Fsutil reparsepoint
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

쿼리 또는 삭제 재분석 지점.  **fsutil reparsepoint** 명령 지원 엔지니어가 일반적으로 사용 됩니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil reparsepoint [query] <FileName>
fsutil reparsepoint [delete] <FileName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|쿼리|연결 된 파일 또는 디렉터리를 지정 된 핸들에 의해 식별 된 재분석 지점 데이터를 검색 합니다.|
|삭제|재분석 지점 파일 또는 디렉터리를 지정 된 핸들에 의해 식별 하지만 파일 또는 디렉터리를 삭제 하지 않습니다 삭제 합니다.|
|<FileName>|파일 이름과 확장명을 예를 들어 C:\documents\filename.txt 포함 파일의 전체 경로 지정 합니다.|

## <a name="remarks"></a>설명

-   재분석 지점은 NTFS 파일 시스템 개체가 사용자 정의 데이터를 포함 하는 정의할 수 있는 특성을가지고 및 입/출력 (I/O) 하위 시스템의 기능을 확장 하는 데 사용 됩니다.

-   재분석 지점은 디렉터리 연결 지점과 볼륨 탑재 지점에 사용 됩니다. 특정 파일에 해당 드라이버에 특별 한 것으로 표시 하 여 파일 시스템 필터 드라이버 사용 되기도 합니다.

-   재분석 지점을 설정 하는 프로그램을 저장 하는 데이터를 고유 하 게 식별 하는 재분석 태그와 함께이 데이터를 저장 합니다. 파일 시스템 재분석 지점 파일을 열면, 연결 된 파일 시스템 필터를 찾으려고 시도 합니다. 파일 시스템 필터 있으면 필터 재분석 데이터에서 지시 된 대로 파일을 처리 합니다. 파일 시스템 필터가 발견 되는 파일 열기 작업이 실패 합니다.

## <a name="BKMK_examples"></a>예제
C:\Server 연관 된 재분석 지점 데이터를 검색 하려면 다음을 입력 합니다.

```
fsutil reparsepoint query c:\server
```

재분석 지점이 지정 된 파일 또는 디렉터리를 삭제 하려면 다음 형식을 사용 합니다.

```
fsutil reparsepoint delete c:\server
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


