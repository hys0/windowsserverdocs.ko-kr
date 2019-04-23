---
title: 실시간 마이그레이션 개요
description: Windows Server 2016의 실시간 마이그레이션 기능 개요를 제공합니다.
ms.prod: windows-server-threshold
ms.service: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5cc875ab-05c4-439e-b27d-6bfc77054660
author: johncslack
ms.author: joslack
ms.date: 06/27/2017
ms.openlocfilehash: 2bbe897ffb8b200a72fac5a662e518d4a4be1131
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887854"
---
# <a name="live-migration-overview"></a>실시간 마이그레이션 개요

실시간 마이그레이션에는 Windows Server에서 Hyper-v 기능입니다.  이 통해 투명 하 게 인식된 가동 중지 시간 없이 다른 Hyper-v 호스트에서 실행 중인 가상 컴퓨터를 이동할 수 있습니다.  실시간 마이그레이션의 주요 장점은 유연성 실행 중인 가상 컴퓨터는 단일 호스트 컴퓨터에 연결 되지 않습니다.  따라서 드레이닝 해제 하거나 업그레이드 하기 전에 가상 머신의 특정 호스트 등의 작업을 수 있습니다.  Windows 장애 조치 클러스터링과 쌍을 이루는 실시간 마이그레이션 하면 항상 사용 가능한 생성 하 고 오류 허용 시스템입니다. 

## <a name="related-technologies-and-documentation"></a>관련된 기술 및 설명서

실시간 마이그레이션은 장애 조치 클러스터링 및 System Center Virtual Machine Manager 같은 몇 가지 관련 기술이 함께 자주 사용 됩니다.  이러한 기술을 통해 실시간 마이그레이션 사용 중인 경우 다음과 같습니다. 해당 최신 설명서에 대 한 포인터
* [장애 조치 클러스터링](../../../failover-clustering/failover-clustering-overview.md) (Windows Server 2016) 
* [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/) (System Center 2016) 

이전 버전의 Windows Server를 사용 하는 이전 버전의 Windows Server에 도입 된 기능에 대 한 정보가 필요한 경우 다음과 같습니다. 기록 설명서에 대 한 포인터 
* [실시간 마이그레이션](https://technet.microsoft.com/library/ee815293(v=ws.10).aspx) (Windows Server 2008 R2)  
* [실시간 마이그레이션](https://technet.microsoft.com/library/hh831435(v=ws.11).aspx) (Windows Server 2012 R2) 
* [장애 조치 클러스터링](https://technet.microsoft.com/library/hh831579(v=ws.11).aspx) (Windows Server 2012 R2)
* [장애 조치 클러스터링](https://technet.microsoft.com/library/ff182338(v=ws.10).aspx) (Windows Server 2008 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/gg610610.aspx) (System Center 2012 R2)
* [System Center Virtual Machine Manager](https://technet.microsoft.com/library/cc917964.aspx) (System Center 2008 R2)

## <a name="live-migration-in-windows-server-2016"></a>Windows Server 2016의에서 실시간 마이그레이션

Windows Server 2016에서 실시간 마이그레이션 배포에 대 한 제한이 있습니다.  이제 장애 조치 클러스터링 없이 작동합니다.  다른 기능은 실시간 마이그레이션의 이전 릴리스에서 변경 되지 않았습니다.  에 대 한 자세한 구성 및 장애 조치 클러스터링이 없는 실시간 마이그레이션 사용: 
* [장애 조치 클러스터링이 없는 실시간 마이그레이션에 대해 호스트 설정](../deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)
* [가상 머신을 이동 하려면 장애 조치 클러스터링이 없는 실시간 마이그레이션 사용](use-live-migration-without-failover-clustering-to-move-a-virtual-machine.md)