---
title: SMB 다이렉트를 사용 하 여 파일 서버의 성능 향상
description: Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016에서 SMB 다이렉트 기능에 설명 합니다.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed8fd5b4114fc9fd9c7dc278a98cea8cc67a8749
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239230"
---
# SMB 다이렉트

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016 라는 SMB 다이렉트 원격 직접 메모리 액세스 (RDMA) 기능이 있는 네트워크 어댑터의 사용을 지 원하는 기능을 포함 합니다. RDMA 된 네트워크 어댑터는 매우 적은 CPU를 사용 하는 동안 매우 짧은 대기 시간을 사용 하 여 전체 속도로 작동할 수 있습니다. Microsoft SQL Server 등 Hyper-v 워크 로드에 대 한이 통해 로컬 저장소와 유사 하 게 원격 파일 서버. SMB 다이렉트 포함 됩니다.

- 처리량 향상된: 네트워크 어댑터 많은 양의 데이터 행 속도로 전송을 조정 하는 고속 네트워크의 전체 처리량을 활용 합니다.
- 대기 시간이 낮은: 네트워크 요청에 대 한 매우 빠르게 응답을 제공 하 고 따라서 있으면 직접 연결 된 블록 저장소 것으로 생각 하는 원격 파일 저장소를 만듭니다.
- 낮은 CPU 사용률: 더 벗어났다가 네트워크를 통해 데이터를 전송 서버 응용 프로그램에 사용할 수 있는 전원 때 더 적은 CPU 주기를 사용 합니다.

SMB 다이렉트가 자동으로 구성 하 여 Windows Server 2012 R2 및 Windows Server 2012 합니다.

## SMB 다중 채널 및 SMB 다이렉트

SMB 다중 채널은 SMB 다이렉트를 사용 하도록 설정 하려면 네트워크 어댑터는 RDMA 기능 감지 담당 기능입니다. SMB 다중 채널 없이 SMB (모든 네트워크 어댑터는 RDMA 스택 새로 함께 TCP/IP 스택에 제공 하는 데 사용) 지원 RDMA 네트워크 어댑터를 사용 하 여 일반 TCP/IP를 사용 합니다.

SMB 다중 채널을 사용 하 여 SMB 네트워크 어댑터 RDMA 기능이 있는지 여부를 감지 하 다음 (인터페이스 마다 2)는 단일 세션에 대 한 여러 RDMA 연결을 만듭니다. 이 높은 처리량을 사용 하 여, 낮은 대기 시간 및 낮은 CPU 사용률 가능 RDMA 네트워크 어댑터에서 제공 하는 SMB 수 있습니다. 또한 여러 RDMA 인터페이스를 사용 하는 경우 내결함성을 제공 합니다.

>[!NOTE]
>네트워크 어댑터는 RDMA 기능을 사용 하려는 경우에 하지 가능 RDMA 네트워크 어댑터를 팀 해야 합니다. 협력을 하는 경우 네트워크 어댑터는 RDMA를 지원 하지 않습니다.
>하나 이상의 RDMA 네트워크 연결을 만든 후 원래 프로토콜 협상에 사용 되는 TCP/IP 연결이 사용 되지 않습니다. 그러나 RDMA 네트워크 연결에 실패할 경우 TCP/IP 연결이 유지 됩니다.

## 요구 사항

SMB 다이렉트 다음 필요합니다.

- Windows Server 2012 R2 또는 Windows Server 2012를 실행 하는 두 개 이상의 컴퓨터
- RDMA 기능을 사용 하 여 하나 이상의 네트워크 어댑터가입니다.

### SMB 다이렉트를 사용할 때 고려 사항

- 에서 사용할 수 있는 SMB 다이렉트 장애 조치 클러스터; 그러나 클라이언트 액세스에 사용 되는 클러스터 네트워크 SMB 다이렉트에 적합 한지 확인 해야 합니다. 장애 조치 클러스터링 여러 네트워크를 사용 하 여 클라이언트 액세스에 대 한 지원, 네트워크 어댑터와 함께 RSS (수신측)-지원 및 RDMA 지원 합니다.
- 사용할 수 있습니다 SMB 다이렉트 Hyper-v 관리 운영 체제에 SMB를 통해 Hyper-v를 사용 하 여 지원 하 고 Hyper-v 저장소 스택을 사용 하는 가상 컴퓨터에 저장소 제공. 그러나 가능 RDMA 네트워크 어댑터 Hyper-v 클라이언트에 직접 노출 되지 않습니다. 네트워크 어댑터는 RDMA를 사용할 수 있는 가상 스위치에 연결 하면 스위치에서 가상 네트워크 어댑터 RDMA 지원 되지 않습니다.
- SMB 다중 채널을 사용 하지 않도록 설정한 경우 SMB 다이렉트도 비활성화 됩니다. 네트워크 어댑터 접근 권한 값을 검색 하 고 네트워크 어댑터는 RDMA 지원 여부를 결정 하는 SMB 다중 채널, 이후 SMB 다이렉트 사용할 수 없습니다 클라이언트에서 SMB 다중 채널을 사용 하지 않도록 설정 하는 경우.
- SMB 다이렉트는 Windows 직각에서 지원 되지 SMB 다이렉트 지원이 필요 합니다. RDMA를 사용할 수 있는 네트워크 어댑터에 대 한 Windows Server 2012 R2 및 Windows Server 2012에서만 사용할 수 있습니다.
- 하위 수준 버전의 Windows Server에서 SMB 다이렉트 지원 되지 않습니다. Windows Server 2012 R2 및 Windows Server 2012 에서만 지원 됩니다.

