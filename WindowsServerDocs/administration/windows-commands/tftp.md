---
title: tftp
description: 원격 컴퓨터에서 파일을 전송 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 772f19a8-dafe-45cd-878a-f5691f6568ef vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad195409076840fda0e8d6bf5cd0c295a62cdede
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845904"
---
# <a name="tftp"></a>tftp

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

원격 컴퓨터에서 파일을 전송 하 Trivial File Transfer Protocol (tftp) 서비스 또는 데몬 실행 하는 UNIX를 실행 하는 컴퓨터를 일반적으로 합니다. tftp는 일반적으로 포함 된 장치 또는 tftp 서버에서 부팅 프로세스 중 펌웨어, 구성 정보 또는 시스템 이미지를 검색 하는 시스템에서 사용 됩니다.   

## <a name="syntax"></a>구문  
```  
tftp [-i] [<Host>] [{get | put}] <Source> [<Destination>]  
```  

### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|-i|이진 이미지 전송 모드 (octet 모드 라고도 함)를 지정 합니다. 이진 이미지 모드에서 1 바이트 단위로 파일 전송 됩니다. 이진 파일을 전송 하는 경우이 모드를 사용 합니다. 경우 **-i** 는 생략 하면 파일이 ASCII 모드로 전송 합니다. 이 기본 전송 모드입니다. 이 모드는 줄의 끝 (EOL) 문자가 지정된 된 컴퓨터에 대 한 적절 한 형식으로 변환합니다. 텍스트 파일을 전송할 때이 모드를 사용 합니다. 파일 전송에 성공한 경우에 데이터 전송 속도가 표시 됩니다.|  
|\<Host\>|로컬 또는 원격 컴퓨터를 지정합니다.|  
|배치|파일 전송 *소스* 파일을 로컬 컴퓨터에 *대상* 원격 컴퓨터에 있습니다. Tftp 프로토콜 사용자 인증을 지원 하지 않으므로, 사용자는 원격 컴퓨터에 로그온 해야 하 고 파일을 원격 컴퓨터의 쓰기 가능 해야 합니다.|  
|get|파일 전송 *대상* 파일을 원격 컴퓨터에서 *소스* 로컬 컴퓨터에 있습니다.|  
|\<원본\>|전송할 파일을 지정 합니다.|  
|\<대상\>|파일 전송 위치를 지정 합니다.|  

## <a name="remarks"></a>설명  
-   추가 기능 마법사를 사용 하는 tftp 클라이언트를 설치할 수 있습니다.  
-   Tftp 프로토콜 인증 또는 암호화 메커니즘을 지원 하지 않으며 따라서 있는 경우 보안 위험이 발생할 수 있습니다. Tftp 클라이언트를 설치 합니다. 인터넷에 연결 하는 시스템에 대 한 권장 되지 않습니다.  
-   Tftp 클라이언트 선택적 소프트웨어 이며 Windows Vista 및 이후 버전의 Windows 운영 체제에서 사용 되지 않는 것으로 표시 합니다. Tftp 서버 서비스는 보안상의 이유로 더 이상 Microsoft에서 제공 됩니다.  

## <a name="BKMK_Examples"></a>예제  
파일 복사 **boot.img** 원격 컴퓨터에서 **Host1**합니다.  
```  
tftp  -i Host1 get boot.img  
```  

## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
