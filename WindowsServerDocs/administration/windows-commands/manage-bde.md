---
title: manage-bde
description: '* * * *에 대 한 참조 항목'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 567e0ed45f6bef42e82c3a68b3c0cbbb352b12d9
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724038"
---
# <a name="manage-bde"></a>manage-bde



설정 하거나 BitLocker 해제를 사용 하는, 지정한 메커니즘을 잠금 해제, 복구 메서드를 업데이트 하 고, BitLocker로 보호 된 데이터 드라이브를 잠금 해제 합니다. 이 명령줄 도구를 대신 사용할 수는 **BitLocker 드라이브 암호화** 제어판 항목입니다.

## <a name="syntax"></a>구문

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm] 
[–SetIdentifier] [-ForceRecovery] [–changepassword] [–changepin] [–changekey] [-KeyPackage] [–upgrade] [-WipeFreeSpace] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>매개 변수

|매개 변수|설명|
|---------|-----------|
|[Manage-bde: status](manage-bde-status.md)|BitLocker로 보호 되는 여부는 컴퓨터에 모든 드라이브에 대 한 정보를 제공 합니다.|
|[Manage-bde: on](manage-bde-on.md)|드라이브를 암호화 하 고 BitLocker를 설정 합니다.|
|[Manage-bde: off](manage-bde-off.md)|드라이브를 해독 하 고 BitLocker를 해제 합니다. 암호 해독 완료 되 면 모든 키 보호기 제거 됩니다.|
|[Manage-bde: pause](manage-bde-pause.md)|일시 중지 암호화 또는 암호 해독 합니다.|
|[Manage-bde: resume](manage-bde-resume.md)|암호화 또는 암호 해독을 다시 시작합니다.|
|[Manage-bde: lock](manage-bde-lock.md)|BitLocker로 보호 된 데이터에 대 한 액세스를 차단합니다.|
|[Manage-bde: unlock](manage-bde-unlock.md)|복구 암호 또는 복구 키를 사용 하 여 BitLocker로 보호 된 데이터에 액세스할 수 있습니다.|
|[Manage-bde: autounlock](manage-bde-autounlock.md)|데이터 드라이브 자동 잠금 해제를 관리 합니다.|
|[Manage-bde: protectors](manage-bde-protectors.md)|암호화 키에 대 한 보호 방법을 관리합니다.|
|[Manage-bde: tpm](manage-bde-tpm.md)|컴퓨터의 신뢰할 수 있는 플랫폼 모듈 (TPM)를 구성합니다. 이 명령은 Windows 8을 실행 하는 컴퓨터에서 지원 되지 않습니다 또는 **win8_server_2**합니다. 이러한 컴퓨터에서 TPM을 관리 하려면 Windows PowerShell에 대 한 TPM 관리 MMC 스냅인 또는 TPM 관리 cmdlet을 사용 합니다.|
|[Manage-bde: setidentifier](manage-bde-setidentifier.md)|드라이브 식별자 필드에 지정 된 값을 드라이브에 설정 된 **조직에 대 한 고유 식별자를 제공** 그룹 정책 설정.|
|[Manage-bde: ForceRecovery](manage-bde-forcerecovery.md)|BitLocker로 보호 된 드라이브를 복구 모드로 다시 시작 되도록합니다. 이 명령은 드라이브에서 모든 TPM 관련 키 보호기를 삭제합니다. 컴퓨터 다시 시작 되 면 복구 암호 또는 복구 키만 데 사용할 수 드라이브의 잠금을 해제 합니다.|
|[Manage-bde: changepassword](manage-bde-changepassword.md)|데이터 드라이브에 대 한 암호를 수정합니다.|
|[Manage-bde: changepin](manage-bde-changepin.md)|운영 체제 드라이브에 대 한 PIN을 수정합니다.|
|[Manage-bde: changekey](manage-bde-changekey.md)|운영 체제 드라이브에 대 한 시작 키를 수정합니다.|
|[Manage-bde: KeyPackage](manage-bde-keypackage.md)|드라이브에 대 한 키 패키지를 생성합니다.|
|[Manage-bde: upgrade](manage-bde-upgrade.md)|BitLocker 버전을 업그레이드합니다.|
|[Manage-bde: WipeFreeSpace](manage-bde-wipefreespace.md)|드라이브의 가용 공간을 초기화 합니다.|
|-? 또는 /?|도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다.|
|-help 또는-h|명령 프롬프트에서 전체 도움말을 표시 합니다.|

## <a name="examples"></a>예

을 (를) 통해 컴퓨터의 드라이브를 표시 하 고 BitLocker로 보호 되는 드라이브 및 현재 암호화 상태를 확인 합니다.
```
manage-bde -status
```
C 드라이브에서 BitLocker를 사용 하도록 설정 하는 방법을 보여 줍니다. 복구 암호 BitLocker에 의해 생성 된 되어 녹음할 수 있도록 화면에 표시 됩니다.
```
manage-bde –on C: -recoverypassword
```
는 복구 암호를 사용 하 여 BitLocker로 보호 된 드라이브의 잠금을 해제 하는 방법을 보여 줍니다.
```
manage-bde –unlock E: -recoverypassword 111111-222222-333333-444444-555555-666666-777777-888888
```

## <a name="additional-references"></a>추가 참조

-   - [명령줄 구문 키](command-line-syntax-key.md)
-   [명령줄을 사용 하 여 BitLocker를 사용 하도록 설정](https://technet.microsoft.com/library/dd894351(v=ws.10).aspx)
