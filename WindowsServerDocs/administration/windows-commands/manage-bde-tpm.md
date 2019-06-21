---
title: 관리 bde tpm
description: '에 대 한 Windows 명령을 항목 * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 11a8530d-edd7-4fe3-ae81-b943766760fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc3cfa583866335d214282be08366854dec77d0f
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280004"
---
# <a name="manage-bde-tpm"></a>관리 bde: tpm

> 적용 대상: Windows Server (반기 채널), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012
> 
> [!IMPORTANT]
> Windows 8, Windows Server 2012 또는 이후 운영 체제를 실행 하는 컴퓨터에서 사용 하기 위해이 명령은 지원 되지 않습니다. 해당 컴퓨터에 대해 사용할 수는 [Windows PowerShell에 대 한 TPM 관리 cmdlet](https://docs.microsoft.com/powershell/module/trustedplatformmodule/)합니다.
> 이 명령은 Windows 7 또는 Windows Server 2008을 실행 하는 컴퓨터를 사용 하는 경우 컴퓨터의 신뢰할 수 있는 TPM (플랫폼 모듈)이이 명령을 사용 하 여 구성할 수 있습니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.
> ## <a name="syntax"></a>구문
> ```
> manage-bde -tpm [-turnon] [-takeownership <OwnerPassword>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
> ```
> ### <a name="parameters"></a>매개 변수
> 
> |    매개 변수    |                                                                              설명                                                                               |
> |-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
> |     -켬     |              사용 하 고 TPM 소유자 암호를 설정 해야 TPM을 활성화 합니다. 사용할 수도 있습니다 **-t** 이 명령의 축약된 버전으로 합니다.              |
> | -takeownership  |                      소유자 암호를 설정 하 여 TPM의 소유권을 갖습니다. 사용할 수도 있습니다 **-o** 이 명령의 축약된 버전으로 합니다.                       |
> | <OwnerPassword> |                                                      TPM에 대해 지정 하는 소유자 암호를 나타냅니다.                                                       |
> |  -computername  | 다른 컴퓨터에서 BitLocker 보호를 수정 하는 관리 bde.exe 사용할지를 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
> |     <Name>      |    BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다.     |
> |    -? 또는 /?     |                                                               명령 프롬프트에서 도움말에 대 한 간단한 표시 됩니다.                                                               |
> |   -help 또는-h   |                                                             전체 명령 프롬프트에서 도움말을 표시 합니다.                                                              |
> 
> ## <a name="BKMK_Examples"></a>예제
> 다음 예제를 사용 하는 **tpm** TPM을 설정 하는 명령입니다.
> ```
> manage-bde  tpm -turnon
> ```
> 다음 예제를 사용 하는 **tpm** TPM의 소유권을 가져올 소유자 암호를 설정 하는 명령을 0wnerP@ss합니다.
> ```
> manage-bde  tpm  takeownership 0wnerP@ss
> ```
> ## <a name="additional-references"></a>추가 참조
> -   [명령줄 구문 키](command-line-syntax-key.md)
> -   [manage-bde](manage-bde.md)
