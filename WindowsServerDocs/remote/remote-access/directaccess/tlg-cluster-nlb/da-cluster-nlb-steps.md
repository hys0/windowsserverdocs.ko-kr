---
title: DirectAccess 클러스터-NLB 테스트 랩 구성 단계
description: 이 항목은 일부 테스트 랩 가이드-Windows Server 2016 Windows NLB를 사용 하 여 클러스터에서 DirectAccess 시연
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2ebda017b41f27c2f69c7b850de44e771732415d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283325"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>DirectAccess 클러스터-NLB 테스트 랩 구성 단계

>적용 대상: Windows Server (반기 채널), Windows Server 2016

다음 단계는 원격 액세스 인프라 구성, 원격 액세스 서버 및 클라이언트를 구성, 인터넷 및 Homenet 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드는 부하 분산 (NLB (네트워크)을 만들 수 있습니다 다음 단계를 수행 하 여 원격 액세스 클러스터를 사용:  
  
-   [1 단계 DirectAccess 구성을 완료할](STEP-1-Complete-the-DirectAccess-Configuration.md)합니다. 모든 단계를 완료 합니다 [테스트 랩 가이드: IPv4 및 IPv6을 사용 하 여 DirectAccess 단일 서버 설치 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004)합니다.  
  
-   [2단계: EDGE1 구성](STEP-2-Configure-EDGE1.md)합니다. EDGE1에서 부하 분산에 대 한 원격 액세스 역할을 구성 합니다.  
  
-   [3단계: 설치 및 구성 EDGE2](STEP-3-Install-and-Configure-EDGE2.md)합니다. EDGE2 원격 액세스 클러스터의 두 번째 원격 액세스 서버로 작동합니다.  
  
-   [4단계: 네트워크 부하 분산 된 원격 액세스 클러스터를 만들](STEP-4-Create-the-Network-Load-Balanced-Remote-Access-Cluster.md)-EDGE1 원격 액세스 클러스터의 첫 번째 서버로 구성 됩니다. EDGE2는 클러스터에 가입 하 고 NLB 클러스터에 대해 구성 된 키를 누릅니다.  
  
-   [5단계: 클러스터를 통해 인터넷에서 DirectAccess 연결을 테스트](STEP-5-Test-DirectAccess-Connectivity-from-the-Internet-and-Through-the-Cluster.md)합니다. NLB 및 클러스터 구성이 완료 된 후에 부하 분산 된 클러스터를 통해 DirectAccess 클라이언트 연결을 테스트할 수 있습니다.  
  
-   [6단계: NAT 장치 뒤에서 DirectAccess 클라이언트 연결을 테스트](STEP-6-Test-DirectAccess-Client-Connectivity-from-Behind-a-NAT-Device.md)합니다. 홈 라우터 뒤에서 DirectAccess 클라이언트 연결 테스트를 시뮬레이션 하는 NAT 장치 뒤에 클라이언트 컴퓨터를 이동 합니다.  
  
-   [7단계: Corpnet에 반환 하는 경우 연결을 테스트](STEP-7-Test-Connectivity-When-Returning-to-the-Corpnet.md)합니다. 클라이언트 컴퓨터가 Corpnet에 반환 하는 경우 회사 리소스 액세스 여전히 수 있는지 확인 합니다.  
  
-   [8단계: 구성 스냅숏 만들기](da-cluster-nlb-s8-snapshot.md)합니다. 테스트 실습을 마친 후 나중에 추가 시나리오를 테스트할로 돌아갈 수 있도록 원격 액세스 NLB 클러스터 작업의 스냅숏을 만듭니다.  
  


