---
title: 수렴 형 NIC 구성 문제 해결
description: 이 항목은 Windows Server 2016에 대 한 수렴 형 NIC 구성 가이드의 일부입니다.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 297044397088bfb64b51e1553d3f69d5b933e81b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405894"
---
# <a name="troubleshooting-converged-nic-configurations"></a>수렴 형 NIC 구성 문제 해결

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 스크립트를 사용 하 여 Hyper-v 호스트에서 RDMA 구성이 올바른지 여부를 확인할 수 있습니다.

- [Test-Rdma 스크립트를 다운로드 합니다.](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

다음 Windows PowerShell 명령을 사용 하 여 수렴 형 Nic의 구성 문제를 해결 하 고 확인할 수도 있습니다.

## <a name="get-netadapterrdma"></a>NetAdapterRdma

네트워크 어댑터 RDMA 구성을 확인 하려면 Hyper-v 서버에서 다음 Windows PowerShell 명령을 실행 합니다.

    
    Get-NetAdapterRdma | fl *
    

Hyper-v 호스트에서이 명령을 실행 한 후 다음과 같은 예상 및 예기치 않은 결과를 사용 하 여 문제를 식별 하 고 해결할 수 있습니다.

### <a name="get-netadapterrdma-expected-results"></a>NetAdapterRdma 예상 결과

호스트 vNIC 및 실제 NIC는 0이 아닌 RDMA 기능을 표시 합니다.

![Windows PowerShell 예상 결과](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>NetAdapterRdma 예기치 않은 결과

**NetAdapterRdma** 명령을 실행할 때 예기치 않은 결과를 수신 하는 경우 다음 단계를 수행 합니다.

1. Mlnx 미니 포트 및 Mlnx 버스 드라이버가 최신 버전 인지 확인 합니다. Mellanox의 경우 최소한 drop 42을 사용 합니다. 
2. Device Manager를 통해 드라이버 버전을 확인 하 여 Mlnx 미니 포트 및 버스 드라이버가 일치 하는지 확인 합니다. 버스 드라이버는 시스템 장치에서 찾을 수 있습니다. 이 이름은 다음 네트워크 어댑터 속성의 스크린샷에 설명 된 대로 Mellanox 연결-X 3 PRO VPI로 시작 해야 합니다.

![네트워크 어댑터 속성](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. 실제 NIC와 호스트 vNIC 모두에서 네트워크 다이렉트 (RDMA)를 사용 하도록 설정 했는지 확인 합니다.
5. RDMA 기능을 확인 하 여 올바른 실제 어댑터에 대해 vSwitch를 만들었는지 확인 합니다.
6. EventViewer 시스템 로그를 확인 하 고 원본 "Hyper-v-VmSwitch"를 기준으로 필터링 합니다.

--- 

## <a name="get-smbclientnetworkinterface"></a>SmbClientNetworkInterface

RDMA 구성을 확인 하는 추가 단계로 Hyper-v 서버에서 다음 Windows PowerShell 명령을 실행 합니다.


    Get-SmbClientNetworkInterface

### <a name="get-smbclientnetworkinterface-expected-results"></a>SmbClientNetworkInterface 예상 결과

호스트 vNIC SMB 관점 에서도 RDMA 가능으로 표시 되어야 합니다.

![네트워크 어댑터 속성](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)


### <a name="get-smbclientnetworkinterface-unexpected-results"></a>SmbClientNetworkInterface 예기치 않은 결과

1. Mlnx 미니 포트 및 Mlnx 버스 드라이버가 최신 버전 인지 확인 합니다. Mellanox의 경우 최소한 drop 42을 사용 합니다. 
2. Device Manager를 통해 드라이버 버전을 확인 하 여 Mlnx 미니 포트 및 버스 드라이버가 일치 하는지 확인 합니다. 버스 드라이버는 시스템 장치에서 찾을 수 있습니다. 이 이름은 다음 네트워크 어댑터 속성의 스크린샷에 설명 된 대로 Mellanox 연결-X 3 PRO VPI로 시작 해야 합니다.
3. 실제 NIC와 호스트 vNIC 모두에서 네트워크 다이렉트 (RDMA)를 사용 하도록 설정 했는지 확인 합니다.
4. RDMA 기능을 확인 하 여 올바른 실제 어댑터를 통해 Hyper-v 가상 스위치를 만들었는지 확인 합니다.
5. 응용 프로그램 및 서비스에서 "SMB 클라이언트"에 대 한 EventViewer 로그를 확인 합니다. **| Microsoft | Windows**.

--- 

## <a name="get-netadapterqos"></a>Get-netadapterqos

다음 Windows PowerShell 명령을 실행 하 여 서비스 \(QoS\) 구성의 네트워크 어댑터 품질을 확인할 수 있습니다.

    Get-NetAdapterQos

### <a name="get-netadapterqos-expected-results"></a>Get-netadapterqos 예상 결과

우선 순위 및 트래픽 클래스는이 가이드를 사용 하 여 수행한 첫 번째 구성 단계에 따라 표시 되어야 합니다.

![서비스 품질 우선 순위 및 클래스](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-netadapterqos 예기치 않은 결과

예기치 않은 결과가 발생 하면 다음 단계를 수행 합니다.

1. 실제 네트워크 어댑터가 데이터 센터 브리징 \(DCB\) 및 QoS를 지원 하는지 확인 합니다.
2. 네트워크 어댑터 드라이버가 최신 상태 인지 확인 합니다.

--- 

## <a name="get-smbmultichannelconnection"></a>SmbMultiChannelConnection

다음 Windows PowerShell 명령을 사용 하 여 원격 노드의 IP 주소가 RDMA\-지원 인지 확인할 수 있습니다.

    Get-SmbMultiChannelConnection


### <a name="get-smbmultichannelconnection-expected-results"></a>SmbMultiChannelConnection 예상 결과

원격 노드의 IP 주소는 RDMA 가능으로 표시 됩니다.

![RDMA 지원 원격 노드 IP 주소](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>SmbMultiChannelConnection 예기치 않은 결과

예기치 않은 결과가 발생 하면 다음 단계를 수행 합니다.

1. Ping이 두 가지 방식으로 작동 하는지 확인 합니다.
2. 방화벽이 SMB 연결 시작을 차단 하지 않는지 확인 합니다. 특히 iWARP 및 445에 대해 SMB 다이렉트 포트 5445에 대 한 방화벽 규칙을 사용 하도록 설정 합니다.

--- 

## <a name="get-smbclientnetworkinterface"></a>SmbClientNetworkInterface

다음 명령을 사용 하 여 rdma에 대해 사용 하도록 설정한 가상 NIC가 SMB에서 지 원하는 rdma\-로 보고 되는지 확인할 수 있습니다.

    Get-SmbClientNetworkInterface


### <a name="get-smbclientnetworkinterface-expected-results"></a>SmbClientNetworkInterface 예상 결과

RDMA에 대해 사용 하도록 설정 된 가상 NIC는 SMB에서 지 원하는 RDMA로 표시 되어야 합니다.

![Nic가 RDMA를 사용할 수 있음을 보고 합니다.](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>SmbClientNetworkInterface 예기치 않은 결과

예기치 않은 결과가 발생 하면 다음 단계를 수행 합니다.

1. Ping이 두 가지 방식으로 작동 하는지 확인 합니다.
2. 방화벽이 SMB 연결 시작을 차단 하지 않는지 확인 합니다.

--- 

## <a name="vstat-mellanox-specific"></a>vstat \(Mellanox 특정\)

Mellanox 네트워크 어댑터를 사용 하는 경우 **vstat** 명령을 사용 하 여 hyper-v 노드에서 수렴 된 이더넷 \(roce\) 버전을 통해 RDMA를 확인할 수 있습니다.

### <a name="vstat-expected-results"></a>vstat 예상 결과

두 노드의 RoCE 버전은 동일 해야 합니다. 이는 두 노드의 펌웨어 버전이 최신 인지 확인 하는 좋은 방법 이기도 합니다.

![RoCE 버전 검사 결과 예](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>vstat 예기치 않은 결과

예기치 않은 결과가 발생 하면 다음 단계를 수행 합니다.

1. MlnxDriverCoreSetting를 사용 하 여 올바른 RoCE 버전 설정
2. Mellanox 웹 사이트에서 최신 펌웨어를 설치 합니다.

--- 

## <a name="perfmon-counters"></a>Perfmon 카운터

성능 모니터에서 카운터를 검토 하 여 구성의 RDMA 활동을 확인할 수 있습니다.

![성능 모니터 결과 예](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

--- 

## <a name="related-topics"></a>관련 항목

- [단일 네트워크 어댑터를 사용 하 여 수렴 형 NIC 구성](cnic-single.md)
- [수렴 형 NIC 팀 NIC 구성](cnic-datacenter.md)
- [수렴 형 NIC에 대 한 물리적 스위치 구성](cnic-app-switch-config.md)

---
