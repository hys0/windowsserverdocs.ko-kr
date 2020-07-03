---
title: systeminfo
description: '운영 체제 구성, 보안 정보, 제품 ID 및 하드웨어 속성 (예: RAM, 디스크 공간 및 네트워크 카드)을 포함 하 여 컴퓨터와 해당 운영 체제에 대 한 자세한 구성 정보를 표시 하는 systeminfo에 대 한 참조 문서입니다.'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 670fdb94a2ccb10476faccab8f265a5e4db060dd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932577"
---
# <a name="systeminfo"></a>systeminfo

자세한 컴퓨터 및 운영 체제 구성, 보안 정보, 제품 ID 및 하드웨어 속성 (예: RAM, 디스크 공간 및 네트워크 카드)를 포함 하 여 해당 운영 체제에 대 한 구성 정보를 표시 합니다.



## <a name="syntax"></a>구문

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/s\<Computer>|이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.|
|/u\<Domain>\<UserName>|지정 된 사용자 계정의 계정 권한으로 명령을 실행 합니다. 경우 **/u** 를 지정 하지 않으면이 명령은 명령을 실행 하는 컴퓨터에 현재 로그온 된 사용자의 사용 권한을 사용 합니다.|
|/p\<Password>|에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.|
|/fo\<Format>|다음 값 중 하 나와 함께 출력 형식을 지정 합니다.</br>테이블: 테이블에 출력을 표시합니다.</br>목록: 목록에 출력을 표시합니다.</br>CSV: 쉼표로 구분 된 값의 출력을 표시합니다.|
|/nh|출력에서 열 머리글을 표시 하지 않습니다. 유효한 경우에는 **/fo** 매개 변수는 테이블 또는 CSV로 설정 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a>예

Srvmain 이라는 컴퓨터에 대 한 구성 정보를 보려면 다음을 입력 합니다.

**systeminfo/s srvmain**

Maindom 도메인에 있는 Srvmain2 이라는 컴퓨터에 대 한 구성 정보를 원격으로 보려면 다음을 입력 합니다.

**systeminfo/s srvmain2/u maindom\hiropln**

Maindom 도메인에 있는 Srvmain2 이라는 컴퓨터에 대 한 구성 정보를 목록 형식으로 원격으로 보려면 다음을 입력 합니다.

**systeminfo/s srvmain2/u maindom\hiropln/p p@ssW23 /fo list**

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)