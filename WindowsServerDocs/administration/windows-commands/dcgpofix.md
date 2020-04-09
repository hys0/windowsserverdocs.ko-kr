---
title: dcgpofix
description: Dcgpofix에 대 한 Windows 명령 항목은 도메인에 대 한 기본 Gpo (그룹 정책 개체)를 다시 만듭니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 81d5fa65-2aea-49d3-b353-357441846c00
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1532d4c8c0266c92b4efce57a6744552a54e51b0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846706"
---
# <a name="dcgpofix"></a>dcgpofix

도메인에 대 한 기본 그룹 정책 개체 (Gpo)를 다시 만듭니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
DCGPOFix [/ignoreschema] [/target: {Domain | DC | Both}] [/?]
```

#### <a name="parameters"></a>매개 변수

|    매개 변수    |                                                                                                 설명                                                                                                 |
|-----------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  생성  | Active Directory® 스키마 mc의 버전을 무시합니다.</br>이 명령을 실행 하면 됩니다. 그렇지 않으면이 명령은 명령이 배송 된 Windows 버전으로 같은 스키마 버전 에서만 작동 합니다. |
| /target {도메인 |                                                                                                     DC                                                                                                      |
|       /?        |                                                                                    명령 프롬프트에서 도움말을 표시합니다.                                                                                     |

## <a name="remarks"></a>주의

-   **Dcgpofix** 명령은 server Core 설치를 제외 하 고 windows Server 2008 R2 및 windows server 2008에서 사용할 수 있습니다.
-   그룹 정책 관리 콘솔 (GPMC)는 Windows Server 2008 R2 및 Windows Server 2008과 함께 배포 되지만 서버 관리자를 통해 그룹 정책 관리 기능으로 설치 해야 합니다.

## <a name="examples"></a><a name=BKMK_Examples></a>예와

기본 도메인 정책 GPO를 원래 상태로 복원 합니다. 이 GPO에 대 한 변경 내용을 손실 됩니다. 모범 사례로, 기본 계정 정책 설정, 암호 정책, 계정 잠금 정책 및 Kerberos 정책 관리에 기본 도메인 정책 GPO를 구성 해야 합니다. Active Directory 스키마의 버전을 무시 하면이 예제에서는 있도록는 **dcgpofix** 명령 명령이 배송 된 Windows 버전으로 동일한 스키마에 제한 되지 않습니다.
```
dcgpofix /ignoreschema /target:Domain
```
기본 도메인 컨트롤러 정책 GPO를 원래 상태로 복원 합니다. 이 GPO에 대 한 변경 내용을 손실 됩니다. 모범 사례로, 기본 도메인 컨트롤러 정책 GPO 사용자 권한을 설정 하 고 감사 정책에만 구성 해야 합니다. Active Directory 스키마의 버전을 무시 하면이 예제에서는 있도록는 **dcgpofix** 명령 명령이 배송 된 Windows 버전으로 동일한 스키마에 제한 되지 않습니다.
```
dcgpofix /ignoreschema /target:DC
```

## <a name="additional-references"></a>추가 참조

-   [그룹 정책 TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   - [명령줄 구문 키](command-line-syntax-key.md)