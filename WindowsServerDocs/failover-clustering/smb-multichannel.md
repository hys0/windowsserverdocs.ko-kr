---
ms.assetid: a6343f1c-e9dd-4a02-91ad-39bd519d66cd
title: "간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크"
ms.prod: windows-server-threshold
ms.technology: storage-failover-clustering
ms.topic: article
author: RobHindman
ms.author: robhind
ms.date: 09/15/2016
ms.openlocfilehash: 45d8364adf9d3db24a8e6d8f7bc91178ce7d1551
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="simplified-smb-multichannel-and-multi-nic-cluster-networks"></a>간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크

> 에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016

다중 SMB 채널 및 다중-간체<abbr title="네트워크 인터페이스 카드">NIC</abbr> 클러스터 네트워크는 여러 Nic 같은 클러스터 네트워크 서브넷에 사용할 수 있는 자동으로 SMB 다중 채널을 통해 Windows Server 2016의에서 새로운 기능입니다.  

간소화 된 SMB 다중 채널 및 다중 NIC 클러스터 네트워크는 다음과 같은 이점을 제공 합니다.  
- 모든 Nic 노드의 동일한 스위치를 사용 하는 자동으로 인식 클러스터링 / 같은 서브넷-추가 구성 없이 합니다.  
- 다중 SMB 채널 자동으로 활성화 됩니다.  
- IP 주소 IPv6 링크 지역 (f e 80) 리소스 하기만 하는 네트워크에는 클러스터 전용 () 사설망에서 인식 합니다.  
- 단일 IP 주소 리소스 각 클러스터 액세스 지점을 (뚜껑) 네트워크 이름 (NN)에서 기본적으로 구성 됩니다.  
- 클러스터 유효성 검사는 더 이상 여러 Nic 같은 서브넷에서 발견 된 경우 경고 메시지를 발행 합니다.  

## <a name="requirements"></a>요구 사항  
-   동일한 스위치를 사용 하 여 서버에 따라 여러 Nic / 서브넷 합니다.  

## <a name="how-to-take-advantage-of-multi-nic-clusters-networks-and-simplified-smb-multichannel"></a>다중 NIC를 활용 하는 방법에 네트워크와 간단한 SMB 다중 채널 클러스터  
Windows Server 2016의 새로운 다중 NIC 클러스터 네트워크 및 간단한 SMB 다중 채널 기능을 활용 하는 방법을 설명 합니다.  

### <a name="use-at-least-two-networks-for-failover-clustering"></a>장애 조치 두 개 이상의 네트워크를 사용 하 여   
드뭅니다 있지만 네트워크 스위치가 실패할 수 있는-장애 조치 두 개 이상의 네트워크를 사용 하 여 여전히 가장 좋은 방법은입니다. 클러스터 하트에 있는 모든 네트워크 사용 됩니다. 오류 단일 지점 되지 않도록 장애 클러스터에 대 한 네트워크를 사용 하지 마세요. 이 가장 좋습니다 있어야 여러 실제 통신 경로 클러스터의 노드와 오류 단일 지점 간에 합니다.  

![두 개의 네트워크가 장애 조치 그림](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig1.png)  
**장애 조치 두 개 이상의 네트워크를 사용 하는 그림 1:**  

### <a name="use-multiple-nics-across-clusters"></a>여러 Nic 클러스터에서 사용 하 여  

여러 Nic 클러스터-저장소 및 저장소 작업 클러스터에서 사용 되는 경우 극대화 간단한 SMB 다중 채널 이루어집니다. 이 작업 클러스터 (Hyper-v 장애 조치 클러스터 SQL Server 인스턴스, 저장소 복제,) SMB 다중 채널 및 결과 사용 하 여에서 네트워크를 보다 효율적으로 사용할 수 있게 합니다. 확장 파일 서버 클러스터 장애 조치 클러스터 SQL Server 인스턴스 또는 Hyper-v 클러스터에 대 한 작업 데이터를 저장 하는 데 사용 되는 위치 (세분화 라고도 함) 클러스터 집약 구성에서는이 네트워크를 라고도 "북쪽 사우스 서브넷" / 네트워크입니다. 대부분의 고객 지원 NIC 카드 RDMA 및 전환에 투자 하 여 처리량이이 네트워크의을 최대화 합니다.  

