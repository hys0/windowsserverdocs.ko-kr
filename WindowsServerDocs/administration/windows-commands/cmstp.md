---
title: cmstp
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 34aad544-11c3-4e85-8bbf-5bc5a971da93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fd2e8dbb08b41875335b35dd802007a0bd1fbd41
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379273"
---
# <a name="cmstp"></a>cmstp

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

설치 하거나 연결 관리자 서비스 프로필을 제거 합니다. 선택적 매개 변수 없이 사용 **cmstp** 사용자의 사용 권한을 클릭 하 여 운영 체제에 적합 한 기본 설정으로 서비스 프로필을 설치 합니다. 
## <a name="syntax"></a>구문
구문 1:
```
ServiceProfileFileName .exe /q:a /c:"cmstp.exe ServiceProfileFileName .inf [/nf] [/ni] [/ns] [/s] [/su] [/u]"
```
구문 2:
```
cmstp.exe [/nf] [/ni] [/ns] [/s] [/su] [/u]  [Drive:][path]ServiceProfileFileName.inf"
```
### <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|< ServiceProfileFileName >.exe|설치 하려는 프로필을 포함 하는 설치 패키지 이름으로 지정 합니다.<br /><br />구문 2에 대 한 구문 1에 있지만 유효 하지 않은 필요합니다.|
|/q:는|프로필이 사용자에 게 확인 하지 않고 설치 수를 지정 합니다. 성공적으로 설치 하는 확인 메시지가 표시 됩니다.<br /><br />구문 2에 대 한 구문 1에 있지만 유효 하지 않은 필요합니다.|
|[드라이브:] [path] @no__t 64,|필수. 프로필을 설치 해야 하는 방법을 결정 하는 구성 파일의 이름을 지정 합니다.<br /><br />[Drive:] [path] 매개 변수는 구문 1에 사용할 수 없습니다.|
|/nf|지원 파일을 설치 하지 않도록 지정 합니다.|
|/ni|바탕 화면 아이콘을 생성 되지 않도록 지정 합니다. 이 매개 변수는 Windows 95, Windows 98, Windows NT 4.0 또는 Windows Millennium edition을 실행 하는 컴퓨터에만 유효 합니다.|
|/ns|바탕 화면 바로 가기를 만들지 않도록 지정 합니다. 이 매개 변수는 Windows Server 2003 제품군, Windows 2000 또는 Windows XP의 멤버를 실행 하는 컴퓨터에만 유효 합니다.|
|/s|서비스 프로필을 설치 또는 자동으로 (사용자 응답에 대 한 메시지를 표시 하거나 표시 하지 않고 확인 메시지) 제거를 지정 합니다.|
|/su|모든 사용자가 아닌 단일 사용자에 대 한 서비스 프로필 설치할 수 있도록 지정 합니다. 이 매개 변수는 Windows Server 2003, Windows 2000 또는 Windows XP를 실행 하는 컴퓨터에만 유효 합니다.|
|/au|모든 사용자에 대 한 서비스 프로필이 설치 수를 지정 합니다. 이 매개 변수 Windows Server 2003, Windows 2000 또는 Windows XP를 실행 하는 컴퓨터에만 유효 합니다.|
|/u|서비스 프로필을 제거 해야 하는 것을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="remarks"></a>설명
**/s** 와 함께에서 사용할 수 있는 유일한 매개 변수는 **/u**합니다.
구문 1은 사용자 지정 설치 응용 프로그램에서 사용 되는 일반적인 구문. 다음이 구문을 사용 하려면 실행 해야 **cmstp** 포함 된 디렉터리에서는 <ServiceProfileFileName>.exe 파일입니다.
## <a name="BKMK_Examples"></a>예와
지원 파일 없이 Fiction 서비스 프로필을 설치 하려면 다음을 입력 합니다.
```
fiction.exe /c:"cmstp.exe fiction.inf /nf"
```
단일 사용자를 위한 Fiction 서비스 프로필을 자동으로 설치 하려면 다음을 입력 합니다.
```
fiction.exe /c:"cmstp.exe fiction.inf /s /su"
```
Fiction 서비스 프로필을 자동으로 제거 하려면 다음을 입력 합니다.
```
fiction.exe /c:"cmstp.exe fiction.inf /s /u"
```
## <a name="additional-references"></a>추가 참조
-   [명령줄 구문 키](command-line-syntax-key.md)
