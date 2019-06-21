---
title: 2 단계 계획 클러스터 서버
description: 이 항목은 Windows Server 2016에서 클러스터에 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 673c5bfb-b590-4932-8e54-ca0a466d90cc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0dcb14a03f02f931d59743f1b1b8b24b84ba8351
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282863"
---
# <a name="step-2-plan-cluster-servers"></a>2 단계 계획 클러스터 서버

>적용 대상: Windows Server (반기 채널), Windows Server 2016

단일 원격 액세스 서버를 배포한 후 클러스터에 추가 서버를 추가 하려고 합니다.  
  
|태스크|설명|  
|----|--------|  
|[2.1 역할 및 기능을 설치 하는](#BKMK_Install)합니다.|클러스터에 추가 될 각 서버에 대해 (필요한 경우) 원격 액세스 역할 및 Windows NLB 기능 설치에 대 한 계획, 토폴로지, IP 주소 지정, 라우팅 및 전달을 계획 합니다.|  
|[2.2 서버 설정 구성](#BKMK_Config)|클러스터에 추가 될 각 서버에 대 한 설정을 구성 합니다. 가상 컴퓨터를 사용 하 여 서버 클러스터를 분산 하는 참고 부하를 구성할 수 있습니다. 라우팅 및 연결에 대 한 제대로 작동 하려면 순서 대로 MAC 주소 스푸핑을 사용 하도록 가상 컴퓨터를 구성 해야 합니다.|  
  
## <a name="BKMK_Install"></a>2.1 역할 및 기능 설치  
클러스터에 조인 하려는 각 서버에 대 한 원격 액세스 역할을 설치 하려고 합니다. 또한 Windows NLB를 사용 하 여 클러스터에 트래픽 분산을 로드 하려는 경우 네트워크 로드 균형 조정 (NLB) 기능을 설치 하려고 합니다. 자세한 내용은 참조 [네트워크 로드 균형 조정](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing)합니다.  
  
## <a name="BKMK_Config"></a>2.2 서버 설정 구성  
클러스터에 추가 될 각 서버에 대 한 IP 주소 및 도메인 설정을 계획 합니다. 다음에 유의하세요.  
  
1.  클러스터의 서버에서에서 모두 동일한 도메인에 속해야 합니다.  
  
2.  클러스터의 서버는 동일한 서브넷에 있어야 합니다.  
  
3.  클러스터의 각 서버는 DirectAccess 배포에 사용 하 여 네트워크 어댑터 수가 있어야 합니다.  
  
Windows NLB를 사용 하 여 클러스터 균형을 로드 하는 경우 다음 Windows NLB 설정은 적용 됩니다.  
  
1.  -유니캐스트 작업 모드입니다. NLB 관리자를 사용 하 여 멀티 캐스트를 변경할 수 있습니다. 이 설정은 원격 액세스 관리 콘솔에서 수정할 수 없습니다.  
  
2.  모든 클러스터 서버가 있는 균등 한 부하 가중치 동일, 요소 정의 로드 합니다.  
  
3.  필터링 모드 트래픽을 부하를 분산할 수 여러 호스트 합니다.  
  
4.  선호도-단일 선호도 정의 됩니다.  
  
5.  프로토콜-모두  

