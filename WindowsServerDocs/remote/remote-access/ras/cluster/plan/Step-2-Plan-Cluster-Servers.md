---
title: 2 단계 클러스터 서버 계획
description: 이 항목은 Windows Server 2016의 클러스터에 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 673c5bfb-b590-4932-8e54-ca0a466d90cc
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7ac00278e501115d81d80f55c1ceae33a379cc4a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855246"
---
# <a name="step-2-plan-cluster-servers"></a>2 단계 클러스터 서버 계획

>적용 대상: Windows Server(반기 채널), Windows Server 2016

단일 원격 액세스 서버를 배포한 후 클러스터에 서버를 추가 하도록 계획 합니다.  
  
|작업|설명|  
|----|--------|  
|[2.1 역할 및 기능 설치](#BKMK_Install)|클러스터에 추가 될 각 서버에 대해 원격 액세스 역할 및 Windows NLB 기능 (필요한 경우)의 설치를 계획 하 고 토폴로지, IP 주소 지정, 라우팅 및 전달을 계획 합니다.|  
|[2.2 서버 설정 구성](#BKMK_Config)|클러스터에 추가할 각 서버에 대 한 설정을 구성 합니다. 가상 컴퓨터를 사용 하 여 서버에 대 한 부하 분산 클러스터를 구성할 수 있습니다. 라우팅 및 연결이 제대로 작동 하려면 MAC 주소 스푸핑을 사용 하도록 가상 컴퓨터를 구성 해야 합니다.|  
  
## <a name="21-installing-roles-and-features"></a><a name="BKMK_Install"></a>2.1 역할 및 기능 설치  
클러스터에 가입 하려는 각 서버에 대해 원격 액세스 역할을 설치 합니다. 또한 Windows NLB를 사용 하 여 클러스터에 대 한 트래픽 부하를 분산 하려면 NLB (네트워크 부하 분산) 기능을 설치 하는 계획을 세워야 합니다. 자세한 내용은 [네트워크 부하 분산](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing)을 참조 하세요.  
  
## <a name="22-configure-server-settings"></a><a name="BKMK_Config"></a>2.2 서버 설정 구성  
클러스터에 추가 될 각 서버에 대해 IP 주소 및 도메인 설정을 계획 합니다. 유의 사항은 다음과 같습니다.  
  
1.  클러스터의 서버는 모두 동일한 도메인에 속해야 합니다.  
  
2.  클러스터에 있는 서버는 동일한 서브넷에 있어야 합니다.  
  
3.  클러스터의 각 서버에는 DirectAccess 배포에 사용 되는 것과 동일한 수의 네트워크 어댑터가 있어야 합니다.  
  
Windows NLB를 사용 하 여 클러스터의 부하를 분산 하는 경우 다음 Windows NLB 설정이 적용 됩니다.  
  
1.  작업 모드-유니캐스트 NLB 관리자를 사용 하 여 멀티 캐스트로 변경할 수 있습니다. 이 설정은 원격 액세스 관리 콘솔에서 수정할 수 없습니다.  
  
2.  로드 가중치 비율-모든 클러스터 서버에 동일한 부하가 있는 동일 하 게 정의 됩니다.  
  
3.  필터링 모드-트래픽이 여러 호스트에서 부하가 분산 됩니다.  
  
4.  선호도-단일 선호도가 정의 됩니다.  
  
5.  프로토콜-모두  

