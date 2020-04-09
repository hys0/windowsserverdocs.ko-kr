---
title: SMB 연결 중 TCP 3 방향 핸드셰이크 오류
description: SMB 연결 중 TCP 3 방향 핸드셰이크 오류를 소개 합니다.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: cb88fa89344172cfc1ed036865a4496ed73e9a22
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815326"
---
# <a name="tcp-three-way-handshake-failure-during-smb-connection"></a>SMB 연결 중 TCP 3 방향 핸드셰이크 오류

네트워크 추적을 분석할 때 SMB 문제가 발생 하도록 하는 TCP (전송 제어 프로토콜) 3 방향 핸드셰이크 오류가 발생 한 것을 알 수 있습니다. 이 문서에서는 이러한 상황을 해결 하는 방법을 설명 합니다.

## <a name="troubleshooting"></a>문제 해결

일반적으로 원인은 트래픽을 차단 하는 로컬 또는 인프라 방화벽입니다. 이 문제는 다음 시나리오 중 하나에서 발생할 수 있습니다.

## <a name="scenario-1"></a>시나리오 1

TCP SYN 패킷은 SMB 서버에 도착 하지만 SMB 서버는 TCP SYN ACK 패킷을 반환 하지 않습니다.

이 시나리오를 해결 하려면 다음 단계를 수행 합니다.

### <a name="step-1"></a>1단계

**Netstat** 또는 **NetTcpConnection** 를 실행 하 여 시스템 프로세스가 소유 해야 하는 TCP 포트 445에 수신기가 있는지 확인 합니다.

```cmd
netstat -ano | findstr :445
```

```PowerShell
Get-NetTcpConnection -LocalPort 445
```

### <a name="step-2"></a>2단계

서버 서비스가 시작 되 고 실행 중인지 확인 합니다.

### <a name="step-3"></a>3단계

WFP (Windows 필터링 플랫폼) 캡처를 사용 하 여 트래픽을 삭제 하는 규칙 또는 프로그램을 확인 합니다. 이렇게 하려면 명령 프롬프트 창에서 다음 명령을 실행 합니다.

```cmd
netsh wfp capture start
```

문제를 재현 한 후 다음 명령을 실행 합니다.

```cmd
netsh wfp capture stop
```

시나리오 추적을 실행 하 고 SMB 트래픽 (TCP 포트 445)에서 WFP 삭제를 찾습니다.

필요에 따라 항상 WFP 기반이 아니기 때문에 바이러스 백신 프로그램을 제거할 수 있습니다.

### <a name="step-4"></a>4단계

Windows 방화벽을 사용 하는 경우 방화벽 로깅을 사용 하도록 설정 하 여 트래픽 삭제를 기록 하는지 여부를 확인 합니다.

**고급 보안이 포함 된 Windows 방화벽** \> **인바운드 규칙**에서 적절 한 "파일 및 프린터 공유 (SMB)" 규칙을 사용 하도록 설정 했는지 확인 합니다.

> [!NOTE]
> 컴퓨터를 설정 하는 방법에 따라 "windows 방화벽"을 "Windows Defender 방화벽" 이라고 합니다.

## <a name="scenario-2"></a>시나리오 2

TCP SYN 패킷은 SMB 서버에 도달 하지 않습니다.

이 시나리오에서는 네트워크 경로를 따라 장치를 조사 해야 합니다. 각 장치에서 캡처된 네트워크 추적을 분석 하 여 트래픽을 차단 하는 장치를 확인할 수 있습니다.
