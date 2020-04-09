---
title: bitsadmin Transfer
description: 하나 이상의 파일을 전송 하는 bitsadmin Transfer에 대 한 Windows 명령 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4e960b4d94416d57e6c42ec27057dafef5e44516
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849006"
---
# <a name="bitsadmin-transfer"></a>bitsadmin Transfer

하나 이상의 파일을 전송합니다. 둘 이상의 파일을 전송 하려면 여러 개 지정 \<RemoteFileName\>-\<LocalFileName\> 쌍입니다. 쌍은 공백으로 구분 됩니다.

## <a name="syntax"></a>구문

```
bitsadmin /Transfer <Name> [<Type>] [/Priority <Job_Priority>] [/ACLFlags <Flags>] [/DYNAMIC] <RemoteFileName> <LocalFileName>
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|이름|작업의 이름입니다. 대부분의 명령과 달리 **name** 은 GUID가 아닌 이름만 될 수 있습니다.|
|형식|선택 사항-작업의 유형을 지정 합니다. 다운로드 작업의 경우에는 **/prodownload** (기본값)를 사용 하 고 업로드 작업에는 **/UPLOAD** 를 사용 합니다.|
|Priority|선택 사항-job_priority을 다음 값 중 하나로 설정 합니다.</br>-전경</br>-높음</br>-표준</br>-낮음|
|ACLFlags|선택 사항-다운로드 하는 파일을 사용 하 여 소유자 및 ACL 정보를 유지 하려고 함을 나타냅니다. 예를 들어 파일을 사용 하 여 소유자와 그룹을 유지 하려면 플래그를 `OG`설정 합니다. 다음 플래그 중 하나 이상 지정 합니다.</br>-O: 파일 소유자 정보를 복사 합니다.</br>-G: 파일 그룹 정보를 복사 합니다.</br>-D: 복사할 파일을 사용 하 여 DACL 정보입니다.</br>-S: 복사할 파일을 사용 하 여 SACL 정보입니다.|
|/DYNAMIC|서버 쪽 요구 사항을 완화 하는 [**BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](/windows/desktop/api/bits5_0/ne-bits5_0-bits_job_property_id)작업을 구성 합니다.|
|RemoteFileName|서버에 전송 되는 파일의 이름입니다.|
|LocalFileName|로컬로 상주 하는 파일의 이름입니다.|

## <a name="remarks"></a>주의

기본적으로 BITSAdmin 서비스에서 실행 되는 다운로드 작업을 만듭니다 **보통** 우선 순위는 중대 한 오류가 발생 하거나 전송이 완료 될 때까지 명령 창 진행률 정보로 업데이트 합니다. 성공적으로 모든 파일을 전송할 때 고 치명적인 오류가 발생 하는 경우 작업을 취소 하는 경우 서비스에서 작업을 완료 합니다. 에 대 한 잘못 된 값을 지정 하는 경우 또는 작업에 파일을 추가할 수 없는 경우는 서비스에서 작업을 생성 하지 *형식* 또는 *Job_Priority*합니다. 둘 이상의 파일을 전송 하려면 여러 개 지정 *RemoteFileName*-*LocalFileName* 쌍입니다. 쌍은 공백으로 구분 됩니다.

> [!NOTE]
> BITSAdmin 명령 일시적인 오류가 발생 하는 경우 실행을 계속 합니다. 이 명령은 종료 하려면 CTRL + C를 누릅니다.

## <a name="examples"></a><a name=BKMK_examples></a>예와

전송 작업으로 다음 예제에서는 시작 이라는 *myDownloadJob*합니다.
```
C:\>bitsadmin /Transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)