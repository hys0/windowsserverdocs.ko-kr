---
title: auditpol 집합
description: Windows 명령 항목 **auditpol 집합** -사용자 단위 감사 정책, 시스템 감사 정책 또는 감사 옵션을 설정 합니다.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4947486-87bd-48cb-ba81-7230c8e70895
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3c9ec2fab4cad408e0bb845fe157cfdf94f8e09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382400"
---
# <a name="auditpol-set"></a>auditpol 집합

>적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

설정 사용자 단위 감사 정책, 시스템 감사 정책 또는 감사 옵션입니다.

## <a name="syntax"></a>구문
```
auditpol /set
[/user[:<username>|<{sid}>][/include][/exclude]]
[/category:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/subcategory:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/option:<option name> /value: <enable>|<disable>]
```
## <a name="parameters"></a>매개 변수

|  매개 변수   |                                                                                                                                          설명                                                                                                                                           |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /user     |                                        사용자에 대 한 사용자 단위 감사 정책 범주 또는 하위 범주에 지정 된 보안 주체 설정 됩니다. 범주 또는 하위 범주 옵션을 SID (보안 식별자) 또는 이름으로 지정 되어야 합니다.                                         |
|   /include   | /User;를 사용 하 여 지정 사용자의 사용자별 정책 시스템 감사 정책에 의해 지정 되지 않은 경우에 생성 되어야 하는 감사 인해 됨을 나타냅니다. 이 설정은 기본값이 며 하지 않으면 자동으로 적용 되는 / 포함 하거나 /exclude 매개 변수를 명시적으로 지정 합니다. |
|   /exclude   |                                /User;를 사용 하 여 지정 사용자의 사용자별 정책 감사 시스템 감사 정책에 관계 없이 않아야 인해 됨을 나타냅니다. 로컬 관리자 그룹의 구성원 인 사용자에 대 한이 설정은 무시 됩니다.                                |
|  /category   |                                                                            전역 고유 식별자 (GUID) 또는 이름으로 지정 된 하나 이상의 감사 범주입니다. 사용자를 지정 하는 경우에 시스템 정책이 설정 됩니다.                                                                             |
| /subcategory |                                                                                         하나 이상의 감사 하위 범주 GUID 또는 이름을 지정 합니다. 사용자를 지정 하는 경우에 시스템 정책이 설정 됩니다.                                                                                          |
|   /success   |                 성공 감사를 지정합니다. 이 설정은 기본값이 며 /success 아니고 /failure 매개 변수를 명시적으로 지정 하는 경우 자동으로 적용 됩니다. 이 설정은 설정을 사용할지 여부를 나타내는 매개 변수와 함께 사용 되어야 합니다.                 |
|   /failure   |                                                                                  실패 감사를 지정합니다. 이 설정은 설정을 사용할지 여부를 나타내는 매개 변수와 함께 사용 되어야 합니다.                                                                                   |
|   /option    |                                                                                   CrashOnAuditFail, 트래버스, AuditBaseObjects 또는 Auditbaseobjects 옵션에 대 한 감사 정책을 설정 합니다.                                                                                    |
|     /sd      |                 감사 정책에 대 한 액세스 권한을 위임 하는 데 사용 되는 보안 설명자를 설정 합니다. 보안 설명자 정의 언어 (SDDL)를 사용 하 여 보안 설명자를 지정 해야 합니다. 보안 설명자는 임의 액세스 제어 목록 (DACL) 있어야 합니다.                 |
|      /?      |                                                                                                                              명령 프롬프트에 도움말을 표시합니다.                                                                                                                              |

## <a name="remarks"></a>설명
사용자 정책 및 시스템 정책에 대 한 모든 집합 작업에 대해 보안 설명자에 설정 된 해당 개체에 대 한 쓰기 또는 모든 제어 권한이 있어야 합니다. 처리 하는 개체로 설정 작업을 수행할 수도 있습니다는 **관리 감사 및 보안 로그** (SeSecurityPrivilege) 사용자 권한이 있습니다. 그러나이 권한을 설정 작업을 수행할 필요가 없는 추가 액세스를 허용 합니다.
## <a name="BKMK_examples"></a>예와
### <a name="examples-for-the-per-user-audit-policy"></a>사용자 단위 감사 정책에 대 한 예제
사용자 mikedan에 대 한 자세한 추적 범주 아래의 모든 하위 범주에 대 한 사용자 단위 감사 정책을 설정 하려면 모든 사용자의 성공 시도가 감사 됩니다.
```
auditpol /set /user:mikedan /category:"detailed Tracking" /include /success:enable
```
지정 된 이름 및 GUID 및 하위 범주를 성공 또는 실패 한 시도 대 한 감사를 표시 하지 않는 GUID로 지정 된 범주에 대 한 사용자 단위 감사 정책을 설정 하려면 다음을 입력 합니다.
```
auditpol /set /user:mikedan /exclude /category:"Object Access","System",{6997984b-797a-11d9-bed3-505054503030} 
/subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},:{0ccee9211-69ae-11d9-bed3-505054503030}, /success:enable /failure:enable
```
성공한 시도 제외한 모든 감사를 억제에 대 한 모든 범주에 대해 지정된 된 사용자에 대 한 사용자 단위 감사 정책을 설정 하려면 다음을 입력 합니다.
```
auditpol /set /user:mikedan /exclude /category:* /success:enable
```
### <a name="examples-for-the-system-audit-policy"></a>시스템 감사 정책에 대 한 예제
성공한 시도에 대 한 감사를 포함 하도록 자세한 추적 범주 아래의 모든 하위 범주에 대 한 시스템 감사 정책을 설정 하려면 다음을 입력 합니다.
```
auditpol /set /category:"detailed Tracking" /success:enable
```
> [!NOTE]
> 실패 설정을 변경 되지 않습니다.
> 개체 액세스 및 시스템 범주 (하위 범주에 나열 된 때문 인 것으로 간주) 및 하려고 했지만 실패 억제 및 성공한 시도 감사에 대 한 Guid로 지정 하는 하위 범주에 대 한 시스템 감사 정책을 설정 하려면 다음을 입력 합니다.
> ```
> auditpol /set /subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},{0ccee9211-69ae-11d9-bed3-505054503030}, /failure:disable /success:enable
> ```
> ### <a name="example-for-auditing-options"></a>감사 옵션에 대 한 예제
> CrashOnAuditFail 옵션에 대 한 상태를 설정된 하는 감사 옵션을 설정 하려면 다음을 입력 합니다.
> ```
> auditpol /set /option:CrashOnAuditFail /value:enable
> ```
> #### <a name="additional-references"></a>추가 참조
> [명령줄 구문 키](command-line-syntax-key.md)
