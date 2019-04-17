---
ms.assetid: 0cd1ac70-532c-416d-9de6-6f920a300a45
title: "클러스터 장애 조치 클라우드 감시 배포"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.topic: article
author: JasonGerend
ms.date: 10/2/2017
description: "Microsoft Azure 클라우드-Windows Server 장애 클러스터에 대 한 감시 개최 된를 사용 하는 방법을 클라우드 감시 배포 하는 방법을 즉 합니다."
ms.openlocfilehash: 564c6668fcc80a8bd1531c05c142996689de8154
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2017
---
# <a name="deploy-a-cloud-witness-for-a-failover-cluster"></a>클러스터 장애 조치 클라우드 감시 배포

> 적용:에 해당: (세미콜론 연간 채널) Windows Server, Windows Server 2016

클라우드 감시는 새로운 유형의 Windows Server 2016에 도입 되는 클러스터 장애 조치 쿼럼 감시 합니다. 이 항목에서는 개요 클라우드 감시 기능를 지 원하는 경우 및 Windows Server 2016 실행 되는 클러스터 장애 조치 클라우드 감시 구성 하는 방법에 대 한 지침을 제공 합니다.

## <a name="CloudWitnessOverview"></a>클라우드 감시 개요

그림 1 되는 여러 사이트 늘어난된 클러스터 장애 조치 쿼럼 구성을 Windows Server 2016을 보여 줍니다. (그림 참조 1)이 예 구성에서 2 데이터 센터 (사이트 라고도 함)에 2 노드 있습니다. Note을 2 개 이상의 데이터 센터에 걸쳐 클러스터에 대 한 것 같습니다. 또한 각 datacenter 2 개 이상의 노드 가질 수 있습니다. 이 설정 (자동 장애 SLA) 일반적인 클러스터 쿼럼 구성 각 노드 투표를 제공합니다. 정전이 발생 한 투표를 추가 하는 데이터 센터 중 하나를 실행 중 경우에 계속 클러스터 수 있도록 쿼럼 감시에 게 제공 됩니다. 수학은 매우 간단-총 투표 5 가지 하 고 유지 해 서 실행 하 고 클러스터에 대 한 투표 3 해야 합니다.  

![세 번째 별도의 파일 공유 감시 다른 사이트 2에서 2 노드와 사이트](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_1.png "파일 공유 감시")  
**그림 1: 파일 공유 감시 쿼럼 감시도 사용 하 여**  

한 datacenter 정전이 발생 하는 경우 클러스터를 실행 하는 상태를 유지 하도록 다른 데이터 센터에 대 한 등호 기회를 제공 것이 좋습니다 호스팅할 두 개의 데이터 센터 다른 위치에 쿼럼 감시 합니다. 이 일반적으로 제 3 필요한 의미 분리 데이터 센터 (사이트)를 개최 된 파일 서버를 백업 쿼럼 감시 (공유 감시 파일)로 사용 되는 파일 공유 하는 합니다.  

대부분의 조직 파일 공유 감시 백업 하는 파일 서버 호스팅할 datacenter 별도 제 필요가 없습니다. 조직 주로 개최 된 하나를 확장 하 여 해당 데이터 센터의 주요 데이터 센터 두 개의 데이터 센터에 파일 서버 의미 합니다. 시나리오에서의 주요 데이터 센터에 정전 여기서 클러스터 다른 데이터 센터에는 필요한 3 투표 쿼럼 대부분 아래에 있는 2 투표도 이동 것입니다. 세 번째 센터 개최 된 파일 서버에 있는 고객을 백업에서 파일 공유 감시 가용성 파일 서버 유지 하기 위해 오버입니다. 게스트 OS에서 실행 되는 파일 공유 감시에 대 한 파일 서버 있는 공개 클라우드에서 가상 컴퓨터 호스트 부담 설정 및 유지 관리입니다.  

클라우드 감시 클러스터 장애 조치 쿼럼 감시 Microsoft Azure (그림 참조 2) 중재 지점으로 활용 하는 새로운 유형의입니다. Azure Blob Storage 읽기/쓰기 다음 split-brain 해상도 발생 하는 경우 중재 지점으로 사용 되는 물방울 파일을 사용 합니다.  

