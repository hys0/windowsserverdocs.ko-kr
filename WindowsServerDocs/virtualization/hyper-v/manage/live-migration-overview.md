---
title: 실시간 마이그레이션 개요
description: Windows Server 2016의 실시간 마이그레이션 기능에 대 한 개요를 제공 합니다.
ms.prod: windows-server
ms.service: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc875ab-05c4-439e-b27d-6bfc77054660
author: johncslack
ms.author: joslack
ms.date: 06/27/2017
ms.openlocfilehash: ba239343728502c4928b86a2a0d4a3db5c36e7f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392549"
---
# <a name="live-migration-overview"></a>실시간 마이그레이션 개요

실시간 마이그레이션은 Windows Server의 Hyper-v 기능입니다.  가동 중지 시간을 발생 시 키 지 않고 실행 중인 Virtual Machines를 한 Hyper-v 호스트에서 다른 Hyper-v 호스트로 투명 하 게 이동할 수 있습니다.  실시간 마이그레이션의 주요 장점은 유연성입니다. Virtual Machines 실행은 단일 호스트 컴퓨터에 연결 되지 않습니다.  이렇게 하면 Virtual Machines의 특정 호스트를 해제 하거나 업그레이드 하기 전에이를 드레이닝 하는 등의 작업을 수행할 수 있습니다.  Windows 장애 조치 (Failover) 클러스터링과 함께 사용 하면 실시간 마이그레이션을 통해 항상 사용 가능한 내결함성 시스템을 만들 수 있습니다. 

## <a name="related-technologies-and-documentation"></a>관련 기술 및 설명서

실시간 마이그레이션은 장애 조치 (Failover) 클러스터링 및 System Center Virtual Machine Manager와 같은 몇 가지 관련 기술과 함께 사용 되는 경우가 많습니다.  이러한 기술을 통해 실시간 마이그레이션를 사용 하는 경우 최신 설명서에 대 한 포인터는 다음과 같습니다.
* [장애 조치 (Failover) 클러스터링](../../../failover-clustering/failover-clustering-overview.md) (Windows Server 2016) 
* [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/) (System Center 2016) 

이전 버전의 Windows Server를 사용 하는 경우 또는 이전 버전의 Windows Server에서 도입 된 기능에 대 한 자세한 내용은 다음을 참조 하세요. 
* [실시간 마이그레이션](https://technet.microsoft.com/library/ee815293(v=ws.10).aspx) (Windows Server 2008 R2)  
* [실시간 마이그레이션](https://technet.microsoft.com/library/hh831435(v=ws.11).aspx) (Windows Server 2012 R2) 
* [장애 조치 (Failover) 클러스터링](https://technet.microsoft.com/library/hh831579(v=ws.11).aspx) (Windows Server 2012 R2)
* [장애 조치 (Failover) 클러스터링](https://technet.microsoft.com/library/ff182338(v=ws.10).aspx) (Windows Server 2008 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/gg610610.aspx) (System Center 2012 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/cc917964.aspx) (System Center 2008 R2)

## <a name="live-migration-in-windows-server-2016"></a>Windows Server 2016의 실시간 마이그레이션

Windows Server 2016에는 실시간 마이그레이션 배포에 대 한 제한 사항이 더 있습니다.  이제 장애 조치 (Failover) 클러스터링 없이 작동 합니다.  다른 기능은 실시간 마이그레이션 이전 버전에서 변경 되지 않은 상태로 유지 됩니다.  장애 조치 클러스터링을 사용 하지 않고 실시간 마이그레이션을 구성 하 고 사용 하는 방법에 대 한 자세한 내용은 
* [장애 조치 (Failover) 클러스터링이 없는 실시간 마이그레이션에 대 한 호스트 설정](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)
* [장애 조치 (Failover) 클러스터링이 없는 실시간 마이그레이션을 사용 하 여 가상 머신 이동](use-live-migration-without-failover-clustering-to-move-a-virtual-machine.md)