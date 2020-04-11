---
title: Windows Server 2016에 대한 서버 역할 업그레이드 및 마이그레이션 매트릭스
description: Windows Server 2016으로 업그레이드 또는 마이그레이션할 수 있는 서버 역할을 보여 줍니다.
ms.prod: windows-server
ms.date: 10/05/2016
ms.technology: server-general
ms.topic: article
ms.assetid: 7e031a64-b1e6-4cf6-994a-e7c575835f6a
author: jaimeo
ms.author: jaimeo
manager: dongill
ms.localizationpriority: medium
ms.openlocfilehash: 4e1b783c43eb435e61c7caaccaf842a0137b5eec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826526"
---
# <a name="server-role-upgrade-and-migration-matrix-for-windows-server-2016"></a>Windows Server 2016에 대한 서버 역할 업그레이드 및 마이그레이션 매트릭스

>적용 대상: Windows Server 2016

이 페이지의 그리드는 특히 Windows Server 2016으로 전환하기 위한 서버 역할 업그레이드 및 마이그레이션 옵션을 설명합니다. 개별 역할 마이그레이션 가이드는 [Windows Server에서 역할 및 기능 마이그레이션](https://docs.microsoft.com/windows-server/get-started/migrate-roles-and-features)을 참조하세요. 설치 및 업그레이드에 대한 자세한 내용은 [Windows Server 설치, 업그레이드 및 마이그레이션](https://docs.microsoft.com/windows-server/get-started/installation-and-upgrade)을 참조하세요.

|서버 역할|Windows Server 2012 R2에서 업그레이드 가능 여부|Windows Server 2012에서 업그레이드 가능 여부|마이그레이션 지원 여부|가동 중지 시간 없이 마이그레이션을 완료할 수 있는지 여부|  
|-------------------|----------|--------------|--------------|----------|  
|Active Directory 인증서 서비스|    예|    예|    예|    아니요|
|Active Directory 도메인 서비스|    예|    예|    예|    예|
|ADFS(Active Directory Federation Services)|    아니요|    아니요|    예|    아니요(새 노드를 팜에 추가해야 함)|
|Active Directory LDS(Lightweight Directory Services)|    예|    예|    예|    예|
|Active Directory Rights Management Services|    예|    예|    예|    아니요|
|DHCP 서버|    예|    예|    예|    예|
|DNS 서버|    예|    예|    예|    아니요|
|장애 조치(failover) 클러스터|예, 노드 일시 중지-드레이닝, 제거, Windows Server 2016으로 업그레이드 및 원본 클러스터 다시 연결을 포함하는 [클러스터 OS 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade) 프로세스 사용. 예, 서버가 업그레이드를 위해 클러스터에 의해 제거된 후 다른 클러스터에 추가되는 경우.|서버가 클러스터에 속하지 않는 동안은 아님. 예, 서버가 업그레이드를 위해 클러스터에 의해 제거된 후 다른 클러스터에 추가되는 경우.    |예|아니요, Windows Server 2012 장애 조치(failover) 클러스터인 경우. 예, Hyper-V VM 포함 Windows Server 2012 R2 장애 조치 클러스터 또는 스케일 아웃 파일 서버 역할을 실행하는 Windows Server 2012 R2 장애 조치 클러스터인 경우. [클러스터 OS 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)를 참조하세요.|
|파일 및 스토리지 서비스|    예|    예|    하위 기능에 따라 다름|    아니요|
|Hyper-V| 예. (호스트가 노드 일시 중지-드레이닝, 제거, Windows Server 2016으로 업그레이드 및 원본 클러스터 다시 연결로 구성되는 클러스터 OS 롤링 업그레이드 프로세스를 통해 클러스터에 포함되는 경우)|  아니요|   예|  아니요, Windows Server 2012 장애 조치(failover) 클러스터인 경우. 예, Hyper-V VM 포함 Windows Server 2012 R2 장애 조치 클러스터 또는 스케일 아웃 파일 서버 역할을 실행하는 Windows Server 2012 R2 장애 조치 클러스터인 경우. [클러스터 OS 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)를 참조하세요.| 
|인쇄 및 팩스 서비스|    아니요|    아니요|    예(Printbrm.exe)|    아니요|
|원격 데스크톱 서비스|    예, 모든 하위 역할, 혼합 모드 팜은 지원되지 않음|    예, 모든 하위 역할, 혼합 모드 팜은 지원되지 않음|    예|    아니요|
|웹 서버(IIS)|    예|    예|    예|    아니요|
|Windows Server Essentials Experience|    예|    해당 없음 – 새 기능|    예|    아니요|
|Windows Server Update Services|    예|    예|    예|    아니요|
|클라우드 폴더|    예|    예|    예|    예, [클러스터 OS 롤링 업그레이드](https://technet.microsoft.com/windows-server-docs/failover-clustering/cluster-operating-system-rolling-upgrade)를 사용할 경우 WS 2012 R2 클러스터에서|

