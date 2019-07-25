---
title: Server Core 설치를 위한 메모리 덤프 파일 구성
description: Windows Server의 Server Core 설치에 대 한 메모리 덤프 파일을 구성 하는 방법에 대해 알아봅니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: 0cea3118abce156acdd9ad933518015a25f8afbf
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476559"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Server Core 설치를 위한 메모리 덤프 파일 구성

>적용 대상: Windows Server 2019, Windows Server 2016 및 Windows Server (반기 채널)

다음 단계를 사용 하 여 Server Core 설치에 대 한 메모리 덤프를 구성 합니다. 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>1단계: 자동 시스템 페이지 파일 관리 사용 안 함

첫 번째 단계는 시스템 오류 및 복구 옵션을 수동으로 구성 하는 것입니다. 나머지 단계를 완료 하려면이 작업을 수행 해야 합니다.

다음 명령을 실행합니다. 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>2단계: 메모리 덤프의 대상 경로 구성

운영 체제가 설치 된 파티션에는 페이지 파일이 필요 하지 않습니다. 다른 파티션에 페이지 파일을 저장 하려면 **DedicatedDumpFile**이라는 새 레지스트리 항목을 만들어야 합니다. **DumpFileSize** 레지스트리 항목을 사용 하 여 페이징 파일의 크기를 정의할 수 있습니다. DedicatedDumpFile 및 DumpFileSize 레지스트리 항목을 만들려면 다음 단계를 수행 합니다. 

1. 명령 프롬프트에서 **regedit** 명령을 실행 하 여 레지스트리 편집기를 엽니다.
2. 다음 레지스트리 하위 키를 찾아 클릭합니다. HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
3. **편집 > 새로 만들기 > 문자열 값**을 클릭 합니다.
4. 새 값의 이름을 **DedicatedDumpFile**로 지정한 다음 enter 키를 누릅니다.
5. **DedicatedDumpFile**를 마우스 오른쪽 단추로 클릭 한 다음 **수정**을 클릭 합니다.
6. **값 데이터** 형식  **\<드라이브\>:Dedicateddumpfile을입력한다음확인을클릭합니다.\\\<\>**

   >[!NOTE] 
   > Drive \< \<\> 를 페이징 파일에 충분 한 디스크 공간이 있는 드라이브로 바꾸고 Dedicateddumpfile을 전용 파일의 전체 경로로 바꿉니다.\>
 
7. **편집 > 새로 만들기 > DWORD 값**을 클릭 합니다.
8. **DumpFileSize**를 입력 한 다음 enter 키를 누릅니다.
9. **DumpFileSize**를 마우스 오른쪽 단추로 클릭 한 다음 **수정**을 클릭 합니다.
10. **DWORD 값 편집**의 **밑**에서 **10 진수**를 클릭 합니다.
11. **값 데이터**에 적절 한 값을 입력 한 다음 **확인**을 클릭 합니다.
    >[!NOTE]
    > 덤프 파일의 크기 (MB)입니다.
12. 레지스트리 편집기를 종료 합니다.

메모리 덤프의 파티션 위치를 확인 한 후에는 페이지 파일에 대 한 대상 경로를 구성 합니다. 페이지 파일에 대 한 현재 대상 경로를 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get DebugFilePath
```

**Debugfilepath** 의 기본 대상은%systemroot%\memory.dmp.입니다. 현재 대상 경로를 변경 하려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

\<FilePath\> 를 대상 경로로 설정 합니다. 예를 들어 다음 명령은 메모리 덤프 대상 경로를 C:\WINDOWS\MEMORY.로 설정 합니다. DMP 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>3단계: 메모리 덤프 유형 설정

서버에 대해 구성할 메모리 덤프 유형을 결정 합니다. 현재 메모리 덤프 유형을 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get DebugInfoType
```

현재 메모리 덤프 유형을 변경 하려면 다음 명령을 실행 합니다. 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\<값\> 은 아래에 정의 된 대로 0, 1, 2 또는 3 일 수 있습니다.

- 0: 메모리 덤프 제거를 사용 하지 않도록 설정 합니다.
- 1: 전체 메모리 덤프. 컴퓨터가 예기치 않게 중지 될 때 시스템 메모리의 모든 콘텐츠를 기록 합니다. 전체 메모리 덤프에는 메모리 덤프가 수집 될 때 실행 중 이었던 프로세스의 데이터가 포함 될 수 있습니다.
- 2: 커널 메모리 덤프 (기본값). 커널 메모리만 기록합니다. 이는 컴퓨터가 예기치 않게 중지 될 때 로그 파일에 정보를 기록 하는 프로세스를 가속화 합니다.
- 3: 작은 메모리 덤프. 컴퓨터가 예기치 않게 중지 된 이유를 식별 하는 데 도움이 될 수 있는 가장 작은 유용한 정보 집합을 기록 합니다.

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>4단계: 메모리 덤프를 생성 한 후 자동으로 다시 시작 되도록 서버 구성

