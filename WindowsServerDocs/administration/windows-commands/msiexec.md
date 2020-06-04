---
title: msiexec
description: 명령줄에서 Windows Installer에 대 한 설치, 수정 및 작업 수행 방법을 제공 하는 msiexec 명령에 대 한 참조 항목입니다.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 122eb0ce-ecbc-4909-a52a-15c3413619af
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f84df28104f581873fe1fd86a3abd6a51532b020
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354343"
---
# <a name="msiexec"></a>msiexec

설치, 수정 및 명령줄에서 Windows Installer에 대 한 작업을 수행 하는 방법을 제공 합니다.

## <a name="install-options"></a>설치 옵션

설치 패키지를 시작 하기 위한 설치 유형을 설정 합니다.

### <a name="syntax"></a>구문

```
msiexec.exe [/i][/a][/j{u|m|/g|/t}][/x] <path_to_package>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ------- | -------- |
| /i | 일반 설치를 지정 합니다. |
| /a | 관리 설치를 지정 합니다. |
| /ju | 현재 사용자에 게 제품을 보급 합니다. |
| /jm | 모든 사용자에 게 제품을 보급 합니다. |
| /j/g | 보급 된 패키지에서 사용 하는 언어 식별자를 지정 합니다. |
| /j/t | 보급 패키지에 변환을 적용 합니다. |
| /x | 패키지를 제거 합니다. |
| `<path_to_package>` | 설치 패키지 파일의 위치와 이름을 지정 합니다. |

#### <a name="examples"></a>예

일반 설치 프로세스를 사용 하 여 C: 드라이브에서 *example .msi* 라는 패키지를 설치 하려면 다음을 입력 합니다.

```
msiexec.exe /i "C:\example.msi"
```

## <a name="display-options"></a>표시 옵션

대상 환경에 따라 설치 프로세스 중에 사용자에 게 표시 되는 내용을 구성할 수 있습니다. 예를 들어 수동 설치를 위해 모든 클라이언트에 패키지를 배포 하는 경우 전체 UI가 있어야 합니다. 그러나 사용자 조작이 필요 하지 않은 그룹 정책를 사용 하 여 패키지를 배포 하는 경우에는 UI가 포함 되지 않아야 합니다.

### <a name="syntax"></a>구문

```
msiexec.exe /i <path_to_package> [/quiet][/passive][/q{n|b|r|f}]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ------- | -------- |
| `<path_to_package>` | 설치 패키지 파일의 위치와 이름을 지정 합니다. |
| /quiet | 자동 모드를 지정 합니다. 즉, 사용자 조작이 필요 하지 않습니다. |
| /passive | 무인 모드를 지정 합니다. 즉, 설치 시 진행률 표시줄만 표시 됩니다. |
| /qn | 설치 과정에서 UI가 없도록 지정 합니다. |
| /qn + | 최종 대화 상자를 제외 하 고 설치 프로세스 중에 UI가 없음을 지정 합니다. |
| /qb | 설치 프로세스 중에 기본 UI를 지정 합니다. |
| /qb + | 최종 대화 상자를 포함 하 여 설치 프로세스 중에 기본 UI를 지정 합니다. |
| /qr | 설치 과정에서 축소 된 UI 환경을 지정 합니다. |
| /qf | 설치 과정에서 전체 UI 환경을 지정 합니다. |

##### <a name="remarks"></a>설명

- 사용자가 설치를 취소 한 경우에는 모달 상자가 표시 되지 않습니다. **Qb +!** 를 사용할 수 있습니다. 또는 **qb! +** 를 클릭 하 여 **취소** 단추를 숨깁니다.

#### <a name="examples"></a>예

일반 설치 프로세스를 사용 하 여 *C:\example.msi*패키지를 설치 하려면 다음을 입력 합니다.

```
msiexec.exe /i "C:\example.msi" /qn
```

## <a name="restart-options"></a>다시 시작 옵션

설치 패키지가 파일을 덮어쓰거나 사용 중인 파일의 변경을 시도 하는 경우 설치를 완료 하기 전에 다시 부팅 해야 할 수 있습니다.

