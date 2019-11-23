---
ms.assetid: 0cd1ac70-532c-416d-9de6-6f920a300a45
title: 장애 조치 (Failover) 클러스터용 클라우드 감시 배포
ms.prod: windows-server
manager: eldenc
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.topic: article
author: JasonGerend
ms.date: 01/18/2019
description: Microsoft Azure를 사용 하 여 클라우드에서 Windows Server 장애 조치 (Failover) 클러스터에 대 한 미러링 모니터 서버를 호스트 하는 방법 즉, 클라우드 감시를 배포 하는 방법을 설명 합니다.
ms.openlocfilehash: 1f38a1a436cfced8637b743817dc1b3d150f7fa6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369884"
---
# <a name="deploy-a-cloud-witness-for-a-failover-cluster"></a>장애 조치(failover) 클러스터용 클라우드 감시 배포

> 적용 대상: Windows Server 2019, Windows Server 2016

클라우드 감시는 Microsoft Azure를 사용 하 여 클러스터 쿼럼에 대 한 응답을 제공 하는 장애 조치 (Failover) 클러스터 쿼럼 감시 유형입니다. 이 항목에서는 클라우드 감시 기능, 지원 되는 시나리오 및 장애 조치 (Failover) 클러스터에 대 한 클라우드 감시를 구성 하는 방법에 대 한 지침을 제공 합니다.

## <a name="CloudWitnessOverview"></a>클라우드 감시 개요

그림 1에서는 Windows Server 2016를 사용 하는 다중 사이트 스트레치 장애 조치 (Failover) 클러스터 쿼럼 구성을 보여 줍니다. 이 예제 구성 (그림 1)에는 2 개의 데이터 센터 (사이트 라고 함)에 2 개의 노드가 있습니다. 클러스터가 2 개 이상의 데이터 센터에 걸쳐 있을 수 있습니다. 또한 각 데이터 센터에는 노드가 2 개 이상 있을 수 있습니다. 이 설정의 일반적인 클러스터 쿼럼 구성 (자동 장애 조치 (failover) SLA)은 각 노드에 투표를 제공 합니다. 데이터 센터 중 하나에서 정전을 경험 하는 경우에도 클러스터를 계속 실행할 수 있도록 쿼럼 감시에 대 한 추가 응답이 제공 됩니다. 수학은 단순 합니다. 5 개의 총 투표를 수행 하 고 클러스터에서 실행을 유지 하는 데 3 개의 투표를 해야 합니다.  

2 개의 다른 사이트(media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_1.png "파일 공유 감시") ![에 2 개의 노드가 있는 세 번째 별도 사이트의 파일 공유 감시]  
**그림 1: 파일 공유 감시를 쿼럼 감시로 사용**  

한 데이터 센터에서 정전이 발생 한 경우 다른 데이터 센터의 클러스터가 계속 실행 되도록 하려면 두 데이터 센터 이외의 위치에 쿼럼 감시를 호스트 하는 것이 좋습니다. 이는 일반적으로 쿼럼 감시 (파일 공유 감시)로 사용 되는 파일 공유를 지 원하는 파일 서버를 호스팅하는 세 번째 별도의 데이터 센터 (사이트)가 필요 함을 의미 합니다.  

대부분의 조직에는 파일 공유 감시를 지 원하는 파일 서버를 호스트 하는 세 번째 별도의 데이터 센터가 없습니다. 이는 조직에서 주로 파일 서버를 두 데이터 센터 중 하나로 호스팅하고,이는 확장으로 인해 해당 데이터 센터가 기본 데이터 센터입니다. 기본 데이터 센터에서 정전이 발생 한 경우 다른 데이터 센터에는 필요한 3 개 응답의 쿼럼 과반수 보다 낮은 2 개의 투표만 있기 때문에 클러스터가 다운 됩니다. 파일 서버를 호스팅하는 세 번째 데이터 센터가 있는 고객의 경우 파일 공유 감시를 지 원하는 항상 사용 가능한 파일 서버를 유지 관리 하는 것이 오버 헤드입니다. 게스트 OS에서 실행 되는 파일 공유 감시에 대 한 파일 서버가 있는 공용 클라우드의 가상 컴퓨터를 호스트 하는 것은 두 설치 & 유지 관리 측면에서 상당한 오버 헤드입니다.  

클라우드 감시는 Microsoft Azure 조정 지점으로 활용 하는 새로운 유형의 장애 조치 (Failover) 클러스터 쿼럼 감시입니다 (그림 2). Azure Blob Storage를 사용 하 여 Blob 파일을 읽고 쓴 다음 분할 된 요소 확인의 경우 중재 지점으로 사용 됩니다.  

