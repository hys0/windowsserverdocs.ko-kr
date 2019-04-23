---
title: systeminfo
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39954968-3c2e-4d3e-9d89-c9c43347461e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d08d3f86bdbd176aa4de157f58a58c9ea418470
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841504"
---
# <a name="systeminfo"></a>systeminfo



자세한 컴퓨터 및 운영 체제 구성, 보안 정보, 제품 ID 및 하드웨어 속성 (예: RAM, 디스크 공간 및 네트워크 카드)를 포함 하 여 해당 운영 체제에 대 한 구성 정보를 표시 합니다.

이 명령을 사용하는 방법의 예는 [예](#BKMK_examples)를 참조하세요.

## <a name="syntax"></a>구문

```
Systeminfo [/s <Computer> [/u <Domain>\<UserName> [/p <Password>]]] [/fo {TABLE | LIST | CSV}] [/nh]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/s \<컴퓨터 >|이름 또는 원격 컴퓨터의 IP 주소를 지정 합니다 (백슬래시를 사용 하지 않습니다). 기본값은 로컬 컴퓨터입니다.|
|/u \<Domain>\<UserName>|지정 된 사용자 계정의 계정 권한으로 명령을 실행 합니다. 경우 **/u** 를 지정 하지 않으면이 명령은 명령을 실행 하는 컴퓨터에 현재 로그온 된 사용자의 사용 권한을 사용 합니다.|
|/p \<Password>|에 지정 된 사용자 계정의 암호를 지정 된 **/u** 매개 변수입니다.|
|/fo \<형식 >|다음 값 중 하 나와 함께 출력 형식을 지정 합니다.</br>테이블: 테이블에 출력을 표시 합니다.</br>목록: 출력을 목록으로 표시 합니다.</br>CSV: 쉼표로 구분 된 값의 출력을 표시 합니다.|
|/nh|출력에서 열 머리글을 표시 하지 않습니다. 유효한 경우에는 **/fo** 매개 변수는 테이블 또는 CSV로 설정 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_examples"></a>예제

Srvmain 라는 컴퓨터에 대 한 구성 정보를 보려면 다음을 입력 합니다.

**systeminfo /s srvmain**

Maindom 도메인에 있는 Srvmain2 라는 컴퓨터에 대 한 구성 정보를 원격으로 보려면 다음을 입력 합니다.

**systeminfo /s srvmain2 /u maindom\hiropln**

Maindom 도메인에 있는 Srvmain2 라는 컴퓨터에 대 한 형식으로 나타낸 목록 구성 정보를 원격으로 보려면 다음을 입력 합니다.

**systeminfo /s srvmain2 /u maindom\hiropln /p p@ssW23 /fo list**

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)