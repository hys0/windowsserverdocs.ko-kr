---
title: mqbkup
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bdd41c4-75ef-455f-b241-1d64a4c7acf5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a809bfc788ba25afab280e80e5c6f0dc9c70dc86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842904"
---
# <a name="mqbkup"></a>mqbkup

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

저장 장치 설정을 MSMQ 메시지 파일 및 레지스트리를 백업 하 고 이전에 저장 된 메시지 및 설정을 복원 합니다.   
백업 및 복원 작업을 모두 로컬 MSMQ 서비스를 중지 합니다. MSMQ 서비스가 이미 시작 된 경우이 유틸리티는 백업 또는 복원 작업의 끝에 MSMQ 서비스를 다시 시작 하려고 합니다. 이 유틸리티를 실행 하기 전에 서비스가 이미 중지 된 서비스를 다시 시작 하려고 하지 이루어집니다.  
MSMQ 메시지 백업/복원 유틸리티를 사용 하기 전에 MSMQ를 사용 하는 모든 로컬 응용 프로그램을 닫아야 합니다.  
## <a name="syntax"></a>구문  
```  
mqbkup {/b | /r} <folder path_to_storage_device>  
```  
### <a name="parameters"></a>매개 변수  
|매개 변수|설명|  
|-------|--------|  
|/b|백업 작업을 지정합니다.|  
|/r|복원 작업을 지정합니다.|  
|< 폴더 path_to_storage\_장치 >|MSMQ 메시지 파일 및 레지스트리 설정이 저장 되는 경로 지정 합니다.|  
|/?|명령 프롬프트에 도움말을 표시합니다.|  
## <a name="BKMK_Examples"></a>예제  
모든 MSMQ 메시지 파일 및 레지스트리 설정을 백업에 저장 하는 *Msmqbkup* c: 드라이브의 폴더에 있습니다.  
```  
mqbkup /b c:\msmqbkup  
```  
지정한 폴더가 없으면 유틸리티 자동으로 만들어집니다. 기존 폴더를 지정 하려는 경우이 폴더는 비어 있어야 합니다. 비어 있지 않은 폴더를 지정 하는 경우 모든 파일 및 하위 폴더 내에 포함 된 유틸리티 삭제 됩니다. 이 경우 기존 파일 및 하위 폴더를 삭제할 수 있는 권한을 부여 하 라는 메시지가 됩니다. 사용할 수는 **/y** 모든 기존 파일 및 지정된 된 폴더에 하위 삭제에 미리 동의 함을 나타내는 매개 변수를 합니다.  
모든 파일 및 하위 폴더에서 삭제 하는 *Oldbkup* 폴더에 c: 드라이브와 저장소 MSMQ 메시지 파일 및 레지스트리 설정을이 폴더에 있습니다.  
```  
mqbkup /b /y c:\oldbkup  
```  
MSMQ 메시지 및 레지스트리 설정을 복원 합니다.  
```  
mqbkup /r c:\msmqbkup  
```  
MSMQ 메시지 파일을 저장 하는 데 사용 되는 폴더의 위치는 레지스트리에 저장 됩니다. 따라서이 유틸리티는 복원 작업 전에 사용 되는 저장소 폴더 아니라는 레지스트리에 지정 된 폴더에 MSMQ 메시지 파일 복원 됩니다. 레지스트리에 지정 된 폴더가 존재 하지 않는 경우 복원 작업이 자동으로 만들어집니다 해당 합니다. 폴더 디렉터리 없는 비어 있지 않은 경우 이러한 폴더의 현재 내용을 삭제 하는 권한을 유틸리티가 묻습니다.  
## <a name="additional-references"></a>추가 참조  
-   [명령줄 구문 키](command-line-syntax-key.md)  
