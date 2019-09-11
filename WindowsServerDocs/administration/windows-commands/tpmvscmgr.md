---
title: tpmvscmgr
description: '\* * * *에 대 한 Windows 명령 항목 '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b2c8ff4-5c5d-446d-99e7-4daa1b36a163
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b1d9b049615322bffc39b5b372ce145579b57b2
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868774"
---
# <a name="tpmvscmgr"></a>tpmvscmgr



Tpmvscmgr을 명령줄 도구를 만들고 삭제 하는 컴퓨터에 TPM 가상 스마트 카드 관리 자격 증명이 있는 사용자를 수 있습니다. 이 명령을 사용할 수 있는 방법을의 예 참조 [예제](#BKMK_Examples)합니다.

## <a name="syntax"></a>구문

```
Tpmvscmgr create [/name] [/AdminKey DEFAULT | PROMPT | RANDOM] [/PIN DEFAULT | PROMPT] [/PUK DEFAULT | PROMPT] [/generate] [/machine] [/?]
```
```
Tpmvscmgr destroy [/instance <instance ID>] [/?]
```

### <a name="parameters-for-create-command"></a>만들기 명령에 대 한 매개 변수

만들기 명령은 사용자의 시스템에 새 가상 스마트 카드를 설정 합니다. 삭제 해야 하는 경우 나중에 참조할 수는 새로 만든된 카드의 인스턴스 ID를 반환 합니다. ID가 형식에서 인스턴스 **ROOT\SMARTCARDREADER\000n** 여기서 **n** 0에서 시작 하 고 새로운 가상 스마트 카드를 만들 때마다 1 씩 증가 됩니다.

|매개 변수|설명|
|---------|-----------|
|이름 /|필수. 새로운 가상 스마트 카드의 이름을 나타냅니다.|
|/ AdminKey|사용자가 PIN을 잊어버린 경우 카드의 PIN을 다시 설정에 사용할 수 있는 원하는 관리자 키를 나타냅니다.</br>**기본** 010203040506070801020304050607080102030405060708의 기본값을 지정 합니다.</br>**프롬프트** 관리자 키에 대 한 값을 입력 하 라는 메시지를 표시 합니다.</br>**임의** 사용자에 게 반환 되지 않는 카드에 대 한 관리자 키에 대 한 임의 설정의 결과입니다. 이 스마트 카드 관리 도구를 사용 하 여 관리할 수 없을 수도 있는 카드를 만듭니다. 난수를 생성 하는 경우 48 자리 16 진수도 관리자가 키를 입력 해야 합니다.|
|/ 핀|원하는 사용자 PIN 값을 나타냅니다.</br>**기본** 기본 12345678의 PIN을 지정 합니다.</br>**프롬프트** 명령줄에서 PIN을 입력 하 라는 메시지입니다. PIN에는 8 자 이상 이어야 합니다 하 고 숫자, 문자 및 특수 문자를 포함할 수 있습니다.|
|/ PUK|원하는 PIN 잠금 해제 키 PUK () 값을 나타냅니다. PUK 값에는 8 자 이상 이어야 합니다 하 고 숫자, 문자 및 특수 문자를 포함할 수 있습니다. 매개 변수를 생략 하면 카드는 PUK 없이 만들어집니다.</br>**기본** PUK 12345678의 기본을 지정 합니다.</br>**프롬프트** 사용자에 게 명령줄에서 PUK를 입력 하 라는 메시지를 표시 합니다.|
|생성 /|가상 스마트 카드에 대 한 함수에 필요한 저장소에 파일을 생성 합니다. 하는 경우는 생성 / 매개 변수가 생략 되는 것을이 파일 시스템 없이 카드를 만드는 것과 같습니다. 예: Microsoft Configuration Manager는 스마트 카드 관리 시스템에 의해서만 파일 시스템이 없는 카드를 관리할 수 있습니다.|
|/machine|에 가상 스마트 카드를 만들 수는 원격 컴퓨터의 이름을 지정할 수 있습니다. 이 도메인 환경 에서만 사용할 수 고 DCOM에 의존 합니다. 이 명령을 실행 하는 사용자는 다른 컴퓨터에서 가상 스마트 카드 만들기에 성공 하려면 명령에 대 한 원격 컴퓨터에서 로컬 관리자 그룹의 구성원 이어야 합니다.|
|/?|이 명령에 대 한 도움말을 표시합니다.|

### <a name="parameters-for-destroy-command"></a>Destroy 명령에 대 한 매개 변수

제거 명령은 사용자의 컴퓨터에서 가상 스마트 카드를 안전 하 게 삭제 합니다.

> [!WARNING]
> 가상 스마트 카드를 삭제 하면 복구할 수 없습니다.

|매개 변수|설명|
|---------|-----------|
|/instance|제거할 가상 스마트 카드의 인스턴스 ID를 지정 합니다. InstanceID는 카드를 만들 때 Tpmvscmgr.exe에서 출력으로 생성 되었습니다. /Instance Destroy 명령에 대 한 필수 필드입니다.|
|/?|이 명령에 대 한 도움말을 표시합니다.|

## <a name="remarks"></a>설명

멤버는 **관리자** 그룹 (또는 해당 하는) 대상 컴퓨터에는이 명령의 모든 매개 변수를 실행 하는 데 필요한 최소입니다.

영숫자 입력에 대 한 전체 127 문자 ASCII 집합 허용 됩니다.

## <a name="BKMK_Examples"></a>예와

다음 명령은 나중에 다른 컴퓨터에서 시작 된 스마트 카드 관리 도구에 의해 관리 될 수 있는 가상 스마트 카드를 만드는 방법을 보여 줍니다.
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey DEFAULT /PIN PROMPT
```
또는 기본 관리자 키를 사용 하는 대신 명령줄에서 관리자 키를 만들 수 있습니다. 다음 명령을 관리자 키를 만드는 방법을 보여 줍니다.
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey PROMPT /PIN PROMPT
```
다음 명령은 인증서를 등록 하는 데 사용할 수 있는 관리 되지 않는 가상 스마트 카드를 만듭니다.
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey RANDOM /PIN PROMPT /generate
```
다음 명령은 임의 관리자 키를 가진 가상 스마트 카드를 만듭니다. 키 생성 cardis 후 자동으로 삭제 됩니다. 이 해야 함을 의미 사용자 PIN을 잊은 또는 PIN 변경 하려는 경우 사용자는 카드를 삭제 하 고 다시 만드십시오. 카드를 삭제 하려면 사용자에는 다음 명령을 실행할 수 있습니다.
```
tpmvscmgr.exe destroy /instance <instance ID> 
```
여기서 \<instance ID >은 사용자가 카드를 만들 때 화면에 인쇄 되는 값입니다. 특히, 만든 첫 번째 카드, 인스턴스 ID가 ROOT\SMARTCARDREADER\0000입니다.

#### <a name="additional-references"></a>추가 참조

-   [명령줄 구문 키](command-line-syntax-key.md)