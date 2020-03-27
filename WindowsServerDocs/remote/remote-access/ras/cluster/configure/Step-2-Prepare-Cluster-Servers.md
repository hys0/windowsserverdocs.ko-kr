---
title: 클러스터 서버를 준비 하는 2 단계
description: 이 항목은 Windows Server 2016의 클러스터에 원격 액세스 배포 가이드의 일부입니다.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 35d68abb-6914-42e0-91e8-803933cf785e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 74aac416a5aa69a0cd935d58e3ecb931e4b5fd02
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/26/2020
ms.locfileid: "80308333"
---
# <a name="step-2-prepare-cluster-servers"></a>클러스터 서버를 준비 하는 2 단계

>적용 대상: Windows Server(반기 채널), Windows Server 2016

클러스터 배포를 구성 하려면 먼저 클러스터에 추가 하려면 추가 서버를 준비 합니다.  
  
|작업|설명|  
|----|--------|  
|[2.1 원격 액세스 인프라 구성](#BKMK_config)|클러스터에 추가 하려는 각 서버에서 서버 토폴로지, IP 주소 지정, 라우팅 및 전달을 구성 합니다. 가상 컴퓨터의 부하 분산 된 클러스터를 구성 하는 경우에 MAC 주소 스푸핑을 사용 하도록 가상 컴퓨터를 구성 해야 합니다.<br /><br />또한 각 서버를 동일한 도메인에 가입 하 고 모든 서버를 동일한 서브넷에 연결 합니다.|  
|[2.2 원격 액세스 역할 설치](#BKMK_Install)|클러스터에 추가 하려는 각 추가 서버에서 원격 액세스 역할 설치|  
|[2.3 NLB 설치](#BKMK_NLB)|배포 된 원격 액세스 서버와 클러스터에 추가 하려는 각 추가 서버에서 NLB 기능을 설치 합니다. 이 단계는는 외부 부하 분산 장치를 사용 하는 경우에 필요 합니다.|  
  
## <a name="21-configure-the-remote-access-infrastructure"></a><a name="BKMK_config"></a>2.1 원격 액세스 인프라 구성  
원격 액세스 클러스터를 구성 하려면 서버 토폴로지, IP 주소 지정, 라우팅 및 전달을 구성 해야 클러스터의 일부를 구성 하는 모든 서버에 있습니다.  
  
### <a name="to-configure-the-remote-access-infrastructure"></a>원격 액세스 인프라를 구성 하려면  
  
1.  각각의 첫 번째 원격 액세스 서버와 동일한 토폴로지를 사용 하 여 클러스터에 있는 서버를 구성 합니다.  
  
2.  각 클러스터에 적절 한 IP 주소 지정, 라우팅 및 첫 번째 원격 액세스 서버 구성에 따라 전달 될 서버를 구성 합니다. 클러스터의 모든 서버는 동일한 서브넷에 연결 해야 하는 참고 합니다.  
  
3.  각 클러스터의 첫 번째 원격 액세스 서버와 동일한 도메인에 있는 서버를 가입 시킵니다.  
  
## <a name="22-install-the-remote-access-role"></a><a name="BKMK_Install"></a>2.2 원격 액세스 역할 설치  
원격 액세스 클러스터를 구성 하려면 클러스터의 일부를 구성 하는 모든 서버에 대 한 원격 액세스 역할을 설치 해야 합니다.  
  
### <a name="to-install-the-remote-access-role-on-always-on-vpn-servers"></a>Always On VPN 서버에 원격 액세스 역할을 설치 하려면  
  
1.  DirectAccess 서버의 서버 관리자 콘솔에는 **대시보드**, 클릭 **역할 및 기능 추가**합니다.  
  
2.  **다음** 을 세 번 클릭하여 서버 역할 선택 화면으로 이동합니다.  
  
3.  에 **서버 역할 선택** 대화 상자에서 **원격 액세스**, 를 클릭 하 고 **다음**합니다.  
  
4.  클릭 **다음** 3 번입니다.  
  
5.  에 **역할 서비스 선택** 대화 상자에서 **DirectAccess 및 VPN (RAS)** 클릭 하 고 **기능 추가**합니다.  
  
6.  선택 **라우팅**, 선택, **웹 응용 프로그램 프록시**, 클릭 **기능 추가**, 를 클릭 하 고 **다음**합니다.  
  
7. **다음**을 클릭한 후 **설치**를 클릭합니다.  
  
8.  **설치 진행률** 대화 상자에서 설치가 정상적으로 완료되었는지 확인하고 **닫기**를 클릭합니다.  
  
9.  클러스터 구성원으로 만들 수 있는 모든 서버에서이 절차를 반복 합니다.  
  
## <a name="23-install-nlb"></a><a name="BKMK_NLB"></a>2.3 NLB 설치  
원격 액세스 클러스터를 구성 하려면 클러스터의 일부를 구성 하는 모든 서버에서 네트워크 부하 분산 기능을 설치 해야 합니다.  
  
> [!NOTE]  
> 외부 부하 분산 장치를 사용 하는 경우에이 단계가 필요 하지 않습니다.  
  
#### <a name="to-install-the-nlb-role"></a>NLB 역할을 설치 하려면  
  
1.  DirectAccess 서버의 서버 관리자 콘솔에는 **대시보드**, 클릭 **역할 및 기능 추가**합니다.  
  
2.  클릭 **다음** 하 여 서버 기능 선택 화면을 4 번입니다.  
  
3.  에 **기능 선택** 대화 상자에서 **네트워크 로드 균형 조정**, 클릭 **기능 추가**, 클릭 **다음**, 를 클릭 하 고 **설치**.  
  
4.  **설치 진행률** 대화 상자에서 설치가 정상적으로 완료되었는지 확인하고 **닫기**를 클릭합니다.  
  
5.  클러스터 구성원으로 만들 수 있는 모든 서버에서이 절차를 반복 합니다.  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>참고 항목  
  
-   [3 단계: 부하 분산 된 클러스터 구성](Step-3-Configure-a-Load-Balanced-Cluster.md)  
  


