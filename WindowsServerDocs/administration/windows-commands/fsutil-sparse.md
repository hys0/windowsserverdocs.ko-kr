---
ms.assetid: 77545920-2d13-4f35-a4d1-14dbec8340dc
title: Fsutil 스파스
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 76a263c82ebc42de4cc6d136f9a814c3a678666b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878394"
---
# <a name="fsutil-sparse"></a>Fsutil 스파스
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

스파스 파일을 관리 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil sparse [queryflag] <FileName>
fsutil sparse [queryrange] <FileName>
fsutil sparse [setflag] <FileName>
fsutil sparse [setrange] <FileName> <BeginningOffset> <Length>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|queryflag|스파스를 쿼리 합니다.|
|queryrange|파일을 검색 하 고 0이 아닌 데이터를 포함할 수 있는 범위를 검색 합니다.|
|setflag|스파스로 표시 된 파일을 표시합니다.|
|setrange|파일의 지정된 된 범위를 0으로 채웁니다.|
|<FileName>|파일 이름과 확장명을 예를 들어 C:\documents\filename.txt 포함 파일의 전체 경로 지정 합니다.|
|<BeginningOffset>|스파스로 표시할 파일 내의 오프셋을 지정 합니다.|
|<Length>|파일을 바이트 단위로 스파스로 표시 영역의 길이 지정 합니다.|

## <a name="remarks"></a>설명

-   스파스 파일은 하나 이상의 영역에 할당 되지 않은 데이터를 포함 하는 파일입니다. 프로그램 0 값을 포함 하 여 바이트를 포함 하는 것이 할당 되지 않은 지역이 표시 됩니다. 그러나 디스크 공간이 없으면이 0을 나타내는 데 사용 됩니다. 모든 의미 있는 또는 0이 아닌 데이터는 할당 되지만 모든 nonmeaningful 데이터 (0으로 구성 된 데이터의 큰 문자열) 할당 되지 않습니다. 스파스 파일을 읽을 때 할당 된 데이터는 저장 시에 반환 되 고 할당 되지 않은 데이터가 반환 기본적으로 c2 보안 요구 사항에 따라 0으로. 할당을 취소할 수에서 아무 곳 이나 파일에서 데이터를 허용 하는 스파스 파일을 지원 합니다.

-   스파스 파일에서 큰 범위의 0 디스크 할당이 필요 하지 않을 수 있습니다. 파일을 작성 하는 경우 필요에 따라 0이 아닌 데이터에 대 한 공간 할당 됩니다.

-   만 스파스 또는 압축 된 파일 수는 0으로 설정 운영 체제에 알려진 범위.

-   파일이 스파스 또는 압축 된 경우 NTFS는 파일 내에서 디스크 공간 할당을 취소 될 수 있습니다. 이 바이트 범위 파일 크기를 확장 하지 않고 0으로 설정 합니다.

## <a name="BKMK_examples"></a>예제
스파스 C:\Temp 디렉터리에 Sample.txt 라는 파일을 표시 하려면 다음을 입력 합니다.

```
fsutil sparse setflag c:\temp\sample.txt 
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


