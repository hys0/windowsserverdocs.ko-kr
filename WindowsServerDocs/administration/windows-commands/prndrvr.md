---
title: prndrvr
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05e03a4b0b5d686c8fbd1646a775c7f0e5c95706
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372123"
---
# <a name="prndrvr"></a>prndrvr

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

**Prndrvr.vbs** 명령을 사용 하 여 프린터 드라이버를 추가, 삭제 및 나열 합니다.

## <a name="syntax"></a>구문
```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] 
[-e <environment>] [-s <ServerName>] [-u <UserName>] [-w <Password>] 
[-h <path>] [-i <inf file>]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|-------|--------|
|-A|드라이버를 설치합니다.|
|-d|드라이버를 삭제 합니다.|
|-l|**-s** 매개 변수로 지정 된 서버에 설치 된 모든 프린터 드라이버를 나열 합니다. 서버를 지정 하지 않으면 Windows 로컬 컴퓨터에 설치 된 프린터 드라이버를 나열 합니다.|
|-x|**-s** 매개 변수로 지정 된 서버의 논리 프린터에서 사용 하지 않는 모든 프린터 드라이버 및 추가 프린터 드라이버를 삭제 합니다. 목록에서 제거 하려면 서버를 지정 하지 않으면 Windows 로컬 컴퓨터에서 모든 사용 하지 않는 프린터 드라이버를 삭제 합니다.|
|-m \<DrivermodelName @ no__t-1|이름을 사용 하 여 드라이버를 설치 하려면 지정 합니다. 드라이버가 지 원하는 프린터 모델에 대 한 자주 라고 합니다. 자세한 내용은 프린터 설명서를 참조 하십시오.|
|-v {0 &#124; 1 &#124; 2 및 #124; 3을 (를)|설치 하려는 드라이버의 버전을 지정 합니다. 에 대 한 설명을 참조는 **-e**버전은 사용할 수 있는 환경에 대 한 정보에 대 한 매개 변수입니다. 버전을 지정 하지 않으면 버전의 드라이버를 설치 하려는 컴퓨터에서 실행 되는 Windows의 버전에 대 한 적절 한 드라이버 설치 됩니다.<br /><br />-버전 **0** 은 windows 95, windows 98 및 windows Millennium edition을 지원 합니다.<br />-버전 **1** 은 Windows NT 3.51를 지원 합니다.<br />-버전 **2** 는 Windows NT 4.0를 지원 합니다.<br />-버전 **3** 은 windows Vista, windows XP, windows 2000 및 windows Server 2003 운영 체제를 지원 합니다. 이 지 원하는 Windows Vista만 프린터 드라이버 버전 note 합니다.|
|-e \<Environment >|설치 하려는 드라이버에 대 한 환경을 지정 합니다. 환경을 지정 하지 않으면 드라이버를 설치 하려는 컴퓨터의 환경이 사용 됩니다. 지원 되는 환경 매개 변수는.<br /><br />-    **"WINDOWS NT x86"**<br />-    **"Windows x64"**<br />-    **"WINDOWS IA64"**|
|-s \<ServerName >|프린터를 관리 하려면를 호스트 하는 원격 컴퓨터의 이름을 지정 합니다. 컴퓨터를 지정 하지 않으면 로컬 컴퓨터가 사용 됩니다.|
|-u \<UserName >-w \<Password >|프린터를 관리 하려면를 호스트 하는 컴퓨터에 연결할 수 있는 권한이 있는 계정을 지정 합니다. 대상 컴퓨터의 로컬 관리자 그룹의 모든 구성원이 이러한 권한이 있지만 사용 권한을 다른 사용자에 게 부여 될 수도 있습니다. 계정을 지정 하지 않으면, 작동 하려면 명령에 대 한 이러한 사용 권한이 있는 계정으로 로그온 해야 합니다.|
|-h \<path >|드라이버 파일의 경로를 지정합니다. 경로 지정 하지 않으면 Windows가 설치 된 위치 경로를 사용 됩니다.|
|-i \<Filename.inf>|설치 하려는 드라이버에 대 한 전체 경로 파일 이름을 지정 합니다. 파일 이름을 지정 하지 않는 경우 스크립트를 사용 하는 Windows 디렉터리의 inf 하위 디렉터리의 받은 편지함 프린터.inf 파일 중 하나입니다.<br /><br />드라이버 경로를 지정 하지 않으면 스크립트는 드라이버 .cab 파일에서 드라이버 파일을 검색 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명
- **Prndrvr.vbs** 명령은%WINdir%\System32\printing_Admin_Scripts @ no__t-1 @ no__t-2 디렉터리에 있는 Visual Basic 스크립트입니다. 이 명령을 사용 하려면 명령 프롬프트에서 **cscript** 다음에 prndrvr.vbs 파일의 전체 경로를 입력 하거나 디렉터리를 적절 한 폴더로 변경 합니다.

  예를 들어 다음과 같은 가치를 제공해야 합니다.
  ```
  cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr
  ```
- 텍스트가 주위에 따옴표를 사용 하 여 사용자가 제공 하는 정보에 공백이 포함 되 면 (예를 들어 `"computer Name"`).
- -X 옵션 기본 드라이버를 사용 하는 경우에 모든 추가 프린터 드라이버 (드라이버 설치 사용 하기 위해 클라이언트에서 실행 중인 다른 버전의 Windows)를 삭제 합니다. 팩스 구성 요소가 설치 되어 있는 경우이 옵션은 또한 팩스 드라이버 삭제 합니다. 기본 팩스 드라이버가 없는 경우에 (즉, 있는 경우 큐)를 사용 하 여 삭제 됩니다. 기본 팩스 드라이버는 삭제, 팩스를 다시 사용 하도록 설정 하는 유일한 방법은 하는 경우 팩스 구성 요소를 다시 설치 해야 합니다.
- 매개 변수 없이 사용 **prndrvr.vbs** **prndrvr.vbs** 명령에 대 한 명령줄 도움말을 표시 합니다.

## <a name="BKMK_examples"></a>예와

@No__t-0 \ printServer1 서버에 모든 드라이버를 나열 하려면 다음을 입력 합니다.
```
cscript Prndrvr -l -s
```

C:\temp 폴더 유형에 저장 된 드라이버에 대 한 C:\temp\Laserprinter1.inf 드라이버 정보 파일을 사용 하 여 프린터의 "레이저 프린터 모델 1" 모델에 대 한 버전 3 Windows x64 프린터 드라이버를 추가 하려면 다음을 수행 합니다.
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows x64" -i c:\temp\Laserprinter1.inf -h c:\temp
```

"레이저 프린터 모델 1"에 대 한 버전 3 Windows NT x86 프린터 드라이버를 삭제 하려면 다음을 입력 합니다.
```
cscript Prndrvr -a -m "Laser printer model 1" -v 3 -e "Windows NT x86" 
```

#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[인쇄 명령 참조](print-command-reference.md)
