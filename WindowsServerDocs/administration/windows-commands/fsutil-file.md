---
ms.assetid: 9f3dc104-dd69-4b03-b824-a29896780164
title: Fsutil 파일
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 2b89d96535512f79c83c601be50327c24dc40787
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376984"
---
# <a name="fsutil-file"></a>Fsutil 파일
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

사용자 이름 (디스크 할당량을 사용 하도록 설정 된 경우)을 사용 하 여 파일을 찾고, 파일의 짧은 이름을 설정 하 고, 파일의 유효한 데이터 길이를 설정 하거나, 파일의 데이터를 0으로 설정 하거나, 새 파일을 만듭니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil file [createnew] <filename> <length>
fsutil file [findbysid] <username> <directory>
fsutil file [optimizemetadata] [/A] <filename>
fsutil file [queryallocranges] offset=<offset> length=<length> <filename>
fsutil file [queryextents] [/R] <filename> [<startingvcn> [<numvcns>]]
fsutil file [queryfileid] <filename>
fsutil file [queryfilenamebyid] <volume> <fileid>
fsutil file [queryoptimizemetadata] <filename>
fsutil file [queryvaliddata] [/R] [/D] <filename>
fsutil file [seteof] <filename> <length>
fsutil file [setshortname] <filename> <shortname>
fsutil file [setvaliddata] <filename> <datalength>
fsutil file [setzerodata] offset=<offset> length=<length> <filename>

