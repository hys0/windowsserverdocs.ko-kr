---
title: Windows Admin Center를 사용 하 여 장애 조치 클러스터 관리
description: Windows Admin Center (Project Honolulu)를 사용 하 여 장애 조치 클러스터 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 63f5fca8e7ef63200e01cfc6e00a979e7f045b51
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296675"
---
# Windows Admin Center를 사용 하 여 장애 조치 클러스터 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md) [지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## 장애 조치 클러스터 관리
[장애 조치 클러스터링](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview) 은 여러 서버 응용 프로그램 및 스케일 아웃 파일 서버, Hyper-v와 같은 서비스의 가용성과 확장성을 높이기 위해 장애 조치 클러스터로 그룹화 할 수 있는 Windows Server 기능 및 Microsoft SQL Server입니다.

Windows Admin Center의 [서버 연결](manage-servers.md) 추가 하 여 개별 서버로 장애 조치 클러스터 노드를 관리할 수, 동안 추가할 수 있습니다 또한 장애 조치 클러스터를 보고 관리 클러스터 리소스, 저장소, 네트워크, 노드, 역할, 가상 대로 컴퓨터 및 가상 스위치입니다.

![장애 조치 클러스터 개요 화면](../media/manage-failover-clusters/fcm-overview.png)

## Windows Admin Center를 장애 조치 클러스터를 추가합니다.
Windows Admin Center를 클러스터를 추가 합니다.

1. 모든 연결에서 **+ 추가** 클릭 합니다.
2. **장애 조치 연결**을 추가 하려면 선택 합니다.
3. 클러스터의 이름을 입력 하 고 메시지가 표시 되 면 자격 증명을 사용 합니다.
4. Windows Admin Center에 개별 서버 연결으로 클러스터 노드를 추가 하는 옵션을 해야 합니다.
5. **제출** 을 완료를 클릭 합니다.

클러스터의 개요 페이지에서 연결 목록에 추가 됩니다. 클러스터에 연결을 클릭 합니다.

> [!NOTE]
> 관리할 수도 있습니다 하이퍼 수렴 형 클러스터에 Windows Admin Center [컨 버 지 드 클러스터 연결](manage-hyper-converged.md) 로 클러스터를 추가 하 여 합니다.

## 도구

다음 도구 장애 조치 클러스터 연결에 사용할 수 있습니다.

| 도구 | 설명 |
| ---- | ----------- |
| 개요 | 장애 조치 클러스터 세부 정보 보기 및 클러스터 리소스 관리 |
| 디스크 | 보기 클러스터 공유 볼륨 및 디스크 |
| 네트워크 | 클러스터의 네트워크 보기 |
| 노드 | 보기 및 클러스터 관리 |
| 역할 | 클러스터 역할을 관리 하거나는 빈 역할 만들기 |
| 업데이트 | 클러스터 인식 업데이트 ( [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)필요) 관리 |
| [가상 컴퓨터](manage-virtual-machines.md) | 보기 및 가상 컴퓨터 관리 |
| 가상 스위치 | 보기 및 가상 스위치 관리 |

## 더 많은 이후

Windows Admin Center에서 장애 조치 클러스터 관리는 적극적으로 개발 하 고 나중에 새로운 기능이 추가 됩니다. UserVoice에서 상태 및 기능에 대 한 응답을 볼 수 있습니다.

|기능 요청|
|-------|
| [클러스터 디스크 정보 표시](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [추가 클러스터 작업을 지원 합니다.](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [서로 다른 클러스터에서 Hyper-v 및 스케일 아웃 파일 서버를 실행 하는 수렴 형된 클러스터 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [보기 CSV 블록 캐시](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [모두를 보거나 새로운 기능을 제안 합니다.](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |