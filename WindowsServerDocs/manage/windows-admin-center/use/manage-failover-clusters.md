---
title: Windows 관리 센터를 사용 하 여 장애 조치 (Failover) 클러스터 관리
description: Windows 관리 센터 (Project Honolulu)를 사용 하 여 장애 조치 (Failover) 클러스터 관리
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: b7f015ac4c9906447069501bf0922b36306a51d7
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950490"
---
# <a name="manage-failover-clusters-with-windows-admin-center"></a>Windows 관리 센터를 사용 하 여 장애 조치 (Failover) 클러스터 관리

>적용 대상: Windows Admin Center, Windows Admin Center 미리 보기

> [!Tip]
> Windows Admin Center를 처음 사용하시나요?
> [Windows 관리 센터에 대해 다운로드 하거나 자세히 알아보세요](../overview.md).

## <a name="managing-failover-clusters"></a>장애 조치 (failover) 클러스터 관리
[장애 조치 (Failover) 클러스터링](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview) 은 여러 서버를 장애 조치 (Failover) 클러스터로 그룹화 하 여 스케일 아웃 파일 서버, hyper-v 및 Microsoft SQL Server와 같은 응용 프로그램 및 서비스의 가용성과 확장성을 향상 시킬 수 있는 Windows Server 기능입니다.

장애 조치 (failover) 클러스터 노드를 Windows 관리 센터에서 [서버 연결](manage-servers.md) 로 추가 하 여 해당 노드를 개별 서버로 관리할 수도 있지만 장애 조치 (failover) 클러스터로 추가 하 여 클러스터 리소스, 저장소, 네트워크, 노드, 역할, 가상 컴퓨터 및 가상 스위치를 보고 관리할 수도 있습니다.

![장애 조치 (Failover) 클러스터 개요 화면](../media/manage-failover-clusters/fcm-overview.png)

## <a name="adding-a-failover-cluster-to-windows-admin-center"></a>Windows 관리 센터에 장애 조치 (failover) 클러스터 추가
Windows 관리 센터에 클러스터를 추가 하려면 다음을 수행 합니다.

1. 모든 연결에서 **+ 추가** 를 클릭 합니다.
2. **장애 조치 (Failover) 연결**을 추가 하도록 선택 합니다.
3. 클러스터의 이름을 입력 하 고, 메시지가 표시 되 면 사용할 자격 증명을 입력 합니다.
4. Windows 관리 센터에서 개별 서버 연결로 클러스터 노드를 추가 하는 옵션이 있습니다.
5. **제출을** 클릭 하 여 완료 합니다.

클러스터가 개요 페이지의 연결 목록에 추가 됩니다. 클릭 하 여 클러스터에 연결 합니다.

> [!NOTE]
> Windows 관리 센터에서 클러스터를 [하이퍼 수렴 형 클러스터 연결](manage-hyper-converged.md) 로 추가 하 여 하이퍼 수렴 형 클러스터를 관리할 수도 있습니다.

## <a name="tools"></a>도구

장애 조치 (failover) 클러스터 연결에 사용할 수 있는 도구는 다음과 같습니다.

| 도구 | 설명 |
| ---- | ----------- |
| 개요 | 장애 조치 (failover) 클러스터 세부 정보 보기 및 클러스터 리소스 관리 |
| 디스크 | 클러스터 공유 디스크 및 볼륨 보기 |
| 네트워크 | 클러스터의 네트워크 보기 |
| 노드 | 클러스터 노드 보기 및 관리 |
| 역할 | 클러스터 역할 관리 또는 빈 역할 만들기 |
| 업데이트 | 클러스터 인식 업데이트 관리 ( [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)필요) |
| [Virtual Machines](manage-virtual-machines.md) | 가상 컴퓨터 보기 및 관리 |
| 가상 스위치 | 가상 스위치 보기 및 관리 |

## <a name="more-coming"></a>추가 예정

Windows 관리 센터의 장애 조치 (Failover) 클러스터 관리는 현재 개발 중 이며 가까운 장래에 새 기능이 추가 될 예정입니다. UserVoice의 기능에 대 한 상태 및 투표를 확인할 수 있습니다.

|기능 요청|
|-------|
| [더 많은 클러스터 된 디스크 정보 표시](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [추가 클러스터 작업 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [Hyper-v를 실행 하 고 다른 클러스터에서 스케일 아웃 파일 서버 수렴 형 클러스터 지원](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [CSV 블록 캐시 보기](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [모든 항목 보기 또는 새 기능 제안](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |