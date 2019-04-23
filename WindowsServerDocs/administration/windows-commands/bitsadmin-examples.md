---
title: bitsadmin 예제
description: 다음 예에서는 가장 일반적인 작업을 수행 하려면 bitsadmin 도구를 사용 하는 방법을 보여 줍니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb8f8374-ba6e-4a68-85a1-9a95b8215354
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/31/2018
ms.openlocfilehash: 4b9deb4fc7fbfccf569250e965274009764054f7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849334"
---
# <a name="bitsadmin-examples"></a>bitsadmin 예제

다음 예제에 사용 하는 방법을 보여 줍니다는 `bitsadmin` 도구에서 가장 일반적인 작업을 수행 합니다.

## <a name="transfer-a-file"></a>파일 전송

합니다 **/transfer** 스위치 아래에 나열 된 작업을 수행 하는 것에 대 한 바로 가기입니다. 이 스위치 작업, 파일 작업을 추가 합니다, 활성화 하는 전송 큐에서 작업을 만들고 작업을 완료 합니다. BITSAdmin 계속 전송이 완료 되거나 오류가 발생할 때까지 MS-DOS 창에 진행률 정보를 표시 합니다.

**bitsadmin /transfer myDownloadJob /download /priority 정상적인 https://downloadsrv/10mb.zip c:\\10mb.zip**

## <a name="create-a-download-job"></a>다운로드 작업 만들기

사용 합니다 **를 만드는** 전환 myDownloadJob 이라는 다운로드 작업을 만듭니다.

**bitsadmin myDownloadJob 만들기 /**

BITSAdmin 고유 하 게 작업을 식별 하는 GUID를 반환 합니다. 후속 호출에서 GUID 또는 작업 이름을 사용 합니다. 다음 텍스트는 샘플 출력입니다.

``` syntax
Created job {C775D194-090F-431F-B5FB-8334D00D1CB6}.
```

다음을 사용 하 여 합니다 **/addfile** 다운로드 작업에 하나 이상의 파일을 추가할 스위치입니다.

## <a name="add-files-to-the-download-job"></a>다운로드 작업에 파일 추가

사용 된 **/addfile** 파일 작업에 추가할 스위치입니다. 추가 하려는 각 파일에 대 한이 호출을 반복 합니다. MyDownloadJob 해당 이름으로 사용 하는 여러 작업을 고유 하 게 작업을 식별 하는 작업의 GUID를 사용 하 여 myDownloadJob 바꾸어야 합니다.

**bitsadmin /addfile myDownloadJob https://downloadsrv/10mb.zip c:\\10mb.zip**

전송 큐에서 작업을 활성화 하려면 사용 합니다 **/다시 시작** 전환 합니다.

## <a name="activate-the-download-job"></a>다운로드 작업을 활성화

새 작업을 만들 때 BITS 작업을 일시 중단 합니다. 전송 큐에서 작업을 활성화 하려면 사용 합니다 **/다시 시작** 전환 합니다. MyDownloadJob 해당 이름으로 사용 하는 여러 작업을 고유 하 게 작업을 식별 하는 작업의 GUID를 사용 하 여 myDownloadJob 바꾸어야 합니다.

**bitsadmin /resume myDownloadJob**

작업의 진행률을 확인 하려면 사용 합니다 **나열/**, **/info**, 또는 **모니터링/** 전환 합니다.

## <a name="determine-the-progress-of-the-download-job"></a>다운로드 작업의 진행률을 확인

사용 된 **/info** 작업의 진행률을 확인 하는 스위치입니다. MyDownloadJob 해당 이름으로 사용 하는 여러 작업을 고유 하 게 작업을 식별 하는 작업의 GUID를 사용 하 여 myDownloadJob 바꾸어야 합니다.

**bitsadmin /info myDownloadJob /verbose**

합니다 **/info** switch 작업의 상태 및 파일과 전송 된 바이트 수가 반환 합니다. 상태를 전송 하는 경우 BITS가 작업의 모든 파일을 전송 했습니다. 합니다 **/verbose** 인수는 작업의 전체 세부 정보를 제공 합니다. 다음 텍스트는 샘플 출력입니다.

``` syntax
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

전송 큐에 모든 작업에 대 한 정보를 받으려면 사용 하 여는 **/list** 또는 **모니터링/** 전환 합니다.

## <a name="completing-the-download-job"></a>다운로드 작업이 완료

작업의 상태를 전송 하는 경우 BITS가 작업의 모든 파일을 전송 했습니다. 그러나 파일이 사용할 수 없는 사용 하기 전에 **완료 /** 전환 합니다. MyDownloadJob 해당 이름으로 사용 하는 여러 작업을 고유 하 게 작업을 식별 하는 작업의 GUID를 사용 하 여 myDownloadJob 바꾸어야 합니다.

**bitsadmin 완료 myDownloadJob /**

## <a name="monitoring-jobs-in-the-transfer-queue"></a>전송 큐에서 작업을 모니터링

사용 하 여는 **/list**, **모니터링/**, 또는 **/info** 전송 큐에 작업을 모니터링 하는 스위치입니다. 합니다 **/list** 스위치는 큐의 모든 작업에 대 한 정보를 제공 합니다.

**bitsadmin /list**

합니다 **/list** switch 작업의 상태 및 파일과 전송 큐에 모든 작업에 대 한 전송 된 바이트 수가 반환 합니다. 다음 텍스트는 샘플 출력입니다.

``` syntax
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN

Listed 2 job(s).
```

사용 된 **모니터링/** 큐에 있는 모든 작업을 모니터링 하는 스위치입니다. 합니다 **모니터링/** 스위치 5 초 마다 데이터를 새로 고칩니다. 새로 고침을 중지 하려면 CTRL + C를 입력 합니다.

**bitsadmin /monitor**

합니다 **모니터링/** switch 작업의 상태 및 파일과 전송 큐에 모든 작업에 대 한 전송 된 바이트 수가 반환 합니다. 다음 텍스트는 샘플 출력입니다.

``` syntax
MONITORING BACKGROUND COPY MANAGER(5 second refresh)
{6AF46E48-41D3-453F-B7AF-A694BBC823F7} job1 SUSPENDED 0 / 0 0 / 0
{482FCAF0-74BF-469B-8929-5CCD028C9499} job2 TRANSIENT_ERROR 0 / 1 0 / UNKNOWN
{0B138008-304B-4264-B021-FD04455588FF} job3 TRANSFERRED 1 / 1 100379370 / 100379370
```

## <a name="deleting-jobs-from-the-transfer-queue"></a>전송 큐에서 삭제 작업

사용 된 **/다시 설정** 전송 큐에서 모든 작업을 제거 하는 스위치입니다.

**bitsadmin /reset**

다음 텍스트는 샘플 출력입니다.

``` syntax
{DC61A20C-44AB-4768-B175-8000D02545B9} canceled.
{BB6E91F3-6EDA-4BB4-9E01-5C5CBB5411F8} canceled.
2 out of 2 jobs canceled.
```