```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|createnew|0으로 구성 하는 내용이 있는 지정 된 이름과 크기의 파일을 만듭니다.|
|\< 파일 이름 >|파일 이름 및 확장명을 포함 하는 파일의 전체 경로를 지정 합니다 (예: C:\documents\filename.txt.).|
|\<length >|파일의 유효한 데이터 길이 지정합니다.|
|findbysid|디스크 할당량을 사용 하도록 설정 된 NTFS 볼륨에 지정된 된 사용자에 속하는 파일을 찾습니다.|
|\< 사용자 이름 >|사용자의 사용자 이름이 나 로그온 이름을 지정합니다.|
|\<directory>|디렉터리의 전체 경로를 지정 합니다 (예: C:\users.).|
|optimizemetadata|이렇게 하면 지정 된 파일에 대 한 메타 데이터의 즉시 압축이 수행 됩니다.|
|/ A|최적화 전후에 파일 메타 데이터를 분석 합니다.|
|queryallocranges|NTFS 볼륨에 있는 파일에 할당 된 범위를 쿼리합니다. 파일을 스파스 영역에 있는지 여부를 결정 하는 데 유용 합니다.|
|offset = \<offset >|0으로 설정 해야 하는 범위의 시작을 지정 합니다.|
|길이 = \<length >|범위의 길이 (바이트)를 지정 합니다.|
|queryextents|파일에 대 한 익스텐트를 쿼리 합니다.|
|/R|@No__t-0이 재분석 지점인 경우 대상 대신 엽니다.|
|@no__t 0startingvcn >|쿼리할 첫 번째 VCN을 지정 합니다. 생략 하면 VCN 0에서 시작 합니다.|
|\<numvcns >|쿼리할 VCNs의 수입니다. 생략 하거나 0 인 경우 EOF까지 쿼리 합니다.|
|queryfileid|NTFS 볼륨에 있는 파일의 파일 ID를 쿼리합니다.<br /><br />이 매개 변수는 다음에 적용 됩니다.  Windows Server 2008 R2 및 Windows 7|
|\<volume >|드라이브 이름 뒤에 콜론으로 볼륨을 지정 합니다.|
|queryfilenamebyid|NTFS 볼륨에 지정 된 파일 ID에 대 한 임의 링크 이름을 표시합니다. 파일을 해당 파일을 가리키는 둘 이상의 링크 이름 수 없으므로 파일 링크를 사용 하는 파일 이름에 대 한 쿼리의 결과로 제공 될 보장 되지 않습니다.<br /><br />이 매개 변수는 다음에 적용 됩니다.  Windows Server 2008 R2 및 Windows 7|
|\<fileid >|NTFS 볼륨에 파일의 ID를 지정합니다.|
|queryoptimizemetadata|파일의 메타 데이터 상태를 쿼리 합니다.|
|queryvaliddata|파일의 유효한 데이터 길이를 쿼리 합니다.|
|/D|자세한 유효한 데이터 정보를 표시 합니다.|
|seteof|지정 된 파일의 EOF를 설정 합니다.|
|setshortname|NTFS 볼륨의 파일에 대 한 짧은 이름 (8.3 문자 길이 파일 이름)을 설정 합니다.|
|@no__t 0shortname >|파일의 짧은 이름을 지정합니다.|
|setvaliddata|NTFS 볼륨에 파일에 대 한 유효한 데이터 길이 가져오거나 설정 합니다.|
|@no__t 0datalength >|파일의 길이 바이트 단위로 지정 합니다.|
|setzerodata|파일의 범위 ( *오프셋* 및 *길이로*지정)를 0으로 설정 하 여 파일을 비웁니다. 스파스 파일의 파일을 사용 하는 경우 원본 할당 단위는 취소 됩니다.|

## <a name="remarks"></a>설명

-   NTFS에는 파일 길이에 대 한 두 가지 중요 한 개념인 EOF (파일 끝) 표식과 올바른 데이터 길이 (VDL)가 있습니다. EOF 파일의 실제 길이 나타냅니다. VDL은 디스크에 유효한 데이터의 길이 식별합니다. VDL과 EOF 사이의 모든 읽기는 자동으로 다시 사용 요구 사항을 C2 개체를 보존 하려면 0을 반환 합니다.

-   **Setvaliddata** 매개 변수는 SeManageVolumePrivilege (볼륨 유지 관리 작업 수행) 권한이 필요 하기 때문에 관리자만 사용할 수 있습니다. 이 기능에만 필요 고급 멀티미디어 및 시스템 영역 네트워크 시나리오입니다. **setvaliddata** 매개 변수는 현재 파일 크기 보다 적은 현재 VDL 보다 큰 양수 값 이어야 합니다.

    프로그램을 VDL를 설정 하는 데 유용 때:

    -   원시 클러스터 하드웨어 채널을 통해 디스크에 직접 쓰는 중입니다. 이렇게 하면이 범위에 사용자에 게 반환 될 수 있는 유효한 데이터가 파일 시스템에 알리기 위해 프로그램입니다.

    -   성능에 문제가 있을 때 파일 크기를 최소화 합니다. 이 파일을 만들거나 확장할 때 파일을 0으로 채우는 데 걸리는 시간을 방지 합니다.

## <a name="BKMK_examples"></a>예와
C 드라이브에 scottb 라는 사용자가 소유 하는 파일을 찾으려면 다음을 입력 합니다.

```
fsutil file findbysid scottb c:\users  
```

NTFS 볼륨에 있는 파일에 할당 된 범위를 쿼리하려면 다음을 입력 합니다.

```
fsutil file queryallocranges offset=1024 length=64 c:\temp\sample.txt  
```

파일에 대 한 메타 데이터를 최적화 하려면 다음을 입력 합니다.

```
fsutil file optimizemetadata C:\largefragmentedfile.txt
```

파일에 대 한 익스텐트를 쿼리하려면 다음을 입력 합니다.

```
fsutil file queryextents C:\Temp\sample.txt
```

파일의 EOF를 설정 하려면 다음을 입력 합니다.

```
fsutil file seteof C:\testfile.txt 1000
```

Longfile.txt C 드라이브에 Longfilename.txt 파일에 대 한 짧은 이름을 설정 하려면 다음을 입력 합니다.

```
fsutil file setshortname c:\longfilename.txt longfile.txt  
```

NTFS 볼륨에 Testfile.txt 라는 파일에 대 한 4, 096 바이트를 유효한 데이터 길이 설정 하려면 다음을 입력 합니다.

```
fsutil file setvaliddata c:\testfile.txt 4096  
```

NTFS 볼륨에 파일의 범위 비우기에 0을 설정 하려면 다음을 입력 합니다.

```
fsutil file setzerodata offset=100 length=150 c:\temp\sample.txt  
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