이 방법에는 상당한 이점이 있습니다.
1. Microsoft Azure를 활용 합니다 (세 번째 별도의 데이터 센터에 대 한 필요 없음).  
2. 표준 사용 가능한 Azure Blob Storage (공용 클라우드에서 호스트 되는 가상 컴퓨터의 추가 유지 관리 오버 헤드 없음)를 사용 합니다.  
3. 동일한 Azure Storage 계정을 여러 클러스터에 사용할 수 있습니다 (클러스터당 하나의 blob 파일, blob 파일 이름으로 사용 되는 클러스터 고유 id).  
4. 저장소 계정에 대 한 매우 낮은 $cost (blob 파일당 매우 작은 데이터는 클러스터 노드의 상태가 변경 될 때 한 번만 업데이트 됨).  
5. 기본 제공 클라우드 감시 리소스 유형입니다.  

쿼럼 감시로 클라우드 감시를 사용 하는 다중 사이트 확장 클러스터를 보여 주는 ![다이어그램](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_2.png)  
**그림 2: 쿼럼 감시로 클라우드 감시를 사용 하는 다중 사이트 확장 클러스터**  

그림 2에 표시 된 것 처럼 별도의 세 번째 사이트가 필요 하지 않습니다. 다른 쿼럼 감시와 마찬가지로 클라우드 감시는 응답을 가져오고 쿼럼 계산에 참여할 수 있습니다.  

## <a name="CloudWitnessSupportedScenarios"></a>클라우드 감시: 단일 미러링 모니터 서버 유형에 대해 지원 되는 시나리오
장애 조치 (Failover) 클러스터 배포에서 모든 노드가 인터넷에 연결할 수 있는 경우 (Azure 확장을 통해), 쿼럼 감시 리소스로 클라우드 감시를 구성 하는 것이 좋습니다.  

쿼럼 감시로 클라우드 감시를 사용 하도록 지원 되는 몇 가지 시나리오는 다음과 같습니다.  
- 재해 복구는 다중 사이트 클러스터를 확대 합니다 (그림 2 참조).  
- 공유 저장소가 없는 장애 조치 (Failover) 클러스터 (SQL Always On 등).  
- 장애 조치 (Failover) 클러스터는 Microsoft Azure 가상 컴퓨터 역할 또는 다른 공용 클라우드에서 호스트 되는 게스트 OS 내에서 실행 됩니다.  
- 사설 클라우드에서 호스트 되는 Virtual Machines의 게스트 OS 내에서 실행 되는 장애 조치 (Failover) 클러스터
- 스케일 아웃 파일 서버 클러스터와 같은 공유 저장소를 포함 하거나 포함 하지 않는 저장소 클러스터  
- 소규모 지점-office 클러스터 (2 개 노드 클러스터도)  

Windows Server 2012 R2부터 클러스터가 감시 응답을 자동으로 관리 하 고 노드가 동적 쿼럼에 투표 하므로 항상 미러링 모니터 서버를 구성 하는 것이 좋습니다.  

## <a name="CloudWitnessSetUp"></a>클러스터에 대 한 클라우드 감시 설정
클러스터에 대 한 쿼럼 감시로 클라우드 감시를 설정 하려면 다음 단계를 완료 합니다.
1. 클라우드 감시로 사용할 Azure Storage 계정 만들기
2. 클러스터에 대 한 쿼럼 감시로 클라우드 감시를 구성 합니다.

## <a name="create-an-azure-storage-account-to-use-as-a-cloud-witness"></a>클라우드 감시로 사용할 Azure Storage 계정 만들기

이 섹션에서는 저장소 계정을 만들고 해당 계정에 대 한 끝점 Url 및 액세스 키를 보고 복사 하는 방법을 설명 합니다.

클라우드 감시를 구성 하려면 blob 파일 (중재에 사용 됨)을 저장 하는 데 사용할 수 있는 유효한 Azure Storage 계정이 있어야 합니다. 클라우드 감시는 Microsoft 저장소 계정에서 잘 알려진 컨테이너 **msft-클라우드 감시** 를 만듭니다. 클라우드 감시는 해당 클러스터의 고유한 ID를 사용 하 여 단일 blob 파일을이 **msft-cloud-미러링 모니터** 컨테이너에 있는 blob 파일의 파일 이름으로 사용 합니다. 즉, 동일한 Microsoft Azure Storage 계정을 사용 하 여 여러 다른 클러스터에 대 한 클라우드 감시를 구성할 수 있습니다.

서로 다른 여러 클러스터에 대해 클라우드 감시를 구성 하는 데 동일한 Azure Storage 계정을 사용 하는 경우 단일 **msft 클라우드-미러링 모니터** 컨테이너가 자동으로 만들어집니다. 이 컨테이너는 클러스터당 blob 파일 하나를 포함 합니다.

