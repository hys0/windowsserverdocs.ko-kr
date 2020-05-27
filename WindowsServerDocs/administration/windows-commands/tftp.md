---
title: tftp
description: 원격 컴퓨터와 파일을 전송 합니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 772f19a8-dafe-45cd-878a-f5691f6568ef vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb9977d0bc4f45b610d8bf3409c6beeadfaf7ee5
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821023"
---
# <a name="tftp"></a>tftp

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

는 tftp (Trivial 파일 전송 프로토콜) 서비스 또는 데몬을 실행 하는 원격 컴퓨터 (일반적으로 UNIX를 실행 하는 컴퓨터)에서 파일을 전송 합니다. tftp는 tftp 서버에서 부팅 프로세스 중 펌웨어, 구성 정보 또는 시스템 이미지를 검색 하는 임베디드 장치 또는 시스템에서 일반적으로 사용 됩니다.

## <a name="syntax"></a>구문
```
tftp [-i] [<Host>] [{get | put}] <Source> [<Destination>]
```

#### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|-i|이진 이미지 전송 모드 (octet 모드 라고도 함)를 지정 합니다. 이진 이미지 모드에서 1 바이트 단위로 파일 전송 됩니다. 이진 파일을 전송 하는 경우이 모드를 사용 합니다. 경우 **-i** 는 생략 하면 파일이 ASCII 모드로 전송 합니다. 이 기본 전송 모드입니다. 이 모드는 줄의 끝 (EOL) 문자가 지정된 된 컴퓨터에 대 한 적절 한 형식으로 변환합니다. 텍스트 파일을 전송할 때이 모드를 사용 합니다. 파일 전송에 성공한 경우에 데이터 전송 속도가 표시 됩니다.|
|\<Host\>|로컬 또는 원격 컴퓨터를 지정합니다.|
|put|파일 전송 *소스* 파일을 로컬 컴퓨터에 *대상* 원격 컴퓨터에 있습니다. Tftp 프로토콜은 사용자 인증을 지원 하지 않으므로 사용자는 원격 컴퓨터에 로그온 해야 하며 파일은 원격 컴퓨터에서 쓸 수 있어야 합니다.|
|Get|파일 전송 *대상* 파일을 원격 컴퓨터에서 *소스* 로컬 컴퓨터에 있습니다.|
|\<원본\>|전송할 파일을 지정 합니다.|
|\<대상\>|파일 전송 위치를 지정 합니다.|

## <a name="remarks"></a>설명
-   기능 추가 마법사를 사용 하 여 tftp 클라이언트를 설치할 수 있습니다.
-   Tftp 프로토콜은 인증 또는 암호화 메커니즘을 지원 하지 않으며,이로 인해 보안 위험이 발생할 수 있습니다. 인터넷에 연결 된 시스템에는 tftp 클라이언트를 설치 하지 않는 것이 좋습니다.
-   Tftp 클라이언트는 선택적 소프트웨어 이며 Windows Vista 이상 버전의 Windows 운영 체제에서 사용 되지 않는 것으로 표시 됩니다. Microsoft에서는 보안상의 이유로 tftp 서버 서비스를 더 이상 제공 하지 않습니다.

## <a name="examples"></a>예
파일 복사 **boot.img** 원격 컴퓨터에서 **Host1**합니다.
```
tftp  -i Host1 get boot.img
```

## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md)
