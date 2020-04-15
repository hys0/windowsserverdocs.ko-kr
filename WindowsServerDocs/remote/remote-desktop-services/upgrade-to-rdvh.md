---
title: 원격 데스크톱 가상화 호스트를 Windows Server 2016으로 업그레이드
description: 이 문서에서는 기존 원격 데스크톱 서비스 배포를 Windows Server 2016으로 업그레이드하는 방법을 설명합니다.
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.topic: article
ms.assetid: 5aed8ba7-f541-4416-b01c-4d3b1712e2b1
author: spatnaik
manager: scottman
ms.openlocfilehash: 7bbf5f6a81a18303d4f9f4b02a1b8dead3c9a53a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857116"
---
# <a name="upgrading-your-remote-desktop-virtualization-host-to-windows-server-2016"></a>원격 데스크톱 가상화 호스트를 Windows Server 2016으로 업그레이드

>적용 대상: Windows Server(반기 채널), Windows Server 2016

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 역할이 설치된 지원되는 OS 업그레이드
Windows Server 2016으로의 업그레이드는 Windows Server 2012 R2 및 Windows Server 2016 TP5에서만 지원됩니다.

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-locally"></a>VM이 로컬로 저장된 배포의 RD 가상화 호스트 서버
이러한 서버는 모두 한 번에 업그레이드해야 합니다. 업그레이드하려면 다음 단계를 수행합니다.

1. 모든 사용자를 로그오프합니다.
1. 각 호스트에서 모든 가상 머신을 해제하거나 저장합니다. 
1. 서버를 Windows Server 2016으로 업그레이드합니다. 
1. 업그레이드가 완료된 후 모든 컬렉션이 사용 가능하고 작동해야 합니다.      

## <a name="rd-virtualization-host-servers-in-the-deployment-where-vms-are-stored-in-cluster-shared-volumes-csv"></a>VM이 CSV(클러스터 공유 볼륨)에 저장된 배포의 RD 가상화 호스트 서버 

1. RDVH 서버 중 일부는 업그레이드되고 일부는 Windows Server 2012 R2에서 계속해서 VM을 호스트하게 되는 업그레이드 전략을 결정합니다.  
2. 모든 VM을 '아직 업그레이드하지 않을' 다른 RDVH 서버로 마이그레이션하여 원래 2012 R2 클러스터의 일부로 유지함으로써 초기 업그레이드 라운드 대상으로 지정한 하나 이상의 RDVH 서버를 격리합니다.
    1. 장애 조치(failover) 클러스터 관리자를 엽니다. 
    1. **역할**을 클릭합니다. 
    1. 하나 이상의 VM을 선택합니다. 마우스 오른쪽 단추를 클릭하여 상황에 맞는 메뉴를 엽니다. 
    1. **이동**을 클릭하고 **실시간** 또는 **빠른 마이그레이션** 중 하나를 선택하여 VM을 초기 업그레이드에 속하지 않는 RD 가상화 호스트 서버 중 하나 이상으로 전환할 수 있습니다. 하드웨어 호환성 또는 온라인 요구 사항 등의 요인에 따라 **실시간** 또는 **빠른** 마이그레이션을 사용합니다. 
3. 업그레이드 준비가 완료된 RDVH 서버를 원본 클러스터에서 제거합니다. 
4. 격리된 RDVH 서버를 업그레이드합니다. 
5. 타기팅된 RDVH 서버를 성공적으로 업그레이드한 후 완전히 다른 SAN 볼륨에 있어야 하는 새 클러스터 및 CSV를 만듭니다.
6. 업그레이드한 모든 RDVH 서버를 새 클러스터에 가입합니다. 
7. 기존 CSV의 기존 폴더 구조를 모방하는 새 CSV의 폴더 구조를 만듭니다. 여기에는 컬렉션 폴더와 각 VM의 최상위 수준 하위 폴더가 포함됩니다. 
8. 원본 CSV의 다양한 VM 컬렉션 폴더에서 /IMGS 폴더 및 내용을 새 CSV의 동일한 위치에 있는 새 컬렉션 폴더로 복사합니다. 
9. 다음과 같이 원본 RDVH 머신에서 클러스터 관리자를 사용하여 고가용성을 위해 VM의 구성을 제거합니다.
    1. 클러스터 관리자를 시작합니다. 
    1. **역할**을 클릭합니다. 
    1. VM 개체를 마우스 오른쪽 단추로 클릭하고 **제거**를 클릭합니다. 
10. 업그레이드하지 않은 RDVH 서버 중 하나에서 Hyper-V 관리자를 사용하여 모든 VM을 업그레이드한 RDVH 서버 및 새 CSV 클러스터 중 하나로 이동합니다.
    1. Hyper-V 관리자를 엽니다. 
    2. 업그레이드하지 않은 RDVH 서버 중 하나를 선택합니다. 
    3. 이동할 VM 중 하나를 마우스 오른쪽 단추로 클릭하고 **이동**을 클릭합니다. 
    4. **가상 머신 이동**을 선택하고 **다음**을 클릭합니다. 
    5. **대상 컴퓨터 지정** 페이지에서 대상을 지정한 업그레이드된 RDVH 서버 이름을 지정한 후, **다음**을 클릭합니다. 
    6. **가상 머신의 데이터를 단일 위치로 이동**을 선택한 후, **다음**을 클릭합니다. 
    7. 대상 위치로 이동합니다. 
       > [!IMPORTANT]
       > 이 경로가 특정 VM의 빈 폴더인지 확인합니다. 

       > [!NOTE]
       > 앞서 설명한 것처럼 이 단계 이전에 새 대상 하위 폴더를 이미 생성했어야 합니다. 이 단계에서는 폴더 선택 대화 상자에서 하위 폴더를 만들 수 없습니다. 
    
       **다음**을 클릭한 후 **마침**을 클릭합니다. 
11. VM이 재배치되면 클러스터 **고가용성** 개체로 추가합니다.
     1. 업그레이드된 RD 가상화 호스트 서버에서 장애 조치(failover) 클러스터 관리자를 엽니다. 
     1. **역할** 노드를 마우스 오른쪽 단추로 클릭하고 **역할 구성**을 클릭합니다. 고가용성 마법사의 **시작** 페이지에서 **다음**을 클릭합니다. 
     1. 사용 가능한 역할 목록에서 **가상 머신**을 선택하고 **다음**을 클릭합니다. 구성되지 않은 VM의 목록이 표시됩니다. 
     1. 모든 VM을 선택합니다. **다음**을 클릭하고, 확인 페이지에서 **다음**을 다시 클릭하여 구성 작업을 시작합니다.  
12. 모든 VM을 재배치했으면 나머지 RDVH 서버를 업그레이드합니다. VM 위치를 적절히 분산하기 위해서는 위의 단계를 따릅니다.

> [!NOTE]  
> 클러스터에서 유형이 다른 Hyper-V 서버는 지원되지 않습니다. 