### <a name="to-create-an-azure-storage-account"></a>Azure 저장소 계정을 만들려면

1. [Azure Portal](http://portal.azure.com)에 로그인 합니다.
2. 허브 메뉴에서 새로 만들기-> 데이터 + 저장소-> 저장소 계정을 선택 합니다.
3. 저장소 계정 만들기 페이지에서 다음을 수행 합니다.
    1. 저장소 계정의 이름을 입력 합니다.
    <br>Storage 계정 이름은 3자에서 24자 사이여야 하고 숫자 및 소문자만 포함할 수 있습니다. 저장소 계정 이름은 Azure 내에서 고유 해야 합니다.
        
    2. **계정 종류**에 대해 **범용**을 선택 합니다.
    <br>클라우드 감시에는 Blob storage 계정을 사용할 수 없습니다.
    3. **성능**으로 **표준**을 선택 합니다.
    <br>클라우드 감시에는 Azure Premium Storage를 사용할 수 없습니다.
    2. **복제**에 대해 **LRS (로컬 중복 저장소)** 를 선택 합니다.
    <br>장애 조치 (Failover) 클러스터링은 데이터를 읽을 때 일관성을 보장 해야 하는 조정 지점으로 blob 파일을 사용 합니다. 따라서 **복제** 유형의 경우 **로컬 중복 저장소** 를 선택 해야 합니다.

### <a name="view-and-copy-storage-access-keys-for-your-azure-storage-account"></a>Azure Storage 계정에 대 한 저장소 액세스 키 보기 및 복사

Microsoft Azure Storage 계정을 만들면 자동으로 생성 된 두 개의 액세스 키 (기본 액세스 키 및 보조 액세스 키)와 연결 됩니다. 클라우드 감시를 처음 만들 때 **기본 액세스 키**를 사용 합니다. 클라우드 감시에 사용할 키에 대 한 제한은 없습니다.  

#### <a name="to-view-and-copy-storage-access-keys"></a>저장소 액세스 키를 보고 복사 하려면

Azure Portal에서 저장소 계정으로 이동 하 고 **모든 설정** 을 클릭 한 다음 **액세스 키** 를 클릭 하 여 계정 액세스 키를 보고, 복사 하 고, 다시 생성 합니다. 액세스 키 블레이드에는 응용 프로그램에서 사용 하기 위해 복사할 수 있는 기본 키 및 보조 키를 사용 하 여 미리 구성 된 연결 문자열도 포함 되어 있습니다 (그림 4 참조).

Microsoft Azure의 액세스 키 관리 대화 ![스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_4.png)  
**그림 4: 저장소 액세스 키**

### <a name="view-and-copy-endpoint-url-links"></a>끝점 URL 링크 보기 및 복사  
저장소 계정을 만들 때 다음 Url은 형식을 사용 하 여 생성 됩니다. `https://<Storage Account Name>.<Storage Type>.<Endpoint>`  

클라우드 감시는 항상 **Blob** 을 저장소 유형으로 사용 합니다. Azure는 core.windows.net을 끝점으로 사용 **합니다.** 클라우드 감시를 구성 하는 경우 시나리오에 따라 다른 끝점을 사용 하 여 구성할 수 있습니다. 예를 들어 중국의 Microsoft Azure 데이터 센터에는 다른 끝점이 있습니다.  

> [!NOTE]  
> 끝점 URL은 클라우드 감시 리소스에 의해 자동으로 생성 되며 URL에 필요한 구성의 추가 단계가 없습니다.  

#### <a name="to-view-and-copy-endpoint-url-links"></a>끝점 URL 링크를 보고 복사 하려면
Azure Portal에서 저장소 계정으로 이동 하 고 **모든 설정** 을 클릭 한 다음 **속성** 을 클릭 하 여 끝점 url을 보고 복사 합니다 (그림 5 참조).  

클라우드 감시 끝점 링크의 ![스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_5.png)  
**그림 5: 클라우드 감시 끝점 URL 링크**

Azure Storage 계정을 만들고 관리 하는 방법에 대 한 자세한 내용은 [Azure Storage 계정 정보](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/) 를 참조 하세요.

## <a name="configure-cloud-witness-as-a-quorum-witness-for-your-cluster"></a>클라우드 감시를 클러스터에 대 한 쿼럼 감시로 구성
클라우드 감시 구성은 장애 조치(Failover) 클러스터 관리자에 기본 제공 되는 기존 쿼럼 구성 마법사 내에서 잘 통합 됩니다.  

### <a name="to-configure-cloud-witness-as-a-quorum-witness"></a>쿼럼 감시로 클라우드 감시를 구성 하려면
1. 장애 조치(Failover) 클러스터 관리자를 시작 합니다.
2. 클러스터 > **추가 작업** 을 마우스 오른쪽 단추로 클릭 하 -> **클러스터 쿼럼 설정 구성** (그림 6 참조). 그러면 클러스터 쿼럼 구성 마법사가 시작 됩니다.  
    장애 조치(Failover) 클러스터 관리자 UI](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_7.png) 그림 6의 Configue 클러스터 쿼럼 설정에 대 한 메뉴 경로의 스냅숏 ![**합니다. 클러스터 쿼럼 설정**

3. **쿼럼 구성 선택** 페이지에서 **쿼럼 감시 선택** 을 선택 합니다 (그림 7 참조).  

    클러스터 쿼럼 마법사의 ' quotrum 미러링 모니터 서버 선택 ' 라디오 단추 ![스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_8.png)  
    **그림 7. 쿼럼 구성 선택**

4. **쿼럼 감시 선택** 페이지에서 **클라우드 감시 구성** 을 선택 합니다 (그림 8 참조).  

    해당 라디오 단추의 스냅숏을 ![하 여 클라우드 감시를 선택](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_9.png)  
    **그림 8. 쿼럼 감시를 선택 합니다.**  

5. **클라우드 감시 구성** 페이지에서 다음 정보를 입력 합니다.  
   1. (필수 매개 변수) 계정 이름 Azure Storage 합니다.  
   2. (필수 매개 변수) 저장소 계정에 해당 하는 액세스 키입니다.  
       1. 처음 만들 때 기본 액세스 키를 사용 합니다 (그림 5 참조).  
       2. 기본 액세스 키를 회전 하는 경우 보조 액세스 키를 사용 합니다 (그림 5 참조).  
   3. (선택적 매개 변수) 다른 Azure 서비스 끝점 (예: 중국의 Microsoft Azure 서비스)을 사용 하려는 경우 끝점 서버 이름을 업데이트 합니다.  

      클러스터 쿼럼 마법사에서 클라우드 감시 구성 창의 스냅숏을 ![](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_10.png)  
      **그림 9: 클라우드 감시 구성**

6. 클라우드 미러링 모니터 서버가 성공적으로 구성 되 면 장애 조치(Failover) 클러스터 관리자 스냅인에서 새로 만든 감시 리소스를 볼 수 있습니다 (그림 10 참조).

    클라우드 감시](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_11.png) 성공적으로 구성 ![  
    **그림 10: 클라우드 미러링 모니터 서버 구성 성공**

### <a name="configuring-cloud-witness-using-powershell"></a>PowerShell을 사용 하 여 클라우드 감시 구성  
기존 집합-ClusterQuorum PowerShell 명령에는 클라우드 감시에 해당 하는 새로운 추가 매개 변수가 있습니다.  

다음 PowerShell 명령을 [`Set-ClusterQuorum`](https://technet.microsoft.com/library/ee461013.aspx) 사용 하 여 클라우드 감시를 구성할 수 있습니다.  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey>
```

다른 끝점을 사용 해야 하는 경우 (드문 경우):  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> -Endpoint <servername>  
```

### <a name="azure-storage-account-considerations-with-cloud-witness"></a>클라우드 감시를 사용 하 여 계정 고려 사항 Azure Storage  
장애 조치 (Failover) 클러스터에 대 한 쿼럼 감시로 클라우드 감시를 구성 하는 경우 다음 사항을 고려 하세요.
* 액세스 키를 저장 하는 대신 장애 조치 (Failover) 클러스터에서 SAS (공유 액세스 보안) 토큰을 생성 하 고 안전 하 게 저장 합니다.  
* 생성 된 SAS 토큰은 액세스 키가 유효한 상태로 유지 되는 동안 유효 합니다. 기본 액세스 키를 회전할 때 기본 액세스 키를 다시 생성 하기 전에 먼저 해당 저장소 계정을 사용 하는 모든 클러스터의 클라우드 감시를 보조 액세스 키로 업데이트 해야 합니다.  
* 클라우드 감시는 Azure Storage 계정 서비스의 HTTPS REST 인터페이스를 사용 합니다. 즉, 모든 클러스터 노드에서 HTTPS 포트를 열어야 합니다.

### <a name="proxy-considerations-with-cloud-witness"></a>클라우드 감시에 대 한 프록시 고려 사항  
클라우드 감시는 HTTPS (기본 포트 443)를 사용 하 여 Azure blob service와의 통신을 설정 합니다. 네트워크 프록시를 통해 HTTPS 포트에 액세스할 수 있는지 확인 하십시오.

## <a name="see-also"></a>참고 항목
- [Windows Server 장애 조치 (Failover) 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)
