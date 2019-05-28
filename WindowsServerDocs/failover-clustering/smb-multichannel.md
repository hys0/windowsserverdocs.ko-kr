---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: 간소화된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 1b9271ceac99ac9b21cbfac902ba133d66815df4
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476122"
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>간소화된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크

> 적용 대상: Windows Server 2019, Windows Server 2016

SMB 다중 채널 및 다중-간체<abbr title="네트워크 인터페이스 카드">NIC</abbr> 클러스터 네트워크는 동일한 클러스터 네트워크 서브넷에 여러 Nic 사용 하도록 설정 하 고 자동으로 SMB 다중 채널을 활성화 하는 기능입니다.

간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크는 다음과 같은 이점을 제공 합니다.  
- 모든 Nic는 동일한 스위치를 사용 하는 노드에서 자동으로 인식 장애 조치 클러스터링 동일한 / 서브넷-추가 구성이 필요 없는 합니다.  
- SMB 다중 채널은 자동으로 활성화 됩니다.  
- 클러스터 전용 (private) 네트워크에서 IPv6 링크 로컬 (fe80) IP 주소 리소스에만 있는 네트워크 인식 됩니다.  
- 단일 IP 주소 리소스는 기본적으로 각 클러스터 액세스 지점 (CAP) 네트워크 이름 (NN)에서 구성 됩니다.  
- 클러스터 유효성 검사는 더 이상 동일한 서브넷에 여러 nic가 발견 되 면 경고 메시지를 발급 합니다.  

## <a name="requirements"></a>요구 사항  
-   동일한 스위치를 사용 하 여 서버당 여러 Nic / 서브넷입니다.  

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>네트워크 및 간소화 된 SMB 다중 채널 클러스터 하는 다중 NIC 기능을 활용 하는 방법  
이 섹션에서는 새 다중 NIC 클러스터 네트워크와 간소화 된 SMB 다중 채널 기능을 활용 하는 방법을 설명 합니다.  

### <a name="use-at-least-two-networks-for-failover-clustering"></a>장애 조치 클러스터링에 대 한 두 개 이상의 네트워크를 사용 합니다.   
드문 경우에 네트워크 스위치에 실패할 수 있습니다-장애 조치 클러스터링에 대 한 두 개 이상의 네트워크를 사용 하려면 여전히 모범 사례입니다. 발견 되는 모든 네트워크는 클러스터 하트 비트에 사용 됩니다. 단일 실패 지점을 방지 하기 위해 장애 조치 클러스터에 대 한 단일 네트워크를 사용 하지 마십시오. 이상적으로 없어야 여러 실제 통신 경로 클러스터의 노드 사이의 단일 실패 지점이 없게 합니다.  

![장애 조치 클러스터링에 대 한 두 네트워크의 그림](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)  
**그림 1: 장애 조치 클러스터링에 대 한 두 개 이상의 네트워크를 사용 합니다.**  

### <a name="use-multiple-nics-across-clusters"></a>클러스터에서 사용 하 여 여러 Nic  

-저장소 및 저장소 워크 로드가 클러스터의 클러스터에서 여러 nic가 사용 하는 경우 간소화 된 SMB 다중 채널의 이익을 극대화할 수 있습니다. 이 네트워크의 효율적 사용에서 워크 로드가 클러스터를 (Hyper-v, SQL Server Failover Cluster Instance, 저장소 복제본 등) SMB 다중 채널 및 결과 사용할 수 있습니다. (세분화 라고도) 수렴 형 클러스터를 스케일 아웃 파일 서버 클러스터를 Hyper-v에 대 한 작업 데이터를 저장 하는 데는 또는 SQL Server 장애 조치 클러스터 인스턴스의 클러스터에이 네트워크에 "북-남 서브넷" 라고 구성/네트워크 . 많은 고객이 RDMA 가능 NIC 카드 및 스위치에 투자 하 여이 네트워크의 처리량을 최대화 합니다.  

![북-남 SMB 서브넷의 그림](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)  
**그림 2: 최대 네트워크 처리량을 달성 하려면 여러 Nic를 사용 하 여 스케일 아웃 파일 서버 클러스터 및 Hyper-v 또는 SQL Server 장애 조치 클러스터 인스턴스의 클러스터 모두에서-북-남 서브넷을 공유 하는**  

