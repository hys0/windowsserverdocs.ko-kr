---
ms.assetid: 7787a72e-a26b-415f-b700-a32806803478
title: Fsutil fsinfo
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b7af3859cd16b89587a86e3436d5c832620c4e22
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82725491"
---
# <a name="fsutil-fsinfo"></a>Fsutil fsinfo
> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

모든 드라이브를 나열 하 고, 드라이브 종류 쿼리, 볼륨 정보 쿼리, NTFS 특정 볼륨 정보 쿼리 또는 파일 시스템 통계를 쿼리 합니다.



## <a name="syntax"></a>구문

```
fsutil fsinfo [drives]
fsutil fsinfo [drivetype] <VolumePath>
fsutil fsinfo [ntfsinfo] <RootPath>
fsutil fsinfo [statistics] <VolumePath>
fsutil fsinfo [volumeinfo] <RootPath>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|드라이브|컴퓨터에 있는 모든 드라이브를 나열합니다.|
|drivetype|드라이브를 쿼리하고 해당 유형 (예: CD-ROM 드라이브)을 나열 합니다.|
|ntfsinfo|섹터, 전체 클러스터, 가능한 클러스터 시작 및 끝 MFT 영역의 수와 같은 지정된 된 볼륨에 대 한 NTFS 관련 볼륨 정보를 나열합니다.|
|sectorinfo|하드웨어의 섹터 크기 및 맞춤에 대 한 정보를 나열 합니다.|
|통계|파일 메타 데이터, 로그 파일 및 MFT 읽기 및 쓰기와 같은 지정된 된 볼륨에 대 한 시스템 통계입니다.|
|volumeinfo|지정 된 볼륨에 대 한 정보 (예: 파일 시스템, 볼륨에서 대/소문자를 구분 하는 파일 이름, 파일 이름의 유니코드, 디스크 할당량 또는 DirectAccess (DAX) 볼륨)를 지원 하는지 여부를 나열 합니다.|
|"VolumePath" < >|드라이브 문자를 지정 하 고 그 뒤에 콜론을 지정 합니다.|
|"RootPathname" < >|루트 드라이브의 드라이브 문자 (콜론)를 지정 합니다.|

## <a name="examples"></a><a name="BKMK_examples"></a>예와
모든 컴퓨터에서 드라이브를 나열 하려면 다음을 입력 합니다.

```
fsutil fsinfo drives
```

출력이 다음이 표시 됩니다.

```
Drives: A:\ C:\ D:\ E:\       
```

C 드라이브의 드라이브 종류를 쿼리하려면 다음을 입력 합니다.

```
fsutil fsinfo drivetype c:
```

쿼리 가능한 결과 다음과 같습니다.

```
Unknown Drive
No such Root Directory
Removable Drive, for example floppy
Fixed Drive
Remote/Network Drive
CD-ROM Drive
Ram Disk
```

볼륨 E에 대 한 볼륨 정보를 쿼리하려면 다음을 입력 합니다.

```
fsinfo volumeinfo e:\
```

출력이 다음이 표시 됩니다.

```
Volume Name :Volume
Serial Number : 0xd0b634d9
Max Component Length : 255
File System Name : NTFS
.
.
.
Supports Named Streams
Is DAX Volume
```

F 드라이브에서 NTFS 관련 볼륨 정보를 쿼리하려면 다음을 입력 합니다.

```
fsutil fsinfo ntfsinfo f:
```

출력이 다음이 표시 됩니다.

```
NTFS Volume Serial Number : 0xe660d46a60d442cb
Number Sectors :            0x00000000010ea04f
Total Clusters :            0x000000000021d409
.
.
.
Mft Zone End   :            0x0000000000004700       
```

파일 시스템의 기본 하드웨어 섹터 정보를 쿼리하려면 다음을 입력 합니다.

```
fsinfo sectorinfo d:
```

출력이 다음이 표시 됩니다.

```
D:\>fsutil fsinfo sectorinfo d:
LogicalBytesPerSector :                                 4096
PhysicalBytesPerSectorForAtomicity :                    4096
.
.
.
Trim Not Supported
DAX capable
```

드라이브 E에 대 한 파일 시스템 통계를 쿼리하려면 다음을 입력 합니다.

```
fsinfo statistics e:
```

출력이 다음이 표시 됩니다.

```
File System Type :     NTFS
Version :              1
UserFileReads :        75021
UserFileReadBytes :    1305244512
.
.
.
LogFileWriteBytes :    180936704       
```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
[Fsutil](Fsutil.md)


