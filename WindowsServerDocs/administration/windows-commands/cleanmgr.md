---
title: cleanmgr
description: 디스크 정리 도구를 특정 파일을 자동으로 정리 (Cleanmgr.exe)를 구성 하려면 명령줄 옵션을 사용 하는 방법에 알아봅니다.
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: fd722dda8476891860773126c84ed10f125715f0
ms.sourcegitcommit: 545dcfc23a81943e129565d0ad188263092d85f6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2019
ms.locfileid: "67407890"
---
# <a name="cleanmgr"></a>cleanmgr

> 적용 대상: Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2008 R2, Windows Server (반기 채널)

컴퓨터의 하드 디스크에서 불필요 한 파일을 지웁니다. Cleanmgr Temp 파일, 인터넷 파일을 다운로드 한 파일 및 재활용 bin 파일을 정리 하지 않으려면 명령줄 옵션을 사용할 수 있습니다. 예약 된 작업 도구를 사용 하 여 특정 시간에 실행 되도록 작업을 예약할 수 있습니다.

이 명령을 사용하는 방법의 예는 [예](#examples)를 참조하세요.

## <a name="syntax"></a>구문

```
cleanmgr [/d <driveletter>] [/sageset:n]  [/sagerun:n] [/TUNEUP:n] [/LOWDISK] [/VERYLOWDISK]
```

## <a name="parameters"></a>매개 변수

|      매개 변수      |    설명     |
| ------------------- | ------------------ |
|  /d \<driveletter>          | 드라이브를 청소 하는 디스크 정리를 지정 합니다.<br>**참고:** /D 옵션 /sagerun:n을 사용 하 여 사용 되지 않습니다. |
| /sageset:n | 디스크 정리 설정 대화 상자를 표시 하 고 또한 선택 하는 설정을 저장 하는 레지스트리 키를 만듭니다. `n` 레지스트리에 저장 된 값을 사용 하면 실행 하는 디스크 정리에 대 한 작업을 지정할 수 있습니다. `n` 0에서 65535 사이의 정수 값을 값일 수 있습니다. 가 모든 사용 가능한 옵션 /sageset 옵션을 사용 하려면 Windows를 설치한 드라이브를 지정 합니다.  |
|  /sagerun:n  |  \Sageset 옵션을 사용 하는 경우 n 값에 할당 된 지정된 된 작업을 실행 합니다. 컴퓨터의 모든 드라이브를 열거 하 고 각 드라이브에 대해 선택한 프로필을 실행 합니다.           |
| /TUNEUP:n    | 동일한 /sageset 및 /sagerun 실행 `n` 합니다. |
| / LOWDISK     | 기본 설정을 사용 하 여 실행 합니다. |
| / VERYLOWDISK | 사용자 요구를 기본 설정으로 실행 합니다. |
| /?           | 도움말을 표시 합니다. |

## <a name="options"></a>변수

디스크 정리를 위한 /sageset 및 /sagerun 사용 하 여 지정할 수 있는 파일에 대 한 옵션은 다음과 같습니다.

- **설치 파일을 임시** -이러한 파일은 더 이상 실행 하는 설치 프로그램에 의해 생성 된 파일입니다.

- **프로그램 파일을 다운로드 한** -다운로드 한 프로그램 파일은 ActiveX 컨트롤 및 Java 프로그램는 특정 페이지를 볼 때 인터넷에서 자동으로 다운로드 됩니다. 이러한 파일은 하드 디스크에 다운로드 한 프로그램 파일 폴더에 임시로 저장 됩니다. 디스크 정리 제거 하기 전에 파일을 볼 수 있도록이 옵션에서 파일 보기 단추를 포함 합니다. 단추는 C:\Winnt\Downloaded Program Files 폴더를 엽니다.

- **임시 인터넷 파일** -의 Temporary Internet Files 폴더에는 빠른 보기에 대 한 하드 디스크에 저장 되어 있는 웹 페이지가 있습니다. 디스크 정리 이러한 페이지를 제거 하지만 웹 페이지에 대 한 사용자 설정을 그대로 둡니다. 이 옵션에는 또한 파일 보기 단추 C:\Documents and settings\ Settings\Temporary 인터넷 Files\Content.IE5 폴더를 포함 합니다. 

- **오래 된 Chkdsk 파일** -오류에 대 한 디스크를 검사 하는 경우 Chkdsk, Chkdsk 디스크의 루트 폴더에 파일로 손실 된 파일 조각에 저장 될 수 있습니다. 이러한 파일이 필요 하지 않습니다.

- **휴지통** -휴지통은 컴퓨터에서 삭제 한 파일을 포함 합니다. 휴지통을 비울 때까지 이러한 파일이 영구적으로 제거 되지 않습니다. 이 옵션에는 휴지통에 열리는 파일 보기 단추가 포함 됩니다. **참고:** 휴지통에는 % SystemRoot %에서 뿐만 아니라 예를 들어 둘 이상의 드라이브에 나타날 수 있습니다.

- **임시 파일** -경우에 따라 프로그램 Temp 폴더에 임시 정보를 저장 합니다. 프로그램이 종료 되기 전에 프로그램은 일반적으로이 정보를 삭제 합니다. 지난 주에 수정 되지 않은 임시 파일을 안전 하 게 삭제할 수 있습니다.

- **오프 라인 파일을 임시** -오프 라인 임시 파일은 최근에 사용한 네트워크 파일의 로컬 복사본. 이러한 파일은 네트워크에서 연결을 끊은 후 사용할 수 있도록 자동으로 캐시 됩니다. 파일 보기 단추 오프 라인 파일 폴더를 엽니다.

- **오프 라인 파일** -오프 라인 파일은 구체적으로 사용할 수 있는 오프 라인으로 네트워크에서 연결을 끊은 후 사용할 수 있도록 하려는 네트워크 파일의 로컬 복사본. 파일 보기 단추 오프 라인 파일 폴더를 엽니다.

- **오래 된 파일 압축** -Windows에는 최근에 사용 하지 않은 파일만 압축 될 수 있습니다. 디스크 공간을 절약 파일을 압축 하지만 파일을 계속 사용할 수 있습니다. 파일이 삭제 됩니다. 서로 다른 속도로 파일 압축 하면 얻을 수 있는 디스크 공간의 표시 되는 시간은 이므로 대략적인 합니다. 옵션 단추를를 통해 디스크 정리를 사용 하지 않는 파일을 압축 하기 전에 대기할 일 수를 지정할 수 있습니다.

- **파일 콘텐츠 인덱서에 대 한 카탈로그** -The 인덱싱 서비스 속도 디스크에 있는 파일의 인덱스를 유지 하 여 파일 검색을 개선 합니다. 이러한 카탈로그 파일 이전 인덱싱 작업의 상태를 유지 하 고 안전 하 게 삭제할 수 있습니다. **참고:** 카탈로그 파일은 % SystemRoot %에서 뿐만 아니라 예를 들어 둘 이상의 드라이브에 나타날 수 있습니다.

**참고** 정리 하 여 Windows 설치를 포함 하는 드라이브를 지정 하는 경우 이러한 모든 옵션에서 사용할 디스크 정리 탭 합니다. 다른 드라이브를 지정 하는 경우만 휴지통 및 콘텐츠 인덱스 옵션에 대 한 카탈로그 파일은 디스크 정리 탭에서 제공 됩니다. 

## <a name="examples"></a>예

디스크 정리 앱을 실행 되므로 집합에 설정을 저장, 나중에 사용할 옵션을 지정 하 여 대화 상자를 사용할 수 있습니다 **1**, 다음을 입력 합니다.

```
cleanmgr /sageset:1
```

디스크 정리를 실행 하 고 cleanmgr /sageset:1 명령을 사용 하 여 지정 된 옵션을 포함 하려면 다음을 입력 합니다.

```
cleanmgr /sagerun:1
```

실행할 ```cleanmgr /sageset:1``` 및 ```cleanmgr /sagerun:1``` 함께 입력 합니다.

```
cleanmgr /tuneup:1
```

## <a name="additional-references"></a>추가 참조

[Windows 10의 드라이브 공간을 확보 하기](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)
