---
title: bitsadmin transfer
description: 하나 이상의 파일을 전송 하는 bitsadmin transfer 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 57de6db53433d0da1a4efd8c212a23183edcbcf9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927425"
---
# <a name="bitsadmin-transfer"></a>bitsadmin transfer

하나 이상의 파일을 전송합니다. 기본적으로 BITSAdmin 서비스는 **정상적** 으로 실행 되는 다운로드 작업을 만들고, 전송이 완료 되거나 오류가 발생할 때까지 진행 정보를 사용 하 여 명령 창을 업데이트 합니다.

성공적으로 모든 파일을 전송할 때 고 치명적인 오류가 발생 하는 경우 작업을 취소 하는 경우 서비스에서 작업을 완료 합니다. 작업에 파일을 추가할 수 없거나 *유형* 또는 *job_priority*에 대해 잘못 된 값을 지정 하는 경우 서비스에서 작업을 만들지 않습니다. 둘 이상의 파일을 전송 하려면 여러 쌍을 지정 `<RemoteFileName>-<LocalFileName>` 합니다. 쌍은 공백으로 구분 되어야 합니다.

> [!NOTE]
> BITSAdmin 명령 일시적인 오류가 발생 하는 경우 실행을 계속 합니다. 이 명령은 종료 하려면 CTRL + C를 누릅니다.

## <a name="syntax"></a>구문

```
bitsadmin /transfer <name> [<type>] [/priority <job_priority>] [/ACLflags <flags>] [/DYNAMIC] <remotefilename> <localfilename>
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| --------- | ----------- |
| name | 작업의 이름입니다. 이 명령은 GUID 일 수 없습니다. |
| 형식 | 선택 사항입니다. 다음을 포함 하 여 작업의 유형을 설정 합니다.<ul><li>**다운로드할지.** 기본값입니다. 다운로드 작업에 대해이 형식을 선택 합니다.</li><li>**업로드할.** 업로드 작업에 대해이 형식을 선택 합니다.</li></ul> |
| priority | 선택 사항입니다. 다음을 포함 하 여 작업의 우선 순위를 설정 합니다.<ul><li>FOREGROUND</li><li>HIGH</li><li>NORMAL</li><li>LOW</li></ul> |
| ACLflags | 선택 사항입니다. 다운로드 하는 파일을 사용 하 여 소유자 및 ACL 정보를 유지 관리 함을 나타냅니다. 다음을 포함 하 여 하나 이상의 값을 지정 합니다.<ul><li>**o** -파일을 사용 하 여 소유자 정보를 복사 합니다.</li><li>**g** -파일을 사용 하 여 그룹 정보를 복사 합니다.</li><li>**d** -파일을 사용 하 여 DACL (임의 액세스 제어 목록) 정보를 복사 합니다.</li><li>**s** -파일이 포함 된 SACL (시스템 액세스 제어 목록) 정보를 복사 합니다.</li></ul> |
| /DYNAMIC | 서버 쪽 요구 사항을 완화 하는 [**BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](https://docs.microsoft.com/windows/win32/api/bits5_0/ne-bits5_0-bits_job_property_id)을 사용 하 여 작업을 구성 합니다. |
| remotefilename | 서버에 전송 된 후의 파일 이름입니다. |
| localfilename | 로컬로 상주 하는 파일의 이름입니다. |

## <a name="examples"></a>예

*Mydownloadjob*이라는 전송 작업을 시작 하려면 다음을 수행 합니다.

```
bitsadmin /transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [bitsadmin 명령](bitsadmin.md)
