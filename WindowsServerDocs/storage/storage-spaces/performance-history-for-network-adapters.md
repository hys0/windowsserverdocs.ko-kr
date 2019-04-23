---
title: 네트워크 어댑터에 대 한 성능 기록
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: 저장소 공간 다이렉트
ms.localizationpriority: medium
ms.openlocfilehash: 340999a8f440975d3736277b1a30dddbb942785d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849984"
---
# <a name="performance-history-for-network-adapters"></a>네트워크 어댑터에 대 한 성능 기록

> 적용 대상: Windows Server Insider Preview

이 하위 항목의 [저장소 공간 다이렉트에 대 한 성능 기록을](performance-history.md) 네트워크 어댑터에 대해 수집 된 성능 기록 세부 정보에 설명 합니다. 네트워크 어댑터 성능 기록은 클러스터의 모든 서버에서 모든 실제 네트워크 어댑터에 대해 사용할 수 있습니다. 원격 직접 메모리 액세스 (RDMA) 성능 기록은 사용 하도록 설정 하는 RDMA를 사용 하 여 모든 실제 네트워크 어댑터에 사용할 수입니다.

   > [!NOTE]
   > 성능 기록 아래에 있는 서버에서 네트워크 어댑터에 대해 수집할 수 없습니다. 컬렉션을 고 서버가 다시 시작 되 면 자동으로 재개 합니다.

## <a name="series-names-and-units"></a>계열 이름 및 단위

이 시리즈는 모든 적합 한 네트워크 어댑터에 대해 수집 됩니다.

| 시리즈                               | 단위            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | 비트 / 초 |
| `netadapter.bandwidth.outbound`      | 비트 / 초 |
| `netadapter.bandwidth.total`         | 비트 / 초 |
| `netadapter.bandwidth.rdma.inbound`  | 비트 / 초 |
| `netadapter.bandwidth.rdma.outbound` | 비트 / 초 |
| `netadapter.bandwidth.rdma.total`    | 비트 / 초 |

   > [!NOTE]
   > 네트워크 어댑터 성능 기록에 기록 됩니다 **비트** 초당 초당 바이트 수 없습니다. 10 GbE 네트워크 어댑터가 도입 되어 1,000,000,000 비트 약를 주고받을 수 하나 125,000,000 바이트 = 1.25 GB 이론적으로 최대 초당 =.

## <a name="how-to-interpret"></a>해석 하는 방법

| 시리즈                               | 해석 하는 방법                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | 네트워크 어댑터에서 받은 데이터의 비율입니다.                         |
| `netadapter.bandwidth.outbound`      | 네트워크 어댑터에서 전송 되는 데이터의 비율입니다.                             |
| `netadapter.bandwidth.total`         | 총 데이터 변동률 받거나 네트워크 어댑터에서 전송 합니다.           |
| `netadapter.bandwidth.rdma.inbound`  | 네트워크 어댑터에서 RDMA를 통한 받은 데이터의 비율입니다.               |
| `netadapter.bandwidth.rdma.outbound` | 네트워크 어댑터에서 RDMA를 통한 전송 되는 데이터의 비율입니다.                   |
| `netadapter.bandwidth.rdma.total`    | 총 데이터 변동률 받거나 네트워크 어댑터에서 RDMA를 통한 전송 합니다. |

## <a name="where-they-come-from"></a>어디에서 생겨날

`bytes.*` 시리즈에서 수집 되는 `Network Adapter` 네트워크 어댑터를 설치한 서버를 설정 하는 성능 카운터, 네트워크 어댑터 당 하나의 인스턴스.

| 시리즈                           | 원본 카운터           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 × `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 × `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 × `Bytes Total/sec`    |

`rdma.*` 시리즈에서 수집 되는 `RDMA Activity` 네트워크 어댑터를 설치한 서버를 설정 하는 성능 카운터를 사용 하도록 설정 하는 rdma 네트워크 어댑터 당 하나의 인스턴스.

| 시리즈                               | 원본 카운터           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 × `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 × `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 × *위의 합계*   |

   > [!NOTE]
   > 카운터는 샘플링 되지 전체 간격을 측정 됩니다. 예를 들어, 네트워크 어댑터 유휴 상태인 경우 9 초 있지만 200 bits 전송에 대 한 10th 1 초 동안에서 해당 `netadapter.bandwidth.total` 으로 기록 됩니다 초당 20 bits 평균 10 초 간격입니다. 이렇게 하면 성능 기록과 모든 활동을 캡처하고 노이즈를 강력 합니다.

## <a name="usage-in-powershell"></a>PowerShell에서 사용

사용 된 [Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter) cmdlet:

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>참조

- [저장소 공간 다이렉트에 대 한 성능 기록](performance-history.md)
