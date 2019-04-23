---
ms.assetid: faad34aa-4ba1-4129-bc1f-08088399e2fa
title: Fsutil usn
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 4bef63f4938b5ce786bbbfdbf3bdd2081280ce95
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829984"
---
# <a name="fsutil-usn"></a>Fsutil usn
>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

업데이트 시퀀스 번호 (USN) 변경 저널을 관리합니다.

## <a name="syntax"></a>구문

```
fsutil usn [createjournal] m=<MaxSize> a=<AllocationDelta> <VolumePath>
fsutil usn [deletejournal] {/D | /N} <volumepath>
fsutil usn [enablerangetracking] <volumepath> [options]
fsutil usn [enumdata] <FileRef> <LowUSN> <HighUSN> <VolumePath>
fsutil usn [queryjournal] <VolumePath>
fsutil usn [readdata] <FileName>
fsutil usn [readjournal] [c= <chunk-size> s=<file-size-threshold>] <volumepath>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------------|---------------|
|createjournal|USN 변경 저널을 만듭니다.|
|m=\<MaxSize>|NTFS 변경 저널에 할당 하는 바이트의 최대 크기를 지정 합니다.|
|a=\<AllocationDelta>|끝에 추가 되 고 변경 저널의 시작 부분에서 제거 된 메모리 할당의 크기를 지정 합니다.|
|\<VolumePath>|(콜론) 드라이브 문자를 지정 합니다.|
|deletejournal|삭제 하거나 활성 USN 변경 저널을 사용 하지 않도록 설정 합니다. **주의:** 변경 저널을 삭제에 영향을 복제 서비스 FRS (파일) 및 인덱싱 서비스에 볼륨의 전체 (및 시간이 오래 걸리는) 검사를 수행 하려면 이러한 서비스가 필요 합니다. FRS SYSVOL 복제 및 DFS 링크 대체 볼륨 다시 검색 되는 동안 간 복제에 차례로 부정적인 영향을 줍니다.|
|/d|활성 USN 변경 저널을 사용 하지 않도록 설정 하 고 변경 저널을 해제 하는 동안 입/출력 (I/O) 컨트롤을 반환 합니다.|
|/n|활성 USN 변경 저널을 사용 하지 않도록 설정 하 고 변경 저널 비활성화 된 후에 I/O 제어를 반환 합니다.|
|enablerangetracking|볼륨에 대 한 추적 USN 쓰기 범위를 사용 하도록 설정 합니다.|
|c=\<chunk-size>|볼륨을 추적 하기 위해 청크 크기를 지정 합니다.|
|s=\<file-size-threshold>|추적 하는 범위에 대 한 파일 크기 임계값을 지정 합니다.|
|enumdata|열거 하 고 지정 된 두 경계 사이의 변경 저널 항목을 나열 합니다.|
|\<FileRef>|열거형을 시작 하려면 볼륨에 있는 파일 내에서 서 수 위치를 지정 합니다.|
|\<LowUSN>|반환 되는 레코드를 필터링 하는 데 사용 하는 범위의 USN 값의 낮은 경계를 지정 합니다. 튜플이 마지막 변경 저널 USN 레코드만 크거나 사이 *LowUSN* 및 *HighUSN* 멤버 값이 반환 됩니다.|
|\<HighUSN>|반환 되는 파일을 필터링 하는 데 사용 되는 범위의 USN 값의 상한값을 지정 합니다.|
|queryjournal|현재 변경 저널, 해당 레코드 및 해당 용량에 대 한 정보를 수집 하는 볼륨의 USN 데이터를 쿼리 합니다.|
|readdata|파일에 대 한 USN 데이터를 읽습니다.|
|\<FileName>|예를 들어 파일 이름과 확장명을 포함 하는 파일에 전체 경로 지정 합니다. C:\documents\filename.txt|
|readjournal|USN 저널에서 USN 레코드를 읽습니다.|
|minver=\<number>|반환할 USN_RECORD의 최소 주 버전입니다. Default = 2.|
|maxver=\<number>|반환할 USN_RECORD의 최대 주 버전입니다. Default = 4.|
|startusn =\<USN 번호 >|USN 저널에서 읽기를 시작 하는 USN입니다. Default = 0.|


## <a name="remarks"></a>설명

-   USN 변경 저널에 대 한

    USN 변경 저널의 볼륨에 파일에 대 한 모든 변경 내용 영구적 로그를 제공 합니다. 파일, 디렉터리 및 기타 NTFS 개체는 추가, 삭제 및 수정, NTFS USN 변경 저널 컴퓨터의 각 볼륨 마다 하나씩 레코드 입력 합니다. 각 기록은 변경 유형 및 변경된 개체를 나타냅니다. 새 레코드 스트림의 끝에 추가 됩니다.

    프로그램을 모든 수정 된 파일 집합을 확인 하려면 USN 변경 저널을 참조 하세요. USN 변경 저널 타임 스탬프를 확인 하거나 파일 알림에 등록 보다 훨씬 더 효율적입니다. USN 변경 저널 사용 하도록 설정 되어 인덱싱 서비스, 복제 서비스 FRS (파일), 원격 설치 서비스 (RIS) 및 원격 저장소에서 사용 됩니다.

-   사용 하 여 **createjournal**

    변경 저널 볼륨에 이미 있는 경우는 **createjournal** 변경 저널을 업데이트 하는 매개 변수 *MaxSize* 및 *AllocationDelta* 매개 변수입니다. 그러면 활성 저널 불가능 하 게 하지 않고 관리 하는 레코드 수를 확장할 수 있습니다.

-   사용 하 여 **m**

    변경 저널을이 대상 값 보다 큰 증가할 수 있지만 변경 저널이이 값 보다 작은 값을 다음 NTFS 검사점에서 잘립니다. NTFS 변경 저널을 검사 하 고 크기의 값을 초과할 때 트림 *MaxSize* 값을 더한 값 *AllocationDelta*합니다. NTFS 검사점에 운영 체제 오류에서 복구 하는 데 필요한 처리를 결정 하는 NTFS를 사용 하도록 설정 하는 NTFS 로그 파일에 레코드를 기록 합니다.

-   사용 하 여 **는**

    변경 저널의 값의 합계 보다 더 커질 수 있는 *MaxSize* 및 *AllocationDelta* 삭제하기 전에 합니다.

-   사용 하 여 **deletejournal**

    삭제 하거나 활성 변경 저널을 사용 하지 않도록 설정 되므로 시간이 많이 시스템 마스터 파일 테이블 (MFT)에서 모든 레코드에 액세스 하 고 마지막 USN 특성을 0 (영)으로 설정 해야 합니다. 이 프로세스는 몇 분 정도 걸릴 수 하 고 다시 시작이 필요한 경우 시스템을 다시 시작한 후 계속할 수 있습니다. 이 과정에서 변경 저널 활성으로 간주 되지 않습니다도 그 사용 하지 않으면. 시스템 업무 일지를 비활성화 하는 동안 액세스할 수 없으며, 및 모든 저널 작업 오류를 반환 합니다. 주의 기울여야 극단적인 활성 저널을 사용 하지 않도록 설정 하는 경우 부정적인 영향을 주므로 저널을 사용 하는 다른 응용 프로그램입니다.

## <a name="BKMK_examples"></a>예제
USN 변경 유형 C 드라이브에 저널을 만들려면:

```
fsutil usn createjournal m=1000 a=100 c:
```

활성 삭제 USN에 변경 저널을 C 드라이브 유형:

```
fsutil usn deletejournal /d c:
```

범위 지정 된 청크 크기 및 파일 크기 임계값을 사용 하 여 추적을 사용 하도록 설정 하려면 다음을 입력 합니다.

```
fsutil usn enablerangetracking c=16384 s=67108864 C:
```

열거 하 고 C 드라이브에 지정 된 두 경계 사이의 변경 저널 항목을 나열 하려면 다음을 입력 합니다.

```
fsutil usn enumdata 1 0 1 c:
```

C 드라이브의 볼륨에 대 한 USN 데이터를 쿼리하려면 다음을 입력 합니다.

```
fsutil usn queryjournal c:
```

C 드라이브에 \Temp 폴더의 파일에 대 한 USN 데이터를 읽으려면 다음을 입력 합니다.

```
fsutil usn readdata c:\temp\sample.txt
```

특정 시작 USN 사용 하 여 USN 저널을 읽으려면 다음을 입력 합니다.

```
fsutil usn readjournal startusn=0xF00
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

