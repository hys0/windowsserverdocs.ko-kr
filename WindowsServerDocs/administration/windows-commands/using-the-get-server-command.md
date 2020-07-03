---
title: 서버 가져오기
description: 지정 된 Windows 배포 서비스 서버에서 정보를 검색 하는 get 서버에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bef60db4-d58d-4304-ab4b-be53dd3271c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f035462de8966756e4b47ca6ba04b7d30a9cb1c6
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932180"
---
# <a name="get-server"></a>서버 가져오기

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

지정된 된 Windows 배포 서비스 서버에서 정보를 검색합니다.

## <a name="syntax"></a>구문
```
wdsutil [Options] /Get-Server [/Server:<Server name>] /Show:{Config | Images | All} [/detailed]
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|[/ 서버:<Server name>]|서버 이름을 지정합니다. 이 NetBIOS 이름 또는 정규화 된 도메인 이름 (FQDN) 수 있습니다. 서버 이름을 지정 하지, 로컬 서버가 사용 됩니다.|
|/ 표시: {구성 (& a) #124; 이미지 및 #124; 모든}|반환할 정보의 유형을 지정 합니다.<p>-   **Config** 구성 정보를 반환 합니다.<br />-   **이미지는** 이미지 그룹, 부팅 이미지 및 설치 이미지에 대 한 정보를 반환 합니다.<br />-   **모든** 구성 정보 및 이미지 정보를 반환 합니다.|
|자세한/|이 옵션을 사용할 수 있습니다 **/Show:Images** 또는 **/Show:All** 각 이미지에서 모든 이미지 메타 데이터 반환 되어야 함을 나타냅니다. **자세한/** 옵션을 사용 하지 않는 경우 기본 동작은 이미지 이름, 설명 및 파일 이름을 반환 하는 것입니다.|
## <a name="examples"></a>예
서버에 대 한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /Get-Server /Show:Config
```
서버에 대 한 자세한 정보를 보려면 다음을 입력 합니다.
```
wdsutil /verbose /Get-Server /Server:MyWDSServer /Show:All /detailed
```
## <a name="additional-references"></a>추가 참조
- [명령줄 구문 키](command-line-syntax-key.md) 
 [Disable Server 명령 사용](using-the-disable-server-command.md) 
 [Enable-Server 명령 사용](using-the-enable-server-command.md) 
 [Initialize 서버 명령을](using-the-initialize-server-command.md) 
 사용 하 여 [하위 명령: 설정-서버](subcommand-set-server.md) 
 [하위 명령: 시작-서버](subcommand-start-server.md) 
 [하위 명령: 중지 서버](subcommand-stop-server.md) 
 [초기화 서버 옵션](the-uninitialize-server-option.md)
