---
title: dcgpofix
description: Dcgpofix 명령에 대 한 참조 문서로, 도메인에 대 한 기본 Gpo (그룹 정책 개체)를 다시 만듭니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cf9e3c37c054c34d602e472a2c5f83e9a8b284b9
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928809"
---
# <a name="dcgpofix"></a>dcgpofix

도메인에 대 한 기본 그룹 정책 개체 (Gpo)를 다시 만듭니다. 그룹 정책 관리 콘솔 (GPMC)를 가져오려면 서버 관리자를 통해 그룹 정책 관리 기능으로 설치 해야 합니다.

>[!IMPORTANT]
> 기본 **계정** 정책 설정, 암호 정책, 계정 잠금 정책 및 Kerberos 정책만 관리 하도록 기본 도메인 정책 GPO를 구성 하는 것이 가장 좋습니다. 또한 사용자 권한 및 감사 정책만 설정 하도록 기본 도메인 컨트롤러 정책 GPO를 구성 해야 합니다.

## <a name="syntax"></a>구문

```
dcgpofix [/ignoreschema] [/target: {domain | dc | both}] [/?]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| 생성 | 이 명령을 실행할 때 Active Directory 스키마의 버전을 무시 합니다. 그렇지 않으면이 명령은 명령이 배송 된 Windows 버전으로 같은 스키마 버전 에서만 작동 합니다. |
| `/target {domain | dc | both` | 기본 도메인 정책, 기본 도메인 컨트롤러 정책 또는 두 유형의 정책을 모두 대상으로 할지를 지정 합니다. |
| /? | 명령 프롬프트에 도움말을 표시합니다. |

## <a name="examples"></a>예

기본 **계정 정책** 설정, 암호 정책, 계정 잠금 정책 및 Kerberos 정책을 관리 하려면 Active Directory 스키마 버전을 무시 하 고 다음을 입력 합니다.

```
dcgpofix /ignoreschema /target:domain
```

기본 도메인 컨트롤러 정책 GPO를 구성 하려면 사용자 권한 및 감사 정책만을 설정 하 고 Active Directory 스키마 버전을 무시 하 고 다음을 입력 합니다.

```
dcgpofix /ignoreschema /target:dc
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)