### <a name="syntax"></a>구문

```
msiexec.exe /i <path_to_package> [/norestart][/promptrestart][/forcerestart]
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ------- | -------- |
| `<path_to_package>` | 설치 패키지 파일의 위치와 이름을 지정 합니다. |
| /norestart | 설치가 완료 된 후 장치를 다시 시작 하지 않도록 합니다. |
| /promptrestart | 다시 부팅 해야 하는 경우 사용자에 게 메시지를 표시 합니다. |
| /forcerestart | 설치가 완료 된 후 장치를 다시 시작 합니다. |

#### <a name="examples"></a>예

*C:\example.msi*패키지를 설치 하려면 마지막에 다시 부팅 하지 않고 일반 설치 프로세스를 사용 하 여 다음을 입력 합니다.

```
msiexec.exe /i "C:\example.msi" /norestart
```

## <a name="logging-options"></a>로깅 옵션

설치 패키지를 디버깅 해야 하는 경우 매개 변수를 설정 하 여 특정 정보를 포함 하는 로그 파일을 만들 수 있습니다.

### <a name="syntax"></a>구문

```
msiexec.exe [/i][/x] <path_to_package> [/L{i|w|e|a|r|u|c|m|o|p|v|x+|!|*}] <path_to_log>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ------- | -------- |
| /i | 일반 설치를 지정 합니다. |
| /x | 패키지를 제거 합니다. |
| `<path_to_package>` | 설치 패키지 파일의 위치와 이름을 지정 합니다. |
| /li | 로깅을 설정 하 고 출력 로그 파일에 상태 메시지를 포함 합니다. |
| /lw | 로깅을 설정 하 고 출력 로그 파일에 치명적이 지 않은 경고를 포함 합니다. |
| /le | 로깅을 설정 하 고 출력 로그 파일에 모든 오류 메시지를 포함 합니다. |
| /la | 로깅을 설정 하 고 출력 로그 파일에서 작업이 시작 된 시기에 대 한 정보를 포함 합니다. |
| /lr | 로깅을 설정 하 고 출력 로그 파일에 작업별 레코드를 포함 합니다. |
| /lu | 로깅을 설정 하 고 출력 로그 파일에 사용자 요청 정보를 포함 합니다. |
| /lc | 로깅을 설정 하 고 출력 로그 파일에 초기 UI 매개 변수를 포함 합니다. |
| /lm | 로깅을 설정 하 고 출력 로그 파일에 메모리 부족 또는 치명적인 종료 정보를 포함 합니다. |
| // | 로깅을 설정 하 고 출력 로그 파일에 디스크 공간 부족 메시지를 포함 합니다. |
| /lp | 로깅을 설정 하 고 출력 로그 파일에 터미널 속성을 포함 합니다. |
| /lp | 로깅을 설정 하 고 출력 로그 파일에 터미널 속성을 포함 합니다. |
| /lv | 로깅을 설정 하 고 출력 로그 파일에 자세한 정보 출력을 포함 합니다. |
| /lp | 로깅을 설정 하 고 출력 로그 파일에 터미널 속성을 포함 합니다. |
| /lx | 로깅을 설정 하 고 출력 로그 파일에 추가 디버깅 정보를 포함 합니다. |
| /l 이상 | 로깅을 켜고 기존 로그 파일에 정보를 추가 합니다. |
| /l! | 로깅을 설정 하 고 각 줄을 로그 파일에 플러시합니다. |
| /l | 자세한 정보 (**/lv**) 또는 추가 디버깅 정보 (**/lx**)를 제외 하 고 로깅을 켜고 모든 정보를 기록 합니다. |
| `<path_to_logfile>` | 출력 로그 파일의 위치와 이름을 지정 합니다. |

#### <a name="examples"></a>예

*C:\example.msi*패키지를 설치 하려면 자세한 정보를 출력 하 고 *C:\package.log*에 출력 로그 파일을 저장 하 여 제공 된 모든 로깅 정보가 포함 된 일반 설치 프로세스를 사용 하 여 다음을 입력 합니다.

