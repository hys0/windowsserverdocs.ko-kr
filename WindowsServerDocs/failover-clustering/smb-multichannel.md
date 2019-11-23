---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: 간소화된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크
ms.prod: windows-server
ms.technology: storage-failover-clustering
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 7816016daae1d06568cd6149791a9a368d8602f8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361106"
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>간소화된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크

> 적용 대상: Windows Server 2019, Windows Server 2016

간소화 된 SMB 다중 채널 및 다중<abbr title="네트워크 인터페이스 카드">NIC</abbr> 클러스터 네트워크는 동일한 클러스터 네트워크 서브넷에서 여러 Nic를 사용 하 고 자동으로 SMB 다중 채널을 사용 하도록 설정 하는 기능입니다.

간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크는 다음과 같은 이점을 제공 합니다.  
- 장애 조치 (Failover) 클러스터링은 동일한 스위치/동일한 서브넷을 사용 하는 노드의 모든 Nic를 자동으로 인식 하며 추가 구성은 필요 하지 않습니다.  
- SMB 다중 채널이 자동으로 설정 됩니다.  
- IPv6 링크 로컬 (fe80) IP 주소 리소스만 있는 네트워크는 클러스터 전용 (개인) 네트워크에서 인식 됩니다.  
- 기본적으로 각 클러스터 액세스 지점 (CAP) 네트워크 이름 (NN)에 단일 IP 주소 리소스가 구성 됩니다.  
- 동일한 서브넷에 여러 Nic가 있는 경우 클러스터 유효성 검사에서 더 이상 경고 메시지가 발생 하지 않습니다.  

## <a name="requirements"></a>요구 사항  
-   동일한 스위치/서브넷을 사용 하는 서버당 여러 Nic.  

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>다중 NIC 클러스터 네트워크 및 간소화 된 SMB 다중 채널을 활용 하는 방법  
이 섹션에서는 새로운 다중 NIC 클러스터 네트워크 및 간소화 된 SMB 다중 채널 기능을 활용 하는 방법을 설명 합니다.  

### <a name="use-at-least-two-networks-for-failover-clustering"></a>장애 조치 (Failover) 클러스터링용 네트워크를 두 개 이상 사용   
네트워크 스위치는 드물게 발생 하지만 장애 조치 (Failover) 클러스터링에는 두 개 이상의 네트워크를 사용 하는 것이 가장 좋습니다. 검색 된 모든 네트워크는 클러스터 하트 비트에 사용 됩니다. 단일 실패 지점을 방지 하기 위해 장애 조치 (Failover) 클러스터에 단일 네트워크를 사용 하지 않도록 합니다. 이상적으로 클러스터의 노드 간에는 여러 개의 실제 통신 경로가 있어야 하며 단일 실패 지점이 없어야 합니다.  

장애 조치 (Failover) 클러스터링용 두 네트워크에 대 한 ![그림](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)  
**그림 1: 장애 조치 (Failover) 클러스터링용 네트워크를 두 개 이상 사용**  

### <a name="use-multiple-nics-across-clusters"></a>클러스터에서 여러 Nic 사용  

저장소 및 저장소 워크 로드 클러스터에서 여러 Nic가 클러스터에서 사용 되는 경우 간소화 된 SMB 다중 채널의 최대 혜택을 얻을 수 있습니다. 이렇게 하면 워크 로드 클러스터 (Hyper-v, SQL Server 장애 조치 (Failover) 클러스터 인스턴스, 저장소 복제본 등)에서 SMB 다중 채널을 사용 하 여 네트워크를 보다 효율적으로 사용할 수 있습니다. 스케일 아웃 파일 서버 클러스터가 Hyper-v 또는 SQL Server 장애 조치 (Failover) 클러스터 인스턴스 클러스터에 대 한 워크 로드 데이터를 저장 하는 데 사용 되는 수렴 형 (세분화 된) 클러스터 구성에서는이 네트워크를 종종 "북 남부 서브넷"/네트워크 라고 합니다. 많은 고객이 RDMA 지원 NIC 카드 및 스위치에 투자 하 여이 네트워크의 처리량을 최대화 합니다.  

