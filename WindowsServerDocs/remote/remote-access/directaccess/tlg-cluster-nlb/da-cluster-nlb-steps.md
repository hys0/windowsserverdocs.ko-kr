---
title: DirectAccess 클러스터-NLB 테스트 랩 구성 단계
description: 이 항목은 테스트 랩 가이드-windows Server 2016 용 Windows NLB를 사용 하는 클러스터의 DirectAccess 시연에 포함 되어 있습니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c4f683cd9745bdb61ee95d89bcfc37622a4acf2c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853016"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>DirectAccess 클러스터-NLB 테스트 랩 구성 단계

>적용 대상: Windows Server(반기 채널), Windows Server 2016

다음 단계에서는 원격 액세스 인프라를 구성 하 고, 원격 액세스 서버 및 클라이언트를 구성 하 고, 인터넷 및 Ho Et 서브넷에서 DirectAccess 연결을 테스트 하는 방법을 설명 합니다.  
  
이 테스트 랩 가이드에서는 다음 단계를 수행 하 여 NLB (네트워크 부하 분산) 사용 원격 액세스 클러스터를 구축 합니다.  
  
-   [1 단계 DirectAccess 구성을 완료](STEP-1-Complete-the-DirectAccess-Configuration.md)합니다. [테스트 랩 가이드: IPv4 및 IPv6 혼합을 사용 하 여 DirectAccess 단일 서버 설정 시연](https://go.microsoft.com/fwlink/p/?LinkId=237004)의 모든 단계를 완료 합니다.  
  
-   [2 단계: EDGE1 구성](STEP-2-Configure-EDGE1.md) 부하 분산을 위해 EDGE1에 대 한 원격 액세스 역할을 구성 합니다.  
  
-   [3 단계: EDGE2 설치 및 구성](STEP-3-Install-and-Configure-EDGE2.md) EDGE2는 원격 액세스 클러스터의 두 번째 원격 액세스 서버 역할을 합니다.  
  
-   [4 단계: 네트워크 부하 분산 된 원격 액세스 클러스터 만들기](STEP-4-Create-the-Network-Load-Balanced-Remote-Access-Cluster.md)-EDGE1는 원격 액세스 클러스터의 첫 번째 서버로 구성 됩니다. EDGE2가 클러스터에 연결 되 고 NLB가 클러스터에 대해 구성 됩니다.  
  
-   [5 단계: 인터넷 및 클러스터를 통해 DirectAccess 연결을 테스트](STEP-5-Test-DirectAccess-Connectivity-from-the-Internet-and-Through-the-Cluster.md)합니다. NLB 및 클러스터 구성이 완료 되 면 부하 분산 된 클러스터를 통해 DirectAccess 클라이언트 연결을 테스트할 수 있습니다.  
  
-   [6 단계: NAT 장치 뒤에서 DirectAccess 클라이언트 연결을 테스트](STEP-6-Test-DirectAccess-Client-Connectivity-from-Behind-a-NAT-Device.md)합니다. 클라이언트 컴퓨터를 NAT 장치 뒤로 이동 하 여 홈 라우터 뒤에서 DirectAccess 클라이언트 연결 테스트를 시뮬레이션 합니다.  
  
-   [7 단계: Corpnet으로 돌아갈 때 연결을 테스트](STEP-7-Test-Connectivity-When-Returning-to-the-Corpnet.md)합니다. Corpnet으로 돌아갈 때 클라이언트 컴퓨터가 회사 리소스에 계속 액세스할 수 있는지 확인 합니다.  
  
-   [8 단계: 구성 스냅숏 만들기](da-cluster-nlb-s8-snapshot.md) 테스트 랩을 완료 한 후 나중에 다시 돌아가서 추가 시나리오를 테스트할 수 있도록 작동 하는 원격 액세스 NLB 클러스터의 스냅숏을 만듭니다.  
  