![북쪽 사우스 SMB 서브넷 그림](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig2.png)  
**그림 2: 최대 네트워크 처리량을 위해 사용 하 여 여러 Nic 확장 파일 서버 클러스터 및 북쪽 사우스 서브넷 공유 하는 Hyper-v 또는 장애 조치 클러스터 SQL Server 인스턴스 클러스터-**  

![두 개의 클러스터 같은 서브넷에 여러 Nic를 사용 하 여 SMB 다중 채널을 활용 하는 Screencap](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig3.png)  
**그림 3: 2 클러스터 (저장소, SQL Server에 대 한 확장 파일 서버 <abbr title="장애 클러스터링 인스턴스">FCI</abbr> 작업에 대 한) SMB 다중 채널을 활용 하 고 네트워크 처리량 더 나은 결과 얻을를 여러 Nic 같은 서브넷에 사용 하 여 둘 다.** 

## <a name="automatic-recognition-of-ipv6-link-local-private-networks"></a>자동으로 IPv6 링크 로컬 사설망 인식  
여러 Nic 사용 하 여 개인 (클러스터에만 해당) 네트워크 감지 되 면 클러스터는 자동으로 인식 IPv6 링크 지역 (f e 80) IP 주소 각 NIC에 대 한 각 서브넷 합니다. 더 이상 수동으로 IPv6 링크 로컬 (f e 80) IP 주소 리소스를 구성 하는이 절약 관리자 시간  

(클러스터에만 해당) 개인 하나 이상의 네트워크를 사용할 때 IPv6 라우팅 구성을 사용 하 여 경로 구성 되어 있는지 확인 되지 네트워크 성능이 저하 됩니다이 이후 서브넷을 확인 하세요.  

![클러스터 장애 조치 관리자 UI에서 구성 자동 네트워크의 Screencap](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig4.png)  
**자동으로 IPv6 링크 지역 (f e 80) 주소 리소스 구성 그림 4:**  

## <a name="throughput-and-fault-tolerance"></a>처리량 및 결함 허용  
Windows Server 2016를 자동으로 검색 NIC 기능 가능한 한 빠른 구성에서 각 NIC 사용 하려고 합니다. 협력는 Nic, Nic RSS, 사용 및 RDMA 기능이 있는 Nic를 모두 사용할 수 있습니다. 아래 표에서 이러한 기술을 사용 하는 경우 장단점 요약 되어 있습니다. 여러 RDMA 가능 Nic를 사용 하는 경우 최대 처리량이 이루어집니다. 자세한 내용은 참조 [SMB Mutlichannel 조정 기본 사항](https://blogs.technet.microsoft.com/josebda/2012/06/28/the-basics-of-smb-multichannel-a-feature-of-windows-server-2012-and-smb-3-0/)합니다.

![NIC 다양 한 구성에서 허용 하 처리량 및 오류는 그림](media/Simplified-SMB-Multichannel-and-Multi-NIC-Cluster-Networks/Clustering_MulitNIC_Fig5.png)  
**다양 한 NIC conifigurations 그림 5: 처리량 및 오류 허용**   

## <a name="frequently-asked-questions"></a>자주 묻는 질문  
**클러스터 심 맞에 사용 되는 다중 NIC 네트워크의 모든 Nic?**  
    예입니다.  

**다중 NIC 네트워크를 사용할 수만 클러스터 통신을 위해? 또는 에서만 사용할 수는 클라이언트와 클러스터 통신을 위해?**  
    중 하나 구성 작동 하는지-모든 클러스터 네트워크 역할은 다중 NIC 네트워크에서 작동 합니다.  

**SMB 다중 채널에도 사용 가장 교통?**  
    예 기본적으로 모든 클러스터 및 하겠습니다는 사용 하 여 사용 가능한 다중 NIC 네트워크 합니다. 관리자는 네트워크 역할을 변경 하려면 장애 클러스터링 PowerShell cmdlet 또는 장애 클러스터 관리자 UI 사용할 수 있습니다.  

**SMB 다중 채널 설정 확인 하려면 어떻게 하나요?**  
    사용 하 여는 **Get SMBServerConfiguration** cmdlet EnableMultiChannel 속성 가치에 대 한 확인 합니다.  

**다중 NIC 네트워크 PlumbAllCrossSubnetRoutes 준수 클러스터 일반적인 속성 인가요?**  
     예입니다.  

## <a name="see-also"></a>참조 하십시오  
- [Windows Server에서 장애 조치 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)  
