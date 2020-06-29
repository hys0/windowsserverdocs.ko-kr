---
title: 네트워크 어댑터에 대 한 성능 기록
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 597abd8e389421eb6875ff3cc94b457f341be3b7
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474750"
---
# <a name="performance-history-for-network-adapters"></a>네트워크 어댑터에 대 한 성능 기록

> 적용 대상: 시작

[스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의이 하위 항목에서는 네트워크 어댑터에 대해 수집 된 성능 기록에 대해 자세히 설명 합니다. 네트워크 어댑터 성능 기록은 클러스터의 모든 서버에 있는 모든 실제 네트워크 어댑터에 대해 사용할 수 있습니다. Rdma를 사용 하는 모든 실제 네트워크 어댑터에 대해 RDMA (원격 직접 메모리 액세스) 성능 기록을 사용할 수 있습니다.

   > [!NOTE]
   > 다운 된 서버의 네트워크 어댑터에 대 한 성능 기록을 수집할 수 없습니다. 서버를 다시 시작 하면 수집이 자동으로 다시 시작 됩니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이러한 시리즈는 적합 한 모든 네트워크 어댑터에 대해 수집 됩니다.

| 계열                               | 단위            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | 초당 비트 수 |
| `netadapter.bandwidth.outbound`      | 초당 비트 수 |
| `netadapter.bandwidth.total`         | 초당 비트 수 |
| `netadapter.bandwidth.rdma.inbound`  | 초당 비트 수 |
| `netadapter.bandwidth.rdma.outbound` | 초당 비트 수 |
| `netadapter.bandwidth.rdma.total`    | 초당 비트 수 |

   > [!NOTE]
   > 네트워크 어댑터 성능 기록은 초당 바이트가 아닌 **비트** 수로 기록 됩니다. 1 10 GbE 네트워크 어댑터는 이론적 최대값으로 약 10억 비트 = 1억2500만 바이트 = 초당 1.25 GB를 보내고 받을 수 있습니다.

## <a name="how-to-interpret"></a>해석 방법

| 계열                               | 해석 방법                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | 네트워크 어댑터에서 받은 데이터의 요금입니다.                         |
| `netadapter.bandwidth.outbound`      | 네트워크 어댑터에서 보낸 데이터의 요금입니다.                             |
| `netadapter.bandwidth.total`         | 네트워크 어댑터에서 받거나 보낸 데이터의 총 비율입니다.           |
| `netadapter.bandwidth.rdma.inbound`  | 네트워크 어댑터에서 RDMA를 통해 받은 데이터의 요금입니다.               |
| `netadapter.bandwidth.rdma.outbound` | 네트워크 어댑터에서 RDMA를 통해 보낸 데이터의 요금입니다.                   |
| `netadapter.bandwidth.rdma.total`    | 네트워크 어댑터에서 RDMA를 통해 받거나 보낸 데이터의 총 비율입니다. |

## <a name="where-they-come-from"></a>원본 위치

이 시리즈는 네트워크 어댑터가 `bytes.*` `Network Adapter` 설치 된 서버에 설정 된 성능 카운터에서 네트워크 어댑터 당 하나의 인스턴스로 수집 됩니다.

| 계열                           | 원본 카운터           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 ×`Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 ×`Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 ×`Bytes Total/sec`    |

`rdma.*`시리즈는 `RDMA Activity` 네트워크 어댑터가 설치 된 서버에 설정 된 성능 카운터에서 수집 되며, RDMA를 사용 하도록 설정 된 네트워크 어댑터 당 하나의 인스턴스입니다.

| 계열                               | 원본 카운터           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 ×`Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 ×`Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 위의 8 × *합계*   |

   > [!NOTE]
   > 카운터는 샘플링 되지 않고 전체 간격으로 측정 됩니다. 예를 들어 네트워크 어댑터가 9 초 동안 유휴 상태 이지만 10 초 안에 200 비트를 전송 하는 경우 `netadapter.bandwidth.total` 이 10 초 간격 동안 평균 초당 20 비트로 기록 됩니다. 이렇게 하면 성능 기록이 모든 활동을 캡처하고 소음에 대해 강력 하 게 됩니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

[Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter) cmdlet을 사용 합니다.

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## <a name="additional-references"></a>추가 참조

- [스토리지 공간 다이렉트에 대 한 성능 기록](performance-history.md)