중요 한 가지이 방법을 사용 하는 혜택:
1. Microsoft Azure (세 번째 별도 데이터 센터에 대 한 필요성 없음)를 활용합니다.  
2. 표준 사용할 수 있는 Azure Blob Storage (가상 컴퓨터를 호스팅할 공개 클라우드에서 추가 유지 관리 오버 없음)를 사용 합니다.  
3. Azure Storage 것과 동일한 계정 여러 클러스터 (클러스터로 파일을 하나의 물방울, 물방울 파일 이름으로 사용 되는 클러스터 고유 id)에 사용할 수 있습니다.  
4. 저장소 계정 (매우 적은 데이터 클러스터 노드에서 상태를 변경할 때 한 번만 물방울 파일이 업데이트 기록 물방울 파일당)에 매우 낮은 지속적인 $cost 합니다.  
5. 기본 제공 클라우드 감시 리소스 형식 있습니다.  

![멀티 사이트 늘어난된 클러스터 클라우드 감시 쿼럼 감시도와 보여 주는 다이어그램](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_2.png)  
**그림 2: 다중 사이트 클라우드 감시 클러스터로 쿼럼 감시 연장**  

그림 2와 같이는 필요한 세 번째 별도 사이트로 없습니다. 투표를 가져오고 쿼럼 계산에 참여할 수 있는 다른 쿼럼 감시 같은 클라우드 감시 합니다.  

## <a name="CloudWitnessSupportedScenarios"></a>클라우드 감시: 시나리오 단일 감시 형식에 대 한 지원
클러스터 장애 조치 배포 모든 노드 (Azure 확장) 하 여 인터넷에 연결할 수 있는으로 있으면 클라우드 감시 쿼럼 감시 리소스를 구성 하는 것이 좋습니다.  

지원 되는 시나리오 중 일부를 사용 하 여 클라우드 감시의 쿼럼 감시는 다음과 같이 다음과 같습니다.  
- 복구 (2 그림 참조) 하는 여러 사이트 클러스터 늘어납니다.  
- 공유 (SQL 항상에 등)를 저장 하지 않고 클러스터 장애 조치입니다.  
- 내 Microsoft Azure 가상 컴퓨터 역할 (또는 기타 공공 클라우드)에서 호스트 되는 게스트 OS에서 실행 중인 장애 조치 클러스터 합니다.  
- 장애 조치 클러스터 내 게스트 OS의 가상 컴퓨터를 호스팅할 개인 클라우드에서 실행 합니다.
- 저장 하거나 사용 하지 않고 공유 저장소 클러스터링 확장 파일 서버 클러스터 같은 합니다.  
- 작은 지점 클러스터 (2-노드도 클러스터)  

Windows Server 2012 r 2와 시작 것이 좋습니다 클러스터 자동 감시 투표를 관리 하 고 동적 쿼럼 노드 투표 미러링 항상 구성할 수 있습니다.  

## <a name="CloudWitnessSetUp"></a>클러스터 클라우드 감시 설정
클라우드 감시 클러스터에 대 한 쿼럼 감시도를 설정 하려면 다음 단계를 완료 합니다.
1. 클라우드 감시도 사용 하 여 Azure Storage 계정 만들기
2. 클러스터에 대 한 쿼럼 감시 클라우드 감시 구성 합니다.

## <a name="create-an-azure-storage-account-to-use-as-a-cloud-witness"></a>클라우드 감시도 사용 하 여 Azure Storage 계정 만들기

이 저장소 계정 및 보기 및 복사 끝점 Url 만들고 키 해당 계정에 대 한 액세스 하는 방법을 설명 합니다.

클라우드 감시도 구성 하려면 (조정을 사용) 물방울 파일을 저장 하는 데 사용할 수 있는 유효한 Azure Storage 계정이 있어야 합니다. 클라우드 감시 만들어 유명 컨테이너 **msft-클라우드-감시** 저장소 Microsoft 계정에서 합니다. 해당 파일을 하나의 물방울 클러스터 클라우드 감시 쓰기 파일 이름 아래에서이 물방울 파일의으로 사용 되는 고유 ID가 **msft-클라우드-감시** 컨테이너 합니다. 여러 가지 클러스터 클라우드 감시 구성 하려면 같은 Microsoft Azure Storage 계정을 사용할 수 있는 것을 의미 합니다.

다른 여러 클라우드 감시 구성에 대 한 같은 Azure Storage 계정을 사용 하는 경우 클러스터, 단일 **msft-클라우드-감시** 컨테이너 자동으로 작성 합니다. 이 컨테이너 클러스터로 물방울 한 파일을 포함 됩니다.

### <a name="to-create-an-azure-storage-account"></a>그러면 계정 만들기

