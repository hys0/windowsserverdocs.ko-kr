---
title: DirectAccess 클러스터-NLB 테스트 랩 구성 단계
description: 이 항목은 테스트 랩 가이드-windows Server 2016 용 Windows NLB를 사용 하는 클러스터의 DirectAccess 시연에 포함 되어 있습니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 108c63298ad3382f5ece790258f2d278bb03b78b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388398"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>DirectAccess 클러스터-NLB 테스트 랩 구성 단계

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 단계에서는 원격 액세스 인프라를 구성 하 고, 원격 액세스 서버 및 클라이언트를 구성 하 고, 인터넷 및 Ho Et 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드에서는 다음 단계를 수행 하 여 NLB (네트워크 부하 분산) 사용 원격 액세스 클러스터를 구축 합니다.  
  
-   [1 단계 DirectAccess 구성을 완료](STEP-1-Complete-the-DirectAccess-Configuration.md)합니다. @No__t-0 테스트 랩 가이드의 모든 단계를 완료 합니다. IPv4 및 IPv6 @ no__t를 혼합 하 여 DirectAccess 단일 서버 설치를 시연 합니다.  
  
-   [2단계: EDGE1 @ no__t-0을 구성 합니다. 부하 분산을 위해 EDGE1에 대 한 원격 액세스 역할을 구성 합니다.  
  
-   [3단계: EDGE2 @ no__t-0을 설치 하 고 구성 합니다. EDGE2는 원격 액세스 클러스터의 두 번째 원격 액세스 서버 역할을 합니다.  
  
-   [4단계: 네트워크 부하 분산 원격 액세스 클러스터 만들기 @ no__t-0-EDGE1가 원격 액세스 클러스터의 첫 번째 서버로 구성 됩니다. EDGE2가 클러스터에 연결 되 고 NLB가 클러스터에 대해 구성 됩니다.  
  
-   [5단계: 인터넷에서 및 클러스터 (@ no__t-0)를 통해 DirectAccess 연결을 테스트 합니다. NLB 및 클러스터 구성이 완료 되 면 부하 분산 된 클러스터를 통해 DirectAccess 클라이언트 연결을 테스트할 수 있습니다.  
  
-   [6단계: NAT 장치 뒤에서 DirectAccess 클라이언트 연결을 테스트 @ no__t-0. 클라이언트 컴퓨터를 NAT 장치 뒤로 이동 하 여 홈 라우터 뒤에서 DirectAccess 클라이언트 연결 테스트를 시뮬레이션 합니다.  
  
-   [7단계: Corpnet @ no__t-0으로 돌아갈 때 연결을 테스트 합니다. Corpnet으로 돌아갈 때 클라이언트 컴퓨터가 회사 리소스에 계속 액세스할 수 있는지 확인 합니다.  
  
-   [8단계: 구성의 스냅숏 @ no__t-0 테스트 랩을 완료 한 후 나중에 다시 돌아가서 추가 시나리오를 테스트할 수 있도록 작동 하는 원격 액세스 NLB 클러스터의 스냅숏을 만듭니다.  
  


