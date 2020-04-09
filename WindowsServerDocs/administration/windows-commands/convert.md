---
title: convert
description: 파일 할당 테이블 (FAT) 및 FAT32 볼륨을 NTFS 파일 시스템으로 변환 하 고 기존 파일 및 디렉터리를 그대로 유지 하는 변환에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 96e437c0-1aa3-46ab-9078-a7b8cdaf3792
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0fb2981d6cd5a54737700b64b28f7a8a52de72b1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847176"
---
# <a name="convert"></a>convert

변환 파일 할당 테이블 (FAT) 및 FAT32 볼륨을 NTFS 파일 시스템으로 기존 파일 및 디렉터리를 그대로입니다. NTFS 파일 시스템으로 변환 된 볼륨을 FAT 또는 FAT32 다시 변환할 수 없습니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
convert [<Volume>] /fs:ntfs [/v] [/cvtarea:<FileName>] [/nosecurity] [/x]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|볼륨 > \<|드라이브 문자 지정 합니다 (콜론), 탑재 지점 또는 볼륨 이름을 NTFS로 변환 합니다.|
|/fs: ntfs|필수입니다. 볼륨을 NTFS로 변환합니다.|
|/v|실행 **변환** 모든 메시지 변환 과정에서 표시 하는 자세한 정보 표시 모드에 있습니다.|
|/cvtarea:\<파일 이름 >|마스터 파일 테이블 (MFT) 및 기타 NTFS 메타 데이터 파일을 기존 인접 한 자리 표시자 파일 기록 됩니다 지정 합니다. 이 파일을 변환할 파일 시스템의 루트 디렉터리에 있어야 합니다. 사용은 **/cvtarea** 변환 후 매개 변수를 덜 조각난된 파일 시스템에 발생할 수 있습니다. 최상의 결과이 파일의 크기가 1KB 되어야 파일 시스템에서 파일 및 디렉터리의 수를 곱한 있지만 **변환** 유틸리티 모든 크기의 파일을 수락 합니다.</br>중요: **convert**를 실행 하기 전에 **fsutil file createnew** 명령을 사용 하 여 자리 표시자 파일을 만들어야 합니다. **변환** 를이 파일을 만들지 않습니다. **변환** NTFS 메타 데이터와이 파일을 덮어씁니다. 변환 후이 파일에 포함 된 사용 하지 않은 공간 해제 됩니다.|
|/nosecurity|변환 된 파일 및 디렉터리에 대 한 보안 설정을 모든 사용자가 액세스할 수 있도록 지정 합니다.|
|/x|변환 하기 전에 필요한 경우 볼륨을 분리 합니다. 볼륨에 대한 열린 핸들은 더 이상 유효하지 않습니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>주의

-   경우 **변환** 드라이브를 잠글 수 없습니다 (예를 들어 드라이브를 시스템 볼륨 또는 현재 드라이브) 드라이브를 변환 하는 컴퓨터를 다시 시작 하면 다음에 대 한 옵션이 제공 됩니다. 즉시 변환을 완료 하려면 컴퓨터를 다시 시작할 수 없으면 컴퓨터를 다시 시작 하 고 완료 하 여 변환 프로세스에 대 한 시간을 할애 하는 데 시간이 계획 합니다.
-   FAT 또는 FAT32에서 NTFS로 변환 된 볼륨의 경우:

    기존 디스크 사용으로 인해 MFT는 원래 NTFS로 포맷 된 볼륨의 경우와는 다른 위치에 만들어지므로 원래 NTFS로 포맷 된 볼륨의 볼륨 성능이 좋지 않을 수 있습니다. 최적의 성능을 위해 NTFS 파일 시스템으로 포맷 하 고 이러한 볼륨을 다시 만들고 것이 좋습니다.

    NTFS로 FAT 또는 FAT32 볼륨 변환 그대로 파일 유지 하지만 볼륨에는 처음에 NTFS로 포맷 한 볼륨에 비해 몇 가지 성능 이점이 없을 수 있습니다. 예를 들어 MFT 변환 된 볼륨에서 조각화 될 수 있습니다. 변환 된 부팅 볼륨에 또한 **변환** Windows 설치 시 적용 되는 동일한 기본 보안을 적용 합니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

드라이브 E에 있는 볼륨을 NTFS로 변환 하 고 변환 과정에서 모든 메시지를 표시 하려면 다음을 입력 합니다.
```
convert e: /fs:ntfs /v
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)