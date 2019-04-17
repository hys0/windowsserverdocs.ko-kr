---
title: Server Core 설치에 대 한 메모리 덤프 파일 구성
description: Windows Server의 Server Core 설치에 대 한 메모리 덤프 파일을 구성 하는 방법을 설명 합니다.
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: bd22378ec7ce5a1ff4e39546246e6e85ca859c45
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "1448127"
---
# <a name="configure-memory-dump-files-for-server-core-installation"></a>Server Core 설치에 대 한 메모리 덤프 파일 구성

>적용 대상: Windows Server(반기 채널) 및 Windows Server 2016

Server Core 설치에 대 한 메모리 덤프를 구성 하려면 다음 단계를 사용 합니다. 

## <a name="step-1-disable-the-automatic-system-page-file-management"></a>1 단계: 자동으로 시스템 페이지 파일 관리를 사용 하지 않도록 설정

수동으로 시스템 오류 및 복구 옵션을 구성 하는 첫번째 단계는 합니다. 이것은 나머지 단계를 완료 해야 합니다.

다음 명령을 실행합니다. 

```
wmic computersystem set AutomaticManagedPagefile=False
```
 
## <a name="step-2-configure-the-destination-path-for-a-memory-dump"></a>2 단계: 메모리 덤프에 대 한 대상 경로 구성 합니다.

가 페이지 파일을 파티션에 운영 체제를 설치할 필요가 없습니다. 다른 파티션에 페이지 파일을 넣을, **DedicatedDumpFile**라는 새 레지스트리 항목도 만들어야 합니다. **DumpFileSize** 레지스트리 항목을 사용 하 여 페이징 파일의 크기를 정의할 수 있습니다. DedicatedDumpFile 및 DumpFileSize 레지스트리 항목을 만들려면 다음이 단계를 따릅니다. 

1. 명령 프롬프트를 **regedit** 명령을 실행 하 여 레지스트리 편집기를 엽니다.
2. 찾은 다음 레지스트리 하위 키를 클릭 한 다음: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl
3. 클릭 **편집 > 새로 만들기 > 문자열 값**합니다.
4. 값의 이름을 새 **DedicatedDumpFile**고 ENTER 키를 누릅니다.
5. **DedicatedDumpFile**마우스 오른쪽 단추로 클릭 하 고 한 다음 **수정**을 클릭 합니다.
6. **값 데이터** 형식에서 **\ < Drive\ >: \\\ < Dedicateddumpfile.sys\ >**, 한 다음 **확인**을 클릭 합니다.

   >[!NOTE] 
   > 교체 \ < Drive\ > 페이징 파일에 대 한 간격을 적용 하 고 바꾸기 충분 한 디스크 공간이 있는 드라이브와 \ < Dedicateddumpfile.dmp\ > 전용된 파일의 전체 경로와 합니다.
 
7. 클릭 **편집 > 새로 만들기 > DWORD 값**합니다.
8. **DumpFileSize**입력 하 고 ENTER 키를 누릅니다.
9. **DumpFileSize**마우스 오른쪽 단추로 클릭 하 고 한 다음 **수정**을 클릭 합니다.
10. **DWORD 값 편집** **자료** **10 진수**를 클릭 합니다.
11. **값 데이터**적절 한 값을 입력 한 다음 **확인**을 클릭 합니다.
   >[!NOTE]
   > 덤프 파일의 크기 (mb) 됩니다.
12. 레지스트리 편집기를 끝냅니다.

메모리 덤프의 파티션 위치를 결정 한 후에 페이지 파일에 대 한 대상 경로 구성 합니다. 페이지 파일에 대 한 현재 대상 경로 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get DebugFilePath
```

**DebugFilePath** 에 대 한 기본 대상은 %systemroot%\memory.dmp 표시 됩니다. 현재 대상 경로 변경 하려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS set DebugFilePath = <FilePath>
```

설정 \ < FilePath\ >의 대상 경로에 있습니다. 예 다음 명령은 C:\WINDOWS\MEMORY를 메모리 덤프 대상 경로 설정합니다. DMP: 