![동일한 서브넷에 여러 Nic를 사용 하 여 SMB 다중 채널을 활용 하 여 두 클러스터의 스크린샷](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)  
**그림 3: 두 클러스터 (storage, SQL Server에 대 한 스케일 아웃 파일 서버 <abbr title="인스턴스를 클러스터링 하는 장애 조치">FCI</abbr> 워크 로드에 대 한) 둘 다 동일한 서브넷에 여러 Nic를 사용 하 여 SMB 다중 채널을 활용 하 고 더 나은 네트워크를 달성 하려면 처리량입니다.** 

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>IPv6 링크 로컬 개인 네트워크의 자동 인식  
다중 Nic이 있는 개인 (클러스터에만 해당) 네트워크 감지 되 면 클러스터는 자동으로 인식 IPv6 링크 로컬 (fe80) IP 주소 각 NIC에 대 한 각 서브넷에 있습니다. 이 저장 관리자 시간 이상 IPv6 링크 로컬 (fe80) IP 주소 리소스를 수동으로 구성 해야 하기 때문입니다.  

둘 이상의 (클러스터에만 해당) 개인 네트워크를 사용 하는 경우 이렇게 하면 네트워크 성능을 줄일 수 있으므로 서브넷 간 라우팅가 구성 되지 않았음을 확인 IPv6 라우팅 구성을 확인 합니다.  

![장애 조치 클러스터 관리자 UI에서 자동 네트워크 구성의 스크린샷](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)  
**그림 4: 자동 IPv6 링크 로컬 (fe80) 주소 리소스 구성**  

## <a name="throughput-and-fault-tolerance"></a>처리량 및 내결함성  
Windows Server 2016 및 Windows Server 2019 자동으로 NIC 기능을 검색 하 고 가능한 가장 빠른 구성에서 각 NIC를 사용 하려고 합니다. Nic 팀으로 구성 되는, RSS를 사용 하 여 Nic 및 RDMA 기능을 사용 하 여 Nic를 모두 사용할 수 있습니다. 다음 표에서 이러한 기술을 사용 하는 경우 균형 요약 합니다. 최대 처리량은 여러 RDMA 가능 Nic를 사용 하는 경우 수행 됩니다. 자세한 내용은 [SMB Mutlichannel의 기본 사항을](https://blogs.technet.microsoft.com/josebda/2012/06/28/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0/)합니다.

![여러 NIC 구성에 대 한 처리량 및 내결함성의 예시](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)  
**그림 5: 다양 한 NIC conifigurations에 대 한 처리량 및 내결함성**   

## <a name="frequently-asked-questions"></a>질문과 대답  
**다중 NIC 네트워크의 모든 Nic는 클러스터 심장 박동을 검사에 대 한 사용 하나요?**  
    예  

**다중 NIC 네트워크를 사용할 수만 클러스터 통신에 있나요? 수 고만 통신에 사용할 클라이언트와 클러스터 여부**  
    하거나 구성이 작동-모든 클러스터 네트워크 역할 다중 NIC 네트워크에서 작동 합니다.  

**SMB 다중 채널 에서도 CSV 및 클러스터 트래픽에 대 한?**  
    예, 기본적으로 모든 클러스터 및 CSV 트래픽에 사용할 수 있는 다중 NIC 네트워크 사용 합니다. 관리자는 장애 조치 클러스터링 PowerShell cmdlet 또는 장애 조치 클러스터 관리자 UI 사용 하 여 네트워크 역할을 변경할 수 있습니다.  

**SMB 다중 채널 설정을 확인 하려면 어떻게 해야 하나요?**  
    사용 된 **Get SMBServerConfiguration** cmdlet EnableMultiChannel 속성의 값을 찾습니다.  

**다중 NIC 네트워크 PlumbAllCrossSubnetRoutes 적용 클러스터의 공용 속성 기능**  
     예  

## <a name="see-also"></a>참조  
- [Windows Server에서 장애 조치 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)  
