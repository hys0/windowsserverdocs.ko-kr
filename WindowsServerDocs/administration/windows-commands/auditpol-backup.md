---
title: auditpol 백업
description: Windows 명령 항목에 대 한 **auditpol 백업** -시스템을 백업 정책 설정, 모든 사용자 및 쉼표로 구분 된 값 (CSV) 텍스트 파일에 모든 감사 옵션에 대 한 사용자 단위 감사 정책 설정을 감사 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc84e581-aa0f-4c91-b13b-1d970bad5517
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78594c0445ae482e49d47b3b67bb867e53866017
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867954"
---
# <a name="auditpol-backup"></a>auditpol 백업

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

시스템을 백업 정책 설정, 사용자 단위 감사 정책 설정을 모든 사용자 및 쉼표로 구분 된 값 (CSV) 텍스트 파일에 있는 모든 감사 옵션에 대 한 감사합니다.

## <a name="syntax"></a>구문
```
auditpol /backup /file:<filename>
```
## <a name="parameters"></a>매개 변수
|매개 변수|설명|
|-------|--------|
|/file|에 감사 정책을 백업할 파일의 이름을 지정 합니다.|
|/?|명령 프롬프트에 도움말을 표시합니다.|
## <a name="remarks"></a>설명
사용자별 정책 및 시스템 정책에 대 한 백업 작업에 대 한 작성 한 해야 하거나 보안 설명자에 해당 개체에 대 한 모든 권한을 설정 합니다. 소유 하 여 백업 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 오른쪽 목록 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.
## <a name="BKMK_examples"></a>예제
사용자 단위 감사를 백업 하려면 모든 사용자가 시스템에 대 한 정책 감사 정책 설정 및 auditpolicy.csv, 형식 라는 CSV 형식의 텍스트 파일에 모든 감사 옵션:
```
auditpol /backup /file:C:\auditpolicy.csv 
```
> [!NOTE]
> 드라이브를 지정 하는 경우 현재 디렉터리가 사용 됩니다.
#### <a name="additional-references"></a>추가 참조
[명령줄 구문 키](command-line-syntax-key.md)
[auditpol 복원](auditpol-restore.md)
