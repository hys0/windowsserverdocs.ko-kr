---
title: manage-bde tpm 관리
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c93a80a076b34ad4e7340387b098042b58103ae8
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820761"
---
# <a name="manage-bde-tpm"></a>manage-bde: tpm

> 적용 대상: Windows Server (반기 채널), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
>
> [!IMPORTANT]
> Windows 8, Windows Server 2012 또는 이후 운영 체제를 실행 하는 컴퓨터에서 사용 하기 위해이 명령은 지원 되지 않습니다. 해당 컴퓨터에 대해 사용할 수는 [Windows PowerShell에 대 한 TPM 관리 cmdlet](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)합니다.
> Windows 7 또는 Windows Server 2008를 실행 하는 컴퓨터에서이 명령을 사용 하는 경우에도이 명령을 사용 하 여 컴퓨터의 신뢰할 수 있는 플랫폼 모듈 (TPM)을 구성할 수 있습니다.
> ## <a name="syntax"></a>구문
> ```
> manage-bde -tpm [-turnon] [-takeownership <OwnerPassword>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
> ```
> #### <a name="parameters"></a>매개 변수
>
> |    매개 변수    |                                                                              설명                                                                               |
> |-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |     -켬     |              사용 하 고 TPM 소유자 암호를 설정 해야 TPM을 활성화 합니다. 사용할 수도 있습니다 **-t** 이 명령의 축약된 버전으로 합니다.              |
> | -takeownership  |                      소유자 암호를 설정 하 여 TPM의 소유권을 갖습니다. 사용할 수도 있습니다 **-o** 이 명령의 축약된 버전으로 합니다.                       |
> | <OwnerPassword> |                                                      TPM에 대해 지정 하는 소유자 암호를 나타냅니다.                                                       |
> |  -computername  | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 데 manage-bde.exe를 사용 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
> |     <Name>      |    BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.     |
> |    -? 또는 /?     |                                                               명령 프롬프트에 대 한 간단한 도움말을 표시 합니다.                                                               |
> |   -help 또는-h   |                                                             명령 프롬프트에서 전체 도움말을 표시 합니다.                                                              |
>
> ## <a name="examples"></a>예
> **-Tpm** 명령을 사용 하 여 tpm을 설정 하는 방법을 보여 줍니다.
> ```
> manage-bde  tpm -turnon
> ```
> Tpm 명령을 사용 하 여 TPM의 소유권을 가져오고 소유자 암호를로 설정 **하는 방법을** 보여 줍니다 0wnerP@ss .
> ```
> manage-bde  tpm  takeownership 0wnerP@ss
> ```
> ## <a name="additional-references"></a>추가 참조
> - [명령줄 구문 키](command-line-syntax-key.md)
> -   [manage-bde](manage-bde.md)
