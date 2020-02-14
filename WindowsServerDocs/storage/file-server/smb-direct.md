---
title: SMB 다이렉트를 사용하여 파일 서버의 성능 향상
description: Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016의 SMB 다이렉트 기능에 대해 설명합니다.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 41126aa0d054607449d57928c1777679e5087e73
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394462"
---
# <a name="smb-direct"></a>SMB 다이렉트

>적용 대상: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

Windows Server 2012 R2, Windows Server 2012 및 Windows Server 2016에는 RDMA(원격 직접 메모리 액세스) 기능이 있는 네트워크 어댑터 사용을 지원하는 SMB 다이렉트라는 기능이 포함되어 있습니다. RDMA 기능이 있는 네트워크 어댑터는 대기 시간이 매우 짧으면서 최대 속도로 작동할 수 있는 동시에 CPU 사용량은 매우 적습니다. Hyper-V 또는 Microsoft SQL Server 등의 워크로드에 이 기능을 사용하면 원격 파일 서버가 로컬 스토리지와 비슷한 역할을 할 수 있습니다. SMB 다이렉트의 기능은 다음과 같습니다.

- 향상된 처리량: 네트워크 어댑터가 회선 속도로 대량의 데이터 전송을 조정하는 고속 네트워크의 최대 처리량을 활용합니다.
- 낮은 대기 시간: 네트워크 요청에 대해 매우 빠른 응답을 제공하므로 원격 파일 스토리지가 직접 연결된 블록 스토리지처럼 느껴집니다.
- 낮은 CPU 사용률: 네트워크를 통해 데이터를 전송할 때 적은 CPU 주기를 사용하므로 서버 애플리케이션에서 더 많은 전원을 사용할 수 있습니다.

SMB 다이렉트는 Windows Server 2012 R2 및 Windows Server 2012에 의해 자동으로 구성됩니다.

## <a name="smb-multichannel-and-smb-direct"></a>SMB 다중 채널 및 SMB 다이렉트

SMB 다중 채널은 네트워크 어댑터의 RDMA 기능을 검색하여 SMB 다이렉트를 사용할 수 있도록 하는 기능입니다. SMB 다중 채널이 없는 경우 SMB는 RDMA 가능 네트워크 어댑터와 일반 TCP/IP를 사용합니다(모든 네트워크 어댑터는 새로운 RDMA 스택과 함께 TCP/IP 스택을 제공함).

SMB 다중 채널이 있는 경우 SMB는 네트워크 어댑터에 RDMA 기능이 있는지를 검색한 다음, 해당 단일 세션에 대해 여러 RDMA 연결을 만듭니다(인터페이스당 두 개). 이를 통해 SMB는 RDMA 가능 네트워크 어댑터에서 제공하는 높은 처리량, 짧은 대기 시간 및 낮은 CPU 사용률을 사용할 수 있습니다. 또한 여러 RDMA 인터페이스를 사용 중인 경우 SMB는 결함 허용을 제공합니다.

>[!NOTE]
>네트워크 어댑터의 RDMA 기능을 사용하려는 경우 RDMA 가능 네트워크 어댑터를 팀으로 구성하면 안 됩니다. 팀으로 구성하면 네트워크 어댑터가 RDMA를 지원하지 않습니다.
>하나 이상의 RDMA 네트워크 연결을 만들고 나면 원래 프로토콜 협상에 사용된 TCP/IP 연결은 더 이상 사용되지 않습니다. 그러나 RDMA 네트워크 연결이 실패할 경우를 대비하여 TCP/IP 연결은 보존됩니다.

## <a name="requirements"></a>요구 사항

SMB 다이렉트에는 다음이 필요합니다.

- Windows Server 2012 R2 또는 Windows Server 2012를 실행하는 두 대 이상의 컴퓨터
- RDMA 기능이 있는 하나 이상의 네트워크 어댑터

### <a name="considerations-when-using-smb-direct"></a>SMB 다이렉트 사용 시 고려 사항

- 장애 조치(failover) 클러스터에서 SMB 다이렉트를 사용할 수는 있지만 클라이언트 액세스에 사용되는 클러스터 네트워크가 SMB 다이렉트에 적절한지 확인해야 합니다. 장애 조치(failover) 클러스터링은 RSS(수신측 배율) 가능 및 RDMA 가능인 네트워크 어댑터와 함께 클라이언트 액세스에 여러 네트워크를 사용하는 것을 지원합니다.
- Hyper-V 관리 운영 체제에서 SMB 다이렉트를 사용하여 SMB를 통한 Hyper-V 사용을 지원하고, Hyper-V 스토리지 스택을 사용하는 가상 머신에 스토리지를 제공할 수 있습니다. 그러나 RDMA 가능 네트워크 어댑터는 Hyper-V 클라이언트에 직접 표시되지 않습니다. RDMA 가능 네트워크 어댑터를 가상 스위치에 연결하는 경우 해당 스위치의 가상 네트워크 어댑터는 RDMA 가능이 아닙니다.
- SMB 다중 채널을 사용하지 않도록 설정하면 SMB 다이렉트도 사용하지 않도록 설정됩니다. SMB 다중 채널은 네트워크 어댑터 기능을 검색하여 네트워크 어댑터가 RDMA 가능인지를 확인하므로 SMB 다중 채널이 사용하지 않도록 설정된 경우 클라이언트가 SMB 다이렉트를 사용할 수 없습니다.
- SMB 다이렉트는 Windows RT에서 지원되지 않습니다. SMB 다이렉트는 Windows Server 2012 R2 및 Windows Server 2012에서만 제공되는 RDMA 지원 네트워크 어댑터에 대한 지원이 필요합니다.
- SMB 다이렉트는 버전이 낮은 Windows Server에서는 지원되지 않습니다. Windows Server 2012 R2 및 Windows Server 2012에서만 지원됩니다.

