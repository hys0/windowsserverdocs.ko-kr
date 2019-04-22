---
title: Windows Admin Center 사용 하 여 장애 조치 클러스터 관리
description: Windows Admin Center (프로젝트 브라 티)를 사용 하 여 장애 조치 클러스터 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f7e14581f7f6b14b0cf39308de236b68a07e8c9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824074"
---
# <a name="manage-failover-clusters-with-windows-admin-center"></a>Windows Admin Center 사용 하 여 장애 조치 클러스터 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows Admin Center에 대해 자세히 알아보거나](../understand/windows-admin-center.md)[지금 다운로드](https://aka.ms/windowsadmincenter)하세요.

## <a name="managing-failover-clusters"></a>장애 조치 클러스터 관리
[장애 조치 클러스터링](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview) 는 여러 서버 응용 프로그램 및 스케일 아웃 파일 서버, Hyper-v와 같은 서비스의 가용성과 확장성을 높이기 위해 내결함성 클러스터로 그룹화 할 수 있는 Windows Server 기능 및 Microsoft SQL Server입니다.

로 추가 하 여 개별 서버로 장애 조치 클러스터 노드를 관리할 수 있습니다 하는 동안 [서버 연결](manage-servers.md) Windows Admin Center 추가할 수 있습니다도 보기 및 관리 클러스터 리소스, 저장소, 네트워크, 노드 장애 조치 클러스터로 역할, virtual machines 및 가상 스위치를 선택 합니다.

![장애 조치 클러스터 개요 화면](../media/manage-failover-clusters/fcm-overview.png)

## <a name="adding-a-failover-cluster-to-windows-admin-center"></a>장애 조치 클러스터를 Windows Admin Center 추가
에 추가 하려면 클러스터를 Windows Admin Center:

1. 클릭 **+ 추가** 모든 연결 합니다.
2. 추가 하도록 선택 된 **장애 조치 연결**합니다.
3. 클러스터의 이름을 입력 하 고 메시지가 표시 되 면 사용할 자격 증명입니다.
4. Windows Admin Center 개별 서버 연결으로 클러스터 노드를 추가 하는 옵션을 해야 합니다.
5. 클릭 **제출** 완료 합니다.

클러스터 개요 페이지에서 연결 목록에 추가 됩니다. 클러스터에 연결 하려면 클릭 합니다.

> [!NOTE]
> 관리할 수도 있습니다 하이퍼 수렴 형 클러스터를 추가 하 여 클러스터를 [Hyper-Converged 클러스터 연결](manage-hyper-converged.md) Windows Admin Center.

## <a name="tools"></a>Tools

다음 도구를 장애 조치 클러스터 연결에 사용할 수 있습니다.

| 도구 | 설명 |
| ---- | ----------- |
| 개요 | 클러스터 리소스 장애 조치 클러스터 세부 정보 보기 및 관리 |
| 디스크 | 보기 클러스터 공유 디스크와 볼륨 |
| 네트워크 | 클러스터의 네트워크 보기 |
| 노드 | 보기 및 관리 클러스터 노드 |
| 역할 | 클러스터 역할을 관리 하거나 빈 역할 만들기 |
| 업데이트 | 클러스터 인식 업데이트 관리 |
| [Virtual Machines](manage-virtual-machines.md) | 가상 컴퓨터 보기 및 관리 |
| 가상 스위치 | 보기 및 가상 스위치 관리 |

## <a name="more-coming"></a>향후 추가 예정

Windows Admin Center 장애 조치 클러스터 관리를 적극적으로 개발 하 고 새로운 기능을 가까운 시일 안에 추가 됩니다. UserVoice에서 상태 및 기능에 대해 투표를 볼 수 있습니다.

|기능 요청|
|-------|
| [추가 클러스터 된 디스크 정보를 표시 합니다.](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [추가 클러스터 작업을 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [다른 클러스터에 Hyper-v 및 스케일 아웃 파일 서버를 실행 하는 수렴 형된 클러스터를 지원 합니다.](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [보기 CSV 블록 캐시](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [모든 참조 또는 새로운 기능 제안](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |