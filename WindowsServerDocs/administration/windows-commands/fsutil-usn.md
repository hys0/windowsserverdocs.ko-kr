---
title: fsutil usn
description: USN (업데이트 시퀀스 번호) 변경 저널을 관리 하는 fsutil usn 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
ms.assetid: faad34aa-4ba1-4129-bc1f-08088399e2fa
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: b3f71588c7221f0ba8e3659d9a1a1dd133971ce9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930473"
---
# <a name="fsutil-usn"></a>fsutil usn

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8

USN (업데이트 시퀀스 번호) 변경 저널을 관리 합니다. USN 변경 저널의 볼륨에 파일에 대 한 모든 변경 내용 영구적 로그를 제공 합니다. 파일, 디렉터리 및 기타 NTFS 개체는 추가, 삭제 및 수정, NTFS USN 변경 저널 컴퓨터의 각 볼륨 마다 하나씩 레코드 입력 합니다. 각 기록은 변경 유형 및 변경된 개체를 나타냅니다. 새 레코드 스트림의 끝에 추가 됩니다.

## <a name="syntax"></a>구문

```
fsutil usn [createjournal] m=<maxsize> a=<allocationdelta> <volumepath>
fsutil usn [deletejournal] {/d | /n} <volumepath>
fsutil usn [enablerangetracking] <volumepath> [options]
fsutil usn [enumdata] <fileref> <lowUSN> <highUSN> <volumepath>
fsutil usn [queryjournal] <volumepath>
fsutil usn [readdata] <filename>
fsutil usn [readjournal] [c= <chunk-size> s=<file-size-threshold>] <volumepath>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| createjournal | USN 변경 저널을 만듭니다. |
| m =`<maxsize>` | NTFS 변경 저널에 할당 하는 바이트의 최대 크기를 지정 합니다. |
| a =`<allocationdelta>` | 끝에 추가 되 고 변경 저널의 시작 부분에서 제거 된 메모리 할당의 크기를 지정 합니다. |
| `<volumepath>` | 드라이브 문자를 지정 하 고 그 뒤에 콜론을 지정 합니다. |
| deletejournal | 삭제 하거나 활성 USN 변경 저널을 사용 하지 않도록 설정 합니다.<p>**주의:** 변경 저널을 삭제 하면 FRS (파일 복제 서비스) 및 인덱싱 서비스에 영향을 줍니다 .이 서비스를 사용 하려면 이러한 서비스에서 볼륨의 전체 및 시간이 많이 사용 되는 검색을 수행 해야 하기 때문입니다. FRS SYSVOL 복제 및 DFS 링크 대체 볼륨 다시 검색 되는 동안 간 복제에 차례로 부정적인 영향을 줍니다. |
| /d | 활성 USN 변경 저널을 사용 하지 않도록 설정 하 고, 변경 저널을 사용 하지 않도록 설정 하는 동안 입/출력 (i/o) 제어를 반환 합니다. |
| /n | 활성 USN 변경 저널을 사용 하지 않도록 설정 하 고 변경 저널을 사용 하지 않도록 설정한 후에만 i/o 제어를 반환 합니다. |
| enablerangetracking | 볼륨에 대 한 USN 쓰기 범위 추적을 사용 하도록 설정 합니다. |
| c =`<chunk-size>` | 볼륨에서 추적할 청크 크기를 지정 합니다. |
| s =`<file-size-threshold>` | 범위 추적의 파일 크기 임계값을 지정 합니다. |
| enumdata | 열거 하 고 지정 된 두 경계 사이의 변경 저널 항목을 나열 합니다. |
| `<fileref>` | 열거형을 시작 하려면 볼륨에 있는 파일 내에서 서 수 위치를 지정 합니다. |
| `<lowUSN>` | 반환 되는 레코드를 필터링 하는 데 사용 하는 범위의 USN 값의 낮은 경계를 지정 합니다. 마지막 변경 저널 USN이 *lowusn* 및 *highusn* 멤버 값과 같은 레코드만 반환 됩니다. |
| `<highUSN>` | 반환 되는 파일을 필터링 하는 데 사용 되는 범위의 USN 값의 상한값을 지정 합니다. |
| queryjournal | 현재 변경 저널, 해당 레코드 및 해당 용량에 대 한 정보를 수집 하는 볼륨의 USN 데이터를 쿼리 합니다. |
| readdata | 파일에 대 한 USN 데이터를 읽습니다. |
| `<filename>` | 파일 이름 및 확장명을 포함 하는 파일의 전체 경로를 지정 합니다 (예: *C:\documents\filename.txt*). |
| readjournal | USN 저널에서 USN 레코드를 읽습니다. |
| minver =`<number>` | 반환할 USN_RECORD의 최소 주 버전입니다. 기본값은 2입니다. |
| maxver =`<number>` | 반환할 USN_RECORD의 최대 주 버전입니다. 기본값은 4입니다. |
| startusn =`<USN number>` | Usn 저널 읽기를 시작 하는 USN입니다. 기본값 = 0 |

#### <a name="remarks"></a>설명

- 프로그램을 모든 수정 된 파일 집합을 확인 하려면 USN 변경 저널을 참조 하세요. USN 변경 저널 타임 스탬프를 확인 하거나 파일 알림에 등록 보다 훨씬 더 효율적입니다. USN 변경 저널은 인덱싱 서비스, FRS (파일 복제 서비스), RIS (원격 설치 서비스) 및 원격 저장소에서 사용 하도록 설정 되 고 사용 됩니다.

- 볼륨에 변경 저널이 이미 있는 경우 **createjournal** 매개 변수는 변경 저널의 **maxsize** 및 **allocationdelta** 매개 변수를 업데이트 합니다. 그러면 활성 저널 불가능 하 게 하지 않고 관리 하는 레코드 수를 확장할 수 있습니다.

- 변경 저널을이 대상 값 보다 큰 증가할 수 있지만 변경 저널이이 값 보다 작은 값을 다음 NTFS 검사점에서 잘립니다. NTFS는 변경 저널을 검사 하 고 크기가 **maxsize** 의 값과 **allocationdelta**의 값을 초과할 때이를 자릅니다. NTFS 검사점에 운영 체제 오류에서 복구 하는 데 필요한 처리를 결정 하는 NTFS를 사용 하도록 설정 하는 NTFS 로그 파일에 레코드를 기록 합니다.

- 변경 저널은 트리밍 전에 **maxsize** 및 **allocationdelta** 값의 합계 보다 크게 증가할 수 있습니다.

- 활성 변경 저널을 삭제 하거나 사용 하지 않도록 설정 하면 시스템에서 MFT (마스터 파일 테이블)의 모든 레코드에 액세스 하 여 마지막 USN 특성을 0 (영)으로 설정 해야 하기 때문에 시간이 많이 소요 됩니다. 이 프로세스는 몇 분 정도 걸릴 수 하 고 다시 시작이 필요한 경우 시스템을 다시 시작한 후 계속할 수 있습니다. 이 과정에서 변경 저널 활성으로 간주 되지 않습니다도 그 사용 하지 않으면. 시스템 업무 일지를 비활성화 하는 동안 액세스할 수 없으며, 및 모든 저널 작업 오류를 반환 합니다. 주의 기울여야 극단적인 활성 저널을 사용 하지 않도록 설정 하는 경우 부정적인 영향을 주므로 저널을 사용 하는 다른 애플리케이션입니다.

### <a name="examples"></a>예

USN 변경 유형 C 드라이브에 저널을 만들려면:

```
fsutil usn createjournal m=1000 a=100 c:
```

활성 삭제 USN에 변경 저널을 C 드라이브 유형:

```
fsutil usn deletejournal /d c:
```

지정 된 청크 크기 및 파일 크기 임계값을 사용 하 여 범위 추적을 사용 하도록 설정 하려면 다음을 입력 합니다.

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

C 드라이브의 \Temp 폴더에 있는 파일에 대 한 USN 데이터를 읽으려면 다음을 입력 합니다.

```
fsutil usn readdata c:\temp\sample.txt
```

특정 시작 USN을 사용 하 여 USN 저널을 읽으려면 다음을 입력 합니다.

```
fsutil usn readjournal startusn=0xF00
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [fsutil](fsutil.md)
