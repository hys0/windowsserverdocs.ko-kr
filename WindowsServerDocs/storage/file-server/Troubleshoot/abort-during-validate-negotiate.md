---
title: 유효성 검사 협상 중 TCP 연결이 중단 됨
description: 유효성을 검사 하는 동안 TCP 연결이 중단 될 때 SMB 문제를 해결 하는 방법을 소개 합니다.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 36bd49777899870246a19531c6681a5b45bb622d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815516"
---
# <a name="tcp-connection-is-aborted-during-validate-negotiate"></a>유효성 검사 협상 중 TCP 연결이 중단 됨

SMB 문제에 대 한 네트워크 추적에서 협상 유효성 검사 프로세스 중에 TCP 다시 설정 중단이 발생 한 것을 확인할 수 있습니다. 이 문서에서는 상황을 해결 하는 방법을 설명 합니다.

## <a name="cause"></a>원인

이 문제는 협상 유효성 검사에 실패 한 경우 발생할 수 있습니다. 이는 일반적으로 WAN 가속기가 원래 SMB NEGOTIATE 패킷을 수정 하기 때문에 발생 합니다.

Microsoft는 어떤 이유로 든 유효성 검사 협상 패킷 수정을 더 이상 허용 하지 않습니다. 이 동작은 심각한 보안 위험을 생성 하기 때문입니다.

다음 요구 사항은 Negotiate Negotiate 패킷에 적용 됩니다.

- Negotiate Validate 프로세스는 FSCTL\_유효성 검사\_협상\_정보 명령을 사용 합니다.

- Negotiate Validate 응답은 서명 되어야 합니다. 그렇지 않으면 연결이 중단 됩니다.

- FSCTL\_유효성 검사\_\_정보 메시지를 negotiate 메시지와 비교 하 여 변경 된 내용이 없는지 확인 해야 합니다.

## <a name="workaround"></a>해결 방법

협상 유효성 검사 프로세스를 일시적으로 사용 하지 않도록 설정할 수 있습니다. 이렇게 하려면 다음 레지스트리 하위 키를 찾습니다.

**HKEY\_로컬\_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\LanmanWorkstation\\매개 변수**

**매개 변수** 키 아래에서 **RequireSecureNegotiate** 을 **0**으로 설정 합니다.

Windows PowerShell에서 다음 명령을 실행 하 여이 값을 설정할 수 있습니다.

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanWorkstation\Parameters" RequireSecureNegotiate -Value 0 -Force
```

> [!NOTE]
> Windows 10, Windows Server 2016 또는 이후 버전의 Windows에서는 Negotiate Validate 프로세스를 사용 하지 않도록 설정할 수 없습니다.

클라이언트 또는 서버에서 Negotiate 유효성 검사 명령을 지원할 수 없는 경우 SMB 서명을 필수로 설정 하 여이 문제를 해결할 수 있습니다. SMB 서명은 협상의 유효성을 검사 하는 것 보다 더 안전 하 게 간주 됩니다. 그러나 서명이 필요한 경우 성능이 저하 될 수도 있습니다.

## <a name="reference"></a>참조

자세한 내용은 다음 문서를 참조하세요.

[3.3.5.15.12 Negotiate 정보 유효성 검사 요청을 처리 하는 방법](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/0b7803eb-d561-48a4-8654-327803f59ec6)

[3.2.5.14.12 Negotiate 정보 유효성 검사 응답을 처리 합니다.](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/6a5bc90d-3c08-4498-905b-e7dab30b2e0e)
