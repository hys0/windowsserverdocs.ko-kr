---
title: auditpol resourceSACL
description: Windows 명령 항목에 대 한 **uditpol resourceSACL** -전역 리소스 시스템 액세스 제어 목록 (Sacl)를 구성 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 28771ba7-967a-45e9-9bf0-b2a2673070f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 375f37250404dd6740027cb18959697626c1ffc1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837494"
---
# <a name="auditpol-resourcesacl"></a>auditpol resourceSACL



전역 리소스 시스템 액세스 제어 목록 (Sacl)를 구성합니다.

> [!NOTE]
> 7 및 Windows Server 2008 R2 Windows에만 적용 됩니다.

이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
auditpol /resourceSACL
[/set /type:<resource> [/success] [/failure] /user:<user> [/access:<access flags>]]
[/remove /type:<resource> /user:<user> [/type:<resource>]]
[/clear [/type:<resource>]]
[/view [/user:<user>] [/type:<resource>]]
```

## <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|설정 /|새 항목을 추가 하거나 업데이트 하는 기존 항목 리소스에 대 한 리소스 SACL에에서 지정 된 형식입니다.|
|/remove|전역 개체 액세스 감사 목록에에서 지정 된 사용자에 대 한 모든 항목을 제거 합니다.|
|/ 지우기|전역 개체 액세스 감사 목록에서에서 모든 항목을 제거 합니다.|
|/view|리소스 SACL에에서 전역 개체 액세스 감사 항목을 나열합니다. 사용자 및 리소스 종류는 선택적입니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="arguments"></a>인수

|인수|설명|
|--------|-----------|
|/ 형식|어떤 개체에 대 한 액세스 감사 구성 되는 리소스입니다. 지원 되는 인수 값은 파일 (디렉터리 및 파일) 및 키 (레지스트리 키).</br>참고: 파일 및 키 값을 대/소문자를 구분 하지 않습니다.|
|/success|성공 감사를 지정합니다.|
|/failure|실패 감사를 지정합니다.|
|/user|다음 형식 중 하나를 사용 하는 사용자를 지정합니다.</br>-DomainName\Account (예: DOM\Administrators)</br>-StandaloneServer\Group 계정 (참조 [LookupAccountName 함수](https://msdn.microsoft.com/library/windows/desktop/aa379159(v=vs.85).aspx))</br>-{S-1-x-x-x-x} (10 진수 x 표현 되 고 전체 SID를 중괄호로 묶어야 합니다); 예를 들어: {s-1-5-21-5624481-130208933-164394174-1001}</br>    참고:     SID 양식을 사용 하는 경우이 계정의 존재 여부를 확인 하려면 검사가 수행 됩니다.|
|/access|다음 두 가지 형식 중 하나로 지정할 수 있는 권한 마스크를 지정 합니다.</br>-단순한 권한 시퀀스:</br>    -일반 액세스 권한:</br>        -모든 제네릭-GA</br>        -GR-일반 읽기</br>        -쓰기 GW-일반</br>        -GX-일반 실행</br>    파일에 대 한 액세스 권한:</br>        --FA 파일 모든 액세스</br>        일반-FR-파일 읽기</br>        -FW-파일에 대 한 일반 쓰기</br>        -FX-파일 일반 실행</br>    레지스트리 키에 대 한 액세스 권한:</br>        -KA-모든 액세스 키</br>        KR-키 읽기</br>        -   KW - KEY WRITE</br>        -KX-키 실행</br>    예: ' / 액세스: FRFW' 읽기에 대 한 감사 이벤트를 설정 하 고 쓰기 작업</br>-16 진수 값 (예: 0x1200a9)의 액세스 마스크를 나타내는</br>    보안 설명자 정의 언어 (SDDL) 표준에 속하지 않은 리소스 특정 비트 마스크를 사용 하는 경우에 유용 합니다. 생략 하면 모든 권한이 사용 됩니다.|

## <a name="remarks"></a>설명

ResourceSACL 작업에 대 한 보안 설명자에 설정 된 해당 개체에 쓰기 또는 모든 권한 사용 권한이 있어야 합니다. 처리 하는 개체로 resourceSACL 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 권한을 제거 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.

## <a name="BKMK_Examples"></a>예제

전역 리소스를 설정 하려면 SACL 성공적으로 액세스를 감사 하는 레지스트리 키에서 사용자가 시도 됩니다.
```
auditpol /resourceSACL /set /type:Key /user:MYDOMAIN\myuser /success
```
에 전역 리소스 일반 읽기를 수행 하 고 파일 또는 폴더에 대 한 함수를 작성 하는 사용자가 성공 및 실패 한 시도를 감사 SACL을 설정 합니다.
```
auditpol /resourceSACL /set /type:File /user:MYDOMAIN\myuser /success /failure /access:FRFW
```
제거 하려면 파일 또는 폴더에 대 한 모든 전역 리소스 SACL 항목:
```
auditpol /resourceSACL /type:File /clear
```
파일이 나 폴더에서 특정 사용자에 대 한 모든 전역 리소스 SACL 항목을 제거 합니다.
```
auditpol /resourceSACL /remove /type:File /user:{S-1-5-21-56248481-1302087933-1644394174-1001}
```
에 전역 개체 액세스 감사 파일 또는 폴더에 설정 하는 항목을 나열 합니다.
```
auditpol /resourceSACL /type:File /view
```
나열 하려면 전역 개체 파일 또는 폴더에 설정 된 특정 사용자에 대 한 감사 항목에 액세스 합니다.
```
auditpol /resourceSACL /type:File /view /user:MYDOMAIN\myuser
```

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)