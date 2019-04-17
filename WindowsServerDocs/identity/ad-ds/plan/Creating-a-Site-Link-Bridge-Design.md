---
ms.assetid: 64142026-07b5-4601-840a-c8dcf6ab9814
title: "사이트 링크 다리 디자인 만들기"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 58dda7c1f56fa3799b902ab5458e71323047ec73
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/12/2017
---
# <a name="creating-a-site-link-bridge-design"></a>사이트 링크 다리 디자인 만들기

>적용 대상: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

사이트 링크 다리 연결 두 또는 더 사이트 링크 사이트 링크 간의 전이성 수 있도록 합니다. 다리의 각 사이트 링크 사이트에이 다리의 다른 사이트 링크와 마찬가지로 있어야 합니다. 정보 일관성 검사 (KCC) 각 사이트 링크 한 사이트 링크의 사이트와에서 다른 사이트 연결에이 다리의 사이트 간의 복제 비용을 계산 하는 정보를 사용 합니다. KCC을 사이트 링크 간에 일반적인 사이트의 존재를 않고도 간에 사이트 동일한 사이트 링크 다리 하 여 연결 되어 있는 도메인 컨트롤러에에서 직접 연결도 설정할 수 없습니다.  
  
모든 사이트 링크는 기본적으로 전이적입니다. 사용 하지의 기본값을 변경 하 여 전이성 유지 하는 것이 좋습니다 **모든 사이트 링크를 줄이는** (기본적으로 사용 가능). 그러나 사용 하지 않도록 설정 해야 합니다 **모든 사이트 링크를 줄이는** 경우 사이트 링크 다리 디자인을 완료 하 고 있습니다.  
  
-   IP 네트워크 완전히 라우팅되지 되었습니다. 비활성화 하면 **모든 사이트 링크를 줄이는**, 모든 사이트 링크, 비전이 정보로 간주 되어 및 만들고 사이트 링크 다리 개체 모델 네트워크의 실제 라우팅 동작을 구성할 수 있습니다.  
  
-   (AD DS) Active Directory Domain Services에서에서 변경한 복제 흐름 제어 해야 합니다. 사용 하지 않도록 설정 하 여 **모든 사이트 링크를 줄이는** 사이트 링크 다리 사이트 링크 IP 전송 하 고 사이트 링크 다리 구성에 대 한 네트워크 연결이 끊긴된에 해당 됩니다. 사이트 링크 다리에 포함 된 모든 사이트 링크, 전이적 경로 설정할 수 있지만 사이트 링크 다리 외 라우팅되지 합니다.  
  
사용 하지 않도록 설정 Active Directory 사이트 및 서비스 스냅인을 사용 하는 방법에 대 한 자세한 내용은 **모든 사이트 링크를 줄이는** 사이트 링크 다리 사용 하지 않도록 설정 또는 참고 설정을 ([https://go.microsoft.com/fwlink/?LinkId=107073](https://go.microsoft.com/fwlink/?LinkId=107073)) 합니다.  
  
## <a name="controlling-ad-ds-replication-flow"></a>AD DS 복제 흐름을 제어  
두 개의 시나리오 복제 흐름을 제어 하는 사이트 링크 다리 디자인 해야 복제 장애 조치를 제어 하 고 방화벽을 통해 복제 제어 포함 됩니다.  
  
### <a name="controlling-replication-failover"></a>복제 장애 조치를 제어합니다.  
조직에는-hub-and-spoke 네트워크 토폴로지, 경우 일반적으로 하지 않을 모든 도메인 컨트롤러 hub 사이트에 실패 하는 경우 다른 위성 사이트로 복제 연결 만드는 위성 사이트 합니다. 사용 하지 않아야 이러한 시나리오에서 **모든 사이트 링크를 줄이는** 복제 연결이 위성 사이트와 하나 또는 두 개만 홉 위성 사이트를 사용 하지 않은 다른 hub 사이트 간에 만들어집니다 있도록 사이트 링크 다리 생성 하 고 있습니다.  
  
### <a name="controlling-replication-through-a-firewall"></a>방화벽을 통해 복제 제어  
하는 경우 두 가지 사이트에서 동일한 도메인 나타내는 두 도메인 컨트롤러 특별히 수 서로 통신할 방화벽을 통해만 비활성화할 수 있습니다 **모든 사이트 링크를 줄이는** 같은 방화벽 쪽에 사이트에 대 한 링크 브리지 사이트를 만듭니다. 따라서 네트워크 방화벽으로 구분 됩니다, 좋습니다 전이성 사이트 링크를 사용 하지 않도록 설정 하 고 네트워크에 대 한 링크 브리지 사이트 한쪽 방화벽 만들기. 방화벽을 통해 복제 관리에 대 한 정보를 참조 방화벽으로 분할 된 네트워크에 대 한 Active Directory ([https://go.microsoft.com/fwlink/?LinkId=107074](https://go.microsoft.com/fwlink/?LinkId=107074)).  
  