```
msiexec.exe /i "C:\example.msi" /L*V "C:\package.log"
```

## <a name="update-options"></a>업데이트 옵션

설치 패키지를 사용 하 여 업데이트를 적용 하거나 제거할 수 있습니다.

### <a name="syntax"></a>구문

```
msiexec.exe [/p][/update][/uninstall[/package<product_code_of_package>]] <path_to_package>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ------- | -------- |
| /p | 패치를 설치 합니다. 자동으로 설치 하는 경우 REINSTALLMODE 속성을 *ecmus* 로 설정 하 고 *모두*에 다시 설치 해야 합니다. 그렇지 않으면 패치는 대상 장치에서 캐시 된 MSI만 업데이트 합니다. |
| /update | 패치 설치 옵션. 여러 업데이트를 적용 하는 경우 세미콜론 (;)을 사용 하 여 구분 해야 합니다. |
| /package | 제품을 설치 하거나 구성 합니다. |

#### <a name="examples"></a>예

```
msiexec.exe /p "C:\MyPatch.msp"
msiexec.exe /p "C:\MyPatch.msp" /qb REINSTALLMODE="ecmus" REINSTALL="ALL"
msiexec.exe /update "C:\MyPatch.msp"
```

```
msiexec.exe /uninstall {1BCBF52C-CD1B-454D-AEF7-852F73967318} /package {AAD3D77A-7476-469F-ADF4-04424124E91D}
```

여기서 첫 번째 GUID는 패치 GUID이 고, 두 번째 GUID는 패치가 적용 된 MSI 제품 코드입니다.

## <a name="repair-options"></a>복구 옵션

이 명령을 사용 하 여 설치 된 패키지를 복구할 수 있습니다.

### <a name="syntax"></a>구문

```
msiexec.exe [/f{p|o|e|d|c|a|u|m|s|v}] <product_code>
```

#### <a name="parameters"></a>매개 변수

| 매개 변수 | Description |
| ------- | -------- |
| /fp | 파일이 없는 경우 패키지를 복구 합니다. |
| /fo | 파일이 없거나 이전 버전이 설치 되어 있는 경우 패키지를 복구 합니다. |
| /fe | 파일이 누락 된 경우 또는 같거나 이전 버전이 설치 된 경우 패키지를 복구 합니다. |
| /fd | 파일이 없거나 다른 버전이 설치 되어 있는 경우 패키지를 복구 합니다. |
| /fc | 파일이 누락 된 경우 또는 체크섬이 계산 된 값과 일치 하지 않는 경우 패키지를 복구 합니다. |
| /fa | 모든 파일을 강제로 다시 설치 합니다. |
| /fu | 모든 필수 사용자 관련 레지스트리 항목을 복구 합니다. |
| /fm | 모든 필수 컴퓨터 관련 레지스트리 항목을 복구 합니다. |
| /fs | 기존의 모든 바로 가기를 복구 합니다. |
| /fc | 원본에서 실행 하 고 로컬 패키지를 다시 캐시 합니다. |

#### <a name="examples"></a>예

복구할 MSI 제품 코드에 따라 모든 파일을 강제로 다시 설치 하려면 *{AAD3D77A-7476-469F-ADF4-04424124E91D}* 을 입력 합니다.

```
msiexec.exe /fa {AAD3D77A-7476-469F-ADF4-04424124E91D}
```

## <a name="set-public-properties"></a>공용 속성 설정

이 명령을 통해 공용 속성을 설정할 수 있습니다. 사용 가능한 속성 및 설정 하는 방법에 대 한 자세한 내용은 [공용 속성](https://docs.microsoft.com/windows/win32/msi/public-properties)을 참조 하세요.

## <a name="additional-references"></a>추가 참조

- [명령줄 구문 키](command-line-syntax-key.md)

- [Msiexec.exe 명령줄 옵션](https://docs.microsoft.com/windows/win32/msi/command-line-options)

- [표준 설치 관리자 명령줄 옵션](https://docs.microsoft.com/windows/win32/msi/standard-installer-command-line-options)
