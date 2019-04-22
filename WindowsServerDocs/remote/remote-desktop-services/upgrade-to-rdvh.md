---
title: 원격 데스크톱 가상화 호스트를 Windows Server 2016으로 업그레이드
description: 이 문서에서는 기존 원격 데스크톱 서비스 배포 Windows Server 2016으로 업그레이드 하는 방법을 설명 합니다.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5aed8ba7-f541-4416-b01c-4d3b1712e2b1
author: spatnaik
manager: scottman
ms.openlocfilehash: 17bf3a49155d29960684acebea870c0b51f664a4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812034"
---
# <a name="upgrading-your-remote-desktop-virtualization-host-to-windows-server-2016"></a>원격 데스크톱 가상화 호스트를 Windows Server 2016으로 업그레이드

>적용 대상: Windows Server (반기 채널), Windows Server 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 역할이 설치 된 OS 업그레이드를 지원
Windows Server 2016으로 업그레이드는 Windows Server 2012 R2 및 Windows Server 2016 TP5 에서만 지원 됩니다.

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-locally"></a>Vm을 저장할 로컬 배포에 RD 가상화 호스트 서버
이러한 서버를 한 번에 업그레이드 해야 합니다. 업그레이드 하려면 다음 단계를 수행 합니다.

1. 모든 사용자 로그 오프 합니다.
1. 각 호스트에 설정 해제 하거나 모든 가상 머신을 저장 합니다. 
1. Windows Server 2016으로 서버를 업그레이드 합니다. 
1. 모든 컬렉션 업그레이드 완료 된 후 사용할 수 있고 작동 해야 합니다.      

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-in-cluster-shared-volumes-csv"></a>Vm에서 클러스터 공유 볼륨 (CSV)에 저장 된 배포에 RD 가상화 호스트 서버 

1. 여기서 RDVH 서버 중 일부는 업그레이드 하 고 일부는 Windows Server 2012 R2에서 호스트 Vm 계속 업그레이드 전략을 결정 합니다.  
1. 모든 Vm를 마이그레이션하여 ' 필요가 아직 업그레이드할 수' 다른 원래 2012 R2 클러스터의 일부가 남아 있는 RDVH 서버를 업그레이드 하는 점의 초기 라운드에 대 한 대상 RDVH 서버 중 하나 이상의 격리 합니다.
    1. 장애 조치 클러스터 관리자를 엽니다. 
    1. **역할**을 누릅니다. 
    1. 하나 이상의 Vm을 선택 합니다. 상황에 맞는 메뉴를 열려면 단추로 클릭 합니다. 
    1. 클릭 **이동** 중 하나를 선택 하 고 **Live** 또는 **Quick Migration** 초기 업그레이드의 일부분이 아닌 RD 가상화 호스트 서버를 하나 이상의 Vm을 이동할 수 있습니다. 사용 하 여 **Live** 하거나 **빠른** 하드웨어 호환성 온라인 요구 사항 등의 요인에 따라 마이그레이션. 
1. 원본 클러스터에서 업그레이드 준비 RDVH 서버를 제거 합니다. 
1. 격리 된 RDVH 서버를 업그레이드 합니다. 
1. 대상된 RDVH 서버를 성공적으로 업그레이드 된 후 새 클러스터와는 완전히 다른 SAN 볼륨에 있어야 하는 CSV를 만듭니다.
1. 새 클러스터로 업그레이드 하는 모든 RDVH 서버를 조인 합니다. 
1. 기존 CSV에서 기존 폴더 구조를 모방 하는 새 CSV의 폴더 구조를 만듭니다. 여기에 컬렉션 폴더와 각 VM의 최상위 수준 하위 폴더 포함 됩니다. 
1. 원본 CSV에서 다양 한 VM 컬렉션 폴더에서 새 CSV에 동일한 위치에 새 컬렉션 폴더로 /IMGS 폴더 및 내용을 복사 합니다. 
1. 원본 RDVH 컴퓨터 클러스터 관리자를 사용 하 여 고가용성을 위해 VM의 구성을 제거 하려면:
    1. 클러스터 관리자를 시작 합니다. 
    1. **역할**을 누릅니다. 
    1. VM 개체를 마우스 오른쪽 단추로 누른 **제거**합니다. 
1. 업그레이드 되지 않은 RDVH 서버 중 하나를 RDVH 서버 업그레이드 및 새 CSV 클러스터 중 하나에 모든 Vm을 이동 하려면 Hyper-v 관리자를 사용 합니다.
    1. Hyper-V 관리자를 엽니다. 
    1. 업그레이드 하지 않은 RDVH 서버 중 하나를 선택 합니다. 
    1. Vm을 이동 하 고 클릭 한 다음 중 하나를 마우스 오른쪽 단추로 클릭 **이동**합니다. 
    1. 선택 **가상 머신을**를 클릭 하 고 **다음**합니다. 
    1. 대상된 업그레이드 RDVH 서버 이름을 제공 합니다 **대상 컴퓨터 지정** 페이지를 선택한 다음 클릭 **다음**합니다. 
    1. 선택할 **단일 위치에 가상 컴퓨터의 데이터를 이동**를 클릭 하 고 **다음**합니다. 
    1. 대상 위치를 찾습니다. 
    > [!IMPORTANT]
    > 이 경로 특정 VM에 대 한 빈 폴더를 확인 합니다. 

    > [!NOTE]
    > 언급 했 듯이이 단계 전에 새 대상 하위 폴더를 이미 생성 해야 합니다. 폴더 선택 대화 상자는이 단계에서는 하위 폴더를 만들 수 없습니다. 
    
    **다음**을 클릭한 후 **마침**을 클릭합니다. 
1. Vm을 재배치 되 면 클러스터로 추가 **고가용성** 개체:
    1. 업그레이드 된 RD 가상화 호스트 서버에서 장애 조치 클러스터 관리자를 엽니다. 
    1. 마우스 오른쪽 단추로 클릭 합니다 **역할** 노드를 차례로 클릭 한 다음 **역할 구성**합니다. 클릭 **다음** 에 **시작** 고가용성 마법사의 페이지입니다. 
    1. 선택할 **가상 머신** 클릭 하 고 사용 가능한 역할 목록에서 **다음**합니다. 구성 되지 않은 Vm의 목록이 표시 됩니다. 
    1. 모든 Vm을 선택 합니다. 클릭 **다음** 을 클릭 한 다음 **다음** 구성 태스크를 시작 하려면 확인 페이지에서 다시 합니다.  
1. 모든 Vm을 재배치 하 되 면 나머지 RDVH 서버를 업그레이드 합니다. VM 위치 적절 하 게 분산 하는 것에 대 한 위의 단계를 따르십시오.

> [!NOTE]  
> 유형이 다른 Hyper-v 서버는 클러스터에 지원 되지 않습니다. 
