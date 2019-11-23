---
title: Scwcmd 레지스터
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe4d126a-9f27-4076-b7b1-fbefa45f378a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e892f7c08461e88d12a072dfb171f9523558ef7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371219"
---
# <a name="scwcmd-register"></a>Scwcmd: register

> 적용 대상: Windows Server 2012 R2, Windows Server 2012

확장 또는 사용자 역할, 작업, 서비스 또는 포트 정의 포함 하는 보안 구성 데이터베이스 파일을 등록 하 여 구성 마법사 SCW (보안) 보안 구성 데이터베이스를 지정 합니다.

## <a name="syntax"></a>구문

```
scwcmd register /kbname:<MyApp> [/kbfile:<kb.xml>] [/kb:<path>] [/d]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/kbname:\<MyApp >|보안 구성 데이터베이스 확장이 등록 이름을 지정 합니다. 이 매개 변수를 지정 합니다.|
|/kbfile:\<Kb .xml >|확장 하거나 기본 보안 구성 데이터베이스를 사용자 지정 하는 데 사용 될 보안 구성 데이터베이스 파일의 경로 파일 이름을 지정 합니다. 보안 구성 데이터베이스 파일이 SCW 스키마와 호환 된다는 유효성을 검사 하려면 %windir%\security\KBRegistrationInfo.xsd 스키마 정의 파일을 사용 합니다. 경우가 아니면이 옵션을 제공 해야는 **/d** 매개 변수를 지정 합니다.|
|/kb:\<경로 >|업데이트할 SCW 보안 구성 데이터베이스 파일이 있는 디렉터리의 경로를 지정 합니다. 이 옵션을 지정 하지 않으면 %windir%\security\msscw\kbs 사용 됩니다.|
|/d|보안 구성 데이터베이스에서 보안 구성 데이터베이스 확장 등록을 취소합니다. 등록을 취소할 확장은 /kbname 매개 변수로 지정 됩니다. ( **/Kbfile** 매개 변수는 지정 하지 않아야 합니다.) 확장을 등록 취소할 보안 구성 데이터베이스는 **/kb** 매개 변수로 지정 됩니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Scwcmd.exe은 Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 컴퓨터에서 사용할 수만 있습니다.

## <a name="BKMK_Examples"></a>예와

\\\\kbserver\kb에 있는 이름 MyApp 아래에 SCWKBForMyApp .xml 이라는 보안 구성 데이터베이스 파일을 등록 하려면 다음을 입력 합니다.
```
scwcmd register /kbfile:d:\SCWKBForMyApp.xml /kbname:MyApp /kb:\\kbserver\kb
```
\\\\kbserver\kb에 있는 보안 구성 데이터베이스 MyApp의 등록을 취소 하려면 다음을 입력 합니다.
```
scwcmd register /d /kbname:MyApp /kb:\\kbserver\kb
```

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)