---
title: manage-bde on
description: 드라이브를 암호화 하 고 BitLocker를 설정 하는 manage-bde on 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f6a12814-df74-416c-a04a-62ea8512263e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bad56c9ade19d94fc5acc9b34a8cc42fe43b7c0d
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222852"
---
# <a name="manage-bde-on"></a>manage-bde on

드라이브를 암호화 하 고 BitLocker를 설정 합니다.

## <a name="syntax"></a>구문

```
manage-bde –on <drive> {[-recoverypassword <numericalpassword>]|[-recoverykey <pathtoexternaldirectory>]|[-startupkey <pathtoexternalkeydirectory>]|[-certificate]|
[-tpmandpin]|[-tpmandpinandstartupkey <pathtoexternalkeydirectory>]|[-tpmandstartupkey <pathtoexternalkeydirectory>]|[-password]|[-ADaccountorgroup <domain\account>]}
[-usedspaceonly][-encryptionmethod {aes128_diffuser|aes256_diffuser|aes128|aes256}] [-skiphardwaretest] [-discoveryvolumetype <filesystemtype>] [-forceencryptiontype <type>] [-removevolumeshadowcopies][-computername <name>]
[{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>매개 변수

| 매개 변수 | 설명 |
| --------- | ----------- |
| `<drive>` | 드라이브 문자를 뒤에 콜론을 나타냅니다. |
| -recoverypassword | 숫자 암호 보호기를 추가합니다. 사용할 수도 있습니다 **-rp** 이 명령의 축약된 버전으로 합니다. |
| `<numericalpassword>` | 복구 암호를 나타냅니다. |
| -recoverykey | 복구에 대 한 외부 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-날짜별** 이 명령의 축약된 버전으로 합니다. |
| `<pathtoexternaldirectory>` | 복구 키에 디렉터리 경로를 나타냅니다. |
| -시작 | 시작에 대 한 외부 키 보호기를 추가 합니다. 사용할 수도 있습니다 **-sk** 이 명령의 축약된 버전으로 합니다. |
| `<pathtoexternalkeydirectory>` | 시작 키에 디렉터리 경로를 나타냅니다. |
| -인증서 | 데이터 드라이브에 대 한 공개 키 보호기를 추가합니다. 사용할 수도 있습니다 **-cert** 이 명령의 축약된 버전으로 합니다. |
| -tpmandpin | 신뢰할 수 있는 플랫폼 모듈 (TPM) 및 운영 체제 드라이브에 대 한 개인 식별 번호 (PIN) 보호기를 추가합니다. 사용할 수도 있습니다 **-tp** 이 명령의 축약된 버전으로 합니다. |
| -tpmandstartupkey | 운영 체제 드라이브에 대 한 TPM 및 시작 키 보호기를 추가합니다. 사용할 수도 있습니다 **-tsk** 이 명령의 축약된 버전으로 합니다. |
| -tpmandpinandstartupkey | TPM, PIN 및 운영 체제 드라이브에 대 한 시작 키 보호기를 추가합니다. 사용할 수도 있습니다 **-tpsk** 이 명령의 축약된 버전으로 합니다. |
| -암호 | 데이터 드라이브에 암호 키 보호기를 추가합니다. 사용할 수도 있습니다 **-pw** 이 명령의 축약된 버전으로 합니다. |
| -ADaccountorgroup | 볼륨에 대 한 SID 기반 id 보호기를 추가합니다. 볼륨에서 사용자 또는 컴퓨터에 적절 한 자격 증명 하는 경우 자동으로 잠금이 해제 됩니다. 컴퓨터 계정을 지정 하는 경우 **$** 컴퓨터 이름에를 추가 하 고 **– service** 를 지정 하 여 사용자 대신 BitLocker 서버의 콘텐츠에서 잠금 해제가 발생 하도록 지정 합니다. 사용할 수도 있습니다 **-sid** 이 명령의 축약된 버전으로 합니다. |
| -usedspaceonly | 사용 중인 공간만 암호화를 암호화 모드를 설정합니다. 사용 중인된 공간을 포함 하는 볼륨의 섹션을 암호화 됩니다 하지 않지만 사용 가능한 공간이 없습니다. 이 옵션을 지정 하지 않으면 볼륨에서 사용 되는 모든 공간과 여유 공간이 암호화 됩니다. 사용할 수도 있습니다 **-사용** 이 명령의 축약된 버전으로 합니다. |
| -encryptionMethod | 암호화 알고리즘 및 키 크기를 구성합니다. 사용할 수도 있습니다 **-em** 이 명령의 축약된 버전으로 합니다. |
| -skiphardwaretest | 하드웨어 테스트 없이 암호화를 시작합니다. 사용할 수도 있습니다 **-s** 이 명령의 축약된 버전으로 합니다. |
| -discoveryvolumetype | 검색 데이터 드라이브에 사용 하 여 파일 시스템을 지정 합니다. 검색 데이터 드라이브는 BitLocker To Go 판독기 포함 된 FAT 포맷의 BitLocker로 보호 된 이동식 데이터 드라이브에 추가 된 숨겨진 드라이브입니다. |
| -forceencryptiontype | 소프트웨어 또는 하드웨어 암호화를 사용 하 여 BitLocker를 강제로 수행 합니다. 하나만 지정할 수 있습니다 **하드웨어** 또는 **소프트웨어** 암호화 형식입니다. **하드웨어** 매개 변수를 선택 했지만 드라이브가 하드웨어 암호화를 지원 하지 않는 경우 manage-bde에서 오류를 반환 합니다. 지정 된 암호화 유형을 금지 하는 그룹 정책 설정, 관리 bde 오류를 반환 합니다. 사용할 수도 있습니다 **-fet** 이 명령의 축약된 버전으로 합니다. |
| -removevolumeshadowcopies | 볼륨의 볼륨 섀도 복사본을 강제로 삭제 합니다. 이 명령을 실행 한 후에는 이전 시스템 복원 시점을 사용 하 여이 볼륨을 복원할 수 없습니다. 사용할 수도 있습니다 **-rvsc** 이 명령의 축약된 버전으로 합니다. |
| `<filesystemtype>` | 검색 데이터 드라이브와 함께 사용할 수 있는 파일 시스템 지정: FAT32 default 또는 none입니다. |
| -computername | Manage-bde를 사용 하 여 다른 컴퓨터에서 BitLocker 보호를 수정 하도록 지정 합니다. 사용할 수도 있습니다 **-cn** 이 명령의 축약된 버전으로 합니다. |
| `<name>` | BitLocker 보호를 수정할 수 있는 컴퓨터의 이름을 나타냅니다. 사용 가능한 값에는 컴퓨터의 NetBIOS 이름 및 컴퓨터의 IP 주소 포함 됩니다. |
| -? 또는 /? | 도움말에 대 한 간단한 명령 프롬프트에 표시 됩니다. |
| -help 또는-h | 명령 프롬프트에서 전체 도움말을 표시 합니다. |

### <a name="examples"></a>예

C 드라이브에 대 한 BitLocker를 설정 하 고 드라이브에 복구 암호를 추가 하려면 다음을 입력 합니다.

```
manage-bde –on C: -recoverypassword
```

C 드라이브에 대 한 BitLocker를 설정 하려면 드라이브에 복구 암호를 추가 하 고 드라이브 E에 복구 키를 저장 하려면 다음을 입력 합니다.

```
manage-bde –on C: -recoverykey E:\ -recoverypassword
```

운영 체제 드라이브의 잠금을 해제 하기 위해 외부 키 보호기 (예: USB 키)를 사용 하 여 C 드라이브에 대 한 BitLocker를 켜려면 다음을 입력 합니다.

```
manage-bde -on C: -startupkey E:\
```

> [!IMPORTANT]
> TPM이 없는 컴퓨터에서 BitLocker를 사용 하는 경우이 방법이 필요 합니다.

데이터 드라이브 E에 대 한 BitLocker를 설정 하 고 암호 키 보호기를 추가 하려면 다음을 입력 합니다.

```
manage-bde –on E: -pw
```

운영 체제 C 드라이브에 대 한 BitLocker를 설정 하 고 하드웨어 기반 암호화를 사용 하려면 다음을 입력 합니다.

```
manage-bde –on C: -fet hardware
```

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [manage-bde off 명령](manage-bde-off.md)

- [manage-bde 일시 중지 명령](manage-bde-pause.md)

- [manage-bde resume 명령](manage-bde-resume.md)

- [manage-bde 명령](manage-bde.md)
