---
title: SMB 다중 채널 문제 해결
description: SMB 다중 채널 문제 해결 방법을 소개 합니다.
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 91f034a0062f509b1185f04554af4383022a68e1
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654544"
---
# <a name="smb-multichannel-troubleshooting"></a>SMB 다중 채널 문제 해결

이 문서에서는 SMB 다중 채널과 관련 된 문제를 해결 하는 방법을 설명 합니다.

## <a name="check-the-network-interface-status"></a>네트워크 인터페이스 상태를 확인 합니다.

SMB 클라이언트 (MS\_클라이언트) 및 SMB 서버 (MS\_서버)에서 네트워크 인터페이스에 대 한 바인딩이 **True** 로 설정 되어 있는지 확인 합니다. 다음 명령을 실행 하면 출력에 두 네트워크 인터페이스에 대해 모두 **사용** 아래에서 **True** 가 표시 됩니다.

```PowerShell
Get-NetAdapterBinding -ComponentID ms_server,ms_msclient
```

그런 다음 네트워크 인터페이스가 다음 명령의 출력에 표시 되는지 확인 합니다.

```PowerShell
Get-SmbServerNetworkInterface
```

```PowerShell
Get-SmbClientNetworkInterface
```

**Get-netadapter** 명령을 실행 하 여 인터페이스 인덱스를 확인 하 고 결과를 확인할 수도 있습니다. 인터페이스 인덱스는 적절 한 인터페이스에 적극적으로 바인딩되는 모든 활성 SMB 어댑터를 표시 합니다.

## <a name="check-the-firewall"></a>방화벽 확인

링크-로컬 IP 주소만 있고 공개적으로 라우팅할 수 없는 경우 네트워크 프로필은 **공용**으로 설정 될 가능성이 높습니다. 이는 기본적으로 SMB가 방화벽에서 차단 됨을 의미 합니다.

다음 명령을 사용 하 여 사용 중인 연결 프로필을 표시 합니다. 네트워크 및 공유 센터를 사용 하 여이 정보를 검색할 수도 있습니다.

**Get NetConnectionProfile**

**파일 및 프린터 공유** 그룹 아래에서 방화벽 인바운드 규칙을 확인 하 여 올바른 프로필에 대해 "SMB 인"이 사용 하도록 설정 되어 있는지 확인 합니다.

![SMB 인 규칙](media/smb-multichannel-troubleshooting-1.png)

**네트워크 및 공유 센터** 창에서 **파일 및 프린터 공유** 를 사용 하도록 설정할 수도 있습니다. 이렇게 하려면 왼쪽 메뉴에서 **고급 공유 설정 변경** 을 선택한 다음 프로필에 대 한 **파일 및 프린터 공유 켜기** 를 선택 합니다. 이 옵션은 파일 및 프린터 공유 방화벽 규칙을 사용 하도록 설정 합니다.

![네트워크에 연결된 장치의 자동 설치를 사용하도록 설정할지를](media/smb-multichannel-troubleshooting-2.png)

## <a name="capture-client-and-server-sided-traffic-for-troubleshooting"></a>문제 해결을 위해 클라이언트 및 서버 측면 트래픽 캡처

TCP 3 방향 핸드셰이크에서 시작 하는 SMB 연결 추적 정보가 필요 합니다. 캡처를 시작 하기 전에 모든 응용 프로그램 (특히 Windows 탐색기)을 닫는 것이 좋습니다. SMB 클라이언트에서 **워크스테이션** 서비스를 다시 시작 하 고 패킷 캡처를 시작한 다음 문제를 재현 합니다.

SMBv3 연결이 협상 되 고 있고 서버와 클라이언트 사이에 있는 어떤 항목도 언어 협상에 영향을 주는지 확인*합니다.* SMBv2 및 이전 버전은 다중 채널을 지원 하지 않습니다.

네트워크\_인터페이스\_정보 패킷을 찾습니다. Smb 클라이언트가 SMB 서버에서 어댑터 목록을 요청 하는 위치입니다. 이러한 패킷을 교환 하지 않으면 다중 채널이 작동 하지 않습니다.

서버는 유효한 네트워크 인터페이스 목록을 반환 하 여 응답 합니다. 그런 다음 SMB 클라이언트는 다중 채널에 사용할 수 있는 어댑터 목록에 추가 합니다. 이 시점에서 다중 채널을 시작 하 고 최소한 연결을 시작 해야 합니다.

자세한 내용은 다음 문서를 참조하세요.

- [서버 네트워크 인터페이스를 쿼리 하는 3.2.4.20.10 응용 프로그램 요청](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/147adde4-d936-4597-924a-8caa3429c6b0)

- [2.2.32.5 NETWORK\_인터페이스\_정보 응답](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/fcd862d1-1b85-42df-92b1-e103199f531f)

- [네트워크 인터페이스 응답을 처리 하는 3.2.5.14.11](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/5459722b-1eaa-4ead-b465-284363264cad)

다음 시나리오에서는 어댑터를 사용할 수 없습니다.

- 클라이언트에 라우팅 문제가 있습니다. 이 문제는 일반적으로 잘못 된 인터페이스를 통해 트래픽을 강제로 수행 하는 잘못 된 라우팅 테이블에 의해 발생 합니다.

- 다중 채널 제약 조건이 설정 되었습니다. 자세한 내용은 [SmbMultichannelConstraint](https://docs.microsoft.com/powershell/module/smbshare/new-smbmultichannelconstraint)를 참조 하세요.

- 네트워크 인터페이스 요청 및 응답 패킷을 차단한 항목이 있습니다.

- 클라이언트와 서버는 추가 네트워크 인터페이스를 통해 통신할 수 없습니다. 예를 들어 TCP 3 방향 핸드셰이크가 실패 했거나, 방화벽이 방화벽에 의해 차단 되 고, 세션을 설정 하지 못했습니다.

서버에서 보낸 목록에 어댑터와 해당 IPv6 주소가 있는 경우 다음 단계는 해당 인터페이스를 통해 통신이 시도 되는지 여부를 확인 하는 것입니다. 링크-로컬 주소 및 SMB 트래픽으로 추적을 필터링 하 고 연결 시도를 찾습니다. NetConnection 추적 인 경우에는 WFP (Windows 필터링 플랫폼) 이벤트를 검토 하 여 연결이 차단 되 고 있는지 여부를 확인할 수도 있습니다.
