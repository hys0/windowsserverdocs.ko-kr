---
title: bitsadmin examples
description: Bitsadmin 도구를 사용 하 여 가장 일반적인 작업을 수행 하는 방법을 보여 주는 예입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 1db9dd387d7b9cc39c582ce79e5163c83579b613
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83819633"
---
# <a name="bitsadmin-examples"></a>bitsadmin examples

다음 예제에서는 도구를 사용 하 여 가장 일반적인 작업을 수행 하는 방법을 보여 줍니다 `bitsadmin` .

## <a name="transfer-a-file"></a>파일 전송

작업을 만들려면 파일을 추가 하 고, 전송 큐에서 작업을 활성화 하 고, 작업을 완료 합니다.

`bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip`

BITSAdmin은 전송이 완료 되거나 오류가 발생할 때까지 MS-DOS 창에 진행률 정보를 계속 표시 합니다.

## <a name="create-a-download-job"></a>다운로드 작업 만들기

*Mydownloadjob*이라는 다운로드 작업을 만들려면 다음을 수행 합니다.

```
bitsadmin /create myDownloadJob
```

BITSAdmin은 작업을 고유 하 게 식별 하는 GUID를 반환 합니다. 후속 호출에서 GUID 또는 작업 이름을 사용 합니다. 다음 텍스트는 샘플 출력입니다.

### <a name="sample-output"></a>샘플 출력

`created job {C775D194-090F-431F-B5FB-8334D00D1CB6}`

## <a name="add-files-to-the-download-job"></a>다운로드 작업에 파일 추가

작업에 파일을 추가 하려면 다음을 수행 합니다.

```
bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip
```

추가 하려는 각 파일에 대 한이 호출을 반복 합니다. 여러 작업에서 *Mydownloadjob* 을 이름으로 사용 하는 경우 작업의 GUID를 사용 하 여 완료를 위해 고유 하 게 식별 해야 합니다.

## <a name="activate-the-download-job"></a>다운로드 작업 활성화

새 작업을 만든 후 BITS가 자동으로 작업을 일시 중단 합니다. 전송 큐에서 작업을 활성화 하려면:

```
bitsadmin /resume myDownloadJob
```

여러 작업에서 *Mydownloadjob* 을 이름으로 사용 하는 경우 작업의 GUID를 사용 하 여 완료를 위해 고유 하 게 식별 해야 합니다.

## <a name="determine-the-progress-of-the-download-job"></a>다운로드 작업의 진행 상황 확인

**/Sinfo** 스위치는 작업 상태 및 전송 된 파일 수와 바이트 수를 반환 합니다. 상태가로 표시 되 면 `TRANSFERRED` BITS가 작업의 모든 파일을 성공적으로 전송 했음을 의미 합니다. 또한 **/verbose** 인수를 추가 하 여 작업에 대 한 전체 세부 정보를 가져오고, **/list** 또는 **/cmonitor** 를 추가 하 여 전송 큐의 모든 작업을 가져올 수 있습니다.

작업 상태를 반환 하려면:

```
bitsadmin /info myDownloadJob /verbose
```

여러 작업에서 *Mydownloadjob* 을 이름으로 사용 하는 경우 작업의 GUID를 사용 하 여 완료를 위해 고유 하 게 식별 해야 합니다.

## <a name="complete-the-download-job"></a>다운로드 작업 완료

상태가 다음으로 변경 된 후 작업을 완료 하려면 `TRANSFERRED` :

```
bitsadmin /complete myDownloadJob
```

`/complete`작업의 파일을 사용할 수 있게 하려면 먼저 스위치를 실행 해야 합니다. 여러 작업에서 *Mydownloadjob* 을 이름으로 사용 하는 경우 작업의 GUID를 사용 하 여 완료를 위해 고유 하 게 식별 해야 합니다.

## <a name="monitor-jobs-in-the-transfer-queue-using-the-list-switch"></a>/List 스위치를 사용 하 여 전송 큐의 작업 모니터링

작업 상태 및 전송 큐의 모든 작업에 대해 전송 되는 파일 및 바이트 수를 반환 하려면:

```
bitsadmin /list
```

### <a name="sample-output"></a>샘플 출력

```
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-monitor-switch"></a>/Cmonitor 스위치를 사용 하 여 전송 큐의 작업 모니터링

작업 상태 및 전송 큐의 모든 작업에 대해 전송 된 파일 및 바이트 수를 반환 하려면 5 초 마다 데이터를 새로 고칩니다.

```
bitsadmin /monitor
```

> [!NOTE]
> 새로 고침을 중지 하려면 CTRL + C를 누릅니다.

### <a name="sample-output"></a>샘플 출력

```
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="monitor-jobs-in-the-transfer-queue-using-the-info-switch"></a>/Sinfo 스위치를 사용 하 여 전송 큐의 작업 모니터링

작업 상태 및 전송 된 파일 수와 바이트 수를 반환 하려면:

```
bitsadmin /info
```

### <a name="sample-output"></a>샘플 출력

```
GUID: {482FCAF0-74BF-469B-8929-5CCD028C9499} DISPLAY: myDownloadJob
TYPE: DOWNLOAD STATE: TRANSIENT_ERROR OWNER: domain\user
PRIORITY: NORMAL FILES: 0 / 1 BYTES: 0 / UNKNOWN
CREATION TIME: 12/17/2002 1:21:17 PM MODIFICATION TIME: 12/17/2002 1:21:30 PM
COMPLETION TIME: UNKNOWN
NOTIFY INTERFACE: UNREGISTERED NOTIFICATION FLAGS: 3
RETRY DELAY: 600 NO PROGRESS TIMEOUT: 1209600 ERROR COUNT: 0
PROXY USAGE: PRECONFIG PROXY LIST: NULL PROXY BYPASS LIST: NULL
ERROR FILE:    https://downloadsrv/10mb.zip -> c:\10mb.zip
ERROR CODE:    0x80072ee7 - The server name or address could not be resolved
ERROR CONTEXT: 0x00000005 - The error occurred while the remote file was being
processed.
DESCRIPTION:
JOB FILES:
0 / UNKNOWN WORKING https://downloadsrv/10mb.zip -> c:\10mb.zip
NOTIFICATION COMMAND LINE: none
```

## <a name="delete-jobs-from-the-transfer-queue"></a>전송 큐에서 작업 삭제

전송 큐에서 모든 작업을 제거 하려면/reset 스위치를 사용 합니다.

```
bitsadmin /reset
```

### <a name="sample-output"></a>샘플 출력

```
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
