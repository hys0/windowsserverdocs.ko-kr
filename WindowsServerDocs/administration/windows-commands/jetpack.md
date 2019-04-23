---
title: jetpack
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3bffc29519df139921bdb1de53e67acd558b306
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858014"
---
# <a name="jetpack"></a>jetpack

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Windows 인터넷 이름 서비스 WINS () 또는 동적 호스트 구성 프로토콜 (DHCP) 데이터베이스를 압축합니다. 했다가 가까워지면 30MB 때마다 WINS 데이터베이스를 압축 하는 것이 좋습니다. 

## <a name="syntax"></a>구문
```
jetpack.EXE <database name> <temp database name>
```

### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|<database name>|원본 데이터베이스 파일을 지정합니다.|
|<temp database name>|임시 데이터베이스 파일을 지정합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="BKMK_Examples"></a>예제
WINS 데이터베이스를 압축 합니다.
```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack WINS.MDB TMP.MDB
NET start WINS
```
DHCP 데이터베이스를 압축 합니다.
```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERver
jetpack DHCP.MDB TMP.MDB
NET start DHCPSERver
```
위의 예에서 **Tmp.mdb** jetpack.exe에서 사용 되는 임시 데이터베이스입니다. **Wins.mdb** WINS 데이터베이스입니다. **Dhcp.mdb** DHCP 데이터베이스입니다.
jetpack.exe 압축 WINS 또는 다음을 수행 하 여 DHCP 데이터베이스:
1.  라는 임시 데이터베이스 파일에 대 한 정보를 데이터베이스 복사본 **Tmp.mdb**합니다.
2.  원본 데이터베이스 파일을 삭제 **Wins.mdb** 하거나 **Dhcp.mdb**합니다.
3.  원래 파일 이름에 임시 데이터베이스 파일을 이름을 바꿉니다.

> [!NOTE]
> 압축 프로세스 동안 jetpack.exe가 지정한 이름의 임시 파일을 만듭니다는 *임시 데이터베이스 이름* 매개 변수입니다. 임시 파일에는 compact 프로세스가 완료 되 면 제거 됩니다. WINS 또는 DHCP에 이미 존재 하는 파일이 없는 있는지에 지정 된 것과 동일한 이름의 폴더를 *임시 데이터베이스 이름* 매개 변수입니다.

## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
