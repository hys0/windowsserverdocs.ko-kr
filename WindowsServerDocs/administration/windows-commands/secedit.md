---
title: secedit
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 58ed57ed-08e3-403d-a363-0620b358637a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8aaa40f21c6f14dc7d686261e9980594c14a8032
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818464"
---
# <a name="secedit"></a>secedit



구성 하 고 지정 된 보안 템플릿을 현재 구성을 비교 하 여 시스템 보안을 분석 합니다.

## <a name="syntax"></a>구문

```
secedit 
[/analyze /db <database file name> /cfg <configuration file name> [/overwrite] /log <log file name> [/quiet]]
[/configure /db <database file name> [/cfg <configuration filename>] [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]]
[/export /db <database file name> [/mergedpolicy] /cfg <configuration file name> [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>]]
[/generaterollback /db <database file name> /cfg <configuration file name> /rbk <rollback file name> [/log <log file name>] [/quiet]]
[/import /db <database file name> /cfg <configuration file name> [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]]
[/validate <configuration file name>]
```

### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[Secedit: 분석](secedit-analyze.md)|데이터베이스에 저장 된 초기 설정에 대 한 현재 시스템 설정을 분석할 수 있습니다.  분석 결과가 데이터베이스의 다른 영역에 저장 되 고 보안 구성 및 분석 스냅인에서 볼 수 있습니다.|
|[Secedit:configure](secedit-configure.md)|데이터베이스에 저장 하는 보안 설정을 사용 하 여 시스템을 구성할 수 있습니다.|
|[Secedit:export](secedit-export.md)|데이터베이스에 저장 하는 보안 설정을 내보낼 수 있습니다.|
|[Secedit:generaterollback](secedit-generaterollback.md)|구성 템플릿에 대 한 롤백 템플릿을 생성할 수 있습니다.|
|[Secedit:import](secedit-import.md)|서식 파일에 지정 된 설정을 시스템에 적용 하거나 시스템에 대해 분석 될 수 있도록 보안 템플릿을 데이터베이스로 가져올 수 있습니다.|
|[Secedit: 유효성 검사](secedit-validate.md)|보안 템플릿의 구문의 유효성을 검사할 수 있습니다.|

## <a name="remarks"></a>설명

모든 파일 이름에 대 한 경로가 지정 되지 않은 경우 현재 디렉터리가 사용 됩니다.

보안 템플릿 및 보안 구성에 보안 템플릿 스냅인을 사용 하 여 만들어지고이 분석 스냅인은 실행, 다음 파일이 생성 됩니다.

|파일|설명|
|----|-----------|
|Scesrv.log|**위치**: %windir%\security\logs</br>**만든**: 운영 체제</br>**파일 유형**: 텍스트</br>**새로 고침 빈도**: 덮어쓸 때 secedit / 분석 / 구성/내보내기 또는 /import 실행 됩니다.</br>**내용**: 정책 유형별로 그룹화 된 분석 결과 포함 합니다.|
|*사용자가 선택한 이름*.sdb|**위치**: %windir%\*사용자 계정 * \Documents\Security\Database</br>**만든**: 보안 구성과 분석 스냅인 실행</br>**파일 유형**: 소유</br>**새로 고침 빈도**: 새 보안 템플릿을 만든 될 때마다 업데이트 됩니다.</br>**내용**: 로컬 보안 정책 및 사용자가 만든 보안 템플릿.|
|*사용자가 선택한 이름*.log|**위치**: 기본값은 %windir% 있지만 사용자 정의\*사용자 계정 * \Documents\Security\Logs</br>**만든 사람**: 실행 되는 /analyze 및 / 하위 구성 (또는 보안 구성과 분석 스냅인을 사용 하 여)</br>**파일 유형**: 텍스트</br>**새로 고침 빈도**: 실행 되는 /analyze 및 / 하위 구성 (또는 보안 구성과 분석 스냅인을 사용 하 여) 덮어씁니다.</br>**내용**:</br>1.  로그 파일 이름</br>2.  날짜 및 시간</br>3.  분석 이나 조사의 결과입니다.|
|*사용자가 선택한 이름*.inf|**위치**: %windir%\*사용자 계정 * \Documents\Security\Templates</br>**만든**: 보안 템플릿 스냅인을 사용 하 여 실행</br>**파일 유형**: 텍스트</br>**새로 고침 빈도**: 보안 템플릿을 업데이트 될 때마다</br>**내용**: Set up 스냅인을 사용 하 여 선택한 각 정책에 대 한 템플릿에 대 한 정보를 포함 합니다.|

> [!NOTE]
> Microsoft Management Console (MMC) 및 보안 구성 및 분석 스냅인 Server Core에서 사용할 수 없는 경우

#### <a name="additional-references"></a>추가 참조

이 명령을 사용할 수 있는 방법을 예제를 보려면 하위 명령 파일의 예 섹션을 참조 합니다.
-   [명령줄 구문 키](command-line-syntax-key.md)