1. 에 로그인 하 여 [Azure Portal](http://portal.azure.com)합니다.
2. 허브 메뉴의 새로운-> 데이터 선택 + 스토리지 스토리지 계정->.
3. 만들기 저장소 계정 페이지에서에서 다음을 수행 합니다.
    1. 저장소 계정에 대해 이름을 입력 합니다.
    <br>저장소 계정 이름 3와 24 자 사이 여야 합니다 및 숫자 및 소문자로 포함 될 수 있습니다. 저장소 계정 이름을 Azure 내 고유 해야 합니다.
        
    2. 에 대 한 **친절 계정**선택 **범용**합니다.
    <br>클라우드 감시 물방울 저장소 계정을 사용할 수 없습니다.
    3. 에 대 한 **성능**선택 **표준**합니다.
    <br>클라우드 감시 Azure 프리미엄 저장소를 사용할 수 없습니다.
    2. 에 대 한 **복제**선택 **로컬로 중복 저장소 (LRS)** 합니다.
    <br>클러스터링 데이터를 읽을 때 일부 일관성 보장 필요한 중재 지점으로 물방울 파일을 사용 합니다. Therefor 선택 해야 **중복 로컬로 저장** 에 대 한 **복제** 형식 있습니다.

### <a name="view-and-copy-storage-access-keys-for-your-azure-storage-account"></a>보기 및 Azure Storage 계정에 대해 선택 키 저장소 복사

Microsoft Azure Storage 계정을 만들 때 두 가지 선택 키를 자동으로 생성-기본 선택 키와 보조 키와 관련이 있습니다. 클라우드 감시 처음으로 만들기 위해 사용 하는 **기본 선택 키**합니다. 클라우드 감시에 사용 하는 키에 대 한 제한 되지 않습니다.  

#### <a name="to-view-and-copy-storage-access-keys"></a>보고 저장소 선택 키에 복사

Azure Portal 저장소 계정으로 이동, 클릭 **모든 설정** 차례로 클릭 하 고 **선택 키** 보고, 복사 및 계정을 선택 키를 다시 생성 합니다. 또한 선택 키 잎 (4 그림 참조) 하 여 응용 프로그램에서 사용 하 여 복사할 수 있는 기본 및 보조 키를 사용 하 여 연결 미리 구성 된 문자열 포함 됩니다.

![Microsoft Azure에 대 한 액세스 키 관리 대화 상자의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_4.png)  
**저장소 선택 키 그림 4:**

### <a name="view-and-copy-endpoint-url-links"></a>보기 및 endpoint URL 링크 복사  
저장소 계정을 만들 때 다음 Url 형식을 사용 하 여 생성 됩니다. `https://<Storage Account Name>.<Storage Type>.<Endpoint>`  

클라우드 감시 사용 하 여 항상 **물방울** 저장소 유형입니다. Azure 사용 하 여 **. core.windows.net** 끝점으로 합니다. 클라우드 감시를 구성할 때 불가능 구성 하는 여러 끝점으로 (예를 들어 중국에서 Microsoft Azure 데이터 센터에는 여러 끝점) 시나리오를 기준으로 합니다.  

> [!NOTE]  
> 끝점 URL 클라우드 감시 리소스 자동으로 생성 됩니다 하 고 필요한 URL에 대 한 구성의 없이 추가 단계입니다.  

#### <a name="to-view-and-copy-endpoint-url-links"></a>보고 끝점 URL 링크 복사
Azure Portal 저장소 계정으로 이동, 클릭 **모든 설정** 차례로 클릭 하 고 **속성** 보고를 복사 끝점 Url (5 그림 참조).  

![클라우드 감시 끝점 링크의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_5.png)  
**그림 5: 클라우드 감시 끝점 URL 링크**

Azure Storage 계정을 만들고 관리에 대 한 자세한 내용은 참조 [Azure Storage 계정에 대 한](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/)

## <a name="configure-cloud-witness-as-a-quorum-witness-for-your-cluster"></a>클러스터에 대 한 쿼럼 감시 클라우드 감시 구성
클라우드 감시 구성이 장애 조치 클러스터 관리자에 기본 제공 기존 쿼럼 구성 마법사 잘 통합 되었습니다.  

### <a name="to-configure-cloud-witness-as-a-quorum-witness"></a>클라우드 감시 쿼럼 감시 구성 하려면
1. 클러스터 장애 조치 관리자를 시작 합니다.
2. 마우스 오른쪽 단추로 클릭 클러스터- **더 많은 기능의** -> **클러스터 쿼럼 설정 구성** (6 그림 참조). 구성 클러스터 쿼럼 마법사를 시작 합니다.  
    ![클러스터 장애 조치 관리자 UI에서 Configue 클러스터 쿼럼 설정 메뉴 경로의 스냅숏을](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_7.png)**그림 6 합니다. 클러스터 쿼럼 설정**

3. 에 **쿼럼 구성 선택** 페이지 선택, **쿼럼 감시 선택** (7 그림 참조).  

    !['선택 quotrum 감시' 스냅샷을 라디오 단추 클러스터 쿼럼 마법사에서](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_8.png)  
    **그림 7 합니다. 쿼럼 구성을 선택합니다**

4. 에 **쿼럼 감시 선택** 페이지 선택, **클라우드 감시 구성** (8 그림 참조).  

    ![클라우드 감시 선택 적절 한 라디오 단추의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_9.png)  
    **그림 8 합니다. 쿼럼 감시 선택**  

5. 에 **클라우드 감시 구성** 페이지에서 다음 정보를 입력 합니다.  
    1. (필수 매개) Azure Storage 계정 이름입니다.  
    2. (필수 매개) 해당 하는 저장소 계정을 선택 키입니다.  
        1. 처음으로 만들 때 사용 하 여 기본 선택 키 (5 그림 참조)  
        2. 보조 키를 사용 하 여 기본 선택 키, 회전 하는 경우 (5 그림 참조)  
    3. (선택 사항 매개 변수) Azure 서비스 여러 끝점 (예: 중국에서 Microsoft Azure 서비스)를 사용 하려는 경우 끝점 서버 이름을 업데이트 합니다.  

    ![클러스터 쿼럼 마법사에서 클라우드 감시 구성 창의 스냅숏](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_10.png)  
    **구성 클라우드 감시 그림 9:**

6. 클라우드 감시, 성공한 구성에 있습니다 새로 만든된 감시 리소스 관리자에서 볼 수 있는 장애 클러스터 스냅인 (10 그림 참조).

    ![성공적으로 클라우드 감시 구성](media/Deploy-a-Cloud-Witness-for-a-Failover-Cluster/CloudWitness_11.png)  
    **클라우드 감시 성공한 구성 그림 10:**

### <a name="configuring-cloud-witness-using-powershell"></a>PowerShell을 사용 하 여 클라우드 감시 구성  
기존 Set-ClusterQuorum PowerShell 명령에 해당 클라우드 감시 하는 새로운 추가 매개 합니다.  

사용 하 여 클라우드 감시 구성할 수는 [`Set-ClusterQuorum`](https://technet.microsoft.com/library/ee461013.aspx)다음 명령을 PowerShell:  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey>
```

경우에 여러 끝점 (드문)을 사용 해야 합니다.  

```PowerShell
Set-ClusterQuorum -CloudWitness -AccountName <StorageAccountName> -AccessKey <StorageAccountAccessKey> -Endpoint <servername>  
```

### <a name="azure-storage-account-considerations-with-cloud-witness"></a>Azure Storage 계정 부담 클라우드 미러링  
클라우드 감시 장애 클러스터에 대 한 쿼럼 감시를 구성할 때 다음을 고려 합니다.
* 선택 키를 저장 하는 대신 클러스터 장애 조치 생성 하 고는 공유 액세스 보안 SAS () 토큰 안전 하 게 저장 됩니다.  
* 생성된 SAS 토큰 선택 키 남아 유효한 유효 합니다. 기본 선택 키, 회전 하는 경우에 먼저 기본 선택 키를 다시 생성 하기 전에 보조 키 (저장소 해당 계정을 사용 하는 모든 클러스터)에서 클라우드 감시를 업데이트 해야 합니다.  
* 클라우드 감시 HTTPS 나머지 인터페이스 Azure Storage 계정 서비스를 사용합니다. 즉, 모든 클러스터 노드에서 열리도록 HTTPS 포트 필요 하다는 것입니다.

### <a name="proxy-considerations-with-cloud-witness"></a>프록시 부담 클라우드 미러링  
Azure 물방울 서비스에 연결 하려면 (기본 포트 443) HTTPS를 사용 하는 클라우드 감시 합니다. HTTPS 포트 프록시 네트워크를 통해 액세스할 수 있는지 확인 합니다.

## <a name="see-also"></a>참조 하십시오
- [Windows Server에서 장애 조치 클러스터링의 새로운 기능](whats-new-in-failover-clustering.md)
