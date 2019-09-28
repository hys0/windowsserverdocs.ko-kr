---
title: auditpol
description: Windows 명령 항목 ( **auditpol** )-에 대 한 정보를 표시 하 고 감사 정책을 조작 하는 기능을 수행 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a02cfb9d-732f-4e77-aeba-f18265daa3af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5e249a9e2a07505f052b774208c514b4d16879b8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382383"
---
# <a name="auditpol"></a>auditpol



에 대 한 정보를 표시 하 고 감사 정책을 조작 하는 함수를 수행 합니다.

이 명령을 사용할 수 있는 방법을 예제를 보려면 각 항목의 예 섹션을 참조 하십시오.

## <a name="syntax"></a>구문

```
Auditpol command [<sub-command><options>]
```

## <a name="parameters"></a>매개 변수

|하위 명령|설명|
|-----------|-----------|
|/get|현재 감사 정책을 표시합니다.</br>참조 [Auditpol get](auditpol-get.md) 구문 및 옵션에 대 한 합니다.|
|설정 /|감사 정책을 설정합니다.</br>참조 [Auditpol 집합](auditpol-set.md) 구문 및 옵션에 대 한 합니다.|
|/list|선택할 수 있는 정책 요소를 표시합니다.</br>참조 [Auditpol 목록](auditpol-list.md) 구문 및 옵션에 대 한 합니다.|
|백업 /|감사 정책 파일에 저장 합니다.</br>참조 [Auditpol 백업](auditpol-backup.md) 구문 및 옵션에 대 한 합니다.|
|/restore|감사 정책을 auditpol /backup을 사용 하 여 이전에 만든 파일에서 복원 합니다.</br>참조 [Auditpol 복원](auditpol-restore.md) 구문 및 옵션에 대 한 합니다.|
|/ 지우기|감사 정책을 지웁니다.</br>참조 [Auditpol 지우기](auditpol-clear.md) 구문 및 옵션에 대 한 합니다.|
|/remove|사용자 단위 감사 정책 설정을 모두 제거 하 고 모든 시스템 감사 정책 설정을 사용 하지 않도록 설정 합니다.</br>참조 [Auditpol 제거](auditpol-remove.md) 구문 및 옵션에 대 한 합니다.|
|/resourceSACL|전역 리소스 시스템 액세스 제어 목록 (Sacl)를 구성합니다.</br>참고: Windows 7 및 Windows Server 2008 r 2에만 적용 됩니다.</br>참조 [Auditpol resourceSACL](auditpol-resourcesacl.md)합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|

## <a name="remarks"></a>설명

감사 정책 명령줄 도구를 사용할 수 있습니다.
-   설정 및 시스템 감사 정책을 쿼리 합니다.
-   설정 하 고는 사용자 단위 감사 정책을 쿼리 합니다.
-   설정 하 고 감사 옵션을 쿼리 합니다.
-   설정 하 고 감사 정책에 대 한 액세스를 위임 하는 데 사용 되는 보안 설명자를 쿼리 합니다.
-   보고서 또는 쉼표로 구분 된 값 (CSV) 텍스트 파일에 감사 정책을를 백업 합니다.
-   CSV 텍스트 파일에서 감사 정책을 로드 합니다.
-   전역 리소스 Sacl을 구성 합니다.

#### <a name="additional-references"></a>추가 참조

[명령줄 구문 키](command-line-syntax-key.md)