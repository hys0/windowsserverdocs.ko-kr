---
title: 수렴 형 NIC 구성 문제 해결
description: 이 항목은 수렴 된 NIC 구성 가이드에 대 한 Windows Server 2016의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3004ff9d6fe874410c24d174755a6d26f99f8f2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876484"
---
# <a name="troubleshooting-converged-nic-configurations"></a>수렴 형 NIC 구성 문제 해결

>적용 대상: Windows Server (반기 채널), Windows Server 2016

RDMA 구성에서 Hyper-v 호스트에서 올바른지 여부를 확인 하려면 다음 스크립트를 사용할 수 있습니다.

- [테스트 Rdma.ps1 스크립트 다운로드](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

문제를 해결 하 고 프로그램 수렴 된 Nic의 구성을 확인 하려면 다음 Windows PowerShell 명령을 이용할 수 있습니다.

## <a name="get-netadapterrdma"></a>Get-NetAdapterRdma

네트워크 어댑터가 RDMA 구성을 확인 하려면 Hyper-v 서버에서 다음 Windows PowerShell 명령을 실행 합니다.

    
    Get-NetAdapterRdma | fl *
    

다음 예상 및 예기치 않은 결과 확인 하 고 Hyper-v 호스트에서이 명령을 실행 한 후 문제를 해결에 사용할 수 있습니다.

### <a name="get-netadapterrdma-expected-results"></a>Get-NetAdapterRdma 예상 결과

호스트 vNIC와 실제 NIC 0이 아닌 RDMA 기능을 보여 줍니다.

![Windows PowerShell 예상 결과](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Get-NetAdapterRdma 예기치 않은 결과

실행할 때 예기치 않은 결과 검색 하는 경우 다음 단계를 수행 합니다 **Get NetAdapterRdma** 명령입니다.

1. Mlnx 미니 포트 및 Mlnx 버스 드라이버 최신 인지 확인 합니다. Mellanox에 대 한 사용 하 여 42 이상 삭제 합니다. 
2. 장치 관리자를 통해 드라이버 버전을 확인 하 여 Mlnx 미니 포트 및 버스 드라이버와 일치 하는지 확인 합니다. 시스템 장치에 bus 드라이버를 찾을 수 있습니다. 네트워크 어댑터 속성의 다음 스크린 샷에 표시 된 것과 같이 이름 Mellanox-Connect-X 3 PRO VPI 시작 해야 합니다.

![네트워크 어댑터 속성](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. 네트워크 다이렉트 (RDMA)를 실제 NIC와 호스트 vNIC에서 사용할 수 있는지 확인 하십시오.
5. RDMA 기능을 확인 하 여 오른쪽 실제 어댑터를 통해 vSwitch를 만드는 지 확인 합니다.
6. EventViewer 시스템 로그 및 원본 "하이퍼-V-VmSwitch"에서 필터를 확인 합니다.

--- 

## <a name="get-smbclientnetworkinterface"></a>Get-SmbClientNetworkInterface

RDMA 구성을 확인 하려면 추가 단계로, Hyper-v 서버에서 다음 Windows PowerShell 명령을 실행 합니다.


    Get-SmbClientNetworkInterface

### <a name="get-smbclientnetworkinterface-expected-results"></a>Get-SmbClientNetworkInterface 예상 결과

호스트 vNIC는 SMB의 관점 에서도 RDMA 지원으로 표시 됩니다.

![네트워크 어댑터 속성](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)


### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface 예기치 않은 결과

1. Mlnx 미니 포트 및 Mlnx 버스 드라이버 최신 인지 확인 합니다. Mellanox에 대 한 사용 하 여 42 이상 삭제 합니다. 
2. 장치 관리자를 통해 드라이버 버전을 확인 하 여 Mlnx 미니 포트 및 버스 드라이버와 일치 하는지 확인 합니다. 시스템 장치에 bus 드라이버를 찾을 수 있습니다. 네트워크 어댑터 속성의 다음 스크린 샷에 표시 된 것과 같이 이름 Mellanox-Connect-X 3 PRO VPI 시작 해야 합니다.
3. 네트워크 다이렉트 (RDMA)를 실제 NIC와 호스트 vNIC에서 사용할 수 있는지 확인 하십시오.
4. RDMA 기능을 확인 하 여 오른쪽 실제 어댑터를 통해 Hyper-v 가상 스위치를 만드는 지 확인 합니다.
5. EventViewer 로그 "SMB 클라이언트" 확인 **응용 프로그램 및 서비스 | Microsoft | Windows**합니다.

--- 

## <a name="get-netadapterqos"></a>Get-NetAdapterQos

서비스의 네트워크 어댑터 품질을 볼 수 있습니다 \(QoS\) 다음 Windows PowerShell 명령을 실행 하 여 구성 합니다.

    Get-NetAdapterQos

### <a name="get-netadapterqos-expected-results"></a>Get-netadapterqos 예상 결과

이 가이드를 사용 하 여 수행한 첫 번째 구성 단계에 따라 우선 순위 및 트래픽 클래스를 표시 되어야 합니다.

![서비스 우선 순위 및 클래스의 품질](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-netadapterqos 예기치 않은 결과

결과 예기치 않은 경우 다음 단계를 수행 합니다.

1. 실제 네트워크 어댑터를 데이터 센터 브리징을 지원 하는지 확인 하십시오 \(DCB\) 및 QoS
2. 네트워크 어댑터 드라이버가 최신 인지 확인 합니다.

--- 

## <a name="get-smbmultichannelconnection"></a>Get-SmbMultiChannelConnection

다음 Windows PowerShell 명령을 사용 하 여 RDMA 원격 노드의 IP 주소 인지 확인 하려면\-가능 합니다.

    Get-SmbMultiChannelConnection


### <a name="get-smbmultichannelconnection-expected-results"></a>Get-SmbMultiChannelConnection 예상 결과

원격 노드의 IP 주소 수 있는 RDMA로 표시 됩니다.

![RDMA 가능 원격 노드 IP 주소](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Get-SmbMultiChannelConnection 예기치 않은 결과

결과 예기치 않은 경우 다음 단계를 수행 합니다.

1. Ping 두 가지 방식으로 작동 하는지 확인 합니다.
2. 방화벽이 SMB 연결 시작을 차단 하 고 있지 있는지 확인 합니다. 특히 5445 iWARP에 대 한 포트를 SMB 다이렉트에 대 한 방화벽 규칙 및 445 ROCE에 대해 사용 하도록 설정 합니다.

--- 

## <a name="get-smbclientnetworkinterface"></a>Get-SmbClientNetworkInterface

다음 명령을 사용 하 여 가상 NIC를 사용 하는 RDMA는 rdma 보고에 대 한 확인\-SMB가 가능 합니다.

    Get-SmbClientNetworkInterface


### <a name="get-smbclientnetworkinterface-expected-results"></a>Get-SmbClientNetworkInterface 예상 결과

RDMA에 사용 하도록 설정 된 가상 NIC SMB에서 RDMA 지원으로 표시 되어야 합니다.

![SMB는 RDMA 지원 크기는 Nic를 보고](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface 예기치 않은 결과

결과 예기치 않은 경우 다음 단계를 수행 합니다.

1. Ping 두 가지 방식으로 작동 하는지 확인 합니다.
2. 방화벽이 SMB 연결 시작 했는지 확인 합니다.

--- 

## <a name="vstat-mellanox-specific"></a>vstat \(Mellanox 관련\)

Mellanox 네트워크 어댑터를 사용 하는 경우 사용할 수 있습니다 합니다 **vstat** 명령을 사용 하는 RDMA over Converged Ethernet 확인 \(RoCE\) Hyper-v 노드의 버전.

### <a name="vstat-expected-results"></a>vstat 예상 결과

두 노드에서 모두 RoCE 버전이 동일 해야 합니다. 두 노드에서 모두 펌웨어 버전이 최신 인지 확인 하는 좋은 방법 이기도 합니다.

![RoCE 버전 확인 결과 예](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>vstat 예기치 않은 결과

결과 예기치 않은 경우 다음 단계를 수행 합니다.

1. MlnxDriverCoreSetting 집합을 사용 하 여 올바른 RoCE 버전 설정
2. Mellanox 웹 사이트에서 최신 펌웨어를 설치 합니다.

--- 

## <a name="perfmon-counters"></a>Perfmon 카운터

구성의 RDMA 활동을 확인 하려면 성능 모니터 카운터를 검토할 수 있습니다.

![성능 모니터 결과 예제](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

--- 

## <a name="related-topics"></a>관련 항목

- [단일 네트워크 어댑터로 수렴 형 된 NIC 구성](cnic-single.md)
- [수렴 형 된 NIC 팀으로 구성 된 NIC 구성](cnic-datacenter.md)
- [수렴 형 된 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)

---
