---
title: Scwcmd 변환
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 640dd892-0bb9-416d-8318-60a26605bcf4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 86c88f0207a53da813f5d4eaed399375bfc5bc02
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820953"
---
# <a name="scwcmd-transform"></a>Scwcmd: 변환

> 적용 대상: Windows Server 2012 R2, Windows Server 2012

에 새 개체 GPO (그룹 정책)에서 Active Directory 도메인 서비스 (SCW (보안 구성 마법사)를 사용 하 여 생성 되는 보안 정책 파일을 변환 합니다. 변환 작업을 수행 하는 서버에서 설정을 변경 되지 않습니다. 변환 작업이 완료 된 후 관리자가 서버에 정책을 배포 하 고 원하는 Ou GPO 연결 해야 합니다.

변환 작업을 완료 하려면 도메인 관리자 자격 증명이 필요 합니다.

> [!IMPORTANT]
> 인터넷 정보 서비스 (IIS) 보안 정책 설정 그룹 정책을 사용 하 여 배포할 수 없습니다.</br>서버를 마지막으로 시작할 때 Windows 방화벽 서비스가 자동으로 시작 되지 않으면 승인 된 응용 프로그램을 나열 하는 > 방화벽 정책을 서버에 배포 하면 안 됩니다.



## <a name="syntax"></a>구문

```
scwcmd transform /p:<Policyfile.xml> /g:<GPODisplayName>
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|/p: \< Policyfile>|적용 해야 하는.xml 정책 파일의 경로 파일 이름을 지정 합니다. 이 매개 변수를 지정 합니다.|
|/g: \< GPODisplayName>|GPO의 표시 이름을 지정합니다. 이 매개 변수를 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

Scwcmd.exe은 Windows Server 2008 R2, Windows Server 2008 또는 Windows Server 2003을 실행 하는 컴퓨터에서 사용할 수만 있습니다.

## <a name="examples"></a>예

FileServerPolicy.xml 라는 파일에서 FileServerSecurity 이라는 GPO를 만들려면 다음을 입력 합니다.
```
scwcmd transform /p:FileServerPolicy.xml /g:FileServerSecurity
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)