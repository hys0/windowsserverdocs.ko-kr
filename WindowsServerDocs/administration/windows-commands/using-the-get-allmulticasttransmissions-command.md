---
title: Get AllMulticastTransmissions 명령을 사용 하 여
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8fb79-7a8a-4f0c-88f4-92bc1111c67f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b05f8802a288d80960cf79356675cb9adce9c260
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440528"
---
# <a name="using-the-get-allmulticasttransmissions-command"></a>Get AllMulticastTransmissions 명령을 사용 하 여

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

서버에서 모든 멀티 캐스트 전송에 대 한 정보를 표시합니다.
## <a name="syntax"></a>구문
for Windows Server 2008:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:Clients] [/ExcludedeletePending]
```
Windows Server 2008 r2:
```
wdsutil /Get-AllMulticastTransmissions [/Server:<Server name>] [/Show:{Boot | Install | All}] [/details:Clients]  [/ExcludedeletePending]
```
## <a name="parameters"></a>매개 변수

|        매개 변수        |                                                                                                                                                                                                                                                                   설명                                                                                                                                                                                                                                                                    |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/ 서버:<Server name>] |                                                                                                                                                                                 서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름이 없는 지정 하는 경우 로컬 서버 사용 됩니다.                                                                                                                                                                                  |
|         [/Show]         | **Windows Server 2008**<br /><br />/Show:Clients-멀티 캐스트 전송에 연결 된 클라이언트 컴퓨터에 대 한 정보를 표시 합니다.<br /><br />**Windows Server 2008 R2**<br /><br />Show: {부팅 & #124; 설치 및 #124; 모든}-반환할 이미지의 형식입니다.                                **부팅** 부팅 이미지 전송을 반환 합니다.                                  **설치** 반환 이미지 전송에만 설치 합니다. **모든** 이미지 형식 모두 반환 합니다. |
|                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|    /details:clients     |                                                                                                                                                                                              Windows Server 2008 r 2 에서만 지원 됩니다. 있는 경우에 전송에 연결 된 클라이언트가 표시 됩니다.                                                                                                                                                                                               |
| [/ExcludedeletePending] |                                                                                                                                                                                                                                              비활성화 된 모든 전송 목록에서 제외 됩니다.                                                                                                                                                                                                                                               |

## <a name="BKMK_examples"></a>예제
모든 전송에 대 한 정보를 보려면 다음을 입력 합니다.
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Show:All` 비활성화 된 전송 제외한 모든 전송에 대 한 정보를 보려면 다음을 입력 합니다.
- Windows Server 2008: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:Clients /ExcludedeletePending`
- Windows Server 2008 R2: `wdsutil /Get-AllMulticastTransmissions /Server:MyWDSServer /Show:All /details:Clients /ExcludedeletePending`
  #### <a name="additional-references"></a>추가 참조
  [명령줄 구문 키](command-line-syntax-key.md)
  [get MulticastTransmission 명령을 사용 하 여](using-the-get-multicasttransmission-command.md)
  [MulticastTransmission 새 명령을 사용 하 여](using-the-new-multicasttransmission-command.md)
  [제거 MulticastTransmission 명령을 사용 하 여](using-the-remove-multicasttransmission-command.md)
  [하위 명령: MulticastTransmission 시작](subcommand-start-multicasttransmission.md)