## 활성화 및 SMB 다이렉트 비활성화

SMB 다이렉트는 기본적으로 Windows Server 2012 R2 또는 Windows Server 2012를 설치할 때 활성화 합니다. SMB 클라이언트는 자동으로 감지 하 고 적절 한 구성을 확인 되 면 여러 네트워크 연결을 사용 합니다.

### SMB 다이렉트 사용 하지 않도록 설정

하지만 일반적으로 SMB 다이렉트 사용 하지 않도록 설정할 필요가 없습니다, 다음 Windows PowerShell 스크립트 중 하나를 실행 하 여 비활성화할 수 있습니다.

RDMA 특정 인터페이스를 비활성화 하려면 다음을 입력 합니다.

```PowerShell
Disable-NetAdapterRdma <name>
```

모든 인터페이스에 대 한 RDMA를 비활성화 하려면 다음을 입력 합니다.

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Disabled
```

RDMA 클라이언트 또는 서버를 비활성화 하면 시스템은 사용할 수 없습니다. *네트워크 Direct* 는 Windows Server 2012 R2 및 Windows Server 2012 기본 네트워킹에 대 한 지원 RDMA 인터페이스에 대 한 내부 이름입니다.

### 다시 SMB 다이렉트 활성화

RDMA를 비활성화 한 후 다음 Windows PowerShell 스크립트 중 하나를 실행 하 여 그 다시 활성화할 수 있습니다.

RDMA 특정 인터페이스를 다시 사용 하려면 다음을 입력 합니다.

```PowerShell
Enable-NetAdapterRDMA <name>
```

RDMA 모든 인터페이스를 다시 사용 하려면 다음을 입력 합니다.

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Enabled
```

다시 사용 하기 시작 하는 클라이언트와 서버 모두에서 RDMA를 사용 하도록 설정 해야 합니다.

## SMB 다이렉트의 성능을 테스트합니다

다음 절차 중 하나를 사용 하 여 성능을 작동 하는 방법을 테스트할 수 있습니다.

### 비교 및 SMB 다이렉트를 사용 하지 않고 파일 복사

향상 된 SMB 다이렉트의 처리량을 측정 하는 방법은 다음과 같습니다.

1. SMB 다이렉트 구성
2. SMB 다이렉트를 사용 하 여 큰 파일 복사본을 실행 하는 시간을 측정 합니다.
3. 네트워크 어댑터에서 RDMA를 사용 하지 않도록 설정, [활성화 및 비활성화 SMB 다이렉트](#enabling-and-disabling-smb-direct)를 참조 하세요.
4. SMB 다이렉트를 사용 하지 않고 큰 파일 복사본을 실행 하는 시간을 측정 합니다.
5. 네트워크 어댑터에서 RDMA를 다시 활성화 한 다음 두 가지 결과 비교 합니다.
6. 캐시의 영향을 방지 하려면 다음을 수행 해야 합니다.
    1. 많은 양의 데이터 (메모리 처리 원하는 것 보다 더 많은 데이터)를 복사 합니다.
    2. 두 번 연습과 다음 두 번째 복사본을 타이밍으로 첫 번째 복사본을 사용 하 여 데이터를 복사 합니다.
    3. 서버와 비슷한 조건에서 작동 하는지 확인 하려면 각 테스트 하기 전에 클라이언트를 다시 시작 합니다.

### SMB 다이렉트를 사용 하 여 파일 복사 하는 동안 여러 네트워크 어댑터 중 하나에 실패

SMB 다이렉트에 장애 조치 기능을 확인 하는 방법은 다음과 같습니다.

1. SMB 다이렉트 작동 하는 여러 네트워크 어댑터 구성에서 확인 합니다.
2. 큰 파일 복사본을 실행 합니다. 복사를 실행 하는 동안 하나 케이블 연결을 끊어 (또는 네트워크 어댑터 중 하나를 사용 하지 않도록 설정 하 여) 네트워크 경로 중 하나에 장애가 시뮬레이트하십시오.
3. 나머지 네트워크 어댑터 중 하나를 사용 하 여 계속 파일을 복사 하 고 파일 복사 오류 없이 있는지 확인 합니다.

>[!NOTE]
>SMB 다이렉트를 사용 하지 않는 작업의 오류를 방지 하려면 다른 워크 로드의 연결이 끊긴된 네트워크 경로 사용 하 여 지를 확인 합니다.

## 자세한 정보

- [서버 메시지 블록 개요](file-server-smb-overview.md)
- [서버, 저장소 및 네트워크 가용성 증가: 시나리오 개요](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