```
wmic RECOVEROS set DebugFilePath = C:\WINDOWS\MEMORY.DMP
```
 
## <a name="step-3-set-the-type-of-memory-dump"></a>3 단계: 메모리 덤프 유형 설정

구성 하 여 서버에 대 한 메모리 덤프 종류를 결정 합니다. 현재 메모리 덤프 종류를 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get DebugInfoType
```

현재 메모리 덤프 종류를 변경 하려면 다음 명령을 실행 합니다. 

```
wmic RECOVEROS set DebugInfoType = <Value>
```

\ \ 아래에 정의 된 대로 < Value\ > 0, 1, 2 또는 3 될 수 있습니다.

- 0: 메모리 덤프의 제거를 사용 하지 않도록 설정 합니다.
- 1: 전체 메모리 덤프 합니다. 컴퓨터가 예기치 않게 중지 될 때 시스템 메모리의 내용을 모두를 기록 합니다. 전체 메모리 덤프 메모리 덤프 수집 될 때 실행 중이 던 프로세스에서 데이터를 포함할 수 있습니다.
- 2: 커널 메모리 덤프 (기본값). 커널 메모리만 기록합니다. 컴퓨터가 예기치 않게 중지 하는 경우 로그 파일에 정보를 기록 하는 프로세스 속도가 향상 됩니다.
- 3: 작은 메모리 덤프 합니다. 가장 작은 집합이 컴퓨터가 예기치 않게 중지 된 이유를 확인할 수 있는 유용한 정보를 기록 합니다.

## <a name="step-4-configure-the-server-to-restart-automatically-after-generating-a-memory-dump"></a>4 단계: 메모리 덤프를 생성 한 후 자동으로 다시 시작 하도록 서버를 구성 합니다.

기본적으로 자동으로 서버는 메모리 덤프를 생성 한 후을 다시 시작 합니다. 현재 구성을 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get AutoReboot
```

**AutoReboot** 에 대 한 값이 TRUE 인 경우 서버는 자동으로 다시 시작 메모리 덤프를 생성 한 후 합니다. 구성이 필요 하지 않습니다 하 고 단계를 진행할 수 있습니다.

**AutoReboot** 에 대 한 값이 FALSE 이면 서버가 자동으로 다시 시작 되지 않습니다. 값을 변경 하려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS set AutoReboot = true
```
 
## <a name="step-5-configure-the-server-to-overwrite-the-existing-memory-dump-file"></a>5 단계: 기존 메모리 덤프 파일을 덮어쓰려면 서버를 구성 합니다.

기본적으로 서버 하나 만들어지는 새 때 기존 메모리 덤프 파일을 덮어씁니다. 기존 메모리 덤프 파일을 덮어쓸 수 이미 구성 되어를 확인 하려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get OverwriteExistingDebugFile
```

값이 1 이면 하는 경우 서버는 기존 메모리 덤프 파일을 덮어씁니다. 없음 구성이 필요 하 고 단계를 진행할 수 있습니다.

값이 0 이면 서버 기존 메모리 덤프 파일을 덮어씁니다 되지 않습니다. 값을 변경 하려면 다음 명령을 실행 합니다. 

```
wmic RECOVEROS set OverwriteExistingDebugFile = 1
```
 
## <a name="step-6-set-an-administrative-alert"></a>6 단계: 관리 경고를 설정 합니다.

관리 경고 적합 한지 여부를 결정 하 고 **SendAdminAlert** 를 적절 하 게 설정 합니다. SendAdminAlert에 대 한 현재 값을 보려면 다음 명령을 실행 합니다.

```
wmic RECOVEROS get SendAdminAlert
```

SendAdminAlert에 대 한 사용 가능한 값은 TRUE 또는 false로 설정 합니다. True로 기존 SendAdminAlert 값을 수정 하려면 다음 명령을 실행 합니다. 

```
wmic RECOVEROS set SendAdminAlert = true
```
 
## <a name="step-7-set-the-memory-dumps-page-file-size"></a>7 단계: 메모리 덤프의 페이지 파일 크기를 설정 합니다.

