---
title: bitsadmin 예제
description: 다음 예에서는 bitsadmin 도구를 사용 하 여 가장 일반적인 작업을 수행 하는 방법을 보여 줍니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 96447410f76e4402c456b5ec402cc730480aedaf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80850806"
---
# <a name="bitsadmin-examples"></a>bitsadmin 예제

다음 예에서는 `bitsadmin` 도구를 사용 하 여 가장 일반적인 작업을 수행 하는 방법을 보여 줍니다.

## <a name="transfer-a-file"></a>파일 전송

**/Stransfer** 스위치는 아래에 나열 된 작업을 수행 하기 위한 바로 가기입니다. 이 스위치는 작업을 만들고, 작업에 파일을 추가 하 고, 전송 큐에서 작업을 활성화 하 고, 작업을 완료 합니다. BITSAdmin은 전송이 완료 되거나 오류가 발생할 때까지 MS-DOS 창에 진행률 정보를 계속 표시 합니다.

`bitsadmin /transfer myDownloadJob /download /priority normal https://downloadsrv/10mb.zip c:\\10mb.zip`

## <a name="create-a-download-job"></a>다운로드 작업 만들기

**/Create** 스위치를 사용 하 여 mydownloadjob 이라는 다운로드 작업을 만듭니다.

### <a name="syntax"></a>구문

```
bitsadmin /create myDownloadJob
```

BITSAdmin은 작업을 고유 하 게 식별 하는 GUID를 반환 합니다. 후속 호출에서 GUID 또는 작업 이름을 사용 합니다. 다음 텍스트는 샘플 출력입니다.

#### <a name="sample-output"></a>샘플 출력

`created job {C775D194-090F-431F-B5FB-8334D00D1CB6}`

## <a name="add-files-to-the-download-job"></a>다운로드 작업에 파일 추가

**/Addfile** 스위치를 사용 하 여 작업에 파일을 추가 합니다. 추가 하려는 각 파일에 대 한이 호출을 반복 합니다.

여러 작업에서 myDownloadJob을 이름으로 사용 하는 경우 작업을 고유 하 게 식별 하려면 myDownloadJob을 작업 GUID로 바꾸어야 합니다.

### <a name="syntax"></a>구문

```
bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip
```

## <a name="activate-the-download-job"></a>다운로드 작업 활성화

새 작업을 만들 때 BITS는 작업을 일시 중단 합니다. 전송 큐에서 작업을 활성화 하려면 **/resume 재개** 스위치를 사용 합니다.

여러 작업에서 myDownloadJob을 이름으로 사용 하는 경우 작업을 고유 하 게 식별 하려면 myDownloadJob을 작업 GUID로 바꾸어야 합니다.

### <a name="syntax"></a>구문

`bitsadmin /resume myDownloadJob`

## <a name="determine-the-progress-of-the-download-job"></a>다운로드 작업의 진행 상황 확인

**/Cinfo** 스위치를 사용 하 여 작업 상태 및 전송 된 파일 수와 바이트 수를 반환 합니다. 상태가 전송 되 면 BITS는 작업의 모든 파일을 성공적으로 전송 합니다.

- **/Verbose** 인수를 사용 하 여 작업에 대 한 전체 세부 정보를 가져옵니다.

- **/List** 또는 **/cmonitor** 스위치를 사용 하 여 전송 큐의 모든 작업을 가져옵니다.

여러 작업에서 myDownloadJob을 이름으로 사용 하는 경우 작업을 고유 하 게 식별 하려면 myDownloadJob을 작업 GUID로 바꾸어야 합니다.

### <a name="syntax"></a>구문

`bitsadmin /info myDownloadJob /verbose`

#### <a name="sample-output"></a>샘플 출력

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

## <a name="completing-the-download-job"></a>다운로드 작업 완료

작업의 상태를 전송 하는 경우 BITS가 작업의 모든 파일을 전송 했습니다. 그러나 파일이 사용할 수 없는 사용 하기 전에 **완료 /** 전환 합니다.

여러 작업에서 myDownloadJob을 이름으로 사용 하는 경우 작업을 고유 하 게 식별 하려면 myDownloadJob을 작업 GUID로 바꾸어야 합니다.

### <a name="syntax"></a>구문

`bitsadmin /complete myDownloadJob`

## <a name="monitoring-jobs-in-the-transfer-queue"></a>전송 큐의 작업 모니터링

**/List**, **/cmonitor**또는 **/cinfo** 스위치를 사용 하 여 전송 큐의 작업을 모니터링할 수 있습니다. **/List** 스위치는 큐의 모든 작업에 대 한 정보를 제공 합니다.

## <a name="list-switch"></a>/list 스위치

**/List** 스위치는 작업의 상태 및 전송 큐의 모든 작업에 대해 전송 된 파일 및 바이트 수를 반환 합니다.

### <a name="syntax"></a>구문

`bitsadmin /list`

#### <a name="sample-output-for-the-list-switch"></a>/List 스위치에 대 한 샘플 출력

```
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

## <a name="monitor-switch"></a>/모니터 스위치

**/Cmonitor** 스위치는 작업 상태 및 전송 큐의 모든 작업에 대해 전송 된 파일 및 바이트 수를 반환 하 고 5 초 마다 데이터를 새로 고칩니다. 새로 고침을 중지 하려면 CTRL + C를 누릅니다.

### <a name="syntax"></a>구문

`bitsadmin /monitor`

#### <a name="sample-output"></a>샘플 출력

```
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="deleting-jobs-from-the-transfer-queue"></a>전송 큐에서 작업 삭제

**/Reset** 스위치를 사용 하 여 전송 큐에서 모든 작업을 제거 합니다.

### <a name="syntax"></a>구문

`bitsadmin /reset`

#### <a name="sample-output"></a>샘플 출력

```
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```