북-남 SMB 서브넷의 ![그림](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)  
**그림 2: 네트워크 처리량을 극대화 하려면 스케일 아웃 파일 서버 클러스터와 Hyper-v 또는 SQL Server 장애 조치 (Failover) 클러스터 인스턴스 클러스터에서 여러 Nic를 사용 합니다 .이 클러스터는 북-남부 서브넷을 공유 합니다.**  

SMB 다중 채널을 활용 하기 위해 동일한 서브넷에서 여러 Nic를 사용 하는 두 클러스터의 ![Screencap](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)  
**그림 3: 두 클러스터 (저장소 용 스케일 아웃 파일 서버, SQL Server <abbr title="장애 조치 (Failover) 클러스터링 인스턴스">FCI CI 워크 로드) 둘 다 동일한 서브넷에서 여러 Nic를 사용 하 여 SMB 다중 채널을 활용 하 고 더 나은 네트워크 처리량을 달성할 수 있습니다.** </abbr> 

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>IPv6 링크 로컬 개인 네트워크의 자동 인식  
여러 Nic가 있는 개인 (클러스터만) 네트워크를 검색 하는 경우 클러스터는 각 서브넷의 각 NIC에 대 한 IPv6 링크 로컬 (fe80) IP 주소를 자동으로 인식 합니다. 이렇게 하면 더 이상 IPv6 링크 로컬 (fe80) IP 주소 리소스를 수동으로 구성할 필요가 없으므로 관리자 시간을 절약할 수 있습니다.  

둘 이상의 개인 (클러스터 전용) 네트워크를 사용 하는 경우 IPv6 라우팅 구성을 확인 하 여 라우팅이 서브넷을 교차 하도록 구성 되지 않았는지 확인 합니다. 이렇게 하면 네트워크 성능이 저하 됩니다.  

장애 조치(Failover) 클러스터 관리자 UI에서 자동 네트워크 구성의 ![Screencap](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)  
**그림 4: 자동 IPv6 링크 로컬 (fe80) 주소 리소스 구성**  

## <a name="throughput-and-fault-tolerance"></a>처리량 및 내결함성  
Windows Server 2019 및 Windows Server 2016은 NIC 기능을 자동으로 감지 하 고 가능한 가장 빠른 구성에서 각 NIC를 사용 하려고 합니다. 팀으로 구성 된 nic, RSS를 사용 하는 nic 및 RDMA 기능을 사용 하는 Nic를 모두 사용할 수 있습니다. 다음 표에서는 이러한 기술을 사용 하는 경우의 장단점을 요약 합니다. 여러 RDMA 지원 Nic를 사용 하는 경우 최대 처리량이 달성 됩니다. 자세한 내용은 [SMB Mutlichannel의 기본 사항](https://blogs.technet.microsoft.com/josebda/2012/06/28/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0/)을 참조 하세요.

다양 한 NIC 구성의 처리량 및 내결함성에 대 한 그림을 ![](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)  
**그림 5: 다양 한 NIC conifigurations에 대 한 처리량 및 내결함성**   

## <a name="frequently-asked-questions"></a>질문과 대답  
**다중 NIC 네트워크의 모든 Nic가 클러스터 하트 태동에 사용 되나요?**  
    예.  

**클러스터 통신에만 다중 NIC 네트워크를 사용할 수 있나요? 또는 클라이언트와 클러스터 통신에만 사용할 수 있나요?**  
    어떤 구성도 작동 합니다. 모든 클러스터 네트워크 역할은 다중 NIC 네트워크에서 작동 합니다.  

**SMB 다중 채널이 CSV 및 클러스터 트래픽에도 사용 되나요?**  
    예, 기본적으로 모든 클러스터 및 CSV 트래픽은 사용 가능한 다중 NIC 네트워크를 사용 합니다. 관리자는 장애 조치 (Failover) 클러스터링 PowerShell cmdlet 또는 장애 조치(Failover) 클러스터 관리자 UI를 사용 하 여 네트워크 역할을 변경할 수 있습니다.  

**SMB 다중 채널 설정은 어떻게 볼 수 있나요?**  
    **SMBServerConfiguration** cmdlet을 사용 하 여 EnableMultiChannel 속성의 값을 찾습니다.  

**클러스터 공용 속성 PlumbAllCrossSubnetRoutes 멀티 NIC 네트워크에서 적용 되나요?**  
     예.  

## <a name="see-also"></a>참고 항목  
- [Windows Server 장애 조치 (Failover) 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)  
