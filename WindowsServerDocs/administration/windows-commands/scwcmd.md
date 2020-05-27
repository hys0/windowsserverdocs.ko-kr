---
title: Scwcmd
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 188ae881-c7d4-4a7a-b967-8fdc79f5f345
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a8c002aa735b188fdd9ad75b0db7dbe06053516
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821163"
---
# <a name="scwcmd"></a>Scwcmd

> 적용 대상: Windows Server 2012 R2, Windows Server 2012

SCW (보안 구성 마법사)에 포함 된 Scwcmd 명령줄 도구를 사용 하 여 다음 작업을 수행할 수 있습니다.
-   SCW에서 생성 된 정책에 하나 이상의 서버를 구성 합니다.
-   SCW에서 생성 된 정책에 하나 이상의 서버를 분석 합니다.
-   HTML 형식으로 분석 결과 확인 합니다.
-   SCW 정책 롤백하십시오.
-   SCW에서 생성 된 정책에는 그룹 정책에 의해 지원 되는 기본 파일로 변환 합니다.
-   SCW로 보안 구성 데이터베이스 확장을 등록 합니다.

사용 하는 경우 **scwcmd** 구성, 분석, 또는 롤백 SCW 원격 서버에 대 한 정책을 원격 서버에 설치 해야 합니다.

## <a name="syntax"></a>구문

```
scwcmd <command> [<subcommand>]
```

### <a name="parameters"></a>매개 변수

|하위 명령|설명|
|----------|-----------|
|/analyze|컴퓨터 정책을 준수 하는지 여부를 결정 합니다.</br>참조 [Scwcmd: 분석](scwcmd-analyze.md) 구문 및 옵션에 대 한 합니다.|
|/ 구성|컴퓨터에는 SCW에서 생성 된 보안 정책을 적용합니다.</br>참조 [Scwcmd: 구성](scwcmd-configure.md) 구문 및 옵션에 대 한 합니다.|
|/register|확장 또는 사용자 역할, 작업, 서비스 또는 포트 정의 포함 하는 보안 구성 데이터베이스 파일을 등록 하 여 SCW 보안 구성 데이터베이스를 지정 합니다.</br>참조 [Scwcmd: 등록](scwcmd-register.md) 구문 및 옵션에 대 한 합니다.|
|같아야|를 사용할 수 있는 가장 최근의 롤백 정책을 적용 하 고 롤백 정책을 삭제 합니다.</br>참조 [Scwcmd: 롤백](scwcmd-rollback.md) 구문 및 옵션에 대 한 합니다.|
|/transform|SCW를 사용 하 여 Active Directory 도메인 서비스에 새 그룹 정책 개체 (GPO)에 의해 생성 된 보안 정책 파일을 변환 합니다.</br>참조 [Scwcmd: 변환](scwcmd-transform.md) 구문 및 옵션입니다.|
|/view|지정 된.xsl 변환을 사용 하 여.xml 파일을 렌더링 합니다.</br>참조 [Scwcmd: 보기](scwcmd-view.md) 구문 및 옵션에 대 한 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)