## <a name="enabling-and-disabling-smb-direct"></a>SMB 다이렉트 사용 및 사용 안 함

SMB 다이렉트는 Windows Server 2012 R2 또는 Windows Server 2012가 설치되면 기본적으로 실행됩니다. 적절한 구성이 식별된 경우 SMB 클라이언트는 자동으로 여러 네트워크 연결을 검색하고 사용합니다.

### <a name="disable-smb-direct"></a>SMB 다이렉트 사용 안 함

일반적으로 SMB 다이렉트를 사용하지 않도록 설정할 필요는 없지만 다음 Windows PowerShell 스크립트 중 하나를 실행하여 SMB 다이렉트를 사용하지 않도록 설정할 수 있습니다.

특정 인터페이스에 대해 RDMA를 사용하지 않도록 설정하려면 다음을 입력합니다.

```PowerShell
Disable-NetAdapterRdma <name>
```

모든 인터페이스에 대해 RDMA를 사용하지 않도록 설정하려면 다음을 입력합니다.

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Disabled
```

클라이언트나 서버 어느 한쪽에서 RDMA를 사용하지 않도록 설정하면 시스템에서 RDMA를 사용할 수 없습니다. *네트워크 다이렉트*는 RDMA 인터페이스에 대한 Windows Server 2012 R2 및 Windows Server 2012 기본 네트워킹 지원의 내부 이름입니다.

### <a name="re-enable-smb-direct"></a>SMB 다이렉트 다시 사용

RDMA를 사용하지 않도록 설정한 후 다음 Windows PowerShell 스크립트 중 하나를 실행하여 RDMA를 다시 사용하도록 설정할 수 있습니다.

특정 인터페이스에 대해 RDMA를 다시 사용하도록 설정하려면 다음을 입력합니다.

```PowerShell
Enable-NetAdapterRDMA <name>
```

모든 인터페이스에 대해 RDMA를 다시 사용하도록 설정하려면 다음을 입력합니다.

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Enabled
```

RDMA를 다시 사용하려면 클라이언트와 서버 둘 다에서 RDMA를 사용하도록 설정해야 합니다.

## <a name="test-performance-of-smb-direct"></a>SMB 다이렉트의 성능 테스트

다음 절차 중 하나를 사용하여 성능을 테스트할 수 있습니다.

### <a name="compare-a-file-copy-with-and-without-using-smb-direct"></a>SMB 다이렉트를 사용한 경우와 사용하지 않은 경우의 파일 복사 비교

SMB 다이렉트의 향상된 처리량을 측정하는 방법은 다음과 같습니다.

1. SMB 다이렉트를 구성합니다.
2. SMB 다이렉트를 사용하여 큰 파일 복사를 실행하는 데 걸리는 시간을 측정합니다.
3. 네트워크 어댑터에서 RDMA를 사용하지 않도록 설정하려면 [Enabling and disabling SMB Direct](#enabling-and-disabling-smb-direct)을 참조하세요.
4. SMB 다이렉트를 사용하지 않고 큰 파일 복사를 실행하는 데 걸리는 시간을 측정합니다.
5. 네트워크 어댑터에서 RDMA를 다시 사용하도록 설정한 다음 두 결과를 비교합니다.
6. 캐싱의 영향을 방지하려면 다음을 수행해야 합니다.
    1. 많은 양의 데이터(메모리가 처리할 수 있는 양 이상의 데이터)를 복사합니다.
    2. 데이터를 두 번 복사합니다. 첫 번째 복사는 연습으로 수행하고 두 번째 복사를 수행합니다.
    3. 각 테스트 전에 서버와 클라이언트를 둘 다 다시 시작하여 서버와 클라이언트가 유사한 조건에서 작동하도록 합니다.

### <a name="fail-one-of-multiple-network-adapters-during-a-file-copy-with-smb-direct"></a>SMB 다이렉트를 사용하여 파일 복사를 수행하는 동안 여러 네트워크 어댑터 중 하나에서 오류 발생

SMB 다이렉트의 장애 조치(failover) 기능을 확인하는 방법은 다음과 같습니다.

1. SMB 다이렉트가 여러 네트워크 어댑터 구성에서 작동하고 있는지 확인합니다.
2. 큰 파일 복사를 실행합니다. 복사가 실행되고 있는 동안 케이블 중 하나를 분리하거나 네트워크 어댑터 중 하나를 사용하지 않도록 설정하여 네트워크 경로 중 하나에서 오류를 시뮬레이트합니다.
3. 나머지 네트워크 어댑터 중 하나를 사용하여 파일 복사가 계속되는지 확인하고 파일 복사 오류가 없는지 확인합니다.

>[!NOTE]
>SMB 다이렉트를 사용하지 않는 워크로드의 오류를 방지하려면 연결이 끊어진 네트워크 경로를 사용하는 다른 워크로드가 없는지 확인합니다.

## <a name="more-information"></a>자세한 정보

- [Server Message Block 개요](file-server-smb-overview.md)
- [서버, 스토리지 및 네트워크 가용성 증가: 시나리오 개요](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [SMB를 통한 Hyper-V 배포](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
