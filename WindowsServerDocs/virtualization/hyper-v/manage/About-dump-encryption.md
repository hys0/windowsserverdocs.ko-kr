---
title: 덤프 암호화 정보
description: 덤프 파일을 암호화 하 고 암호화 문제를 해결 하는 방법을 설명 합니다.
ms.prod: windows-server
manager: dongill
ms.topic: article
author: larsiwer
ms.asset: b78ab493-e7c3-41f5-ab36-29397f086f32
ms.author: kathydav
ms.date: 11/03/2016
ms.openlocfilehash: a7df8de5a828b68a341191eaa1a400f80dd9127b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852906"
---
# <a name="about-dump-encryption"></a>덤프 암호화 정보
덤프 암호화를 사용 하 여 시스템에 대해 생성 된 크래시 덤프와 라이브 덤프를 암호화할 수 있습니다. 덤프는 각 덤프에 대해 생성 된 대칭 암호화 키를 사용 하 여 암호화 됩니다. 그런 다음 호스트의 신뢰할 수 있는 관리자가 지정한 공개 키 (크래시 덤프 암호화 키 보호기)를 사용 하 여이 키가 암호화 됩니다. 이렇게 하면 일치 하는 개인 키가 있는 사용자만 암호를 해독 하 여 덤프의 내용에 액세스할 수 있습니다. 이 기능은 보호 된 패브릭에서 활용 됩니다.
참고: 덤프 암호화를 구성 하는 경우에도 Windows 오류 보고을 사용 하지 않도록 설정 합니다. WER에서 암호화 된 크래시 덤프를 읽을 수 없습니다.

## <a name="configuring-dump-encryption"></a>덤프 암호화 구성
### <a name="manual-configuration"></a>수동 구성
레지스트리를 사용 하 여 덤프 암호화를 켜려면 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl` 아래에서 다음 레지스트리 값을 구성 합니다.

| 값 이름 | 형식 | 값 |
| ---------- | ---- | ----- |
| 안 함 | DWORD | 1 덤프 암호화를 사용 하도록 설정 하려면 0, 덤프 암호화를 사용 하지 않으려면 0 |
| UblicKey::P | Binary | 덤프를 암호화 하는 데 사용 해야 하는 공개 키 (RSA, 2048 비트)입니다. [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)형식으로 지정 해야 합니다. |
| \ 인증서:: 지문 | String | 크래시 덤프의 암호를 해독할 때 로컬 인증서 저장소에서 개인 키를 자동으로 조회할 수 있도록 하는 인증서 지문입니다. |


### <a name="configuration-using-script"></a>스크립트를 사용 하 여 구성
구성을 간소화 하기 위해 [샘플 스크립트](https://github.com/Microsoft/Virtualization-Documentation/tree/live/hyperv-tools/DumpEncryption) 를 사용 하 여 인증서의 공개 키를 기반으로 하는 덤프 암호화를 사용 하도록 설정할 수 있습니다.

1. 신뢰할 수 있는 환경에서: 2048 비트 RSA 키가 있는 인증서를 만들고 공용 인증서를 내보냅니다.
2. 대상 호스트: 로컬 인증서 저장소에 공용 인증서 가져오기
3. 샘플 구성 스크립트 실행 
    ```
    .\Set-DumpEncryptionConfiguration.ps1 -Certificate (Cert:\CurrentUser\My\093568AB328DF385544FAFD57EE53D73EFAAF519) -Force
    ```

## <a name="decrypting-encrypted-dumps"></a>암호화 된 덤프 암호 해독
기존의 암호화 된 덤프 파일의 암호를 해독 하려면 Windows 용 디버깅 도구를 다운로드 하 여 설치 해야 합니다. 이 도구 집합에는 암호화 된 덤프 파일의 암호를 해독 하는 데 사용할 수 있는 KernelDumpDecrypt이 포함 되어 있습니다.
개인 키를 포함 하는 인증서가 현재 사용자의 인증서 저장소에 있는 경우를 호출 하 여 덤프 파일의 암호를 해독할 수 있습니다.

```
    KernelDumpDecrypt.exe memory.dmp memory_decr.dmp
```
암호 해독 후 WinDbg와 같은 도구는 해독 된 덤프 파일을 열 수 있습니다.

## <a name="troubleshooting-dump-encryption"></a>덤프 암호화 문제 해결
시스템에서 덤프 암호화를 사용 하도록 설정 했지만 덤프가 생성 되지 않는 경우 시스템의 `System` 이벤트 로그에서 `Kernel-IO` 이벤트 1207을 확인 하세요. 덤프 암호화를 초기화할 수 없는 경우이 이벤트가 만들어지고 덤프가 사용 하지 않도록 설정 됩니다.

| 자세한 오류 메시지 | 완화 단계 |
| ---------------------- | ----------------- |
| 공개 키 또는 지문 레지스트리가 없습니다. | 두 레지스트리 값이 모두 예상 위치에 있는지 확인 합니다. |
| 잘못 된 공개 키 | PublicKey 레지스트리 값에 저장 된 공개 키가 [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)로 저장 되었는지 확인 합니다. |
| 지원 되지 않는 공개 키 크기 | 현재는 2048 비트 RSA 키만 지원 됩니다. 이 요구 사항과 일치 하는 키 구성 |

또한 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled` 아래 `GuardedHost` 값이 0이 아닌 값으로 설정 되었는지 확인 합니다. 이렇게 하면 크래시 덤프가 완전히 사용 되지 않습니다. 이 경우 0으로 설정 합니다.
