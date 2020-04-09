---
title: jetpack
description: '\* * * *에 대 한 Windows 명령 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82a2b7ef-0db5-4575-a028-8acb0bf6c7ba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 008e9dd4d41fe270d775b1c44d799dd16429046f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841976"
---
# <a name="jetpack"></a>jetpack

>적용 대상: Windows Server(반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

WINS (Windows Internet Name Service) 또는 DHCP (Dynamic Host Configuration Protocol) 데이터베이스를 압축 합니다. 30 MB에 도달할 때까지 WINS 데이터베이스를 압축 하는 것이 좋습니다. 

## <a name="syntax"></a>구문
```
jetpack.EXE <database name> <temp database name>
```

#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|<database name>|원본 데이터베이스 파일을 지정 합니다.|
|<temp database name>|임시 데이터베이스 파일을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="examples"></a><a name=BKMK_Examples></a>예와
WINS 데이터베이스를 압축 하려면:
```
cd %SYSTEMROOT%\SYSTEM32\WINS
NET STOP WINS
jetpack WINS.MDB TMP.MDB
NET start WINS
```
DHCP 데이터베이스를 압축 하려면:
```
cd %SYSTEMROOT%\SYSTEM32\DHCP
NET STOP DHCPSERver
jetpack DHCP.MDB TMP.MDB
NET start DHCPSERver
```
위의 예에서 **.tmp** 는 jetpack에서 사용 하는 임시 데이터베이스입니다. **Wins-r은 wins** 데이터베이스입니다. Dhcp 데이터베이스 **는 dhcp 데이터베이스** 입니다.
jetpack는 다음을 수행 하 여 WINS 또는 DHCP 데이터베이스를 압축 합니다.
1.  데이터베이스 정보를 **.tmp**라는 임시 데이터베이스 파일에 복사 합니다.
2.  원본 데이터베이스 파일 ( **wins-a** 또는 **Dhcp .mdb**)을 삭제 합니다.
3.  임시 데이터베이스 파일의 이름을 원래 파일 이름으로 바꿉니다.

> [!NOTE]
> 압축 프로세스 중 jetpack는 임시 *데이터베이스 이름* 매개 변수로 지정 된 이름으로 임시 파일을 만듭니다. 압축 프로세스가 완료 되 면 임시 파일이 제거 됩니다. *Temp 데이터베이스 이름* 매개 변수에 지정 된 것과 이름이 같은 WINS 또는 DHCP 폴더에 이미 존재 하는 파일이 없는지 확인 합니다.

## <a name="additional-references"></a>추가 참조
-   - [명령줄 구문 키](command-line-syntax-key.md)
