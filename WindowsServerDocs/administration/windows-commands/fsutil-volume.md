---
ms.assetid: 0397c204-b3f8-4fd8-b71d-b7efb117766d
title: Fsutil 볼륨
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: c4496cfec94823ae177bc6de4fac83dc977fb61d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376701"
---
# <a name="fsutil-volume"></a>Fsutil 볼륨
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

볼륨을 분리 하거나 쿼리를 하드 디스크 드라이브 여유 공간을 하드 디스크 드라이브에서 현재 사용할 수 또는 파일에는 특정 클러스터를 사용 하는 경우를 확인 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
fsutil volume [allocationreport] <VolumePath>
fsutil volume [diskfree] <VolumePath>
fsutil volume [dismount] <VolumePath>
fsutil volume [filelayout] <VolumePath> <fileid>
fsutil volume [list]
fsutil volume [querycluster] <VolumePath> <Cluster> [<Cluster>] … …
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|allocationreport|지정 된 볼륨에서 저장소를 사용 하는 방법에 대 한 정보를 표시 합니다.|
|@no__t 0VolumePath >|드라이브 문자를 지정 하 고 그 뒤에 콜론을 지정 합니다.|
|diskfree|하드 디스크 드라이브에 사용 가능한 공간의 크기를 확인 하려면을 쿼리 합니다.|
|분리|볼륨을 분리합니다.|
|filelayout|지정 된 파일에 대 한 NTFS 메타 데이터를 표시 합니다.|
|\<fileid >|파일 id를 지정 합니다.|
|list|시스템의 모든 볼륨을 나열 합니다.|
|querycluster|파일은 지정된 된 클러스터를 사용 하 여 찾습니다. 여러 클러스터를 지정할 수는 **querycluster** 매개 변수입니다.<br /><br />이 매개 변수는 다음에 적용 됩니다.  Windows Server 2008 R2 및 Windows 7|
|\<cluster >|LCN (logical cluster number)을 지정 합니다.|

## <a name="BKMK_examples"></a>예와
할당 된 클러스터 보고서를 표시 하려면 다음을 입력 합니다.

```
fsutil volume allocationreport C:
```

C 드라이브에 볼륨을 탑재 하려면 다음을 입력 합니다.

```
fsutil volume dismount c:
```

C 드라이브에 볼륨의 사용 가능한 공간의 크기를 쿼리하려면 다음을 입력 합니다.

```
fsutil volume diskfree c:
```

지정 된 파일에 대 한 모든 정보를 표시 하려면 다음을 입력 합니다.

```
fsutil volume C: *
fsutil volume C:\Windows
fsutil volume C: 0x00040000000001bf
```

디스크의 볼륨을 나열 하려면 다음을 입력 합니다.

```
fsutil volume list
```

클러스터를 사용 하는 파일을 찾으려면 C 드라이브에서 논리 클러스터 번호 50 및 0x2000에 의해 지정 된 다음을 입력 합니다.

```
fsutil volume querycluster C: 50 0x2000
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[NTFS 작동 방법](https://go.microsoft.com/fwlink/?LinkId=183396)


