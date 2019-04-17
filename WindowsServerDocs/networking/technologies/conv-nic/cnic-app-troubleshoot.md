---
title: NIC 구성 수렴 문제 해결
description: 이 항목은 Windows Server 2016 용 수렴 NIC 구성 가이드의 일부입니다.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 373ecd9b9fff62aaabd8caa176ff091ec98ad81c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-converged-nic-configurations"></a>NIC 구성 수렴 문제 해결

>적용 대상: Windows Server (세미콜론 연간 채널) Windows Server 2016

Hyper-v 호스트 RDMA 구성 올바른지 확인 하려면 다음 스크립트를 사용할 수 있습니다.

- [스크립트 Test-Rdma.ps1 다운로드](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

또한 집약된 Nic 구성을 확인 하 고 문제를 해결 하는 다음과 같은 Windows PowerShell 명령을 사용할 수 있습니다.

## <a name="get-netadapterrdma"></a>Get-NetAdapterRdma

네트워크 어댑터 RDMA 구성을 확인 하려면 Hyper-v 서버에 다음과 같은 Windows PowerShell 명령을 실행 합니다.

    
    Get-NetAdapterRdma | fl *
    

확인 하 고 Hyper-v 호스트에서이 명령을 실행 하면 문제가 해결 예상 다음 및 예기치 않게 결과 사용할 수 있습니다.

### <a name="get-netadapterrdma-expected-results"></a>Get-NetAdapterRdma 결과를 필요합니다.

호스트 vNIC와 물리적 NIC 0이 아닌 RDMA 기능이 표시 됩니다.

![Windows PowerShell 결과를 필요합니다.](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Get-NetAdapterRdma 예기치 않게 결과

실행할 때 예상치 결과가 경우 다음 단계를 수행는 **Get NetAdapterRdma** 명령을 합니다.

1. Mlnx 미니 및 Mlnx 버스 드라이버는 최신 있는지 확인 합니다. Mellanox에 대 한 사용 하 여 최소 42를 삭제 합니다. 
2. 장치 관리자를 통해 드라이버 버전을 확인 하 여 Mlnx 미니 및 버스 드라이버와 일치 하는지 확인 합니다. 시스템 장치에서 버스 드라이버를 찾을 수 있습니다. 네트워크 어댑터 속성의 다음 스크린샷와 같이 Mellanox Connect-X 3 PRO VPI 된 이름이 시작 해야 합니다.

![네트워크 어댑터 속성](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. 실제 NIC와 호스트 vNIC에서 네트워크 직접 (RDMA)을 사용할 수 있는지 확인 합니다.
5. VSwitch RDMA 기능을 확인 하 여 실제 바로 어댑터를 통해 만들어집니다 있는지 확인 합니다.
6. 이벤트 시스템 로그와 "하이퍼 V VmSwitch" 소스에서 필터를 확인 하세요.

## <a name="get-smbclientnetworkinterface"></a>SmbClientNetworkInterface 받기

RDMA 구성 되었는지 확인 하려면 추가 단계로, Hyper-v 서버에 다음과 같은 Windows PowerShell 명령을 실행 합니다.


    Get SmbClientNetworkInterface

### <a name="get-smbclientnetworkinterface-expected-results"></a>SmbClientNetworkInterface 예상한 결과가

호스트 vNIC는 또한 SMB의 측면에서 지원 RDMA로 표시 됩니다.

![네트워크 어댑터 속성](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)


### <a name="get-smbclientnetworkinterface-unexpected-results"></a>다운로드 SmbClientNetworkInterface 예기치 않게 결과

1. Mlnx 미니 및 Mlnx 버스 드라이버는 최신 있는지 확인 합니다. Mellanox에 대 한 사용 하 여 최소 42를 삭제 합니다. 
2. 장치 관리자를 통해 드라이버 버전을 확인 하 여 Mlnx 미니 및 버스 드라이버와 일치 하는지 확인 합니다. 시스템 장치에서 버스 드라이버를 찾을 수 있습니다. 네트워크 어댑터 속성의 다음 스크린샷와 같이 Mellanox Connect-X 3 PRO VPI 된 이름이 시작 해야 합니다.
3. 실제 NIC와 호스트 vNIC에서 네트워크 직접 (RDMA)을 사용할 수 있는지 확인 합니다.
4. Hyper-v 가상 스위치 RDMA 기능을 확인 하 여 실제 바로 어댑터를 통해 만들어집니다 있는지 확인 합니다.
5. 체크인 이벤트 로그 "SMB 클라이언트"에 대 한 **응용 프로그램 및 서비스 | Microsoft | Windows**합니다.

## <a name="get-netadapterqos"></a>Get-NetAdapterQos

다음 Windows PowerShell 명령을 실행 하 여 서비스 \(QoS\) 구성 네트워크 어댑터 품질을 볼 수 있습니다.

    Get-NetAdapterQos

### <a name="get-netadapterqos-expected-results"></a>Get-NetAdapterQos 결과를 필요합니다.

이 가이드를 사용 하 여 수행 하는 첫 번째 구성 단계에 따라 우선 및 교통 클래스 표시 되어야 합니다.

![서비스 우선 순위 및 클래스 품질](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-NetAdapterQos 예기치 않게 결과

결과가 예기치 않은 경우 다음 단계를 수행 합니다.

1. 데이터 센터 브리지 \(DCB\) 및 QoS 실제 네트워크 어댑터를 지원 하는지 확인
2. 네트워크 어댑터 드라이버를 최신 상태로 있는지 확인 합니다.


## <a name="get-smbmultichannelconnection"></a>Get-SmbMultiChannelConnection

원격 노드 IP 주소 RDMA\ 수 있는지 확인 하려면 다음 Windows PowerShell 명령을 사용할 수 있습니다.

    Get-SmbMultiChannelConnection


### <a name="get-smbmultichannelconnection-expected-results"></a>Get-SmbMultiChannelConnection 결과를 필요합니다.

원격 노드 IP 주소 지원 RDMA로 표시 됩니다.

![RDMA 원격 지원 노드 IP 주소](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Get-SmbMultiChannelConnection 예기치 않게 결과

결과가 예기치 않은 경우 다음 단계를 수행 합니다.

1. Ping 두 가지 방식으로 작동 하는지 확인 합니다.
2. 방화벽 SMB 연결 시작을 차단 하 고 있지 있는지 확인 합니다. 특히, SMB 직접 포트 iWARP에 대 한 5445 방화벽 규칙 및 445 ROCE에 대 한 사용 하도록 설정 합니다.

## <a name="get-smbclientnetworkinterface"></a>Get-SmbClientNetworkInterface

다음 명령을 SMB 하 여 가상 NIC RDMA에 대 한 사용 하도록 설정한 RDMA\ 지원으로 보고 된다는 확인 하기 위해 사용할 수 있습니다.

    Get-SmbClientNetworkInterface


### <a name="get-smbclientnetworkinterface-expected-results"></a>Get-SmbClientNetworkInterface 결과를 필요합니다.

RDMA에 대 한 사용 하도록 설정 된 가상 NIC SMB RDMA 가능로 볼 수 해야 합니다.

![Nic RDMA 지원 되는 SMB 보고서](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface 예기치 않게 결과

결과가 예기치 않은 경우 다음 단계를 수행 합니다.

1. Ping 두 가지 방식으로 작동 하는지 확인 합니다.
2. 방화벽이 SMB 연결 시작 있는지 확인 합니다.

## <a name="vstat-mellanox-specific"></a>Vstat \(Mellanox specific\)

사용할 수 있는 Mellanox 네트워크 어댑터를 사용 하는 경우는 **vstat** 명령을 사용 하 여 RDMA Hyper-v 노드에서 수렴 이더넷 \(RoCE\) 버전을 확인 합니다.

### <a name="vstat-expected-results"></a>예상 vstat 결과

두 노드에서 RoCE 버전 동일 해야 합니다. 또한 최신 두 노드에서 펌웨어 버전 인지 확인 하려면 좋은 방법입니다.

![RoCE 버전 검사 결과 예시](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>Vstat 예기치 않게 결과

결과가 예기치 않은 경우 다음 단계를 수행 합니다.

1. 올바른 RoCE 버전이 Set-MlnxDriverCoreSetting를 사용 하 여 설정
2. Mellanox 웹 사이트에서 최신 펌웨어가 설치 합니다.


## <a name="perfmon-counters"></a>성능 카운터

성능 모니터 구성 RDMA 활동을 확인 하려면에 카운터 검토할 수 있습니다.

![모니터 결과 예 성능](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

## <a name="all-topics-in-this-guide"></a>이 가이드의 모든 항목

이 가이드는 다음 항목이 포함 되어 있습니다.

- [단일 네트워크 어댑터를 사용 하 여 집약된 NIC 구성](cnic-single.md)
- [집약된 NIC 어댑터당된 NIC 구성](cnic-datacenter.md)
- [실제 스위치 구성 집약 nic](cnic-app-switch-config.md)
- [NIC 구성 수렴 문제 해결](cnic-app-troubleshoot.md)
