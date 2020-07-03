---
title: manage-bde
description: BitLocker를 설정 또는 해제 하 고, 잠금을 해제 하 고, 복구 방법을 업데이트 하 고, BitLocker로 보호 되는 데이터 드라이브의 잠금을 해제 하는 manage-bde 명령에 대 한 참조 문서입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 480f44c6467587918ad347413315b208c874f8cd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922127"
---
# <a name="manage-bde"></a>manage-bde

BitLocker를 설정 또는 해제 하 고, 잠금 해제 메커니즘을 지정 하 고, 복구 방법을 업데이트 하 고, BitLocker로 보호 된 데이터 드라이브의 잠금을 해제 합니다.

> [!NOTE]
> 이 명령줄 도구를 대신 사용할 수는 **BitLocker 드라이브 암호화** 제어판 항목입니다.

## <a name="syntax"></a>구문

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm]
[–setidentifier] [-forcerecovery] [–changepassword] [–changepin] [–changekey] [-keypackage] [–upgrade] [-wipefreespace] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- |------------ |
| [manage-bde 상태](manage-bde-status.md) | BitLocker로 보호 되는 여부는 컴퓨터에 모든 드라이브에 대 한 정보를 제공 합니다. |
| [manage-bde on](manage-bde-on.md) | 드라이브를 암호화 하 고 BitLocker를 설정 합니다. |
| [manage-bde 꺼짐](manage-bde-off.md) | 드라이브를 해독 하 고 BitLocker를 해제 합니다. 암호 해독 완료 되 면 모든 키 보호기 제거 됩니다. |
| [manage-bde 일시 중지](manage-bde-pause.md) | 일시 중지 암호화 또는 암호 해독 합니다. |
| [manage-bde resume](manage-bde-resume.md) | 암호화 또는 암호 해독을 다시 시작합니다. |
| [manage-bde 잠금](manage-bde-lock.md) | BitLocker로 보호 된 데이터에 대 한 액세스를 차단합니다. |
| [manage-bde 잠금 해제](manage-bde-unlock.md) | 복구 암호 또는 복구 키를 사용 하 여 BitLocker로 보호 된 데이터에 액세스할 수 있습니다. |
| [manage-bde autounlock](manage-bde-autounlock.md) | 데이터 드라이브 자동 잠금 해제를 관리 합니다. |
| [manage-bde 보호기](manage-bde-protectors.md) | 암호화 키에 대 한 보호 방법을 관리합니다. |
| [manage-bde tpm 관리](manage-bde-tpm.md) | 컴퓨터의 신뢰할 수 있는 플랫폼 모듈 (TPM)를 구성합니다. 이 명령은 Windows 8 또는 **win8_server_2**를 실행 하는 컴퓨터에서 지원 되지 않습니다. 이러한 컴퓨터에서 TPM을 관리 하려면 Windows PowerShell에 대 한 TPM 관리 MMC 스냅인 또는 TPM 관리 cmdlet을 사용 합니다. |
| [manage-bde setidentifier](manage-bde-setidentifier.md)   | 드라이브 식별자 필드에 지정 된 값을 드라이브에 설정 된 **조직에 대 한 고유 식별자를 제공** 그룹 정책 설정. |
| [manage-bde ForceRecovery](manage-bde-forcerecovery.md) | BitLocker로 보호 된 드라이브를 복구 모드로 다시 시작 되도록합니다. 이 명령은 드라이브에서 모든 TPM 관련 키 보호기를 삭제합니다. 컴퓨터 다시 시작 되 면 복구 암호 또는 복구 키만 데 사용할 수 드라이브의 잠금을 해제 합니다. |
| [manage-bde changepassword](manage-bde-changepassword.md) | 데이터 드라이브에 대 한 암호를 수정합니다. |
| [manage-bde changepin](manage-bde-changepin.md) | 운영 체제 드라이브에 대 한 PIN을 수정합니다. |
| [manage-bde 변환](manage-bde-changekey.md) | 운영 체제 드라이브에 대 한 시작 키를 수정합니다. |
| [manage-bde KeyPackage](manage-bde-keypackage.md) | 드라이브에 대 한 키 패키지를 생성합니다. |
| [manage-bde 업그레이드](manage-bde-upgrade.md) | BitLocker 버전을 업그레이드합니다. |
| [manage-bde WipeFreeSpace](manage-bde-wipefreespace.md) | 드라이브의 가용 공간을 초기화 합니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [명령줄을 사용 하 여 BitLocker를 사용 하도록 설정](https://technet.microsoft.com/library/dd894351(v=ws.10).aspx)
