---
title: 네트워크 어댑터에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 340999a8f440975d3736277b1a30dddbb942785d
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239240"
---
# 네트워크 어댑터에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목이에서는 [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md) 의 성능 기록을 수집 네트워크 어댑터에 대해 자세히 설명 합니다. 네트워크 어댑터 성능 기록은 클러스터의 모든 서버에서 모든 실제 네트워크 어댑터에 사용할 수 있습니다. 원격 직접 메모리 액세스 (RDMA) 성능 기록은 RDMA 활성화 된 모든 실제 네트워크 어댑터에 대해 사용할 수 있습니다.

   > [!NOTE]
   > 아래에 있는 서버에 있는 네트워크 어댑터에 대 한 성능 기록을 수집할 수 없습니다. 컬렉션의 서버가 다시 시작 되 면 자동으로 다시 됩니다.

## 시리즈 이름과 단위

이러한 시리즈 모든 적합 한 네트워크 어댑터에 대해 수집 됩니다.

| 시리즈                               | Unit            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | 초당 비트 |
| `netadapter.bandwidth.outbound`      | 초당 비트 |
| `netadapter.bandwidth.total`         | 초당 비트 |
| `netadapter.bandwidth.rdma.inbound`  | 초당 비트 |
| `netadapter.bandwidth.rdma.outbound` | 초당 비트 |
| `netadapter.bandwidth.rdma.total`    | 초당 비트 |

   > [!NOTE]
   > 네트워크 어댑터 성능 기록 초당 바이트 수 없는 초당 **비트** 기록 됩니다. 10 GbE 네트워크 어댑터가 약 1000000000 비트를 주고받을 수 하나 125,000,000 바이트 = 1.25 GB 이론상 최대한 초당 = 합니다.

## 해석 하는 방법

| 시리즈                               | 해석 하는 방법                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | 네트워크 어댑터에서 받은 데이터의 속도입니다.                         |
| `netadapter.bandwidth.outbound`      | 네트워크 어댑터에서 전송 된 데이터 속도입니다.                             |
| `netadapter.bandwidth.total`         | 데이터의 총 속도 수신 하거나 네트워크 어댑터에서 전송 합니다.           |
| `netadapter.bandwidth.rdma.inbound`  | 네트워크 어댑터에서 RDMA를 통해 받은 데이터의 속도.               |
| `netadapter.bandwidth.rdma.outbound` | 네트워크 어댑터에서 RDMA를 통해 전송 된 데이터 속도.                   |
| `netadapter.bandwidth.rdma.total`    | 데이터의 총 속도 수신 하거나 네트워크 어댑터에서 RDMA를 통해 전송 합니다. |

## 어디에서 보 딩

`bytes.*` 시리즈에서 수집 되는 `Network Adapter` 성능 카운터 네트워크 어댑터가 설치 되어 있는 서버에 설정, 네트워크 어댑터당 인스턴스만 합니다.

| 시리즈                           | 원본 카운터           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 × `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 × `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 × `Bytes Total/sec`    |

`rdma.*` 에서 수집 된 일련의 `RDMA Activity` 성능 카운터 네트워크 어댑터가 설치 되어 있는 서버에 설정, RDMA 사용할 수 있는 네트워크 어댑터 당 하나의 인스턴스.

| 시리즈                               | 원본 카운터           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 × `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 × `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 × *위의의 합*   |

   > [!NOTE]
   > 카운터는 샘플링 하지는 전체 간격을 통해 측정 됩니다. 예를 들어 네트워크 어댑터는 유휴 9 초 하지만 전송이 200 비트 10 초에 해당 `netadapter.bandwidth.total` 기록 될 초당 20 비트로 평균적으로이 10 초 간격 동안 합니다. 이렇게 하면 성능 기록 모든 활동 캡처하고 노이즈 강력 합니다.

## Powershell 사용

[Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter) cmdlet을 사용 합니다.

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## 참고 항목

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
