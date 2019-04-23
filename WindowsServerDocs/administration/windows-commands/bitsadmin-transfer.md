---
title: bitsadmin Transfer
description: Windows 명령 항목에 대 한 **bitsadmin 전송** -하나 이상의 파일을 전송 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe302141-b33a-4a05-835e-dc4fc4db7d5a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2ef29a242a834fae42d1de3994a82aedcf87ec2d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852464"
---
# <a name="bitsadmin-transfer"></a>bitsadmin Transfer

하나 이상의 파일을 전송합니다. 둘 이상의 파일을 전송 하려면 여러 개 지정 \<RemoteFileName\>-\<LocalFileName\> 쌍입니다. 쌍은 공백으로 구분 됩니다.

## <a name="syntax"></a>구문

```
bitsadmin /Transfer <Name> [<Type>] [/Priority <Job_Priority>] [/ACLFlags <Flags>] [/DYNAMIC] <RemoteFileName> <LocalFileName>
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|이름|작업의 이름입니다. 대부분의 명령과 달리 **이름을** 이름과 GUID가 아닌 수만 있습니다.|
|형식|선택 사항-작업의 유형을 지정 합니다. 사용 하 여 **다운로드/** (기본값) 다운로드 작업을 위해 또는 **업로드/** 업로드 작업에 대 한 합니다.|
|우선 순위|선택적-job_priority는 다음 값 중 하나로 설정 합니다.</br>-전경</br>-높음</br>-표준</br>-낮음|
|ACLFlags|선택적-다운로드할 파일의 소유자 및 ACL 정보를 유지 하려는 나타냅니다. 예를 들어, 소유자 및 그룹 파일을 유지 하려면 플래그를 설정할 `OG`합니다. 다음 플래그 중 하나 이상 지정 합니다.</br>-   O: 파일 소유자 정보를 복사 합니다.</br>-   G: 파일 그룹 정보를 복사 합니다.</br>-   D: 파일과 함께 DACL 정보를 복사 합니다.</br>-   S: 파일을 사용 하 여 SACL 정보를 복사 합니다.|
|\/DYNAMIC|사용 하 여 작업 구성 [ **BITS_JOB_PROPERTY_DYNAMIC_CONTENT**](/windows/desktop/api/bits5_0/ne-bits5_0-bits_job_property_id), 서버 쪽 요구 사항을 완화 하는 합니다.|
|RemoteFileName|서버에 전송 하는 경우에 파일의 이름입니다.|
|LocalFileName|로컬로 상주 하는 파일의 이름입니다.|

## <a name="remarks"></a>설명

기본적으로 BITSAdmin 서비스에서 실행 되는 다운로드 작업을 만듭니다 **보통** 우선 순위는 중대 한 오류가 발생 하거나 전송이 완료 될 때까지 명령 창 진행률 정보로 업데이트 합니다. 성공적으로 모든 파일을 전송할 때 고 치명적인 오류가 발생 하는 경우 작업을 취소 하는 경우 서비스에서 작업을 완료 합니다. 에 대 한 잘못 된 값을 지정 하는 경우 또는 작업에 파일을 추가할 수 없는 경우는 서비스에서 작업을 생성 하지 *형식* 또는 *Job_Priority*합니다. 둘 이상의 파일을 전송 하려면 여러 개 지정 *RemoteFileName*-*LocalFileName* 쌍입니다. 쌍은 공백으로 구분 됩니다.

> [!NOTE]
> BITSAdmin 명령 일시적인 오류가 발생 하는 경우 실행을 계속 합니다. 이 명령은 종료 하려면 CTRL + C를 누릅니다.

## <a name="BKMK_examples"></a>예제

전송 작업으로 다음 예제에서는 시작 이라는 *myDownloadJob*합니다.
```
C:\>bitsadmin /Transfer myDownloadJob http://prodserver/audio.wma c:\downloads\audio.wma
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)