기본적으로 서버는 메모리 덤프를 생성 한 후 자동으로 다시 시작 됩니다. 현재 구성을 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get AutoReboot
```

**AutoReboot** 의 값이 TRUE 이면 메모리 덤프를 생성 한 후 서버가 자동으로 다시 시작 됩니다. 구성이 필요 하지 않으며 다음 단계로 진행할 수 있습니다.

**AutoReboot** 의 값이 FALSE 이면 서버가 자동으로 다시 시작 되지 않습니다. 다음 명령을 실행 하 여 값을 변경 합니다.

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>5단계: 기존 메모리 덤프 파일을 덮어쓰도록 서버 구성

기본적으로 서버는 새 파일을 만들 때 기존 메모리 덤프 파일을 덮어씁니다. 기존 메모리 덤프 파일을 덮어쓰도록 이미 구성 했는지 확인 하려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

값이 1 이면 서버는 기존 메모리 덤프 파일을 덮어씁니다. 구성이 필요 하지 않으며 다음 단계로 진행할 수 있습니다.

값이 0 이면 서버는 기존 메모리 덤프 파일을 덮어쓰지 않습니다. 다음 명령을 실행 하 여 값을 변경 합니다. 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>6단계: 관리 경고 설정

관리 경고가 적절 한지 확인 하 고이에 따라 **Sendadminalert** 를 설정 합니다. SendAdminAlert의 현재 값을 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get SendAdminAlert
```

SendAdminAlert에 사용할 수 있는 값은 TRUE 또는 FALSE입니다. 기존 SendAdminAlert 값을 true로 수정 하려면 다음 명령을 실행 합니다. 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>7단계: 메모리 덤프의 페이지 파일 크기를 설정 합니다.

현재 페이지 파일 설정을 확인 하려면 다음 명령 중 하나를 실행 합니다.

   ```
   wmic.exe pagefile
   ```

   로 구분하거나 여러

   ```
   wmic.exe pagefile list /format:list
   ```

예를 들어 다음 명령을 실행 하 여 페이지 파일의 초기 크기와 최대 크기를 구성 합니다.

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>8단계: 서버를 구성 하 여 수동 메모리 덤프 생성

PS/2 키보드를 사용 하 여 메모리 덤프를 수동으로 생성할 수 있습니다. 이 기능은 기본적으로 사용 하지 않도록 설정 되어 있으며, USB (범용 직렬 버스) 키보드에는 사용할 수 없습니다.

PS/2 키보드를 사용 하 여 수동 메모리 덤프를 사용 하도록 설정 하려면 다음 명령을 실행 합니다.

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

기능이 제대로 사용 하도록 설정 되었는지 확인 하려면 다음 명령을 실행 합니다.

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

변경 내용을 적용 하려면 서버를 다시 시작 해야 합니다. 다음 명령을 실행 하 여 서버를 다시 시작할 수 있습니다.

```
Shutdown / r / t 0
```

SCROLL LOCK 키를 두 번 누를 때 오른쪽 CTRL 키를 누른 상태에서 서버에 연결 된 PS/2 키보드를 사용 하 여 수동 메모리 덤프를 생성할 수 있습니다. 이렇게 하면 컴퓨터 버그 검사에 오류 코드 0xE2가 사용 됩니다. 서버를 다시 시작 하면 2 단계에서 설정한 대상 경로에 새 덤프 파일이 표시 됩니다.

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>9단계: 메모리 덤프 파일이 올바르게 만들어졌는지 확인 합니다.

Dumpchk를 사용 하 여 메모리 덤프 파일이 올바르게 생성 되었는지 확인할 수 있습니다. Dumpchk 유틸리티는 Server Core 설치 옵션과 함께 설치 되지 않으므로 데스크톱 환경이 나 Windows 10이 설치 된 서버에서 실행 해야 합니다. 또한 Windows 제품용 디버깅 도구를 설치 해야 합니다.  

Dumpchk 유틸리티를 사용 하면 선택한 미디어를 사용 하 여 Windows Server 2008의 Server Core 설치에서 다른 컴퓨터로 메모리 덤프 파일을 전송할 수 있습니다.

> [!WARNING]
> 페이지 파일은 매우 클 수 있으므로 전송 방법 및 메서드에 필요한 리소스를 신중 하 게 고려해 야 합니다.
 

추가 참조

메모리 덤프 파일을 사용 하는 방법에 대 한 일반 정보는 [Windows의 메모리 덤프 파일 옵션 개요](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows)를 참조 하세요.

전용 덤프 파일에 대 한 자세한 내용은 [시스템 메모리 덤프를 캡처하는 동안 시스템 드라이브의 공간 제한을 극복 하려면 DedicatedDeumpFile 레지스트리 값을 사용 하는 방법](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/)을 참조 하세요.



