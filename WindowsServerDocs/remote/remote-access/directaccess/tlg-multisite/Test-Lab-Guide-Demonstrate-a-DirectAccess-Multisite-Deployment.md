---
title: 테스트 랩 가이드-DirectAccess 멀티 사이트 배포 시연
description: 이 항목에서는 테스트 랩 가이드의 일부인-DirectAccess 멀티 사이트 배포에 대 한 Windows Server 2016를 보여 줍니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c98106c-67cc-406a-810e-f2e09f7e2c5e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 87c1f629d96d247d273d48066797795b9fe724e6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281387"
---
# <a name="test-lab-guide-demonstrate-a-directaccess-multisite-deployment"></a>테스트 랩 가이드: DirectAccess 멀티 사이트 배포 시연

>적용 대상: Windows Server (반기 채널), Windows Server 2016

원격 액세스는 원격 사용자가 안전 하 게 DirectAccess 또는 RRAS VPN을 사용 하 여 내부 네트워크 리소스에 액세스할 수 있는 Windows Server 2016, Windows Server 2012 R2 및 Windows Server 2012 운영 체제에서 서버 역할입니다. 이 가이드에는 확장에 대 한 단계별 지침이 포함 되어 있습니다.는 [테스트 랩 가이드: IPv4 및 IPv6을 사용 하 여 DirectAccess 단일 서버 설치 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004) 멀티 사이트 시나리오에서 원격 액세스를 보여 줍니다.  
  
원격 액세스 멀티 사이트 시나리오에서 배포할 지리적 위치에 원격 액세스 서버를 구성할 수 있습니다. 이전에 원격 사용자가 항상 특정 DirectAccess 서버를 통해 회사 네트워크에 연결 해야 했습니다. Windows Server 2016, Windows Server 2012 R2 또는 Windows Server 2012 및 Windows 10 또는 Windows 8을 사용 하 여 배포의 각 지리적 위치에 대 한 진입점을 구성할 수 있습니다. 각 진입점에는 단일 원격 액세스 서버 또는 원격 액세스 서버의 클러스터 수 있습니다. 원격 사용자가 회사의 원격 액세스 진입점에 연결 하는 옵션이 있습니다. 예를 들어 원격 사용자 아시아에 있는 원격 액세스 진입점에 일반적으로 연결 하지만 그런 다음 유럽 이동 출장 경우 클라이언트 컴퓨터 자동으로 연결할 가장 가까운 원격 액세스 진입점입니다.  
  
## <a name="about-this-guide"></a>이 가이드 정보  
이 가이드를 구성 및 시연 9 명의 서버 한 개와 클라이언트 컴퓨터를 사용 하 여 원격 액세스에 대 한 지침을 포함 합니다. 완료 된 원격 액세스 멀티 사이트 테스트 랩 인트라넷, 인터넷 및 홈 네트워크 시뮬레이션 및 다른 인터넷 연결 시나리오에서 원격 액세스 기능을 보여 줍니다.  
  
> [!IMPORTANT]  
> 이 랩을 통해 컴퓨터의 개수를 최소한으로 사용하는 개념을 파악할 수 있습니다. 이 가이드에 나와 있는 세부 구성은 테스트 랩 전용이므로, 프로덕션 환경에서 사용해서는 안 됩니다.  
  


