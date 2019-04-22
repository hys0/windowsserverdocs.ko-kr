---
title: 덤프 암호화에 대 한
description: 덤프 파일을 암호화 하 고 암호화 문제 해결 방법을 설명 합니다.
ms.prod: windows-server-threshold
manager: dongill
ms.topic: article
author: larsiwer
ms.asset: b78ab493-e7c3-41f5-ab36-29397f086f32
ms.author: kathydav
ms.date: 11/03/2016
ms.openlocfilehash: e0ca8829aa8f93e7543b4183539beade3b4aeb47
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812394"
---
# <a name="about-dump-encryption"></a>덤프 암호화에 대 한
크래시 덤프 및 시스템에 대해 생성 된 라이브 덤프 암호화를 덤프 암호화를 사용할 수 있습니다. 덤프가 생성 되는 대칭 암호화 키를 사용 하 여 각 덤프 암호화 됩니다. 이 키 자체 호스트 (크래시 덤프 암호화 키 보호기)의 신뢰할 수 있는 관리자가 지정한 공개 키를 사용 하 여 암호화 됩니다. 이렇게 하면 개인 키를 일치 하는 사람만 수 해독 따라서 덤프의 내용에 액세스 합니다. 보호 된 패브릭에서 이러한 기능을 활용 합니다.
참고: 덤프 암호화를 구성 하는 경우 Windows 오류 보고를 해제할 수도 있습니다. WER는 암호화 된 크래시 덤프를 읽을 수 없습니다.

# <a name="configuring-dump-encryption"></a>덤프 암호화를 구성합니다.
## <a name="manual-configuration"></a>수동 구성
레지스트리를 사용 하 여 덤프 암호화를 설정 하려면 아래에 다음 레지스트리 값 구성 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl`

| 값 이름 | 형식 | 값 |
| ---------- | ---- | ----- |
| DumpEncryptionEnabled | DWORD | 덤프 암호화를 덤프 암호화를 해제 하려면 0을 사용 하도록 설정 하려면 1 |
| EncryptionCertificates\Certificate.1::PublicKey | 이진 | 공개 키 (RSA, 2048 비트) 덤프 암호화 하는 데 사용 해야 하는입니다. 이 형식으로 지정 해야 [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)합니다. |
| EncryptionCertificates\Certificate.1::Thumbprint | 문자열 | 크래시 덤프를 암호 해독할 때 로컬 인증서 저장소에 개인 키의 자동 조회를 허용 하도록 인증서 지문입니다. |


## <a name="configuration-using-script"></a>스크립트를 사용 하 여 구성
구성을 간소화 하는 [샘플 스크립트](https://github.com/Microsoft/Virtualization-Documentation/tree/live/hyperv-tools/DumpEncryption) 인증서의 공개 키를 기반으로 하는 덤프 암호화를 사용 하도록 설정할 수 있습니다.

1. 신뢰할 수 있는 환경: 2048 비트 RSA 키를 사용 하 여 인증서를 만들고 공용 인증서 내보내기
2. 대상 호스트: 로컬 인증서 저장소에 공용 인증서 가져오기
3. 샘플 구성 스크립트를 실행 합니다. 
    ```
    .\Set-DumpEncryptionConfiguration.ps1 -Certificate (Cert:\CurrentUser\My\093568AB328DF385544FAFD57EE53D73EFAAF519) -Force
    ```

# <a name="decrypting-encrypted-dumps"></a>암호화 된 덤프를 암호 해독
기존 암호화 된 덤프 파일을 암호 해독 하려면 다운로드 하 여 Windows에 대 한 디버깅 도구를 설치 해야 합니다. 이 도구 집합에는 암호화 된 덤프 파일을 암호 해독에 사용할 수 있는 KernelDumpDecrypt.exe 포함 되어 있습니다.
호출 하 여 덤프 파일의 암호를 해독할 수 개인 키를 포함 하 여 인증서가 현재 사용자의 인증서 저장소에 있는 경우

```
    KernelDumpDecrypt.exe memory.dmp memory_decr.dmp
```
암호 해독 후 WinDbg와 같은 도구 암호 해독 된 덤프 파일을 열 수 있습니다.

# <a name="troubleshooting-dump-encryption"></a>덤프 암호화 문제 해결
덤프 암호화를 시스템에서 사용할 수 없는 덤프를 생성 하지만 경우에 시스템의 확인 하십시오 `System` 에 대 한 이벤트 로그 `Kernel-IO` 1207 이벤트입니다. 덤프 암호화를 초기화할 수 없습니다이 이벤트가 생성 되 고 덤프는 사용 하지 않도록 설정 합니다.

| 자세한 오류 메시지 | 완화 하는 단계 |
| ---------------------- | ----------------- |
| 공개 키 또는 지문 레지스트리 누락 | 레지스트리 값이 모두 예상된 위치에 있는지 확인 합니다. |
| 잘못 된 공개 키 | PublicKey 레지스트리 값에 저장 된 공개 키로 저장 되도록 해야 [BCRYPT_RSAKEY_BLOB](https://msdn.microsoft.com/library/windows/desktop/aa375531(v=vs.85).aspx)합니다. |
| 공개 키 크기가 지원 되지 않는 | 현재, 2048 비트 RSA 키만 지원 됩니다. 이 요구 사항 일치 하는 키를 구성 합니다. |

또한 값 `GuardedHost` 아래에서 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\CrashControl\ForceDumpsDisabled` 0이 아닌 값으로 설정 됩니다. 이 완전히 크래시 덤프를 해제합니다. 이 경우 0으로 설정 합니다.