현재 페이지 파일 설정을 확인 하려면 다음 명령 중 하나를 실행 합니다.

   ```
   wmic.exe pagefile
   ```

   또는

   ```
   wmic.exe pagefile list /format:list
   ```

예, 페이지 파일의 초기 및 최대 크기를 구성 하려면 다음 명령을 실행 합니다.

```
wmic pagefileset where name="c:\\pagefile.sys" set InitialSize=1000,MaximumSize=5000
```

## <a name="step-8-configure-the-server-to-generate-a-manual-memory-dump"></a>8 단계: 수동 메모리 덤프를 생성 하도록 서버를 구성 합니다.

PS/2 키보드를 사용 하 여 수동으로 메모리 덤프를 생성할 수 있습니다. 이 기능은 기본적으로 사용 하지 않도록 설정 하 고 범용 직렬 버스 (USB) 키보드를 사용할 수 없는 합니다.

수동 메모리를 사용 하도록 설정 하려면 다음 명령을 실행 하는 PS/2 키보드를 사용 하 여 덤프:

```
reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters /v CrashOnCtrlScroll /t REG_DWORD /d 1 /f
```

기능이 제대로 활성화 된 경우를 확인 하려면 다음 명령을 실행 합니다.

```
Reg query HKEY_LOCAL_MACHINE \ SYSTEM \ CurrentControlSet \ Services \ i8042prt \ Parameters / v CrashOnCtrlScroll
```

변경 내용을 적용 하려면 서버를 다시 시작 해야 합니다. 다음 명령을 실행 하 여 서버를 다시 시작할 수 있습니다.

```
Shutdown / r / t 0
```

오른쪽 CTRL 키를 두 번 SCROLL LOCK 키를 누르면 채 하 여 서버에 연결 된 PS/2 키보드와 수동 메모리 덤프를 생성할 수 있습니다. 이렇게 하면 컴퓨터 버그 0xE2 오류 코드로 확인 합니다. 서버를 다시 시작 하면 새 덤프 파일을 2 단계에서 설정한 대상 경로에 나타납니다.

## <a name="step-9-verify-that-memory-dump-files-are-being-created-correctly"></a>단계 9: 파일이 올바르게 만들어지고 해당 메모리 덤프를 확인 하십시오.

메모리 덤프 파일은 되 고 제대로 만들어졌는지 확인 하려면 dumpchk.exe 유틸리티를 사용할 수 있습니다. 데스크톱 경험을 사용 하 여 서버에서 또는 Windows 10에서 실행 해야 하므로 dumpchk.exe 유틸리티 Server Core 설치 옵션을 함께 설치 되어있지 않습니다. 또한 Windows 제품용 디버깅 도구를 설치 해야 합니다.  

Dumpchk.exe 유틸리티를 사용 하면 사용자가 선택한 중간 규모를 사용 하 여 다른 컴퓨터에 Windows Server 2008의 Server Core 설치에서 메모리 덤프 파일을 전송할 수 있습니다.

> [!WARNING]
> 페이지 파일을 주의깊게 메서드 및 메서드를 사용 하려면 리소스 전송 고려 매우 커질 수 있습니다.
 

추가 참조 자료

메모리 덤프 파일을 사용 하는 방법에 대 한 일반적인 정보에 대 한 [Windows에 대 한 메모리 덤프 파일 옵션의 개요](https://support.microsoft.com/help/254649/overview-of-memory-dump-file-options-for-windows)를 참조 합니다.

전용된 덤프 파일에 대 한 자세한 내용은 [시스템 메모리 덤프를 캡처하는 동안 시스템 드라이브 공간 한계를 극복 하기 위해 DedicatedDeumpFile 레지스트리 값을 사용 하는 방법을](https://blogs.msdn.microsoft.com/ntdebugging/2010/04/02/how-to-use-the-dedicateddumpfile-registry-value-to-overcome-space-limitations-on-the-system-drive-when-capturing-a-system-memory-dump/)참조 하십시오.



